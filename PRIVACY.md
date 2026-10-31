# Waypoints Privacy Policy

**Effective date:** 2026-07-16
**Last updated:** 2026-07-22

Waypoints ("we", "us", "the app") is a native EV road-trip planner for iOS and iPadOS. This policy explains what data the app handles and where it lives. We've tried to keep it short and free of legalese — if anything is unclear, open an issue at https://github.com/amoghsa/Waypoints/issues.

## Summary, in one paragraph

Everything you put into Waypoints — your trips, the stops you plan, your household profile, your vehicle choice, and the dwell habits the app learns — is stored and computed **locally on your device**. We do not run a backend for your data, we do not have accounts, and we do not sync anything to the cloud. To plan around real charging, the app does send the **route you're viewing** — the coordinates of your trip's start, destinations, and stops — to our own backend so it can look up public charging stations along that route and, where a network reports it, how busy they are; those requests carry no name, no household details, and no account (there are no accounts), and are never used to build a profile of you. There are no advertising or analytics SDKs, no ads, and no background tracking of any kind. What is new in this version: Waypoints now offers **optional links you tap yourself** to third-party travel services — a "Find a place to stay" lodging link on overnight/destination stops, and an "Open in … app" link to a charging network's own app. When *you choose* to tap one, the app opens that partner's site or app and passes along only the stop's location and your planned dates so it can show relevant results; it never sends your name, your household details, or any identity for you. We may earn a commission on bookings made this way, and that **never** influences how the app ranks chargers or stops. To remove your on-device data, reset it in the app or uninstall Waypoints.

## What stays only on your device

Waypoints stores the following locally using Apple's SwiftData, in the app's own sandbox. None of it is sent to a server we operate:

- **Trip plans** — the trip name, your "From" and "To" as free text, departure and arrive-by dates, total distance, your starting and reserve-floor state of charge, trip priority, weather mode, status, and progress.
- **Intent stops & destinations** — for each stop you add: its kind, a free-text name, mile marker, planned arrival time, how long you plan to dwell, whether it has a charger, and its order in the trip. If you pick a place from address autocomplete, its coordinates are captured and stored locally too (these are what a lodging link uses — see below).
- **Household profile** — the number of adults and kids in your party, your kids' ages (free text) if you enter them, dietary notes (free text), an accessibility-needs flag, a no-fast-food preference, and your break cadence. This is the most sensitive data the app holds, and it never leaves your device — and it is never included in the partner links described below.
- **Learned dwell habits** — each time you advance to the next waypoint, the app quietly records how long you planned to stay versus how long you actually stayed, by stop kind, with a timestamp. This is what lets future plans lean on your real behavior instead of just your schedule.
- **Vehicle** — a built-in catalog of preset EVs the app ships with, plus which vehicle you've marked as active. Vehicle details are picked from the catalog, not typed in.
- **Map and catalog data** — charger sites and points of interest. These ship with the app.
- **A few app preferences** — stored in the standard iOS preferences store: whether you've finished onboarding, your active trip, your selected vehicle, whether the demo trip is seeded, and your household adult/kid counts.

To clear just the learned dwell habits, use **Settings → Forget my habits**. To wipe everything Waypoints has stored, use **Settings → Reset all data**, or uninstall the app. See [Data Deletion](./DATA-DELETION.md) for details.

## What is sent off the device

**Your saved data is never uploaded.** Your trips, stops, household profile, learned habits, and preferences stay on your device — Waypoints has no backend for *them*, no accounts, no iCloud/CloudKit sync, and embeds no third-party analytics, advertising, or crash-reporting SDKs. Two things do leave your device, both described below: charger data the app fetches for the route you're viewing, and travel-partner links you tap yourself.

### Charger data for the route you're viewing (automatic)

When you open a trip's plan, Waypoints looks up **real public charging stations along your route** — and, where a network reports it, how many stalls are currently free — so it can time charging around stops you actually want. To do that it sends the **route geometry**: the latitude/longitude of your trip's start, destinations, and any stops you picked from address search. It sends **nothing else** — not your name, not your household profile or your kids' details, not any account or per-user identifier (there are no accounts).

