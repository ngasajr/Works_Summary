# Audited implementation excerpts

These are code snapshots/excerpts, not instructions to execute. Original best files are unchanged.

## best2_contribution_study_20261125/code/study.py

```text
28: def od_view(x):
29:  """Explicit prospective OD projection, not asserted to be the saved model's transform."""
30:  od=-tf.math.log(tf.clip_by_value(tf.cast(x,tf.float32)/255.,0.,1.)+1.e-6)
31:  h=tf.math.l2_normalize(tf.constant([.650,.704,.286]));e=tf.math.l2_normalize(tf.constant([.072,.990,.105]))
32:  z=.8*tf.tensordot(od,h,axes=1)+.2*tf.tensordot(od,e,axes=1)
33:  mean,var=tf.nn.moments(z,[1,2],keepdims=True);z=(z-mean)/tf.sqrt(var+1.e-6)
34:  lo=tf.reduce_min(z,[1,2],keepdims=True);hi=tf.reduce_max(z,[1,2],keepdims=True)
35:  z=255.*tf.math.divide_no_nan(z-lo,hi-lo)
36:  return tf.repeat(z[...,None],3,-1)
37: 
38: class Augmentation(core.MedicalAugmentation):
39:  def call(self,x,training=False):
40:   with tf.device('/CPU:0'):return super().call(x,training=training)
```

```text
50:  keys=['classification','adversarial','orthogonality','alignment','morphology']
51:  bounds=[(.8,3.),(.001,.35),(.001,.1),(.005,.5),(0.,.2)]
52:  def __init__(self,kind,morph):
53:   self.kind=kind;self.weights=dict(zip(self.keys,[1.,.04,.012,.07,morph]));self.pending=None;self.baseline=None;self.updates=0;self.samples=0
54:   self.heuristic=core.AdaptiveLossController(morph);self.factors=np.array([.9,.95,1.,1.05,1.1],np.float32)
55:   self.policy=tf.keras.Sequential([tf.keras.layers.InputLayer(input_shape=(6,)),tf.keras.layers.Dense(32,activation='tanh'),tf.keras.layers.Dense(25)])
56:   self.opt=tf.keras.optimizers.Adam(3e-4)
57:  def state_reward(self,f1,rec,stats):
58:   conf=1-min(1.,2*abs(stats.get('domain_accuracy',.5)-.5));dist=np.exp(-max(0.,stats.get('alignment_loss',0.)))
59:   cov=stats.get('pseudo_label_coverage',0.);agree=np.exp(-max(0.,stats.get('target_view_agreement_loss',0.)))
60:   state=np.array([f1,rec,conf,dist,cov,agree],np.float32)
61:   # No target accuracy surrogate is described as a measured target accuracy.
62:   reward=.7*f1+.2*rec+.05*conf+.025*dist+.025*agree
63:   return state,float(reward)
64:  def act(self,state):
65:   if self.kind not in ['learned','random']:return None
66:   logits=tf.reshape(self.policy(state[None],training=False),(5,5))
67:   if self.kind=='random':logits=tf.zeros_like(logits)
68:   probs=tf.nn.softmax(logits).numpy();actions=tf.random.categorical(logits,1)[:,0].numpy();before=self.weights.copy()
69:   for j,k in enumerate(self.keys):self.weights[k]=float(np.clip(self.weights[k]*(.6+.4*self.factors[actions[j]]),*self.bounds[j]))
70:   self.samples+=1;self.pending=(state.copy(),actions.copy());return {'state':state.tolist(),'distribution':probs.tolist(),'actions':actions.tolist(),'multipliers':self.factors[actions].tolist(),'weights_before':before,'weights_after':self.weights.copy()}
71:  def observe(self,f1,rec,stats):
72:   state,reward=self.state_reward(f1,rec,stats);row={'reward':reward,'theta_updates_before':self.updates,'policy_optimizer_iteration_before':int(self.opt.iterations.numpy())}
73:   if self.kind=='learned' and self.pending is not None:
74:    oldstate,actions=self.pending;b=reward if self.baseline is None else self.baseline;adv=reward-b
75:    before=[v.numpy().copy() for v in self.policy.trainable_variables]
76:    with tf.GradientTape() as tape:
77:     logits=tf.reshape(self.policy(oldstate[None],training=True),(5,5));lp=tf.nn.log_softmax(logits)
78:     selected=tf.gather_nd(lp,np.stack([np.arange(5),actions],1));entropy=-tf.reduce_sum(tf.exp(lp)*lp)
79:     loss=-tf.reduce_sum(selected)*tf.stop_gradient(tf.constant(adv,tf.float32))-.01*entropy
80:    gradients=tape.gradient(loss,self.policy.trainable_variables)
81:    for g in gradients:tf.debugging.assert_all_finite(g,'policy gradient')
82:    self.opt.apply_gradients(zip(gradients,self.policy.trainable_variables));self.updates+=1
83:    delta=np.sqrt(sum(np.square(v.numpy()-w).sum() for v,w in zip(self.policy.trainable_variables,before)))
84:    row.update(policy_loss=float(loss),advantage=adv,baseline=b,entropy=float(entropy),gradient_norm=float(tf.linalg.global_norm(gradients)),parameter_delta_l2=float(delta))
85:   self.baseline=reward if self.baseline is None else .9*self.baseline+.1*reward
86:   if self.kind=='heuristic':
87:    self.heuristic.weights=self.weights.copy()
88:    self.weights=self.heuristic.update(source_macro_f1=f1,target_macro_f1=f1,source_min_recall=rec,target_min_recall=rec,domain_acc=stats.get('domain_accuracy',.5),feature_distance=stats.get('alignment_loss',0.),macro_f1_gap=0.)
89:    row['heuristic_inputs']='source validation metrics occupy both historical performance slots; no target labels'
90:   row.update(theta_updates_after=self.updates,policy_optimizer_iteration_after=int(self.opt.iterations.numpy()),weights=self.weights.copy());return state,row
91: 
92: class Trainer(model.TwoViewDomainAdaptationTrainer):
93:  def __init__(self,c,out,case):
94:   self.case=case;super().__init__(c,out);self.encoder_a.augmentation=Augmentation(c.use_vertical_flip)
95:   if case['view']=='single':self.classifier_b=self.classifier_a
96:  def _encode_a(self,x,training):
97:   view=self.case['view']
98:   if view in ['od','duplicate_od']:x=od_view(x)
99:   elif view=='gray':x=tf.image.grayscale_to_rgb(tf.image.rgb_to_grayscale(x))
100:   features=self.encoder_a(x,training=training)
101:   if view=='single':self._single_features=features
```

