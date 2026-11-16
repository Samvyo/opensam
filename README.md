# opensam

Open-source building blocks for real-time video and voice AI: a pure-mesh WebRTC
call, a mediasoup SFU conference, and an AI participant that joins the call.
Each one builds on the last, and each runs on your own machine with Docker Compose.

Free to read, run and change under the [MIT licence](LICENSE).

## Projects

### 1. `full-mesh` — Peer-to-peer WebRTC calling

A real-time multi-user video calling app built on a pure WebRTC mesh, where every
participant connects directly to every other participant (no media server in the
path). Node.js + WebSocket signalling, React UI, and a coturn TURN relay.

- Video/audio calls for up to 4 users, mute/unmute, camera toggle, screen sharing
- In-call chat, full-call recording (`.webm`), connection-quality indicator
- JWT-authenticated room access
- Simplest architecture; best for small rooms.

See [full-mesh/README.md](full-mesh/README.md).

### 2. `mediasoup` — SFU-based conferencing

The same experience re-architected on a **mediasoup SFU**: clients upload their
media once and the server forwards it to everyone else, cutting client CPU and
bandwidth and scaling far better than a mesh.

- Multi-user conferencing, mute/camera/screen-share, DataChannel chat, client-side recording
- JWT auth, per-peer signalling rate limiting, graceful shutdown
- Redis persistence, Prometheus + Grafana monitoring
- Best for larger rooms.

See [mediasoup/README.md](mediasoup/README.md).

### 3. `v2ai` — AI meeting participant

An AI participant that joins a live mediasoup conference, listens, thinks, and
speaks in real time. It pulls RTP audio (and VP8 video) off a mediasoup plain
transport and runs it through STT → LLM → TTS and vision pipelines.

- Wake-word detection and Silero Voice Activity Detection (VAD)
- Speech-to-Text: Deepgram (primary), Whisper (fallback)
- Context-aware conversation with Anthropic Claude, with PII scrubbing before the LLM
- Meeting summaries, action-item extraction, decision tracking, and meeting Q&A
- Consent-gated screen-share analysis and slide summarization via Claude vision (LLaVA local fallback)
- Multi-provider Text-to-Speech: Cartesia / Deepgram / Kokoro
- OpenTelemetry tracing, Docker-based deployment

You bring your own API keys for the speech and language models.
See [v2ai/README.md](v2ai/README.md).

## Getting started

You need Docker with Docker Compose. Clone the repository, open the folder for
the project you want to run, and follow its README:

```bash
git clone https://github.com/Samvyo/opensam.git
cd opensam/full-mesh        # or mediasoup, or v2ai
docker compose up --build
```

| Project | Folder | Best for |
| --- | --- | --- |
| Full-mesh WebRTC | [`full-mesh`](full-mesh/) | Small peer-to-peer rooms |
| mediasoup SFU | [`mediasoup`](mediasoup/) | Larger, scalable conferences |
| AI meeting participant | [`v2ai`](v2ai/) | Adding an AI participant to a conference |

The `certs/` folders hold a self-signed `localhost` certificate so the browser
apps run over HTTPS on your machine. They are for local development only; never
use them for a deployment anyone else can reach.

## Contributing

Bug reports, fixes and improvements are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md)
before you open an issue or a pull request.

## Licence

[MIT](LICENSE).