These requests go to **Waypoints' own backend proxy**, a small serverless service we operate. The proxy exists precisely so the app never has to embed third-party API keys and so your requests are never attributed to *you* with those providers: it relays your route to public data sources — the U.S. Department of Energy's Alternative Fuel Data Center (charger locations), Mapbox (route geometry), and TomTom (live availability) — and returns only charger locations, attributes, and availability, which the app then caches on your device for that trip. A request is used only to answer the lookup for the route you're viewing; it is not tied to any identity and is not used to build a profile of you. Responses may be briefly cached at the edge to speed up repeat lookups.

If the backend is unavailable, the app falls back to its built-in charger catalog and keeps working.

Separately, when you type in the "From"/"To" or stop fields, address suggestions come from **Apple's MapKit**, which sends what you type to Apple under [Apple's privacy policy](https://www.apple.com/legal/privacy/); the place you pick is then stored on your device.

### Travel-partner links (only when you tap)

The other data that leaves your device does so only through **links you deliberately tap** to a travel partner:

- **Lodging — "Find a place to stay" (Stay22).** On an overnight or destination stop you can tap through to look for a place to stay. This opens an in-app web view to Stay22, a travel-booking aggregator, at a URL that contains the stop's **location (latitude/longitude)** and your planned **check-in/check-out dates** so it can show relevant accommodations, plus a fixed **partner code** that identifies Waypoints — not you — so Stay22 can credit us if you book. It does **not** contain your name, your household profile, or any per-user identifier we assign.
- **Charging — "Open in … app".** For a charger, you can tap to open that charging network's own app or website. We pass no personal data; this simply hands you off to the network.

Once you follow one of these links you are on the third party's website or app, and **their** privacy policy governs whatever they collect there (for example, cookies Stay22 or a charging network sets in your browser):

- Stay22: https://www.stay22.com/privacy-policy
- The relevant charging network's policy, linked from its own app or site.

**If you never tap these links, nothing is sent to a travel partner** — the only data the app sends on its own is the route lookup for charging described above.

For transparency: the app also includes a developer-only diagnostic log present **only in debug builds** used during development. It writes to your device's own system log and never leaves the device. The release build you install from the App Store records nothing at all. Aside from the route lookup described above — which isn't tied to you or retained to profile you — the app embeds no analytics, advertising, or tracking SDKs; its Apple privacy manifest declares no collected data types and no in-app tracking. The partner links above are ordinary web navigations that you initiate, not in-app data collection.

## Affiliate disclosure

Some of the partner links above are affiliate links: if you book through them, Waypoints may earn a commission, at no extra cost to you. This is disclosed in the app right next to the link. It has **no effect on the app's ranking** — chargers and stops are always ordered by *fit* (proximity, charging power, price, amenities, and how well a stop matches what you wanted), never by who pays us. We do not sell your data, and we do not accept payment to change what the planner recommends.

## Permissions

Waypoints requests **no system permissions**. It does not ask for location, microphone, camera, contacts, photos, calendar, health data, or notifications.

## Children's privacy

Waypoints is a trip-planning utility intended for adults planning a drive. If you tell it how many kids are in your party — and optionally their ages, so it can plan family-friendly break cadence and stops — that information is stored only on your device, is never transmitted anywhere, and is never included in the partner links above. It is not a profile of a child or tied to any identity. The app has no accounts and no way for a child to sign up, because there are no accounts at all. We do not knowingly collect personal information from anyone under the age of 13 (or under 16 where that threshold applies).

## Changes to this policy

This version (updated 2026-07-22) adds the **automatic charger lookup** described above: the app now sends the route you're viewing to our backend proxy to fetch real charging stations and live availability along it. The prior version (2026-07-16) had added the optional, user-initiated lodging and charging-network partner links; the original release had no network features at all. If we change what the app does again — for example, if a future version adds accounts, cloud sync, analytics, or starts sending anything beyond route geometry to the backend — we will update this document and bump the **Last updated** date before that change ships.

## Contact

- Privacy contact: waypoints@amoghsa.com
- Issues and questions: https://github.com/amoghsa/Waypoints/issues
