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
- [Real Face Safety Review — Understanding the Content Policy](#️-real-face-safety-review--understanding-the-content-policy)
- [Portrait Library — Real Face Support](#-portrait-library--real-face-support)
- [Core Features Deep Dive](#-core-features-deep-dive)
- [Models on Atlas Cloud](#-models-on-atlas-cloud)
- [API Quick Start](#-api-quick-start)
- [Complete API Tutorial — How to Use Seedance 2.0 API](#-complete-api-tutorial--how-to-use-seedance-20-api)
- [Portrait Library API](#-portrait-library-api)
- [Seedance 2.0 Prompt Engineering Guide](#-seedance-20-prompt-engineering-guide)
- [Seedance 2.0 Tips & Tricks](#-seedance-20-tips--tricks)
- [Seedance 2.0 vs Competitors](#-seedance-20-vs-competitors)
- [Seedance 2.0 vs Kling 3.0 — Detailed Comparison](#-seedance-20-vs-kling-30--detailed-comparison)
- [Seedance 2.0 vs 1.5 Pro](#-seedance-20-vs-15-pro)
- [Migration from Seedance 1.5 to 2.0](#-migration-from-seedance-15-to-20)
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

## ⚠️ Real Face Safety Review — Understanding the Content Policy

### Why Real Faces Get Blocked

Seedance 2.0 enforces a strict **real-face content safety policy**. This is the most common issue new users encounter:

> **Any real human face submitted through the standard image input will be automatically blocked by safety review.** This applies to all endpoints — image-to-video, reference-to-video, and standard image fields.

This policy exists because:
- 🔒 **Preventing deepfake abuse** — unauthorized use of real people's likenesses
- ⚖️ **Legal compliance** — aligning with global AI safety regulations
- 🛡️ **Platform integrity** — maintaining trust in generated content
- 🔍 **Traceability** — all generated content includes invisible watermarks

### What Gets Blocked vs What's Allowed

| Input Type | Standard Input | Portrait Library |
|-----------|---------------|-----------------|
| **Real human photo** | 🚫 Blocked | ✅ Allowed (after registration) |
| **AI-generated face** | ✅ Allowed | ✅ Allowed |
| **Cartoon/anime character** | ✅ Allowed | ✅ Allowed |
| **Landscape/object photo** | ✅ Allowed | N/A |
| **Celebrity photo** | 🚫 Blocked | ⚠️ Requires consent verification |

### Common Errors When Using Real Faces

| Error | Cause | Solution |
|-------|-------|----------|
| `content_policy_violation` | Real face detected in standard image input | Register face in Portrait Library first |
| `safety_review_failed` | Image flagged during safety scan | Use a clearer, front-facing portrait |
| Asset stuck at `Processing` | Image quality below threshold | Re-upload: 300-6000px, clear face, no occlusions |
| Asset status `Failed` | Face not detectable | Ensure single face, well-lit, front-facing |
| `asset:// reference invalid` | Asset not yet Active | Wait for Processing → Active transition |
| `asset not found` | Wrong asset ID or deleted asset | Check asset list or restore from trash |

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

### Seedance 2.0 Portrait Library Tutorial

Follow these steps to get started with the Portrait Library feature:

#### Step 1: Prepare Your Portrait Image

| Spec | Value |
|------|-------|
| Formats | JPEG, PNG, WebP, BMP, TIFF, GIF, HEIC |
| Dimensions | 300 – 6,000 px per side |
| Aspect ratio | 0.4 – 2.5 |
| Max size | 30 MB |

**Best practices for portrait photos:**
- Use a well-lit, front-facing photo with a neutral background
- Ensure the face is clearly visible and not obscured by accessories
- Higher resolution images produce better identity preservation
- Avoid heavy filters or extreme color grading on the source image

#### Step 2: Upload via Playground

1. Open **Portrait Library** in the image input area
2. **Upload** portrait and wait for preprocessing
3. **Select** the prepared portrait → available as reference
4. Write prompt and generate!

#### Step 3: Upload via API

```python
import requests

API_KEY = "your-atlas-cloud-api-key"
H = {"Authorization": f"Bearer {API_KEY}", "Content-Type": "application/json"}

# Create a portrait asset
resp = requests.post("https://console.atlascloud.ai/api/v1/sd/assets", headers=H, json={
    "image_url": "https://example.com/portrait.jpg",
    "name": "My Portrait"
})
asset_id = resp.json()["data"]["id"]
print(f"Asset created: {asset_id}")
```

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

## 📘 Complete API Tutorial — How to Use Seedance 2.0 API

This step-by-step Seedance 2.0 tutorial covers everything from setup to advanced workflows.

### Step 1: Get Your API Key

1. Sign up at [Atlas Cloud](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0)
2. Navigate to **Settings → API Keys**
3. Click **Create API Key** and save it securely
4. You'll receive free credits to start experimenting immediately

### Step 2: Install Dependencies

```bash
pip install requests python-dotenv
```

Create a `.env` file:

```
ATLASCLOUD_API_KEY=your-api-key-here
```

### Step 3: Build a Reusable Client

```python
import requests
import time
import os
from dotenv import load_dotenv

load_dotenv()

class SeedanceClient:
    """Seedance 2.0 API client for Atlas Cloud."""
    
    BASE_URL = "https://api.atlascloud.ai/api/v1/model/prediction"
    PORTRAIT_URL = "https://console.atlascloud.ai/api/v1/sd/assets"
    
    def __init__(self):
        self.api_key = os.getenv("ATLASCLOUD_API_KEY")
        self.headers = {
            "Authorization": f"Bearer {self.api_key}",
            "Content-Type": "application/json"
        }
    
    def text_to_video(self, prompt, duration=10, resolution="720p", 
                      ratio="16:9", audio=True, web_search=False):
        """Generate video from text prompt."""
        payload = {
            "model": "bytedance/seedance-2.0/text-to-video",
            "prompt": prompt,
            "duration": duration,
            "resolution": resolution,
            "ratio": ratio,
            "generate_audio": audio,
            "web_search": web_search
        }
        return self._submit_and_poll(payload)
    
    def image_to_video(self, image_url, prompt, duration=8,
                       ratio="adaptive", audio=True):
        """Animate a still image into video."""
        payload = {
            "model": "bytedance/seedance-2.0/image-to-video",
            "image": image_url,
            "prompt": prompt,
            "duration": duration,
            "ratio": ratio,
            "generate_audio": audio
        }
        return self._submit_and_poll(payload)
    
    def reference_to_video(self, reference_images, prompt, 
                           duration=10, audio=True):
        """Generate video using portrait references."""
        payload = {
            "model": "bytedance/seedance-2.0/reference-to-video",
            "reference_images": reference_images,
            "prompt": prompt,
            "duration": duration,
            "generate_audio": audio
        }
        return self._submit_and_poll(payload)
    
    def create_portrait(self, image_url, name="portrait"):
        """Register a portrait in the Portrait Library."""
        resp = requests.post(self.PORTRAIT_URL, headers=self.headers, json={
            "image_url": image_url,
            "name": name
        })
        return resp.json()["data"]["id"]
    
    def get_portrait_status(self, asset_id):
        """Check portrait processing status."""
        resp = requests.get(
            f"{self.PORTRAIT_URL}/{asset_id}", 
            headers=self.headers
        )
        return resp.json()["data"]["status"]
    
    def _submit_and_poll(self, payload, interval=5, timeout=300):
        """Submit a generation request and poll until complete."""
        resp = requests.post(self.BASE_URL, headers=self.headers, json=payload)
        prediction_id = resp.json()["data"]["id"]
        
        elapsed = 0
        while elapsed < timeout:
            result = requests.get(
                f"{self.BASE_URL}/{prediction_id}", 
                headers=self.headers
            ).json()
            status = result["data"]["status"]
            
            if status in ("completed", "succeeded"):
                return result["data"]["outputs"]
            elif status == "failed":
                raise Exception(f"Generation failed: {result['data'].get('error')}")
            
            time.sleep(interval)
            elapsed += interval
        
        raise TimeoutError(f"Generation timed out after {timeout}s")
```

### Step 4: Generate Your First Video

```python
client = SeedanceClient()

# Text-to-Video
outputs = client.text_to_video(
    prompt="A photographer walks through a sunlit Tokyo alley, cherry blossoms falling, "
           "handheld camera follows from behind, shallow depth of field, golden hour",
    duration=10,
    resolution="720p",
    ratio="16:9"
)
print("Video URL:", outputs[0])
```

### Step 5: Use Portrait Library in Code

```python
client = SeedanceClient()

# Register a portrait
asset_id = client.create_portrait(
    image_url="https://example.com/headshot.jpg",
    name="CEO Portrait"
)

# Wait for processing
import time
while True:
    status = client.get_portrait_status(asset_id)
    if status == "active":
        break
    time.sleep(3)

# Generate video with the registered face
outputs = client.reference_to_video(
    reference_images=[f"asset://{asset_id}"],
    prompt="The person in image 1 presents quarterly results in a modern boardroom, "
           "confident posture, professional lighting, camera slowly zooms in",
    duration=12
)
print("Video URL:", outputs[0])
```

### Step 6: Chain Videos for Longer Content

```python
# Generate a sequence of connected scenes
first_scene = client.text_to_video(
    prompt="A detective enters a dimly lit office, noir style, rain on windows",
    duration=8
)

# Use the last frame of scene 1 as the starting frame of scene 2
second_scene = client.image_to_video(
    image_url=first_scene[0],  # last frame URL from the outputs
    prompt="The detective picks up a photograph from the desk, camera pulls in close",
    duration=8
)
```

> 💡 **[Try the full API on Atlas Cloud](https://www.atlascloud.ai/models/bytedance/seedance-2.0/text-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0) — includes interactive playground and code snippets.**

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

## 🎨 Seedance 2.0 Prompt Engineering Guide

Writing effective prompts for Seedance 2.0 can dramatically improve output quality. Below are tested prompt patterns organized by style and use case.

### Cinematic & Film Style Prompts

**1. Noir Detective Scene**
```
A private detective sits alone in a rain-streaked office at midnight, smoking light 
curls upward, venetian blind shadows across the desk, camera slowly dollies forward, 
film noir lighting with high contrast, 1940s aesthetic, moody jazz score
```

**2. Epic Landscape Reveal**
```
Aerial drone shot ascending over misty mountain peaks at sunrise, clouds rolling through 
valleys below, golden light hits snow-capped summits, camera tilts down then pushes 
forward, sweeping orchestral score, 4K cinematic quality
```

**3. Intimate Dialogue Scene**
```
Two friends sit across a cafe table, warm afternoon light through large windows, one 
laughs while the other tells a story, shallow depth of field shifting between faces, 
handheld camera feel, ambient cafe sounds with soft background music
```

### Commercial & Product Prompts

**4. Product Showcase**
```
A sleek smartphone rotates slowly on a reflective black surface, studio lighting with 
soft rim light, particles of light float around the device, camera circles smoothly, 
minimalist style, premium tech aesthetic
```

**5. Food Commercial**
```
Fresh pasta being tossed in a sizzling pan, steam rising, herbs scattered mid-air in 
slow motion, warm kitchen lighting from above, macro close-up then pull back to reveal 
the chef, sizzling sound effects
```

### Social Media & Short-Form Prompts

**6. TikTok-Style Transition**
```
A woman in streetwear snaps her fingers and outfit changes instantly, urban rooftop 
setting at golden hour, upbeat energy, camera zooms in on the snap then zooms out to 
reveal new look, 9:16 portrait format, trendy pop music
```

**7. Instagram Reel — Travel**
```
Montage of Santorini Greece highlights: white buildings with blue domes, sunset over 
the caldera, local food close-ups, swimming in crystal water, smooth transitions 
between scenes, warm color grading, chill lo-fi soundtrack
```

### Character & Portrait Prompts

**8. AI Spokesperson Introduction**
```
[Use with Portrait Library] The person in @image1 stands in a modern glass office, 
delivers a welcome message to camera with confident smile, professional attire, soft 
key light from left, slow subtle zoom in, corporate but warm tone
```

**9. Educational Presenter**
```
[Use with Portrait Library] The instructor in @image1 explains a concept at a digital 
whiteboard, gestures naturally toward floating 3D diagrams, clean studio background, 
well-lit, calm authoritative voice, medium shot with occasional close-up
```

### Artistic & Experimental Prompts

**10. Abstract Art Animation**
```
Flowing liquid metal transforms into organic plant shapes, bioluminescent colors pulsing 
in deep blue and magenta, macro lens extreme close-up, slow dreamlike movement, ambient 
electronic soundscape, art installation aesthetic
```

**11. Anime-Style Action**
```
An anime warrior charges through a bamboo forest, sword drawn, leaves scatter in slow 
motion, dramatic speed lines, camera tracks alongside the character, cel-shaded aesthetic 
with vibrant colors, intense orchestral combat music
```

**12. Retro VHS Aesthetic**
```
A teenager rides a bicycle through suburban streets at dusk, VHS tape artifacts and scan 
lines overlay, warm 1980s color palette, lens flare from streetlights, camera follows from 
a car window, synthwave soundtrack
```

### Prompt Writing Tips for Seedance 2.0

- **Be specific about camera movement**: "camera slowly dollies forward" beats "camera moves"
- **Include lighting details**: "warm golden hour side light" creates mood
- **Mention audio when using `generate_audio: true`**: "ambient rain sounds with distant thunder"
- **Use the @reference system**: "@image1 walks toward @image2 in the style of @image3"
- **Specify aspect ratio context**: write vertical scene descriptions for 9:16 content
- **Layer your description**: subject → action → environment → camera → mood → audio

---

## 💡 Seedance 2.0 Tips & Tricks

### Getting the Best Quality Output

1. **Use 720p for iteration, 2K for final output** — iterate at lower resolution to save time and credits, then regenerate your best prompt at full 2K
2. **Always describe camera movement** — Seedance 2.0 has the best camera control of any model (9/10), so take advantage of it
3. **Enable audio generation strategically** — audio adds richness but increases generation time; disable during rapid iteration
4. **Use web search for real-world subjects** — set `web_search: true` when prompting about specific locations, celebrities, or branded content

### Advanced Techniques

5. **Multi-reference compositing** — use @image1 for character, @image2 for art style, @image3 for background to control every element independently
6. **Video chaining for long content** — use `return_last_frame: true` then feed it into image-to-video for seamless multi-shot sequences
7. **Fast model for storyboarding** — generate 6-8 variants with the Fast model, pick the best direction, then regenerate with the standard model
8. **Voice cloning workflow** — upload a 10-30 second voice sample, then reference it in prompts mentioning dialogue; works best with clear, single-speaker audio
9. **Portrait Library batch workflow** — register multiple portraits, then reference them in the same scene using `@image1`, `@image2`, etc. for multi-character scenes
10. **Negative prompting through specificity** — instead of trying to exclude elements, describe exactly what you want in detail; Seedance 2.0 responds well to precise positive instructions

### Common Mistakes to Avoid

- **Don't upload real faces directly** — always go through Portrait Library
- **Don't use overly short prompts** — "a cat" will give generic results; add environment, lighting, camera, and mood
- **Don't set duration too long for simple scenes** — 4-6 seconds is ideal for single-action clips; use chaining for longer content
- **Don't forget aspect ratio** — match your output to your platform (9:16 for TikTok/Reels, 16:9 for YouTube, 1:1 for Instagram posts)

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

## 🔥 Seedance 2.0 vs Kling 3.0 — Detailed Comparison

Seedance 2.0 and Kling 3.0 are the two leading Chinese AI video models in 2026. Here's how they compare in depth:

### Visual Quality
- **Kling 3.0** takes the edge in raw visual fidelity with 4K/60fps output and a visual quality score of 8.4/10
- **Seedance 2.0** scores 8.2/10 overall but offers native 2K with superior consistency across multi-shot generations

### Camera & Controllability
- **Seedance 2.0** leads decisively with a 9/10 camera control rating — the highest of any video model
- Kling 3.0 scores 8/10 on camera control; strong but without Seedance's fine-grained director controls

### Unique Strengths
- **Seedance 2.0**: Portrait Library for identity-consistent faces, web search for real-world references, 12-input multimodal control, voice cloning with 3 characters
- **Kling 3.0**: Longer video duration (up to 2 minutes), higher maximum resolution (4K/60fps), motion brush for precise movement control

### Best Use Cases
- Choose **Seedance 2.0** when you need: real-face identity preservation, complex multi-reference scenes, audio-video joint generation, or maximum camera control
- Choose **Kling 3.0** when you need: maximum visual resolution, longer form video (>15s), or simpler single-subject generation

### API Pricing Comparison

| Platform | Seedance 2.0 (10s) | Kling 3.0 (10s) |
|----------|-------------------|-----------------|
| Atlas Cloud | $0.10/req | $0.10/req |
| Native Platform | ~$0.60 | ~$0.50 |

> 💡 **[Try both models side-by-side on Atlas Cloud](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0) — compare outputs at the same price point.**

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

## 🔄 Migration from Seedance 1.5 to 2.0

Upgrading from Seedance 1.5 to Seedance 2.0 is straightforward. Here's what you need to know:

### API Changes

**Model ID Update:**
```python
# Seedance 1.5
"model": "bytedance/seedance-v1.5-pro/text-to-video"

# Seedance 2.0
"model": "bytedance/seedance-2.0/text-to-video"
```

**New Parameters Available in 2.0:**
```python
{
    "web_search": True,          # New: enable real-time web references
    "generate_audio": True,       # New: joint audio-video generation
    "resolution": "2k",          # New: native 2K support
    "reference_images": [...],   # New: up to 9 reference images
    "reference_videos": [...],   # New: up to 3 reference videos
    "reference_audio": "...",    # New: audio-driven generation
}
```

### What Requires Changes

1. **Real face inputs** — If you were passing face photos directly, you now need to use the Portrait Library. Register faces as assets first, then reference them with `asset://` URIs.
2. **Model IDs** — Update from `seedance-v1.5-pro` to `seedance-2.0` in all API calls
3. **NSFW content** — Seedance 2.0 does not support spicy mode. Continue using `seedance-v1.5-pro/image-to-video-spicy` for this use case.

### What's Backwards Compatible

- The basic request/response structure remains the same
- Prompt format is unchanged — your existing prompts will work
- Polling mechanism for async results is identical
- Authentication and API key format haven't changed

### Migration Checklist

- [ ] Update model IDs in all API calls
- [ ] Register any real-face images in the Portrait Library
- [ ] Update any code that passes face images directly
- [ ] Test audio generation with existing prompts
- [ ] Update resolution settings to take advantage of 2K
- [ ] Review and update prompt templates to include camera/audio directions
- [ ] Keep Seedance 1.5 Pro integration for NSFW use cases if needed

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

### 7. How do I get the best results from the Seedance 2.0 API?

Write detailed prompts that include subject, action, environment, camera movement, lighting, and audio descriptions. Use the reference system (@image1, @image2) for multi-element control. Start with the Fast model for iteration, then switch to standard for final output.

### 8. Can I use Seedance 2.0 for commercial projects?

Yes. Content generated through the API can be used commercially, subject to ByteDance's terms of service. Ensure you have rights to any reference images you upload, especially when using the Portrait Library with real people's faces.

---

<div align="center">

### [👉 Try Seedance 2.0 on Atlas Cloud — $0.10/video, Free Credits 👈](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0)

**Made with ❤️ by the open-source community**

[⬆ Back to Top](#-awesome-seedance-20--bytedances-cinema-grade-video-model-with-portrait-library)

</div>
