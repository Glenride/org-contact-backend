# org-contact-backend

Contact form backend for the .org sites (dvaughnhouse.org, thinktank.dvaughnhouse.org)
and the Links page (links.dvaughnhouse.com).

Cloudflare Worker serving `POST /api/contact` on `dvaughnhouse.org`, via a Worker
route on that zone. Mirrors the .com backend (`dvaughnhouse.com/functions/api/contact.js`)
exactly: same fields, validation, honeypot, 5/hr per-IP rate limit, same D1 database
(`dvaughnhouse-contacts`) so every contact lands in one `contacts` table, same Resend
email to dvaughnhouse@gmail.com.

CORS allowlist: `https://dvaughnhouse.org`, `https://thinktank.dvaughnhouse.org`,
`https://links.dvaughnhouse.com`, `https://links-d-vaughn-house.pages.dev`, `https://muse.ai`.

Secrets: `RESEND_API_KEY` (set with `wrangler secret put RESEND_API_KEY` — never committed).

Deploy: `wrangler deploy` (uses the Cloudflare credential surrogate).
