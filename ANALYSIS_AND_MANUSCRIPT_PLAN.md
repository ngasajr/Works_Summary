# Final analysis organized around the manuscript's three concerns

All 27 matched training runs and their diagnostics are complete. Unless stated otherwise, performance below is whole-dataset macro-F1 (%) without TTA, mean ± sample SD over seeds 42/43/44. Diagnostic panels are separate: 32 images per class per domain. This is the new controlled-study cohort, not the earlier frozen-model cohort or a different manuscript checkpoint. Use the full reference from this cohort when reporting its ablation deltas.

## 1. Does each component contribute?

### Controlled ResNet50 comparison

| Configuration | Acevedo target | Raabin external | AML external |
|---|---:|---:|---:|
| Full model | 81.88 ± 5.72 | **68.47 ± 1.49** | **69.68 ± 1.85** |
| Architecture-matched source-only | 80.71 ± 2.41 | 63.05 ± 12.65 | 59.62 ± 6.78 |
| Without orthogonality | 68.68 ± 12.81 | 59.73 ± 0.85 | 58.45 ± 3.92 |
| Without class-supervised contrastive loss | 78.42 ± 6.89 | 66.89 ± 3.54 | 65.28 ± 2.23 |
| Tied augmented input views | 89.23 ± 0.36 | 57.67 ± 9.98 | 61.32 ± 8.87 |
| Without agreement losses | **89.67 ± 3.88** | 64.24 ± 8.96 | 61.98 ± 5.84 |
| Fixed objective weights | 75.00 ± 15.12 | 63.18 ± 3.42 | 63.41 ± 6.04 |

All removal controls share the full model's architecture, optimizer, data split and phase budget; matched-source retains the architecture and source objectives over 80 supervised epochs instead of adaptation. Selection uses source-validation macro-F1. The controller receives source-validation/unlabeled-training feedback, not target labels. Removing a component changes the coupled optimization trajectory and source-selected checkpoint; effects are total effects of that removal, not additive causal contributions with all other trajectories held fixed.

### Findings that deserve emphasis

**Orthogonality: strongest one-factor evidence.** Full-minus-no-orthogonality gains are +13.20 pp Acevedo, +8.73 pp Raabin and +11.23 pp AML. Every domain improves in every seed (3/3 per domain). This supports a beneficial regularization contribution under this protocol. It does not establish semantic morphology/style disentanglement.

**Adaptive weighting: consistent external benefit.** Full-minus-fixed gains are +5.29 pp Raabin and +6.27 pp AML, positive in all three seeds on both datasets. Acevedo mean improvement is +6.88 pp, but paired seed differences are +12.64, −16.07 and +24.07 pp; its paired SD is 20.68 pp. Do not call the target effect uniformly stable. The experiment tests the complete hybrid controller versus fixed initial weights; it does not isolate the learned policy residual from the heuristic prior or establish superiority over other balancing algorithms.

**View independence: an external-transfer tradeoff.** Relative to tied inputs, independent views improve mean Raabin F1 by 10.80 pp (3/3 seeds) and AML by 8.35 pp (2/3 seeds), but reduce Acevedo by 7.35 pp (worse in all three seeds). These are two draws from the same augmentation family, not a demonstrated distinct morphology-view/style-view pair. Call this an independent-augmentation control, not proof of semantic view complementarity.

**Agreement: improves external transfer but hurts clean target performance.** Full versus no agreement is +4.23 pp Raabin (2/3 seeds), +7.69 pp AML (3/3), and −7.79 pp Acevedo (worse in all three). This is an important result, not an inconvenient exception to omit. It supports a target-versus-external-transfer tradeoff; it does not establish that the full configuration is optimal for target accuracy.

**Contrastive learning: strongest benefit is AML and appearance robustness.** Whole-dataset gains are +3.46 pp Acevedo, +1.58 pp Raabin and +4.39 pp AML. Only AML improves in all three seeds; the first two means are heterogeneous. The loss uses source class labels, not anatomical morphology annotations. Its relation to morphology must be supported by input/representation analyses rather than its name alone.

### Replacement for concern 1

