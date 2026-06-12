# hubble-wms-backups

Encrypted nightly `pg_dump` backups of the Hubble WMS Supabase database.

- Schedule: 01:00 ICT daily (`0 18 * * *` UTC; GH cron may drift 5-30 min)
- Scope: `public` + `auth` schemas, read-only `backup_role`
- Encryption: `age` (public key in repo variable `AGE_PUBLIC_KEY`; private key offline)
- Retention: `daily/` 30 newest, `monthly/` 12 newest (1st of month)
- Restore: `age -d -i age-key.txt wms_YYYYMMDD.sql.gz.age | gunzip > restore.sql`

Setup, operations, and restore-drill checklist: `supabase/backups/README.md` in the
local (non-published) WMS project folder.
