# Proposed application contracts

These are design interfaces, not existing Brilliant SDK method names.

```text
HaloDevicePort
  connect() / disconnect()
  events: connected | disconnected | tap | button | audio_chunk | capture_error
  show(Card { requestId, title, lines, page, pageCount, state })
  startAudioCapture(maxDuration) / stopAudioCapture()
  playAudio(bytes, codec)

AssistantPort
  ask({ requestId, audio, locale, context? }) -> Answer
  cancel(requestId)

Answer
  { requestId, transcript, shortText, spokenText?, sources?, generatedAt }
```

Gateway sketch: authenticated `POST /v1/questions` with multipart audio, request ID and locale. Return an answer with the matching ID. Reject oversized audio, unsupported MIME types, unauthorized calls and duplicate requests. Avoid logging audio/transcripts by default. Set wire format and streaming details during implementation.

| Current | Event | Next |
| --- | --- | --- |
| Disconnected | BLE connected | Idle |
| Idle | Deliberate activation | Listening |
| Listening | Capture complete | Processing |
| Listening or Processing | Cancel/disconnect/timeout | Idle or Disconnected |
| Processing | Matching answer ID | Presenting |
| Processing | Error | Error |
| Presenting or Error | Dismiss/new request | Idle or Listening |

Drop late or mismatched answers. Camera content requires a separate action and consent gate.
