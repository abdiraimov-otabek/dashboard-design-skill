# Layout ideas: eight named pages

Before building a new dashboard, propose **two** of these by name with one line each on why they fit the screen's
question, and let the user pick. Never default to the same strip-chart-lists page for every brief. Widths, grids and
phones for whichever you pick: [layout.md](layout.md). Live examples: [inspiration.md](inspiration.md).

Each layout names its question, its wireframe (desktop, 12 columns), when it wins and when it does not.

## 1. Classic strip

"How is it going, and what's driving it?" The analytics default: a KPI strip, one chart the selected tile drives,
then ranked lists in pairs.

```
[ range · filter · updated ]
[ KPI ][ KPI ][ KPI ][ KPI ][ KPI ]   ← selected tile tints and drives the chart
[ main chart ··························· ]
[ ranked list ][ ranked list ]
[ ranked list ][ ranked list ]
```

Wins: traffic, product usage, any "one metric over time, then where it came from". Seen in Plausible, Vemetric,
Fathom, OpenPanel. Loses: monitoring (problems hide in the lists), anything without a single headline metric.

## 2. Control center

"Which of my metrics moved?" A grid of metric cards, each with its own small chart and a "from $X" baseline, plus a
side column for what moved and a live feed.

```
[ MRR + chart ][ Net revenue + chart ] [ Breakdown: what moved ]
[ Fees + chart ][ Other + chart      ] [ Live feed            ]
```

Wins: revenue and finance, where 4–6 metrics matter equally. Seen in Baremetrics. Loses: when one metric matters
most; give it the hero instead.

## 3. Status board

"Is anything broken right now, and since when?" An overall state banner, the open incident with its timeline, then
one row per service of daily bars.

```
[ ● All systems operational · 09:45 UTC ]
[ Open incident: title · updates, newest first ]
[ Service A  ▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮  99.96% ]
[ Service B  ▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮▮  100%   ]
```

Wins: uptime, background jobs, integrations, anything with "up or not". Seen in OpenStatus, Claude Status. Colour only
the bad days.

## 4. Monitor grid

"Who needs attention today?" A heatmap (entities × days) is the main view; problem cells carry their action.

```
[ KPI ][ KPI ][ KPI ][ KPI ]
[ heatmap: rows = classes/clients, cols = days   ][ needs attention: 3 ]
[ bullet graphs: budget or goal per row          ]
```

Wins: many similar entities checked daily (classes, clients, stores, servers); the school case study and the README's ads test use it. Loses: one entity; use Classic strip.

## 5. Leaderboard

"Who is winning, and who is moving?" Ranked rows of logo, name, value, delta and a sparkline, often in two columns,
with one trend chart above.

```
[ usage over time (stacked, ≤6 series + Other) ]
[ 1 ◉ Model A  66.8T ↑9% ][ 6 ◉ Model F  6.6T ↓10% ]
[ 2 ◉ Model B  23.5T ↑…  ][ 7 ◉ Model G  4.5T ↑33% ]
```

Wins: AI models, products, customers, stocks, sales reps. Seen in OpenRouter, Stocks. Loses: when rank does not
matter, only thresholds.

## 6. Map hero

"Where is it happening?" A choropleth fills the first screen, one sequential scale, events as markers of a different
shape and hue, a location filter at the top.

```
[ location: Worldwide ▾ ]
[ map ······························ legend ]
[ explore tabs: by country · by city ]
```

Wins only when place is the question (traffic, outages, delivery, field teams). Seen in Cloudflare Radar. Otherwise a
ranked country list with flags reads faster.

## 7. Wall

"Readable from across the room." Four to eight giant numbers, each over a faint sparkline, one colour for normal and
one for the single bad number; no controls, auto-refresh, the time in a corner.

```
[   549   ][  3483  ][   433   ][   86   ]   ← only the bad one is red
[ trend chart ··········][ trend chart ·········· ]
```

Wins: TV in an office, on-call screens. Seen in Grafana. Keep it wordless: no instruction paragraphs, no gauges.

## 8. List and detail

"Show me everything, then one thing in depth." A dense list on the left (each row: name, sparkline, value, delta
pill), the selected item's detail on the right.

```
[ search ][                                   ]
[ row ~~~ 49 595 +1.4k ][ Detail: name, value  ]
[ row ~~~  7 237  +326 ][ chart                ]
[ row ~~~    349  +6.5 ][ related items        ]
```

Wins: portfolios, inboxes, queues, projects, native Mac and iPad apps. Seen in Stocks, Activity Monitor. On a phone
the list is the screen and the detail pushes.

## Choosing two

| The screen's question | First pick | Second pick |
|---|---|---|
| How is it going, what's driving it? | Classic strip | Control center |
| Which of my metrics moved? | Control center | Classic strip |
| Is anything broken? | Status board | Wall |
| Who needs attention today? | Monitor grid | List and detail |
| Who is winning or moving? | Leaderboard | List and detail |
| Where is it happening? | Map hero | Classic strip with a country list |
| What is the room looking at? | Wall | Status board |
