# Working glossary and small examples

Use this when a term in the [tutorial](TUTORIAL.md) is unfamiliar. Descriptions explain the implemented ideas; they are not additional experimental findings.

| Term | Meaning in this project |
|---|---|
| Encoder/backbone | The image network that turns pixels into features; ResNet50 is one encoder family. |
| Head/classifier | The learned mapping from features to five class scores. Different heads can change results even with the same backbone. |
| Logit | A class score before softmax. A high logit alone is not a calibrated probability. |
| Softmax | Converts class scores to nonnegative probabilities that sum to one. |
| GAP | Global average pooling: average each feature channel over spatial locations. |
| GeM | Generalized-mean pooling: a power-mean aggregation that can emphasize larger activations differently from simple averaging. |
| Shared encoder | The same parameterized network processes multiple views. Two calls increase computation without creating two independent backbone parameter sets. |
| Source supervision | Learning from the known source class labels. |
| Target pseudo-label | The model's own target-class guess used as training supervision. It is not verified ground truth. |
| Confidence threshold | A filter on predicted probability. A0.95 score can still be wrong under domain shift. |
| Coverage | The fraction of examples passing a filter; high coverage does not imply high pseudo-label accuracy. |
| Stop-gradient/detach | Treat a computed value as a constant for a particular gradient calculation. It prevents the teacher distribution from changing through the student's matching loss. |
| Agreement/consistency | Encourage two predictions for the same image to match. Both predictions may agree incorrectly. |
| EMA teacher | A slowly moving average of student weights, e.g. teacher←0.9teacher+0.1student in the MIC port. It is different from an independent model trained with extra labels. |
| Contrastive objective | Pull selected related embeddings together and separate selected unrelated embeddings. Incorrectly treating same-class target samples as negatives can be harmful. |
| Memory bank/queue | Stored features/predictions from previous batches or epochs, supplying more neighbors/negative pairs than the current small batch. |
| Orthogonality | Here, a penalty on cross-branch feature correlations. It does not prove statistical independence or anatomical meaning. |
| CORAL | Compare source and target feature covariance matrices; try to reduce their difference. Matching covariances does not guarantee each class aligns correctly. |
| Domain discriminator | Predict whether a feature came from source or target. It is distinct from the five-class cell classifier. |
| CDAN | Conditional domain-adversarial adaptation: domain discrimination conditions on features and class-prediction information. It is part of the MIC classification recipe. |
| MCC | Minimum class confusion: a target-prediction regularizer used in the MIC recipe to reduce confusion between classes. |
| SAM in MIC | Sharpness-Aware Minimization, an optimizer seeking parameters with lower loss in a neighborhood. It is not Segment Anything. |
| CLIP | An image–text pretrained model with image and text embedding spaces. Class descriptions/prompts help define classification directions. |
| Prompt learning | Learn continuous prompt parameters influencing text embeddings, rather than necessarily updating the full pretrained image network. |
| Distillation | Train one model to match informative outputs of another. The teacher can also be wrong or mismatched to the task. |
| Optimal transport | Match distributions/assignments under a defined cost. In CRPL it helps impose clustering relationships between visual/text representations. |
| SGD | Parameter updates using loss gradients, often with momentum; the source-only port uses SGD. |
| Adam/AdamW | Adaptive gradient optimizers; AdamW also uses decoupled weight decay. New classifier training uses AdamW and policy optimization uses Adam. |
| Policy | A parameterized probability distribution over actions, conditioned on state. A predetermined rule table is not a learned policy-gradient network. |
| Action | In the new controller, a sampled multiplier for a loss coefficient, not a class prediction. |
| State | The six training-feedback numbers passed to the new policy. |
| Reward | A scalar proxy evaluated after training with the action. It is not final target accuracy. |
| Baseline in REINFORCE | A reference reward subtracted to reduce policy-gradient variability. It is unrelated to a comparison method such as MIC. |
| Entropy | Uncertainty of a probability distribution. Policy entropy encourages action diversity; target prediction entropy is a different quantity. |
| CKA | A measure of representational similarity. High CKA does not independently identify which features causally determine predictions. |
| Main effect | Average change from switching a factor over the specified other settings. |
| Interaction | Change in one factor's effect when another factor changes. Positive interaction does not require the full combination to be best. |
| Sample SD | Variation across independent training seeds. It is not a patient confidence interval, and cannot be estimated from one model. |

## A hypothetical policy-gradient example

Suppose an action was sampled, the resulting epoch gives reward0.95, and the moving baseline is 0.90. The advantage is+0.05. Minimizing `−0.05×log(probability of the sampled action)` tends to increase that action's probability in a comparable state. If the advantage is negative, the reward term tends to decrease its probability. Entropy regularization additionally discourages overly concentrated action distributions.

This example is illustrative. The first real logged epoch in the tutorial has zero centered advantage because of baseline initialization; its nonzero policy change can come from the entropy term.

## Why the current reward may favor source retention

The new reward allocates0.70 coefficient to source-validation F1 and 0.20 to source minimum recall. Those bounded source metrics account for 90% of its possible coefficient mass. The other10% comes from unlabeled proxies. Thus a high reward is compatible with poor external classification. This is a reason to evaluate reward design, not proof that a particular replacement reward will solve the problem.

## Averaging logits versus probabilities

In the recovered training code, pseudo-label teacher probabilities come from softmax of a weighted average of head logits. Final classification averages the two heads' softmax probabilities. These are generally different operations:

`softmax((logitsA+logitsB)/2) ≠ (softmax(logitsA)+softmax(logitsB))/2`.

Therefore “average the heads” should be described precisely when reproducing training and inference.