## best2_contribution_study_20261125/code/recovered_model.py

```text
420:             pseudo_label_loss = tf.constant(0.0, dtype=tf.float32)
421:             soft_pseudo_label_loss = tf.constant(0.0, dtype=tf.float32)
422:             pseudo_view_agreement_loss = tf.constant(0.0, dtype=tf.float32)
423:             pseudo_label_coverage = tf.constant(0.0, dtype=tf.float32)
424:             if self.config.use_pseudo_labeling:
425:                 teacher_probs = tf.stop_gradient(tf.nn.softmax(target_logits_mean, axis=-1))
426:                 pseudo_confidence = tf.reduce_max(teacher_probs, axis=-1)
427:                 pseudo_labels = tf.argmax(teacher_probs, axis=-1, output_type=tf.int32)
428:                 pseudo_mask = tf.cast(pseudo_confidence >= self.config.pseudo_label_confidence, tf.float32)
429:                 pseudo_losses_a = tf.keras.losses.sparse_categorical_crossentropy(
430:                     pseudo_labels,
431:                     tf.cast(target_logits_a, tf.float32),
432:                     from_logits=True,
433:                 )
434:                 pseudo_losses_b = tf.keras.losses.sparse_categorical_crossentropy(
435:                     pseudo_labels,
436:                     tf.cast(target_logits_b, tf.float32),
437:                     from_logits=True,
438:                 )
439:                 pseudo_losses = 0.5 * (pseudo_losses_a + pseudo_losses_b)
440:                 pseudo_label_loss = tf.reduce_sum(pseudo_losses * pseudo_mask) / tf.maximum(
441:                     tf.reduce_sum(pseudo_mask),
442:                     1.0,
443:                 )
444:                 pseudo_label_coverage = tf.reduce_mean(pseudo_mask)
445:                 coverage_gate = tf.cast(
446:                     pseudo_label_coverage <= self.config.max_pseudo_label_coverage,
447:                     tf.float32,
448:                 )
449:                 pseudo_label_loss = pseudo_label_loss * coverage_gate
450:                 soft_a = tf.keras.losses.categorical_crossentropy(
451:                     teacher_probs,
452:                     tf.cast(target_logits_a, tf.float32),
453:                     from_logits=True,
454:                 )
455:                 soft_b = tf.keras.losses.categorical_crossentropy(
456:                     teacher_probs,
457:                     tf.cast(target_logits_b, tf.float32),
458:                     from_logits=True,
459:                 )
460:                 soft_weights = tf.stop_gradient(tf.square(pseudo_confidence))
461:                 soft_pseudo_label_loss = tf.reduce_sum(0.5 * (soft_a + soft_b) * soft_weights) / tf.maximum(
462:                     tf.reduce_sum(soft_weights),
463:                     1.0,
464:                 )
465:                 pseudo_view_agreement_loss = target_agreement * tf.stop_gradient(pseudo_label_coverage)
```

