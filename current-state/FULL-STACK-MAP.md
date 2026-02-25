# JARVIS Full Stack Map

*Auto-updated daily. See git log for last update.*

## Every Running Process

| Process | File | Manager | Model | Cost/Day | Purpose |
|---------|------|---------|-------|---------|---------|
| agent-zero | Docker container | Docker | Set in settings.json | Varies | Main JARVIS AI |
| searxng | Inside container | supervisord | None | $0 | Private search engine |
| run_tunnel.py | Inside container | supervisord | None | $0 | Cloudflare tunnel |
| run_ui.py | Inside container | supervisord | None | $0 | Web dashboard |
| bridge.py | /home/claude-mcp/ | PM2 | None | $0 | Telegram router |
| watchdog.py | /home/claude-mcp/ | PM2 | None | $0 | Self-healing |
| background_agents.py | /home/claude-mcp/ | PM2 | None | $0 | Health monitor |
| convo_logger.py | /home/claude-mcp/ | PM2 | None | $0 | Memory logger |
| self_training_engine.py | /home/claude-mcp/ | PM2 | Gemini 2.0 Flash | ~$0.40 | 4-module AI learner |
| discord_bridge.py | /root/ | PM2/systemd | Unknown | Unknown | Discord integration |
| jarvis.service | systemd unit | systemd | None | $0 | Boot orchestrator |
| jarvis-backup.sh | cron | crontab | None | $0 | 6hr config backup |
| jarvis-docs-sync.sh | cron | crontab | None | $0 | Daily GitHub docs push |

## Network Map
```
Internet
  → VPS (187.77.214.201)
  → nginx (port 80/443)
  → Agent Zero dashboard (localhost:50080)

Telegram API (outbound from bridge.py)
  → bridge.py → Agent Zero API (localhost:50080)

OpenRouter API
  → self_training_engine.py (STE)
  → Agent Zero (when responding to you)

GitHub API (outbound from proactive_intel.py)
  → Monitors Dpungee repos for activity + failed Actions
```

## Message Flow (Telegram → JARVIS → Back)
```
1. You type in Telegram
2. bridge.py receives → logs to /tmp/jarvis-bridge-audit.jsonl
3. POST to http://localhost:50080/telegram_message_sync
4. Agent Zero → AI model via OpenRouter
5. Response → bridge.py
6. Sent to Telegram (text + any images)
```

