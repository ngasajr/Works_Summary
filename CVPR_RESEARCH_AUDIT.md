# Experimental and manuscript audit — 6 November 2026

The highest-priority issue is validity and provenance, ahead of additional plots. The current manuscript cannot support strict unsupervised adaptation or performance superiority using the supplied evidence. This is fixable, but additional experiments cannot guarantee CVPR acceptance. The experimental program below is a research recommendation, not a formal CVPR checklist.

## Findings in this workspace

1. **Target-label supervision during adaptation.** `rl_two_view_hybrid_policy_rl_orthogonal_domain_adaptation_wbc.py`, training lines around 1134–1198, evaluates labeled target data every epoch. Target macro-F1 and minimum recall enter controller state/reward and the default `target_balanced` checkpoint score. Setting `source_domain` alone is insufficient: target-supervised reward remains, and source-test metrics influence its source-generalization term. A model whose loss weights learn from target labels is not strict UDA, even when backpropagation sees only target images. Do not relabel old results as strict UDA.
2. **Train/Test duplication.** Exact decoded pixels match between `data/Train/eosinophil/SCHBC_PB2_03 (50).jpg` and `data/Test/eosinophil/SCHBC_PB2_03 (45).jpg`. The audit found eight duplicate groups in total, no decoding errors, and one cross-domain group (Train/Test). The derived `cvpr_data` view removes eight redundant source training images. It does not alter the evaluation images. Counts must change in the paper; patient/slide independence remains unverified.
3. **Manuscript/report mismatch.** The only supplied hybrid run's saved JSON metrics differ from Table 3:

| Domain | Manuscript accuracy / macro-F1 | Supplied saved run accuracy / macro-F1 |
|---|---:|---:|
| SCHBC | 98.48 / 98.47 | 97.26 / 97.26 |
| Acevedo | 93.07 / 93.07 | 91.73 / 91.71 |
| Raabin | 87.55 / 88.18 | 66.35 / 58.43 |
| AML | 74.19 / 73.78 | 70.97 / 70.52 |

Values are percentages. Evidence: `rl_two_view_resnet50_hybrid_policy_rl_external_safe_raabin_aml/reports/{source_test,target,external_target_raabin,external_target_aml}_metrics.json`. This does not prove the manuscript numbers are wrong; it means their generating run is missing or unidentified. Resolve checkpoint/run hashes, predictions, split manifest and metric definitions before publication. Never combine rows from different runs without disclosure.
4. **Hyperparameter mismatch.** The PDF describes 0.95 confidence, 45% cap and eight controller-inactive epochs. The stored run config has 0.96 confidence, 37.5% cap and policy warmup 10. New defaults follow the manuscript's confidence/cap, but the new controller/protocol are explicitly different. Explain which experiment every configuration supports.
5. **The two views are not morphology/style-specific implementations.** Both use `MedicalAugmentation`. In shared-encoder mode `_encode_b` calls `encoder_a`, whose augmentation is `augmentation_a`; the separately created `augmentation_b` is unused. Two random draws can still aid consistency, but they do not validate the semantic view names. At inference both views encode the same image, so diversity comes from classifier heads, not two distinct morphology/style image transformations.
6. **The adversarial implementation is domain confusion, not a gradient-reversal layer.** It trains a discriminator on style features, then trains the encoder to confuse it. Describe the actual loss and branch. Confusing a style branch also conflicts with a strong claim that it explicitly retains domain information; probe it rather than assuming its semantics.
7. **Metric definitions matter.** With 2,660/4,339 neutrophils, Raabin accuracy is dominated by neutrophils. A table that reports recall equal to accuracy may be using weighted/micro recall; label each metric precisely. Use macro-F1 and balanced accuracy as primary metrics and inspect class supports. The PDF's AML confusion matrix shows weak monocyte recall (approximately 0.45), which is worth a focused error analysis; it is not a validated new-run finding.

