# Curaters Website B — Review Notes

## Included
- Multi-page route files for home, destinations, about, booking, FAQs, four trip categories, and individual trip details.
- About cards use Website B palette and the three approved statements.
- Hero carousel now auto-advances and has a slow zoom/drift treatment.
- Hero live destination card shows local time, weather, and sunset when Open-Meteo data is available.
- Horizontal ticker repeats destination entries for a continuous movement effect, with local time and weather.
- Existing currency selector and Open Exchange Rates API integration retained (USD, GHS, EUR, GBP).
- Existing Open-Meteo current weather and seven-day forecast retained.
- Wikimedia enrichment retained with static data fallback.
- Image credits and Wikipedia background attribution are plain text, not outbound links.
- Booking wizard retained; secure direct-send Edge Function template added.

## Destination exclusions
The source destination list contains no Uganda, Rwanda, or Namibia entries.

## Validation performed
- JavaScript syntax checked with Node.js `node --check`.
- Static route files and local links checked.
- External Wikipedia/Wikimedia image-navigation anchors removed from the destination dialog.

## Not yet verified live
- API responses and live time/weather rendering in a deployed browser.
- Brevo email delivery.
- Supabase Edge Function deployment.
- Any hosting-side cache behavior.
- Admin dashboard/database work (intentionally deferred).

## Required before booking can go live
Set Supabase function secrets, deploy the function, and configure the endpoint and publishable key in the HTML meta tags as described in `SETUP.md`.