> Matched one-factor ablations identify orthogonality as the most consistent component: removing it reduces macro-F1 on the adapted target and both external datasets in all three seeds. Adaptive weighting also improves both external datasets relative to fixed weights. Independent views and agreement exhibit a tradeoff, improving mean external transfer while reducing clean adapted-target performance. These results establish protocol-specific effects of component removal, while interactions among objectives and controller feedback prevent an additive decomposition of the gains.

Do not claim every component helps every domain, or claim statistically significant gains from three seed SDs alone. The dot plots expose individual seed outcomes.

## 2. Does morphology-emphasized learning help?

Use the architecture-matched controls, not only comparison with a smaller/different source-only architecture. On the FIXED CLASS-BALANCED GRAYSCALE panels:

| Configuration | Acevedo | Raabin | AML |
|---|---:|---:|---:|
| Full | **62.52 ± 7.24** | **41.22 ± 5.54** | **41.09 ± 9.98** |
| Matched source-only | 40.80 ± 0.22 | 40.38 ± 4.52 | 33.64 ± 3.61 |
| Without contrastive loss | 46.25 ± 13.86 | 35.80 ± 3.32 | 32.41 ± 0.15 |
| Tied input views | 33.40 ± 12.33 | 37.65 ± 10.04 | 29.63 ± 8.40 |
| Without agreement | 31.93 ± 5.51 | 35.25 ± 4.99 | 28.81 ± 2.87 |

Full-minus-matched-source grayscale gains are +21.72 pp Acevedo, +0.84 pp Raabin and +7.45 pp AML. The Raabin advantage is small, not a broad color-invariance result. Relative to no contrastive learning, gains are +16.27, +5.42 and +8.68 pp; Acevedo and AML improve in all three seeds, Raabin in two. Independent augmentation and agreement substantially improve Acevedo color-removal robustness despite lowering its clean target performance. This links the objective choices to an observed robustness tradeoff more concretely than a confusion matrix does.

The new full reference's clean panel F1 is 82.38% Acevedo, 77.86% Raabin and 71.69% AML. Histogram-preserving tile scrambling lowers these to 8.41%, 6.67% and 6.67%. This supports dependence on spatial organization beyond a global pixel histogram. The same intervention also damages source-only models, adds artificial patch boundaries and is not label preserving. Its severity is not perceptually matched to grayscale/hue/gamma changes.

**Defensible interpretation:** structural information remains useful after color removal, and selected learning objectives improve robustness to that intervention. **Not established:** reliance specifically on the nucleus/cytoplasm rather than background/context; pure nuisance-style removal; semantic disentanglement; or that color itself is an undesirable cue. WBC staining contains useful biological information, and grayscale removes some of it.

### Replacement morphology paragraph

> On class-balanced diagnostic panels, the full model retains higher grayscale macro-F1 than the architecture-matched source-only control, with the largest gain on Acevedo (+21.72 percentage points). Removing class-supervised contrastive learning reduces grayscale F1 by 16.27, 5.42 and 8.68 points on Acevedo, Raabin-WBC and AML, respectively. Histogram-preserving spatial scrambling produces much larger degradation than selected mild appearance changes. Together, these findings support the use of spatially organized, partly color-robust cues, without establishing anatomical localization or complete invariance to staining.

## 3. Computational cost and backbone dependence

### Within-backbone matched performance

| Backbone | Training | Acevedo F1 | Raabin F1 | AML F1 | Mean training minutes |
|---|---|---:|---:|---:|---:|
| ResNet50 | Matched source-only | 80.71 ± 2.41 | 63.05 ± 12.65 | 59.62 ± 6.78 | 9.12 |
| ResNet50 | Full | 81.88 ± 5.72 | 68.47 ± 1.49 | 69.68 ± 1.85 | 14.91 |
| EfficientNetB0 | Matched source-only | 78.13 ± 1.19 | 62.93 ± 3.86 | 72.94 ± 0.16 | 10.31 |
| EfficientNetB0 | Full | 81.58 ± 2.26 | 66.30 ± 3.99 | 73.04 ± 2.80 | 15.93 |

