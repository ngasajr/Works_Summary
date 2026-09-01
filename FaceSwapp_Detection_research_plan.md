# RegionSwap-Guard: research and submission plan

## 1. Scope and conference fit

AID 2026 is an in-person IEEE PRDC workshop in Hong Kong SAR, 2–4 December
2026. The supplied call lists AI-based attack detection, AI model attacks and
defenses, AI dependability, and responsible/trustworthy AI. A regular paper is
the right track only after completed evaluation; otherwise use the R&D track.
The submission is double-blind, IEEE double-column, and at most six pages
including references. The supplied CFP gives 11 September 2026 (AoE) as the
submission deadline, 9 October notification, and 20 October camera-ready.

## 2. What changes from the supplied material

The notebook is a two-image OpenCV baseline: dlib 68-point landmarks, Delaunay
triangles, affine warping, and Poisson seamless cloning. It has no learned
identity representation, regional latent space, training loop, discriminator,
or detector. The slide deck proposes diffusion, concatenation, a generator, and
a discriminator, but does not specify supervision or a falsifiable novelty.

E4S (CVPR 2023) is the technical baseline: it reenacts the source toward the
target, parses both faces, encodes per-region texture/style, swaps semantic masks
and selected regional codes, and injects them into a pretrained StyleGAN. This
project retains explicit shape/texture regions but makes the forensic signal a
first-class output.

## 3. Proposed contribution

**RegionSwap-Guard (RSG)** has two independently evaluated components:

1. **RegionSwap generator.** A source and target are parsed into K semantic
   regions. Region-wise pooled source appearance codes are injected into a
   target-conditioned decoder. A user vector `a in [0,1]^K` selects full or
   partial swaps. The target parsing supplies shape/pose; source region codes
   supply selected appearance/identity. The generator also returns an exact
   soft manipulation map.
2. **Guard detector.** A dual-domain encoder processes RGB and fixed high-pass
   residuals. It predicts authenticity, a pixel manipulation map, and the
   manipulated region vector. Localization discourages shortcut learning from
   background, identity, or one codec.
3. **Detached hard-negative curriculum.** RSG samples are added to detector
   training with their known masks. Detector gradients never update the
   generator. This is crucial: an end-to-end adversarial discriminator would
   train the generator to hide forensic evidence and would not establish
   general detector robustness.

The defensible novelty claim is: **controlled regional synthesis supplies
accurate, diverse localization labels and improves cross-manipulation detection
under compression.** It must be accepted or rejected by held-out experiments.

## 4. Model formulation

For source `x_s`, target `x_t`, label maps `m_s,m_t`, and region selector `a`,
the appearance encoder produces a feature map `F_s`. Masked pooling gives

`z_s^k = sum_p F_s(p) 1[m_s(p)=k] / (sum_p 1[m_s(p)=k] + eps)`.

Target features and `m_t` condition a decoder. At every scale, regional affine
parameters modulate normalized activations only inside selected target regions:

`h' = sum_k m_t^k * ((1-a_k) h + a_k (gamma_k(z_s^k) norm(h)+beta_k(z_s^k)))`.

The output and manipulation prior are

`x_hat = G(x_s,x_t,m_s,m_t,a)`,
`q = clip(sum_k a_k m_t^k,0,1) * |x_hat-x_t|_channel_mean`.

Train the generator with

`L_G = lambda_rec L1 + lambda_id (1-cos(phi(x_hat),phi(x_s))) +`
`lambda_perc L_perc + lambda_bg ||(1-q)(x_hat-x_t)||_1 +`
`lambda_mask Dice(q, stopgrad(change_target)) + lambda_adv L_adv`.

The lightweight code implements reconstruction, background, total-variation,
and optional embedding terms; publication experiments should plug in frozen
ArcFace and LPIPS features and a PatchGAN critic.

The detector predicts `(y_hat, q_hat, a_hat)=D(x)`. Its loss is

