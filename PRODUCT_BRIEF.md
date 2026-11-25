# Product brief: Family Trip Planner

> Read by Mridula's app team (Product Manager, UX Designer, UX Writer, Product Developer) before any work on this app. Update it whenever a decision changes. Technical how-to lives in README.md. Built from the group app (Art Butterfly); its brief and README are in `reference/` for lessons, not as rules for this app.

## 1. Snapshot

| | |
|---|---|
| Owner | Mridula (plans every trip; does not code) |
| Status | Kickoff done 25 Nov 2026; release 1 waiting on decisions (see §9) |
| App | Planned: https://mridula-techwriter.github.io/family-trip-planner/ |
| Repo | mridula-techwriter/family-trip-planner (Claude can push) |
| Reuses | Code from mridula-techwriter/arty-butterfly-trip-planner (`index.html`, `sw.js`, manifest, icons) |
| Backend | New Google Apps Script web app + new Google Sheet + new private Drive folder in Mridula's Google account. Nothing shared with the group app. |
| Purpose | Free, private planner for Mridula's own family trips. Not a paid product. |

## 2. Audience

- **Owner:** Mridula. Plans and pays; forgets dates and where things are; wants everything visible at a glance; plain language, clear hierarchy.
- **Child:** Mridula's child, on their own phone via their own link. Sees a simpler app.
- **Not users:** the friends group (they use Art Butterfly). A pet-sitter gets a printed or PDF sheet, not app access.
- **Household:** Mridula, her child, three cats who stay home.
- **Devices:** Android (Mridula: OnePlus, Chrome); Mac laptop for planning.
- **Accounts:** none. Access works from a link.
- **Context:** India, ₹ by default; some trips abroad in other currencies.

## 3. Problems it solves

1. Keeping a family trip's itinerary, bookings and tickets in one place (as the group app does).
2. Knowing how much of the trip budget is left, including spends in other currencies.
3. Leaving home and the cats safely sorted, without rewriting the same notes every trip.
4. Not being caught out by an expiring passport or visa.
5. Giving the child their own packing and day plan without exposing documents or money.
6. Keeping several trips a year straight.

## 4. Decisions (log)

| Date | Decision | Why |
|---|---|---|
| 25 Nov 2026 | Fork the group app's code instead of building new | Mridula: reuse what exists, no redundant effort |
| 25 Nov 2026 | Completely separate from the group app: own repo, Pages site, Apps Script, Sheet, Drive folder, passcodes | Mridula: family and group data must stay apart |
| 25 Nov 2026 | Prefix all browser storage keys (`fam.`) and name the offline cache `family-shell-vN`; delete only own caches | Both apps share the web address `mridula-techwriter.github.io`, so unchanged they would read each other's passcode and wipe each other's offline copy |
| 25 Nov 2026 | Two roles: Owner (everything) and Child (own link, limited view) | Mridula and her child are the only users |
| 25 Nov 2026 | Remove split, settle up, "joining" and the group invite | Family trip money is one budget, not a split |
| 25 Nov 2026 | Budget vs spent: trip budget in ₹, spends by category, "Left" shown first | Mridula's choice |
| 25 Nov 2026 | Spends in any currency; rate auto-filled from Frankfurter (free, no key), editable; store original amount, rate and ₹ amount | Trips abroad; card and forex rates differ from reference rates |
| 25 Nov 2026 | Home & cats set up once and copied into each trip; printable sheet for the sitter | Details rarely change between trips |
| 25 Nov 2026 | Trip screen grouped into three tabs: Plan, Money, Before you go | Group app's eight tabs plus new features would crowd a phone screen |
| 25 Nov 2026 | Itinerary gets an optional Break item (rest, meal, nap) | Child-paced days |
| 25 Nov 2026 | Documents ship last; never visible to the Child role, never in PDFs or emails by default | Most sensitive data |
| 25 Nov 2026 | New name and colours, chosen by Mridula from team options | Never open the wrong app |
| 25 Nov 2026 | Ship in four releases: separate → budget → before you go → documents | Smallest useful version first |

Privacy note: the DPDP Act does not apply to personal data an individual processes for a personal or domestic purpose (s.3(c)(i)). This app is personal use. If it is ever offered to other families, that changes and needs professional advice.

## 5. Shipped

