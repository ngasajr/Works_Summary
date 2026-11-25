# All completed numbers

## Reading the tables

Accuracy and macro-F1 are percentages. SD is sample standard deviation where available. `NaN` means unavailable, not zero. The variation unit distinguishes training seeds, batch permutations and deterministic fits. Do not pool different protocols.

## recent_UDA

| method | domain | accuracy | accuracy_sd | macro_f1 | macro_f1_sd | n | variation_unit | target_labels |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| crpl | acevedo | 52.22 | 1.84 | 50.71 | 1.84 | 3 | training seeds | 0 |
| crpl | aml | 38.17 | 2.97 | 36.45 | 3.05 | 3 | training seeds | 0 |
| crpl | raabin | 45.59 | 5.97 | 34.41 | 3.08 | 3 | training seeds | 0 |
| crpl | source_test | 63.22 | 6.79 | 62.11 | 8.13 | 3 | training seeds | 0 |
| difo | acevedo | 59.51 | 4.20 | 54.12 | 4.74 | 3 | training seeds | 0 |
| difo | aml | 31.11 | 8.24 | 23.85 | 12.64 | 3 | training seeds | 0 |
| difo | raabin | 20.60 | 2.23 | 16.20 | 1.94 | 3 | training seeds | 0 |
| difo | source_test | 48.83 | 0.98 | 46.80 | 1.82 | 3 | training seeds | 0 |
| mic | acevedo | 97.07 | 1.96 | 97.06 | 1.97 | 3 | training seeds | 0 |
| mic | aml | 59.45 | 18.24 | 58.02 | 19.82 | 3 | training seeds | 0 |
| mic | raabin | 50.47 | 22.72 | 28.55 | 13.92 | 3 | training seeds | 0 |
| mic | source_test | 99.29 | 0.76 | 99.29 | 0.84 | 3 | training seeds | 0 |
| ours | acevedo | 83.02 | 7.64 | 81.37 | 10.90 | 3 | training seeds | 0 |
| ours | aml | 65.67 | 2.62 | 65.65 | 2.71 | 3 | training seeds | 0 |
| ours | raabin | 74.55 | 3.09 | 63.35 | 3.17 | 3 | training seeds | 0 |
| ours | source_test | 98.58 | 0.46 | 98.58 | 0.38 | 3 | training seeds | 0 |
| plue | acevedo | 92.71 | 1.28 | 92.62 | 1.26 | 3 | training seeds | 0 |
| plue | aml | 72.89 | 1.73 | 70.18 | 3.96 | 3 | training seeds | 0 |
| plue | raabin | 75.24 | 1.84 | 59.47 | 1.87 | 3 | training seeds | 0 |
| plue | source_test | 90.27 | 0.30 | 90.45 | 0.56 | 3 | training seeds | 0 |
| ours_source | acevedo | 85.60 | 4.73 | 85.54 | 5.00 | 3 | training seeds | 0 |
| ours_source | aml | 57.76 | 6.46 | 58.20 | 7.27 | 3 | training seeds | 0 |
| ours_source | raabin | 77.56 | 10.72 | 66.14 | 10.74 | 3 | training seeds | 0 |
| ours_source | source_test | 99.19 | 0.18 | 99.21 | 0.14 | 3 | training seeds | 0 |

## recovered_natural_source_only_DG

| method | domain | accuracy | accuracy_sd | macro_f1 | macro_f1_sd | n | variation_unit | target_labels |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| clip_erm | OfficeHome | 75.47 | 0.09 | 73.50 | 0.15 | 3 | training seeds | 0 |
| ours_source_only_DG | OfficeHome | 44.28 | 4.32 | 39.73 | 5.40 | 3 | training seeds | 0 |
| plain_erm | OfficeHome | 61.58 | 0.32 | 59.77 | 0.52 | 3 | training seeds | 0 |
| vl2v_sd | OfficeHome | 83.60 | 0.23 | 82.30 | 0.25 | 3 | training seeds | 0 |
| wen2025 | OfficeHome | 84.61 | 0.10 | 83.47 | 0.12 | 3 | training seeds | 0 |
| clip_erm | PACS | 88.61 | 0.34 | 89.49 | 0.41 | 3 | training seeds | 0 |
| ours_source_only_DG | PACS | 69.02 | 0.87 | 67.41 | 1.26 | 3 | training seeds | 0 |
| plain_erm | PACS | 70.33 | 0.86 | 69.16 | 1.63 | 3 | training seeds | 0 |
| vl2v_sd | PACS | 93.90 | 0.42 | 94.72 | 0.44 | 3 | training seeds | 0 |
| wen2025 | PACS | 94.90 | 0.65 | 95.72 | 0.56 | 3 | training seeds | 0 |
| wen_base | PACS | 93.97 | 0.42 | 94.79 | 0.36 | 3 | training seeds | 0 |
| clip_erm | VLCS | 74.92 | 3.19 | 67.19 | 3.93 | 3 | training seeds | 0 |
| ours_source_only_DG | VLCS | 75.93 | 0.20 | 69.49 | 1.07 | 3 | training seeds | 0 |
| plain_erm | VLCS | 75.65 | 0.78 | 69.33 | 0.44 | 3 | training seeds | 0 |
| vl2v_sd | VLCS | 82.58 | 0.50 | 79.31 | 1.18 | 3 | training seeds | 0 |
| wen2025 | VLCS | 82.71 | 0.16 | 79.74 | 0.45 | 3 | training seeds | 0 |

