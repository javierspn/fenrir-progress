---
layout: default
title: Home
---

## What this is

[Fenrir](https://github.com/javierspn/fenrir-agent) is a small, locally-run model that tries to get
better at **mathematics** over time — by accumulating memory and crystallizing *verified* skills, and
leaning on an expensive frontier "teacher" model **less and less**.

The bet: competence can **compound** through experience instead of scale. This page is the running,
public record of whether it actually does — cohort numbers, learning curves, and screenshots, posted
as they come. **A flat curve is a valid result and stays on the page.**

<section id="metrics">

## Latest numbers

<div class="metrics">
  <div class="metric"><div class="v">175</div><div class="k">skills</div></div>
  <div class="metric"><div class="v">352</div><div class="k">abstractions</div></div>
  <div class="metric"><div class="v up">5 → 9</div><div class="k">reuse / day ↑</div></div>
  <div class="metric"><div class="v">98.2%</div><div class="k">escalation</div></div>
  <div class="metric"><div class="v">$0.13</div><div class="k">cost / cohort</div></div>
</div>

<small style="color:#8b98a8">Escalation still high — reuse can't bite until the task curriculum
biases toward skill-adjacent problems. That's the next experiment. Honesty first.</small>

</section>

<hr>

<section id="log">

## Progress log

<ul class="posts">
{% for post in site.posts %}
  <li>
    <span class="date">{{ post.date | date: "%Y-%m-%d" }}</span>
    <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
    <div class="excerpt">{{ post.excerpt | strip_html | truncate: 160 }}</div>
  </li>
{% endfor %}
</ul>

</section>

<hr>

## Support the compute

Every donation goes **straight to compute** — frontier-teacher API credits, and local-inference
hardware (a Mac Mini lets the loop run more, cheaper, and lean on the paid teacher *less* — which is
literally the metric being measured).

→ **[☕ ko-fi.com/javierspn](https://ko-fi.com/javierspn)**
