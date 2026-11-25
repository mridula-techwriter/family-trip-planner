> **Reference only.** Technical README of the group travel app (Art Butterfly), copied on 25 Nov 2026. Its code lives in mridula-techwriter/arty-butterfly-trip-planner.

# Art Butterfly Travel App

A group trip planner for Mridula, Linz, Rakhi and Niranjana. Installable phone app (PWA) with a private Google backend. No accounts needed to use it.

Product decisions, audience and backlog: see [PRODUCT_BRIEF.md](PRODUCT_BRIEF.md). Team meeting notes: [meetings/](meetings/).

Live app: https://mridula-techwriter.github.io/arty-butterfly-trip-planner/

## What it does

- **My travel plans** home screen: create a travel plan (group or solo), trips grouped as In progress, Upcoming, Finished (dates passed, not yet closed) and Completed (greyed, deletable). Cancel trip, Mark as complete, Undo complete.
- Per trip: **Itinerary** (day by day, hour/minute dropdowns, Add to my calendar), **Bookings** (flights, hotel, attachments), **Tickets** (each person's own PNR, seat and e-ticket; entries never overwrite each other), **Reminders** (calendar button + email at the set time), **Packing & to-dos** (each person ticks their own packing), **Expenses** (who paid, which day, split equally among those joining, Settle up with fewest payments, Mark paid), **Trip & people**, **Print** (PDFs: travel info, itinerary, checklist, expense report).
- Invites: **group invite** (home screen) gives full access to all group trips. **Single-trip invite** (inside a trip) opens only that trip.

## How it is built

| Part | Where | Notes |
|---|---|---|
| App (front end) | This repo, served by GitHub Pages from `main` / root | `index.html` (all UI + logic), `sw.js` (offline cache, network-first), `manifest.webmanifest`, icons |
| Backend | Google Apps Script web app in Mridula's Google account ("Kolkata Trip Backend") | `doPost` JSON API, called with `fetch` POST `text/plain` (no CORS preflight). Deployed: Execute as Me, Access Anyone |
| Data | Google Sheet "Trip Planner Data" in Mridula's Drive | One row per document: collection, id, JSON, updated |
| Files | Drive folder "Trip Planner Tickets" | Private; fetched through the API, never shared by link |
| Email reminders | Apps Script time trigger every 15 min (`sendDueReminders`) | Sends from Mridula's Gmail; `installReminders()` sets it up |

Collections: `trip` (one doc per trip; legacy Kolkata id is `meta`), `stops`, `bookings` (flight `pax` map per person), `lists`, `expenses` (with `split`; settlements have `kind:'settle'`), `reminders`. Every non-trip doc has `trip:<tripId>` (missing = `meta`).

Access: every request carries a passcode. The organiser/group passcode sees all trips. Each trip also has its own key (Script Properties `TRIP_KEYS`) that opens only that trip; the server filters reads and refuses writes outside it. **Passcodes live only in Apps Script and on phones — never in this repo.**

Join links: `#join=<base64url {u: exec URL, k: passcode}>`. The hash never reaches the server; the app stores it in localStorage and clears the hash.

## How to update

- **App changes**: edit files here and push to `main`. Pages redeploys in 1–2 minutes. Bump the cache name in `sw.js` (`trip-shell-vN`) on every release. Users just close and reopen the app.
- **Backend changes**: paste the new `Code.gs` into Apps Script, save, then Deploy → Manage deployments → ✏️ → Version: New version → Deploy. The `/exec` link stays the same. New permissions (email, triggers) need a one-time Run of `installReminders`.

## Lessons learned (keep these)

- Decide early: who uses it, do they have accounts, must data be private, phone app or web page, notifications. Changing these later cost three rebuilds (Claude artifact → Apps Script page → PWA).
- Apps Script `HtmlService` silently truncates inline scripts at text like `<\/button>`. Do not serve the UI from HtmlService; use GitHub Pages + JSON API (or base64-wrap the script).
- A Library deployment shows a function list, not the app — always choose **Web app**.
- Copying code from previews adds junk (file names, "100%"). Give plain-text files with line counts to check.
- Android time pickers can lack an OK button: use hour/minute dropdowns.
- jsPDF standard fonts are ASCII only: print `Rs`, not ₹.
- Remember the user's role locally so the app opens on the right screen without flashing.
- Web apps cannot push notifications without a push server; use calendar links and email.
