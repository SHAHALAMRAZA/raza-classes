# Raza Classes — Supabase Auth Integration (v1.1.2)

This build keeps the existing Raza Classes portal and adds server-side Supabase Auth integration for student accounts. Admin authentication remains protected by the existing server-side admin system.

## What changed

- Student registration creates a Supabase Auth user on the trusted server.
- Student login verifies credentials through Supabase Auth.
- Existing students can be migrated to Supabase Auth automatically on their first successful legacy login.
- Admin-created students are also created in Supabase Auth.
- Admin password reset updates the linked Supabase Auth password.
- Added `/health` endpoint for deployment checks.
- Server explicitly binds to `0.0.0.0` for hosted deployments.

## Environment variables

Required for Supabase Auth integration:

- `SUPABASE_URL=https://<project-ref>.supabase.co`
- `SUPABASE_SECRET_KEY=sb_secret_...`

Keep the Supabase secret key only in the server/Render environment. Never put it in browser code, GitHub, screenshots, or chat.

Existing variables remain:

- `NODE_ENV=production`
- `APP_SECRET=<long random secret>`
- `HASH_SALT=<different long random secret>`
- `ADMIN_PASSWORD=<strong initial password>`
- `PORT=<provider supplied port>`

## Local test

```bash
npm install
npm start
```

If `SUPABASE_URL` and `SUPABASE_SECRET_KEY` are absent, the app keeps its legacy local authentication mode so the package can still be tested locally.

## Important production note

This step integrates Supabase Auth, but the application's main content data and uploads are still being migrated from the local JSON/file storage to Supabase Database + Storage. Do not treat this build as the final persistence migration yet.

### Supabase Auth Admin compatibility
Some hosted Supabase projects currently reject Auth Admin POST mutations (`/auth/v1/admin/users`) when only the new `sb_secret_...` key is supplied, returning `bad_jwt` / “This endpoint requires a valid Bearer token”. This build supports `SUPABASE_SERVICE_ROLE_KEY` as a temporary server-only compatibility key for Auth Admin create/update operations, while `SUPABASE_SECRET_KEY` remains available for server-side Supabase access. Never expose either key in browser code or commit their real values.


## v1.1.4 Auth key compatibility
The server supports both Supabase legacy `service_role` JWT keys (sent with apikey + Authorization Bearer) and new `sb_secret_...` keys (apikey only). Never expose either key to the browser or GitHub.


### Supabase profile sync
Student Auth accounts are synchronized to `public.students` using the server-only `SUPABASE_SERVICE_ROLE_KEY`. Never expose this key in frontend code or commit it to GitHub.