## DoRL_extra_mask_supervision

| method | domain | accuracy | accuracy_sd | macro_f1 | macro_f1_sd | n | variation_unit | target_labels |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| dorl_ann | acevedo | 71.51 | 8.83 | 71.35 | 8.74 | 3 | training seeds | 0 |
| dorl_ann | raabin | 42.08 | 22.51 | 28.82 | 12.18 | 3 | training seeds | 0 |
| dorl_ann | aml | 65.59 | 5.15 | 62.24 | 4.69 | 3 | training seeds | 0 |
| dorl_ann | source_test | 95.74 | 1.39 | 95.84 | 1.39 | 3 | training seeds | 0 |
| dorl_lr | acevedo | 65.16 | 21.70 | 64.43 | 22.28 | 3 | training seeds | 0 |
| dorl_lr | raabin | 29.71 | 23.09 | 21.67 | 14.52 | 3 | training seeds | 0 |
| dorl_lr | aml | 65.51 | 7.85 | 61.53 | 8.62 | 3 | training seeds | 0 |
| dorl_lr | source_test | 95.95 | 1.15 | 96.01 | 1.21 | 3 | training seeds | 0 |
| dorl_rf | acevedo | 60.04 | 8.31 | 59.11 | 8.87 | 3 | training seeds | 0 |
| dorl_rf | raabin | 40.98 | 14.65 | 26.31 | 7.45 | 3 | training seeds | 0 |
| dorl_rf | aml | 51.31 | 7.90 | 46.68 | 8.39 | 3 | training seeds | 0 |
| dorl_rf | source_test | 84.70 | 2.07 | 85.30 | 2.03 | 3 | training seeds | 0 |
| dorl_svm_linear | acevedo | 63.96 | 17.89 | 63.16 | 17.92 | 3 | training seeds | 0 |
| dorl_svm_linear | raabin | 36.11 | 28.20 | 25.56 | 15.69 | 3 | training seeds | 0 |
| dorl_svm_linear | aml | 63.21 | 8.49 | 58.12 | 9.25 | 3 | training seeds | 0 |
| dorl_svm_linear | source_test | 96.66 | 1.22 | 96.83 | 1.25 | 3 | training seeds | 0 |
| dorl_svm_poly | acevedo | 58.98 | 6.05 | 57.02 | 7.69 | 3 | training seeds | 0 |
| dorl_svm_poly | raabin | 38.15 | 10.52 | 26.59 | 5.37 | 3 | training seeds | 0 |
| dorl_svm_poly | aml | 48.69 | 4.20 | 45.49 | 4.39 | 3 | training seeds | 0 |
| dorl_svm_poly | source_test | 80.65 | 3.35 | 81.73 | 3.34 | 3 | training seeds | 0 |

## Wen_source_only

| method | domain | accuracy | accuracy_sd | macro_f1 | macro_f1_sd | n | variation_unit | target_labels |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| wen2025 | acevedo | 84.84 | 1.81 | 84.64 | 2.05 | 3 | training seeds | 0 |
| wen2025 | raabin | 69.96 | 10.59 | 56.69 | 5.78 | 3 | training seeds | 0 |
| wen2025 | aml | 69.05 | 1.04 | 66.97 | 1.01 | 3 | training seeds | 0 |
| wen2025 | source_test | 99.29 | 0.35 | 99.21 | 0.39 | 3 | training seeds | 0 |
| wen_base | acevedo | 82.93 | 1.01 | 82.59 | 1.10 | 3 | training seeds | 0 |
| wen_base | raabin | 69.97 | 7.49 | 54.84 | 3.52 | 3 | training seeds | 0 |
| wen_base | aml | 72.12 | 2.05 | 69.13 | 2.11 | 3 | training seeds | 0 |
| wen_base | source_test | 99.19 | 0.18 | 99.09 | 0.19 | 3 | training seeds | 0 |

