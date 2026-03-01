# System Health Snapshot

*Auto-generated: 2026-03-01 00:02 UTC*

## VPS Status
| Metric | Value |
|--------|-------|
| Uptime | up 1 week, 6 hours, 54 minutes |
| Disk | 26G / 96G (28%) |
| Memory | 3.8Gi / 7.8Gi |

## Docker Containers
```
nebula-mint: Up 2 days
```

## PM2 Processes (Online)
jarvis-convo-logger, jarvis-ste, jarvis-context-api, jarvis-monitor, jarvis-watchdog, jarvis-trainer, jarvis-openclaw, jarvis-comms, jarvis-briefing, jarvis-agents, mission-api, jarvis-log-watcher, pm2-slack, agent-codebot, agent-devops, agent-analyst, agent-scribe, agent-scheduler, pm2-health, pm2-logrotate, jarvis-memory, openclaw-tunnel, pnl-games

## Cron Jobs
```
0 */6 * * * /home/claude-mcp/jarvis-backup.sh >> /home/claude-mcp/jarvis-backup.log 2>&1
2 0 * * * /home/claude-mcp/jarvis-docs-sync.sh >> /home/claude-mcp/jarvis-docs-sync.log 2>&1
@reboot sleep 15 && /usr/local/bin/pm2 resurrect
@reboot sleep 30 && docker exec agent-zero sh -c 'mkdir -p /root/.claude && cp /a0/usr/.claude-credentials.json /root/.claude/.credentials.json && cp /a0/usr/.claude-config.json /root/.claude/.claude.json' 2>/dev/null || true
0 */6 * * * cat /root/.claude/.credentials.json | docker exec -i agent-zero bash -c 'cat > /root/.claude/.credentials.json' 2>/dev/null
0 * * * * /home/claude-mcp/jarvis-chat-cleanup.sh >> /home/claude-mcp/jarvis-chat-cleanup.log 2>&1
0 13 * * * /home/claude-mcp/openclaw-workspace/daily-briefing.sh
5 13 * * * python3 /home/claude-mcp/openclaw-workspace/drive-sync/sync.py >> /home/claude-mcp/openclaw-workspace/drive-sync/sync.log 2>&1
0 * * * * curl -sf http://localhost:8888/landing.html > /dev/null && curl -s 'http://localhost:4200/log?msg=Landing+page+up&level=gray' || curl -s 'http://localhost:4200/log?msg=Landing+page+DOWN&level=red'
0 4 * * * find /tmp -name 'subagent-*' -mtime +1 -delete 2>/dev/null
0 3 * * * /home/claude-mcp/.nvm/versions/node/v22.22.0/bin/openclaw sessions cleanup >> /tmp/sessions-cleanup.log 2>&1
```
