# Creator Check-in

A 30-second creative-state check-in for solo music creators. Pre-session and post-session, log energy, focus, mood, and a one-line note. See your patterns over time.

Course final project. Client and developer both performed by Yan (see [client spec](docs/client-spec.md), section 8).

## Run it

### Live URL

🔗 **https://510-client-developer.vercel.app** *(URL will be confirmed after Vercel deployment)*

Auto-deployed from `main` via Vercel. Every merge into `main` triggers a fresh production build.

### Run locally

No build step. Open `index.html` in any modern browser. All data is stored in your browser's `localStorage` — nothing leaves your machine.

​```bash
# from repo root
open index.html        # macOS
xdg-open index.html    # linux
start index.html       # windows
​```

## What's in here

```
.
├── index.html                  # the MVP — single-file web app (deployed root)
├── vercel.json                 # Vercel deployment config
├── .env.example                # env-variable template (no vars currently used)
├── docs/
│   ├── client-spec.md          # the spec the developer is building against
│   └── mid-point-check.md      # Client-02 review (this assignment)
├── .github/
│   └── ISSUE_TEMPLATE/
│       └── bug-report.md       # bug report template
├── assets/                     # screenshots referenced by docs and issues
└── README.md
```

## Status (Sprint 4, May 25, 2026)

All Developer-04 deliverables complete. PR #5 merged.

| Deliverable | Where to find it |
|-------------|------------------|
| Bug #2 fix (history date format) | `index.html` `formatEntryDate()` + PR [#5](../../pull/5), closes [#2](../../issues/2) |
| Bug #3 fix (insights chart Y-axis) | `index.html` `renderInsights()` + PR [#5](../../pull/5), closes [#3](../../issues/3) |
| Automated tests (12 assertions, 3 groups) | `tests/test.html` — open in a browser |
| Security review | [`SECURITY.md`](SECURITY.md) |
| PR review feedback | PR [#5](../../pull/5) conversation — 3 inline comments + 3 replies |

All 3 client-reported bugs now closed. Live URL deployed from latest `main`: https://510-client-developer.vercel.app

## Status (mid-point, May 4, 2026)

MVP is functional. All check-in / history / insights flows work end-to-end. Three bugs filed during the mid-point review (see GitHub Issues). On track for Sprint 3.

## Updated timeline

Original timeline is in [client-spec.md §5](docs/client-spec.md#5-initial-timeline-negotiated-at-project-kickoff). Below reflects status as of mid-point review.

| Phase | Original dates | Status | Notes |
|-------|----------------|--------|-------|
| Kickoff | week of Apr 6 | ✅ done | Spec frozen at v1.0; repo initialized |
| Sprint 1 — form + storage | Apr 13 – Apr 26 | ✅ done | AC-1, AC-2, AC-3, AC-8 pass |
| Sprint 2 — history + insights | Apr 27 – May 4 | ✅ done | AC-4, AC-5, AC-6, AC-7 pass |
| **Mid-point check** | **May 4** | **✅ in progress** | **This document set** |
| Sprint 3 — bug fixes + polish | May 5 – May 18 | 🔄 in progress | Bug #1 resolved in this PR; Bug #2, #3 next |
| Developer-03 — deployment | May 12 – May 18 | ✅ done | Vercel auto-deploy from main; .env.example provided |
| Mobile / a11y pass | May 12 – May 18 | ⏳ upcoming | AC-9 needs verification on real devices |
| Demo prep | May 19 – May 25 | ⏳ upcoming | Demo script, deck, GitHub Pages deploy |
| Demo day | per course schedule | ⏳ upcoming | — |

### Risk register (mid-point)

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Solo client+dev role means no external reviewer challenges spec | High | Mid-point check is written as a true client review with rejection authority, not a self-affirming summary. |
| `localStorage` quota or private-browsing modes break persistence | Low | Documented constraint; out of scope for MVP. Add a warning banner in Sprint 3. |
| Mobile viewport not yet tested on real device | Medium | Schedule device test in Sprint 3 before demo. |

## Acceptance criteria — current pass/fail

See [client-spec.md §4](docs/client-spec.md#4-acceptance-criteria) for the full list.

| # | Status |
|---|--------|
| AC-1 submit valid check-in | ✅ pass |
| AC-2 reject incomplete | ✅ pass (fix verified in [#1](../../issues/1)) |
| AC-3 form clears after save | ✅ pass |
| AC-4 history view | ✅ pass (fix verified in [#2](../../issues/2)) |
| AC-5 insights totals | ✅ pass |
| AC-6 chart edge cases | ✅ pass (fix verified in [#3](../../issues/3)) |
| AC-7 reset confirmation | ✅ pass |
| AC-8 reload persistence | ✅ pass |
| AC-9 mobile 375px | ✅ pass (verified Jun 1, 2026 — see `docs/final-acceptance.md`) |

## License

Course project. Not for redistribution.
