# Components

Each pattern: what it is for, the spec, and the trap that shipped once and had to be fixed. Written in Tailwind
terms with the tokens from [tokens.md](tokens.md) (`accent` for traffic, `money` for revenue); translate freely to
any stack. Code for the fiddly parts: [snippets.md](snippets.md).

## KPI strip and the selected tile

For: the 3–7 headline numbers; clicking one picks the metric the main chart shows.

- One card, tiles divided by hairlines (`border-r border-line`), not seven floating cards.
- Tile content: label (14 px, ink-2) with a small monochrome icon square or the delta on the right · value (28–32 px
  semibold, `tracking-[-.03em]`, tabular) · the delta with a one- or two-word baseline ("▲ 13% vs last week") ·
  optional sparkline. The explanation ("3% of visitors", "$7.31 per order, after tax") is the tile's tooltip, never a
  sentence on a sub-line: a row of tiles with sub-lines reads as a paragraph.
- Two layouts: one card divided by hairlines when tiles are selectable and drive the chart; separate cards with a
  16 px gap when tiles only report.
- **Selected** = an inner rounded fill inside the cell: `rounded-xl bg-accent/[.06] ring-1 ring-inset ring-accent/20`
  (money metrics: `bg-money/[.07] ring-money/25`), label `font-medium text-ink`. Unselected: transparent,
  `hover:bg-soft/70`, value in ink-2, sparkline grey. Wrap the cell in `p-2` so the fill floats inside the dividers.
- Button with `aria-pressed`, visible `focus-visible` ring on the inner fill.
- Exact value in `title`/tooltip when the tile shows a compact number.
- Trap: an underline or left edge to mark selection reads as a heavy marker. Use the fill.
- Trap: a partial period compared with a full one ("today so far" vs "yesterday") as a red delta. Show the
  comparison value neutrally ("94% yesterday") until the period closes.

## Delta badge

- `▲ 13%` green / `▼ 9%` red, 12 px medium, tabular; `±0%` grey. Colour by meaning, not direction: a
  lower-is-better metric (cost, CPL, churn) turns red when it rises; a neutral one (spend, volume) stays grey both
  ways.
- Base below ~5 (counts) → `was 1` in grey with the formatted previous value. A red −100% for 1 → 0 is noise.
- Over ±999% → `10×+` / `−99%`.
- Never repeat a tile's delta anywhere else on the screen.

## Sparkline

