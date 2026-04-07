# Embedding Size Comparison Observations

This note compares two experiment groups with the same core setup:

- `max_features = 15000`
- `max_len = 300`
- `ff_dim = 256`
- tuning metric tracked: `acc_gap`
- selection type noted as: `min`

The only major change between the two groups below is the embedding size:

- Group A: `embed_dim = 128`
- Group B: `embed_dim = 64`

## Important observation

From these results, it is reasonable to say that the higher embedding dimension (`128`) performs better overall than `64`.

It is **not** valid to conclude that higher `ff_dim` performs better from this comparison alone, because `ff_dim` stayed fixed at `256` in both groups.

## Group A: `embed_dim = 128`

| num_heads | lambda | lr | batch | best_epoch | val_accuracy | val_loss | train_accuracy | train_loss | acc_gap | auc_gap |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 2 | 0.0002 | 0.0001 | 512 | 13 | 0.8668 | 0.4880 | 0.9129 | 0.4333 | 0.04615 | 0.01958 |
| 2 | 0.0001 | 0.0001 | 512 | 13 | 0.8742 | 0.4087 | 0.9107 | 0.3556 | 0.03655 | 0.01998 |
| 4 | 0.0002 | 0.0001 | 512 | 14 | 0.8722 | 0.4901 | 0.9254 | 0.4034 | 0.05320 | 0.02661 |
| 4 | 0.0001 | 0.0001 | 512 | 13 | 0.8724 | 0.4082 | 0.9114 | 0.3534 | 0.03895 | 0.01994 |
| 2 | 0.0002 | 0.0001 | 128 | 6 | 0.8734 | 0.4827 | 0.9068 | 0.4345 | 0.03340 | 0.01449 |
| 2 | 0.0001 | 0.0001 | 128 | 6 | 0.8708 | 0.4115 | 0.9050 | 0.3636 | 0.03420 | 0.01385 |
| 4 | 0.0002 | 0.0001 | 128 | 7 | 0.8704 | 0.4756 | 0.9223 | 0.3902 | 0.05190 | 0.02438 |
| 4 | 0.0001 | 0.0001 | 128 | 6 | 0.8700 | 0.4074 | 0.9064 | 0.3579 | 0.03640 | 0.01620 |

### Best runs inside Group A

| Factor | Best configuration | Why it stands out |
|---|---|---|
| Highest validation accuracy | `embed=128, heads=2, lambda=0.0001, lr=0.0001, batch=512` | Best `val_accuracy = 0.8742` |
| Lowest validation loss | `embed=128, heads=4, lambda=0.0001, lr=0.0001, batch=128` | Best `val_loss = 0.4074` |
| Smallest accuracy gap | `embed=128, heads=2, lambda=0.0002, lr=0.0001, batch=128` | Best `acc_gap = 0.03340` within this group |
| Smallest AUC gap | `embed=128, heads=2, lambda=0.0001, lr=0.0001, batch=128` | Best `auc_gap = 0.01385` |

## Group B: `embed_dim = 64`

| num_heads | lambda | lr | batch | best_epoch | val_accuracy | val_loss | train_accuracy | train_loss | acc_gap | auc_gap |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 2 | 0.0002 | 0.0001 | 512 | 16 | 0.8696 | 0.4477 | 0.9234 | 0.3598 | 0.05380 | 0.02836 |
| 2 | 0.0001 | 0.0001 | 512 | 15 | 0.8710 | 0.3879 | 0.9123 | 0.3232 | 0.04130 | 0.02258 |
| 4 | 0.0002 | 0.0001 | 512 | 14 | 0.8654 | 0.4469 | 0.9017 | 0.4183 | 0.03625 | 0.01448 |
| 4 | 0.0001 | 0.0001 | 512 | 14 | 0.8698 | 0.3824 | 0.9026 | 0.3496 | 0.03285 | 0.01515 |
| 2 | 0.0002 | 0.0001 | 128 | 7 | 0.8678 | 0.4455 | 0.9107 | 0.3830 | 0.04295 | 0.01964 |
| 2 | 0.0001 | 0.0001 | 128 | 5 | 0.8630 | 0.3935 | 0.8710 | 0.4123 | 0.00800 | -0.00344 |
| 4 | 0.0002 | 0.0001 | 128 | 7 | 0.8692 | 0.4454 | 0.9086 | 0.3836 | 0.03945 | 0.01922 |
| 4 | 0.0001 | 0.0001 | 128 | 6 | 0.8684 | 0.3846 | 0.8931 | 0.3659 | 0.02475 | 0.00800 |

