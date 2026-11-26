# Presentation script for the professor meeting

Use this after reading the full [tutorial](TUTORIAL.md). The script is an opening explanation of about8–10 minutes, followed by a longer evidence discussion. Do not present every chart in the first pass.

## 1. State what was done — about one minute

> “I separated the contribution question from the benchmark-performance question. We completed54 controlled training runs across18 configurations and three seeds, plus 12 frozen diagnostic runs. We then repeated five UDA/source-only baselines across three seeds, and evaluated the recovered Best2 checkpoint. That is 69 complete top-level training jobs in the two new suites; one recovered model evaluation is not another training job.”

Show [the evidence map](assets/01_evidence_map.png).

> “The primary manuscript results, submitted supplementary tables, archived earlier controls and the two new studies are different result cohorts. I have kept their values and protocols separate.”

## 2. Answer the controller questions first — about two minutes

Show [the feedback loop](assets/04_closed_loop.png).

> “The new controller uses source-validation and unlabeled-domain statistics to create a six-value state. A6→32→25 network outputs five categorical distributions. Each chooses a factor among0.90,0.95,1,1.05,1.10. The factors are smoothed and bounded, converted to coefficient tensors, and used in all138 adaptation minibatches of that epoch.”

> “After the epoch, source-validation and unlabeled statistics provide a reward. REINFORCE updates the policy, and the next action changes the following epoch's training. We saved action probabilities, consumed coefficients, model steps, policy optimizer iterations, gradients and parameter changes. The weighted terms reconstruct the real optimized total.”

Show [the actual probability matrix](assets/05_actual_action_distribution.png) and [weighted losses](assets/06_actual_weighted_losses.png).

> “There are three independent trained-policy runs,45 optimizer updates each, for 135 actual updates. There are 135 learned action vectors; the other135 vectors in the combined count belong to the uniform-random control. The first update has zero centered reward advantage and can update entropy; the final update has no subsequent classifier epoch.”

Then make the critical distinction:

> “This directly proves the new implementation's feedback path. It does not retrospectively prove learned RL in the recovered best checkpoint: the recovered controller is deterministic and its inspected script uses target/source-test metrics. Also, the new policy controls five code coefficients that are grouped differently from the submitted equation and it does not use the paper's eight adaptation-epoch warm-up.”

If asked whether learning helps:

> “It improves the external means versus fixed weighting but loses on Acevedo and does not consistently beat random or rule-driven weighting. The implemented loop is established; general policy-learning superiority is not.”

## 3. Explain why the new ablation is scientifically more informative — about two minutes

Show [OD × self-training](assets/02_factorial_od_self.png).

> “The manuscript's cumulative removal follows one path: after self-training is removed, the next alignment difference is measured without self-training. It cannot tell us whether alignment behaves differently when self-training is present. The factorial experiment explicitly tests those combinations.”

> “On Acevedo, self-training improves F1 by 10.03 points with the registered OD view but changes it by−4.15 with RGB. The interaction is 14.18 points and is similar in all three seeds. However, the average OD effect on AML is−9.92 points, so the result is conditional, not a universal morphology benefit.”

Show [orthogonality × contrastive learning](assets/03_orthogonality_interaction.png).

> “Orthogonality improves the contrastive-on Acevedo condition by 15.20 points. But the both-on configuration is still below both-off. An interaction can be positive without making the complete combination best. This is why we need both absolute scores and contrasts.”

Add:

> “The earlier hybrid code selects a top-confidence subset, while the recovered/new code disables the hard pseudo-label term if confident coverage exceeds0.45. With four confident images in a batch of eight, these procedures behave differently. Thus nominally similar component names do not guarantee the same intervention.”

## 4. Explain the recent-method comparison — about two minutes

Show [the per-seed UDA comparison](assets/07_uda_seed_comparison.png).

> “MIC tests masked teacher–student consistency; PLUE tests uncertainty-guided source-free pseudo-labeling; DIFO tests prompt-customized foundation-model distillation; CRPL tests cluster-preserving prompt learning. They are relevant alternative mechanisms, but the ports have different source access and resources.”

> “The recovered checkpoint gives 91.40 Acevedo,72.66 Raabin and 68.71 AML macro-F1 with the predefined common input geometry and no TTA. Its Raabin result exceeds every tested baseline seed. MIC is better on Acevedo at 97.06, and PLUE has the higher AML mean at 70.18. Therefore our clearest competitive claim is Raabin transfer.”

Show [the class heatmap](assets/per_class_comparison.png).

> “The Raabin advantage over PLUE spans four classes. Monocytes remain problematic: recall is 40.60% on Raabin and 35.23% on AML. In AML,38 of 88 monocytes become basophils. The matrices identify these errors but do not prove a morphological cause.”

> “Because Proposed is one historically selected checkpoint, it has no three-seed SD and does not share the strict baseline selection protocol. I have put those differences next to the results.”

## 5. Raise the evidence reconciliation clearly — about one minute

Show [submitted versus retained supplementary values](assets/08_supplement_reconciliation.png).

> “Before drawing stronger conclusions, I need help matching the submitted higher supplementary rows to their actual runs. S1 reports full-model F1 of 91.88/83.47/73.68, while the retained earlier controlled CSV contains 81.88/68.47/69.68. Some other rows also differ. This may be another cohort, but I do not have its run-level provenance. I have preserved both sources rather than assuming or replacing values.”

> “Can we identify the corresponding experiment folders, seeds, input preprocessing, controller version and selected checkpoints? If the runs came from another server, can we obtain prediction files, histories or configuration records?”

Do not speculate about the cause of the discrepancy. A matching difference between two rows does not by itself validate their absolute numbers.

## 6. End with concrete decisions

Ask the professor to prioritize:

1. Reconcile historical table/run provenance and exact implementation descriptions.
2. Reproduce the intended proposed model in three target-label-free runs, rather than substituting a new OD/controller implementation under the old name.
3. Validate the morphology view and monocyte decision behavior on a separate development/confirmation protocol.
4. Add stronger matched source-only controls and diagnose the failing DIFO/CRPL configurations before broad method-family conclusions.

## A compact answer if interrupted

**“What have we learned?”**

> “We have a strong Raabin checkpoint result, verified implementation of a new policy-feedback loop, and controlled evidence that the component effects are conditional. We also found limits in the registered OD transformation, monocyte recall, policy-learning superiority and historical evidence provenance. The next improvement is to resolve those specific issues, not simply add more favorable comparisons.”

## What to have open on your laptop

- [Tutorial](TUTORIAL.md), especially sections5,8–10 and 15.
- [Code evidence](CODE_EVIDENCE.md).
- [Controller audit CSV](evidence/controller_audit.csv).
- [Submitted/archived table comparison](evidence/submitted_s1_vs_archived.csv).
- [Full accuracy/F1 table image](assets/comparison_table.pdf).
