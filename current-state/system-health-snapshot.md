# System Health Snapshot

*Auto-generated: 2026-02-26 00:02 UTC*

## VPS Status
| Metric | Value |
|--------|-------|
| Uptime | up 4 days, 6 hours, 54 minutes |
| Disk | 33G / 96G (35%) |
| Memory | 3.1Gi / 7.8Gi |

## Docker Containers
```
agent-zero: Up 8 minutes
```

## PM2 Processes (Online)
jarvis-agents, jarvis-convo-logger, jarvis-ste, jarvis-context-api, jarvis-monitor, jarvis-watchdog, jarvis-bridge

## Cron Jobs
```
0 */6 * * * /home/claude-mcp/jarvis-backup.sh >> /home/claude-mcp/jarvis-backup.log 2>&1
2 0 * * * /home/claude-mcp/jarvis-docs-sync.sh >> /home/claude-mcp/jarvis-docs-sync.log 2>&1
```
