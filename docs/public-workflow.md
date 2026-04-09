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

## High-level pipeline

<table>
  <tr>
    <th align="center" width="25%">Baseline detector</th>
    <th align="center" width="25%">Forget/retain split</th>
    <th align="center" width="25%">Unlearning strategy</th>
    <th align="center" width="25%">Scenario control</th>
  </tr>
  <tr>
    <td align="center">Train or load the original detector that defines the reference utility level.</td>
    <td align="center">Build the forgetting setup and the complementary retain split for the target experiment.</td>
    <td align="center">Run retraining or approximate unlearning methods on the detector.</td>
    <td align="center">Frame the run around either privacy-driven deletion or confusion-removal objectives.</td>
  </tr>
  <tr>
    <th align="center" width="25%">Utility audit</th>
    <th align="center" width="25%">Forget-set audit</th>
    <th align="center" width="25%">Privacy check</th>
    <th align="center" width="25%">Trade-off reading</th>
  </tr>
  <tr>
    <td align="center">Measure retained detection quality with object-detection metrics such as mAP and IoU.</td>
    <td align="center">Inspect the targeted data to verify that the removed influence no longer behaves like the original model.</td>
    <td align="center">Use MIA-style signals as an additional privacy-oriented check rather than relying only on accuracy shifts.</td>
    <td align="center">Compare forgetting effectiveness and retained utility together instead of optimizing only one side.</td>
  </tr>
</table>

In practice, the public-safe workflow can be summarized as:

1. Choose an object detector and a benchmark dataset.
2. Train an original baseline model.
3. Build a forget set and the corresponding retain set.
4. Apply an unlearning strategy for the selected scenario.
5. Evaluate retained performance, forgetting behavior, and privacy-oriented signals together.

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
