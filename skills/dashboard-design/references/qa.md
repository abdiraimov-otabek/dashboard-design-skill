# QA pass

Run it before showing anyone, and before every UI commit. Look at every screenshot (open the PNG); reading the code
is not seeing the screen.

## Known totals (numbers before pixels)

Screenshots catch broken layouts, not three components agreeing on the same wrong number. Before the screenshot pass:

1. **Seed a small fixed dataset** (a fixture, or the app's sample-data switch with a fixed seed) and work out the
   expected answers outside the dashboard's code: by hand, or in a script that doesn't import its queries. Period
   total, previous-period total and delta, busiest day, the top row of each ranked list and its share.
2. **Check each component on its own** against those answers, reading what it renders rather than shared state:
   - KPI tile: the number and the delta as displayed.
   - Chart: the plotted series summed over the range equals the tile total; the peak is the busiest day.
   - Table or ranked list: rows (plus any "Other") sum to the total; the top row and its share match.
   - Every insight, tooltip or caption that repeats a number.
3. **Make it a test that fails on a mismatch**: Playwright reading the tile text, the chart's data or aria labels
   and the table footer, or unit tests on the selector feeding each component. Rerun it after any change to
   queries, ranges, time zones or rounding.

Done when every component matches the expected answers independently. Then screenshots.

## Screenshot protocol

- Drive the real app with Playwright (`npm i -D playwright && npx playwright install chromium`, or reuse an install
  elsewhere on the machine). `deviceScaleFactor: 2` for crisp crops.
- Logged-in pages: create a throwaway account through the app's own sign-up API, add a site, switch on sample or
  seed data, and delete the account at the end. If sign-up is rate-limited per IP and the dev server trusts
  `X-Forwarded-For`, give each run its own value, or the run silently lands on the login page.
- Widths: **3440** (ultrawide), **1440** (laptop), **375** (phone, full page).
- Capture: each mode or tab, a selected tile, the date menu open, the custom calendar mid-pick (start set,
  hovering) and complete, the filter menu, the phone menu open, an empty account, dark theme.
- Crop to the component (`locator.screenshot()` or `clip`) to judge details; full page to judge balance.
- Verify layout by measurement when unsure: `getComputedStyle(el).gridTemplateColumns`, and on phones
  `document.documentElement.scrollWidth === innerWidth`.

## Consistency checks (honest)

- The same number agrees everywhere: tile vs insight, chart peak vs "busiest day", channel vs source share.
- Sparklines and the main chart cover the same days.
- No red delta on a base under ~5; the comparison window is the same length and the same elapsed time.
- No `NaN`, `Infinity`, `–$0.00`, `−0%`, `1m 60s`, `1 visitors`, `0.0%`.
- Switch site and range quickly: old data dims, nothing flashes to zero, an older response never overwrites a newer one.
- A failed fetch shows one note even while old data is on screen.
- Tooltip and helper text match reality (refresh interval, what "revenue" includes).

## Smell list (spot it → do this instead)

| Smell | Instead |
|---|---|
| Tinted block behind each list row | 3 px bar along the row's bottom edge |
| Underline or left edge marking the selected tile | Soft tinted fill + faint ring |
| Native date inputs | Popover calendar with a band and end caps |
| Narrow centred column on a wide screen | Wide page mode, more columns |
| Sideways-scrolling tabs or nav | Shrinking segmented control; Menu grid on phones |
| Red −100% on 1 → 0 | Grey "was 1" |
| A card repeating a tile's number | Delete the card |
| Wide cards holding one small number each | One slim insights row, or nothing |
| Random y-axis ticks (2,103) | Round ticks (1k, 2k), 0 baseline |
| Flat sparkline with a spike at the end | Trim to the chart's window |
| Two names for one thing ("Threads" vs "Referral") | One taxonomy, labelled source |
| A 2–3 slice donut as the main view | Ranked list with share bars |
| Glossy glass, neon gradients, 3D icons in KPI cards, a date chip on every card | Quiet surfaces, one accent, one global range |
| The same error text in every card | One page-level note |

## Tailwind v4 gotchas met in practice

- An arbitrary px breakpoint (`min-[1800px]:`) is not ordered against named rem breakpoints and can lose to `lg:`.
  Write it in rem (`min-[112.5rem]:`).
- Class names must appear literally in source; strings assembled from fragments are never generated.
