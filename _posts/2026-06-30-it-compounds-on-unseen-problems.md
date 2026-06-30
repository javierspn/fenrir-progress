---
layout: post
title: "It compounds — on problems it has never seen"
---

The last post bent the escalation curve and I refused to celebrate, for one specific reason: the
problems were a contaminated grab-bag (GSM8K/MATH). A falling escalation rate there could be the
system *reusing skills* — the whole bet — or it could be the small model quietly recognising problems
it already saw in pretraining. Recall, dressed up as learning. I couldn't tell the two apart, so I
didn't claim the win.

So I built the experiment that *can* tell them apart, and ran it today. This is the result.

## The clean test

Feature **006** generates its own problems: a small open model writes the prose **and** executable
solution code, then SymPy runs the code to derive the answer — the model is never trusted for the
ground truth. Every problem is fresh, so **contamination is off the table by construction**. The
problems come in **10 families** — one solution *method* each (two-step rate, system of two equations,
percent-of-percent, distance-meet, …). 1,000 of them generated on a free Kaggle GPU, sandbox-verified
on load (965 passed, 35 rejected — the verifier doing its job).

Then I biased the task stream to draw whole families in sequence and asked the only question that
matters: **within a family, once the loop has paid to solve the first problem and crystallised a
skill, does it solve the siblings cheaply?**

## The numbers

The cleanest cut splits every family solve by whether the loop actually **retrieved a stored skill**
for it:

| On a family problem… | tasks | teacher escalation |
|---|---|---|
| **a skill was retrieved** | 233 | **7.7%** |
| **no skill — cold** | 91 | **100.0%** |

Cold, it calls the paid teacher every single time. With a matched skill, it calls it **7.7%** of the
time. Same loop, same models — the only difference is whether the library had something to offer. On
problems **the model has provably never seen.**

Aggregated by position within a family: the **first** member escalates **75%** of the time; **later**
members, **32.6%**. The expensive first solve gets amortised across the rest of the family.

## The honest part

This is the strongest result the project has produced. It is not a finished one:

- **Retrieval coverage isn't 100%.** 91 of 324 later-problems still came up cold and paid full price.
  The win is real *when the skill is found*; finding it every time is the next job, not a solved one.
- **The per-position curve is monotone to about position 8, then it bounces** (62 → 25 → 50 → 75 …).
  That isn't the effect weakening — it tracks exactly whether retrieval fired on that specific
  problem. But it means "later = cheaper" is a trend with noise on it, not a smooth law.
- **n is about 8 per position, one domain (math), one pool.** A clean signal, not yet a large one.
- The reuse-vs-coverage decoupling I flagged last time — here they move **together** (high reuse ↔ low
  escalation at every position), which is the reassuring direction. One pool isn't enough to retire
  the worry, but it didn't reproduce.

What changed from last post: there, the bent curve *might* have been contamination. Here it **can't
be** — and the gap got wider, not narrower (7.7% vs 100%, against 27% vs 100% on the dirty set). The
contamination-safe version of the experiment came back stronger than the contaminated one. That's the
update I didn't have a week ago.

## The curves

<figure class="shot">
  <img src="{{ '/assets/img/byfamily-retrieved-gap.png' | relative_url }}" alt="escalation when a skill was retrieved vs cold">
  <figcaption>The whole bet in one chart: on contamination-safe family problems, a retrieved skill drops teacher escalation from 100% to 7.7%.</figcaption>
</figure>

<div class="grid">
  <figure class="shot">
    <img src="{{ '/assets/img/byfamily-escalation-position.png' | relative_url }}" alt="escalation by position within a family">
    <figcaption>Escalation by position within a family — falling as the family's skill accrues, then noisy past position 8 (n≈8 each).</figcaption>
  </figure>
  <figure class="shot">
    <img src="{{ '/assets/img/byfamily-escalation-reuse.png' | relative_url }}" alt="escalation vs reuse per position">
    <figcaption>Escalation and reuse mirror each other position by position — when the skill gets retrieved, the teacher call disappears. That coupling is the mechanism.</figcaption>
  </figure>
</div>

The contaminated nightly series keeps running ("does the loop work at all"); this clean family series
answers the sharper one ("does it *compound*"). Next: more families, deeper positions, and pushing
retrieval coverage up so the 7.7% lane is the common case, not the lucky one.
