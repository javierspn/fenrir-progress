---
layout: post
title: "First cohorts after the memory-consolidation rebuild"
---

Feature **003 — memory consolidation replay** is live: a faithful port of hippocampal two-stage
consolidation (significance bookmarking while awake → competitive replay during "sleep"). Ran two
back-to-back cohorts to see whether **reuse** lifts off zero while **escalation** and **cost** fall.

## The numbers

| Signal | 300-batch | 200-batch | Direction |
|---|---|---|---|
| Skills crystallized | 175 | — | grew from 56 |
| Abstractions | 352 | — | grew from 143 |
| Abstraction-reuse / day | 3 | **5** | ↑ |
| Retrieval-solve / day | 4 | **9** | ↑ |
| Escalation % | 98.4 | 98.2 | ~flat |
| Cost / cohort | $0.076 | $0.127 | — |

**Reuse lifted off zero and is climbing** (3→5, 4→9). That's the first real sign memory is being
*used*, not just stored.

## The honest part

Escalation is still stuck around **98%** — the small model almost always calls the teacher. That's
expected, not hidden: reuse can only pay off when consecutive tasks are *similar enough* for a prior
skill to apply, and the current curriculum draws problems at random. Next experiment biases the task
stream toward **skill-adjacent** problems so reuse becomes observable — then we watch whether
escalation finally bends down.

## Screenshots

<figure class="shot">
  <img src="{{ '/assets/img/PLACEHOLDER-overview.png' | relative_url }}" alt="Are we learning? dashboard">
  <figcaption>Grafana — "Are we learning?" overview (verdict tiles + curves). Drop a PNG to replace.</figcaption>
</figure>

<div class="grid">
  <figure class="shot">
    <img src="{{ '/assets/img/PLACEHOLDER-reuse.png' | relative_url }}" alt="reuse curve">
    <figcaption>Reuse / day over cohorts</figcaption>
  </figure>
  <figure class="shot">
    <img src="{{ '/assets/img/PLACEHOLDER-decay.png' | relative_url }}" alt="decay + strength">
    <figcaption>Read-time decay + replay strength</figcaption>
  </figure>
</div>

More cohorts running nightly (04:00 UTC) plus ad-hoc batches. Numbers update as they land.
