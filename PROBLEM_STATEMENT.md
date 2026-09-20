# Problem Statement — SIH26173

| Field | Value |
|---|---|
| **Problem Statement ID** | 26173 |
| **Title** | iTantra — Indian Multilingual TTS & STT Aided Neural Transceiver Radio Access for Low Bitrate Links |
| **Organisation** | Indian Space Research Organisation (ISRO) |
| **Department** | Department of Space |
| **Category** | Software |
| **Theme** | Smart Automation |
| **Idea submission deadline** | 20 September 2026 |

## Background

Vocal audio information is very data-intensive, making it difficult to transmit through low-data-rate links. In alert and distress-based scenarios, transmitting audio information is critical, as it is more inclusive and caters to everyone — even if they are not literate — unlike a written message.

## Description

Build an Android app with lightweight, highly accurate STT and TTS models for 10 Indian languages (Hindi, Gujarati, Marathi, Kannada, Malayalam, Tamil, Telugu, Odia, Bengali, English) that runs **locally on a low-power device**.

- The **STT module**, when activated, detects pauses/stoppages, forms the sentence detected, and instantly and efficiently streams the data through WiFi/Bluetooth to a connected embedded device or another phone running the same app, with minimal latency.
- The **TTS module**, when activated after receiving text data, converts it into intelligible speech, played as a voice note; alert-type messages are announced at highest volume, non-interruptible.
- To verify the complete loop: two phones with the same app — one in TTS mode, one in STT mode — connected via WiFi/Bluetooth, should work like a walkie-talkie using a push-to-talk feature. If turned off, the phone should work like a normal phone.

## Key Evaluation Metrics

| Metric | Weight | Details |
|---|---|---|
| **Efficiency** | 20% | Model size, app size (RAM/Flash footprint), CPU usage during idle listening |
| **Accuracy** | 40% | Low Word Error Rate (WER) for STT, high human legibility and natural flow for TTS |
| **Latency** | 20% | Time delay: speech → STT completion; text received → audio played (TTS) + RTF (Real-Time Factor); end-to-end delta between sentence spoken and audio started on the receiving phone |

## Software & Framework Restrictions

- **Open-source only** — no proprietary/closed-source/commercial voice-activation SDKs
- **Allowed frameworks** — TensorFlow Lite for Microcontrollers, PyTorch Mobile, or similar
- **Fully offline** — no internet-hosted API-based solutions for STT or TTS

## Hardware & Runtime Environment

The Android application must run smoothly on **low and mid-range mobile phones**.
