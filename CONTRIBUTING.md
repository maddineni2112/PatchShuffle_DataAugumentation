# Contributing

Thanks for your interest in improving this project.

## Recommended workflow

1. Create a feature branch from `main`.
2. Keep experiments reproducible by documenting seeds, hardware, and library versions.
3. Do not commit CIFAR-10 downloads, checkpoints, caches, or generated environments.
4. Update the notebook and README when changing the augmentation pipeline or evaluation protocol.
5. Open a pull request with a concise description of the change and its effect on the comparison.

## Experiment reporting

When adding a new augmentation, report the same baseline settings and explain any changes to patch size, probability, optimizer, or training schedule. Avoid presenting unverified metrics as conclusions.
