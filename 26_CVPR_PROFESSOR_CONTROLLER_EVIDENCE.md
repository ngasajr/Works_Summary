# Evidence addressing the controller questions

## How many model runs and policy updates?

**54 model-training runs completed** (18 configurations × three seeds). One configuration uses a learned policy and was repeated across three seeds: **3 learned-policy runs ×45 optimizer updates =135 actual policy-parameter updates**. Other configurations have0 learned-policy optimizer updates. The12 frozen diagnostic runs and engineering smoke tests are not additional full training runs.

| Weighting condition | Model runs | Action vectors per run | Total vectors | Policy optimizer updates |
|---|---:|---:|---:|---:|
| Fixed OD reference | 3 | 0 | 0 | 0 |
| Deterministic heuristic | 3 | 0 | 0 | 0 |
| Uniform random weighting | 3 | 45 | 135 | 0 |
| Learned stochastic weighting | 3 | 45 | 135 | 135 |

The combined count of270 sampled vectors includes135 random-control vectors. It is not270 learned-policy actions. Each vector contains five categorical selections, giving675 learned-policy selections and675 random-control selections.

Across all54 runs, **2,295 adaptation epochs** were checked for coefficient consumption (51 adaptation runs ×45; three source-only runs have none). Logged weighted-loss reconstruction errors are below3e-8 in this completed cohort.

## From which distribution were actions sampled?

The learned network takes six state statistics, uses32 tanh units and outputs five categorical distributions over factors **0.90,0.95,1.00,1.05,1.10**. Actions are sampled independently conditional on the state. The five implemented keys are classification, adversarial, orthogonality, alignment and morphology-contrastive loss. Multipliers are smoothed and bounded before use. Agreement and pseudo-label coefficients remain fixed.

`controller_trace.json` saves the full probabilities, selected actions, multiplier values, states and resulting weights. The random control samples uniformly over the same five factors. It is not a frozen copy of the initial learned network.

## Were the lambdas used in the model loss?

**Yes, in the new controlled implementation.** Each action specifies the coefficients consumed by every minibatch of the associated adaptation epoch. Each epoch then supplies source-validation and unlabeled adaptation statistics for a REINFORCE update; a subsequent action is sampled and consumed by the next epoch. The analysis verifies equality between sampled/applied and consumed coefficients, and reconstructs the actual optimized total from weighted loss terms.

Every learned update has a logged nonzero gradient norm and parameter delta. The first update in each run has zero centered reward advantage and can update entropy regularization;44 later updates per run have nonzero reward advantages. The terminal update is recorded but has no subsequent model-training epoch. Optimizer updates should therefore not be confused with135 feedback transitions that all affect later training.

## What this evidence does and does not establish

It establishes actual policy optimization, stochastic action sampling and a closed epoch-level feedback loop for the new implementation. It does **not** establish that the recovered historical checkpoint used a learned policy. The inspected recovered controller is deterministic, and its historical script uses labeled-target and source-test feedback. Those historical facts must remain distinct from the new strict-UDA cohort.

The learned policy improves the two external means over the matched source-only control, while lowering Acevedo performance. It does not consistently beat fixed, heuristic or random weighting. Implementation evidence is therefore stronger than the evidence for a general performance benefit from learning the policy.

## Supporting artifacts

- [Actual per-run controller counts](controller_audit.csv)
- [Completed-results analysis](RESULTS_ANALYSIS.md)
- [Registered protocol](../PROTOCOL.md)
- Per-run controller traces, batch traces, policy weights and final optimizer checkpoints under `../results/controller_learned/seed_42`, `seed_43`, and `seed_44`.

![Feedback evidence: seed42](policy_closed_loop_seed42.png)

![Feedback evidence: seed43](policy_closed_loop_seed43.png)

![Feedback evidence: seed44](policy_closed_loop_seed44.png)
