# Pulse 2.0 Responsive — Commercial / Multi-user build

## What this build is
A mobile-first Pulse PWA using ONE Supabase project and PostgreSQL Row Level Security (RLS). Every user gets an isolated data space by `user_id`; a separate database per user is not needed.

## Before deploying
1. Run `supabase_commercial_schema.sql` in Supabase SQL Editor.
2. Verify RLS is enabled and Security Advisor has no unexpected high-severity findings.
3. In Supabase Authentication > URL Configuration, set Site URL to your production GitHub Pages URL, for example:
   https://prem0592.github.io/pulse-expense-tracker_cloud/
   Add the same production URL/path to Redirect URLs.
4. Edit `config.js` and replace `PASTE_YOUR_SB_PUBLISHABLE_KEY_HERE` with the project's `sb_publishable_...` key.
5. NEVER use `sb_secret_...` or `service_role` in config.js.
6. Upload `index.html`, `config.js`, `manifest.json`, and `sw.js` to the root of GitHub Pages.
7. Keep the repository free of personal expense CSVs and backups.

## Existing users
The new schema uses new `categories`, `payment_methods`, `budgets`, etc. Your existing `expenses` table can be migrated separately if you already have it. Do not drop your existing data blindly.

## Commercial security model
- Public app code is expected.
- Publishable key is expected to be public.
- Supabase Auth authenticates the user.
- RLS enforces per-user row isolation in PostgreSQL.
- No secret/service-role key is used in the browser.
- The browser never receives another user's rows if RLS is configured correctly.

## iPhone
Open the GitHub Pages URL in Safari and use Share > Add to Home Screen.

## Important
This is a production-oriented foundation, not a substitute for a formal security review. Before charging customers, add a privacy policy, terms, account deletion/export, backups, monitoring, abuse/rate-limit controls, and a server-side billing/entitlements system.
