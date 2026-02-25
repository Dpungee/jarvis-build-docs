# V1 — Foundation: Agent Zero + JARVIS Mode + Skill System

## What We Built
The foundation of everything. Installed Agent Zero on a Hostinger VPS and transformed it from a generic AI agent into JARVIS — a personal AI with persistent memory and self-learning capabilities.

## Why We Built It
Before this, AI assistants were stateless — every conversation started from zero. You wanted an AI that:
- Remembered what it had done before
- Got smarter over time without being retrained
- Could actually run code, access the internet, manage your server
- Survived model changes (so switching from expensive to cheap model didn't lose all knowledge)

## The Key Breakthrough
The **skill file system**. If you make the AI write detailed documentation of every task it completes — with exact commands, gotchas, and step-by-step procedures — then even a cheap dumb model can follow those procedures later. The expensive model does the thinking once. The cheap model executes forever.

## The Problem With Model Differences
Gemini Flash struggled with complex multi-step tasks (Docker networking, nginx config) — it would get confused mid-task, forget what it was doing, or skip steps. Claude Sonnet 4.5 could handle these reliably. The solution: use Sonnet for training sessions that produce detailed skill files, then let Flash follow the skill files.

## Core Components

### Agent Zero Framework
- Installed in Docker container on VPS
- Port 50080 internally (not exposed externally without nginx proxy)
- Has built-in: code execution, web browsing, memory system, file management
- Model configured via Settings panel in the web dashboard

### JARVIS Mode Skill
The first skill we built manually. Located at `/a0/prompts/agent.system.main.role.md`. Transforms Agent Zero's personality/behavior into JARVIS.

### Auto-Learning Rule
Built into the system prompt: after every completed task, JARVIS must save a skill file at `/a0/usr/skills/jarvis-learned/[task-name]/SKILL.md` with this structure:
- When To Use
- Key Commands
- Patterns & Gotchas
- Step-by-Step Procedure

### Skill Storage Location
```
/a0/usr/skills/jarvis-learned/
├── docker/
├── github-repository-creation/
├── deployment-checklist/
├── mission-control-dashboard/
└── ... (grows over time)
```

## Key Lessons Learned

**Docker port exposure is impossible from inside a running container.** If a service needs external access, you must modify `docker-compose.yml` on the HOST, then recreate the container. Alternative: use nginx reverse proxy on host to forward traffic in.

**systemd does not work inside Docker containers.** Use PM2, nohup, or background processes (`&`) instead.

**Model IDs in OpenRouter must be exact.** Format: `anthropic/claude-sonnet-4.5` — longer version strings don't work.

**Agent Zero's Settings panel requires a new chat session** to apply model changes. Changing model mid-conversation doesn't take effect.

## Files Created In V1
| File | Location | Purpose |
|------|----------|---------|
| JARVIS role prompt | `/a0/prompts/agent.system.main.role.md` | Core personality/behavior |
| Skill learning rule | Inside system prompt | Forces skill file creation after tasks |
| Skills directory | `/a0/usr/skills/jarvis-learned/` | Where all learned skills live |

