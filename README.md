# JARVIS — Complete Build History & Documentation Vault

> "It's not about building AI. It's about building YOUR AI." — Donald

---

## 📁 Folder Structure

```
jarvis-docs/
├── README.md                          ← You are here
├── v1-foundation/                     ← The starting point
├── v2-telegram-bridge/                ← Making JARVIS accessible anywhere
├── v3-automation-stack/               ← The self-running infrastructure
├── v4-self-training/                  ← JARVIS making himself smarter
├── current-state/                     ← Live snapshot (auto-updated daily)
└── reference/                         ← Technical reference
```

---

## 🗺️ JARVIS Evolution Timeline

| Version | What Changed | Why |
|---------|-------------|-----|
| **v0** | Discovered Agent Zero | Needed autonomous AI that runs code, not just chat |
| **v1** | Agent Zero + JARVIS Mode skill + skill learning system | Persistent knowledge that survives model/session changes |
| **v2** | Telegram bridge: voice + image support | Talk to JARVIS from anywhere, not just the dashboard |
| **v3** | Full automation stack — watchdog, health monitor, cron, systemd | JARVIS kept dying when terminal closed. Needed it to run forever |
| **v4** | Self-Training Engine — 4 AI modules on Gemini Flash 24/7 | JARVIS gets smarter automatically without manual training |

---

## 🔑 Key Design Decisions

1. **Agent Zero over OpenClaw** — Workhorse for DevOps/building. OpenClaw was flashier but unstable.
2. **Skills in `/a0/usr/skills/jarvis-learned/`** — Knowledge survives model changes. Cheap models follow procedures expensive models wrote.
3. **Gemini Flash for STE, Claude Sonnet for training** — Expensive model writes the skill → cheap model follows it.
4. **PM2 not systemd for daemons** — systemd doesn't work inside Docker containers.
5. **Everything via Telegram** — Single interface. No dashboard checking needed.

---

## 📊 Cost Summary (Auto-Updated Daily)

See `current-state/real-cost-data.md` for live numbers.

| What | Cost |
|------|------|
| STE background AI (Gemini Flash) | ~$0.30–0.50/day |
| JARVIS conversations (Agent Zero) | Depends on model setting |
| Monitoring/watchdog/backups | $0 (pure Python) |

---

*This repo is auto-updated daily by the JARVIS docs-sync cron job.*
*Last updated: see git log*

