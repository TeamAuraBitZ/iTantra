# Research References

Every core technical choice in this architecture is grounded in a published paper or an established open-source release. Cite these directly in the SIH presentation / report for credibility.

## Speech Recognition (STT)

**[1] Conformer: Convolution-augmented Transformer for Speech Recognition**
Gulati, A., Qin, J., Chiu, C-C., et al. — Interspeech 2020
https://arxiv.org/abs/2005.08100
> The base architecture underlying AI4Bharat's IndicConformer. Combines convolution and self-attention for state-of-the-art ASR accuracy with reasonable compute cost — the reason Conformer-based models are viable for mobile deployment.

**[2] Vistaar: Diverse Benchmarks and Training Sets for Indian Language ASR**
Bhogale, K. S., Sundaresan, S., Raman, A., Javed, T., Khapra, M. M., Kumar, P. — Interspeech 2023
https://arxiv.org/abs/2305.15948
> Defines the benchmark and training methodology used to train/evaluate IndicConformer across Indian languages. Directly relevant to justifying WER claims.

**[3] CLSRIL-23: Cross Lingual Speech Representations for Indic Languages**
Gupta, A., Chadha, H. S., Shah, P., Chimmwal, N., Dhuriya, A., Gaur, R., Raghavan, V. — 2021
https://arxiv.org/abs/2107.07402
> Cross-lingual speech representation learning across Indic languages — foundational to why a single multilingual model generalizes across the 10 target languages.

## Speech Synthesis (TTS)

**[4] Text-to-Speech for Languages of India: Databases and Models (Indic-TTS)**
AI4Bharat team — Accepted at ICASSP 2023
https://arxiv.org/abs/2211.09536
> The exact paper describing the FastPitch + HiFi-GAN architecture used in AI4Bharat Indic-TTS, including evaluation of acoustic models, vocoders, and training schedules across Dravidian and Indo-Aryan languages.

## Model Compression / On-Device Efficiency

**[5] Quantization and Training of Neural Networks for Efficient Integer-Arithmetic-Only Inference**
Jacob, B., Kligys, S., Chen, B., et al. — Google, CVPR 2018
https://arxiv.org/abs/1712.05877
> Foundational paper for INT8 quantization — the exact scheme TensorFlow Lite's post-training quantization implements. Directly justifies the "Model Compression" row in the tech stack.

**[6] MobileNetV2: Inverted Residuals and Linear Bottlenecks**
Sandler, M., Howard, A., Zhu, M., Zhmoginov, A., Chen, L-C. — Google, CVPR 2018
https://arxiv.org/abs/1801.04381
> Classic reference for efficient, low-power neural network design on mobile hardware — useful to justify the overall "on-device, low/mid-range phone" design philosophy.

## Voice Activity Detection

**Silero VAD** (open-source project, no formal peer-reviewed paper)
https://github.com/snakers4/silero-vad
> Pretrained, language-agnostic VAD model, ONNX-exportable, ~1MB. Used as-is without fine-tuning since VAD is not language-specific.

## Model / Code Repositories

| Resource | Link |
|---|---|
| IndicConformer (Hugging Face) | https://huggingface.co/ai4bharat/indic-conformer-600m-multilingual |
| Indic-TTS (GitHub) | https://github.com/AI4Bharat/Indic-TTS |
| Silero VAD (GitHub) | https://github.com/snakers4/silero-vad |

## How to Cite in the Presentation

> "Our STT module (IndicConformer) is built on the Conformer architecture [Gulati et al., 2020] and trained per the Vistaar benchmark methodology [Bhogale et al., 2023]. Our TTS module uses AI4Bharat's Indic-TTS [ICASSP 2023]. Model compression follows Google's integer-only quantization scheme [Jacob et al., 2018], enabling deployment on low/mid-range Android hardware."
