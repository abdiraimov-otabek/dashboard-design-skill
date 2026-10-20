# Components

Each pattern: what it is for, the spec, and the trap that shipped once and had to be fixed. Written in Tailwind
terms with the tokens from [tokens.md](tokens.md) (`accent` for traffic, `money` for revenue); translate freely to
any stack. Code for the fiddly parts: [snippets.md](snippets.md).

## KPI strip and the selected tile

For: the 3–7 headline numbers; clicking one picks the metric the main chart shows.

- One card, tiles divided by hairlines (`border-r border-line`), not seven floating cards.
- Tile content: label (14 px, ink-2) with the delta on the right · value (28–32 px semibold, `tracking-[-.03em]`,
  tabular) · one muted sub-line that explains it ("3% of visitors", "$7.31 per order, after tax") · sparkline.
- **Selected** = an inner rounded fill inside the cell: `rounded-xl bg-accent/[.06] ring-1 ring-inset ring-accent/20`
  (money metrics: `bg-money/[.07] ring-money/25`), label `font-medium text-ink`. Unselected: transparent,
  `hover:bg-soft/70`, value in ink-2, sparkline grey. Wrap the cell in `p-2` so the fill floats inside the dividers.
- Button with `aria-pressed`, visible `focus-visible` ring on the inner fill.
- Exact value in `title`/tooltip when the tile shows a compact number.
- Trap: an underline or left edge to mark selection reads as a heavy marker. Use the fill.

## Delta badge

- `+13%` green / `−9%` red, 12 px medium, tabular; `±0%` grey.
- Base below ~5 (counts) → `was 1` in grey with the formatted previous value. A red −100% for 1 → 0 is noise.
- Over ±999% → `10×+` / `−99%`.
- Never repeat a tile's delta in an insight card.

## Sparkline

- 24–40 px tall, 1.5 px line, faint fill, no axes. Selected tile in the metric colour, others grey.
- Trap: it must draw **the same window as the main chart**. If the chart trims empty leading days ("Nothing before
  26 Sep · show all"), trim the sparklines identically, or every tile becomes a flat line with a spike at the end.

## Main chart

- One metric at a time in its colour, 1.5–2 px line, gradient fill from ~15% to 0%. No point markers until hover.
- Y axis: 4–5 round ticks (0, 1k, 2k), labels 11–12 px muted, baseline 0. Odd ticks like 2,103 look broken
  (`niceTicks` in snippets.md).
- X axis: 5–7 ticks ("21 Sep"), never every day. Hourly for Today, daily up to ~120 days, monthly beyond.
- Previous period: grey or dashed line, no fill, behind the current series; legend "This period / Period before".
- Incomplete current bucket: dotted tail.
- Tooltip: date header, coloured dot + value, previous value and % change when comparing; vertical hairline.
- Revenue view: money as soft bars on a right-hand $ axis against the visitors line works well. Mark the biggest
  sale days with the source's logo over the bar, so the chart says where the money came from.
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
- Trap: one taxonomy per question. If an insight says "73% from Threads" while Channels says "Referral 73%",
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

## Insights line

- Plain sentences computed from the data: "56% of revenue from Mac users", "36 hours median to purchase",
  "Conversion peaks Monday 3 pm".
- Show a card only when it says something the tiles don't. Drop a top-page insight under ~3 visitors; plural-aware
  copy ("1 visitor").
- Prefer one slim row of 2–3 statements over wide, mostly empty cards.
- Deeper insight pages (visits-to-purchase, days-to-purchase bars, weekday×hour heatmap) can be gated behind the
  data they need, with a blurred sample and one call to action.

## Tables and recent activity

- Hairline row separators, muted date column, right-aligned amounts, small source chips with favicons.
- Money rows: flag · amount (18–20 px semibold) · product/country · source chip ("likely" in muted text when the
  source is estimated) · relative time with a live dot for the last hour.

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
- **Empty**: keep the structure; show sample data under a soft overlay with one call to action ("Add goals"), or a
  one-line hint. Revenue with no orders: "$0", flat grey sparkline, hint line.
- **Tiny data**: grey "was N" deltas, no percentages on bases under ~5, hide single-row tabs.
- **Sample data**: a clear SAMPLE banner with "Hide sample", never mixed with real numbers.

## Trust cues (revenue)

- Say what money means once: "net of tax, before fees, in USD".
- Label estimates: a "likely" chip with a tooltip stating the method; attributed vs likely counted separately.
- "Updated 2 min ago" with a spinner while refreshing; the tooltip states the real refresh interval.