`L_D = BCE(y_hat,y) + lambda_loc [BCE(q_hat,q)+Dice(q_hat,q)] +`
`lambda_region BCE(a_hat,a) + lambda_cons ||D(T1(x))-D(T2(x))||`,

where `T` samples JPEG quality, resize, blur, noise, color, and re-encoding.

## 5. Data

Recommended use:

| Purpose | Dataset | Use |
|---|---|---|
| Generator pretraining | FFHQ or CelebA-HQ | Consented/licensed still-image appearance diversity; generate identity-disjoint pairs. |
| In-domain detector train | FaceForensics++ | Real plus DeepFakes, Face2Face, FaceSwap, NeuralTextures; masks and compression levels. |
| Hard negatives | RSG outputs from training identities only | Exact region/change masks and selector labels. |
| Cross-dataset test | Celeb-DF v2 | Never tune thresholds on its test set. |
| Cross-method test | FaceShifter and DeeperForensics-1.0 | Unseen generator and perturbation robustness. |
| Large stress test (resources permitting) | DFDC | Demographic, capture, and compression diversity. |

Access is not always click-to-download: FaceForensics++ requires accepting its
terms. Check every dataset's current license. Split by original video and
identity before extracting frames. Sample at most a few frames per track per
epoch so adjacent frames do not dominate.

## 6. Training procedure

1. Align faces consistently, retain the inverse transform, and create six-class
   parsing masks with a frozen parser. Audit failures manually on a fixed subset.
2. Train generator self-reconstruction (`source=target`, random regions), then
   paired same-identity reconstruction, then different-identity swapping. Freeze
   identity/perceptual networks. Use AdamW, mixed precision, EMA, and early stop
   on identity/pose/background metrics, not pixel loss alone.
3. Freeze the selected generator checkpoint. Pre-generate RSG training samples
   or generate them on the fly under `no_grad`; store source/target hashes,
   selector, mask, and checkpoint ID.
4. Train detector on balanced real/external-fake/RSG batches. Apply independent
   post-processing twice for consistency. Tune threshold only on validation.
5. Lock code and seeds, then run held-out and cross-dataset tests once. Report
   mean and 95% bootstrap confidence intervals over videos, with three seeds.

## 7. Evaluation and ablations

Generator: ArcFace identity similarity to source, pose/expression error to
target, LPIPS/SSIM on self-reconstruction, background L1, FID/KID (with sample
count disclosed), and human preference with consent. Report full and regional
swaps separately.

Detector: video-level ROC-AUC, PR-AUC, EER, balanced accuracy, TPR at 1% FPR,
ECE/Brier calibration, pixel IoU/F1, and inference cost. Report raw, JPEG
Q={90,70,50}, resize, blur, noise, and combinations.

Required ablations:

- RGB only vs residual only vs dual-domain;
- classification only vs classification+localization+region prediction;
- no RSG augmentation vs random RSG vs detector-loss hard-negative sampling;
- global swapping vs regional codes; without mask modulation;
- classical notebook warps, E4S outputs, and RSG outputs as training negatives;
- identity-disjoint vs accidental frame-level split (the latter only to expose
  leakage, not as a headline result).

## 8. Six-page paper organization

1. **Introduction (0.6 page):** threat, dependability motivation, gap, three
   concise contributions.
2. **Related work (0.5):** regional face swapping, diffusion/GAN inversion,
   manipulation detection/localization.
3. **Method (1.5):** generator, known-mask construction, detector, objectives.
4. **Experimental setup (0.8):** datasets/splits, metrics, baselines, ethics.
5. **Results (1.5):** main cross-dataset table, robustness plot, localization,
   ablation. Never call a result SOTA without matching protocols.
6. **Limitations/conclusion (0.4):** demographic bias, unseen generators,
   parser dependence, image-only limitation, misuse safeguards.
7. **References (0.7):** fit within the six-page inclusive limit.

Suggested title: **RegionSwap-Guard: Region-Supervised Hard Negatives for
Robust Face Manipulation Detection**. Lead with detection dependability; the
generator is the controlled data engine, not the paper's end goal.
