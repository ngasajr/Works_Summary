# Complete accuracy and macro-F1 tables

New controlled cohort only: percentages, mean ± sample SD across seeds 42–44. Source-validation selection; historical checkpoint scores are excluded. No row is a faithful reproduction of an unrelated published method.

## Primary: no test-time augmentation

| Configuration | Source Acc. | Source F1 | Acevedo Acc. | Acevedo F1 | Raabin Acc. | Raabin F1 | AML Acc. | AML F1 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| OD + RGB, heuristic controller | 98.48 ± 0.30 | 98.56 ± 0.24 | 69.20 ± 13.71 | 64.68 ± 19.98 | 72.78 ± 12.88 | 69.11 ± 7.20 | 56.99 ± 5.18 | 55.84 ± 6.78 |
| OD + RGB, learned controller | 97.77 ± 0.63 | 97.80 ± 0.64 | 69.38 ± 10.66 | 62.78 ± 13.87 | 71.86 ± 7.77 | 66.17 ± 0.32 | 58.22 ± 8.81 | 57.58 ± 9.19 |
| OD + RGB, random weighting | 97.57 ± 0.30 | 97.63 ± 0.20 | 74.31 ± 7.21 | 72.76 ± 9.25 | 71.61 ± 7.37 | 66.22 ± 4.52 | 53.00 ± 6.45 | 52.19 ± 6.54 |
| OD view A; alignment 0; self-training 0 | 98.28 ± 0.46 | 98.36 ± 0.45 | 64.04 ± 16.55 | 59.52 ± 21.04 | 69.42 ± 7.06 | 67.50 ± 6.50 | 52.07 ± 7.53 | 51.68 ± 8.20 |
| OD view A; alignment 0; self-training 1 | 98.48 ± 0.53 | 98.54 ± 0.60 | 73.60 ± 12.88 | 72.27 ± 14.56 | 70.95 ± 3.02 | 66.12 ± 2.80 | 57.83 ± 7.14 | 57.60 ± 7.97 |
| OD view A; alignment 1; self-training 0 | 98.38 ± 0.63 | 98.50 ± 0.60 | 71.56 ± 2.48 | 68.47 ± 3.46 | 72.92 ± 5.88 | 67.00 ± 4.58 | 57.76 ± 11.28 | 56.42 ± 12.12 |
| OD + RGB, fixed reference | 98.68 ± 0.46 | 98.83 ± 0.46 | 76.62 ± 5.78 | 75.78 ± 6.46 | 66.93 ± 1.22 | 62.71 ± 0.90 | 52.69 ± 7.07 | 52.70 ± 7.76 |
| RGB view A; alignment 0; self-training 0 | 98.48 ± 0.80 | 98.48 ± 0.79 | 73.11 ± 8.42 | 71.96 ± 10.07 | 78.47 ± 1.71 | 69.73 ± 1.31 | 68.59 ± 1.62 | 68.40 ± 1.67 |
| RGB view A; alignment 0; self-training 1 | 98.48 ± 0.61 | 98.46 ± 0.66 | 64.62 ± 9.38 | 61.94 ± 9.48 | 70.38 ± 7.75 | 60.49 ± 9.80 | 61.44 ± 9.53 | 61.59 ± 9.33 |
| RGB view A; alignment 1; self-training 0 | 98.38 ± 0.63 | 98.31 ± 0.67 | 72.18 ± 5.27 | 70.04 ± 6.21 | 73.73 ± 7.85 | 64.21 ± 3.42 | 65.05 ± 1.85 | 64.25 ± 0.30 |
| RGB + RGB, fixed weights | 98.28 ± 0.46 | 98.29 ± 0.47 | 73.87 ± 14.32 | 71.77 ± 15.79 | 75.16 ± 3.39 | 64.25 ± 2.60 | 64.13 ± 6.16 | 63.81 ± 6.10 |
| OD + RGB; orthogonality 0; contrastive 0 | 97.67 ± 0.18 | 97.82 ± 0.15 | 79.24 ± 6.77 | 79.21 ± 6.56 | 68.06 ± 9.76 | 64.17 ± 8.49 | 52.00 ± 6.72 | 50.56 ± 7.26 |
| OD + RGB; orthogonality 0; contrastive 1 | 98.28 ± 0.46 | 98.27 ± 0.42 | 65.91 ± 6.40 | 60.58 ± 5.39 | 70.02 ± 2.67 | 63.62 ± 4.99 | 52.84 ± 7.86 | 50.84 ± 9.39 |
| OD + RGB; orthogonality 1; contrastive 0 | 98.28 ± 0.46 | 98.39 ± 0.37 | 75.42 ± 9.15 | 72.24 ± 12.05 | 72.77 ± 1.94 | 67.59 ± 1.16 | 56.91 ± 4.86 | 57.43 ± 5.24 |
| Source-only architecture control (OD + RGB) | 98.18 ± 0.53 | 98.28 ± 0.45 | 81.20 ± 2.81 | 81.30 ± 2.87 | 62.40 ± 3.33 | 60.94 ± 2.57 | 47.08 ± 3.47 | 46.61 ± 5.14 |
| OD + OD | 97.57 ± 0.30 | 97.72 ± 0.38 | 69.20 ± 3.28 | 62.77 ± 4.02 | 68.48 ± 7.06 | 65.22 ± 5.79 | 26.88 ± 4.53 | 19.58 ± 6.18 |
| Grayscale + RGB | 98.48 ± 0.30 | 98.56 ± 0.34 | 82.22 ± 9.04 | 80.45 ± 12.34 | 88.28 ± 1.27 | 73.54 ± 3.34 | 72.12 ± 2.22 | 70.98 ± 2.24 |
| Single RGB / shared head | 98.28 ± 0.18 | 98.29 ± 0.27 | 85.64 ± 4.83 | 85.38 ± 5.21 | 76.86 ± 5.32 | 68.76 ± 2.80 | 67.20 ± 2.92 | 67.30 ± 2.42 |