## Cyto_source_only_budget_port

| method | domain | accuracy | accuracy_sd | macro_f1 | macro_f1_sd | n | variation_unit | target_labels |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| cytodiffusion | acevedo | 49.78 | 21.99 | 44.01 | 25.06 | 3 | training seeds | 0 |
| cytodiffusion | aml | 47.24 | 4.45 | 45.07 | 6.03 | 3 | training seeds | 0 |
| cytodiffusion | raabin | 40.86 | 18.89 | 32.79 | 2.54 | 3 | training seeds | 0 |
| cytodiffusion | source_test | 93.31 | 0.61 | 92.67 | 0.50 | 3 | training seeds | 0 |

## StatA_test_time

| method | domain | accuracy | accuracy_sd | macro_f1 | macro_f1_sd | n | variation_unit | target_labels |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| clip_zero_shot | acevedo | 21.73 | NaN | 10.66 | NaN | 1 | single deterministic fit | 0 |
| clip_zero_shot | aml | 19.59 | NaN | 8.88 | NaN | 1 | single deterministic fit | 0 |
| clip_zero_shot | raabin | 9.40 | NaN | 7.26 | NaN | 1 | single deterministic fit | 0 |
| clip_zero_shot | source_test | 32.22 | NaN | 14.90 | NaN | 1 | single deterministic fit | 0 |
| stata_frozen_acevedo_gaussian | acevedo | 19.07 | NaN | 7.81 | NaN | 1 | single deterministic fit | 0 |
| stata_frozen_acevedo_gaussian | aml | 22.58 | NaN | 14.04 | NaN | 1 | single deterministic fit | 0 |
| stata_frozen_acevedo_gaussian | raabin | 2.21 | NaN | 1.28 | NaN | 1 | single deterministic fit | 0 |
| stata_frozen_acevedo_gaussian | source_test | 25.23 | NaN | 13.50 | NaN | 1 | single deterministic fit | 0 |
| stata_full_domain | acevedo | 18.93 | NaN | 7.29 | NaN | 1 | single deterministic fit | 0 |
| stata_per_domain_batch64 | acevedo | 20.04 | 0.08 | 6.76 | 0.15 | 3 | batch permutations | 0 |
| stata_per_domain_batch64 | aml | 18.82 | 0.13 | 7.31 | 0.29 | 3 | batch permutations | 0 |
| stata_per_domain_batch64 | raabin | 7.47 | 0.02 | 2.85 | 0.10 | 3 | batch permutations | 0 |
| stata_per_domain_batch64 | source_test | 31.00 | 0.00 | 9.47 | 0.00 | 3 | batch permutations | 0 |

## CLIP_source_anchor_diagnostics

| method | domain | accuracy | accuracy_sd | macro_f1 | macro_f1_sd | n | variation_unit | target_labels |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| clip_source_logistic | source_test | 70.82 | NaN | 67.48 | NaN | 1 | single deterministic fit | 0 |
| clip_source_prototype | source_test | 71.43 | NaN | 70.73 | NaN | 1 | single deterministic fit | 0 |
| stata_source_anchor_frozen | source_test | 44.38 | NaN | 44.03 | NaN | 1 | single deterministic fit | 0 |
| clip_source_logistic | acevedo | 47.33 | NaN | 41.62 | NaN | 1 | single deterministic fit | 0 |
| clip_source_prototype | acevedo | 45.47 | NaN | 43.93 | NaN | 1 | single deterministic fit | 0 |
| stata_source_anchor_frozen | acevedo | 41.87 | NaN | 41.91 | NaN | 1 | single deterministic fit | 0 |
| stata_source_anchor_target_graph | acevedo | 41.33 | NaN | 41.27 | NaN | 1 | single deterministic fit | 0 |
| clip_source_logistic | raabin | 58.47 | NaN | 35.96 | NaN | 1 | single deterministic fit | 0 |
| clip_source_prototype | raabin | 53.15 | NaN | 37.84 | NaN | 1 | single deterministic fit | 0 |
| stata_source_anchor_frozen | raabin | 6.75 | NaN | 4.93 | NaN | 1 | single deterministic fit | 0 |
| clip_source_logistic | aml | 44.70 | NaN | 40.52 | NaN | 1 | single deterministic fit | 0 |
| clip_source_prototype | aml | 33.87 | NaN | 30.06 | NaN | 1 | single deterministic fit | 0 |
| stata_source_anchor_frozen | aml | 30.41 | NaN | 24.60 | NaN | 1 | single deterministic fit | 0 |

