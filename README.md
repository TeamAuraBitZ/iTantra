# iTantra — Offline Multilingual Voice Communication System
### Smart India Hackathon 2026 · Problem Statement SIH26173 · Indian Space Research Organisation (ISRO)

> **Indian Multilingual TTS & STT Aided Neural Transceiver Radio Access for Low-Bitrate Links**

---

## 1. What This Is

iTantra is an Android application that lets two devices talk to each other **like a walkie-talkie**, but instead of transmitting raw audio (which is heavy and unreliable on weak/low-bandwidth links), it:

1. Converts speech to **text** on the sender's phone (on-device, offline),
2. Transmits the **text packet** over Bluetooth/WiFi Direct,
3. Converts the text back to **speech** on the receiver's phone (on-device, offline).

This makes voice-based alerts and communication possible in **low-bandwidth, no-internet, disaster/distress scenarios**, while remaining inclusive for users who cannot read/write (since the final output is still spoken audio, not just a text message).

Built entirely with **open-source, on-device ML** — no cloud APIs, no proprietary SDKs, fully functional on low/mid-range Android hardware.

---

## 2. Core Constraints (from the official PS)

| Constraint | Requirement |
|---|---|
| Languages | 10 Indian languages: Hindi, Gujarati, Marathi, Kannada, Malayalam, Tamil, Telugu, Odia, Bengali, English |
| Connectivity | Fully offline — no internet-hosted APIs allowed |
| Frameworks | Open-source only — TensorFlow Lite / PyTorch Mobile / similar |
| Hardware target | Low and mid-range Android phones |
| Evaluation | 20% Efficiency (model/app size, RAM, CPU), 40% Accuracy (WER for STT, intelligibility for TTS), 20% Latency (STT delay, TTS delay, end-to-end delta), 20% (robustness/other) |
| Mode | Push-to-talk walkie-talkie; when off, falls back to a normal phone call |

---

## 3. Repository Structure

```
iTantra-SIH26173/
├── README.md                          ← you are here
├── PROBLEM_STATEMENT.md               ← full official PS text
├── diagrams/
│   ├── 01_system_architecture.png     ← full end-to-end system diagram (Phone A ↔ Phone B)
│   ├── 02_handwritten_concept_notes.jpeg  ← original concept sketch / training flow
│   └── 03_model_dev_vs_runtime.png    ← model development vs. on-device runtime split
└── docs/
    ├── ARCHITECTURE.md                ← detailed architecture write-up (Mermaid + explanation)
    ├── TRAINING_PIPELINE.md           ← how STT/TTS models are fine-tuned & quantized
    ├── TECH_STACK.md                  ← full technology table with justifications
    └── RESEARCH_REFERENCES.md         ← every paper this design is grounded in, with links
```

---

## 4. Quick Architecture Summary

```
Phone A (Speaker)                                Phone B (Listener)
────────────────────                             ────────────────────
Mic → VAD → STT → Pack text  ──[BLE/WiFi Direct]──▶  Unpack → TTS → Speaker
```

Full detail in [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md).

---

## 5. Technology Stack (short version)

| Layer | Technology |
|---|---|
| VAD | Silero VAD (ONNX Runtime) |
| STT | AI4Bharat IndicConformer (fine-tuned, TFLite INT8) |
| TTS | AI4Bharat Indic-TTS (fine-tuned, TFLite INT8) |
| Transport | WiFi Direct + BLE (Android Nearby Connections) |
| Compute optimization | NNAPI Delegate (hardware acceleration where available) |
| App | Kotlin + Android SDK |

Full table with justifications: [`docs/TECH_STACK.md`](docs/TECH_STACK.md)

---

## 6. Team

**Problem Statement:** SIH26173 — iTantra (ISRO / Department of Space)
**Category:** Software · **Theme:** Smart Automation
**Submission deadline (idea stage):** 20 September 2026

---

## 7. License

MIT — model weights and libraries used (AI4Bharat, Silero, TFLite) retain their own respective open-source licenses; see `docs/RESEARCH_REFERENCES.md` for attribution.