## Secondary: identical five-view TTA

| Configuration | Source Acc. | Source F1 | Acevedo Acc. | Acevedo F1 | Raabin Acc. | Raabin F1 | AML Acc. | AML F1 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| OD + RGB, heuristic controller | 99.09 ± 0.80 | 99.11 ± 0.68 | 69.11 ± 13.61 | 64.47 ± 19.79 | 74.20 ± 12.80 | 70.58 ± 7.32 | 55.84 ± 5.91 | 53.79 ± 8.42 |
| OD + RGB, learned controller | 98.78 ± 0.30 | 98.76 ± 0.32 | 69.87 ± 10.79 | 63.23 ± 14.28 | 74.93 ± 7.51 | 69.50 ± 1.51 | 58.60 ± 7.67 | 57.40 ± 8.10 |
| OD + RGB, random weighting | 98.38 ± 0.63 | 98.39 ± 0.52 | 75.64 ± 6.98 | 74.32 ± 8.65 | 72.75 ± 7.25 | 66.73 ± 4.12 | 52.15 ± 5.34 | 50.62 ± 5.91 |
| OD view A; alignment 0; self-training 0 | 98.58 ± 0.63 | 98.68 ± 0.60 | 64.49 ± 16.78 | 60.09 ± 21.11 | 70.73 ± 5.74 | 68.39 ± 6.24 | 49.85 ± 7.12 | 48.79 ± 8.17 |
| OD view A; alignment 0; self-training 1 | 98.68 ± 0.46 | 98.78 ± 0.47 | 73.96 ± 12.97 | 72.72 ± 14.50 | 72.00 ± 2.27 | 67.43 ± 2.87 | 56.45 ± 9.71 | 55.59 ± 11.20 |
| OD view A; alignment 1; self-training 0 | 99.19 ± 0.63 | 99.20 ± 0.53 | 71.69 ± 3.40 | 68.24 ± 5.05 | 74.46 ± 4.51 | 68.17 ± 4.16 | 56.61 ± 12.06 | 54.46 ± 13.67 |
| OD + RGB, fixed reference | 98.89 ± 0.63 | 98.96 ± 0.56 | 76.76 ± 5.79 | 75.89 ± 6.55 | 68.01 ± 1.20 | 62.65 ± 0.93 | 50.31 ± 8.38 | 49.42 ± 9.69 |
| RGB view A; alignment 0; self-training 0 | 98.89 ± 0.63 | 98.83 ± 0.62 | 74.27 ± 8.60 | 73.13 ± 10.50 | 78.52 ± 2.08 | 70.01 ± 1.93 | 70.51 ± 1.83 | 70.31 ± 1.98 |
| RGB view A; alignment 0; self-training 1 | 99.29 ± 0.46 | 99.30 ± 0.51 | 66.13 ± 8.90 | 63.37 ± 8.96 | 69.65 ± 7.67 | 60.74 ± 9.92 | 63.36 ± 10.41 | 63.50 ± 10.25 |
| RGB view A; alignment 1; self-training 0 | 98.89 ± 0.88 | 98.80 ± 1.03 | 73.73 ± 6.07 | 71.81 ± 7.23 | 72.90 ± 7.99 | 64.00 ± 3.81 | 66.13 ± 2.20 | 65.49 ± 1.12 |
| RGB + RGB, fixed weights | 98.78 ± 0.30 | 98.74 ± 0.43 | 75.42 ± 13.10 | 73.13 ± 14.86 | 73.99 ± 3.23 | 63.53 ± 3.20 | 64.82 ± 5.94 | 64.56 ± 6.00 |
| OD + RGB; orthogonality 0; contrastive 0 | 98.28 ± 0.70 | 98.40 ± 0.54 | 79.51 ± 6.49 | 79.49 ± 6.38 | 70.82 ± 11.06 | 66.57 ± 9.39 | 50.84 ± 8.32 | 49.13 ± 9.15 |
| OD + RGB; orthogonality 0; contrastive 1 | 99.19 ± 0.18 | 99.12 ± 0.13 | 65.87 ± 5.89 | 60.42 ± 5.01 | 72.25 ± 2.01 | 64.26 ± 5.84 | 50.84 ± 9.22 | 47.04 ± 12.06 |
| OD + RGB; orthogonality 1; contrastive 0 | 99.19 ± 0.35 | 99.22 ± 0.31 | 75.64 ± 9.74 | 72.32 ± 12.74 | 74.13 ± 1.59 | 68.29 ± 0.66 | 54.22 ± 4.05 | 53.65 ± 4.78 |
| Source-only architecture control (OD + RGB) | 98.58 ± 0.76 | 98.68 ± 0.70 | 81.91 ± 2.93 | 82.02 ± 2.98 | 62.95 ± 3.37 | 60.88 ± 1.99 | 46.16 ± 1.67 | 45.13 ± 3.18 |
| OD + OD | 98.07 ± 0.70 | 98.18 ± 0.73 | 69.82 ± 2.96 | 63.50 ± 3.61 | 68.70 ± 7.21 | 66.69 ± 5.58 | 26.96 ± 4.32 | 19.41 ± 5.49 |
| Grayscale + RGB | 99.19 ± 0.18 | 99.16 ± 0.23 | 83.20 ± 9.17 | 81.44 ± 12.41 | 88.35 ± 1.73 | 73.93 ± 4.11 | 73.96 ± 1.84 | 72.98 ± 1.64 |
| Single RGB / shared head | 99.09 ± 0.30 | 99.05 ± 0.37 | 87.60 ± 5.34 | 87.40 ± 5.60 | 76.68 ± 5.07 | 69.19 ± 2.62 | 69.35 ± 2.44 | 69.33 ± 2.21 |

## Interpretation boundaries

The alignment factor combines adversarial learning and statistical alignment. The self-training factor combines hard/soft pseudo-label and pseudo-agreement terms. Alignment = 0 and self-training = 0 still retains target agreement and target orthogonality; it is not the source-only control. Orthogonality is varied during adaptation; contrastive learning is varied across both phases. The single-head variant also changes agreement, classifier capacity, and encoder-pass count.
