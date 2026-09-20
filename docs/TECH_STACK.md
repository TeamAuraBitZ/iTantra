# Technology Stack

| Purpose | Technology | Reason to Choose |
|---|---|---|
| Voice Activity Detection | **Silero VAD (ONNX Runtime)** | Open-source, tiny (~1MB), near-zero idle CPU usage |
| Speech to Text (10 languages) | **AI4Bharat IndicConformer** (fine-tuned, TFLite INT8) | Best open WER for Indian languages; TFLite-exportable |
| Text to Speech (10 languages) | **AI4Bharat Indic-TTS** (fine-tuned, TFLite INT8) | Open-source, multilingual, RTF < 1 on mobile |
| Model Compression | **TensorFlow Lite (INT8 Quantization)** | ~4x smaller, 2–3x faster on low/mid-range CPUs |
| Wireless Transport | **WiFi Direct + BLE** (Android Nearby Connections) | Handles discovery/handshake, fully offline device-to-device |
| CPU / Compute Optimization | **NNAPI Delegate (Android)** | Offloads inference to on-device DSP/NPU where available; since models are already small post-quantization, no complex memory-offloading scheme is needed |
| App Framework | **Kotlin + Android SDK** | Native performance, direct mic/audio access |
| Alert Playback | **AudioFocus API** (`STREAM_ALARM`, `AUDIOFOCUS_GAIN_TRANSIENT_EXCLUSIVE`) | Guarantees non-interruptible, max-volume playback for distress alerts |
| Normal Playback | **AudioTrack** (`STREAM_MUSIC`) | Standard voice-note style playback |
| Fallback Communication | **Telephony / VoIP APIs** | When push-to-talk is off, device behaves as a normal phone |
| Packet Format | **Custom JSON / Protobuf** | Lightweight payload: `{ text, language, alert_flag }` |

## Why NOT the following (common pitfalls)

| Rejected Option | Why Rejected |
|---|---|
| Cloud STT/TTS APIs (Google Cloud Speech, AWS Transcribe, etc.) | PS explicitly bans internet-hosted API solutions — must be fully offline |
| Proprietary voice-activation SDKs | PS explicitly bans closed-source/commercial SDKs |
| Whisper (large/medium) for STT | Too large for low/mid-range phones even after quantization; WER is not necessarily better than IndicConformer for Indic languages specifically |
| LLM-style memory offloading (e.g. MoE expert paging techniques) | Designed for multi-billion-parameter models; irrelevant here since STT/TTS/VAD models are already only tens of MBs post-quantization and fit fully in RAM |
| Raw audio transmission | Defeats the entire purpose of the PS — audio is too data-heavy for low-bitrate links; this is precisely the problem the text-relay approach solves |
