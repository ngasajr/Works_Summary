# Interpretation of the completed contribution experiments

**The experiments support component dependence and some external-transfer gains. They do not support a general claim that the tested optical-density view or learned controller is the strongest configuration.** The most useful outcome is that the study separates an implemented mechanism from its actual performance benefit.

## 1. What was completed and verified

- **54 full training runs:** 18 configurations × three seeds (42–44).
- **12 frozen diagnostic runs:** four configurations × three seeds.
- **432 final prediction archives:** four datasets × two inference settings × 54 runs. Their labels, image IDs, probabilities, accuracy, and macro-F1 were rechecked against the saved manifest and summaries.
- All queued training runs returned successfully. Completion: **26 November 2026, 08:40 KST**, after approximately 12 h 27 min.
- Three seeds quantify training variability, not independent patients or hospitals. Confidence intervals based on these seeds are descriptive; no correction for multiple comparisons or clinical population inference is claimed.

The controlled cohort uses the recovered **ResNet50 configuration**, despite “EfficientNet” in the folder name. Causal training comparisons start from matched ImageNet initialization rather than an already adapted checkpoint. The recovered checkpoint is evaluated separately. The implemented OD operator is a prospectively specified realization of the manuscript equations; its numerical basis and coefficients were not recovered historical settings.

## 2. Main performance comparison

Values are **macro-F1 (%)**, mean ± sample SD, without TTA. These are new-cohort results, not replacements for historical manuscript numbers.

| Configuration | Acevedo F1 | Raabin F1 | AML F1 |
|---|---:|---:|---:|
| Source-only architecture control (OD + RGB) | 81.30 ± 2.87 | 60.94 ± 2.57 | 46.61 ± 5.14 |
| RGB + RGB, fixed weights | 71.77 ± 15.79 | 64.25 ± 2.60 | 63.81 ± 6.10 |
| OD + RGB, fixed reference | 75.78 ± 6.46 | 62.71 ± 0.90 | 52.70 ± 7.76 |
| OD + RGB, heuristic controller | 64.68 ± 19.98 | 69.11 ± 7.20 | 55.84 ± 6.78 |
| OD + RGB, random weighting | 72.76 ± 9.25 | 66.22 ± 4.52 | 52.19 ± 6.54 |
| OD + RGB, learned controller | 62.78 ± 13.87 | 66.17 ± 0.32 | 57.58 ± 9.19 |
| Grayscale + RGB | 80.45 ± 12.34 | 73.54 ± 3.34 | 70.98 ± 2.24 |
| Single RGB / shared head | 85.38 ± 5.21 | 68.76 ± 2.80 | 67.30 ± 2.42 |

[All 18 configurations with accuracy and F1, including TTA](COMPARISON_TABLES.md).

### What the full fixed reference establishes

Against the matched source-only architecture control, the OD + RGB reference changes macro-F1 by **−5.52 pp on Acevedo, +1.78 pp on Raabin, and +6.09 pp on AML**. Adaptation therefore improves the two external means while reducing the observed adaptation-target mean. This is a transfer tradeoff, not uniform improvement. The source-only control is itself the proposed two-view architecture, not a conventional RGB ERM model.

### Which configurations are strongest in this cohort

The single-RGB control has the highest observed Acevedo mean (**85.38**). Grayscale + RGB has the highest observed Raabin (**73.54**) and AML (**70.98**) means. These rankings are descriptive observations from the complete experiment matrix; selecting a new final method from these test outcomes requires an independent confirmation protocol.

The single-RGB comparison changes head sharing, agreement, and encoder computations together. It does **not** isolate “one view versus two views.” Grayscale versus OD holds the shared backbone and two-head setup fixed and is the more direct test of the proposed input transform.

## 3. Morphology emphasis: conditional benefit, with a clear AML weakness

### Average effect across the factorial design

Replacing RGB view A with the registered OD view changes macro-F1, averaged across alignment/self-training settings, by:

| Dataset | OD minus RGB effect (pp) | Effects for seeds 42 / 43 / 44 |
|---|---:|---|
| Acevedo | +0.08 | −7.58 / +0.25 / +7.57 |
| Raabin | +1.16 | +0.50 / +3.99 / −0.99 |
| AML | **−9.92** | **−7.63 / −10.04 / −12.08** |

There is no consistent average Acevedo gain, and the AML loss occurs in all three seeds. The effect applies to this particular fixed OD projection and full training path; it does not rule out useful morphology-aware learning with a different, validated operator.

