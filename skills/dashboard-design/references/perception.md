# Perception: what the eye reads, and how fast

The science under the rules in SKILL.md, distilled from Stephen Few, Edward Tufte, Cole Nussbaumer Knaflic,
Cleveland & McGill (via Nielsen Norman Group), Lisa Charlotte Muth (Datawrapper) and the WCAG. Summaries in our own
words; sources in [sources.md](sources.md). Reach for this file when choosing how to draw a number, how to colour a
scale, or why a screen fails the first-glance test.

## Monitor: the reader's sequence

A dashboard is a monitoring tool. The reader moves through four steps, and the screen serves each in turn (Few):

1. **Overview**: the state of everything at once.
2. **What needs attention**: the few items that are wrong, found in a glance, not a search.
3. **Closer look**: enough context on those items to decide whether to act.
4. **Act**: the action sits one click from the problem (remind, call, open the record), so the dashboard is a
   launch pad, not a report to read and then go elsewhere.

A screen that shows everything with equal weight passes step 1 and fails step 2.

## Encoding ladder: how to draw a number

People judge some visual properties accurately and others badly (Cleveland & McGill, 1984 and 1985). Pick the
highest rung that fits:

| Rung | Encoding | Use for |
|---|---|---|
| 1 | Position on a common scale | Lines, dots, bars on one axis: trends and comparisons |
| 2 | Length | Bars, bullet graphs, share bars |
| 3 | Colour intensity (one hue, light → dark) | Matrices only: a heatmap where position is taken by the grid |
| 4 | Area, angle | Almost never: donuts and pies only to show one overwhelming share |
| — | Hue | Categories, never magnitude: people do not read hues as ordered |

Off the ladder: radial gauges and dials (angle, wasted space), treemaps on a monitoring screen (fine for slow
exploration), and 3D. Apple's rule for 3D charts (WWDC25) is narrow: data that is truly three-dimensional, where the
shape matters more than exact values and the reader rotates it to see it. That is never a monitoring screen.

Pie and donut: casual part-to-whole where precision is not critical (Apple, WWDC23), a handful of slices, the
headline value in the hole. On a dashboard prefer a segmented bar or a ranked list; a donut earns its place only for
one share that dominates.

### Choose with real data

Pick the mark with the real, messy data, not a neat sample (Apple, WWDC22): noise, zero days, one huge outlier, an
empty week. Lines between alternating zeros turn into zigzags that hide the values; bars keep zeros readable and
their total weight still reads as the total.

### Axes and gridlines

- **Fixed range** when the bounds are known (0–100% for a rate, a battery, attendance), so full and empty read at a
  glance. **Dynamic range** when there is no natural maximum, so small values still show their shape.
- Bars always start at zero. A line may start above zero when the axis says so.
- About four gridlines at intuitive steps: round values (20, 40, 60), and for time, steps the reader counts in
  (7 days across a 30-day window, months across a year).
- A glanceable preview (a sparkline, a card thumbnail) has no gridlines and no labels at all.

## Preattentive attributes: what is seen before it is read

Colour, size, position, length, orientation and enclosure are processed in under a quarter of a second, before
reading starts. Spend them on the one thing per region that needs attention:

- A single saturated element in a grey field is found instantly; ten saturated elements are a search.
- Big numbers draw the eye first and early (Tableau eye-tracking study); the top of the screen gets the most
  dwell time; attention fades along a run of repeated, identical elements, so the most important item goes first.
- **Salience test**: ask "where does the eye land first?" (or blur the screenshot). It must land on the thing the
  screen is for, or on the problem. If it lands on a logo, a decoration or a healthy number, the hierarchy is wrong.

## Colour rules

Few's nine rules, compressed:

1. Same colour looks different on different backgrounds: keep chart backgrounds flat and consistent, no gradients.
2. Data must contrast with its background.
3. Add colour only for a purpose: to highlight, to group, or to encode a value.
4. Different colours only for different meanings; bars that differ only by name share one colour.
5. Three intensities with three jobs: **pale** for non-data and de-emphasis (grids, tracks, the other series),
   **medium** for data, **bright or dark** only for what needs attention.
6. Quantity is one hue from pale (low) to dark (high); two such ramps meeting at a meaningful midpoint make a
   diverging scale.
7. Non-data ink (axes, borders, gridlines) is just visible enough to do its job.
8. Red and green alone are invisible to about 8% of men: pair them with shape, icon, position or text, or use
   blue / orange.
9. No visual effects: no shadows on data, no gloss, no 3D.

### Balance and meaning (Apple)

- Categories look equally important: even out saturation and lightness across their colours, and spend a heavier
  colour only on what should draw the eye.
