# Tokens

Define every colour once, for light and dark, then use tokens + alpha for tints (`bg-accent/10`), so a tint adapts
to the theme by itself. Starter set (Tailwind v4 `@theme`; plain CSS variables work the same):

```css
@import "tailwindcss";

@theme {
  --color-page: #f8f8f6;        /* app background */
  --color-card: #ffffff;        /* panels */
  --color-soft: #f1f1ef;        /* hover, segmented track */
  --color-side: #f3f3f1;        /* sidebar */
  --color-ink: #17171a;         /* primary text */
  --color-ink-2: #48484d;       /* secondary text, unselected values */
  --color-muted: #66666d;       /* labels, axes; >= 4.5:1 on every light surface */
  --color-line: rgb(0 0 0 / .075);        /* hairlines, bar tracks */
  --color-line-strong: rgb(0 0 0 / .14);  /* inputs, disabled text */
  --color-accent: #3e63dd;      /* traffic metrics, selection, focus */
  --color-on-accent: #ffffff;
  --color-money: #0f7f57;       /* revenue metrics */
  --color-up: #0f7f57;          /* good change */
  --color-down: #d23f45;        /* bad change on a meaningful base */
  --color-live: #12a150;        /* live dots */
  --shadow-card: 0 1px 2px rgb(0 0 0 / .04), 0 1px 1px rgb(0 0 0 / .02);
  --shadow-pop: 0 12px 32px -8px rgb(0 0 0 / .18), 0 0 0 1px rgb(0 0 0 / .06);
}

/* dark: same names, new values. Follows the system unless the app pins a theme with data-theme. */
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --color-page: #0b0b0d; --color-card: #141417; --color-soft: #1c1c20; --color-side: #101013;
    --color-ink: #f3f3f5; --color-ink-2: #c4c4ca; --color-muted: #8c8c95;
    --color-line: rgb(255 255 255 / .08); --color-line-strong: rgb(255 255 255 / .16);
    --color-accent: #7b96ff; --color-money: #34c48b; --color-up: #34c48b; --color-down: #ff6b70;
  }
}
:root[data-theme="dark"] { /* the same dark values again, for a pinned dark theme */ }
```

(Copy the dark values into the pinned-theme rule too; the point is one name, two values.)

## Rules

- Two semantic hues carry meaning: `accent` (traffic, selection) and `money` (revenue). Everything else is ink,
  muted or line. A third hue needs a reason (a third entity), not decoration.
- Tints are token + alpha: selection `bg-accent/[.06] ring-accent/20`, range band `bg-accent/10`, bar track
  `bg-line/70`, hover `bg-soft/70`.
- Check muted text contrast on every surface it sits on (card, soft, hover, page), in both themes.
- A theme setting inside the app overrides the system scheme: test dark mode by setting the app's theme too.