- 24–40 px tall, 1.5 px line, faint fill, no axes. Selected tile in the metric colour, others grey.
- Trap: it must draw **the same window as the main chart**. If the chart trims empty leading days ("Nothing before
  26 Sep · show all"), trim the sparklines identically, or every tile becomes a flat line with a spike at the end.

## Main chart

- Three sizes, one chart (Apple, WWDC22): a **glance** (sparkline or card thumbnail: no axes, no labels, a tap opens
  more), an **interactive** chart (axes, tooltips, a range control), and an **expanded** view for deep
  investigation. Moving between them keeps the shape, the values and the selection; adding detail is fine, showing
  something different is disorienting.
- The card's title carries the takeaway as a label and a number: a small muted label over the large value ("Total
  sales / 1,234 pancakes", as in Apple's own charts), not a bare noun and not a paragraph. An interpretive sentence
  ("up 12% on last month, best day Sunday") is the chart's tooltip and screen reader summary.
- Summary chips under the chart give macro, meso and micro views as label + number ("Daily avg 41", "Weekdays vs
  weekends +18%", "Best day Sun"); tapping one overlays it on the chart.
- Familiar forms (bars, lines) for supporting charts; one novel form (a heatmap, a custom matrix) only when it is
  the screen's centre, with its legend. When two charts differ (time vs category), make the difference visible:
  vertical bars over time, horizontal bars for categories.
- One metric at a time in its colour, 1.5–2 px line, gradient fill from ~15% to 0%. No point markers until hover.
- Y axis: 4–5 round ticks (0, 1k, 2k), labels 11–12 px muted, baseline 0. Odd ticks like 2,103 look broken
  (`niceTicks` in snippets.md).
- X axis: 5–7 ticks ("21 Sep"), never every day. Hourly for Today, daily up to ~120 days, monthly beyond.
- Previous period: grey or dashed line, no fill, behind the current series; legend "This period / Period before".
- Incomplete current bucket: dotted tail.
- Tooltip: date header, coloured dot + value, previous value and % change when comparing; vertical hairline.
- Selected bar: a full-height rounded outline around the bar's column (Apple's charts); the same column is the hit
  area and the keyboard focus mark.
- Y-axis labels may sit on the right edge, next to the latest values, leaving the left edge clean; x labels at
  week steps across a month.
- Revenue view: money as soft bars on a right-hand $ axis against the visitors line works well. Mark the biggest
  sale days with the source's logo over the bar, so the chart says where the money came from.
- Bars on their own: pastel fill (~20% of the entity hue) with a solid 6–7 px rounded cap at the top; the unfinished
  period as a dashed outline with a faint fill, its axis label in the accent.
- Tooltip: a dark card with the exact value large and the period in a muted line under it.
- Trim leading empty days by default, with a "show all" link.

## Ranked breakdown list

For: sources, pages, countries, devices — "what's the top of this, and by how much".

- Row: icon (favicon/flag, 16 px) · name (truncate) · value (tabular, right) · share % (muted, fixed width).
- Bar: a 3 px rounded track spanning the row's bottom edge (`bg-line/70`), the share filled in the entity colour
  at ~75% opacity, full on hover. Row `h-11 px-3 pb-1.5`, `hover:bg-soft/60`. No tinted block behind the text.
- Header row: column name left, metric right, 12 px muted.
- Tabs inside a panel (Channels / Referrers / Campaigns): a segmented control that shrinks and truncates on narrow
  cards, never scrolls sideways.
- Expand button opens the full list with search.
- Shares below 0.1% read `<0.1%`; the footnote says what shares add up to.
- Clicking a row filters the whole dashboard by it.
- Trap: one taxonomy per question. If a tooltip says "73% from Threads" while Channels says "Referral 73%",
  the reader sees two answers. Imported data may group channels by another tool's rules; normalise or label it.

## Date range picker

- Trigger: one pill showing the active range ("Last 30 days", or "6 Oct – 17 Oct 2026" for custom), chevron;
  optional ‹ › arrows to step to the previous/next period.
- Menu: presets grouped by hairlines (Today, 7 / 30 / 90 days, 12 months | Yesterday, This week, This month,
  Last month | Custom range…), check on the active row. Optional: a live "Now" row with a green dot, one-letter
  keyboard shortcuts as `kbd` chips (disabled while typing in an input), the current time as a header line.
- **Custom range… swaps the menu for a calendar** (back link "‹ Ranges"):
  - One month, Monday-first, 6 fixed rows (no height jump), 36 px cells, weekday letters 11 px muted.
  - Click first day, then last; a click before the start moves the start; while picking, the band follows the
    pointer.
  - Range = soft band `bg-accent/10` between solid circular end days `bg-accent text-on-accent`; band halves
    round only at the outer edge where a week row breaks it.
  - Today: a small dot under the number. Days after today and beyond the allowed span are disabled.
  - Footer: "6 Oct – 17 Oct 2026 · 12 days" and an accent Apply button (disabled until both ends exist).
  - Phones: same calendar in a bottom sheet.
- Trap: native `<input type="date">` renders "21/09/2026 📅" and looks unfinished in every browser.

## Filters

- One Filter button opening a grouped menu: Source (channel, referrer, campaign) · URL (hostname, page, entry) ·
  Location · System · Visitor · Custom (goal).
- "Suggested filters" chips at the bottom ("Country is 🇺🇸 United States") built from the top rows.
- Active filters as removable chips under the header; a new filter dims the old numbers until the new ones land.

## Attention and actions

For: the Monitor step "what needs attention", answered by shape where the data already is.

- Flag the problem in place: a warm heatmap cell, a red overdue chip, a dashed "not done yet" cell. The flag is the
  most salient mark in its card.
- Put the action on or beside the flag: a not-marked cell is itself a "remind" button; a debtor row ends in call and
  remind icon buttons; a flagged pupil row opens the record. After the action the flag changes state (bell → check)
  and a toast confirms in one line.
- A separate attention row is the last resort, for a problem with no home on the screen: noun + number + action
  ("3 debtors over 30 days · View"), at most three, never full sentences, never repeating a tile.
- Deeper insight pages (visits-to-purchase, weekday × hour) can be gated behind the data they need, with a blurred
  sample and one call to action.

## Heatmap (matrix)

For: one measure across two dimensions where the grid is the point: classes × days, weekday × hour, team × week.

- Rounded pill cells (8–10 px radius, 32–36 px tall, 5–8 px gap), row labels left, column headers above with
  the latest column marked (accent number plus a dot): today when today has data, otherwise the latest complete day,
  with the "as of" date in the toolbar.
- Columns are a fixed trailing window (the last 7 days, labelled in the card header) whatever the page range; for a
  range past ~14 columns, aggregate to weeks instead of shrinking cells.
- Colour in classed tiers of one hue at meaningful thresholds, with intensity growing toward the problem: the
  healthiest values palest, the values nearing the threshold darker, and one warm tier past it. For attendance:
  ≥95 pale, ≥90 light, ≥85 medium, below 85 warm. For a lower-is-better metric like CPL: at or under target pale,
  up to 1.1× light, up to 1.2× medium, above 1.2× warm. Never a ramp where the worst cell is the palest, and never
  one where the best cell is the loudest (perception.md → inverted salience).
- The warm tier also carries a non-colour cue (an underlined or bold number, or a small ▲), so it survives
  greyscale and colour blindness. Check it under achromatopsia emulation while building, not only at the end.
- Text in every cell is ink (or ink-2), never the accent: accent text on an accent tint fails 4.5:1.
- Numbers in cells only on small grids (up to ~60 cells) with enough contrast; exact value and its parts
  ("5-A · 28 Oct · 20/26") in the tooltip.
- Missing data is its own state: a dashed outline cell with an icon, and when someone can fix it, the cell is the
  button that asks them to.
- Legend in the header row: the tier swatches with their thresholds and the missing-state swatch, one or two words
  each.

## Bullet graph

For: a measure against a target in a small space, the replacement for gauges and dials (Few's specification in
perception.md).

- Horizontal bar about a third of the track's height; the target as a short perpendicular line; two to five
  background ranges in intensities of one hue, darker for poor.
- Rows of bullet graphs share one layout and stack like a ranked list; each row: label, bullet, value.
- Future target: show actual and projected segments, so "on track?" reads today.

## Segmented share bar

For: a total split into a few ordered parts (debt by age, tickets by priority).

- One row of rounded pills whose widths are the parts' shares, 2–6 px apart, 8–10 px tall; ordered parts use one
  hue's intensities ending in the warning or danger hue.
- Legend under it: swatch, short label, amount; the share and exact amount in each segment's tooltip.

## Tables and recent activity

- Hairline row separators, muted date column, right-aligned amounts, small source chips with favicons.
- Money rows: flag · amount (18–20 px semibold) · product/country · source chip ("likely" in muted text when the
  source is estimated) · relative time with a live dot for the last hour.
- People rows: letter avatar (pastel tint of a categorical hue, initials) · name with one muted detail under it ·
  status chip · value · icon actions. On phones drop the avatar and the chip and fold their facts into the muted
  line ("8-A · 64 days"), before any name truncates.

## Words that remain

The few words left on a wordless screen do real work:

- Actions name what they do: "Remind teacher", "Call parent", "Keep subscription"; never "OK" / "Yes" / "Submit".
- One word per concept across the product: keep a word list, so a "debtor" is never also a "late payer".
- Empty states say what will appear here and how to get it ("Payments appear here after the first one is taken" +
  "Take payment"), not whimsy.
- Errors say what went wrong and offer the fix as a button; no "Oops", no error codes as the message.
- An instruction sits where the eye already is (next to the control), not in a banner elsewhere.
- Text expands in translation and weekday abbreviations differ by language (one letter, two letters, none): size
  for the longest locale and take abbreviations from the locale, not a hard-coded list.

## Tooltip

- One tooltip system for the whole screen: dark surface, white text, 12 px, 8–10 px radius, placed above the
  element and kept inside the viewport.
- Chart tooltips lead with the big exact value, then a muted label line (period, partial-period note).
- Every icon-only control and every compact number has one; it also shows on keyboard focus, and hides on scroll,
  on Escape and after the element it belongs to re-renders.

## Realtime

- "Now" = last 30 minutes; active = a hit in the last 5–10 minutes.
- Live count with a breathing green dot in the nav.
- A map/globe with avatars and a live feed is delightful but optional; a ranked "likely to buy" list with reasons
  is more useful.

## States

- **Loading**: skeleton blocks the size of the final content.
- **Stale** (another site/range/filter loading): keep the old payload visible but dimmed (`opacity-40
  pointer-events-none`); never flash zeros; ignore responses that arrive after a newer request.
- **Error**: one page-level note, shown even when old data is on screen ("Couldn't refresh. These are the last
  numbers…"); not the same message repeated in every card.
- **Empty**: never an all-clear ("nothing urgent today") on an account with no data; no data is not good news.
  Keep the structure; show sample data under a soft overlay with one call to action ("Add goals"), or a
  one-line hint. Revenue with no orders: "$0", flat grey sparkline, hint line.
- **Tiny data**: grey "was N" deltas, no percentages on bases under ~5, hide single-row tabs.
- **Sample data**: a clear SAMPLE banner with "Hide sample", never mixed with real numbers.

## Trust cues (revenue)

- Say what money means once: "net of tax, before fees, in USD".
- Label estimates: a "likely" chip with a tooltip stating the method; attributed vs likely counted separately.
- "Updated 2 min ago" with a spinner while refreshing; the tooltip states the real refresh interval.
