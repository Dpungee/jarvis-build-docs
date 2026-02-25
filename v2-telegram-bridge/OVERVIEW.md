# V2 — Telegram Bridge: JARVIS In Your Pocket

## What We Built
A Telegram bot that routes your messages to JARVIS (Agent Zero), with voice-to-text input, text-to-speech output, and automatic image delivery.

## Why We Built It
The Agent Zero dashboard requires a browser at a computer. You wanted to message JARVIS from your phone like a normal chat — and get voice replies.

## Architecture
```
Your Phone (Telegram)
  → Telegram Bot API
  → bridge.py (VPS host, /home/claude-mcp/)
  → Agent Zero API (http://localhost:50080)
  → JARVIS (Claude/Gemini via OpenRouter)
  → Reply back up the chain
```

## Key File
`/home/claude-mcp/bridge.py`

## PM2 Process Name
`jarvis-bridge`

## Features

### Voice Pipeline
1. Voice message received → downloaded as OGG
2. Sent to Agent Zero `/telegram_transcribe` (Whisper STT)
3. Transcribed text → sent to JARVIS
4. If you say "voice reply" / "say it" / "read that" → TTS synthesized
5. Audio sped up 1.5x (`TTS_SPEED` constant) → sent as voice note

### Image Auto-Detection
- Snapshots `/a0/usr/workdir/` before request
- After response: compares workdir, finds new image files
- Also scans JARVIS text response for file paths (.png/.jpg/.webp etc.)
- `docker cp` pulls images out of container → sent as Telegram photos automatically

### Context Persistence
Each Telegram user gets a conversation context UUID. JARVIS remembers the session. `/reset` clears it.

## Commands
| Command | What It Does |
|---------|-------------|
| /start | Status — confirms JARVIS is online |
| /reset | Clear conversation context, fresh start |
| Any text | Goes directly to JARVIS |
| Any voice | Transcribed → JARVIS |

## Security
`AUTHORIZED_USERS = {6994984137}` — locked to your Telegram user ID only. All others get "Access denied." and the event is logged to the bridge audit log.

