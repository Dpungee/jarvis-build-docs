# Cron Jobs

## User Crontab (claude-mcp user)
```
0 */6 * * * /home/claude-mcp/jarvis-backup.sh >> /home/claude-mcp/jarvis-backup.log 2>&1
2 0 * * * /home/claude-mcp/jarvis-docs-sync.sh >> /home/claude-mcp/jarvis-docs-sync.log 2>&1
```

## Backup Job (Every 6 Hours)
| File Backed Up | Backup Location |
|----------------|----------------|
| /a0/usr/settings.json | /home/claude-mcp/jarvis-backups/settings/ |
| /a0/usr/.env | /home/claude-mcp/jarvis-backups/env/ |
| /a0/prompts/agent.system.main.role.md | /home/claude-mcp/jarvis-backups/prompts/ |
| bridge.py, watchdog.py, background_agents.py | /home/claude-mcp/jarvis-backups/bridge/ |

Keeps last 10 snapshots per type. Auto-prunes older ones.

## Docs Sync Job (Daily at 12:02 AM UTC)
Updates current-state docs with live data and pushes to GitHub.
See: `/home/claude-mcp/jarvis-docs-sync.sh`

## Restore From Backup
```bash
# List available
ls /home/claude-mcp/jarvis-backups/settings/

# Restore settings
docker cp /home/claude-mcp/jarvis-backups/settings/settings_TIMESTAMP.json agent-zero:/a0/usr/settings.json

# Restore system prompt  
docker cp /home/claude-mcp/jarvis-backups/prompts/role_TIMESTAMP.md agent-zero:/a0/prompts/agent.system.main.role.md
```

## System Crons (Ubuntu auto-installed)
- certbot: daily SSL cert renewal
- logrotate, apt, dpkg: standard Ubuntu maintenance