The complete framework improves mean Acevedo and Raabin F1 on both backbones. EfficientNetB0 gains are +3.45 and +3.37 pp and positive in all three seeds for those domains. Its AML gain is only +0.10 pp, with a negative seed-43 effect. The ResNet50 AML gain is +10.05 pp in all three seeds. Therefore the supported claim is **positive mean adaptation benefits on two tested backbones for Acevedo/Raabin, with dataset-dependent magnitude**. Universal backbone independence is not established. EfficientNetB0 has stronger absolute AML F1 than ResNet50, so do not claim ResNet50 is uniformly the best backbone.

Training time is approximately 1.64× matched-source for ResNet50 and 1.55× for EfficientNetB0, including graph tracing in the timed training loop but excluding separate final diagnostics. Both sides use the same compiled implementation. The roughly eightfold implementation speedup versus the old eager loop is not an algorithmic efficiency gain.

### Dedicated inference profiling

The completed independent profiling cohort compares the proposed inference architecture with the STANDARD average-pooled ResNet50 source-only architecture, not the identical-architecture source control. On one RTX 4090, with decoding excluded, eight warmups and 30 synchronized repetitions per configuration:

| Architecture | Batch-1 one-view latency | Active inference parameters |
|---|---:|---:|
| Standard source-only | 3.05 ± 0.53 ms | 24.11 M |
| Proposed | 3.24 ± 0.64 ms | 24.97 M |

The mean observed overhead is approximately 0.19 ms and 0.86 M parameters. Latency variability overlaps; do not claim a statistically established percentage penalty or speed advantage. At batch 32, one-view median batch latency is 11.56 versus 11.40 ms. Five-view TTA increases proposed batch-1 latency to 11.91 ms. The controller and adaptation losses are training-only. The architecture-matched source-only control has the same inference graph as the full model, but its inference latency was not separately measured in this benchmark.

### Replacement for concern 2

> Matched source-only comparisons show positive mean Acevedo and Raabin gains with both ResNet50 and EfficientNetB0, while the AML gain is strongly backbone-dependent. The full training procedure costs approximately 1.64× and 1.55× its matched source-only reference on these backbones. Dedicated GPU profiling measures 3.24 ms single-image inference and 24.97 M active parameters for the proposed architecture, compared with 3.05 ms and 24.11 M for a standard source-only ResNet50. These results quantify an accuracy–cost tradeoff rather than computational superiority or universal backbone independence.

## 4. What the representations actually contain

Use probes from the NEW full control references when discussing these ablations. The earlier diagnostic cohort has different values and should not be blended into this table.

| Branch | Acevedo class-probe F1 | Raabin class-probe F1 | AML class-probe F1 | Class-conditional domain accuracy |
|---|---:|---:|---:|---:|
| Morphology | 79.08 | 77.23 | 70.28 | 89.17 |
| Style | 83.98 | 76.59 | 70.42 | 89.95 |
| Alignment projection | 79.21 | 76.68 | 69.01 | 90.16 |
| Shared | 79.00 | 77.21 | 69.62 | 92.97 |

Class probes are trained on source labels and evaluated without target fitting. Domain probes use equal class/domain sample counts, within-fold standardization and four-fold image-level CV; four-domain chance is 25%. Shuffled-label control results are saved. Domain decoding includes all domain-associated differences, which may include biological as well as acquisition variation.

The style branch retains substantial class information, sometimes more than the branch called morphology. Domain accuracy of the morphology branch is 89.17% for full versus 88.80% without orthogonality; there is no evidence that the penalty removes domain identity. The full model also has higher domain decodability than matched source-only (82.34%), so domain invariance is not a demonstrated explanation of the observed transfer gains.

Orthogonality does reduce the measured cross-correlation statistic: full/no-orthogonality values are 0.225/0.253 on Acevedo, 0.198/0.236 on Raabin and 0.185/0.222 on AML. However, cross-branch linear CKA remains around 0.95–0.98. The correct interpretation is **useful regularization of overlapping representations**, not a clean semantic factorization. High domain decodability does not prove that the classifier uses those domain cues to make mistakes, just that the cues remain accessible.

### Replacement for concern 3

> Representation probes show that class information is retained across multiple projections, while domain identity remains readily decodable, including from the morphology branch. Orthogonality lowers cross-correlation and improves classification under the evaluated protocol, but does not establish semantic morphology/style separation. Input interventions additionally reveal sensitivity to both spatial organization and appearance. These analyses characterize representation content and input dependence; identifying the anatomical or acquisition-specific causes of individual errors still requires annotated structures or controlled paired acquisitions.

