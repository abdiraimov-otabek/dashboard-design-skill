# Case study: a school's home dashboard, three versions

The home page of a school management system (October 2026): the director's first screen of the day. It went
through three versions in one day. Each was judged on screenshots, and the second was rejected by its owner in one
line: "a bunch of text speaks". Reach for this file when a dashboard explains itself in sentences, or when a
redesign is "honest but still not good".

## The question

"Is the school OK today, and what needs me?" Answered by: today's attendance, this month's payments, outstanding
debt, pupil count. Problems: a class that has not marked attendance, a class below 85%, a debt over 30 days, a pupil
in the warning zone. Actions: remind the teacher, call or remind the parent, open the pupil.

## Version 0: the original

- Numbers that disagreed: attendance "—" on the KPI while the heatmap showed data; "1 lead" next to "no leads";
  a "last 9 months" chart with future months; "+22%" with no baseline.
- A rainbow of icon tiles (seven hues meaning nothing), twelve KPI cards, a heatmap of 29 dashes out of 30 cells,
  a floating AI button over content, a header that overflowed at 1100 px.

Lesson: honesty first. The redesign started by making every number come from one fixture with a self-check.

## Version 1: honest, but a page of sentences (rejected)

Every number agreed (18 cross-checks passed), the layout was clean, and the owner hated it:

- An attention row of three sentences ("9-A and 9-B have not marked attendance today").
- A sentence under every KPI ("121 pupils expected, 110 came · 2 classes not marked").
- A note under every chart ("Daily %, the axis starts at 60%").

The rules that produced it were this skill's own defaults at the time: "one muted sub-line that explains the
number" and "an insights line of plain sentences". Both are now gone; the page reads as a report, and a director
scans rather than reads.

## Version 2: the page speaks for itself

Rebuilt after studying a dashboard designer's shipped work (sources.md → Designers):

- **Toolbar of pills**: branch, date, a green-dot "updated 10:42" that turns red with "not updated" on error.
- **KPI cards**: label, monochrome icon square, number, "▼ 15% vs Sep"; the sentence moved into the tooltip.
- **Attendance heatmap**: classes × last six school days as rounded number pills. Classed tiers: healthy values
  in pale-to-medium blue, below 85% in amber, not-marked as a dashed cell with a bell that *is* the remind button.
- **Revenue**: pastel bars with a solid cap, the unfinished month dashed, a dark tooltip with one big value.
- **Debt**: a segmented bar by age (0–30, 31–60, 60+ days) above the debtor list, each row ending in call and
  remind buttons.
- **School year**: three numbers with weekly sparklines.
- **Watch list and open leads**: letter-avatar lists.

## What the screenshots caught in version 2

1. **A blue wall.** The first heatmap used a plain light-to-dark ramp from 70% to 100%. Real attendance sits at
   86–100%, so every cell was dark, and the worst class (77%) was the palest cell on the grid: inverted salience.
   Fix: classed tiers plus a warm tier for "below target" (perception.md).
2. **Holes.** A ring chart beside the tall heatmap, and a one-row card beside a six-row table, left half-empty
   cards. Fix: the debt split moved into the debtor card as a segmented bar, and the short cards were paired in
   their own row.
3. **Truncated names on phones.** "Ergasheva …" while avatars and chips kept their space. Fix: drop the
   decorations first and fold the overdue days into the muted line ("8-A · 64 days").

## Lessons now in the skill

- Wordless: the sentence count on screen is a QA check, target zero (qa.md → Words audit).
- Attention lives on the data, with the action on or beside the flag (components.md → Attention and actions).
- Heatmaps use classed tiers with a warm problem tier, never a ramp where bad is pale. A later test build (an ad
  dashboard for targetologists) showed the mirror flaw in this very version: the healthiest cells were the darkest.
  The rule now says intensity grows toward the problem.
- No holes: restructure rows instead of stretching cards.
- On phones, decorations go before words truncate.
- The owner's stated taste beats the skill's defaults; when they conflict, note it and follow the owner.
