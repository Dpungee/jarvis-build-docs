# V4 — Self-Training Engine: JARVIS That Gets Smarter 24/7

## What We Built
A background AI system running 4 continuous learning modules using Gemini Flash, making JARVIS smarter without any manual effort from you.

## Why We Built It
Every conversation contained useful information — patterns, preferences, project details — that got lost because nothing was extracting and storing it. Also wanted JARVIS's knowledge to grow even when you weren't actively talking to him.

## The Core Insight
Gemini Flash costs ~$0.001/call. Running it 200+ times per day = less than $0.50. That's an AI working for you 24/7 for less than the cost of a coffee.

## The 4 Modules

### Module 1: Memory Miner (every 10 min)
Reads conversation history from bridge audit log + dashboard HTML logs. Gemini Flash extracts:
- Facts, preferences, decisions, goals, projects, observations
- Stored in JARVIS memory with importance scores

Example: You mention "deploy before Friday" → stored as `[goal] Deploy before Friday, importance: 7`

### Module 2: Skill Auditor (every 1 hour)
Reads each learned skill file, has Gemini Flash rate it:
- Quality score 1-10
- Status: good / needs_fix / broken / outdated
- Issues and suggestions saved to `/tmp/jarvis-ste/skill_audits.jsonl`
- Broken skills flagged in memory so JARVIS knows to be careful

### Module 3: Knowledge Builder (every 30 min)
- Looks at recent memories + active projects
- Identifies a knowledge gap
- Researches it with Gemini Flash
- Stores 3-8 facts as memory entries
- JARVIS knows the answer before you even ask

### Module 4: Pattern Optimizer (every 2 hours)
- Reads JARVIS feedback/effectiveness data
- Identifies recurring errors and high-performing approaches
- Stores optimization recommendations as memories

## Daily Training Report
Sent to Telegram at 9pm EST (2am UTC):
- Conversations mined, memories created, skills audited, knowledge entries, API calls

## Key File
`/home/claude-mcp/self_training_engine.py`

## State Files
| File | Purpose |
|------|---------|
| /tmp/jarvis-ste/state.json | Current counters + timestamps |
| /tmp/jarvis-ste/skill_audits.jsonl | Skill audit history |
| /tmp/jarvis-intel/cost_history.jsonl | OpenRouter spend over time |
| /tmp/jarvis-intel/disk_history.jsonl | Disk usage trend |

