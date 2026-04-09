# 🎬 Awesome Seedance 2.0 — ByteDance의 시네마급 비디오 생성 모델 (포트레이트 라이브러리 탑재)

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Seedance 2.0](https://img.shields.io/badge/Seedance-2.0-blue.svg)](https://www.atlascloud.ai/models/bytedance/seedance-2.0/text-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0)
[![Try on Atlas Cloud](https://img.shields.io/badge/Try-Atlas%20Cloud-green.svg)](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

**Language / 언어:** [English](README.md) | [中文](README_zh.md) | [日本語](README_ja.md) | 한국어

---

> 🔥 **Seedance 2.0** — ByteDance의 플래그십 비디오 생성 모델. **Diffusion Transformer (DiT)** 아키텍처 기반. 종합 점수 **8.2/10** (Veo 3, Wan, Kling 상회). 포트레이트 라이브러리(실제 얼굴 지원), 네이티브 2K, 오디오-비디오 동시 생성, 음성 복제, 웹 검색, 12입력 멀티모달 제어 지원. **Atlas Cloud에서 $0.10/요청.**

---

## 목차

- [Seedance 2.0의 새로운 기능](#seedance-20의-새로운-기능)
- [벤치마크 및 순위](#-벤치마크-및-순위)
- [포트레이트 라이브러리 — 실제 얼굴 지원](#-포트레이트-라이브러리--실제-얼굴-지원)
- [핵심 기능 상세](#-핵심-기능-상세)
- [Atlas Cloud 모델 목록](#-atlas-cloud-모델-목록)
- [API 빠른 시작](#-api-빠른-시작)
- [완전한 API 튜토리얼](#-완전한-api-튜토리얼)
- [포트레이트 라이브러리 API](#-포트레이트-라이브러리-api)
- [프롬프트 엔지니어링 가이드](#-프롬프트-엔지니어링-가이드)
- [Seedance 2.0 vs 경쟁 모델](#-seedance-20-vs-경쟁-모델)
- [Seedance 2.0 vs 1.5 Pro](#-seedance-20-vs-15-pro)
- [활용 사례](#-활용-사례)
- [리소스](#-리소스)
- [FAQ](#faq)

---

## Seedance 2.0의 새로운 기능

ByteDance가 **2026년 2월 12일** 출시한 Seedance 2.0은 비디오 AI의 세대 교체를 상징합니다:

- **아키텍처**: Diffusion Transformer (DiT) — U-Net을 대체하여 더 나은 확장성
- **통합 멀티모달**: 텍스트, 이미지, 비디오, 오디오에서 오디오-비디오 동시 생성
- **네이티브 2K**: 2048×1080 (가로) / 1080×2048 (세로) — 1080p에서 업그레이드
- **포트레이트 라이브러리**: 전용 실제 얼굴 에셋 관리 시스템을 탑재한 최초의 주요 모델
- **음성 복제**: 장면당 최대 3개의 커스텀 캐릭터 음성
- **웹 검색**: 생성 중 실시간 인터넷 참조
- **CapCut 통합**: 2026년 3월 26일부터 CapCut에서 글로벌 이용 가능
- **내부 벤치마크**: SeedVideoBench-2.0 (지시 준수, 모션 품질, 미학, 오디오 포함)

---

## 📊 벤치마크 및 순위

### Artificial Analysis 리더보드

| 지표 | 점수 | 순위 |
|------|------|------|
| **텍스트→비디오 Elo** | 1,273 | Top 3 (720p) |
| **이미지→비디오 Elo** | 1,355 | Top 3 (720p) |
| **종합 점수** | **8.2/10** | 출시 시 1위 |
| **카메라 제어** | **9/10** | 전 모델 1위 |
| **창의적 제어** | 5/5 | 최상위 |
| **오디오 동기화** | 5/5 | 최상위 |

### 모델 비교

| 모델 | 종합 | 카메라 | 오디오 |
|------|------|--------|--------|
| **Seedance 2.0** | **8.2** | **9/10** | **5/5** |
| Google Veo 3 | 7.0 | 7/10 | 5/5 |
| Alibaba Wan 2.2 | 5.6 | — | — |
| Kuaishou Kling 2.1 | 4.4 | — | — |

> Seedance 2.0은 **VBench-2.0**에 포함되어 Veo 3, Vidu, Wan, Kling과 함께 평가되었습니다.

---

## 🎭 포트레이트 라이브러리 — 실제 얼굴 지원

### 문제점
Seedance 2.0은 안전 규정 준수를 위해 **표준 입력으로 제출된 실제 얼굴 이미지를 차단**합니다. 실제 인물의 사진을 직접 붙여넣을 수 없습니다.

### 해결책: 포트레이트 라이브러리
전용 에셋 관리 시스템입니다:

1. 초상화 이미지를 **등록** → 전처리 및 검증
2. 상태를 **확인**: `Processing → Active`
3. 이미지 필드에서 `asset://<asset_id>`로 **참조**
4. **아이덴티티 일관성**이 보장된 비디오 결과 생성

### 이미지 요구사항

| 사양 | 값 |
|------|-----|
| 형식 | JPEG, PNG, WebP, BMP, TIFF, GIF, HEIC |
| 크기 | 각 변 300 – 6,000 px |
| 종횡비 | 0.4 – 2.5 |
| 최대 크기 | 30 MB |

### Playground에서 사용하기

1. 이미지 입력 영역에서 **포트레이트 라이브러리**를 엽니다
2. 초상화를 **업로드**하고 전처리를 기다립니다
3. 처리된 초상화를 **선택** → 참조로 사용 가능
4. 프롬프트를 작성하고 생성하세요!

> **팁**: Playground 옆의 **"API" 탭**에서 요청 예제와 SDK 스니펫을 확인하세요. **"Copy for LLM"**으로 AI 코딩 어시스턴트를 통한 통합을 빠르게 구축할 수 있습니다.

---

## ✨ 핵심 기능 상세

### 🔊 네이티브 오디오-비디오 동시 생성
단일 추론으로 비디오 + 동기화된 오디오(대사, 효과음, 음악)를 생성합니다. 중국어, 영어, 스페인어 등에서 자동 립싱크를 지원합니다. 스테레오 출력.

### 🗣️ 음성 복제
실제 음성 샘플을 업로드하여 톤, 억양, 표현을 가이드합니다. 장면당 최대 **3개의 커스텀 캐릭터 음성**을 지원합니다.

### 🌐 웹 검색 (Seedance 2.0 전용)
`web_search: true`를 활성화하여 생성 중 실시간 인터넷 참조를 가져옵니다. 모델이 학습하지 않은 특정 인물, 장소, 스타일에 적합합니다.

### 🖼️ 12입력 멀티모달 제어 (@참조 시스템)
`@` 시스템으로 참조를 프롬프트 요소에 바인딩:
- 최대 **9개의 참조 이미지** (캐릭터, 스타일, 장면)
- 최대 **3개의 참조 비디오** (총 ≤15초)로 편집/확장
- **1개의 참조 오디오**로 오디오 기반 생성
- 프롬프트 예시: "@image1의 캐릭터가 @image2의 스타일로 @audio1에 맞춰 춤을 춥니다"

### 🎬 디렉터급 카메라 제어
실제 영화 감독처럼 카메라를 제어:
- 푸시/풀 줌, 포커스 풀
- 트래킹 샷, POV 전환
- 핸드헬드 흔들림 효과
- 카메라 제어 점수 **9/10** (전 모델 중 최고)

### ✂️ 비디오 편집
- 기존 비디오 확장
- 모션 참조 적용
- 오브젝트 제거
- 비주얼 이펙트 추가

### 📐 출력 사양
- **해상도**: 네이티브 2K (2048×1080 / 1080×2048), 720p, 480p
- **길이**: 4-15초, 멀티샷 자연스러운 전환
- **종횡비**: 16:9, 4:3, 1:1, 3:4, 9:16, 21:9, 적응형
- **마지막 프레임 반환**: 비디오 체이닝 지원

---

## 💰 Atlas Cloud 모델 목록

| 모델 | ID | 가격 |
|------|-----|------|
| **텍스트→비디오** | `bytedance/seedance-2.0/text-to-video` | $0.10/회 |
| **이미지→비디오** | `bytedance/seedance-2.0/image-to-video` | $0.10/회 |
| **참조→비디오** | `bytedance/seedance-2.0/reference-to-video` | $0.10/회 |
| **빠른 T2V** | `bytedance/seedance-2.0-fast/text-to-video` | $0.10/회 |
| **빠른 I2V** | `bytedance/seedance-2.0-fast/image-to-video` | $0.10/회 |
| **빠른 Ref2V** | `bytedance/seedance-2.0-fast/reference-to-video` | $0.10/회 |

> 빠른 모델은 30-60초 내에 5-10초 비디오를 생성합니다 (표준 모델은 수 분 소요). 다른 플랫폼보다 ~33% 저렴하며, Atlas Cloud에서는 동일 가격입니다.

---

## ⚡ API 빠른 시작

### 텍스트→비디오 (Python)

```python
import requests, time

API_KEY = "your-atlas-cloud-api-key"
H = {"Authorization": f"Bearer {API_KEY}", "Content-Type": "application/json"}

r = requests.post("https://api.atlascloud.ai/api/v1/model/prediction", headers=H, json={
    "model": "bytedance/seedance-2.0/text-to-video",
    "prompt": "젊은 영화 제작자가 빈티지 모니터에서 영상을 검토하는 장면, 따뜻한 스튜디오 조명, 시네마틱 그레인",
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
        print("비디오 URL:", res["data"]["outputs"][0])
        break
    elif res["data"]["status"] == "failed":
        print("오류:", res["data"].get("error"))
        break
    time.sleep(5)
```

### 포트레이트 참조→비디오

```python
# 포트레이트 라이브러리에 등록 후 (asset_id = "ark-xxxxx")
r = requests.post("https://api.atlascloud.ai/api/v1/model/prediction", headers=H, json={
    "model": "bytedance/seedance-2.0/reference-to-video",
    "reference_images": ["asset://ark-xxxxx"],
    "prompt": "이미지 1의 인물이 TED 강연을 하는 장면, 자신감 있는 제스처, 청중의 박수",
    "duration": 12,
    "generate_audio": True
})
```

> 💡 **[Atlas Cloud에서 API 키 발급](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0) — 무료 크레딧, 신용카드 불필요!**

---

## 📘 완전한 API 튜토리얼

### 1단계: API 키 발급

1. [Atlas Cloud](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0)에 가입
2. **Settings → API Keys**로 이동
3. **Create API Key** 클릭 후 안전하게 저장
4. 무료 크레딧으로 즉시 실험 시작 가능

### 2단계: 의존성 설치

```bash
pip install requests python-dotenv
```

### 3단계: 재사용 가능한 클라이언트 구축

```python
import requests, time, os
from dotenv import load_dotenv

load_dotenv()

class SeedanceClient:
    """Seedance 2.0 API 클라이언트"""
    
    BASE_URL = "https://api.atlascloud.ai/api/v1/model/prediction"
    
    def __init__(self):
        self.api_key = os.getenv("ATLASCLOUD_API_KEY")
        self.headers = {
            "Authorization": f"Bearer {self.api_key}",
            "Content-Type": "application/json"
        }
    
    def text_to_video(self, prompt, duration=10, resolution="720p",
                      ratio="16:9", audio=True):
        """텍스트 프롬프트에서 비디오 생성"""
        payload = {
            "model": "bytedance/seedance-2.0/text-to-video",
            "prompt": prompt,
            "duration": duration,
            "resolution": resolution,
            "ratio": ratio,
            "generate_audio": audio
        }
        return self._submit_and_poll(payload)
    
    def image_to_video(self, image_url, prompt, duration=8,
                       ratio="adaptive", audio=True):
        """정지 이미지를 비디오로 변환"""
        payload = {
            "model": "bytedance/seedance-2.0/image-to-video",
            "image": image_url,
            "prompt": prompt,
            "duration": duration,
            "ratio": ratio,
            "generate_audio": audio
        }
        return self._submit_and_poll(payload)
    
    def _submit_and_poll(self, payload, interval=5, timeout=300):
        """요청 제출 및 완료까지 폴링"""
        resp = requests.post(self.BASE_URL, headers=self.headers, json=payload)
        pid = resp.json()["data"]["id"]
        elapsed = 0
        while elapsed < timeout:
            result = requests.get(
                f"{self.BASE_URL}/{pid}", headers=self.headers
            ).json()
            status = result["data"]["status"]
            if status in ("completed", "succeeded"):
                return result["data"]["outputs"]
            elif status == "failed":
                raise Exception(f"생성 실패: {result['data'].get('error')}")
            time.sleep(interval)
            elapsed += interval
        raise TimeoutError(f"생성 시간 초과 ({timeout}초)")
```

> 💡 **[Atlas Cloud에서 전체 API 체험](https://www.atlascloud.ai/models/bytedance/seedance-2.0/text-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0) — 인터랙티브 Playground 및 코드 스니펫 포함.**

---

## 🔧 포트레이트 라이브러리 API

**기본 URL**: `https://console.atlascloud.ai/api/v1`

| 메서드 | 경로 | 설명 |
|--------|------|------|
| POST | `/sd/assets` | 이미지 URL에서 포트레이트 생성 |
| GET | `/sd/assets/:id` | 에셋 조회 (처리 중 자동 폴링) |
| GET | `/sd/assets` | 에셋 목록 (페이지네이션, 필터 지원) |
| PUT | `/sd/assets/:id` | 에셋 이름 변경 |
| DELETE | `/sd/assets/:id` | 휴지통으로 이동 (복구 가능) |
| GET | `/sd/assets/trash` | 휴지통 에셋 목록 |
| POST | `/sd/assets/:id/restore` | 휴지통에서 복구 |

---

## 🎨 프롬프트 엔지니어링 가이드

### 시네마틱 스타일

**1. 필름 누아르 탐정 장면**
```
자정, 비가 창문을 타고 흐르는 사무실에 홀로 앉은 사립 탐정, 담배 연기가 
피어오르고, 블라인드 그림자가 책상 위에 드리워진다, 카메라가 천천히 돌리인,
필름 누아르 하이 콘트라스트 조명, 1940년대 미학, 우울한 재즈 스코어
```

**2. 웅장한 풍경 샷**
```
해돋이 때 안개에 싸인 산봉우리 위로 드론이 상승, 구름이 아래 계곡을 흐르고,
금빛 햇살이 설산 정상을 비추는, 카메라가 내려다보다가 앞으로 전진,
웅장한 오케스트라 스코어, 시네마급 화질
```

**3. 제품 쇼케이스**
```
반사되는 검은 표면 위에서 세련된 스마트폰이 천천히 회전, 부드러운 림 라이트의
스튜디오 조명, 빛 입자가 기기 주위를 떠다님, 카메라가 부드럽게 원형으로 이동,
미니멀리스트 스타일, 프리미엄 테크 미학
```

### 프롬프트 작성 팁

- **카메라 움직임을 구체적으로 기술**: "카메라가 천천히 돌리 포워드"가 "카메라가 움직인다"보다 훨씬 효과적
- **조명 디테일 포함**: "따뜻한 골든아워 사이드 라이트"로 분위기 연출
- **@참조 시스템 활용**: "@image1의 캐릭터가 @image2의 스타일로 걸어간다"
- **레이어 구조로 기술**: 피사체 → 동작 → 환경 → 카메라 → 분위기 → 오디오

---

## 📊 Seedance 2.0 vs 경쟁 모델

| 기능 | Seedance 2.0 | Kling 3.0 | Sora 2 | Veo 3.1 | Wan 2.7 |
|------|-------------|-----------|--------|---------|---------|
| **아키텍처** | DiT | — | DiT | — | DiT |
| **종합 점수** | **8.2/10** | 8.1/10 | — | 7.0/10 | — |
| **포트레이트 라이브러리** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **네이티브 오디오** | ✅ | ❌ | ✅ | ✅ | ✅ |
| **음성 복제** | ✅ (3음성) | ❌ | ❌ | ❌ | ✅ |
| **웹 검색** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **최대 해상도** | **2K** | 4K/60fps | 1080p | 4K | 720p |
| **최대 길이** | 15초 | 2분 | 20초 | 8초 | 15초 |
| **멀티 참조** | **9이미지+3비디오** | 1이미지 | N/A | 1참조 | 5참조 |
| **카메라 제어** | **9/10** | 8/10 | 7/10 | 7/10 | — |
| **가격 (10초)** | **~$0.60** | ~$0.50 | ~$1.00 | ~$2.50 | ~$0.40 |

---

## 📊 Seedance 2.0 vs 1.5 Pro

| 기능 | 2.0 | 1.5 Pro |
|------|-----|---------|
| 아키텍처 | DiT | 이전 세대 |
| 해상도 | **네이티브 2K** | 1080p |
| 포트레이트 라이브러리 | ✅ | ❌ |
| 웹 검색 | ✅ | ❌ |
| 음성 복제 | ✅ (3음성) | ❌ |
| 멀티 참조 | 9이미지+3비디오+오디오 | 제한적 |
| 비디오 편집 | ✅ | ❌ |
| 길이 | 4-15초 | 4-12초 |
| 종횡비 | 7종+적응형 | 제한적 |
| 카메라 제어 | 9/10 | 기본 |
| NSFW | ❌ | ✅ |
| 가격 | $0.10/회 | $0.15-0.72 |

> NSFW: Atlas Cloud에서 `bytedance/seedance-v1.5-pro/image-to-video-spicy`를 사용하세요.

---

## 🎯 활용 사례

- 🎭 **AI 대변인** — 얼굴을 등록하고 무제한 비디오 변형 생성
- 📱 **소셜 미디어** — TikTok/YouTube/Instagram용 일관된 AI 아바타
- 🎓 **교육** — 다국어 음성 복제 지원 가상 강사
- 🛒 **이커머스** — 브랜드 담당자의 제품 데모
- 📰 **뉴스** — 포트레이트 에셋을 사용한 AI 앵커
- 🎬 **단편 영화** — 디렉터급 카메라 제어로 일관된 캐릭터
- 🎮 **게임** — 컨셉 아트에서 캐릭터 소개 생성
- 🌐 **다국어** — 동일한 얼굴 + 다른 언어의 음성 복제

---

## 📚 리소스

### 공식
- 🌐 [Seedance 2.0 공식 페이지](https://seed.bytedance.com/en/seedance2_0)
- 📄 [출시 블로그](https://seed.bytedance.com/en/blog/official-launch-of-seedance-2-0)
- 📚 [위키백과](https://en.wikipedia.org/wiki/Seedance_2.0)
- 🎬 [CapCut 통합](https://www.capcut.com/newsroom/dreamina-seedance-2)

### Atlas Cloud
- 🚀 [Seedance 2.0 T2V](https://www.atlascloud.ai/models/bytedance/seedance-2.0/text-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0)
- 🚀 [Seedance 2.0 I2V](https://www.atlascloud.ai/models/bytedance/seedance-2.0/image-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0)
- 🚀 [Seedance 2.0 Ref2V](https://www.atlascloud.ai/models/bytedance/seedance-2.0/reference-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0)

### 리뷰 및 분석
- 📰 [TechCrunch: Seedance 2.0 CapCut 탑재](https://techcrunch.com/2026/03/26/bytedances-new-ai-video-generation-model-dreamina-seedance-2-0-comes-to-capcut/)
- 📊 [WaveSpeedAI: SD 2.0 vs Kling vs Sora vs Veo](https://wavespeed.ai/blog/posts/seedance-2-0-vs-kling-3-0-sora-2-veo-3-1-video-generation-comparison-2026/)
- 📝 [BuildFastWithAI: SD 2.0 리뷰](https://www.buildfastwithai.com/blogs/seedance-2-bytedance-ai-video-2026)
- 📊 [Artificial Analysis 리더보드](https://artificialanalysis.ai/video/leaderboard/image-to-video)

---

## FAQ

### 1. 실제 얼굴 사진을 직접 업로드할 수 없는 이유는?

Seedance 2.0은 콘텐츠 안전 정책을 적용합니다. 실제 얼굴 이미지는 **포트레이트 라이브러리**를 통해 전처리 및 검증이 필요합니다. 이를 통해 악용을 방지하면서 합법적인 얼굴 기반 콘텐츠 생성을 지원합니다.

### 2. Seedance 2.0은 2026년 최고의 비디오 모델인가요?

Artificial Analysis에서 종합 점수 **8.2/10**을 기록했으며, 출시 시점 최고입니다. 카메라 제어 최고 (9/10), 멀티모달 입력 시스템 최강 (12 참조). Kling 3.0은 영상 품질 (8.4/10)과 최대 길이 (2분)에서 우위입니다.

### 3. NSFW 콘텐츠를 지원하나요?

아니요. Seedance 2.0은 포트레이트 라이브러리를 통한 콘텐츠 안전을 적용합니다. 무제한 콘텐츠는 Atlas Cloud의 **Seedance 1.5 Pro Spicy** (`bytedance/seedance-v1.5-pro/image-to-video-spicy`)를 사용하세요.

### 4. 표준판 vs 빠른판 — 어떤 것을 사용해야 하나요?

**빠른판**: 30-60초 생성, 미리보기와 반복 작업에 적합. 얼굴과 고속 모션 장면에서 약간의 품질 저하. **표준판**: 최고 품질, 수 분 소요. 최종 출력물에 사용.

### 5. 여러 비디오를 연결할 수 있나요?

네! `return_last_frame: true`로 마지막 프레임을 가져온 후, 다음 `image-to-video` 호출의 첫 프레임으로 사용하세요.

### 6. 상업 프로젝트에 사용할 수 있나요?

네. API를 통해 생성된 콘텐츠는 ByteDance 서비스 약관에 따라 상업적으로 사용할 수 있습니다. 참조 이미지의 권리를 확인해 주세요.

---

<div align="center">

### [👉 Atlas Cloud에서 Seedance 2.0 체험 — $0.10/비디오, 무료 크레딧 👈](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0)

**오픈소스 커뮤니티가 ❤️으로 제작**

[⬆ 맨 위로 돌아가기](#-awesome-seedance-20--bytedance의-시네마급-비디오-생성-모델-포트레이트-라이브러리-탑재)

</div>