### A reproducible OD–self-training interaction on Acevedo

Averaging over alignment settings, self-training changes Acevedo F1 by **+10.03 pp with OD**, versus **−4.15 pp with RGB**. The difference-in-differences is **+14.18 pp**, with per-seed effects **14.27, 14.01, and 14.26 pp**. This is evidence that the input representation changes how self-training behaves. It is not evidence that OD independently improves every condition or generalizes better to unseen sites. The three-seed result still needs replication beyond this split.

### Retaining RGB information matters

OD + RGB beats duplicate OD inputs by **+13.01 pp on Acevedo** and **+33.12 pp on AML**, with positive differences in every seed. Raabin changes by **−2.50 pp**, so complementarity is dataset-dependent. This comparison supports retaining information available in RGB; it does not establish that OD is preferable to other views.

Grayscale + RGB exceeds OD + RGB by **+10.83 pp on Raabin** and **+18.28 pp on AML**, in all three seeds for both external datasets. The current OD transformation should therefore be treated as a mechanism needing refinement, not an established optimal morphology representation.

## 4. Orthogonality and contrastive learning depend on each other

All rows below use OD + RGB, alignment and self-training, and fixed weighting.

| Orthogonality | Source contrastive | Acevedo F1 | Raabin F1 | AML F1 |
|---|---|---:|---:|---:|
| Off | Off | 79.21 | 64.17 | 50.56 |
| Off | On | 60.58 | 63.62 | 50.84 |
| On | Off | 72.24 | 67.59 | 57.43 |
| On | On | 75.78 | 62.71 | 52.70 |

With contrastive learning enabled, orthogonality improves Acevedo by **+15.20 pp**, with positive effects in every seed. With contrastive learning disabled, its Acevedo effect is **−6.97 pp**. Their Acevedo interaction is **+22.17 pp**, demonstrating dependence. However, the complete pair still scores below the configuration with both disabled (**75.78 versus 79.21**); “positive interaction” does not mean “best performance.”

On Raabin, adding contrastive learning when orthogonality is enabled reduces F1 by **4.88 pp**, in every seed. Its AML mean effect is **−4.73 pp**. These data do not justify saying that all representation objectives independently improve external transfer.

Orthogonality is switched during adaptation only, whereas the contrastive factor changes both pretraining and adaptation. The effects concern those explicitly defined interventions, not identical scheduling of all objectives.

## 5. Alignment and self-training have different target/external effects

Averaged over the other factors, the alignment group changes Acevedo/Raabin/AML F1 by **+5.09 / −1.42 / −0.52 pp**. The self-training group changes them by **+2.94 / −3.72 / −1.26 pp**. Their wide seed-based intervals and interactions preclude a general “every component helps” conclusion.

These factors are grouped mechanisms: alignment includes adversarial and statistical terms; self-training includes hard/soft pseudo-label and pseudo-agreement terms. The study identifies their grouped contribution and dependence, not separate adversarial-versus-CORAL or hard-versus-soft pseudo-label effects.

## 6. Professor’s RL questions: implementation demonstrated, superiority not demonstrated

The new learned controller has **three independent training runs, 45 optimizer updates each, totaling 135 actual parameter updates**. It samples **135 five-component action vectors** from learned categorical distributions. The random control samples another 135 vectors; the combined count of 270 must not be described as 270 learned-policy actions.

All learned-controller updates have nonzero logged gradients and parameter changes. In each run, the first update has zero centered reward advantage and can update entropy regularization; the remaining 44 updates have nonzero logged reward advantages. The sampled coefficients are consumed by the next model-training epochs, and the weighted objective is reconstructed from saved losses. This directly addresses whether the feedback loop was closed. The final policy update has no subsequent model-training epoch.

### Actual performance of learned weighting

Compared with fixed OD weighting, learned weighting changes Acevedo/Raabin/AML F1 by **−13.00 / +3.45 / +4.88 pp**. Both external differences are positive in all three seeds. Compared with the source-only architecture control, it changes them by **−18.53 / +5.23 / +10.97 pp**; again, both external gains occur in all seeds.

However, learned versus random weighting is **−9.98 / −0.05 / +5.39 pp**. Learned versus heuristic weighting is **−1.90 / −2.95 / +1.74 pp**. Consequently, these experiments demonstrate real policy training and an external-transfer tradeoff, but **not consistent performance superiority from policy learning itself**. The Raabin SD is low (**0.32 pp**), while Acevedo and AML remain variable (**13.87 and 9.19 pp**).