## Related CVPR papers and what to learn from them

Sources below are CVF proceedings pages/abstracts, with available full text for LEAD and the evaluation-protocol paper. Some PDF requests returned 403. The review therefore supports conceptual and protocol comparisons; it does not claim an exhaustive reproduction of their experimental settings. Search included 2026 proceedings as well as older direct baselines.

| Paper | Relationship to your idea | Experiment or discussion it motivates | Comparison boundary |
|---|---|---|---|
| [MCD, CVPR 2018](https://openaccess.thecvf.com/content_cvpr_2018/html/Saito_Maximum_Classifier_Discrepancy_CVPR_2018_paper.html) | Two classifiers and target feature alignment | Compare agreement-based two heads against discrepancy maximization/minimization under the same backbone and data | Direct closed-set source-accessible UDA baseline; local implementation added |
| [Contrastive Adaptation Network, CVPR 2019](https://openaccess.thecvf.com/content_CVPR_2019/html/Kang_Contrastive_Adaptation_Network_for_Unsupervised_Domain_Adaptation_CVPR_2019_paper.html) | Class-structured contrastive adaptation | Stronger class-aware adaptation comparison; distinguish source-only supervised contrastive loss from cross-domain class-aware alignment | Official implementation still needs integration and WBC reruns |
| [LEAD, CVPR 2024](https://openaccess.thecvf.com/content/CVPR2024/html/Qu_LEAD_Learning_Decomposition_for_Source-free_Universal_Domain_Adaptation_CVPR_2024_paper.html) | Explicit decomposition and orthogonal geometry | Quantify decomposition utility; probe branches; report efficiency | LEAD separates known/unknown components in source-free universal DA, not morphology/style in closed-set UDA. Its reported VisDA H-score gain is not comparable to your WBC accuracy |
| [Discriminative Pattern Calibration, CVPR 2024](https://openaccess.thecvf.com/content/CVPR2024/html/Xia_Discriminative_Pattern_Calibration_Mechanism_for_Source-Free_Domain_Adaptation_CVPR_2024_paper.html) | Preserving relevant visual evidence across shift | Region localization, perturbation/occlusion controls and failure examples | Source-free setting; attention is supporting evidence, not proof of morphology |
| [Disentangled Prompt Representation, CVPR 2024](https://openaccess.thecvf.com/content/CVPR2024/html/Cheng_Disentangled_Prompt_Representation_for_Domain_Generalization_CVPR_2024_paper.html) | Invariant/domain-specific factors | Separate factor semantics and show class retention/domain suppression | CLIP/prompt DG has different pretraining and target access; compare in a separate resource tier |
| [Rethinking the Evaluation Protocol of DG, CVPR 2024](https://openaccess.thecvf.com/content/CVPR2024/papers/Yu_Rethinking_the_Evaluation_Protocol_of_Domain_Generalization_CVPR_2024_paper.pdf) | Selection and leakage risks | Declare model selection, multiple external domains and pretraining assumptions | Your main setting remains UDA plus external transfer, not source-only DG |
| [StyleMix, CVPR 2021](https://openaccess.thecvf.com/content/CVPR2021/html/Hong_StyleMix_Separating_Content_and_Style_for_Enhanced_Data_Augmentation_CVPR_2021_paper.html) | Separating content and style through augmentation | Compare against a simpler content/style augmentation control and ordinary two stochastic views | Augmentation method, not a matched UDA result by itself |
| [Preserving Clusters in Prompt Learning for UDA, CVPR 2025](https://openaccess.thecvf.com/content/CVPR2025/html/Vuong_Preserving_Clusters_in_Prompt_Learning_for_Unsupervised_Domain_Adaptation_CVPR_2025_paper.html) | Pseudo-label/self-training and cluster preservation | Include a recent strong adaptation method and distinguish pretraining benefits from adaptation benefits | CLIP resource tier; add zero-shot and self-training controls if implemented |
| [VLM Guided Source-Free DA via Optimal Transport, CVPR 2026](https://openaccess.thecvf.com/content/CVPR2026/html/Han_Vision-Language_Model_Guided_Source-Free_Domain_Adaptation_via_Optimal_Transport_CVPR_2026_paper.html) | Pseudo-label noise, semantic priors, alignment | Update related work beyond 2024/2025; analyze confidence-quality and strong VLM guidance | Source-free + VLM resources; retrieved proceedings abstract describes four benchmark datasets. Not implemented here |

Do not copy literature accuracies into a WBC leaderboard: class sets, datasets, backbones, label access and metrics differ. Numerical performance comparison requires rerunning each algorithm on your frozen WBC protocol, or running your method on the exact public benchmark protocol of the comparison paper. DANN and Deep CORAL are useful standard controls but are ICML 2015 and ECCV Workshops 2016, respectively, not CVPR papers.

## Experiment priorities and implementation status

| Priority | Evidence needed | How to obtain it | Supplied implementation / remaining work |
|---|---|---|---|
| P0 | Valid data and selection protocol | Remove duplicates; establish patient/slide separation; fix target-supervised reward and checkpoint selection | Exact duplicate audit, clean data view and strict runner supplied. Group metadata still needed |
| P0 | Matched baseline gains | Source-only 80 epochs and 35-epoch reference; DANN, CORAL, MCD; full/fixed model, same split/seeds/backbone | `train.py`, `suite.py`; local classical baselines, not official reproductions |
| P0 | Repeatability | 3 seeds minimum; 5 preferred; same data membership; report mean ± SD | Suite seeds 42/43/44 and analysis supplied |
| P1 | Independent component effects | Full versus each single removal, same seeds; no cumulative causal attribution | Orthogonality, contrastive, adversarial, CORAL, pseudo-labeling, agreement and shared single-head controls supplied |
| P1 | Controller necessity | Full versus fixed, linear schedule; source-val reward only; show weight/reward trajectories and time | Fixed/scheduled supplied. Uncertainty weighting/GradNorm, random and heuristic-only controller controls still need implementations |
| P1 | Morphology claim | True distinct view definitions; ordinary-augmentation, geometry-only, style-only and grayscale controls; expert review | Current symmetric view implementation is preserved honestly. Semantic view controls not implemented; revise claims or implement before submission |
| P1 | Minority-class performance | Five class F1/recall, balanced accuracy, confusions; failure gallery, especially AML monocytes | Tables/calibration/confusions supplied; expert failure gallery and biological explanations need review |
| P1 | Representation semantics | Source-trained class probes for morphology/style/alignment branches; class-balanced domain probes; compare with no-orthogonality; report cross-correlation | Frozen branch export, source-trained class probes, class-conditional domain probes and branch correlations supplied. Localization ground truth remains |
| P1 | Confidence quality | Offline pseudo-label precision/coverage per class and epoch; no feedback into training; calibration plots | Final ECE/NLL/Brier supplied. Per-epoch pseudo-label precision requires saved frozen epoch predictions/checkpoints; not currently supplied |
| P1 | TTA contribution | All methods with identical 1-view and 5-view inference; separate gain and cost | Final prediction exports supplied; preserve no-TTA main table |
| P1 | Broader validity | Multiple WBC directions and a standard nonmedical UDA benchmark if claiming general vision contribution | New label-blind data adapters/protocols needed; current runner is five-class WBC only |
| P2 | Robustness and tuning stability | Confidence × cap grid, fixed stain/acquisition perturbations, no target-label configuration choice | Grid + brightness/contrast/saturation/noise supplied. These are custom diagnostics, not a standard benchmark |
| P2 | Efficiency | Parameters, training wall time, GPU peak allocation, TTA wall time; same hardware/settings | Recorded by runner. Add warmup/synchronized latency throughput measurements for publication |
| P2 | Label/target data efficiency | Source labels 10/25/50/100%, target images 10/25/50/100%, fixed nested subsets and seeds | Subset manifest support still needed; do not emulate by changing minibatch counts |

The suite is a substantial starting implementation, not every experiment above. It is especially important to add a modern official method, patient independence, real view-specific controls, and a second adaptation task before claiming a broad methodological advance.

## Defensible statistics and selection

Freeze one protocol before looking at target/external scores. Use only source validation for selection in the supplied strict runner. Hyperparameter comparisons must have equal search budgets and the same allowed selection signal across methods. Reporting a target-label sensitivity grid is post-hoc analysis, not permission to pick its best cell. Labels for external datasets must never guide reward, early stopping, hyperparameters or manuscript variant choice.

Separate training-seed SD from test-sample uncertainty. The supplied bootstrap assumes independent cells and conditions on one model. Once patient/slide IDs are available, replace it with grouped bootstrap and group-aware splitting/probes. For paired model comparisons, use identical test image IDs and seeds, report macro-F1 effect size/interval, and optionally exact McNemar for accuracy. Do not imply a small p-value establishes clinical benefit. Correct multiple comparisons when needed.

## Organizing the manuscript

Use the experimental section to answer a sequence of concrete questions:

1. **Protocol and implementation:** label-space harmonization; acquisition and patient/slide information; exact splits and duplicate handling; what target images are accessible; ImageNet pretraining; checkpoint and controller signals; exact transformations; all optimizer/loss settings. Explain the new source-validation controller explicitly.
2. **Main comparison:** source-only and matched UDA baselines on Acevedo, plus separate columns for external Raabin/AML; accuracy, macro-F1, balanced accuracy, mean ± SD; without TTA first. Mark source-free/VLM methods in separate tiers with resource/access details.
3. **Component and controller analysis:** individual removals with matched seeds; full versus fixed/scheduled; coefficient trajectories; compute cost. State when component gains are small, variable or domain-dependent.
4. **Mechanism:** representation probes, morphology localization if masks exist, augmentation examples, pseudo-label precision/coverage, and class-wise errors. Orthogonality is a regularizer, not a semantic proof.
5. **Robustness and efficiency:** perturbation curves, label/target efficiency when implemented, runtime/parameters/memory, TTA accuracy-cost tradeoff.
6. **Failure analysis and limitations:** AML monocyte confusions, remaining stain sensitivity, cell-level versus patient-level evidence, limited domains, class balance/selection, closed-set assumption and absent blast/open-set evaluation.

Suggested figures: protocol/access diagram; real view pairs; ablation plot with per-seed points; pseudo-label quality/coverage and controller traces; class-conditional domain-probe chart; fixed corruption severity curves; representative success/failure cells reviewed by a domain expert. t-SNE alone is insufficient mechanism evidence.

Discuss measured effects with numerical deltas and uncertainty: e.g., “Removing orthogonality changes macro-F1 by [measured delta] on [domain], with [interval]; the class probe shows [measured effect].” Keep placeholders until runs finish. A gain on Acevedo with loss on AML is a target-versus-external-transfer tradeoff to explain, not hide. If fixed weights match the controller, simplify the contribution. If the two views behave like ordinary augmentation, revise the title and mechanism accordingly.

Main text should contain the strongest completed evidence, not “TO RUN” tables or promised experiments. Move exhaustive settings, seed rows, extra confusions and sensitivity grids to supplementary material. Replace first-person planning statements in Sec. 4.1 with completed findings only. Retain a candid limitations section. Method novelty must be established beyond combining several established losses; a broad claim is stronger with a standard nonmedical benchmark and mechanism evidence, not simply more WBC tables.

## Practical next decision

Trace the manuscript's original run and supply patient/slide identities. Meanwhile complete the corrected baseline suite and use its results to decide whether the key contribution is supported. Do not combine the new decontaminated strict-UDA numbers with the old target-supervised scores as if they share a protocol.
