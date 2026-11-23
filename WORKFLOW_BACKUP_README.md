# n8n workflow backup

This guide maps the backup-related files and settings in this checkout. It is not a tested recovery procedure.

## What is checked in

- The main [Compose manifest](docker-compose.yml) and the [alternate manifest](docker-composebackup.yml) both declare `n8n_backup`, whose entrypoint schedules PostgreSQL dumps under the host bind mount `./backups/n8n_db_backups` and removes dumps that match `-mtime +7`.
- Both files declare `N8N_PUSH_BACKUP_ENABLED` and `N8N_RECOVERY_MODE` on `n8n_main`. Treat those as configuration declarations, not proof that the selected n8n image recognizes them or creates or restores workflow backups.
- [`backup_n8n_workflows.sh`](backup_n8n_workflows.sh) and [`backup_n8n_workflows.ps1`](backup_n8n_workflows.ps1) are helpers for an existing instance, not part of an offline check.
- `n8n/backup/workflows/` contains a checked-in example. The separate `backups/` directory is for instance data; it is not a checked-in recovery guide or a trusted source of test fixtures.

## Recovery status

There is no tracked `backups/n8n_README.md`. Verify the actual backup files and restore behavior in a separately authorized environment before relying on them. A tracked script or volume setting does not prove a backup is current or restorable.

For docs-only changes, use the README's [offline verification](README.md#offline-verification). Do not run backup scripts, schedule jobs, read credentials, or restore, import, or execute workflows for this check.