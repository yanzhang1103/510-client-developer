# Bug #1 — Incomplete check-in: error message is too quiet, missing fields are not highlighted

> Filed during Client-02 mid-point review. Use this content when creating the GitHub issue.

## Summary

When the user taps "save check-in" without selecting all three rating scales, a small toast briefly appears at the bottom of the screen, but no visual cue is shown on the actual missing fields. On mobile, where the toast is below the fold or behind the keyboard, users won't know why nothing happened.

## Acceptance criterion affected

**AC-2** — *Submitting a check-in without all required ratings shows an error and does NOT save.*

The "does NOT save" half passes. The "shows an error" half is technically met but the error is too low-contrast to be reliably noticed.

## Environment

- **Browser:** Chrome 134, Safari 18 (both reproduce)
- **OS:** macOS 14.6
- **Build / commit:** `app/index.html` @ current `main`
- **Date observed:** May 4, 2026

## Steps to reproduce

1. Open `app/index.html` in a browser.
2. On the "check in" tab, leave the default phase (pre-session) selected.
3. Tap **only** the "3" button under Energy. Do not touch Focus or Mood.
4. Tap **save check-in**.

## Expected behavior

- The form does not save (this part works).
- The Focus and Mood fields are visually marked as missing — for example, a red border on the scale group, or an inline error message under each empty field.
- The toast message remains as a secondary cue.

## Actual behavior

- Form does not save (correct).
- A toast at the bottom of the page reads "please rate energy, focus, and mood" for 1.8 seconds, then disappears.
- The empty Focus and Mood scales look identical to before — no border change, no inline message.
- A user who didn't see the toast has no idea why their tap did nothing.

## Screenshot / video

`assets/bug-01-validation.png` — screenshot showing the form after a failed save, with no visible indication that Focus and Mood are the problem.

## Severity

- [ ] Blocker
- [x] Major — violates the "shows an error" half of AC-2 in spirit, even if literally a message appears.
- [ ] Minor

## Suggested fix

In the `saveBtn` click handler, before showing the toast, add a class like `.missing` to each empty `.scale` element and to the field's label. Define `.missing` in CSS as a 1.5px red border and a red label color. Clear the class on next selection.
