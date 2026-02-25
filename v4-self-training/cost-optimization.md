# Cost Optimization Strategy

## The Core Model Strategy

### Claude Sonnet 4.5 — Training Mode
Use for: complex multi-step tasks, writing new skills, debugging hard problems, anything Gemini Flash fails at.
Cost: ~$3/M input tokens, ~$15/M output tokens

### Gemini Flash 2.0 — Execution Mode
Use for: STE background tasks, following documented procedures, simple pattern extraction, high-volume low-complexity work.
Cost: ~$0.10/M input, ~$0.40/M output (30-100x cheaper than Sonnet)

## Why This Works
Gemini Flash is dumb but obedient. Give it a clear procedure written by a smart model and it follows it reliably. The expensive model's intelligence is "compiled" into the skill file. The cheap model executes.

```
Is this task in a documented skill file?
  YES → Gemini Flash (follow the procedure)
  NO  → Is it complex/multi-step?
    YES → Claude Sonnet (execute + write skill file after)
    NO  → Either works, use Flash to save money
```

## STE Daily Cost Breakdown
| Module | Calls/Day | Est. Cost/Day |
|--------|-----------|--------------|
| Memory Miner (10min) | ~144 | ~$0.08 |
| Knowledge Builder (30min) | ~48 | ~$0.10 |
| Skill Auditor (1hr) | ~24 | ~$0.07 |
| Pattern Optimizer (2hr) | ~12 | ~$0.05 |
| **Total STE** | **~228** | **~$0.30-0.50** |

## ⚠️ Set A Spending Limit
OpenRouter limit is currently NULL (unlimited). Set one at openrouter.ai:
- Suggested daily: $2
- Suggested monthly: $30

## Model ID Reference (OpenRouter)
| Model | OpenRouter ID |
|-------|-------------|
| Claude Sonnet 4.5 | anthropic/claude-sonnet-4.5 |
| Claude Haiku 4.5 | anthropic/claude-haiku-4.5 |
| Gemini 2.0 Flash | google/gemini-2.0-flash-001 |

## Change STE Model
In `/home/claude-mcp/self_training_engine.py`:
```python
MODEL = "google/gemini-2.0-flash-001"  # Change this line
```

