# MISP for YunoHost (Docker/Compose)

**Status:** experimental. Test in a lab before production.

## What this package does

- Runs MISP, MariaDB, Redis, and misp-modules via Docker Compose
- Proxies through YunoHost’s Nginx (TLS & SSO portal integration)
- Secures Redis with a password by default
- Lets advanced users opt into DB-backed MISP settings

## Install

```bash
sudo yunohost app install ./misp_ynh
```

You’ll be prompted for:
- domain & path (prefer a subdomain and `/`)
- public/private portal access (recommend **private**)
- image tags (default **v2.4.185** for both core & modules)
- DB & Redis passwords (auto-generated if you accept defaults)
- whether to enable DB-backed settings

## Files & data

- Compose file: `/var/www/misp/docker-compose.yml`
- Data directory: `/home/yunohost.app/misp/{db,redis,misp}`

## Upgrade

Bump tags via `yunohost app upgrade` (the script re-renders compose, pulls, and restarts).

## Backup & Restore

Uses YunoHost hooks to stop the stack, archive volumes, and restart on backup; restore replays the files and brings the stack up.

## Notes

- For heavy use, plan for more RAM/IO and tune worker counts.
- Keep the app **private** in YunoHost; manage users inside MISP itself.
