# report-scam-email Edge Function

Sends scam/impersonation report form submissions to **support@themartinhenderson.org** via Resend (from noreply@themartinhenderson.org). No email to the reporter.

## Deploy (Supabase Dashboard)

1. **Edge Functions** → **Create a new function** → name: `report-scam-email`.
2. Paste the contents of `index.ts`.
3. Ensure secrets **RESEND_API_KEY** and optionally **ADMIN_EMAIL** are set (same as other email functions).
4. Deploy. URL: `https://cgmvzrjxkldxtkrydcdv.supabase.co/functions/v1/report-scam-email`

## Required fields (validated)

platform, handle, details. Optional: name, email, amount.
