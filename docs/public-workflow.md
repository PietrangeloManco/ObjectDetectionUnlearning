# Public Workflow Notes

This document summarizes the shareable part of the thesis workflow without reproducing the private research repository.

## Problem Framing

The core question was:

`How can machine unlearning be evaluated and implemented for object detection, where predictions combine class labels and localization?`

That requires more than deleting class-level information. The framework has to reason about:

- structured outputs
- bounding boxes
- retain / forget splits
- privacy-oriented audits
- preservation of overall utility

## Two Main Scenarios

### User Privacy

This scenario treats unlearning as a way to remove the influence of selected training samples from a detector, motivated by privacy regulations and deletion-oriented requirements.

### Resolving Confusion

This scenario treats unlearning as a correction tool for noisy or corrupted supervision, where the goal is to reduce the impact of misleading labels or annotations.

## Publicly Shareable Pipeline

The workflow can be described at a high level as:

1. Choose an object detector and a benchmark dataset.
2. Train an original baseline model.
3. Build a forget set and the corresponding retain set.
4. Apply an unlearning strategy.
5. Evaluate utility on retained data.
6. Evaluate forgetting behavior on targeted data.
7. Compare privacy-oriented signals and standard detection performance together.

## Publicly Shareable Technical Highlights

- Object detection metrics were part of the evaluation, not just classification-style scores.
- Forgetting behavior was not assessed only through performance drop, but also through MIA-oriented analysis.
- The framework supported repeatable experiments across datasets, models, and forget-set definitions.
- Experiment management, logging, and checkpointing were important parts of the practical work, not just the model definition itself.

## Boundaries

This public summary intentionally excludes:

- code copied from the original private repository
- exact implementation details for internal experiments
- checkpoints, weights, and raw logs
- private experimental notes and supervisor-owned repository content

The goal of this repository is to present the thesis direction and my contribution clearly, not to republish the supervised research environment.
