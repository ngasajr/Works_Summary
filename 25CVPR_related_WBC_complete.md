# Related WBC systems

Related WBC configurations evaluated on the same750Acevedo/4339Raabin/434AML images. Accuracy/macro-F1(%), mean ± sample SD across three seeds. Training access/resources differ, so these are system-level descriptive comparisons. DoRL uses1427extra mask annotations; Cyto uses reduced inference budget; Wen is independently implemented and source-only. AllDoRLheads are reported separately rather than selecting by external performance.

| Configuration | Training information | Acevedo Acc. | F1 | Raabin Acc. | F1 | AML Acc. | F1 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Proposed | Source+unlabeled Acevedo | 83.02 ± 7.64 | 81.37 ± 10.90 | 74.55 ± 3.09 | 63.35 ± 3.17 | 65.67 ± 2.62 | 65.65 ± 2.71 |
| Wen distillation baseline | Source only | 82.93 ± 1.01 | 82.59 ± 1.10 | 69.97 ± 7.49 | 54.84 ± 3.52 | 72.12 ± 2.05 | 69.13 ± 2.11 |
| Wen2025 full port | Source only | 84.84 ± 1.81 | 84.64 ± 2.05 | 69.96 ± 10.59 | 56.69 ± 5.78 | 69.05 ± 1.04 | 66.97 ± 1.01 |
| DoRL-RF port (primary) | Source+Acevedo+extra masks | 60.04 ± 8.31 | 59.11 ± 8.87 | 40.98 ± 14.65 | 26.31 ± 7.45 | 51.31 ± 7.90 | 46.68 ± 8.39 |
| DoRL-ANN port | Source+Acevedo+extra masks | 71.51 ± 8.83 | 71.35 ± 8.74 | 42.08 ± 22.51 | 28.82 ± 12.18 | 65.59 ± 5.15 | 62.24 ± 4.69 |
| CytoDiffusion budgeted port | Source only | 49.78 ± 21.99 | 44.01 ± 25.06 | 40.86 ± 18.89 | 32.79 ± 2.54 | 47.24 ± 4.45 | 45.07 ± 6.03 |

## Interpretation and learning

The proposed model leads Raabin macro-F1 in this table, but Wen distillation leads AML macro-F1. The table includes RF and ANN; the other three DoRL heads are retained in the all-numbers document.

**Practice:** Compare AML accuracy and F1 for proposed and ANN. Explain why extra segmentation masks and unlabeled target access matter.

See [all completed numbers](ALL_COMPLETED_NUMBERS.md) and [analysis](FINAL_ANALYSIS_AND_MANUSCRIPT_PLAN.md).
