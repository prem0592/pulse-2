# Pulse 2.0 — Commercial v9

Clean commercial build for GitHub Pages + Supabase.

## Replace in GitHub
- index.html
- manifest.json
- sw.js

Keep your existing `config.js` and its `sb_publishable_...` key unchanged.

## v9 changes
- Cleaned duplicate account-menu/sign-out handlers.
- Username click opens account menu; it no longer opens Profile automatically.
- Sign out is available from the account menu and Settings.
- Compact responsive greeting and username.
- Exact starter categories and payment-method lists are account-scoped and only applied when the signed-in user chooses “Replace list”.
- Payment methods: AXIS Indian Oil CC, AXIS Select CC, BOB UNI Card Rupay CC, Cash, HDFC Dinners Club CC, HDFC Regalia CC, ICICI Amazon Pay CC, ICICI Rupay CC, IDFC First CC, PhonePe, SBI CC, Uni Card CC, Gpay, Pluxee Sodexo.
- Categories: Bike petrol, Car petrol, Non Veg, Outing, Groceries, Home Decor, Medicine, Milk, Saloon, Snacks, Veggies.
- Removed sensitive expense data from localStorage caching; cloud data is loaded from Supabase after authentication.
- PWA cache bumped to v9.

Do not upload Supabase service-role/secret keys or SQL admin files to the public GitHub repository.
