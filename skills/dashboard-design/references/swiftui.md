# SwiftUI (iOS, iPadOS, macOS)

The rules in SKILL.md and the patterns in components.md hold on every platform. This file maps them to SwiftUI and
Swift Charts, and replaces the browser QA with a simulator one. Targets iOS 17 / macOS 14 and later.

## Tokens

- Colours live in the asset catalog with Any and Dark appearances: `Accent` (traffic, selection), `Money`
  (revenue), `Up`, `Down`. Everything else is semantic: `.primary`, `.secondary`, `.tertiary`, separators from
  `Color(.separator)` (iOS) / `Color(nsColor: .separatorColor)` (macOS).
- Tints are the token with opacity: selection `Color.accentColor.opacity(0.06)`, range band `.opacity(0.10)`,
  share-bar track `.quaternary`.
- Numbers: `.monospacedDigit()` on every changing value; text styles (`.title`, `.headline`, `.caption`) so Dynamic
  Type works, never fixed point sizes for text.

## Numbers

```swift
extension Double {
    var compact: String { formatted(.number.notation(.compactName).precision(.fractionLength(0...1))) } // 1.2K
    var usd: String { formatted(.currency(code: "USD").precision(.fractionLength(0))) }
    /// Share of a total in percent: never "0.0%" for a real but tiny share.
    var share: String { self == 0 ? "0%" : self < 0.1 ? "<0.1%" : self < 1 ? String(format: "%.1f%%", self) : "\(Int(rounded()))%" }
}
```

The delta rule is the same as the web one: no previous value → nothing; previous under ~5 → "was 1" in
`.secondary`; otherwise a signed percentage in `Up` / `Down`, `±0%` in `.secondary`.

## KPI tile and the selected fill

```swift
struct KPITile: View {
    let label: String, value: String, sub: String, delta: Text?, series: [Double]
    let selected: Bool, money: Bool
    var tint: Color { money ? Color("Money") : .accentColor }
    var body: some View {
        VStack(alignment: .leading, spacing: 4) {
            HStack { Text(label).fontWeight(selected ? .medium : .regular); Spacer(); delta }.font(.subheadline)
            Text(value).font(.title.weight(.semibold)).monospacedDigit().foregroundStyle(selected ? .primary : .secondary)
            Text(sub).font(.caption).foregroundStyle(.secondary).lineLimit(2)
            Sparkline(values: series, color: selected ? tint : .secondary)   // same window as the main chart
        }
        .padding(12)
        .background(selected ? tint.opacity(0.06) : .clear, in: .rect(cornerRadius: 12))
        .overlay { if selected { RoundedRectangle(cornerRadius: 12).strokeBorder(tint.opacity(0.22)) } }
        .contentShape(.rect)
        .accessibilityAddTraits(selected ? [.isButton, .isSelected] : .isButton)
    }
}
```

Tiles sit in one container divided by hairlines (`Divider()` between them), not as separate floating cards.

## Charts (Swift Charts)

```swift
Chart {
    ForEach(previous) { p in                                     // the period before: grey, dashed, behind
        LineMark(x: .value("Day", p.day), y: .value("Value", p.value), series: .value("Period", "Before"))
            .foregroundStyle(.gray.opacity(0.6)).lineStyle(StrokeStyle(lineWidth: 1.5, dash: [4, 3]))
    }
    ForEach(current) { p in
        AreaMark(x: .value("Day", p.day), y: .value("Value", p.value), series: .value("Period", "Now"))
            .foregroundStyle(.linearGradient(colors: [tint.opacity(0.15), tint.opacity(0)], startPoint: .top, endPoint: .bottom))
        LineMark(x: .value("Day", p.day), y: .value("Value", p.value), series: .value("Period", "Now"))
            .foregroundStyle(tint).lineStyle(StrokeStyle(lineWidth: 2))
    }
    if let day = selectedDay {                                   // hover / scrub hairline with the value
        RuleMark(x: .value("Day", day)).foregroundStyle(.secondary.opacity(0.4))
            .annotation(position: .top, overflowResolution: .init(x: .fit, y: .disabled)) { Tooltip(day: day) }
    }
}
.chartYScale(domain: 0...ticks.last!)                            // ticks = niceTicks(max), ported from snippets.md
.chartYAxis { AxisMarks(position: .leading, values: ticks) { AxisGridLine(); AxisValueLabel() } }
.chartXAxis { AxisMarks(values: .automatic(desiredCount: 6)) }
.chartXSelection(value: $selectedDay)
```

