---
layout: default
title: Research journal
description: Human-readable notes at five-hour research milestones, with earlier evidence clearly marked.
permalink: /
---
<section class="intro">
  <p class="eyebrow">Hutter Prize · Large Text Compression Benchmark</p>
  <h1>Five GPU-hours at a time.</h1>
  <p class="intro-copy">Field notes explain the decisions as they happen; a longer milestone essay closes every five charged GPU-hours. Each account follows the question, evidence, cost, and next decision. A completed run is not a win: the goal is a smaller complete package that decodes exactly and meets the competition’s rules.</p>
</section>

<section class="meter" aria-labelledby="meter-title">
  <div class="meter-heading">
    <div>
      <p class="eyebrow">Cumulative charged GPU time</p>
      <h2 id="meter-title">{{ site.data.meter.campaign_hours | round: 3 }} hours recorded</h2>
    </div>
    <p class="meter-date">Updated {{ site.data.meter.as_of_utc | date: "%d %b %Y, %H:%M UTC" }}</p>
  </div>
  {% assign completed_hours = site.data.meter.campaign_hours | minus: site.data.meter.itemized_from_hours %}
  {% assign milestone_span = site.data.meter.next_five_hour_boundary | minus: site.data.meter.itemized_from_hours %}
  {% assign milestone_progress = completed_hours | times: 100.0 | divided_by: milestone_span %}
  <div class="meter-track" role="meter" aria-label="Progress toward the next five-hour research summary" aria-valuemin="{{ site.data.meter.itemized_from_hours }}" aria-valuemax="{{ site.data.meter.next_five_hour_boundary }}" aria-valuenow="{{ site.data.meter.campaign_hours }}">
    <span style="width: {{ milestone_progress }}%"></span>
  </div>
  <p class="meter-note">Next five-hour summary at {{ site.data.meter.next_five_hour_boundary }} GPU-hours · {{ site.data.meter.hours_to_next_boundary | round: 3 }} hours remain · ceiling {{ site.data.meter.campaign_ceiling_hours }} hours.</p>
</section>

<aside class="archive-note">
  <span class="archive-mark">Archive note</span>
  <p>The campaign entered this itemized ledger at {{ site.data.meter.inherited_anchor_hours }} GPU-hours. Earlier records preserve the aggregate total and major decisions, but do not include a complete per-run timeline. The retrospective below summarizes verifiable findings; it does not invent five-hour boundaries for the missing history. The notes after it document individual decisions before the first fully itemized milestone, due at 85 GPU-hours.</p>
</aside>

<section class="journal-list" aria-labelledby="notes-title">
  <div class="section-heading">
    <p class="eyebrow">Research notes</p>
    <h2 id="notes-title">What the evidence changed</h2>
  </div>
  {% for post in site.posts %}
    <article class="journal-entry">
      <div class="entry-date">
        <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%d %b %Y" }}</time>
        <span>{{ post.research_span }}</span>
      </div>
      <div class="entry-content">
        <p class="entry-range">{{ post.campaign_range }} <span>·</span> {{ post.cost_label }}</p>
        <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
        <p>{{ post.summary }}</p>
        <a class="read-link" href="{{ post.url | relative_url }}">Read the note <span aria-hidden="true">→</span></a>
      </div>
      <span class="status-tag status-{{ post.outcome_class }}">{{ post.outcome }}</span>
    </article>
  {% endfor %}
</section>
