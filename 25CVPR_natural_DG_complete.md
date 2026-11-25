# Natural-image domain generalization

Source-only DG accuracy (%), mean ± sample SD across three seeds after averaging all held-out domains within each seed. PACS, VLCS and OfficeHome use the recovered audited cohorts; TerraIncognita and DomainNet are from the earlier completed suite. Missing methods are not imputed and no five-dataset average is reported. Proposed source-only is not the complete UDA framework. Encoders, samplers and selection differ; see protocol matrix.

| Method | PACS | VLCS | OfficeHome | TerraIncognita | DomainNet |
| --- | --- | --- | --- | --- | --- |
| Plain ResNet50 ERM | 70.33 ± 0.86 | 75.65 ± 0.78 | 61.58 ± 0.32 | — | — |
| Proposed source-only variant | 69.02 ± 0.87 | 75.93 ± 0.20 | 44.28 ± 4.32 | 24.93 ± 0.74 | 3.74 ± 0.66 |
| CLIP-ERM | 88.61 ± 0.34 | 74.92 ± 3.19 | 75.47 ± 0.09 | 26.73 ± 4.15 | 51.93 ± 0.19 |
| VL2V-SD port | 93.90 ± 0.42 | 82.58 ± 0.50 | 83.60 ± 0.23 | 51.09 ± 0.61 | 58.38 ± 0.20 |
| Wen2025 paper-based port | 94.90 ± 0.65 | 82.71 ± 0.16 | 84.61 ± 0.10 | — | — |
| Wen distillation baseline | 93.97 ± 0.42 | — | — | — | — |

## Interpretation and learning

Wen leads PACS, VLCS and OfficeHome; VL2V-SD leads TerraIncognita and DomainNet among available methods. The proposed source-only variant is not the full UDA framework.

**Practice:** Calculate the OfficeHome gap versus plain ERM (−17.30 pp). Explain why a five-dataset average would be misleading.

See [all completed numbers](ALL_COMPLETED_NUMBERS.md) and [analysis](FINAL_ANALYSIS_AND_MANUSCRIPT_PLAN.md).