- Round ticks: pass explicit `values:` from a ported `niceTicks`; `.automatic(desiredCount:)` alone can still land
  on odd values.
- Today's incomplete bucket: draw the last segment as its own `LineMark` series with `dash: [2, 3]`.
- Revenue view: `BarMark` for money on a second scale reads well; keep the visitors line on top.
- Sparkline: the same `Chart` with `.chartXAxis(.hidden)`, `.chartYAxis(.hidden)`, height ~32, no area or a faint one.
- Accessibility: give marks `.accessibilityLabel` / `.accessibilityValue`, or a full `.accessibilityChartDescriptor`
  so VoiceOver users get Audio Graphs.

## Ranked list with a slim share bar

```swift
HStack(spacing: 10) {
    icon.frame(width: 16)
    Text(name).lineLimit(1)
    Spacer()
    Text(count, format: .number).monospacedDigit()
    Text(sharePercent.share).font(.caption).foregroundStyle(.secondary).frame(width: 44, alignment: .trailing)
}
.padding(.vertical, 8)
.overlay(alignment: .bottom) {
    GeometryReader { g in
        Capsule().fill(.quaternary)
            .overlay(alignment: .leading) { Capsule().fill(tint.opacity(0.75)).frame(width: max(2, g.size.width * barFraction)) }
    }
    .frame(height: 3)
}
```

## Date range

- A `Menu` (or `Picker` with `.menu` style) of presets with a checkmark on the active one: Today, 7 / 30 / 90 days,
  12 months, Yesterday, This week, This month, Last month, then "Custom range…".
- Custom range opens a sheet (iOS) or popover (macOS) with the one-month grid from snippets.md ported to a
  `LazyVGrid(columns: Array(repeating: GridItem(.flexible(), spacing: 0), count: 7))`: soft band between solid
  circular end days, today's dot, future days disabled, "12 days" + Apply. Two graphical `DatePicker`s for start
  and end are the acceptable fallback; `MultiDatePicker` picks separate days, not a range.
- On iPhone the sheet uses `.presentationDetents([.medium, .large])`.

## Layout

- Panels: `LazyVGrid(columns: [GridItem(.adaptive(minimum: 320), spacing: 16)])` grows columns with the window,
  the native form of "width grows with the screen" (a resizable Mac window, iPad split view).
- KPI strip: `ViewThatFits` from one row of tiles to a 2-column `Grid`; at accessibility text sizes
  (`dynamicTypeSize.isAccessibilitySize`) stack label and value vertically instead of truncating.
- iPhone navigation: a `TabView` with at most 5 tabs, or a `NavigationStack` list; never a sideways-scrolling row.
- macOS: `NavigationSplitView` sidebar + content; toolbar holds the range menu and filter.

## States

- Loading: `.redacted(reason: .placeholder)` on the real layout.
- Empty: `ContentUnavailableView` with one action, or sample data with a clear "Sample" badge.
- Stale (new range loading): keep the old content at `.opacity(0.4)` with `.allowsHitTesting(false)`; cancel or
  ignore older `Task`s (`.task(id: range)` cancels the previous one automatically).
- Error: one banner for the screen, not one per card.
- Motion: number tweens (`.contentTransition(.numericText())`) only when `accessibilityReduceMotion` is false.

## QA pass (simulator)

After every UI change: build, run, screenshot, look, fix. Before the full pass, check known totals (qa.md): a
fixed sample dataset with hand-computed answers, and an XCTest per component (tile, chart data, list rows) that
fails on a mismatch. Then the full pass:

```bash
xcrun simctl boot "iPhone 16 Pro"                                             # and a small one (iPhone SE) and an iPad
xcrun simctl ui booted appearance dark                                        # then light
xcrun simctl ui booted content_size accessibility-extra-extra-extra-large    # biggest Dynamic Type; reset to large
xcrun simctl io booted screenshot ~/Desktop/qa-iphone-dark-ax5.png
```

- Sizes: smallest iPhone, largest iPhone, iPad portrait and landscape; Mac at a narrow and a wide window
  (`screencapture -l <windowID>` or `ImageRenderer` on the view in a test).
- One pass with Increase Contrast (`xcrun simctl ui booted increase_contrast enabled`) and one with Reduce Motion
  on (Settings › Accessibility › Motion in the simulator).
- Open every screenshot and run the consistency checks and smell table from qa.md; they apply unchanged.
- `#Preview` with fixed sample data for each state (empty, tiny data, loading, error) catches most issues before
  the simulator.
