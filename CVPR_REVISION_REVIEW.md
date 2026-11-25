# Review of CVPR_Morphology_Aware_Two_View_Learning.pdf

Reviewed 9 November 2026. These suggestions use the numbers printed in the revised PDF. The new checkpoint-based run logs, predictions and configurations were not found in the shared workspace, so the revised scores are not independently verified. The previous local results must not be substituted for the newly reported results.

## Essential corrections before adopting the prose

1. **Checkpoint comparability.** State what each method started from and how every checkpoint was trained and selected. A source-only checkpoint shared by all methods is a defensible matched initialization. A proposed-model checkpoint already adapted to Acevedo is not equivalent to an ImageNet initialization for the baselines. If that checkpoint was selected using labeled target performance, its results cannot establish strict UDA. A shared ResNet backbone does not eliminate this problem. If Table 7 represents three independently trained models, say so; repeatedly evaluating one recovered checkpoint is not three independent training seeds.
2. **Figure 3 provenance.** The current stability figure is from the earlier local runs, while Table 7 is described as new checkpoint-based results. Similar appearance does not make them the same experiment. Regenerate the plot from the exact histories used for Table 7. Alternatively label and move the old figure to supplementary diagnostic experiments with its separate protocol; do not use it to substantiate the new runs' stability.
3. **Figure 2 versus Table 3.** The displayed Raabin diagonal is approximately 0.92, 0.82, 0.97, 0.67, 0.88, implying macro recall about 85.2%, whereas Table 3 reports recall 87.55%. That recall may be weighted rather than macro; define it. More importantly, multiplying the rounded row-normalized matrix by Table 1 supports and renormalizing its rows yields approximate macro-F1 79.3%, far from Table 3's 88.18%. This reconstruction is approximate, not a replacement score. Regenerate raw-count and normalized matrices and all metrics from the same predictions. Two-decimal matrix rounding should not explain a discrepancy of this size.
4. **Inference convention.** Table 7 does not specify whether each row uses TTA. State one-view or five-view for every row; if both are included, separate them. Table 3/4 single-checkpoint scores and Table 7 means can differ legitimately, but identify the representative checkpoint and explain that distinction explicitly. Do not combine TTA and non-TTA entries in one unnamed protocol.
5. **Data counts.** Table 1 lists 1,108 train/200 validation, whereas the earlier cleaned local protocol used 1,102/198 after removing eight duplicate source images. Confirm the actual rerun manifest and report those counts. Do not silently restore known train/test duplicates to recover a preferred score.
6. **Architecture and optimizer disclosure.** Existing local baselines use average pooling and Adam; the proposed model uses GeM, branches and AdamW. Its source-validation performance additionally informs the controller. Therefore do not call all architectures, optimization settings or validation use identical. These are local adaptations of baseline mechanisms, not exact official reproductions. Include an architecture-matched source-only model before attributing the full gain to adaptation.
7. **Method description.** The code previously inspected uses two draws from the same augmentation family, not separately demonstrated morphology/style views. Keep that description unless the rerun implementation actually changed. The proposed model uses alternating discriminator training and encoder domain-confusion updates, not the DANN gradient-reversal implementation. The rounded 45% pseudo-label cap can permit 4/8=50% of a minibatch. Figure 1's claim that the controller changes the pseudo-label threshold needs implementation evidence; the inspected implementation adjusts objective weights with a fixed configured threshold.
8. **Seed statistics.** Table 7's DANN Acevedo mean F1 25.56% ± 7.97 does not match either earlier local aggregate (23.41% ± 8.53 without TTA; 23.56% ± 7.97 with TTA). Reruns may legitimately differ, but export the whole table programmatically from the new prediction files. Do not update means separately from SDs. Specify whether SD uses the sample convention across three independent trainings.

## Places that still read as unfinished experiments

