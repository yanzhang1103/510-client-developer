# Client Spec — Creator Check-in

**Project:** Creator Check-in
**Client:** Yan (sole role: client + developer)
**Course:** TECHIN — Final Project
**Spec version:** 1.1
**Last updated:** May 4, 2026

---

## 1. Problem statement

Music creators and producers often work in long, intuition-driven sessions without any structured awareness of their own state going in or coming out. Energy, focus, and mood shape what gets made — but the relationship is invisible because nothing is logged. Existing tools (mood trackers, journaling apps, DAW session notes) are either too heavy (full journaling) or too disconnected from the creative session (generic wellness apps).

This project explores whether a 30-second check-in tied to a creative session, repeated over weeks, can surface useful patterns about when a creator does their best work.

## 2. Target user

- Solo music creators / producers / songwriters
- Working in short-to-medium sessions (30 min – 3 hr) on their own
- Already comfortable with simple web tools
- Not looking for therapy, not looking for a full journal

## 3. Scope (MVP — what the developer must deliver)

### In scope
- Single-page web app, runs in modern browsers, no install
- Pre-session and post-session check-in flow
- 5-point scales for energy, focus, mood
- Optional free-text note (1 line)
- Data persists locally (no account, no cloud)
- History view: chronological list of past check-ins
- Insights view: total count, average energy, average focus, simple line chart of last 14 check-ins
- Reset / clear-all-data option

### Out of scope (MVP)
- Cloud sync, accounts, auth
- Native mobile app
- DAW integration
- Multi-user / sharing
- Notifications / reminders
- Statistical correlation between check-ins and creative output (post-MVP research direction)

## 4. Acceptance criteria

A delivered build is accepted if and only if all of the following are true:

| # | Criterion | How tested |
|---|-----------|------------|
| AC-1 | User can submit a check-in with phase + 3 ratings + optional note | Manual: fill out and save |
| AC-2 | Submitting a check-in without all required ratings shows an error and does NOT save | Manual: try to save partial form |
| AC-3 | After saving, form clears so the next check-in starts fresh | Manual: save, observe form |
| AC-4 | History view shows all saved check-ins, most recent first, with date, phase, ratings, and note if present | Manual: save 3+ entries, switch to history |
| AC-5 | Insights view shows correct totals and averages | Manual: save known values, check math |
| AC-6 | Insights chart renders without error for 0, 1, and 14+ entries | Manual: edge cases |
| AC-7 | Reset button asks for confirmation and clears all data when confirmed | Manual: reset, check history empty |
| AC-8 | Data survives page reload | Manual: save, reload, check history |
| AC-9 | App is usable on a 375px-wide mobile viewport | Manual: responsive check |

## 5. Initial timeline (negotiated at project kickoff)

| Phase | Dates | Deliverable |
|-------|-------|-------------|
| Kickoff | week of Apr 6 | Spec accepted, repo initialized, dev fee agreed |
| Sprint 1 | Apr 13 – Apr 26 | Check-in form + localStorage write |
| Sprint 2 | Apr 27 – May 4 | History view + Insights view + chart |
| **Mid-point check** | **May 4** | **Client-02 review — this document set** |
| Sprint 3 | May 5 – May 18 | Bug fixes, polish, mobile pass, accessibility pass |
| Demo prep | May 19 – May 25 | Final testing, demo script, deck |
| Demo day | TBD per course schedule | Working build + presentation |

## 6. Negotiated dev fee

**40 GIX Bucks**, paid from client to developer at kickoff.

Rationale: scope is single-page, no backend, no auth, no third-party APIs. Estimated 2–3 sprints of focused work. 40 GIX Bucks leaves the client with 60 to invest on demo day, which is enough exposure to other projects to participate meaningfully in the investment round without high bankruptcy risk.

## 7. Definition of done (final, not mid-point)

- All 9 acceptance criteria pass
- README explains how to run the app (open `app/index.html` in a browser)
- All filed bugs are either resolved or explicitly deferred with rationale
- Code committed to `main` branch with clean history
- Demo-ready build accessible via GitHub Pages or equivalent

## 8. Sign-off

Client signature (Yan): _accepted, May 4, 2026_
Developer signature (Yan): _accepted, May 4, 2026_

> Note on dual role: due to enrollment timing, this project is staffed solo. Client and developer responsibilities are separated by deliverable rather than by person. All client-side reviews (this spec, Client-02 mid-point check, and final acceptance) are documented as standalone artifacts to maintain the review boundary the course requires.