- Colours in one chart are easy to tell apart **by name** ("purple and green", not "purple and pink-purple").
- Beyond red/green, blue/yellow is the second most common confusion. Check every chart through a colour-blindness
  filter.
- Colour meanings are cultural: green for gains and red for losses is reversed in some markets (China). Follow the
  readers' convention and back it with ▲ / ▼.
- Respect the reader's settings: more contrast (`prefers-contrast: more`, Increase Contrast), differentiate without
  colour (add shapes), reduced transparency, dark mode.

### Scales (Muth)

- **Sequential** (light → dark) when the data has no natural middle; readers understand "darker = more" without a key.
- **Diverging** when a meaningful middle exists: zero, a target, the average, 50%. It emphasises both extremes and
  always needs a key.
- **Classed** (a few steps) when readers must sort items into groups or read ranges, or when meaningful thresholds
  exist (a target, the average). **Unclassed** (continuous) for general patterns.

### The inverted-salience trap

A sequential scale makes low values pale. When low is the problem (attendance, uptime, conversion), the worst cell
becomes the least visible one. The mirror mistake is as common: tiers where the best values are the darkest, so the
healthiest cells are the loudest on the grid. Use classed tiers whose intensity grows toward the threshold, with the
healthiest values palest, and a warm warning hue past it. The problem is then the most salient cell on the grid.

## Heatmaps

- One hue, intensity steps that grow toward the problem (healthy palest); three to five classes at meaningful
  thresholds; one warm tier past the threshold, which also carries a non-colour cue (underline, bold or ▲).
- Numbers inside cells only when the matrix is small (up to ~60 cells) and every number fits with 4.5:1 contrast;
  otherwise colour only, with the exact value in the tooltip (Few: reading numbers slows pattern scanning).
- A missing value is its own state (outline, dashed border, or icon), never an empty-looking cell that reads as zero.
- Today's column is marked; future cells are not drawn.

## Bullet graph (Few's specification)

The compact replacement for gauges: one measure against a target and qualitative ranges.

- Parts: label (left), a linear scale starting at zero, the featured measure as a bar about one third of the
  container's thickness, the comparative measure (target) as a short perpendicular line, and two to five
  background ranges (ideally three).
- Ranges are intensities of one hue, darker for poor and lighter for good (three ranges: 40%, 25%, 10% grey).
- "Lower is better" measures (expenses, defects) reverse the range order.
- A target in the future (end-of-quarter revenue) gets a projected segment so "on track?" is answerable today.

## Sparklines (Tufte, Few)

Word-sized lines that give history to a current number: no axes, no gridlines, a dot on the last point. They show
the shape of change, not values; the value sits next to them. Every sparkline in a set covers the same window.

## Context: compared to what?

A number alone says nothing (Few's second mistake). Each headline number carries one comparison: the previous
period (same elapsed time), a target, a normal range, or its history. One comparison, said in a symbol and one or
two words ("▲ 2 vs Sep", "▼ 15% vs last month"), with the exact baseline in the tooltip.

## Accessibility

- Colour is never the only carrier of meaning (WCAG 1.4.1): add a shape, icon, pattern, line style or label.
- Data marks need 3:1 contrast against their neighbours (WCAG 1.4.11); text in charts follows text contrast,
  4.5:1 (1.4.3). Heatmap cells are exempt from 1.4.11 when the colour is the data, but their numbers are not.
- Every chart has a text alternative: an `aria-label` summary (range, extremes, latest value) and keyboard access
  to the values (arrow keys move a focus point and show its tooltip).
- Spoken values put the context first and spell words out: "June 1, 36 pancakes", "5-A, 28 October, 20 of 26
  present", never "Jun" or "6-1". Large series speak in intervals ("1–7 June: 240 sold"), not point by point.
- The hit area of an interactive chart is its whole plot height, not the thin marks; every pointer interaction has a
  keyboard and screen-reader equivalent with a visible focus mark.
- Native apps add an audio graph (swiftui.md → Accessibility).

## Few's thirteen mistakes (checklist)

1. Exceeding one screen for the monitoring view.
2. Numbers without context.
3. Excessive detail or precision.
4. A deficient measure (unclear unit, or not what the decision needs).
5. The wrong display medium for the message.
6. Meaningless variety (a different chart type per panel to look interesting).
7. Poorly designed display media (unlabelled, 3D, badly ordered).
8. Inaccurate encoding (bars not starting at zero).
9. Poor arrangement (things to compare are not side by side on one scale).
10. Important data not highlighted, or everything highlighted.
11. Useless decoration.
12. Misused or overused colour.
13. An unattractive display: a busy screen is a slow screen.