## Best2_rl_two_view_EfficientNet_best_single_encoder_raabin_aml_external/rl_two_view_orthogonal_domain_adaptation_wbc.py

```text
730:             trainer,
731:             datasets["source_test"],
732:             class_names,
733:             "source_test",
734:         )
735:         source_val_metrics, _, _ = evaluate_two_view_classifier(
736:             trainer,
737:             datasets["source_val"],
738:             class_names,
739:             "source_val",
740:         )
741:         target_metrics, _, _ = evaluate_two_view_classifier(
742:             trainer,
743:             datasets["target_labeled_eval"],
744:             class_names,
745:             "target_eval",
746:         )
747:         batch_mean = mean_metrics(batch_records)
748:         source_min_recall = min_class_recall(source_metrics, class_names)
749:         target_min_recall = min_class_recall(target_metrics, class_names)
750:         accuracy_gap = source_metrics["accuracy"] - target_metrics["accuracy"]
751:         macro_f1_gap = source_metrics["macro_f1"] - target_metrics["macro_f1"]
752: 
753:         if trainer.config.use_rl_controller:
754:             weights = trainer.controller.update(
755:                 source_macro_f1=source_metrics["macro_f1"],
756:                 target_macro_f1=target_metrics["macro_f1"],
757:                 source_min_recall=source_min_recall,
758:                 target_min_recall=target_min_recall,
759:                 domain_acc=batch_mean.get("domain_accuracy", 1.0),
760:                 feature_distance=batch_mean.get("alignment_loss", 0.0),
761:                 macro_f1_gap=macro_f1_gap,
762:             )
763:         else:
764:             weights = trainer.controller.weights.copy()
765: 
766:         if trainer.config.checkpoint_selection == "target_balanced":
767:             selection_score = (
768:                 0.34 * source_metrics["macro_f1"]
769:                 + 0.44 * target_metrics["macro_f1"]
770:                 + 0.12 * min(source_min_recall, target_min_recall)
771:                 + 0.04 * (1.0 - batch_mean.get("target_view_agreement_loss", 0.0))
772:                 - 0.10 * abs(macro_f1_gap)
773:             )
774:         else:
775:             domain_confusion = 1.0 - min(1.0, 2.0 * abs(batch_mean.get("domain_accuracy", 1.0) - 0.5))
776:             source_generalization = 1.0 - min(1.0, abs(source_val_metrics["macro_f1"] - source_metrics["macro_f1"]))
777:             feature_stability = 1.0 / (1.0 + 100.0 * max(0.0, batch_mean.get("alignment_loss", 0.0)))
778:             selection_score = (
779:                 0.50 * source_val_metrics["macro_f1"]
```
