# RU Soko on Cloudflare Workers
1. `npm i -g wrangler && wrangler login`
2. `wrangler d1 create ru-soko-db` → paste the id into wrangler.toml
3. `wrangler d1 execute ru-soko-db --remote --file=schema.sql`
4. Secrets (never stored in code):
   - `wrangler secret put JWT_SECRET`   (long random string)
   - `wrangler secret put ADMIN_USER`   (your secret admin username)
   - `wrangler secret put ADMIN_PASS`   (long unique passphrase)
5. `wrangler deploy`
Admin sign-in: open `https://YOUR-SITE/#staff` (no link exists in the UI). 5 failed tries per 15 min per IP are blocked; admin tokens last 1 hour.

## PWA
Served over HTTPS by Workers, so it's installable (Chrome/Edge "Install", iOS Safari → Share → Add to Home Screen).
Offline: app shell + last listings are cached (`public/sw.js`). Login/contact/reviews always need a connection.
After changing files, bump `V` in `public/sw.js` so users get the update.
Custom domain: Workers & Pages → ru-soko → Settings → Domains.
