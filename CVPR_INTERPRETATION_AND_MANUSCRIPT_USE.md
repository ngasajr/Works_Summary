# How to use this evidence in the manuscript

## Evidence produced now

The three-seed frozen-model diagnostic study is complete for the proposed model and source-only comparator. It measures behavior on exactly the same hash-selected, class-balanced panel: 32 cells per class in each of four domains (640 images/model). It is a new mechanism analysis of the proposed model. Its balanced-panel F1 values are not interchangeable with whole-dataset scores in the manuscript.

1. **Input intervention figure:** combine `figures/intervention_examples.pdf` with `figures/appearance_structure_interventions.pdf`. Color interventions keep spatial layout; tile scrambling preserves the exact pixel histogram while destroying layout. Report all conditions, not only favorable ones. Different interventions have different severities, so the figure supports spatial dependence, not a calibrated biological shape-versus-style causal decomposition.
2. **Representation figure:** combine `figures/class_information.pdf` and `figures/domain_information.pdf`. Source-trained class probes show where class information remains decodable. Class-conditional, balanced domain probes reveal retained acquisition/domain information. Both sides of the result must appear together.
3. **Controlled-component table:** `controlled_summary.csv/.tex` and `controlled_paired_deltas.csv` are generated automatically as matched retraining finishes. These isolate removals relative to a newly trained full reference, using matching architecture, optimizer, data split, epoch budget and seeds. Do not fill incomplete cells with old or assumed results.
4. **Cost table:** use the dedicated `efficiency_summary.csv`, not exploratory timing from the diagnostic jobs. Report batch size, TTA, synchronization, warmup and timing repetitions. These measurements compare inference costs; training efficiency additionally requires the matched retraining costs in `controlled_cost.csv`.
5. **Backbone table:** compare full against matched-source within both ResNet50 and EfficientNetB0. A gain on both supports transfer across those two backbones, not unrestricted backbone independence.

## Completed input-intervention findings

On the class-balanced panels, proposed-model clean macro-F1 is 73.09 ± 10.89% on Acevedo, 72.23 ± 1.84% on Raabin and 67.49 ± 1.33% on AML. Under histogram-preserving spatial scrambling these scores fall to 10.94 ± 6.35%, 9.59 ± 5.07% and 7.46 ± 1.38%, respectively. Selected mild appearance changes have much smaller effects. This demonstrates reliance on spatial organization beyond a global color histogram. However, source-only models are also strongly affected; this alone does not establish the contribution of the proposed morphology objective.

Grayscale F1 is 52.20 ± 10.63%, 39.77 ± 11.37% and 33.46 ± 7.82%, versus source-only 38.82 ± 4.72%, 34.96 ± 11.28% and 30.30 ± 11.07%. These observations support partial retention of class-discriminative information without chromatic input, particularly on Acevedo. They do not imply color invariance: the proposed model still loses substantial performance relative to its clean input. In WBC images, staining can encode biologically useful granule/chromatin information as well as nuisance acquisition variation; grayscale is therefore not a perfect intervention on nuisance style alone.

## Representation finding that should remain a limitation

Class-conditional four-domain accuracy remains about 87.97% in the morphology branch and 88.59% in the style branch, against 25% chance. The style branch also supports strong cell-class decoding. The evidence does not establish semantically separated, domain-free morphology features. A narrower interpretation is that the framework learns useful, partially overlapping representations while retaining domain information. Orthogonality is a regularizer, not a guarantee of semantic disentanglement. The forthcoming no-orthogonality control can measure the regularizer's effect; it cannot retrospectively turn branch names into anatomical ground truth.

## Suggested Results paragraph (completed diagnostic study only)

> We examined morphology-related behavior using fixed-checkpoint interventions on a class-balanced panel of 32 cells per class per domain, shared across models and three training seeds. Spatial tile permutation preserves the pixel histogram while disrupting spatial organization. The proposed model's macro-F1 decreased from 73.09%, 72.23%, and 67.49% to 10.94%, 9.59%, and 7.46% on Acevedo, Raabin-WBC, and AML, respectively. In contrast, selected mild gamma and hue perturbations produced smaller changes. Grayscale inputs retained higher macro-F1 than the source-only comparator on all three panels, although substantial degradation remained. These results support dependence on spatially organized cues and partial robustness to appearance changes; the same destruction tests affect source-only models and do not independently establish the benefit of the morphology objective.

## Suggested representation paragraph

> Source-trained linear probes show that class information is retained in multiple projected representations. Class-conditioned, domain-balanced probes nevertheless decode domain identity from the morphology branch with 87.97% accuracy, well above 25% chance, and the style branch also retains class information. The learned branches therefore remain overlapping and domain-informative. These results support representation utility without establishing a semantic morphology/style decomposition.

## Suggested limitation update now

> Input interventions provide evidence that predictions depend on spatial organization and retain some class information after color removal. They do not establish anatomical localization or a nuisance-free morphology representation. Domain and class probes reveal residual overlap between the projected branches. Cell/nucleus annotations, patient-aware evaluation, and completed matched component controls are required for stronger semantic and mechanism claims.

## What changes only after controlled results finish

- Replace the cumulative-ablation limitation with measured one-factor deltas, including intervals/seed SD and any domains with losses. Do not call component effects additive or independent of controller interactions.
- Replace the cost limitation with measured latency/throughput/training-time tradeoffs, not a generic claim of efficiency.
- Replace the backbone limitation only to the extent supported by matched full/source results on each tested backbone.
- A paired bootstrap over panel cells conditions on one trained model and assumes independent cells. It does not solve missing patient/slide identities; three seed SDs and patient uncertainty are different quantities.

## Research context

The distinction between reduced appearance/style bias and generalization is consistent with the motivation of [Reducing Domain Gap by Reducing Style Bias (CVPR 2021)](https://openaccess.thecvf.com/content/CVPR2021/html/Nam_Reducing_Domain_Gap_by_Reducing_Style_Bias_CVPR_2021_paper.html). Region-level interpretation requires more than visually plausible attribution, as emphasized by [Sanity Checks for Saliency Maps](https://arxiv.org/abs/1810.03292). These sources motivate the diagnostic design; the measurements here are new WBC experiments and do not reproduce either paper's benchmark.
