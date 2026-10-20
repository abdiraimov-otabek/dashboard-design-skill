# Layout

## Page order

Header row (title left; "Updated …", Filter, date range right, in one pill group) → setup or sample banner when
relevant → KPI strip + main chart in one card → insights line → breakdown panels → recent activity / tables.

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
- Insights: 1 → 2 → up to 4 across, only as many cards as there are real statements (2+; one lonely card reads as
  a leftover).
- Panels: 1 → 2 (`lg`) → 4 (≥112.5rem). Equal heights per row are fine; keep row counts similar (limit 8) so a
  2-row Devices panel doesn't float in a tall empty card — or let short panels hug content.

## Phones (375 px)

- No horizontal page scroll; check `document.documentElement.scrollWidth === innerWidth`.
- Navigation: site picker + current page + a **Menu** button opening a grid of all pages (3 columns, icon over
  label); close on tap, on Escape, on outside tap, on route change. Not a sideways-scrolling tab row.
- Charts: `touch-pan-y` (never `touch-none`) so a vertical swipe still scrolls the page.
- Segmented tabs: shrink and truncate with `title`, never scroll.
- Date calendar: bottom sheet, one month.

## Density and type

- Base 14 px, labels 12–13 px muted, KPI values 28–32 px, panel titles 15–16 px semibold.
- Cards: `rounded-2xl border border-line bg-card shadow-card p-6`; inner rows `h-10–11`.
- Hairlines at ~7.5% ink; muted text ≥ 4.5:1 contrast on every surface it sits on.

## Dark mode

- Every colour is a token defined for both themes (`--color-line`, `--color-muted`, `--color-accent`…); tints are
  token + alpha (`bg-accent/10`), so they adapt.
- Check dark mode on screenshots by setting the app's own theme, not only the browser colour scheme (an app theme
  setting overrides `prefers-color-scheme`).