## 5. Recommended manuscript organization

### Main paper

1. **Protocol:** put the frozen split, initialization, shared architecture/optimizer for controls, 35+45 versus 80 source-only budget, source-validation-only selection, three independent seeds, and consistent no-TTA inference before the result tables. Say that the adaptive controller additionally receives source-validation feedback. Disclose cell-level rather than verified patient-level evaluation.
2. **Benchmark comparison:** retain separately verified baseline results, with their exact initialization and inference convention. Do not mix this controlled cohort's full-model row with a different manuscript checkpoint's 90.57/82.72/74.66 values.
3. **Controlled component analysis:** replace cumulative attribution with the seven-row table above and `component_effects.pdf`. Keep cumulative removals only as supplementary system simplification results. Explicitly discuss negative target effects of agreement/independent views.
4. **Morphology-related robustness:** show `matched_grayscale.pdf` and compact intervention examples. Include a concise description of pixel-histogram preservation, the destruction-control caveat, and the fixed balanced panel. Put all nine conditions and per-class/seed outcomes in supplementary material.
5. **Backbone and cost:** use the four-row matched-backbone table and `backbone_matched_gains.pdf`; include a small inference-cost table. If space is tight, move detailed profiling at all batch sizes/TTA settings to supplement.
6. **Representation analysis:** present `matched_representation_probes.pdf` and a short orthogonality-statistic table or `orthogonality_dependence.pdf`. Report the strong domain decoding in the main text because it directly qualifies a morphology/style semantic claim.
7. **Discussion:** focus on the adapted-target versus external-transfer/appearance-robustness tradeoff, strong orthogonality evidence, and conditional backbone gains.

### Supplementary material

- All seed rows and paired deltas; all TTA counterparts; full source-test results.
- All appearance interventions, panel image IDs/hashes and original-class distribution versus diagnostic balance.
- Class/domain probe protocol, shuffled-label references, dependence/CKA statistics, and raw predictions.
- GPU/software timing conditions, active versus auxiliary parameter accounting, training-time inclusion/exclusion rules.
- Exact checkpoint lineage and model-selection policy. Patient grouping remains unresolved; image-bootstrap intervals do not repair that gap.

### Claims to retain, narrow or remove

- **Retain:** matched evidence for orthogonality; consistent external benefits of configured adaptive weighting; color-removal robustness linked to source contrastive/consistency training; dataset-specific external gains.
- **Narrow:** view complementarity to independent-augmentation effects and an external-transfer tradeoff; morphology awareness to spatially organized and partly color-robust discrimination; backbone generality to the tested pairs/domains.
- **Remove:** clean semantic disentanglement, universal domain invariance, universal superiority of the full configuration on the adapted target, computational efficiency/speed superiority, or standalone proof that the learned RL residual drives the controller's benefit.
- **Keep as limitations:** patient/specimen independence, anatomical localization, shared objective/controller interactions, small three-seed sample, and effects on untested domains/backbones. A heuristic-only versus learned-residual controller control is still needed if a specific RL-learning novelty claim is retained.

## 6. Suggested discussion and conclusion

**Discussion:** The controlled results support orthogonality as a useful regularizer and adaptive weighting as a contributor to external transfer. Independent augmentation and agreement improve external and appearance-shift performance at a cost to clean adapted-target F1, indicating that target accuracy and transfer robustness are distinct objectives. Probe results show that this benefit does not require the learned branches to become domain-free: they remain overlapping and domain-informative. Thus the evidence supports regularized, partly appearance-robust representation learning rather than a demonstrated anatomical morphology/style decomposition.

**Conclusion:** We evaluated the framework using matched component removals, two backbone-specific source controls, input interventions and representation probes. Orthogonality consistently improves target/external classification in the tested ResNet50 setting, while adaptive weighting benefits both external datasets. View consistency introduces a target–external-transfer tradeoff, and matched backbone experiments show dataset-dependent gains. These findings support the practical value of the combined framework while delimiting its morphology and invariance claims.
