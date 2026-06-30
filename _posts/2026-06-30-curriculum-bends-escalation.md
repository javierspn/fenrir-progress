---
layout: post
title: "The escalation curve finally bent"
---

Last post ended on a promise: the small model was calling the teacher **98% of the time**, and I
blamed the curriculum — it drew problems at random, so a stored skill almost never matched the next
task. The fix was to bias the task stream toward **skill-adjacent** problems and watch whether
escalation finally moved. That experiment (feature **004 — feasibility-gated curriculum**) is now
live. It moved.

## The numbers

Two cohorts under the old random draw, then two under the new skill-adjacent draw. Same loop, same
models, same budget — only the task-selection policy changed.

| Signal | Random draw (Jun 28) | Skill-adjacent (Jun 29 → Jun 30) | Direction |
|---|---|---|---|
| **Coverage** — a stored skill matched the task | 2.9% | **56% → 60%** | ↑ ~20× |
| **Reuse** — a consolidated abstraction drove the solve | 0.9% | **40% → 28%** | ↑ (off zero) |
| **Escalation** — had to call the paid teacher | 98.0% | **62% → 56%** | **↓ at last** |
| Skills crystallized | (was 175) | 463 | ↑ |
| Abstractions | (was 352) | 965 | ↑ |
| Cost / cohort | $0.23 | <$0.01 | ↓ |

The escalation rate is the one I care about — it's the kill switch I named in the very first post.
For the entire project it sat flat near 98%. With problems aimed near skills the system already
owns, it dropped to **56%**. That's the first time the curve that decides whether this whole bet is
*compounding* or merely *recall* has pointed the right way.

## The honest part

I'm not declaring victory, and here's exactly why not:

- **It's two cohorts of 50 tasks each.** That's a signal, not a verdict. The real call needs
  ~8–13 nightly cohorts; I have two. n=50 is small enough that any single number could wobble.
- **Reuse went 40% → 28% while coverage went 56% → 60%.** Those should move *together* — if
  coverage keeps rising but reuse doesn't track it, the lift is recall or contamination, not the
  compounding library. One night's dip is probably noise, but it's the exact decoupling I have to
  watch, so I'm flagging it now rather than after.
- **Some retrieved solves come back wrong.** A skill matching a problem isn't a skill *solving* it
  correctly — the verifier still catches misses. Coverage is necessary, not sufficient.
- **56% is still a lot of teacher calls.** What changed is the *direction*, on a curve that
  refused to move for weeks. Absolute level is next.

One more cut makes the mechanism obvious. Split each cohort's escalation by whether a skill matched
the task. On **cold** tasks — nothing stored — the model escalates ~100%, every cohort, flat. On
**skill-covered** tasks it escalates far less, and falling: **36% → 32% → 27%**. The overall rate
drops simply because more tasks are now covered. That gap *is* the bet: a matched skill lets the
small model skip the teacher. If it ever closed — covered and cold escalating alike — I'd be
hoarding skills I never actually reuse, which is recall, not learning.

To keep myself honest I added a **per-cohort** cut of all four signals to the engineer "Learning"
dashboard, each drawn so a *flat or falling* line renders plainly. A negative result has to be as
readable as a positive one.

## The curves

<figure class="shot">
  <img src="{{ '/assets/img/cohort-escalation.png' | relative_url }}" alt="teacher escalation per cohort">
  <figcaption>Teacher escalation per cohort — flat at ~98% under random draw, then a cliff to 56% once the curriculum aims at skill-adjacent problems.</figcaption>
</figure>

<div class="grid">
  <figure class="shot">
    <img src="{{ '/assets/img/cohort-coverage-reuse.png' | relative_url }}" alt="coverage and reuse per cohort">
    <figcaption>Coverage vs reuse, per cohort — they have to rise together; the Jun-30 reuse dip is the thing I'm watching.</figcaption>
  </figure>
  <figure class="shot">
    <img src="{{ '/assets/img/cohort-escalation-gap.png' | relative_url }}" alt="skill-covered vs cold escalation">
    <figcaption>Skill-covered vs cold escalation — cold stays pinned at 100%, covered keeps falling. The gap is the kill switch.</figcaption>
  </figure>
</div>

Cohorts run nightly (one per night) plus the odd ad-hoc batch. I'll post the verdict — bent curve
or flat one — once the series is long enough to mean something.