### Best runs inside Group B

| Factor | Best configuration | Why it stands out |
|---|---|---|
| Highest validation accuracy | `embed=64, heads=2, lambda=0.0001, lr=0.0001, batch=512` | Best `val_accuracy = 0.8710` |
| Lowest validation loss | `embed=64, heads=4, lambda=0.0001, lr=0.0001, batch=512` | Best `val_loss = 0.3824` |
| Smallest accuracy gap | `embed=64, heads=2, lambda=0.0001, lr=0.0001, batch=128` | Best `acc_gap = 0.00800` |
| Smallest AUC gap | `embed=64, heads=2, lambda=0.0001, lr=0.0001, batch=128` | Best `auc_gap = -0.00344` |

## Best configurations across both groups

| Factor | Best overall configuration | Value |
|---|---|---:|
| Highest validation accuracy | `embed=128, heads=2, lambda=0.0001, lr=0.0001, batch=512` | `0.8742` |
| Lowest validation loss | `embed=64, heads=4, lambda=0.0001, lr=0.0001, batch=512` | `0.3824` |
| Smallest accuracy gap | `embed=64, heads=2, lambda=0.0001, lr=0.0001, batch=128` | `0.00800` |
| Smallest precision gap | `embed=64, heads=2, lambda=0.0001, lr=0.0001, batch=128` | `-0.00034` |
| Smallest recall gap | `embed=64, heads=2, lambda=0.0001, lr=0.0001, batch=128` | `0.00945` |
| Smallest AUC gap | `embed=64, heads=2, lambda=0.0001, lr=0.0001, batch=128` | `-0.00344` |

## Is there a single overall best?

There is no single best run for every metric.

The answer depends on what "best" means:

- If you care most about **highest validation accuracy**, the best run here is:
  - `embed=128, heads=2, lambda=0.0001, lr=0.0001, batch=512`
- If you care most about **lowest overfitting gap**, the best run here is:
  - `embed=64, heads=2, lambda=0.0001, lr=0.0001, batch=128`
- If you care most about **lowest validation loss**, the best run here is:
  - `embed=64, heads=4, lambda=0.0001, lr=0.0001, batch=512`

## Recommended overall choice

If the goal is to choose the strongest and most practical model from these results, the best overall candidate is:

`embed=128, heads=2, lambda=0.0001, lr=0.0001, batch=512`

Why:

- It has the **highest validation accuracy** of all runs: `0.8742`
- Its validation loss is also competitive: `0.4087`
- Its generalization gaps are moderate and not the worst in the sweep
- It gives a better balance between performance and overfitting than the extreme low-gap run

## Why the minimum `acc_gap` run is probably not the overall best

The run:

`embed=64, heads=2, lambda=0.0001, lr=0.0001, batch=128`

has the smallest `acc_gap = 0.00800`, but it also has:

- lower `val_accuracy = 0.8630`
- higher `train_loss = 0.4123` than several stronger runs
- a positive `loss_gap = 0.01877`, which suggests it may be slightly underfit rather than ideally balanced

So it is the best **regularized / least-overfit-looking** run, but not the best **performing** run.

## Final conclusion

- `embed_dim = 128` looks better overall than `embed_dim = 64` in this comparison
- `lambda = 0.0001` is consistently stronger than `0.0002` across the best runs
- `num_heads = 2` appears more reliable than `4` when using validation accuracy as the main selection metric
- `batch_size = 512` gives the best validation accuracy in these experiments

If your assignment values generalization balance more than raw validation accuracy, you can also mention the low-gap `embed=64, heads=2, lambda=0.0001, batch=128` run as the most conservative choice.
