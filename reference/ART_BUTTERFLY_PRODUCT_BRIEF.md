> **Reference only.** This is the product brief of the group travel app (Art Butterfly), copied on 25 Nov 2026 as the starting point for the family travel app. Reuse its decisions and lessons where they fit; the family app's own brief will be `PRODUCT_BRIEF.md` in this repo, written at the kickoff meeting. Group-only details (the four friends, the Kolkata trip, group invite rules) do not apply here.

# Product brief: Art Butterfly Travel App

> Read by Mridula's app team (Product Manager, UX Designer, UX Writer, Product Developer) before any work on this app. Update it whenever a decision changes. Technical how-to lives in README.md.

## 1. Snapshot

| | |
|---|---|
| Owner | Mridula (organiser; does not code) |
| Status | Live, in use for the Kolkata trip (4–7 Feb 2027) |
| App | https://mridula-techwriter.github.io/arty-butterfly-trip-planner/ |
| Repo | mridula-techwriter/arty-butterfly-trip-planner (Claude can push) |
| Backend | Google Apps Script web app + Google Sheet in Mridula's Google account (Claude cannot reach it; Mridula pastes and deploys) |
| Purpose | Free, private tool for one friends group. Not a paid product. |

## 2. Audience

- **Who:** a fixed group of four friends in Bangalore: Mridula, Linz, Rakhi, Niranjana. Mid-career women who travel together several times a year.
- **Devices:** Android phones (Mridula: OnePlus, Chrome). Mridula also uses a Mac laptop.
- **Accounts:** they will not create accounts for this. Access must work from a link.
- **Context:** India; ₹; IndiGo-style separate bookings (each person has their own PNR); WhatsApp group is where links are shared.
- **Mridula's own needs:** forgets dates and where things are; wants everything visible at a glance; values clear visual hierarchy and plain language.

## 3. Problems it solves

1. Planning a group trip across chats loses details (itinerary, bookings, PNRs, hotel).
2. Splitting money fairly and knowing who pays whom after the trip.
3. Remembering what to pack and what to do before leaving.
4. Keeping several upcoming trips straight across a year.

## 4. Decisions (log)

| Date | Decision | Why |
|---|---|---|
| 24 Nov 2026 | Installable phone app (PWA) on GitHub Pages, not a website or Claude artifact | Must feel like an app; friends have no Claude accounts |
| 24 Nov 2026 | Data private, behind passcodes; nothing secret in the repo | Mridula: "our data must remain private" |
| 24 Nov 2026 | Expenses split equally among people marked "joining" (a person can be listed but not joining) | Niranjana not on the Kolkata trip; split by 3 |
| 24 Nov 2026 | Each person ticks their own packing items; each person has their own PNR/seat/ticket | Separate bookings; no overwriting each other |
| 24 Nov 2026 | Reminders = Add to calendar + email (no push) | Web apps can't push without a push server |
| 25 Nov 2026 | Many trips: home screen "My travel plans", Create a travel plan first, cards show dates | Mridula plans several trips a year and forgets dates |
| 25 Nov 2026 | This app is for the friends group only; family travel will be a separate app | Keep group and family data apart |
| 25 Nov 2026 | All four have equal rights via one group invite link; single-trip invites for outsiders | Simple for four friends; trade-off: can't remove one person without changing the passcode |
| 25 Nov 2026 | Keep a "Finished" state (dates passed, not yet closed) before "Completed" | Reminder to close the trip (settle up) |

## 5. Shipped

My travel plans home; create, cancel, mark complete, undo, delete trips; itinerary with calendar links; bookings with attachments; per-person tickets; reminders (calendar + email); per-person packing and shared to-dos; expenses with day grouping, settle up, mark paid; trip & people; PDFs (travel info, itinerary, checklist, expense report); group and single-trip invites; offline last copy.

## 6. Backlog and ideas

- Show "Settle-up pending" on Finished trip cards (offered, not yet confirmed).
- Optional: one link per person so one person can be removed without changing everyone's access (needs backend update).
- Family travel app: separate app, separate data (future project).

## 7. Constraints and known limits

- Backend updates need Mridula to paste Code.gs and deploy a New version; app updates reach everyone automatically.
- Sync refreshes every ~6 seconds, not instant.
- Free Gmail sends about 100 reminder emails a day.
- Anyone with the group link can see and change all group trips.

## 8. Voice and design notes for this app

- Name: Art Butterfly (short name). Butterfly icon in blue and coral.
- Colours: sky blue #1d6fd8, coral #ff6b4a, paper white; fonts Archivo / Archivo Narrow.
- Indian English; ₹ on screen, "Rs" in PDFs; dates like "Thu 4 Feb – Sun 7 Feb 2027".

## 9. Open questions

- Add "Settle-up pending" to Finished cards?
- Per-person links: needed or not?

## 10. Meetings

Team meeting notes are saved in `meetings/` (newest first by date in the file name).
