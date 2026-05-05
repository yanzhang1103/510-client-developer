# Mid-point check — Client-02 review

**Date:** May 4, 2026
**Reviewer (client role):** Yan
**Project under review:** Creator Check-in (`app/index.html`)
**Spec being tested against:** [docs/client-spec.md](client-spec.md), v1.1

---

## Task 1 — Access the work from the developer

The developer's working build is at `app/index.html` on the `main` branch. The file opens directly in the browser, no build step required.

For this review, the build was run locally in:
- Chrome 134 on macOS 14.6
- Safari 18 on macOS 14.6
- Mobile viewport simulation in Chrome DevTools (375 × 812 iPhone preset)

Git history was reviewed via `git log --oneline`. Commits are atomic and describe the feature added in each step (form scaffold → scale interactions → localStorage write → history rendering → insights view → chart).

## Task 2 — Test core features against acceptance criteria and timeline

Each acceptance criterion from §4 of the spec was tested manually. Pass/fail summary:

| # | Criterion | Result | Notes |
|---|-----------|--------|-------|
| AC-1 | Submit valid check-in | ✅ pass | Form saves entry; toast confirms. |
| AC-2 | Reject incomplete | ⚠️ partial | Save is correctly blocked, but error feedback is too quiet — see Bug #1. |
| AC-3 | Form clears after save | ✅ pass | All scales reset, note field cleared, phase resets to "pre". |
| AC-4 | History view | ⚠️ partial | Functional, but date format collapses across weeks/months — see Bug #2. |
| AC-5 | Insights totals & averages | ✅ pass | Spot-checked with hand calculations on 6 known entries. |
| AC-6 | Chart edge cases | ⚠️ partial | 0 and 14+ render cleanly. 1 entry triggers SVG console warning — see Bug #3. |
| AC-7 | Reset confirmation | ✅ pass | `confirm()` dialog works; cancel preserves data; OK clears it. |
| AC-8 | Reload persistence | ✅ pass | localStorage round-trip verified across full reload and DevTools "empty cache and hard reload". |
| AC-9 | Mobile 375px | ⏳ deferred | Layout looks correct in DevTools simulation. Real-device test scheduled for Sprint 3. |

**Timeline test.** Per spec §5, Sprint 1 (form + storage) and Sprint 2 (history + insights + chart) should be complete by today. Both are. The build covers every in-scope feature listed under MVP, so the developer is on track relative to the original timeline.

## Task 3 — Evaluation: is the developer on track?

**Yes, on track. Conditional acceptance for the mid-point.**

What this means concretely:

- 6 of 9 acceptance criteria fully pass.
- 3 are "partial pass" — the feature works but has a defect documented in a filed bug.
- 1 (AC-9, mobile) is not fully verified yet but is explicitly scheduled for Sprint 3, which matches the original plan.
- No bugs filed today are blockers. None require re-architecting. All have a suggested fix in the report.
- No scope creep. The build does exactly what the spec describes — no surprise features, no missing features.

**What I (client) need to see by end of Sprint 3:**
1. Bugs #1, #2, #3 closed.
2. AC-9 verified on at least one real mobile device.
3. README updated again with Sprint 3 changelog.

If those land, the project will be ready for the demo-prep phase as scheduled. If any of them slip, we re-negotiate scope before demo day rather than ship broken features.

## Task 4 — Bug reports filed

Three distinct bugs filed today as GitHub Issues. Each has reproduction steps and a screenshot.

| # | Title | Severity | AC affected |
|---|-------|----------|-------------|
| 1 | Validation feedback is too quiet — missing fields not highlighted | Major | AC-2 |
| 2 | History date format lacks year and grouping; ambiguous for older entries | Major | AC-4 |
| 3 | Insights chart has no Y-axis labels; single-entry case logs SVG warning | Major | AC-5, AC-6 |

Full text for each is in `docs/bug-reports/`. The same content is filed as GitHub issues using the bug-report template at `.github/ISSUE_TEMPLATE/bug-report.md`.

---

## Mid-point sign-off (client)

The developer's work to date is **conditionally accepted** at mid-point. Continued payment / continued engagement contingent on resolving the three filed bugs and verifying AC-9 by end of Sprint 3.

— Yan, May 4, 2026
