# Raza Classes — Supabase Auth Integration (v1.1.8)

This patch keeps the existing Raza Classes portal and fixes privileged Supabase database writes for student profile synchronization.

## Render environment
- `SUPABASE_URL`
- `SUPABASE_SECRET_KEY`
- `SUPABASE_SERVICE_ROLE_KEY` (legacy JWT service_role; used for privileged PostgREST/Admin operations)
- `SUPABASE_PUBLISHABLE_KEY` (used for normal email/password sign-in)

Do not commit `.env` or any secret values.


### v1.1.8
Mirrors Admin Classes, Subjects, and Chapters into the Supabase `classes`, `subjects`, and `chapters` tables while preserving the existing portal UI and local fallback. Existing local classes are synchronized on server startup.
