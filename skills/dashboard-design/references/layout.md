# Layout

## Page order

Header row (title left; "Updated …", Filter, date range right, in one pill group) → setup or sample banner when
relevant → KPI cards (+ main chart in one card when tiles drive it) → the main view where problems show →
breakdown panels → recent activity / tables. Most important top-left: readers scan top-down in an F, and the top
gets the most attention.

## Width

- Content pages (settings, forms, docs): cap at ~1180 px, centred.
- Dashboards: grow on big screens. From 1800 px viewport the content may reach ~1640 px and the four breakdown
  panels sit in one row (`lg:grid-cols-2` → 4 columns). An ultrawide window showing a 1,100 px column between two
  empty bands reads as broken.
- Make "wide" opt-in per page (a `wide` prop on the page shell that the header row follows too), so forms stay narrow.
- **Tailwind v4 gotcha**: an arbitrary breakpoint in px (`min-[1800px]:`) is not ordered against named rem breakpoints
  (`lg:` = 64rem) and can lose to them. Write it in rem: `min-[112.5rem]:grid-cols-4`. Verify the computed
  `grid-template-columns` in the browser.
- Class strings must stay literal (`'min-[112.5rem]:max-w-[1640px]'`), never assembled from fragments, or Tailwind
  never generates them.

## Grids

- KPI strip: 2 columns on phones, 3 on small screens, 5 (or the tile count) from `lg`.
- Attention row (only when a problem has no home on the screen): 1 → up to 3 items across, noun + number + action,
  never sentences; two or more items, since one lonely card reads as a leftover.
- Panels: 1 → 2 (`lg`) → 4 (≥112.5rem), or a 12-column grid with 7 + 5 and 6 + 6 rows.
- **No holes**: cards in one row hold similar amounts of content (limit 8 rows each). When one card is half empty,
  restructure (fold it into its neighbour, pair it with another short card, move it to a shorter row) instead of
  stretching it; a stretched card with a blank lower half reads as broken.

## The monitoring view fits one screen

The KPI cards and the main view where problems show fit above the fold at 1440 × 900 (Few's first mistake is a
monitoring view that needs scrolling). Breakdowns and detail lists may scroll; the answer and the problems may not.
This rule wins over "KPI strip + main chart in one card": on a monitoring screen the KPI cards only report, and the
trend chart moves below the problem view; the tile-driven chart belongs to analytics screens.

## Phones (375 px)

- No horizontal page scroll; check `document.documentElement.scrollWidth === innerWidth`.
- Navigation: site picker + current page + a **Menu** button opening a grid of all pages (3 columns, icon over
  label); close on tap, on Escape, on outside tap, on route change. Not a sideways-scrolling tab row.
- Charts: `touch-pan-y` (never `touch-none`) so a vertical swipe still scrolls the page.
- Segmented tabs: shrink and truncate with `title`, never scroll.
- Date calendar: bottom sheet, one month.
- Rows fold before they truncate: drop decorations (avatars, icon squares, chips) and move their facts into the
  muted second line, so names and numbers stay whole.
- Heatmaps keep every column at 375 px: narrower label column (36 px), 5 px gaps, 32 px cells, legend hidden
  (the tooltip still explains each cell). That holds for up to ~7 columns; components.md → Heatmap says what a
  longer range does.

## Density and type

- Base 14 px, labels 12–13 px muted, KPI values 28–32 px, panel titles 15–16 px semibold.
- Cards: `rounded-2xl border border-line bg-card shadow-card p-6`; inner rows `h-10–11`.
- Hairlines at ~7.5% ink; muted text ≥ 4.5:1 contrast on every surface it sits on.

## Dark mode

- Every colour is a token defined for both themes (`--color-line`, `--color-muted`, `--color-accent`…); tints are
  token + alpha (`bg-accent/10`), so they adapt.
- Check dark mode on screenshots by setting the app's own theme, not only the browser colour scheme (an app theme
  setting overrides `prefers-color-scheme`).
