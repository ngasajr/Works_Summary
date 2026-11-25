# Morphology and component evidence

Completed diagnostic models: 6/6. Completed matched retraining runs: 27/27.

This report describes new proposed-model analyses under the recorded protocol. Frozen intervention results use 32 images per class per domain (160/domain), fixed by hashed identity, and three training seeds when complete. These panel scores are separate from full-dataset manuscript scores.

## Appearance versus spatial arrangement

Appearance interventions preserve spatial pixel positions. The 7×7 tile permutation preserves the exact pixel/color histogram but destroys spatial arrangement and adds patch boundaries; it is not a label-preserving corruption. This is operational evidence about spatial dependence, not anatomical proof. Perturbation severities are not matched in perceptual strength. Both proposed and source-only models are evaluated on identical images.

### Acevedo
- ours: clean F1 73.09 ± 10.89; grayscale 52.20 ± 10.63; spatial scramble 10.94 ± 6.35.
- source: clean F1 76.36 ± 5.97; grayscale 38.82 ± 4.72; spatial scramble 14.88 ± 8.92.
### Raabin
- ours: clean F1 72.23 ± 1.84; grayscale 39.77 ± 11.37; spatial scramble 9.59 ± 5.07.
- source: clean F1 77.14 ± 6.04; grayscale 34.96 ± 11.28; spatial scramble 15.70 ± 10.40.
### Aml
- ours: clean F1 67.49 ± 1.33; grayscale 33.46 ± 7.82; spatial scramble 7.46 ± 1.38.
- source: clean F1 60.92 ± 8.15; grayscale 30.30 ± 11.07; spatial scramble 20.18 ± 6.56.

All conditions and seed rows are included in the CSV tables and intervention figure; no favorable subset was selected.

## Representation semantics

Source-trained linear probes measure cell-class information. Four-domain probes are trained within each class using equal domain counts, fold-contained standardization, fixed C=1 and four-fold image-level CV. Shuffled domain labels provide a reference. High domain predictability means the representation remains domain-informative; low correlation alone cannot establish semantic disentanglement. Folds are not patient-grouped because group IDs are unavailable.

- Proposed morphology domain accuracy: 87.97% (four-domain chance 25%).
- Proposed projection domain accuracy: 90.31% (four-domain chance 25%).
- Proposed shared domain accuracy: 92.55% (four-domain chance 25%).
- Proposed style domain accuracy: 88.59% (four-domain chance 25%).

## What can and cannot be concluded

- A greater response to scrambling than to selected color changes supports spatial dependence. It does not establish that the proposed method is more morphology-aware than a source-only classifier unless their paired difference supports that comparison.
- All planned retraining cases are complete; use the paired component deltas below, including negative effects. Controller-aware removals measure full-system responses, not additive effects independent of all other losses.
- Class information present in the style branch and domain information present in the morphology branch must be reported, even if the classification results are strong.
- Runtime and throughput are measured on one RTX 4090 after warmup with synchronized GPU execution. Training throughput gains from graph compilation are an implementation optimization, not evidence that the proposed architecture is inherently efficient.
- Backbone claims are limited to the two evaluated backbones and require a full-versus-matched-source comparison within each. Two backbones cannot establish universal backbone independence.

## Dedicated GPU timing (mean across completed model seeds)

- ours, batch 1, 1-view: median batch latency 3.24 ms; throughput 316.2 images/s.
- ours, batch 1, 5-view: median batch latency 11.91 ms; throughput 84.0 images/s.
- ours, batch 8, 1-view: median batch latency 4.14 ms; throughput 1933.1 images/s.
- ours, batch 8, 5-view: median batch latency 18.18 ms; throughput 440.2 images/s.
- ours, batch 32, 1-view: median batch latency 11.56 ms; throughput 2769.3 images/s.
- ours, batch 32, 5-view: median batch latency 65.18 ms; throughput 490.9 images/s.
- source, batch 1, 1-view: median batch latency 3.05 ms; throughput 335.3 images/s.
- source, batch 1, 5-view: median batch latency 10.39 ms; throughput 96.3 images/s.
- source, batch 8, 1-view: median batch latency 3.80 ms; throughput 2104.3 images/s.
- source, batch 8, 5-view: median batch latency 17.69 ms; throughput 452.2 images/s.
- source, batch 32, 1-view: median batch latency 11.40 ms; throughput 2806.9 images/s.
- source, batch 32, 5-view: median batch latency 62.53 ms; throughput 511.8 images/s.

