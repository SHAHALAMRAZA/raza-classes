# Raza Classes — Supabase Auth Integration (v1.1.7)

This patch keeps the existing Raza Classes portal and fixes privileged Supabase database writes for student profile synchronization.

## Render environment
- `SUPABASE_URL`
- `SUPABASE_SECRET_KEY`
- `SUPABASE_SERVICE_ROLE_KEY` (legacy JWT service_role; used for privileged PostgREST/Admin operations)
- `SUPABASE_PUBLISHABLE_KEY` (used for normal email/password sign-in)

Do not commit `.env` or any secret values.
