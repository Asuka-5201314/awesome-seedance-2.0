# 🎬 Awesome Seedance 2.0 — ByteDance's Cinema-Grade Video Model with Portrait Library

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Seedance 2.0](https://img.shields.io/badge/Seedance-2.0-blue.svg)](https://www.atlascloud.ai/models/bytedance/seedance-2.0/text-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0)
[![Try on Atlas Cloud](https://img.shields.io/badge/Try-Atlas%20Cloud-green.svg)](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

**Language / 语言:** English | [中文](README_zh.md) | [日本語](README_ja.md) | [한국어](README_ko.md)

---

> 🔥 **Seedance 2.0** — ByteDance's flagship video model built on **Diffusion Transformer (DiT)**. Overall score **8.2/10** (ahead of Veo 3, Wan, Kling). Features Portrait Library for real faces, native 2K, audio-video joint generation, voice cloning, web search, and 12-input multimodal control. **$0.10/request on Atlas Cloud.**

---

## Table of Contents

- [What's New in Seedance 2.0?](#whats-new-in-seedance-20)
- [Benchmarks & Rankings](#-benchmarks--rankings)
- [Portrait Library — Real Face Support](#-portrait-library--real-face-support)
- [Core Features Deep Dive](#-core-features-deep-dive)
- [Models on Atlas Cloud](#-models-on-atlas-cloud)
- [API Quick Start](#-api-quick-start)
- [Portrait Library API](#-portrait-library-api)
- [Seedance 2.0 vs Competitors](#-seedance-20-vs-competitors)
- [Seedance 2.0 vs 1.5 Pro](#-seedance-20-vs-15-pro)
- [Use Cases](#-use-cases)
- [Resources](#-resources)
- [FAQ](#faq)

---

## What's New in Seedance 2.0?

Released **February 12, 2026** by ByteDance, Seedance 2.0 represents a generational leap in video AI:

- **Architecture**: Diffusion Transformer (DiT) — replacing U-Net for better scalability
- **Unified multimodal**: Audio-video joint generation from text, images, video, and audio
- **Native 2K**: 2048×1080 (landscape) / 1080×2048 (portrait) — up from 1080p
- **Portrait Library**: First major model with dedicated real-face asset management
- **Voice cloning**: Up to 3 custom character voices per scene
- **Web search**: Real-time internet references during generation
- **CapCut integration**: Globally available via CapCut (March 26, 2026)
- **Internal benchmark**: SeedVideoBench-2.0 covering instruction compliance, motion quality, aesthetics, and audio

---

## 📊 Benchmarks & Rankings

### Artificial Analysis Leaderboard

| Metric | Score | Ranking |
|--------|-------|---------|
| **Text-to-Video Elo** | 1,273 | Top 3 (720p) |
| **Image-to-Video Elo** | 1,355 | Top 3 (720p) |
| **Overall Score** | **8.2/10** | #1 at launch |
| **Camera Control** | **9/10** | #1 (all models) |
| **Creative Control** | 5/5 | Top tier |
| **Audio Synchronization** | 5/5 | Top tier |

### Comparison Scores

| Model | Overall | Camera | Audio |
|-------|---------|--------|-------|
| **Seedance 2.0** | **8.2** | **9/10** | **5/5** |
| Google Veo 3 | 7.0 | 7/10 | 5/5 |
| Alibaba Wan 2.2 | 5.6 | — | — |
| Kuaishou Kling 2.1 | 4.4 | — | — |

> Seedance 2.0 has been included in **VBench-2.0** alongside Veo 3, Vidu, Wan, and Kling.

---

## 🎭 Portrait Library — Real Face Support

### The Problem
Seedance 2.0 **blocks real-face images submitted through standard input** for safety compliance. You can't just paste a photo of a real person.

### The Solution: Portrait Library
A dedicated asset management system where you:

1. **Register** a portrait image → preprocessed and validated
2. **Wait** for status: `Processing → Active`
3. **Reference** via `asset://<asset_id>` in any image field
4. The model generates video with **identity-consistent** results

### Image Requirements

| Spec | Value |
|------|-------|
| Formats | JPEG, PNG, WebP, BMP, TIFF, GIF, HEIC |
| Dimensions | 300 – 6,000 px per side |
| Aspect ratio | 0.4 – 2.5 |
| Max size | 30 MB |

### Using in Playground

1. Open **Portrait Library** in the image input area
2. **Upload** portrait and wait for preprocessing
3. **Select** the prepared portrait → available as reference
4. Write prompt and generate!

> **Tip**: Click the **"API" tab** next to Playground for request examples and SDK snippets. Use **"Copy for LLM"** to scaffold the integration via your AI coding assistant.

---

## ✨ Core Features Deep Dive

### 🔊 Native Audio-Video Joint Generation
Single inference generates video + synchronized audio (dialogue, SFX, music). Supports automatic lip sync in Chinese, English, Spanish, and more. Stereo output.

### 🗣️ Voice Cloning
Upload real voice samples to guide tone, accent, and expression. Supports up to **3 custom character voices** per scene.

### 🌐 Web Search (Seedance 2.0 only)
Enable `web_search: true` to pull real-world references during generation. Great for specific people, locations, or styles the model hasn't seen.

### 🖼️ 12-Input Multimodal Control (@Reference System)
The `@` system lets you bind references to prompt elements:
- Up to **9 reference images** (character, style, scene)
- Up to **3 reference videos** (total ≤15s) for editing/extension
- **1 reference audio** for audio-driven generation
- Prompt: "The character in @image1 dances to @audio1 in the style of @image2"

### 🎬 Director-Level Camera Control
Control camera like a real director:
- Push/pull zoom, focus pull
- Tracking shots, POV switches
- Handheld shake effect
- Scored **9/10** on camera control (highest among all models)

### ✂️ Video Editing
- Extend existing videos
- Apply motion references
- Remove objects
- Add visual effects

### 📐 Output Specs
- **Resolution**: Native 2K (2048×1080 / 1080×2048), 720p, 480p
- **Duration**: 4-15 seconds, multi-shot with natural transitions
- **Aspect ratios**: 16:9, 4:3, 1:1, 3:4, 9:16, 21:9, adaptive
- **Last frame return**: Chain videos seamlessly

---

## 💰 Models on Atlas Cloud

| Model | ID | Price |
|-------|-----|-------|
| **Text-to-Video** | `bytedance/seedance-2.0/text-to-video` | $0.10/req |
| **Image-to-Video** | `bytedance/seedance-2.0/image-to-video` | $0.10/req |
| **Reference-to-Video** | `bytedance/seedance-2.0/reference-to-video` | $0.10/req |
| **Fast T2V** | `bytedance/seedance-2.0-fast/text-to-video` | $0.10/req |
| **Fast I2V** | `bytedance/seedance-2.0-fast/image-to-video` | $0.10/req |
| **Fast Ref2V** | `bytedance/seedance-2.0-fast/reference-to-video` | $0.10/req |

> Fast models generate 5-10s video in 30-60 seconds (vs minutes for standard). ~33% cheaper on other platforms, same price on Atlas Cloud.

---

## ⚡ API Quick Start

### Text-to-Video (Python)

```python
import requests, time

API_KEY = "your-atlas-cloud-api-key"
H = {"Authorization": f"Bearer {API_KEY}", "Content-Type": "application/json"}

r = requests.post("https://api.atlascloud.ai/api/v1/model/prediction", headers=H, json={
    "model": "bytedance/seedance-2.0/text-to-video",
    "prompt": "A young filmmaker reviews footage on a vintage monitor, warm studio lighting, cinematic grain",
    "duration": 10,
    "resolution": "720p",
    "ratio": "16:9",
    "generate_audio": True,
    "web_search": False
})
pid = r.json()["data"]["id"]

while True:
    res = requests.get(f"https://api.atlascloud.ai/api/v1/model/prediction/{pid}", headers=H).json()
    if res["data"]["status"] in ("completed", "succeeded"):
        print("Video:", res["data"]["outputs"][0])
        break
    elif res["data"]["status"] == "failed":
        print("Error:", res["data"].get("error"))
        break
    time.sleep(5)
```

### Portrait Reference-to-Video

```python
# After registering portrait in Portrait Library (asset_id = "ark-xxxxx")
r = requests.post("https://api.atlascloud.ai/api/v1/model/prediction", headers=H, json={
    "model": "bytedance/seedance-2.0/reference-to-video",
    "reference_images": ["asset://ark-xxxxx"],
    "prompt": "The person in image 1 delivers a TED talk, confident gestures, audience applause",
    "duration": 12,
    "generate_audio": True
})
```

### Image-to-Video (cURL)

```bash
curl -X POST "https://api.atlascloud.ai/api/v1/model/prediction" \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "bytedance/seedance-2.0/image-to-video",
    "image": "https://example.com/first-frame.jpg",
    "prompt": "Camera slowly pushes in, soft particles drift through warm light",
    "duration": 8,
    "generate_audio": true,
    "ratio": "adaptive"
  }'
```

> 💡 **[Get your API key at Atlas Cloud](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0) — free credits, no credit card!**

---

## 🔧 Portrait Library API

**Base URL**: `https://console.atlascloud.ai/api/v1`

| Method | Path | Description |
|--------|------|-------------|
| POST | `/sd/assets` | Create portrait from image URL |
| GET | `/sd/assets/:id` | Get asset (auto-polls when Processing) |
| GET | `/sd/assets` | List assets (paginated, filterable) |
| PUT | `/sd/assets/:id` | Rename asset |
| DELETE | `/sd/assets/:id` | Move to trash (recoverable) |
| GET | `/sd/assets/trash` | List trashed assets |
| POST | `/sd/assets/:id/restore` | Restore from trash |

**Error codes**: 200 (success), 400 (invalid request), 401 (auth error), 404 (not found), 500 (server error)

---

## 📊 Seedance 2.0 vs Competitors

| Feature | Seedance 2.0 | Kling 3.0 | Sora 2 | Veo 3.1 | Wan 2.7 |
|---------|-------------|-----------|--------|---------|---------|
| **Architecture** | DiT | — | DiT | — | DiT |
| **Overall Score** | **8.2/10** | 8.1/10 | — | 7.0/10 | — |
| **Portrait Library** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **Native Audio** | ✅ | ❌ | ✅ | ✅ | ✅ |
| **Voice Cloning** | ✅ (3 voices) | ❌ | ❌ | ❌ | ✅ |
| **Web Search** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **Max Resolution** | **2K** | 4K/60fps | 1080p | 4K | 720p |
| **Max Duration** | 15s | 2min | 20s | 8s | 15s |
| **Multi-Reference** | **9 img + 3 vid** | 1 img | N/A | 1 ref | 5 refs |
| **Camera Control** | **9/10** | 8/10 | 7/10 | 7/10 | — |
| **Price (10s)** | **~$0.60** | ~$0.50 | ~$1.00 | ~$2.50 | ~$0.40 |
| **NSFW** | ❌ | ❌ | ❌ | ❌ | ✅ (Spicy) |

---

## 📊 Seedance 2.0 vs 1.5 Pro

| Feature | 2.0 | 1.5 Pro |
|---------|-----|---------|
| Architecture | DiT | Previous gen |
| Resolution | **2K native** | 1080p |
| Portrait Library | ✅ | ❌ |
| Web Search | ✅ | ❌ |
| Voice Cloning | ✅ (3 voices) | ❌ |
| Multi-Reference | 9 img + 3 vid + audio | Limited |
| Video Editing | ✅ | ❌ |
| Duration | 4-15s | 4-12s |
| Aspect Ratios | 7 + adaptive | Limited |
| Camera Control | 9/10 | Basic |
| NSFW (Spicy) | ❌ | ✅ |
| Price | $0.10/req | $0.15-0.72 |

> For NSFW: use `bytedance/seedance-v1.5-pro/image-to-video-spicy` on Atlas Cloud.

---

## 🎯 Use Cases

- 🎭 **AI Spokesperson** — register face, generate unlimited video variants
- 📱 **Social Media** — consistent AI avatar for TikTok/YouTube/Instagram
- 🎓 **Education** — virtual instructor with voice cloning across languages
- 🛒 **E-Commerce** — product demos with brand representative
- 📰 **News** — AI anchor with registered portrait asset
- 🎬 **Short Film** — consistent characters with director-level camera control
- 🎮 **Gaming** — character intros from concept art
- 🌐 **Multi-language** — same face + voice clone in different languages

---

## 📚 Resources

### Official
- 🌐 [Seedance 2.0 Official Page](https://seed.bytedance.com/en/seedance2_0)
- 📄 [Launch Blog Post](https://seed.bytedance.com/en/blog/official-launch-of-seedance-2-0)
- 📚 [Wikipedia](https://en.wikipedia.org/wiki/Seedance_2.0)
- 🎬 [CapCut Integration](https://www.capcut.com/newsroom/dreamina-seedance-2)

### Atlas Cloud
- 🚀 [Seedance 2.0 T2V](https://www.atlascloud.ai/models/bytedance/seedance-2.0/text-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0)
- 🚀 [Seedance 2.0 I2V](https://www.atlascloud.ai/models/bytedance/seedance-2.0/image-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0)
- 🚀 [Seedance 2.0 Ref2V](https://www.atlascloud.ai/models/bytedance/seedance-2.0/reference-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0)

### Reviews & Analysis
- 📰 [TechCrunch: Seedance 2.0 on CapCut](https://techcrunch.com/2026/03/26/bytedances-new-ai-video-generation-model-dreamina-seedance-2-0-comes-to-capcut/)
- 📊 [WaveSpeedAI: SD 2.0 vs Kling vs Sora vs Veo](https://wavespeed.ai/blog/posts/seedance-2-0-vs-kling-3-0-sora-2-veo-3-1-video-generation-comparison-2026/)
- 📝 [BuildFastWithAI: SD 2.0 Review](https://www.buildfastwithai.com/blogs/seedance-2-bytedance-ai-video-2026)
- 📊 [Artificial Analysis Leaderboard](https://artificialanalysis.ai/video/leaderboard/image-to-video)
- 🔬 [HuggingFace Technical Analysis](https://discuss.huggingface.co/t/seedance-2-0-technical-analysis-of-bytedances-multimodal-video-generation-model/174924)

---

## FAQ

### 1. Why can't I upload a real face photo directly?

Seedance 2.0 enforces content safety. Real-face images must go through the **Portrait Library** for preprocessing and validation. This prevents misuse while enabling legitimate face-driven content.

### 2. Is Seedance 2.0 the best video model in 2026?

It scored **8.2/10 overall** on Artificial Analysis — the highest at launch. It has the best camera control (9/10) and strongest multimodal input system (12 references). Kling 3.0 leads in visual fidelity (8.4/10) and max duration (2min).

### 3. Does it support NSFW content?

No. Seedance 2.0 enforces content safety through the Portrait Library. For uncensored content, use **Seedance 1.5 Pro Spicy** (`bytedance/seedance-v1.5-pro/image-to-video-spicy`) on Atlas Cloud.

### 4. What about the Disney copyright controversy?

On Feb 13, 2026, Disney sent a cease-and-desist to ByteDance regarding training data usage. ByteDance responded that they respect IP and will strengthen protections. Users should avoid generating content that infringes copyrights.

### 5. Standard vs Fast — when to use which?

**Fast**: 30-60s generation, good for previews and iteration. Minor quality loss on faces and high-motion scenes. **Standard**: Full quality, takes several minutes. Use for final output.

### 6. Can I chain multiple videos?

Yes! Set `return_last_frame: true` to get the last frame, then use it as the first frame of the next `image-to-video` call.

---

<div align="center">

### [👉 Try Seedance 2.0 on Atlas Cloud — $0.10/video, Free Credits 👈](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0)

**Made with ❤️ by the open-source community**

[⬆ Back to Top](#-awesome-seedance-20--bytedances-cinema-grade-video-model-with-portrait-library)

</div>
