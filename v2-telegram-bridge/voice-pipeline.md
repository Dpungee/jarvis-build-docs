# Voice Pipeline Technical Details

## Full Flow
OGG audio → base64 encode → POST to /telegram_transcribe → Whisper → text string → JARVIS → response → (optional) TTS → speed up → OGG voice note

## TTS Details
- Text response → POST to /telegram_synthesize
- Returns base64 WAV audio
- ffmpeg `atempo=1.5` filter speeds it up
- Output: OGG/Opus (Telegram-compatible voice note format)

## Speed Setting
`TTS_SPEED = 1.5` in bridge.py — change to adjust reply speed.

## Max TTS Length
First 600 characters only. Markdown and URLs stripped before synthesis.

## Voice Reply Trigger Words
"voice", "say it", "speak", "read it", "read that", "audio", "talk to me",
"say that", "read this", "speak to me", "voice reply", "voice note",
"send voice", "reply voice", "talk back"