The random policy is uniform, not a frozen copy of the initially untrained network. A frozen-policy or coefficient-replay control would more closely isolate the effect of learning and feedback. Increasing the source/unlabeled proxy reward is not proof of improved target performance.

The recovered historical controller is deterministic and used labeled-target/source-test feedback in the inspected script. The new strict-UDA policy evidence cannot retrospectively establish learned RL in that historical run. The new policy controls five coefficient keys of the implementation, not every objective or the manuscript’s four-group formulation.

[Full answer and audit links](PROFESSOR_CONTROLLER_EVIDENCE.md).

## 7. What representation and robustness evidence actually establishes

Frozen diagnostics use **32 images per class per domain**. Their scores must not be substituted for whole-test metrics: the panels differ in class prevalence and sampled images. Probes use view-A features; in OD conditions these are OD-input features, while final predictions combine both views.

### Spatial dependence is present, but is not unique to OD

The OD reference’s balanced-panel Raabin F1 falls from **74.04 to 6.67** after tile disruption. The RGB reference falls from **74.75 to 6.67**. Both depend on spatial organization. This supports a structural sensitivity statement, not unique anatomical feature semantics or a uniquely superior morphology mechanism. Tile shuffling is destructive and is not asserted to preserve the label.

### Some appearance tolerance, not complete invariance

On the Raabin panel, fixed channel gains change the OD reference from **74.04 to 74.04**, versus **74.75 to 70.07** for RGB. That supports tolerance to this specific perturbation. On AML, the OD reference falls from **53.23 to 45.06**, so appearance robustness is not uniform. Applying grayscale to the entire input at inference is a different experiment from training with grayscale only in view A.

### Domain information remains strongly decodable

Within-class four-domain probe accuracy in the morphology branch is **93.07% for the OD reference**, **92.60% for learned weighting**, and **84.48% for RGB**; chance is 25%. The tested OD representation is therefore not demonstrably domain-invariant. Probe decodability also does not establish which domain cues cause individual errors.

Morphology/style CKA remains high: for example, the OD reference has **0.964 on Acevedo** and **0.961 on AML**. Its style branch’s source-trained linear probe reaches **83.99 Acevedo F1**, versus **72.89** from the morphology branch. Branch names and orthogonality alone do not establish semantic separation or independence.

The view-A morphology probe’s AML F1 is **22.55 with OD versus 65.82 with RGB**. This is consistent with the OD transform losing useful transferable information under this linear-probe protocol; it does not prove information is absent under every possible decoder.

## 8. Per-class interpretation

The learned controller’s Acevedo eosinophil F1 is **13.69**, versus **62.91** for fixed OD weighting. Its low target-domain mean is therefore accompanied by a pronounced class-specific failure, despite source-test F1 remaining high (**97.80**).

On AML, learned weighting improves eosinophil and lymphocyte F1 over fixed weighting (**57.77 vs 44.28**, **61.82 vs 48.73**), but reduces monocyte F1 (**43.81 vs 49.18**). Better overall external performance does not imply every class improves.

Grayscale + RGB reaches **88.28% Raabin accuracy** but **73.54% macro-F1**. Its monocyte F1 remains **48.45**. Retain both accuracy and macro-F1 and report per-class errors; high overall accuracy on the imbalanced Raabin set does not establish balanced class reliability. These are classification observations, not clinical validation.

## 9. Cost and test-time augmentation

Mean measured training wall time is **13.81 min** for the fixed OD reference, **13.99 min** for learned weighting, **7.81 min** for the source-only architecture control, and **8.64 min** for the single-RGB variant. The fixed reference costs about **1.77×** the source-only control and **1.60×** the single variant under these schedules. The latter also changes encoder-pass count, head sharing and objectives. This does not establish computational efficiency over recent methods, inference speed, or backbone-independent benefits.

Five-view TTA is not uniformly beneficial. For fixed OD, Raabin/AML F1 changes from **62.71/52.70** to **62.65/49.42**; for grayscale + RGB it changes from **73.54/70.98** to **73.93/72.98**. Keep no-TTA results primary and report the matched secondary setting for every configuration.

## 10. How to use this evidence in the manuscript

