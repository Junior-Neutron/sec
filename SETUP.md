# Curaters Website B — Setup

## Files and routes
- `index.html` — Home
- `destinations.html` — Destination explorer
- `about.html` — About / three Curaters principles
- `day-trips.html`, `group-trips.html`, `private-trips.html`, `hosted-trips.html` — Trip categories
- `trip.html?id=<offer-id>` — Individual offer details
- `book.html` — Booking wizard
- `faq.html` — FAQs
- `style.css`, `script.js` — Shared styling and behavior

Upload all HTML files plus `style.css` and `script.js` to the same GitHub Pages repository folder. Keep the `supabase/` folder in the repository for the server-side booking function.

## Booking delivery — not live until configured
The browser does not open an email application. It POSTs to the configured Supabase Edge Function. The endpoint and publishable key are intentionally blank in the HTML until a Curaters-owned Supabase project is selected.

1. Create or select a Supabase project for Curaters.
2. From the project folder, deploy the function to the chosen project (use the exact project reference shown in Supabase):
   `supabase functions deploy booking-request --project-ref <project-ref>`
3. Set these secrets in the Supabase project (Dashboard → Edge Functions → Secrets, or `supabase secrets set`): (never place them in browser JavaScript):
   - `BREVO_API_KEY`
   - `BREVO_SENDER_EMAIL` (must be a verified sender in Brevo)
   - `BREVO_SENDER_NAME` (optional)
   - `CURATERS_TO_EMAIL` (defaults to `travelcuraters@gmail.com`)
   - `CURATERS_ALLOWED_ORIGIN` (defaults to `https://junior-neutron.github.io`)
4. Deploy the function and copy its URL:
   `https://<project-ref>.supabase.co/functions/v1/booking-request`
5. In every HTML page, set:
   - `curaters-booking-endpoint` to that function URL
   - `curaters-booking-api-key` to the project's publishable key
6. Submit a test booking and confirm delivery to `travelcuraters@gmail.com`.

Do not reuse credentials from another project unless the owner explicitly approves that. Supabase secrets stay on the server; the publishable key may be placed in the HTML meta tag.

The function validates the request and sends the email using Brevo's server-side API key. The API key is never exposed to visitors. Do not commit `.env` files or real keys.

## APIs
- Exchange rates: open.er-api.com, base USD, currencies USD/GHS/EUR/GBP.
- Weather and sunset: Open-Meteo.
- Destination background and Commons images: Wikipedia/Wikimedia APIs.
- Local time: timezone returned by Open-Meteo, formatted in the browser.

## Image navigation
Destination cards open an internal Curaters dialog. The dialog uses plain-text image attribution and plain-text source context; there are no clickable Wikipedia/Wikimedia source links. Images do not open an external source page.

## Important limitations
- The booking service is prepared but not active until Supabase and Brevo are configured and deployed.
- The admin dashboard and its database are deliberately deferred to a later phase.
- External image APIs can fail or change their results; existing local destination data remains the fallback.
