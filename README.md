# Tafuta

**Tafuta** (Swahili for "find") is an AI-assisted lost & found matching and recovery system for airline operations. It was built as a working prototype for the **Kenya Airways Innovation Challenge 2026**, in response to the *Intelligent Digital Lost & Found* challenge brief.

**Live demo:** [tafuta-blond.vercel.app](https://tafuta-blond.vercel.app)

## The problem

Today, airline lost & found runs on phone calls, shelves and paper. Found items are stored by security teams with no reliable way to link them to their owners, so a backlog builds up and unclaimed items are handed to Customs after 90 days.

## What Tafuta does

1. **Log:** cabin crew, cleaners, gate, lounge and sales-office staff (and KAA Security) log a found item in under a minute: photo, category, colour, brand, description, station, and flight and seat for cabin finds. A private detail for checking ownership is recorded for staff only.
2. **Report:** passengers report a loss with their booking reference and get a tracking reference straight away.
3. **Match:** every report is scored against every item in custody across the network on six signals: category, description, colour, brand, place and time. Staff see a confidence score and the reasons behind it.
4. **Tell passengers first:** items found at a seat are matched to the booking manifest, so the passenger can be contacted before they report the loss.
5. **Verify & release:** a digital version of the release form, with ID sighted, booking confirmed, a private detail only the owner knows, and an e-signature.
6. **Close out:** a 90-day holding clock on every item, an automatic Customs manifest, a shared custody record with KAA, and a full audit trail.

## Try the demo

Open the live demo, or download `index.html` and open it in any browser. No install is needed.

- **Staff console:** Overview, Match queue, Custody register, Log found item, Customs handover, Audit & messages, How it fits KQ.
- **Passenger view:** report a lost item (try booking `B8LK3S`, surname `Njeri`) or track a report (try `NBOKQ10452`).
- **Reset demo data** is in the footer.

All people, bookings and items in the demo are fictional, and messages are simulated.

## How matching works

| Signal | Weight | Scoring |
| --- | --- | --- |
| Description | 30 | TF-IDF text similarity with airline-specific synonyms |
| Category | 20 | Same or related category |
| Where | 14 | Same flight and seat, same flight, same station |
| Colour | 12 | Same colour or colour family |
| Brand | 12 | Exact match (skipped when unknown) |
| When | 12 | Found within 48 hours of the loss, fading over 4 weeks |

Weights are re-balanced when a signal is missing. 75% and above is a high-confidence match. Staff confirm every match before anything is released.

## Roadmap to production

- TypeScript / Next.js front end, an API service and a managed PostgreSQL database
- Reservation-system adapter (Amadeus today, Sabre after migration) for booking and seat-manifest lookups
- WhatsApp, SMS and email notifications through the airline's existing channels
- Single sign-on for staff, role-based access, retention rules in line with Kenya's Data Protection Act, 2019
- Image recognition on item photos and multilingual (English and Swahili) text matching

## Author

Valerie Mwangi, BSc Software Engineering, USIU-Africa · [github.com/Kare100](https://github.com/Kare100) · [Portfolio](https://valerie-portfolio-chi.vercel.app/)
