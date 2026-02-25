# PM2 Process Management

## View Status
```bash
pm2 list
pm2 status
```

## Logs
```bash
pm2 logs jarvis-bridge       # Telegram bridge
pm2 logs jarvis-agents       # Health monitor
pm2 logs jarvis-watchdog     # Watchdog
pm2 logs jarvis-ste          # Self-training engine
pm2 logs --lines 100         # All, last 100 lines
```

## Control
```bash
pm2 restart jarvis-bridge
pm2 restart all
pm2 stop jarvis-bridge
pm2 delete jarvis-bridge
```

## Start A Process
```bash
cd /home/claude-mcp
pm2 start bridge.py --name jarvis-bridge --interpreter python3
pm2 start background_agents.py --name jarvis-agents --interpreter python3
pm2 start watchdog.py --name jarvis-watchdog --interpreter python3
pm2 start convo_logger.py --name jarvis-convo-logger --interpreter python3
pm2 start self_training_engine.py --name jarvis-ste --interpreter python3
pm2 save  # ← always save after changes
```

## PM2 Environment (Required)
```bash
export HOME=/home/claude-mcp
export PATH=/home/claude-mcp/.npm-global/bin:/usr/local/bin:/usr/bin:/bin:$PATH
```

## Full Restart From Scratch
```bash
pm2 delete all
# then start each process as above
pm2 save
```

