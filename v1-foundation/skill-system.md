# The JARVIS Skill System

## Concept
JARVIS automatically creates documentation files after completing any significant task. This documentation becomes reusable "skills" that any model can follow.

## Why This Works
AI models are stateless — they forget everything between conversations. But the file system persists. By forcing JARVIS to write detailed notes about what he just did, that knowledge outlives the conversation, the model, and even container restarts.

## Skill File Format
Every skill lives in its own folder: `/a0/usr/skills/jarvis-learned/[skill-name]/SKILL.md`

```markdown
# Skill: [Name]

## When To Use
[Trigger conditions]

## Key Commands
[Most important commands, exact syntax]

## Patterns & Gotchas
[Things that break, common mistakes]

## Step-By-Step Procedure
1. [Exact step]
2. [Exact step]

## Example
[Concrete example]
```

## How To Read A Skill
```bash
docker exec agent-zero cat /a0/usr/skills/jarvis-learned/docker/SKILL.md
```

## How To List All Skills
```bash
docker exec agent-zero ls /a0/usr/skills/jarvis-learned/
```

