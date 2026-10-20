# Case study: DataFast

A revenue-first web analytics product (datafa.st), studied in October 2026 from its public demo, a trial account,
its documentation and changelog. Summarised in our own words for the design lessons; no affiliation.

## Patterns worth learning from

- **Top bar** as one row: site picker · ‹ range › (step to previous/next period) · Compare · granularity · Filter ·
  refresh.
- **Date menu** with the current time as a header line, a live **Now** option, one-letter shortcuts on each preset,
  "More periods" collapsed, and Custom as a two-month calendar with typed start/end fields.
- **KPI strip** that includes the money ratios a revenue product lives on: revenue, conversion rate, revenue per
  visitor, alongside visitors, bounce, session time and a live "online" count.
- **Revenue on the main chart**: visitors as a line, revenue as bars on a right-hand currency axis, and the source's
  logo pinned over the days with sales.
- **Empty sections that sell themselves**: goals, funnels and journeys show sample data under a soft overlay with a
  single call to action, so a new user sees what they will get.
- **Grouped filter menu** (source, URL, location, system, visitor, custom) with suggested filter chips built from
  the current top rows.
- **Insights page** written as sentences ("most revenue from desktop users"), with visits-to-purchase and
  days-to-purchase bars, a median time to purchase, and a weekday × hour heatmap; locked behind the data it needs,
  with a blurred preview.
- **Onboarding**: a corner checklist of setup steps, and a "set up with AI" card that copies a ready prompt for a
  coding agent.
- **Agent-friendly docs**: every docs page also served as Markdown, an `llms.txt` index, an MCP server whose writes
  preview first and need confirmation, a CLI and an API playground.
- **Realtime as delight**: a globe of live visitors with friendly generated names and avatars, next to a live feed.

## Trade-offs to weigh when borrowing

- Attribution relies on a long-lived first-party cookie; the cookieless mode is documented as less capable. A
  privacy-first product would pair these UI patterns with cookieless matching.
- Two ways to detect a sale (redirect URL and payment metadata) can double-count unless one is switched off — a
  reminder to make the default path the safe one.
- Ranked rows use tinted bars behind the text; the slim-bar pattern in components.md reads cleaner.
- Alerts are email-only at the time of study; chat channels (Slack, Telegram, Discord) are a common ask.
