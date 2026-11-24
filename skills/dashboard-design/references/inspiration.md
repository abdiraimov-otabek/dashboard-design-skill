# Inspiration: what experienced dashboard designers on X keep doing

A study of dashboard design posts on X (24 November 2026): eight searches ("dashboard design", "analytics dashboard",
"saas dashboard", "finance dashboard design" and more, each with a like floor of 150–500 and images only) returned
197 posts by 127 authors. The 64 most-liked posts by designers were looked at one by one; 43 of them are
dashboards (the rest were chat apps, landing pages and course covers). Counts below are "posts that do it / 45".

Use this file when a design needs taste beyond the rules: when the user says "make it look like a Dribbble shot",
when the page is honest but plain, or when you want a second visual direction. Borrow the craft, never a designer's
exact layout, brand or illustrations; credit them when the user asks where an idea came from.

## The designers to learn from

| Designer | What they are the reference for | Posts in the sample |
|---|---|---|
| **Marcel Kargul** (@marcelkargul) | Calm light dashboards: grey page, white cards, pill toolbars, pastel bars with a solid cap, one dark tooltip; the "page speaks for itself" school. Also clean mobile finance screens. | 13 of 64, 455–1,856 likes |
| **Sajibur Rahman** (@sajiburdesign) | Finance dashboards with one bold accent card (orange or green) and payment cards as objects. | 4 |
| **Sujon** (@sujon_co) | Finance and medical concepts: green highlight bar, wallet rows with flags, soft tooltips. | 4 |
| **ln_dev7** (@ln_dev7) | Open-source shadcn dashboard layouts, dark: a dense, real, buildable reference rather than a concept. | 3 |
| **Toby Belhome** (@TobyBelhome) | shadcn/ui CRM and finance templates: ring with the value in the centre, tasks next to numbers. | 2 |
| **Salung Prastyo** (@salungprastyo) | Mini bars inside KPI tiles and a dot-matrix bar chart that reads as texture. | 2 |
| **Bagus Fikri** (@bagus_fikri) | Insight cards: each metric with its own small line chart, and a cohort grid inside a card. | 1 |
| **Yasir Ahmad Noori, heysatya, Augustas** | Light work and finance dashboards with an AI side panel that is an action, not a paragraph. | 1 each |

## Patterns across the 43

| Pattern | Count | Example posts |
|---|---|---|
| Light page | 27/43 | Marcel Kargul, Sujon, Sajibur, Barly |
| Dark page | 16/43 | ln_dev7, Toby Belhome, Marcel Kargul (FlowSync) |
| A greeting as the page title ("Welcome back, Marcel", "Good morning, Sajibur") | 16/43 | ln_dev7, Sajibur, Sujon, Salung Prastyo |
| One highlighted bar among pale bars, with a dark tooltip on it | 9/43 | Sujon, Barly, heysatya, Yasir |
| A donut or ring with the total in its centre | 7/43 | Toby Belhome, ln_dev7, TailAdmin |
| Payment or wallet cards drawn as objects | 6/43 | Sajibur, Sujon, Mide Ajibade |
| A 3D render, photo or drone shot as the main visual | 6/43 | srotimi_ui, UiRahMan92, Sujon (medical heart) |
| An AI panel: suggested questions, or "your week, summarized" as an action | 5/43 | Marcel Kargul, Yasir, heysatya, Augustas |

What the numbers say:

- **Style does not decide likes.** Dark posts had a median of 709 likes, light 628; every pattern above sits between
  about 620 and 750. The author decides likes: Marcel Kargul alone posted 13 of the 64. Pick the look for the
  reader, not for the feed.
- **The highlighted bar is the most copied chart idea.** Nine designers make the whole series pale and colour only
  the bar that matters (this month, the selected point) with its value in a dark tooltip. It is the visual form of
  this skill's "quiet until something matters".
- **Greetings are everywhere and cost a line.** A short greeting is fine as the page title; the sentence under it
  ("Here's what's happening with your store today") is the first thing to delete (Wordless).
- **Concept shots are not dashboards.** Drone footage, 3D hearts and isometric buildings get likes as art; in a
  product the picture pushes the numbers below the fold. Keep the craft, skip the backdrop.

## Rules designers wrote down

Short rule lists that designers posted (each is one person's practice, not a standard; where one differs from tokens.md
or layout.md, the skill's tokens win):

- **@_heyrico**, dashboard cheatsheet: 14 px base font; 16 px base icons; icon strokes of 1, 1.2 or 1.5; regular and
  medium weights, semibold rarely.
- **@Tanjim38**, SaaS dashboard cheatsheet: Inter at 14 px body with −0.2 px letter spacing; a 240 px sidebar; table
  rows at least 48 px tall; the primary action top right; empty states with a picture and an action, never just
  "No data".
- **Marcel Kargul**, mobile: consistent spacing, light drop shadows, a 430 × 932 frame, one great typeface (Inter,
  Geist, SF Pro or SF Pro Rounded), simplify everything down.

## Steal these

1. **The quiet series with one lit bar.** All bars in a pale tint of the accent; the current or selected bar solid,
   with a dark tooltip holding one big value and the comparison under it. (Sujon, Barly, heysatya)
2. **Pastel bars with a solid cap.** Each bar a pale fill with a 3–4 px solid top, so stacked or grouped bars stay
   calm. (Marcel Kargul)
3. **KPI tiles with a texture.** A mini bar chart or dot matrix inside each tile shows its own week without a second
   chart. (Salung Prastyo)
4. **An attention banner with a count and an action.** "12 pending leave requests and 5 overtime approvals need
   action" with the button beside it: the monitor pattern in one line. (ln_dev7)
5. **One accent card.** In a grid of white cards, one card (the balance, the goal) in the brand colour carries the
   number that matters most. Only one. (Sajibur, Sujon)
6. **Objects for money.** A drawn card or wallet row with a flag and currency reads as "my money" faster than a
   table. Finance only. (Sajibur, Mide Ajibade)
7. **An AI panel that does things.** Suggested questions ("How much runway do I have left?") or "Summarize my week"
   as buttons. Never an AI paragraph of insights on the page. (Marcel Kargul, heysatya, Augustas)
8. **A cohort grid inside an insight card.** Retention as a small tiered grid next to the metric it explains.
   (Bagus Fikri)

## Skip these

- Rainbow stacked bars (five hues in every bar) and multi-line charts in neon on black: the eye finds no answer.
- A big pie with a dozen slices; a donut used where a number would do.
- Photos, 3D renders and isometric scenes behind or instead of the data.
- A paragraph under the greeting.
- More than one accent card, or every card coloured.

## Also: live products

The first study (sources.md) read shipped products. Revisited in the same week, a few still teach patterns the
designers above do not show:

- **Simple Analytics**: annotations on the chart ("HN job post"), the only chart in either study that says why.
- **Baremetrics**: "from $183,045" beside the headline, and a breakdown of what moved MRR.
- **OpenStatus, Claude Status**: rows of daily uptime bars, the open incident first.
- **OpenRouter**: "Usage data through Nov 23" under the title, and a two-column leaderboard.
- **Cloudflare Radar**: the map as the hero only because place is the question.
- **Apple Stocks**: name, sparkline, value and a delta pill in one row; the model for a list.
