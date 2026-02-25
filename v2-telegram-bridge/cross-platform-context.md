# Cross-Platform Context System (v2 upgrade)

## The Problem
Telegram and the Agent Zero dashboard were completely separate.
- Context IDs lived only in bridge.py memory — wiped on every restart
- Dashboard conversations had no connection to Telegram conversations
- JARVIS had no idea what was happening in the other interface
- You had to repeat yourself constantly when switching between them

## What We Built
A shared SQLite database (`/home/claude-mcp/jarvis-context.db`) that both
interfaces read and write. JARVIS is now one continuous mind.

## Three Core Pieces

### 1. jarvis_context.py — Shared State Manager
Every thread (conversation) is a row in the DB with:
- `id` — the Agent Zero context UUID (persists across bridge restarts)
- `title` — auto-set from your first message
- `status` — active / paused / background / closed
- `source` — telegram or dashboard
- `last_msg`, `last_reply` — for quick previews

### 2. Handoff Context Block
Every message to JARVIS now starts with a context injection:
```
[JARVIS CONTEXT — Cross-platform state]
CURRENT THREAD: Deploy the auth system
  Started: 2026-02-25 | Source: telegram | Messages: 14
  Last user message: Make sure the tests pass before deploying

BACKGROUND TASKS (1):
  [a3f91c2b] Build the dashboard API — last updated 2026-02-25 16:30
[END CONTEXT — Respond naturally, reference threads if relevant]
```
JARVIS knows what's active before you say a word.

### 3. Multi-Thread Commands (Telegram)
| Command | What It Does |
|---------|-------------|
| /threads | See all active threads with status |
| /new | Start a new thread, push current to background |
| /bg | Send current to background (JARVIS keeps working) |
| /switch \<id\> | Jump to a different thread |
| /resume \<id\> | Resume a paused/background thread |
| /reset | Close current thread, start fresh |

## How The "Human-Like" Multi-tasking Works
1. You're discussing project X with JARVIS in Telegram
2. You say "go deploy that in the background" → `/bg`
3. Current thread moves to `background` status
4. New thread created, you're now talking freely
5. JARVIS's context block shows the background task
6. When done, JARVIS tells you — or you `/switch` back to check

## Files
| File | Purpose |
|------|---------|
| /home/claude-mcp/jarvis_context.py | Full context manager library |
| /home/claude-mcp/jarvis-context.db | SQLite state database |
| /home/claude-mcp/bridge.py | Updated to use context system |

