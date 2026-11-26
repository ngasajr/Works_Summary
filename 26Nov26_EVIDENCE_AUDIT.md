# Evidence questions for the meeting

This is a reconciliation list, not a claim about why any discrepancy occurred. The submitted PDFs and local artifacts are preserved separately. The tutorial's new experimental numbers come from the completed suites; submitted historical values are explicitly marked as reported.

| Question | Submitted statement/value | Available record | Needed resolution |
|---|---|---|---|
| Supplement S1 full model |91.88/83.47/73.68 F1|Archived81.88/68.47/69.68|Matching run-level metrics/predictions/configs for the submitted row|
| Supplement S2 full grayscale |72.52/51.22/51.09|Archived62.52/41.22/41.09|Matching diagnostic panel and checkpoint files|
| Supplement S4 EfficientNet full |91.58/81.30/77.04|Archived81.58/66.30/73.04|Which backbone cohort generated the submitted numbers?|
| Main Table5 Proposed |Three-seed 90.57/82.72/74.66|Earlier retained recent suite81.37/63.35/65.65; today's single checkpoint91.40/72.66/68.71|Exact three-seed provenance; do not mix these cohorts|
| Five policy groups in main Eq.1 |Classification/representation/domain/view/self|New code controls classification/adversarial/orthogonality/alignment/contrastive|Identify equation-to-code mapping for each run|
| Eight adaptation warm-up epochs |Policy activated after warm-up|New policy starts at epoch 1; source backbone also has a different eight-epoch warm-up|Report each schedule separately|
| Strict label-free target feedback |Method excludes target labels from training/selection|Recovered script supplies target/source-test metrics to its deterministic controller and selector|Which primary runs actually follow strict UDA?|
| Historical learned RL |Policy-training description|Recovered Best2 controller is deterministic; new policy audit is separate|Historical optimizer/action/parameter records if a different learned-policy checkpoint was used|
| OD morphology view |Submitted OD emphasis|New operator has explicit registered choices; recovered path lacks verified historical OD transform|Recover exact operator/constants and identify checkpoints trained with it|
| Pseudo-label coverage |“Cap45%” shorthand|Earlier hybrid keeps top-k; recovered/new code gates the whole hard term|Describe the actual implementation; don't treat them as identical|

## How to address this constructively

Ask for the experiment folder, seed identifiers, configuration JSON, data membership/geometry, selected epoch and per-image predictions for the disputed rows. If available records correspond to a different legitimate cohort, label it explicitly. If they do not support a reported value, agree how to correct/document the issue through the appropriate manuscript process. No submitted PDF has been edited by this tutorial task.

[Cell-by-cell S1 comparison](evidence/submitted_s1_vs_archived.csv) · [PDF source hashes](evidence/source_pdf_sha256.json) · [Code evidence](CODE_EVIDENCE.md)
