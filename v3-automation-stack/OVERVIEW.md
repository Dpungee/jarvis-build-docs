# V3 — Automation Stack: JARVIS That Never Dies

## What We Built
A complete self-managing infrastructure: watchdog, health monitor, config backup cron, systemd service for boot persistence, proactive intelligence, and conversation logging.

## Why We Built It
JARVIS kept dying whenever:
- You closed the terminal (bridge stopped)
- The VPS rebooted (nothing restarted)
- A process crashed (no auto-recovery)
- Config got corrupted (no backups)

V3 made JARVIS fully autonomous. It starts itself, monitors itself, heals itself, and backs itself up.

## Components Added

### 1. watchdog.py — Self-Healing
- Checks all JARVIS components every 60 seconds
- Auto-restarts crashed processes
- Maintains config backups with rollback
- Falls back to alternative model if OpenRouter is down
- PM2 name: `jarvis-watchdog`

### 2. background_agents.py — Health Monitor
- CPU alert > 85%, RAM alert > 90%, Disk alert > 80%
- Docker container status check every cycle
- Telegram alerts with 5-min cooldown (no spam)
- Zero AI calls — pure Python
- PM2 name: `jarvis-agents`

### 3. jarvis-backup.sh — Config Backup Cron
- Runs every 6 hours via crontab (`0 */6 * * *`)
- Backs up: settings.json, .env, system prompt, bridge.py, watchdog.py, background_agents.py
- Keeps last 10 snapshots per file type
- Location: `/home/claude-mcp/jarvis-backups/`

### 4. jarvis.service — Systemd Boot Service
- `Type=oneshot + RemainAfterExit=yes`
- Runs `jarvis-startup.sh` on every VPS boot
- Order: wait Docker → start Agent Zero → PM2 resurrect → verify processes → Telegram notification
- Check: `systemctl is-active jarvis`

### 5. proactive_intel.py — Intelligence Monitor
- GitHub activity check every 6 hours (repos under Dpungee)
- Detects failed GitHub Actions
- OpenRouter spend anomaly detection
- Projects monthly cost from current burn rate
- Disk growth rate tracking, predicts full date

### 6. convo_logger.py — Conversation Logger
- Reads bridge audit log every 5 minutes
- Extracts text/voice commands, groups by hour
- Stores summaries to JARVIS memory system
- PM2 name: `jarvis-convo-logger`

## VPS Boot Sequence
```
VPS boots
  → systemd starts jarvis.service
  → jarvis-startup.sh
  → wait for Docker (up to 60s)
  → ensure agent-zero container running
  → wait for Agent Zero dashboard (up to 2min)
  → PM2 resurrect (restores all saved processes)
  → verify bridge/agents/watchdog online
  → start any missing processes manually
  → PM2 save
  → Telegram: "JARVIS System Boot Complete"
```

## PM2 Process List
```
jarvis-bridge        ← Telegram bridge
jarvis-agents        ← Health monitor + proactive intel
jarvis-watchdog      ← Self-healing
jarvis-convo-logger  ← Conversation memory logger
jarvis-ste           ← Self-training engine (v4)
```

