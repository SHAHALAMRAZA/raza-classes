# Raza Classes — Persistent Supabase Storage (v1.2.0)

This patch keeps the existing Raza Classes portal UI and adds a persistent Supabase-backed application state layer so Render restarts/redeploys do not erase classes, materials, assignments, tests, quizzes, notices, homepage highlights, syllabus, Exam Adda, or student records.

## Required Render environment variables
- `SUPABASE_URL`
- `SUPABASE_SECRET_KEY`
- `SUPABASE_SERVICE_ROLE_KEY` (legacy service_role JWT; used for privileged Auth/PostgREST compatibility)
- `SUPABASE_PUBLISHABLE_KEY` (new `sb_publishable_...` key for student password sign-in)
- Existing `APP_SECRET`, `HASH_SALT`, `ADMIN_PASSWORD`

## Supabase setup
Create the following table once in SQL Editor:

```sql
create table if not exists public.app_data (
  key text primary key,
  value jsonb not null,
  updated_at timestamptz not null default now()
);

alter table public.app_data enable row level security;
```

The server accesses this table with the server-side privileged key. Do not expose any secret/service-role key in frontend code.

## Important
The application state is mirrored to `public.app_data`. The existing normalized `students`, `classes`, `subjects`, and `chapters` tables are still maintained where supported, but `app_data` is the authoritative persistent state for the current portal until the full normalized migration is completed.
