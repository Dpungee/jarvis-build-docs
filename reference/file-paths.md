# Reference: All File Paths

## VPS Host — /home/claude-mcp/
```
bridge.py                    ← Telegram bridge
bridge_audit.py              ← Audit logging module
watchdog.py                  ← Self-healing watchdog
background_agents.py         ← Health monitor
convo_logger.py              ← Conversation memory logger
dashboard_miner.py           ← Extracts msgs from Agent Zero HTML logs
proactive_intel.py           ← GitHub/cost/server intelligence
self_training_engine.py      ← STE — 4-module AI learner
jarvis-startup.sh            ← Boot orchestration script
jarvis-backup.sh             ← Config backup cron script
jarvis-docs-sync.sh          ← Daily GitHub docs push (added v3+)
jarvis.service               ← systemd service file
jarvis-backups/              ← Timestamped config backups (last 10 each)
jarvis-docs/                 ← This documentation repo
```

## Inside Agent Zero Container — /a0/
```
prompts/agent.system.main.role.md   ← JARVIS personality (CRITICAL — back this up)
usr/settings.json                   ← Agent Zero config (model, context length, etc.)
usr/.env                            ← Environment variables + API keys
usr/workdir/                        ← Where JARVIS creates files during tasks
usr/skills/jarvis-memory/memory.py  ← Memory CLI tool
usr/skills/jarvis-feedback/         ← Feedback tracking
usr/skills/jarvis-learned/          ← All auto-learned skill files
logs/*.html                         ← One HTML file per conversation session
```

## Runtime / Temp
```
/tmp/jarvis-bridge-audit.jsonl      ← Real-time log of all bridge messages
/tmp/jarvis-dashboard-audit.jsonl   ← Messages from dashboard logs
/tmp/jarvis-convo-processed.json    ← What convo_logger has processed
/tmp/jarvis-ste/state.json          ← STE counters + timestamps
/tmp/jarvis-ste/skill_audits.jsonl  ← Skill audit history
/tmp/jarvis-intel/cost_history.jsonl ← OpenRouter spend over time
/tmp/jarvis-intel/disk_history.jsonl ← Disk usage trend
/tmp/jarvis-intel/latest_report.json ← Most recent intelligence report
```