## KDE_two_episode_100labels

| method | domain | accuracy | accuracy_sd | macro_f1 | macro_f1_sd | n | variation_unit | target_labels |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| source_head | acevedo | 60.97 | 4.11 | 59.72 | 5.23 | 3 | training seeds | 0 |
| source_head | aml | 37.86 | 1.53 | 31.78 | 2.44 | 3 | training seeds | 0 |
| source_head | raabin | 40.94 | 4.63 | 32.21 | 5.62 | 3 | training seeds | 0 |
| source_head | source_test | 84.30 | 5.21 | 83.73 | 5.71 | 3 | training seeds | 0 |
| target_finetune | acevedo | 77.08 | 2.82 | 76.64 | 3.46 | 3 | training seeds | 100 |
| target_finetune | aml | 43.55 | 5.42 | 40.88 | 6.10 | 3 | training seeds | 100 |
| target_finetune | raabin | 40.38 | 17.40 | 25.07 | 11.16 | 3 | training seeds | 100 |
| target_finetune | source_test | 79.23 | 4.89 | 78.94 | 5.07 | 3 | training seeds | 100 |
| target_kde_kd | acevedo | 73.08 | 4.15 | 73.06 | 4.36 | 3 | training seeds | 100 |
| target_kde_kd | aml | 39.78 | 4.16 | 34.75 | 5.41 | 3 | training seeds | 100 |
| target_kde_kd | raabin | 45.31 | 18.63 | 28.37 | 9.67 | 3 | training seeds | 100 |
| target_kde_kd | source_test | 84.09 | 5.17 | 83.31 | 5.42 | 3 | training seeds | 100 |

## common_650_holdout

| method | domain | accuracy | accuracy_sd | macro_f1 | macro_f1_sd | n | variation_unit | target_labels |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ours | acevedo | NaN | NaN | 81.31 | 10.86 | 3 | training seeds | 0 |
| mic | acevedo | NaN | NaN | 97.02 | 1.82 | 3 | training seeds | 0 |
| plue | acevedo | NaN | NaN | 92.10 | 1.30 | 3 | training seeds | 0 |
| wbc | acevedo | NaN | NaN | 96.31 | 0.41 | 3 | training seeds | 100 |

## WBC_source_only_DG

| method | domain | accuracy | accuracy_sd | macro_f1 | macro_f1_sd | n | variation_unit | target_labels |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| clip_erm | acevedo | 75.24 | 5.79 | 75.08 | 5.56 | 3 | training seeds | 0 |
| clip_erm | aml | 68.20 | 0.61 | 65.41 | 0.33 | 3 | training seeds | 0 |
| clip_erm | raabin | 29.74 | 0.58 | 21.18 | 0.64 | 3 | training seeds | 0 |
| clip_erm | source_test | 98.78 | 0.61 | 98.60 | 0.70 | 3 | training seeds | 0 |
| ours_source_only_DG | acevedo | 78.09 | 7.75 | 77.59 | 8.67 | 3 | training seeds | 0 |
| ours_source_only_DG | aml | 55.15 | 10.76 | 55.42 | 10.50 | 3 | training seeds | 0 |
| ours_source_only_DG | raabin | 61.41 | 8.31 | 52.66 | 8.83 | 3 | training seeds | 0 |
| ours_source_only_DG | source_test | 98.28 | 0.35 | 98.35 | 0.19 | 3 | training seeds | 0 |
| vl2v_sd | acevedo | 82.36 | 0.20 | 81.89 | 0.31 | 3 | training seeds | 0 |
| vl2v_sd | aml | 71.58 | 2.59 | 68.53 | 1.91 | 3 | training seeds | 0 |
| vl2v_sd | raabin | 66.60 | 7.97 | 53.33 | 6.33 | 3 | training seeds | 0 |
| vl2v_sd | source_test | 99.29 | 0.46 | 99.18 | 0.56 | 3 | training seeds | 0 |

## natural_source_only_DG

