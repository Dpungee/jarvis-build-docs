# System Health Snapshot

*Auto-generated: 2026-02-27 00:02 UTC*

## VPS Status
| Metric | Value |
|--------|-------|
| Uptime | up 5 days, 6 hours, 54 minutes |
| Disk | 22G / 96G (23%) |
| Memory | 1.8Gi / 7.8Gi |

## Docker Containers
```
nebula-mint: Up 3 hours
```

## PM2 Processes (Online)
jarvis-agents, jarvis-convo-logger, jarvis-ste, jarvis-context-api, jarvis-monitor, jarvis-watchdog, jarvis-trainer, jarvis-autonomy, jarvis-openclaw, openclaw-tunnel, jarvis-training, jarvis-telegram

## Cron Jobs
```
0 */6 * * * /home/claude-mcp/jarvis-backup.sh >> /home/claude-mcp/jarvis-backup.log 2>&1
2 0 * * * /home/claude-mcp/jarvis-docs-sync.sh >> /home/claude-mcp/jarvis-docs-sync.log 2>&1
@reboot sleep 15 && /usr/local/bin/pm2 resurrect
@reboot sleep 30 && docker exec agent-zero sh -c 'mkdir -p /root/.claude && cp /a0/usr/.claude-credentials.json /root/.claude/.credentials.json && cp /a0/usr/.claude-config.json /root/.claude/.claude.json' 2>/dev/null || true
0 */6 * * * cat /root/.claude/.credentials.json | docker exec -i agent-zero bash -c 'cat > /root/.claude/.credentials.json' 2>/dev/null
0 * * * * /home/claude-mcp/jarvis-chat-cleanup.sh >> /home/claude-mcp/jarvis-chat-cleanup.log 2>&1
```
