# System Health Snapshot

*Auto-generated: 2026-02-25 18:04 UTC*

## VPS Status
| Metric | Value |
|--------|-------|
| Uptime | up 4 days, 56 minutes |
| Disk | 68G / 96G (70%) |
| Memory | 3.1Gi / 7.8Gi |

## Docker Containers
```
agent-zero: Up 10 hours
```

## PM2 Processes (Online)
jarvis-bridge, jarvis-agents, jarvis-watchdog, jarvis-convo-logger, jarvis-ste, jarvis-context-api

## Cron Jobs
```
0 */6 * * * /home/claude-mcp/jarvis-backup.sh >> /home/claude-mcp/jarvis-backup.log 2>&1
2 0 * * * /home/claude-mcp/jarvis-docs-sync.sh >> /home/claude-mcp/jarvis-docs-sync.log 2>&1
```