1. **Separate primary historical performance from this controlled cohort.** Disclose different initialization, selection and transform provenance. Do not insert a historical best checkpoint score into a new ablation row or silently present different protocols as one matched table.
2. **Use interaction tables in the main paper.** The strongest mechanistic evidence is the Acevedo OD–self-training interaction and orthogonality–contrastive dependence. Include external columns so target benefits and transfer costs remain visible.
3. **Put the complete 18-row accuracy/F1 table in the supplement.** Report all outcomes, three-seed dispersion, per-seed contrasts, per-class failures and no-TTA/TTA results. Negative results are part of the contribution analysis.
4. **Answer RL implementation separately from RL effectiveness.** Show actual update/action counts and coefficient consumption, then present fixed/heuristic/random/learned outcomes. Avoid “RL improves performance” without specifying the comparator and dataset.
5. **Use representation diagnostics to bound claims.** Say spatial dependence and perturbation-specific appearance tolerance, not verified morphological semantics or complete domain invariance. Report high domain decodability and retained class information in the style branch.
6. **Keep older MIC/PLUE/DIFO/CRPL comparisons in their own verified protocol cohorts.** These 54 runs are contribution tests, not new recent-method reproductions. They cannot establish superiority over those methods through cross-cohort score substitution.

### Suggested short findings paragraph

> Controlled factorial experiments reveal that the proposed objectives interact rather than contribute additively. Morphology emphasis changes the effectiveness of self-training on Acevedo, while orthogonality moderates the effect of source contrastive learning. These target-domain interactions do not translate into uniform external gains: the tested optical-density projection reduces AML performance relative to RGB and grayscale controls. The learned controller is trained through an explicitly verified feedback loop and improves external macro-F1 over the matched source-only control, but does not consistently outperform nonlearned weighting. The findings support further development of morphology-sensitive adaptation while identifying input construction and transfer-aware optimization as current limitations.

## 11. Priorities for improvement

- **Validate the morphology operator first.** Recover exact historical settings if available; compare fixed OD with grayscale, stain-appropriate alternatives and learned morphology views. Select settings on source validation or a separate development site, then confirm on untouched sites. Do not assume H/E-like projections faithfully isolate WBC structures.
- **Measure actual morphology preservation.** On an independent annotated subset, quantify nucleus/cytoplasm structure or expert-defined cell measurements before and after transformation. Perturbation robustness and visual examples alone cannot validate anatomical semantics.
- **Preserve an RGB residual path.** OD + OD’s AML collapse indicates useful information is removed. Test calibrated view weighting and whether class-specific signals lost by OD are retained without relying on target labels.
- **Redesign the source contrastive objective for transfer.** The current source-only contrastive term has reproducible Raabin costs in the orthogonal setting. Study its weight, class conditioning and agreement interaction under a preregistered development protocol; a target-aware contrastive extension would be a new method requiring confirmation.
- **Improve controller evaluation before adding more RL complexity.** Compare fixed, learned, frozen-untrained and coefficient-replay controls; predefine rewards and budgets. The current controller is a single epoch-level trajectory per seed, with only45 decisions, not extensive policy training across independent environments. Correlations in reward/weights alone do not establish beneficial causal control.
- **Investigate class-specific failure.** Analyze target eosinophils and external monocytes/eosinophils with per-class confidence, pseudo-label coverage, calibration and label-quality checks. Do not infer a morphological cause from a confusion matrix alone.
- **Strengthen generalization evidence.** Obtain patient/slide identifiers, add independent transfer directions and sites, and reproduce strong recent baselines under declared source access, backbone and model-selection rules. The present18-configuration study uses one adaptation direction and a single backbone.

This study makes the contribution claims more precise. It does not by itself establish state-of-the-art performance, clinical readiness, or suitability for acceptance at a particular venue.

## Supporting files

- [All accuracy/F1 tables](COMPARISON_TABLES.md)
- [Original numerical summary](summary.csv)
- [Per-run results](per_run.csv)
- [Paired contrasts and uncertainty](paired_contrasts_summary.csv)
- [Seed-specific contrasts](paired_contrasts_per_seed.csv)
- [Controller execution audit](controller_audit.csv)
- [Per-class summaries](per_class_summary.csv)
- [Compute and parameter summaries](runtime_summary.csv)
- [Representation probes](representation_probes.csv)
- [Frozen sensitivity summaries](frozen_sensitivity_summary.csv)
- [Recomputation verification](markdown_report_verification.json)
- [Registered protocol](../PROTOCOL.md)

![All configurations, macro-F1](all_components_macro_f1.png)

![Controller training stability](controller_training_stability.png)

![Factorial effects with descriptive seed-based intervals](factorial_effects_descriptive_ci95.png)

![Closed-loop controller evidence for seed42](policy_closed_loop_seed42.png)
