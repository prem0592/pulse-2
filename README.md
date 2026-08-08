# Pulse v10 — Clean Commercial Build

Pulse is a responsive, cloud-synced expense tracker for GitHub Pages + Supabase.

## Replace in GitHub
- `index.html`
- `manifest.json`
- `sw.js`

Keep your existing `config.js` with ONLY the Supabase project URL and `sb_publishable_...` key.
Do not upload a `sb_secret_...` or service-role key.

## v10 highlights
- Email/password authentication retained; no paid SMS/WhatsApp dependency.
- Forgot-password flow.
- Compact responsive account identity and reliable account menu.
- Fast expense entry and account-scoped Categories / Payment Methods / Paid by.
- Approved starter lists are available through Setup → Replace list and never overwrite another account.
- Cloud data is read/written through Supabase after authentication; expense data is not cached in localStorage.
- Dashboard with monthly totals, transaction count, average, largest expense, category breakdown, budget health and improved daily Spending Pulse chart.
- Reports screen with month selector, category totals and payment-method totals.
- CSV import/export uses one expense per row and escapes commas/quotes/newlines safely.
- Responsive desktop, Android and iPhone browser/PWA layouts.
- Delete-account UI with password re-authentication and a server-side Edge Function.

## Supabase security
The database should have RLS policies based on `auth.uid() = user_id` and user-owned tables linked to `auth.users(id)` with `ON DELETE CASCADE`.

## Delete Account Edge Function
Deploy `supabase/functions/delete-account/index.ts` as the Supabase Edge Function named `delete-account`.

The function verifies the caller's JWT, derives the user ID from the verified session, and performs `auth.admin.deleteUser(user.id)` using the server-side `SUPABASE_SERVICE_ROLE_KEY` environment variable. The service-role key must never be placed in `index.html`, `config.js`, GitHub, or any browser-accessible file.

If the Edge Function is not deployed, Pulse will show an error and will not pretend that the account was deleted.

## Recommended deployment
1. Keep your current Supabase database and RLS configuration.
2. Replace the three GitHub Pages files above.
3. Keep your current `config.js`.
4. Deploy the Edge Function from `supabase/functions/delete-account`.
5. Hard-refresh the PWA/browser after deployment.
6. Test with a separate test account before using Delete Account on a real account.

## Commercial defaults
Pulse does not hard-code a personal user's categories/payment methods. New users should configure their own lists. The starter lists are only applied when that signed-in user explicitly chooses Replace list.
