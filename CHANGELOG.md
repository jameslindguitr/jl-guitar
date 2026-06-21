# Changelog — James Lind Guitar app

A running record of changes. Newest at the top. One line each: what changed, and why if it isn't obvious.

Format: `YYYY-MM-DD  what changed — why (if not obvious)`

---

## 2026-06

- 2026-06-18  Summary now has a Quarterly breakdown (MTD-ready) panel — splits the tax year into the four standard MTD quarters (6 Apr–5 Jul, 6 Jul–5 Oct, 6 Oct–5 Jan, 6 Jan–5 Apr) showing income/expenses/net. Presents data in the shape MTD wants WITHOUT claiming filing capability. "Readiness costs nothing; compliance costs money." First concrete piece of the "MTD ready" positioning.
- 2026-06-18  Log Payment: "Stream" label renamed to "Source".
- 2026-06-18  Log Payment: roster field reads "Client / venue from roster" for the Performance source (was "Student / client"). Considered separate performance sub-rosters (agent/venue/promoter) but deferred — booking is mostly direct (a venue/society books and pays). Parked as a product idea.
- 2026-06-18  Removed the Substack roster tab (was empty/contacts-only and unused; Substack income is logged via Log Payment → Other Income instead). Roster is now St Margaret's / Private / Performances.
- 2026-06-18  Expenses: added a "Receipt kept" checkbox + optional "where it's kept" note (autocompletes), and a Receipt column in the table flagging kept (✓ + location) or missing. Deliberately does NOT store the receipt files themselves — the app is the ledger, not the filing cabinet; phone/email/paper remain the store. Avoids needing Firebase Storage / the paid Blaze plan.
- 2026-06-18  Supplier field on expenses now autocompletes from previously-entered suppliers — saves retyping, keeps spelling consistent. Self-maintaining (derived from existing expenses, no separate list).
- 2026-06-18  Invoice log restructured: Outstanding section pinned at top (unpaid, sorted by due date, with total owed), full history below in collapsible monthly sections with per-month totals, and a Group-by selector (invoice date / due date / paid date) — stops the log becoming an unusable flat list as it grows.
- 2026-06-18  Invoice due date is now editable (defaults to 14 days after invoice date, auto-updates if invoice date changes, but can be overridden) — was previously fixed at 14 days with no override.
- 2026-06-17  Added "Substack" and "Other" to the Log Payment stream options — these route to Other Income (not invoice records) so they show in the right stream totals.
- 2026-06-11  Invoice PDF dates now use UK format (dd/mm/yyyy) via fmtDate, not raw ISO.
- 2026-06-11  Switched invoice PDF generation to jsPDF drawing text directly — html2pdf/html2canvas produced blank pages (couldn't capture the off-screen element). jsPDF loaded from jsDelivr, NOT cdnjs (cdnjs was returning errors and silently breaking the load).
- 2026-06-11  Download invoice now produces a real .pdf file (was downloading as .html before).
- 2026-06-11  Added "Log Payment" tab under Income & Expenses — records money already received without issuing an invoice (incl. back-filling earlier in the tax year). Stored as paid records so they flow into totals.
- 2026-06-11  Added tax-year Summary (6 Apr–5 Apr) with year selector, income-by-stream breakdown, and expenses-by-category — for self-assessment prep.
- 2026-06-11  Added data export/import backup (JSON) in Settings.
- 2026-06-11  Migrated from browser local storage to Firebase Firestore + email/password login — data now survives browser wipes and syncs across devices. Hosted on GitHub Pages.
- 2026-06-11  Roster gained four tabs at the same level: St Margaret's, Private, Performances (invoiceable, editable fees), Substack (contacts only).
- 2026-06-11  Seeded roster with real data: 22 St Margaret's students + 10 private students.

---

## Notes / decisions worth remembering

- Attendance tracking was considered and deliberately scrapped — no billing consequence (school is billed per term regardless), so it would just be a chore that rots.
- CDN lesson: prefer cdnjs/jsDelivr over unpkg (unpkg had outages that caused blank pages). If the app ever loads blank after a change, a library failing to load from a CDN is the first suspect.
- After updating index.html on GitHub: hard-refresh, or append `?v=2` (bump the number) to the URL to bust the cache.
- Firebase config in the client code is public by design and safe — the Firestore security rule (`allow read, write: if request.auth != null`) is what actually protects the data.

---

## Ideas parked for later (product, not personal use)

- Generalise "Substack" income to a user-definable income source — let users add and name their own streams (Patreon, YouTube, function band, etc.) rather than a fixed list. Build only when there are real users to inform it.
- MTD: keep the app as the digital record; hand off to HMRC-recognised software for filing. Becoming HMRC-recognised software is a year-three decision, only if demand proves it.
- Bank feed (Open Banking via an aggregator) and native App Store presence are later/optional costs, not initial.

### Flagship features (the ones that sell the thinking, not just the tool)

These are the features that make the product more than a commodity ledger — each one makes the user *realise* something, not just *record* something. They enact "owner-thinking" and are what Xero/FreeAgent structurally can't copy, because they don't have the thesis behind them. Build them AFTER the summer Mom Test conversations, which will tell us which realisation each musician most needs and how to get the details right (e.g. what counts toward "true hourly rate").

- **True hourly rate** — show what you actually earn per hour once unpaid admin, prep, and travel are counted, not just the headline lesson rate. Makes the user confront real cost-of-delivery.
- **Annual inflation review prompt** — nudge to review and raise rates yearly, surfacing the silent real-terms pay cut taken by leaving rates unchanged.
- **Income-by-stream visibility** — surface the split across teaching/performance/writing so the user sees themselves as a multi-stream business, not a teacher with odd extra bits.
- (future) **What you could afford to invest** — once income is visible, surface genuine surplus, echoing the ISA/owner-thinking philosophy.

Design filter for ALL future features: does this just *record* something (commodity, table-stakes) or does it make the user *realise* something (the actual product)? Prefer realisation features.

### Positioning principle

Sell the thinking, not the tool. People won't pay much for a ledger (commodity — competes with Xero/FreeAgent/spreadsheets). They pay to think differently about their working life: musician-as-employee → musician-as-owner. The tool is the daily proof of that shift, not the product itself. Content (Substack, talks, videos) does the persuading and comes first; the tool converts believers. Compete on meaning and perception, not features and price (Sutherland / Dunford / Godin).