| Location in revised PDF | Existing wording/problem | Suggested replacement |
|---|---|---|
| p.2, Method, lines 100–102 | “we propose explicit probes in Sec. 4” but no probe results appear | “The penalty reduces cross-correlation between designated projections without establishing semantic disentanglement.” Remove the unfulfilled section reference. |
| p.2, Sec.4.2, lines 133–134 | “existing model's ... results” reads like an inherited draft | “Table 3 reports source-test, adapted-target, and external-transfer performance of the proposed model.” |
| p.2, Sec.4.3, lines 140–142 | “not yet controlled UDA baselines, planned to be included” contradicts Sec.4.5/Table 7 | “Table 6 evaluates backbone sensitivity; controlled comparisons with alternative UDA objectives are reported separately in Sec.4.5.” |
| p.3, Sec.4.4 | Empty subsection | Use the per-class draft, once Fig.2 matches the metrics. |
| p.3, Sec.4.5, lines 145–146 | One sentence introduces repeated seeds but offers no interpretation | Use the baseline protocol and result paragraphs. |
| p.3, Sec.4.6 | Empty subsection | Use the stability draft after regenerating Fig.3 from the reruns. |
| p.6, Discussion, lines 154–155 | “No repeated-seed uncertainty or controlled ... table is yet available” contradicts Table 7 | “Table 7 quantifies training-seed variability and comparison with local UDA baselines; the cumulative ablation does not isolate individual component effects.” |
| p.6, Discussion, lines 157–160 | “Before submission ... should be audited” is an internal action item | Replace with a factual description of the audit if completed. Otherwise state the unresolved limitation, e.g. “Patient/specimen independence could not be established from the available metadata.” Do not claim completed auditing without evidence. |
| p.6, Conclusion, lines 165–167 | Says controlled baselines and repeated trials are still necessary, despite reported results | Summarize completed comparative evidence, then limit remaining work to mechanism isolation, stronger baseline validation and broader/grouped evaluation. |

Related Work lines 83–85 may discuss foundation-model approaches as future work, but there is no need to promise a comparison. A concise alternative: “Foundation-model adaptation and test-time adaptation use different pretraining resources or access assumptions and are distinct from the source-accessible setting considered here.”

## Other wording and presentation changes

- Table 3/Figure 2: replace “validation” with “test/evaluation” when referring to source test, final adapted-target evaluation and external testing. Source validation is a different split used in training decisions.
- Table 7: correct “Controled” to “Controlled”; more precisely describe it as “Comparison with local ResNet50 UDA reimplementations.”
- Table 5: say “cumulative ablation” in the caption. Its 4.53 pp target-F1 drop after removing pseudo-labeling is an observed configuration contrast. Subsequent cumulative drops do not estimate independent alignment/controller effects.
- Table 6: ResNet50 exceeds EfficientNetB0 by 1.32 pp Acevedo F1, 2.64 pp Raabin F1 and 2.62 pp AML F1. Describe this as backbone sensitivity of the evaluated configurations, not an isolated causal backbone effect without matched settings and repeated seeds.
- Table 4: delta values are fractional F1 units. 0.0329 corresponds to 3.29 percentage points; make the unit explicit.
- Keep percentages consistent: 0.9057 is 90.57%; the target gap versus 0.7903 is 11.54 percentage points, not an 11.54% relative improvement.
- Do not say “statistically significant” without an appropriate test. Three seed SDs do not establish patient-level uncertainty or clinical reliability.

## Strongest defensible reading of Table 7 (conditional on verified protocol)

The proposed row has the highest mean macro-F1 on Acevedo (90.57%), Raabin (82.72%) and AML (74.66%). Relative to the strongest listed baseline on each of those domains, the margins are 11.54, 20.92 and 16.00 percentage points, respectively. Source-only is that baseline in all three domains. These are descriptive mean gaps, not significance tests.

The proposed model does NOT have the best source-test macro-F1 (98.51% versus MCD 99.11%). Acevedo SD remains 10.65 pp, larger than source-only 3.09 pp. Raabin F1 SD is 4.99 pp but accuracy SD is 12.56 pp: stability depends on the metric. AML F1 SD is only 0.54 pp, supporting a focused observation of repeatable performance on that dataset rather than universal stability.

Figure 2 suggests monocyte recall is about 67% on Raabin and 45% on AML; acknowledge this class-specific weakness. Do not infer precision from row-normalized diagonals or invent morphological causes from the confusion matrix alone.

## Draft usage

`recommended_replacements.tex` contains concise replacement text for Abstract, comparison protocol, Secs.4.4–4.6, Discussion and Conclusion. Numerical comparison statements are conditional on the revised Table 7 being verified. Bracketed protocol fields require the rerun configurations; the stability prose requires a regenerated figure. Preserve the original PDF and update its LaTeX source rather than editing the PDF in place.
