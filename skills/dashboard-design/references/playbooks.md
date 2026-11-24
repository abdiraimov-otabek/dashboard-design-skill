# Playbooks: ten dashboard types

Step 1 of the build ("name the question") already filled in for the dashboards people ask for most. Start from the
closest playbook, then change it to the user's data: their metric names, their targets, their problems. A playbook is
a first draft of the four lists in SKILL.md (question, numbers, problem rules, actions), not a template to paste.

Each playbook gives: the **question**, the **numbers** (3–6, in order), the **problem rules** as numbers, the
**main view**, the **layout** from [layout-ideas.md](layout-ideas.md), and **look at** from
[inspiration.md](inspiration.md). Thresholds are sensible defaults; replace them with the user's.

## 1. Web analytics

- Question: how many people came, from where, and did they do the thing?
- Numbers: visitors · pageviews · conversion rate · top source · live visitors
- Problems: visitors down >30% vs the same elapsed time last period on a base ≥ 100; a source that drove ≥10% of
  visits drops to 0; tracking silent for >2 h in business hours.
- Main view: visitors over time, previous period dashed, annotations for launches and posts.
- Layout: Classic strip. Look at: Marcel Kargul's light dashboards; Simple Analytics for chart annotations.

## 2. SaaS revenue (MRR)

- Question: is revenue growing, and what moved it?
- Numbers: MRR (from last month's value) · net new MRR · churn rate · ARPA · active customers
- Problems: net new MRR < 0 for the month so far; monthly churn above 5%; one customer over 20% of MRR; failed
  payments not retried for >3 days.
- Main view: MRR over 12 months, plus a movement breakdown (new, expansion, contraction, churn) with losses in red.
- Layout: Control center. Look at: Baremetrics. Money rules: components.md → Trust cues (revenue).

## 3. Product analytics

- Question: are people using the product, and where do they drop?
- Numbers: active users (day, week) · activation rate · week-4 retention · the key action per user
- Problems: activation below target for 3 days running; a funnel step converting <50% of its normal; week-4
  retention of the newest cohort below the median cohort.
- Main view: a funnel for the core flow, and a cohort retention grid (components.md → Funnel, Cohort grid).
- Layout: Classic strip, or Control center with funnel and cohorts as cards. Look at: Bagus Fikri's insight cards (cohort grid in a card).

## 4. E-commerce

- Question: are we selling, and what's selling?
- Numbers: revenue · orders · average order value · conversion rate · refunds
- Problems: conversion down >25% vs the same weekday; a top product out of stock; refund rate above 3%; checkout
  errors above 1% of attempts.
- Main view: revenue by hour or day against the same period last week; top products as a leaderboard with stock.
- Layout: Classic strip, with a Leaderboard card for products. Look at: Barly's admin dashboard (one highlighted bar, top products table).

## 5. Ads and marketing

- Question: is each client or campaign spending well, and which one needs me today?
- Numbers: spend · leads · cost per lead (lower is better) · CTR · budget runway
- Problems: CPL above 1.2× target on 2 of the last 3 days; spend pacing over 110% of budget; a campaign with spend
  and zero leads for 48 h.
- Main view: CPL heatmap (clients × days) with classed tiers toward the problem; budget runway as bullet graphs.
- Layout: Monitor grid. Spend is neutral (grey deltas); CPL flips red and green. Look at: ln_dev7's attention banner (a count plus the action).

## 6. AI and LLM usage

- Question: what are we spending on models, and is it worth it?
- Numbers: cost (period) · tokens in and out · requests · cost per successful task · error or timeout rate
- Problems: daily cost above 1.5× the 7-day median; error rate above 2%; one model or user over 50% of cost;
  p95 latency above the target.
- Main view: cost by day stacked by model (six at most, the rest as "Other"); a leaderboard of models or users with
  cost, share and delta. Always show "data through <time>": usage often arrives late.
- Layout: Leaderboard, or Control center. Look at: OpenRouter (freshness label, leaderboard); heysatya's AI panel as actions.

## 7. Ops and uptime

- Question: is anything broken right now, and since when?
- Numbers: overall state · services down or degraded · p75 latency · error rate · open incidents
- Problems: any service down; latency above 2× its baseline for 10 minutes; error rate above 1%; a cron or queue
  that missed its last run.
- Main view: one row of daily bars per service, colour only on bad days; the open incident's timeline above.
- Layout: Status board, or Wall for a TV. Look at: OpenStatus, Claude Status, Grafana.

## 8. Support desk

- Question: are customers waiting too long, and on what?
- Numbers: open tickets · first response time (median) · tickets breaching SLA · CSAT · backlog trend
- Problems: any ticket past its SLA; first response median above target; backlog growing 3 days running; CSAT
  below 80% on a base ≥ 20.
- Main view: a queue table sorted by time to breach, with the action (assign, reply) on each row.
- Layout: List and detail, with the KPI strip above.

## 9. Finance and portfolio

- Question: what do I have, and what changed today?
- Numbers: total value · change today (amount and %) · cash · allocation · largest mover
- Problems: a holding moving >5% in a day; cash below a floor; allocation drifting >5 points from target.
- Main view: a list of holdings, each row with sparkline, value and a delta pill; allocation as a segmented share bar.
- Layout: List and detail. Look at: Sajibur Rahman and Sujon (one accent card, wallet rows with flags), Apple Stocks (the row). Say "at close" or the quote time; prices are never live by default.

## 10. School and operations (many similar entities)

- Question: which classes, stores or sites need attention today?
- Numbers: entities on track · attendance or throughput · the entities below threshold · tasks not done today
- Problems: attendance below 85%; a register not marked by 10:00; one entity below threshold 3 days running.
- Main view: a heatmap of entities × days where the problem tier is the strongest colour, the remind or fix action
  on the cell itself.
- Layout: Monitor grid. Worked example: [case-study-school-dashboard.md](case-study-school-dashboard.md).

## Admin and internal tools

Not a dashboard: a CRUD table with filters. Use List and detail, keep one KPI strip at most, and spend the effort on
the table (tables and recent activity in components.md).