Nothing yet. Repo has README, reference copies of the group app's brief and README, and kickoff minutes.

## 6. Backlog and ideas

**Release 1: Separate and rename**
- Copy group app code; apply new name, icon, colours, manifest (`id`, `start_url`, `scope` under `/family-trip-planner/`).
- Storage and cache separation (see Decisions).
- New `Code.gs` with Owner and Child keys; new Sheet, Drive folder, passcodes.
- Owner/Child roles; remove split, settle up, joining, group invite.
- Child view: Today and My packing.

**Release 2: Budget**
- Trip budget; categories (Travel, Stay, Food, Activities, Shopping, Other); spends by day.
- Currency per spend with auto-filled, editable rate; totals in ₹.
- Budget report PDF (replaces expense report; prints "Rs").

**Release 3: Before you go**
- Home & cats: sitter name and phone, each cat's food, litter and medicine notes, house checklist (gas, taps, plants, deliveries); saved once, copied into each trip; sitter PDF.
- Child's packing template reused across trips.
- Break items in the itinerary.

**Release 4: Documents**
- Per person: document type, expiry date, where the original is kept.
- Warning when a passport expires less than 6 months after the return date (Nepal, Bhutan excepted); reminder 9 months before expiry.
- Visa dates per trip.

**Ideas, not planned:** school-holiday calendar; share a read-only trip with grandparents.

## 7. Constraints and known limits

- Backend updates need Mridula to paste `Code.gs` and deploy a New version; app updates reach both phones automatically.
- Claude cannot reach Mridula's Google account; the group app's `Code.gs` is not in GitHub.
- Sync refreshes every ~6 seconds, not instant.
- Reminder emails come from Mridula's Gmail; the ~100/day free limit is shared with the group app's reminders.
- No push notifications (no push server); reminders are calendar links and email.
- Exchange rates are reference rates, not what the bank charges; editable for that reason.
- Anyone with the Owner link sees everything; keep it off shared devices.

## 8. Voice and design notes

**Design principles for this app**
1. Answer first: "₹8,400 left of ₹60,000", then the list.
2. Three places per trip (Plan, Money, Before you go); nothing more than two taps deep.
3. Set up once, reuse: home & cats, child's packing.
4. The child's app is smaller, not a locked-down copy of Mridula's: Today and My packing only.
5. Sensitive things (documents, budget) are Owner-only and say so on screen.

Plus the group app's rules: hour/minute dropdowns (no Android time picker), 44px touch targets, 16px text, two-step delete naming the item, remember role locally, design empty/loading/offline states.

**Voice**
- Indian English; ₹ on screen, "Rs" in PDFs; dates like "Thu 4 Feb – Sun 7 Feb 2027" plus "In 10 days".
- Same terms as the group app: My travel plans, Create a travel plan, Mark as complete.

| Use | Avoid |
|---|---|
| Budget, Spent, Left | Expenses split, settle up, per share |
| Before you go | Pre-trip, checklist module |
| Home & cats | Pet management |
| Things to pack (child view) | Packing items |
| "Passport expires Mon 3 May 2027, less than 6 months after you return. Some countries won't let you in." | "Passport validity insufficient" |

**Name and colours:** pending Mridula's choice (§9). Must look nothing like Art Butterfly (blue #1d6fd8, coral #ff6b4a).

## 9. Open questions (for Mridula)

1. **Child's access:** A. Today + own packing *(recommended)*; B. A + full itinerary and bookings; C. A + add spends.
2. **Documents:** A. Expiry dates + where the original is *(recommended to start)*; B. A + copies in private Drive, Owner only, online only; C. B + offline copies.
3. **Name and look:** A. **Kite**, teal #0f766e + mango #f59e0b *(recommended)*; B. **Homeward**, forest green #2f6b4f + terracotta #c8553d; C. **Nest & Go**, plum #6b3fa0 + saffron #f4a300.
4. **Group app's Code.gs:** A. Share a copy for the Developer to adapt *(recommended)*; B. Developer writes a fresh one.
5. **Next family trip date:** sets the release 1–2 deadline.

## 10. Meetings

Team meeting notes are in `meetings/` (one file per meeting, `YYYY-MM-DD-topic.md`).
- 25 Nov 2026: [Kickoff](meetings/2026-11-25-kickoff.md)