| method | domain | accuracy | accuracy_sd | macro_f1 | macro_f1_sd | n | variation_unit | target_labels |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| clip_erm | DomainNet | 51.93 | 0.19 | NaN | NaN | 3 | training seeds | 0 |
| clip_erm | TerraIncognita | 26.73 | 4.15 | NaN | NaN | 3 | training seeds | 0 |
| ours_source_only_DG | DomainNet | 3.74 | 0.66 | NaN | NaN | 3 | training seeds | 0 |
| ours_source_only_DG | TerraIncognita | 24.93 | 0.74 | NaN | NaN | 3 | training seeds | 0 |
| vl2v_sd | DomainNet | 58.38 | 0.20 | NaN | NaN | 3 | training seeds | 0 |
| vl2v_sd | TerraIncognita | 51.09 | 0.61 | NaN | NaN | 3 | training seeds | 0 |

## historical_local_1view

| method | domain | accuracy | accuracy_sd | macro_f1 | macro_f1_sd | n | variation_unit | target_labels |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| coral | acevedo | 76.93 | 11.75 | 76.39 | 12.87 | 3 | training seeds | 0 |
| coral | aml | 53.53 | 10.34 | 52.83 | 12.00 | 3 | training seeds | 0 |
| coral | raabin | 71.32 | 4.41 | 57.81 | 5.88 | 3 | training seeds | 0 |
| coral | source_test | 98.68 | 0.98 | 98.71 | 0.99 | 3 | training seeds | 0 |
| dann | acevedo | 33.87 | 3.19 | 23.41 | 8.53 | 3 | training seeds | 0 |
| dann | aml | 33.18 | 12.79 | 26.52 | 16.16 | 3 | training seeds | 0 |
| dann | raabin | 14.47 | 10.78 | 21.99 | 15.90 | 3 | training seeds | 0 |
| dann | source_test | 70.01 | 26.08 | 69.76 | 25.41 | 3 | training seeds | 0 |
| mcd | acevedo | 43.38 | 31.17 | 36.02 | 37.76 | 3 | training seeds | 0 |
| mcd | aml | 46.39 | 19.76 | 43.01 | 24.26 | 3 | training seeds | 0 |
| mcd | raabin | 52.75 | 40.88 | 38.79 | 31.64 | 3 | training seeds | 0 |
| mcd | source_test | 98.38 | 0.70 | 98.48 | 0.62 | 3 | training seeds | 0 |
| ours | acevedo | 76.22 | 8.71 | 73.92 | 10.72 | 3 | training seeds | 0 |
| ours | aml | 62.98 | 0.27 | 63.13 | 0.29 | 3 | training seeds | 0 |
| ours | raabin | 70.77 | 12.56 | 62.30 | 4.99 | 3 | training seeds | 0 |
| ours | source_test | 97.87 | 1.32 | 97.95 | 1.13 | 3 | training seeds | 0 |
| source | acevedo | 78.18 | 2.90 | 77.49 | 3.03 | 3 | training seeds | 0 |
| source | aml | 56.91 | 8.41 | 57.12 | 9.15 | 3 | training seeds | 0 |
| source | raabin | 71.98 | 6.69 | 61.50 | 6.36 | 3 | training seeds | 0 |
| source | source_test | 98.78 | 0.53 | 98.89 | 0.49 | 3 | training seeds | 0 |

## historical_local_5view

| method | domain | accuracy | accuracy_sd | macro_f1 | macro_f1_sd | n | variation_unit | target_labels |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| coral | acevedo | 78.18 | 11.20 | 77.67 | 12.15 | 3 | training seeds | 0 |
| coral | aml | 54.45 | 10.84 | 53.71 | 12.34 | 3 | training seeds | 0 |
| coral | raabin | 70.99 | 4.77 | 57.65 | 7.27 | 3 | training seeds | 0 |
| coral | source_test | 98.89 | 0.88 | 98.86 | 0.89 | 3 | training seeds | 0 |
| dann | acevedo | 34.36 | 2.48 | 23.56 | 7.97 | 3 | training seeds | 0 |
| dann | aml | 33.95 | 13.37 | 26.86 | 17.06 | 3 | training seeds | 0 |
| dann | raabin | 13.78 | 10.29 | 21.74 | 15.61 | 3 | training seeds | 0 |
| dann | source_test | 71.12 | 26.62 | 70.97 | 25.91 | 3 | training seeds | 0 |
| mcd | acevedo | 44.00 | 32.54 | 36.65 | 39.16 | 3 | training seeds | 0 |
| mcd | aml | 46.62 | 21.63 | 42.72 | 26.90 | 3 | training seeds | 0 |
| mcd | raabin | 54.23 | 42.17 | 40.02 | 32.81 | 3 | training seeds | 0 |
| mcd | source_test | 99.09 | 0.30 | 99.11 | 0.33 | 3 | training seeds | 0 |
| ours | acevedo | 77.47 | 8.53 | 75.15 | 10.65 | 3 | training seeds | 0 |
| ours | aml | 64.44 | 1.31 | 64.66 | 0.54 | 3 | training seeds | 0 |
| ours | raabin | 69.61 | 13.35 | 61.74 | 5.21 | 3 | training seeds | 0 |
| ours | source_test | 98.78 | 0.80 | 98.79 | 0.77 | 3 | training seeds | 0 |
| source | acevedo | 79.73 | 2.79 | 79.03 | 3.09 | 3 | training seeds | 0 |
| source | aml | 58.53 | 9.33 | 58.66 | 9.86 | 3 | training seeds | 0 |
| source | raabin | 71.31 | 6.57 | 60.80 | 7.06 | 3 | training seeds | 0 |
| source | source_test | 99.29 | 0.35 | 99.33 | 0.26 | 3 | training seeds | 0 |

