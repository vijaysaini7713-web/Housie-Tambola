# Housie / Tambola — Employee Game

## Shared Supabase project configuration (November 2026)
Both games use the **same Supabase project** (project ref `jlwgzopkdlsgwcaxvfnn`). Their `config.js` public URL and publishable key are configured. The database **is not installed by simply editing config.js**.

**Run the combined installer once:** open [supabase/install-both-games.sql](https://github.com/vijaysaini7713-web/Spin-the-Wheel/blob/main/supabase/install-both-games.sql), copy its complete contents, then run them in your Supabase project's **SQL Editor**. This provisions shared admin/employee tables, separate settings tables, games, security policies and RPC functions. Do not run separate outdated SQL installers instead.

**Admin setup:** Supabase Dashboard > Authentication > Users > Add user (set email and password). Copy UUID and run `insert into public.admins(user_id) values ('UUID_FROM_AUTH_USERS') on conflict do nothing;`. No default admin password exists. Never share your admin password, database password or service-role key. GitHub Pages must also be enabled separately if you need a public URL.


A responsive browser-based employee Tambola game with an admin-controlled random 1–90 number caller, unique persistent tickets, live board updates, and server-verified winners.

## Features
- Employee Name and unique Employee ID registration; one ticket per ID.
- Each ticket contains 15 unique numbers (5 per row across 3 rows).
- Auto-highlight called numbers; player display refreshes every 4 seconds.
- Secure admin: login via Supabase Auth, event name, open/close ticket registration, call numbers, export participants, reset event.
- Server-verifiable first-winner claims: Early Five, Top Row, Middle Row, Bottom Row, Full House.

## Setup
1. Create a new Supabase project (separate from Wheel unless you deliberately integrate schemas).
2. Run [supabase/schema.sql](supabase/schema.sql) in the **SQL Editor**.
3. Add admin user under **Authentication → Users** and run `insert into public.admins(user_id) values ('ADMIN_AUTH_UUID');`.
4. Edit `config.js` with the **project URL** and **publishable/anon key**. Never use a service-role key.
5. Serve via a local static server or enable GitHub Pages at **Settings → Pages → Deploy from a branch → main → root**.

## Notes
This version uses a 3 × 5 ticket, not the traditional 3 × 9 ticket layout. One ticket per ID per round; admin reset starts a fresh round. An Employee ID is not identity proof: use HR/SSO/OTP and manual winner verification for real prizes. Simultaneous claims and draws are serialized by database advisory locks and primary keys. Admin authentication never uses a hardcoded frontend password.
