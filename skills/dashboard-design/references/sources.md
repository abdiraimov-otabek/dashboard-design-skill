# Sources (what each is the best example of)

Studied October 2026; summaries in our own words. No affiliation with any product listed. Revisit the live ones
before a big redesign — they change.

## Books and research

Studied October 2026 through the authors' own published papers and specifications, and reputable summaries of the
books; the books themselves were not reproduced. Their rules live in [perception.md](perception.md).

- **Stephen Few** — *Information Dashboard Design* (2006/2013): the thirteen common mistakes, single-screen
  monitoring, context for every number. Papers on perceptualedge.com: "Why Most Dashboards Fail" (2007, the
  monitoring sequence; grey display with one red flag), "Practical Rules for Using Color in Charts" (2008, nine
  rules: three intensities, one hue for quantity, no red/green pairs, no effects), "Bullet Graph Design
  Specification" (2013).
- **Edward Tufte** — *The Visual Display of Quantitative Information*: data-ink, chartjunk, the lie factor, small
  multiples; sparklines from *Beautiful Evidence*.
- **Cole Nussbaumer Knaflic** — *Storytelling with Data*: declutter, preattentive attributes used sparingly, the
  "where do your eyes go first?" test.
- **Steve Wexler, Jeffrey Shaffer, Andy Cotgreave** — *The Big Book of Dashboards*: scenarios over templates; lead
  with the answer, group related metrics.
- **Cleveland & McGill** (1984, 1985) via **Nielsen Norman Group** ("Dashboards: Making Charts and Graphs Easier to
  Understand"): position and length beat area and angle; colour for categories, not magnitude; no gauges, 3D or
  treemaps on monitoring screens.
- **Tableau eye-tracking study** (2016–2018): big numbers are seen first and early; the top gets the most time;
  attention fades along repeated elements. Vendor research, directional.
- **Lisa Charlotte Muth, Datawrapper** — "Which color scale to use": sequential vs diverging (a meaningful
  midpoint), classed vs unclassed (thresholds, readable ranges).
- **IBM Carbon** — presentation vs exploration dashboards, F-pattern priority, one colour per dataset everywhere,
  white space.
- **WCAG 2.2** — 1.4.1 (colour never alone), 1.4.11 (3:1 for data marks), 1.4.3 (text in charts), 1.1.1 (a text
  alternative per chart).

## Apple (WWDC sessions: transcripts, and key frames captured from the videos)

- **Design an effective chart** (WWDC22) — marks chosen with real data; fixed vs dynamic axis ranges; about four
  gridlines at intuitive steps; the takeaway in the title; large hit areas; colour balanced, distinct by name and
  never alone; spoken labels context first.
- **Design app experiences with charts** (WWDC22) — when to chart (change over time, part of a whole, comparison);
  macro / meso / micro summaries as tappable stats; glance → interactive → expanded with continuity; familiar
  forms, deliberate differences. Its advice to describe every chart in a full sentence is moved here into the
  title's number and the tooltip, to keep screens wordless.
- **Bring accessibility to charts in your app** (WWDC21) — charts as navigable containers, audio graphs through
  `AXChartDescriptor`, interval grouping for large series, red/green and blue/yellow pairs to avoid.
- **Writing for interfaces** (WWDC22) — purpose, anticipation, context, empathy; let visuals carry meaning; specific
  action labels; empty states that guide; errors with a fix; a word list; localisation.
- **Explore pie charts and interactivity in Swift Charts** (WWDC23) — pies for casual part-to-whole, donut centre
  label, selection dimming, scrollable long series.
- **Bring Swift Charts to the third dimension** (WWDC25) — 3D only for truly three-dimensional data explored by
  rotation, where shape matters more than values.

## Designers

- **Marcel Kargul** (Kargul Studio; x.com/marcelkargul) — a body of shipped dashboard work: light grey pages with
  white cards, a toolbar of pills, KPI cards with a monochrome icon square and a one-word baseline, heatmaps of
  rounded number pills, ring charts with the value in the centre and a % legend (for one share, not as gauges),
  pastel stacked bars with solid caps, dark tooltips with one big value, segmented pills for parts of a total. The
  clearest example of "the page speaks for itself".

## Analytics products (live demos)

- **Plausible** — plausible.io/plausible.io — the reference for selected-tile fill, grouped date menu with
  keyboard letters, compare in the date menu, calm single-hue chart, tooltip with both periods.
- **Fathom** — usefathom.com/demo — two-month range picker with presets rail and soft band; dotted incomplete day;
  "+ Add comparison" chip; events table with conversion rate and value columns.
- **Simple Analytics** — simpleanalytics.com/simpleanalytics.com — big light numerals, grey 0% deltas, preset pills
  above the calendar, timezone footer.
- **DataFast** — datafa.st (public demo and a trial account) — revenue bars on a right $ axis over visitors,
  source logos on sale spikes, plain-sentence Insights page (visits/days/hours to purchase, weekday×hour heatmap),
  "Now" range, suggested filter chips, sample data under empty-state overlays, "Set up with AI" copyable prompt,
  3D realtime globe, Goal/Funnel/User/Journey tabs. Case study: [case-study-datafast.md](case-study-datafast.md).
- **Pirsch** — pirsch.pirsch.io — compare menu (previous period, year over year, match day of week); list bars as
  a thin underline. Also a live example of native date inputs looking unfinished.
- **Vemetric** — app.vemetric.com/public/snappify.com — tile swatch doubling as chart legend; multi-metric overlay.
- **OpenPanel** — demo.openpanel.dev — mini bar chart per tile, natural-language filter box.
- **GoatCounter** — sparkline plus delta per row.
- **Matomo** — compare checkbox and Apply inside the period popover (otherwise dated and dense).
- **Databuddy, Cabin, Counter.dev, Swetrix, PostHog, Umami, Mixpanel** — secondary examples (preset strips,
  stacked bars, error states, percent chips).

## Revenue and SaaS

- **Baremetrics** — demo.baremetrics.com — date picker with each preset's resolved dates, "from $X" previous value
  next to the headline, MRR history row (1/3/6/12 months ago), goals bar with plain-words pacing, live money feed.
- **TrustMRR** — trustmrr.com/stats — thin 3 px line per row with % at the right; "verified" trust framing.
- **Shopify** — thin bar with value at the bar end; dotted previous-period overlay.
- **Mercury** — thin dotted-track bars in money in/out; small decimals.
- **Stripe, Lemon Squeezy, Polar, Lago, Metronome, RevenueCat, ProfitWell** — money formatting, shaded gap between
  revenue and cost (Polar), "data differs from other systems because…" honesty (RevenueCat).

## Design systems

- **Tremor** — KPI cards, area chart conventions (its BarList uses the tinted-row style to avoid).
- **shadcn/ui** — range calendar (pale band, solid end days), chart card header with range select.
- **Untitled UI** — presets column + two months, ring on today.
- **React Aria** — accessible DateRangePicker: grid roles, keyboard (arrows, PageUp/Down, Home/End).
- **Radix Themes** — segmented control (grey track, raised white thumb) for mode toggles.
- **Material 3, Ant, Carbon, Atlassian, Mantine** — typed-date switches, masked inputs, chart anatomy checklist.
- **Apple HIG (charts)** — emphasise the one series that matters; no decoration.

## Galleries

- **SaaSFrame, Dribbble** (popular "analytics dashboard", "date range picker", "KPI cards") — good for compact
  picker patterns; also the clearest catalogue of AI-looking tells to avoid (glass, neon, 3D icons, 3-slice donuts).
