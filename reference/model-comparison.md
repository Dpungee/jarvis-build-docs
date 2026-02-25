# Model Comparison: When To Use What

## Models In Use

### Claude Sonnet 4.5 — `anthropic/claude-sonnet-4.5`
**Best for:** Complex multi-step tasks, writing skill docs, debugging, building new features
**Context:** 200,000 tokens
**Cost:** ~$3/M in, ~$15/M out

### Gemini 2.0 Flash — `google/gemini-2.0-flash-001`
**Best for:** STE background tasks, following existing skill procedures, simple extraction
**Cost:** ~$0.10/M in, ~$0.40/M out (30-100x cheaper)
**Limitation:** Struggles with complex tasks without a skill file to follow

## Decision Rule
```
Documented skill exists for this task?
  YES → Gemini Flash
  NO + complex/multi-step?
    YES → Claude Sonnet (+ write skill file when done)
    NO  → Either works, prefer Flash
```

## How To Switch Models In Agent Zero
1. Settings (gear icon) in dashboard
2. Change "Chat Model"
3. Start a NEW conversation (change doesn't apply to current chat)

## All OpenRouter Model IDs
| Model | ID |
|-------|----|
| Claude Sonnet 4.5 | anthropic/claude-sonnet-4.5 |
| Claude Haiku 4.5 | anthropic/claude-haiku-4.5 |
| Gemini 2.0 Flash | google/gemini-2.0-flash-001 |
| GPT-4o Mini | openai/gpt-4o-mini |