## Matched retraining results (completed pairs only)

Positive full-minus-control macro-F1 favors the full model; negative values favor the control. Paired seed counts are shown explicitly. These descriptive effects are not significance tests.
- efficientnetb0, acevedo_tta1, full minus matched_source: +3.45 pp; seed SD 2.40; matched seeds 3/3.
- efficientnetb0, aml_tta1, full minus matched_source: +0.10 pp; seed SD 2.67; matched seeds 3/3.
- efficientnetb0, raabin_tta1, full minus matched_source: +3.37 pp; seed SD 2.57; matched seeds 3/3.
- efficientnetb0, source_test_tta1, full minus matched_source: -0.47 pp; seed SD 0.79; matched seeds 3/3.
- resnet50, acevedo_tta1, full minus fixed: +6.88 pp; seed SD 20.68; matched seeds 3/3.
- resnet50, acevedo_tta1, full minus matched_source: +1.17 pp; seed SD 3.42; matched seeds 3/3.
- resnet50, acevedo_tta1, full minus no_agreement: -7.79 pp; seed SD 8.01; matched seeds 3/3.
- resnet50, acevedo_tta1, full minus no_contrastive: +3.46 pp; seed SD 11.25; matched seeds 3/3.
- resnet50, acevedo_tta1, full minus no_orthogonality: +13.20 pp; seed SD 7.34; matched seeds 3/3.
- resnet50, acevedo_tta1, full minus tied_views: -7.35 pp; seed SD 5.75; matched seeds 3/3.
- resnet50, aml_tta1, full minus fixed: +6.27 pp; seed SD 4.27; matched seeds 3/3.
- resnet50, aml_tta1, full minus matched_source: +10.05 pp; seed SD 7.16; matched seeds 3/3.
- resnet50, aml_tta1, full minus no_agreement: +7.69 pp; seed SD 4.81; matched seeds 3/3.
- resnet50, aml_tta1, full minus no_contrastive: +4.39 pp; seed SD 3.14; matched seeds 3/3.
- resnet50, aml_tta1, full minus no_orthogonality: +11.23 pp; seed SD 5.19; matched seeds 3/3.
- resnet50, aml_tta1, full minus tied_views: +8.35 pp; seed SD 7.71; matched seeds 3/3.
- resnet50, raabin_tta1, full minus fixed: +5.29 pp; seed SD 2.65; matched seeds 3/3.
- resnet50, raabin_tta1, full minus matched_source: +5.42 pp; seed SD 12.41; matched seeds 3/3.
- resnet50, raabin_tta1, full minus no_agreement: +4.23 pp; seed SD 7.97; matched seeds 3/3.
- resnet50, raabin_tta1, full minus no_contrastive: +1.58 pp; seed SD 4.65; matched seeds 3/3.
- resnet50, raabin_tta1, full minus no_orthogonality: +8.73 pp; seed SD 2.32; matched seeds 3/3.
- resnet50, raabin_tta1, full minus tied_views: +10.80 pp; seed SD 9.36; matched seeds 3/3.
- resnet50, source_test_tta1, full minus fixed: +1.11 pp; seed SD 1.31; matched seeds 3/3.
- resnet50, source_test_tta1, full minus matched_source: +0.20 pp; seed SD 0.79; matched seeds 3/3.
- resnet50, source_test_tta1, full minus no_agreement: +0.27 pp; seed SD 0.37; matched seeds 3/3.
- resnet50, source_test_tta1, full minus no_contrastive: +1.11 pp; seed SD 0.10; matched seeds 3/3.
- resnet50, source_test_tta1, full minus no_orthogonality: +1.11 pp; seed SD 1.64; matched seeds 3/3.
- resnet50, source_test_tta1, full minus tied_views: +0.13 pp; seed SD 1.04; matched seeds 3/3.

Training costs are recorded in controlled_cost.csv; compare matched compiled implementations, not compiled timings against older eager runs.
