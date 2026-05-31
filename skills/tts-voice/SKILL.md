---
name: tts-voice
description: "Text-to-speech — convert text to audio for voice messages, stories, and narrations."
---

# TTS Voice

Convert text to audio using ElevenLabs or built-in TTS providers.

## Usage

```json
{"text": "Text to speak", "channel": "optional_channel_hint", "timeoutMs": 30000}
```

- Audio is auto-delivered from tool result
- After success, follow reply instructions — no duplicate text/audio

## When to Use

- Voice messages (explicit voice/speech/TTS intent)
- Stories and narrations
- Movie/book summaries as "storytime"
- Multi-character dialog with different voices

## When NOT to Use

- Ordinary text replies (just type the response)
- Status updates
- Data reports

## Tips

- Use expressive language for better voice output
- Add pauses with punctuation (..., —, etc.)
- For stories, consider using funny/dramatic voices
- Audio delivery is automatic — no need to send separately
