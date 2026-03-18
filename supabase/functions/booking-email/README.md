# booking-email Edge Function

Sends booking form submissions to **support@themartinhenderson.org** via Resend. No email is sent to the user.

## Deploy (Supabase Dashboard)

1. **Supabase** → your project → **Edge Functions** → **Create a new function**.
2. Name it `booking-email` and paste the contents of `index.ts` (from this folder).
3. **Settings** → **Edge Function Secrets** → add:
   - `RESEND_API_KEY` = your API key from [resend.com](https://resend.com) (API Keys).
   - `ADMIN_EMAIL` (optional) = who receives the booking emails. If unset, uses `support@themartinhenderson.org`.
4. Deploy the function. Note the URL:  
   `https://<YOUR_PROJECT_REF>.supabase.co/functions/v1/booking-email`

**Resend “testing” mode:** With an unverified domain, Resend only allows sending **to your own Resend account email**. So for testing, set `ADMIN_EMAIL` to that address (e.g. the one you used to sign up, like `mathen2314@proton.me`). After you [verify your domain](https://resend.com/domains) (e.g. themartinhenderson.org) and use a `from` address on that domain, you can send to any address (e.g. support@themartinhenderson.org).

## Frontend

In your booking page HTML, set the form endpoint so it points to your function:

```html
<form id="bookingForm" data-endpoint="https://YOUR_PROJECT_REF.supabase.co/functions/v1/booking-email" ...>
```

Replace `YOUR_PROJECT_REF` with your Supabase project reference (from Project Settings → General).

## Resend

- **From address:** The function uses `Booking Form <onboarding@resend.dev>` by default (Resend’s test sender). For production, verify your domain in Resend and change the `from` value in `index.ts` to e.g. `Booking Form <noreply@themartinhenderson.org>`.
- **To:** Controlled by the `ADMIN_EMAIL` secret (default `support@themartinhenderson.org`). For testing without a verified domain, set `ADMIN_EMAIL` to your Resend account email.

## Required fields (all validated)

fullName, email, phone, organization, bookingFor, sex, occupation, homeAddress, city, state, zipcode, nearestAirport, preferredDate, preferredTime, location.
