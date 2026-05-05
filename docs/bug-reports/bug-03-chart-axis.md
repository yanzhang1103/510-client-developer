# Bug #3 — Insights chart: no Y-axis labels and no gridlines, so the line is shape-only — users cannot read off actual energy values

> Filed during Client-02 mid-point review. Use this content when creating the GitHub issue.

## Summary

The "energy over last 14 check-ins" chart on the insights tab draws a polyline correctly, but has no Y-axis ticks, no labels (1 / 2 / 3 / 4 / 5), and no horizontal gridlines. The user can see that energy went *up* or *down*, but cannot tell whether a peak is a 3 or a 5 without counting pixels.

A single edge case also reproduces a console warning: when there is exactly **one** check-in saved, the chart renders a single dot but the polyline produces an SVG warning because `points` contains only one coordinate pair.

## Acceptance criterion affected

**AC-5** — *Insights view shows correct totals and averages.* (averages are correct, but the chart visualizing the same data is unreadable in absolute terms)

**AC-6** — *Insights chart renders without error for 0, 1, and 14+ entries.* (0 and 14+ work, 1 logs a console warning)

## Environment

- **Browser:** Chrome 134, Safari 18
- **OS:** macOS 14.6
- **Build / commit:** `app/index.html` @ current `main`
- **Date observed:** May 4, 2026

## Steps to reproduce

### Reproducing the unreadable Y-axis (AC-5)

1. Save 6+ check-ins with varied energy values (e.g. 1, 4, 2, 5, 3, 4).
2. Switch to the **insights** tab.
3. Look at the line chart and try to determine the highest energy value without checking the underlying entries.

### Reproducing the single-entry console warning (AC-6)

1. Open the page in a fresh browser profile, or click "reset all data".
2. Save exactly **one** check-in.
3. Open DevTools → Console.
4. Switch to the **insights** tab.

## Expected behavior

- Y-axis shows tick marks at 1, 2, 3, 4, 5 with light gridlines so values are readable.
- With one data point, the chart shows a single dot and produces no console warnings.

## Actual behavior

- Y-axis is empty. The polyline floats inside an unlabeled box. To know that yesterday's energy was a 4, the user must mentally interpolate based on the chart height.
- With one data point, the polyline element receives a single `x,y` pair instead of two; Chrome logs an SVG warning about the malformed `points` attribute. Visually it still works (just the dot is shown) so this is minor, but it indicates a code path that wasn't designed for this case.

## Screenshot / video

- `assets/bug-03-chart-noaxis.png` — chart with 6 entries, no axis labels.
- `assets/bug-03-chart-console.png` — DevTools console showing the warning with 1 entry.

## Severity

- [ ] Blocker
- [x] Major — chart is the headline feature of the insights tab; without Y-axis labels it doesn't deliver insight, only shape.
- [ ] Minor

## Suggested fix

In `renderInsights()`:

1. Before drawing the polyline, render 5 horizontal gridlines (one per integer from 1 to 5) and label each on the left side using SVG `<text>` elements. Use the existing `--muted` color at low opacity.
2. Guard the polyline against the single-point case: if `recent.length === 1`, skip drawing the `<polyline>` and render only the `<circle>`.