## Complete natural DG (domain-average within seed):

| dataset | method | accuracy | accuracy_sd | macro_f1 | macro_f1_sd | cohort |
| --- | --- | --- | --- | --- | --- | --- |
| OfficeHome | clip_erm | 75.47 | 0.09 | 73.50 | 0.15 | recovered_audited_20261121 |
| OfficeHome | ours_source_only_DG | 44.28 | 4.32 | 39.73 | 5.40 | recovered_audited_20261121 |
| OfficeHome | plain_erm | 61.58 | 0.32 | 59.77 | 0.52 | recovered_audited_20261121 |
| OfficeHome | vl2v_sd | 83.60 | 0.23 | 82.30 | 0.25 | recovered_audited_20261121 |
| OfficeHome | wen2025 | 84.61 | 0.10 | 83.47 | 0.12 | recovered_audited_20261121 |
| PACS | clip_erm | 88.61 | 0.34 | 89.49 | 0.41 | recovered_audited_20261121 |
| PACS | ours_source_only_DG | 69.02 | 0.87 | 67.41 | 1.26 | recovered_audited_20261121 |
| PACS | plain_erm | 70.33 | 0.86 | 69.16 | 1.63 | recovered_audited_20261121 |
| PACS | vl2v_sd | 93.90 | 0.42 | 94.72 | 0.44 | recovered_audited_20261121 |
| PACS | wen2025 | 94.90 | 0.65 | 95.72 | 0.56 | recovered_audited_20261121 |
| PACS | wen_base | 93.97 | 0.42 | 94.79 | 0.36 | recovered_audited_20261121 |
| VLCS | clip_erm | 74.92 | 3.19 | 67.19 | 3.93 | recovered_audited_20261121 |
| VLCS | ours_source_only_DG | 75.93 | 0.20 | 69.49 | 1.07 | recovered_audited_20261121 |
| VLCS | plain_erm | 75.65 | 0.78 | 69.33 | 0.44 | recovered_audited_20261121 |
| VLCS | vl2v_sd | 82.58 | 0.50 | 79.31 | 1.18 | recovered_audited_20261121 |
| VLCS | wen2025 | 82.71 | 0.16 | 79.74 | 0.45 | recovered_audited_20261121 |
| DomainNet | clip_erm | 51.93 | 0.19 | 49.50 | 0.22 | earlier_professor_suite |
| DomainNet | ours_source_only_DG | 3.74 | 0.66 | 1.39 | 0.53 | earlier_professor_suite |
| DomainNet | vl2v_sd | 58.38 | 0.20 | 56.32 | 0.13 | earlier_professor_suite |
| TerraIncognita | clip_erm | 26.73 | 4.15 | 13.49 | 2.93 | earlier_professor_suite |
| TerraIncognita | ours_source_only_DG | 24.93 | 0.74 | 15.79 | 0.11 | earlier_professor_suite |
| TerraIncognita | vl2v_sd | 51.09 | 0.61 | 29.00 | 0.53 | earlier_professor_suite |

## Practice

1. Calculate the AML macro-F1 difference between `ours` and `ours_source` in recent UDA (answer: 7.45 pp).
2. Find a deterministic fit and explain why its SD is unavailable.
3. Compare historical one-view and five-view results without mixing them with recent UDA.

