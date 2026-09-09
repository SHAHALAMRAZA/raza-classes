# Raza Classes — Production Package

This package preserves the existing Raza Classes portal and adds production-oriented server hardening without removing the existing features.

## Local test

```bash
npm install
npm start
```

Open the URL printed by the server. If port 3000 is busy, the app automatically tries the next available port.

Default admin credentials for a fresh local database:
- Username: `admin`
- Password: `Admin@12345`

Change the password immediately in Admin Settings.

## Production

Set these environment variables in your hosting provider:

- `NODE_ENV=production`
- `APP_SECRET=<long random secret>`
- `HASH_SALT=<different long random secret>`
- `ADMIN_PASSWORD=<strong initial password>`
- `PORT=<provider supplied port>`

The application stores its data in `data/db.json`, including uploaded files as encoded data. **For real student use, the `data` directory must be on persistent storage/volume** so deployments or restarts do not erase data. For larger production usage, move file uploads and application data to managed object/database storage.

The server also adds security headers, session expiry, atomic database writes, upload/request size limits, and basic login/registration rate limiting.
