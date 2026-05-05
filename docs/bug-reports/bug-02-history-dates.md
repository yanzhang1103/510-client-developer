# Bug #2 — History view: same-day entries all show only month + day, no year, making it ambiguous which week an entry belongs to

> Filed during Client-02 mid-point review. Use this content when creating the GitHub issue.

## Summary

On the history tab, every entry's date label is rendered as `"May 4"` (month + day) plus the time. When the user has check-ins spanning multiple weeks or months — exactly the use case AC-4 implies — there's no year displayed, and no separator between days. After 10+ entries it becomes very hard to tell at a glance which entries are from this week versus a month ago.

## Acceptance criterion affected

**AC-4** — *History view shows all saved check-ins, most recent first, with date, phase, ratings, and note if present.*

The date is shown, but the format is too compressed to function as a real date once the dataset grows.

## Environment

- **Browser:** Chrome 134
- **OS:** macOS 14.6
- **Build / commit:** `app/index.html` @ current `main`
- **Date observed:** May 4, 2026

## Steps to reproduce

1. Open `app/index.html` in Chrome.
2. Open DevTools console and seed test data spanning multiple months:
   ```js
   const seed = [];
   const now = Date.now();
   const day = 86400000;
   for (let i = 0; i < 12; i++) {
     seed.push({
       id: now - i * day * 7,
       timestamp: new Date(now - i * day * 7).toISOString(),
       phase: i % 2 ? 'pre' : 'post',
       energy: 3, focus: 3, mood: 3, note: ''
     });
   }
   localStorage.setItem('creator_checkin_v1', JSON.stringify(seed));
   ```
3. Reload the page and switch to the **history** tab.

## Expected behavior

- Entries from a different year show the year (`"May 4, 2025"`).
- Entries from the same week are visually grouped, or at least the day-of-week is shown (`"Mon, May 4"`).
- A user can scan the list and tell roughly when each entry happened.

## Actual behavior

- Every entry shows `"<Month> <day>"` only, e.g. `"May 4"`, `"Apr 27"`, `"Apr 20"`.
- No year appears anywhere — an entry from May 2025 looks identical to one from May 2026.
- No grouping, no day-of-week, no relative labels ("today", "yesterday", "last week").

## Screenshot / video

`assets/bug-02-history-dates.png` — screenshot of the history list with seeded entries spanning 12 weeks. The dates blur together.

## Severity

- [ ] Blocker
- [x] Major — once a real user has more than ~2 weeks of data, the history view loses its core function.
- [ ] Minor

## Suggested fix

In `renderHistory()`, replace the `toLocaleDateString('en-US', { month: 'short', day: 'numeric' })` call with a small helper:

- If the entry is from today: show `"Today"` + time.
- If from yesterday: show `"Yesterday"` + time.
- If within the last 7 days: show day-of-week + time.
- Else if same calendar year: show `"Mon, May 4"`.
- Else: show `"May 4, 2025"`.
