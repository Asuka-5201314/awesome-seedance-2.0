# 🎬 Awesome Seedance 2.0 — 字节跳动影院级视频模型（含人像库功能）

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Seedance 2.0](https://img.shields.io/badge/Seedance-2.0-blue.svg)](https://www.atlascloud.ai/models/bytedance/seedance-2.0/text-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0)
[![Try on Atlas Cloud](https://img.shields.io/badge/Try-Atlas%20Cloud-green.svg)](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

**Language / 语言:** [English](README.md) | 中文 | [日本語](README_ja.md) | [한국어](README_ko.md)

---

> 🔥 **Seedance 2.0** — 字节跳动旗舰视频生成模型，基于 **Diffusion Transformer (DiT)** 架构。综合评分 **8.2/10**（超越 Veo 3、Wan、Kling）。支持人像库（真人面部）、原生 2K 分辨率、音视频联合生成、声音克隆、联网搜索、12 路多模态输入控制。**Atlas Cloud 上仅需 $0.10/次。**

---

## 目录

- [Seedance 2.0 有什么新功能？](#seedance-20-有什么新功能)
- [基准测试与排名](#-基准测试与排名)
- [人像库 — 真人面部支持](#-人像库--真人面部支持)
- [核心功能详解](#-核心功能详解)
- [Atlas Cloud 可用模型](#-atlas-cloud-可用模型)
- [API 快速入门](#-api-快速入门)
- [完整 API 教程](#-完整-api-教程)
- [人像库 API](#-人像库-api)
- [Seedance 2.0 提示词工程指南](#-seedance-20-提示词工程指南)
- [Seedance 2.0 使用技巧](#-seedance-20-使用技巧)
- [Seedance 2.0 与竞品对比](#-seedance-20-与竞品对比)
- [Seedance 2.0 与 Kling 3.0 详细对比](#-seedance-20-与-kling-30-详细对比)
- [Seedance 2.0 与 1.5 Pro 对比](#-seedance-20-与-15-pro-对比)
- [从 Seedance 1.5 迁移到 2.0](#-从-seedance-15-迁移到-20)
- [使用场景](#-使用场景)
- [资源](#-资源)
- [常见问题](#常见问题)

---

## Seedance 2.0 有什么新功能？

字节跳动于 **2026 年 2 月 12 日**发布 Seedance 2.0，这是视频 AI 领域的一次代际飞跃：

- **架构升级**：Diffusion Transformer (DiT) — 取代 U-Net，具有更好的可扩展性
- **统一多模态**：支持从文本、图片、视频、音频进行音视频联合生成
- **原生 2K**：2048×1080（横版）/ 1080×2048（竖版）— 从 1080p 升级
- **人像库**：首个具备专业真人面部资产管理系统的主流模型
- **声音克隆**：每个场景最多支持 3 个自定义角色声音
- **联网搜索**：生成时可实时参考互联网信息
- **剪映集成**：2026 年 3 月 26 日起通过 CapCut/剪映全球可用
- **内部基准**：SeedVideoBench-2.0 覆盖指令遵循、运动质量、美学和音频

---

## 📊 基准测试与排名

### Artificial Analysis 排行榜

| 指标 | 分数 | 排名 |
|------|------|------|
| **文生视频 Elo** | 1,273 | Top 3 (720p) |
| **图生视频 Elo** | 1,355 | Top 3 (720p) |
| **综合评分** | **8.2/10** | 发布时第一 |
| **镜头控制** | **9/10** | 所有模型第一 |
| **创意控制** | 5/5 | 顶级 |
| **音频同步** | 5/5 | 顶级 |

### 各模型对比

| 模型 | 综合 | 镜头 | 音频 |
|------|------|------|------|
| **Seedance 2.0** | **8.2** | **9/10** | **5/5** |
| Google Veo 3 | 7.0 | 7/10 | 5/5 |
| 阿里 Wan 2.2 | 5.6 | — | — |
| 快手 Kling 2.1 | 4.4 | — | — |

> Seedance 2.0 已被纳入 **VBench-2.0**，与 Veo 3、Vidu、Wan 和 Kling 一同评测。

---

## 🎭 人像库 — 真人面部支持

### 问题所在
Seedance 2.0 出于安全合规考虑，**会拦截通过标准输入提交的真人面部图片**。你不能直接粘贴真人照片。

### 解决方案：人像库
这是一个专用的资产管理系统：

1. **注册**人像图片 → 预处理和验证
2. **等待**状态变更：`处理中 → 已激活`
3. 在任何图片字段中通过 `asset://<asset_id>` **引用**
4. 模型生成出**身份一致**的视频结果

### 人像库使用教程

#### 第一步：准备人像图片

| 规格 | 要求 |
|------|------|
| 格式 | JPEG、PNG、WebP、BMP、TIFF、GIF、HEIC |
| 尺寸 | 每边 300 – 6,000 像素 |
| 宽高比 | 0.4 – 2.5 |
| 最大体积 | 30 MB |

**人像照片最佳实践：**
- 使用光线充足、正面拍摄、背景简洁的照片
- 确保面部清晰可见，不被配饰遮挡
- 更高分辨率的图片能产生更好的身份保持效果
- 避免对源图片使用重度滤镜或极端色彩调整

#### 第二步：通过 Playground 上传

1. 在图片输入区域打开**人像库**
2. **上传**人像并等待预处理完成
3. **选择**已处理的人像 → 可作为参考使用
4. 编写提示词并生成！

#### 第三步：通过 API 上传

```python
import requests

API_KEY = "your-atlas-cloud-api-key"
H = {"Authorization": f"Bearer {API_KEY}", "Content-Type": "application/json"}

# 创建人像资产
resp = requests.post("https://console.atlascloud.ai/api/v1/sd/assets", headers=H, json={
    "image_url": "https://example.com/portrait.jpg",
    "name": "我的人像"
})
asset_id = resp.json()["data"]["id"]
print(f"资产已创建：{asset_id}")
```

> **提示**：点击 Playground 旁边的 **"API"标签** 查看请求示例和 SDK 代码片段。使用 **"Copy for LLM"** 功能可通过 AI 编程助手快速搭建集成。

---

## ✨ 核心功能详解

### 🔊 原生音视频联合生成
单次推理同时生成视频和同步音频（对话、音效、音乐）。支持中文、英文、西班牙语等多语言自动口型同步。立体声输出。

### 🗣️ 声音克隆
上传真实语音样本来引导语气、口音和表情。每个场景最多支持 **3 个自定义角色声音**。

### 🌐 联网搜索（Seedance 2.0 独有）
启用 `web_search: true` 在生成时获取真实世界参考。适用于模型未见过的特定人物、地点或风格。

### 🖼️ 12 路多模态输入（@引用系统）
`@` 系统允许你将参考绑定到提示词元素：
- 最多 **9 张参考图片**（角色、风格、场景）
- 最多 **3 段参考视频**（总计 ≤15 秒）用于编辑/延伸
- **1 段参考音频**用于音频驱动生成
- 提示词示例："@image1 中的角色在 @image2 的风格场景中跟着 @audio1 跳舞"

### 🎬 导演级镜头控制
像真正的导演一样控制镜头：
- 推拉变焦、焦点切换
- 跟踪镜头、视角切换
- 手持晃动效果
- 镜头控制评分 **9/10**（所有模型中最高）

### ✂️ 视频编辑
- 延伸已有视频
- 应用动作参考
- 移除物体
- 添加视觉效果

### 📐 输出规格
- **分辨率**：原生 2K（2048×1080 / 1080×2048）、720p、480p
- **时长**：4-15 秒，多镜头自然过渡
- **宽高比**：16:9、4:3、1:1、3:4、9:16、21:9、自适应
- **尾帧返回**：可无缝拼接视频

---

## 💰 Atlas Cloud 可用模型

| 模型 | ID | 价格 |
|------|-----|------|
| **文生视频** | `bytedance/seedance-2.0/text-to-video` | $0.10/次 |
| **图生视频** | `bytedance/seedance-2.0/image-to-video` | $0.10/次 |
| **参考生视频** | `bytedance/seedance-2.0/reference-to-video` | $0.10/次 |
| **快速文生视频** | `bytedance/seedance-2.0-fast/text-to-video` | $0.10/次 |
| **快速图生视频** | `bytedance/seedance-2.0-fast/image-to-video` | $0.10/次 |
| **快速参考生视频** | `bytedance/seedance-2.0-fast/reference-to-video` | $0.10/次 |

> 快速模型在 30-60 秒内生成 5-10 秒视频（标准模型需要数分钟）。其他平台上便宜约 33%，Atlas Cloud 统一价格。

---

## ⚡ API 快速入门

### 文生视频 (Python)

```python
import requests, time

API_KEY = "your-atlas-cloud-api-key"
H = {"Authorization": f"Bearer {API_KEY}", "Content-Type": "application/json"}

r = requests.post("https://api.atlascloud.ai/api/v1/model/prediction", headers=H, json={
    "model": "bytedance/seedance-2.0/text-to-video",
    "prompt": "一位年轻电影人在复古显示器前回看素材，温暖的工作室灯光，电影胶片质感",
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
        print("视频地址:", res["data"]["outputs"][0])
        break
    elif res["data"]["status"] == "failed":
        print("错误:", res["data"].get("error"))
        break
    time.sleep(5)
```

### 人像参考生成视频

```python
# 在人像库中注册人像后（asset_id = "ark-xxxxx"）
r = requests.post("https://api.atlascloud.ai/api/v1/model/prediction", headers=H, json={
    "model": "bytedance/seedance-2.0/reference-to-video",
    "reference_images": ["asset://ark-xxxxx"],
    "prompt": "图片 1 中的人物在进行 TED 演讲，自信的手势，观众鼓掌",
    "duration": 12,
    "generate_audio": True
})
```

> 💡 **[在 Atlas Cloud 获取 API 密钥](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0) — 免费额度，无需信用卡！**

---

## 📘 完整 API 教程

### 第一步：获取 API 密钥

1. 在 [Atlas Cloud](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0) 注册账号
2. 进入 **Settings → API Keys**
3. 点击 **Create API Key** 并安全保存
4. 你将获得免费额度，可立即开始实验

### 第二步：安装依赖

```bash
pip install requests python-dotenv
```

### 第三步：构建可复用客户端

```python
import requests, time, os
from dotenv import load_dotenv

load_dotenv()

class SeedanceClient:
    """Seedance 2.0 API 客户端"""
    
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
        """从文本提示词生成视频"""
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
        """将静态图片转为视频"""
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
        """提交请求并轮询直到完成"""
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
                raise Exception(f"生成失败：{result['data'].get('error')}")
            time.sleep(interval)
            elapsed += interval
        raise TimeoutError(f"生成超时（{timeout}秒）")
```

> 💡 **[在 Atlas Cloud 上试用完整 API](https://www.atlascloud.ai/models/bytedance/seedance-2.0/text-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0) — 包含交互式 Playground 和代码示例。**

---

## 🔧 人像库 API

**基础 URL**：`https://console.atlascloud.ai/api/v1`

| 方法 | 路径 | 描述 |
|------|------|------|
| POST | `/sd/assets` | 从图片 URL 创建人像 |
| GET | `/sd/assets/:id` | 获取资产（处理中时自动轮询）|
| GET | `/sd/assets` | 列出资产（分页、可过滤）|
| PUT | `/sd/assets/:id` | 重命名资产 |
| DELETE | `/sd/assets/:id` | 移入回收站（可恢复）|
| GET | `/sd/assets/trash` | 列出回收站资产 |
| POST | `/sd/assets/:id/restore` | 从回收站恢复 |

**错误码**：200（成功）、400（无效请求）、401（认证错误）、404（未找到）、500（服务器错误）

---

## 🎨 Seedance 2.0 提示词工程指南

编写有效的提示词可以显著提升 Seedance 2.0 的输出质量。以下是按风格分类的经过验证的提示词模板。

### 电影风格提示词

**1. 黑色电影侦探场景**
```
一位私家侦探午夜独坐在雨水划过窗户的办公室里，香烟的烟雾向上袅袅升起，
百叶窗的阴影投在桌面上，镜头缓慢推进，黑色电影风格高对比度打光，
1940年代美学，忧郁的爵士配乐
```

**2. 史诗风景揭示**
```
航拍无人机镜头在日出时分从迷雾山峰上方升起，云雾在下方山谷中翻滚，
金色阳光照亮雪顶山峰，镜头先俯视再向前推进，恢宏的管弦乐配乐，
电影级画质
```

**3. 亲密对话场景**
```
两个朋友坐在咖啡馆桌子两侧，温暖的午后阳光穿过落地窗，一个人笑着听另一个人
讲故事，浅景深在两人面部之间切换，手持摄影机质感，环境咖啡馆声音配轻柔背景音乐
```

### 商业与产品提示词

**4. 产品展示**
```
一部精致的智能手机在反光黑色表面上缓慢旋转，工作室灯光带柔和轮廓光，
光粒子在设备周围漂浮，镜头平滑环绕，极简风格，高端科技美学
```

**5. 美食广告**
```
新鲜意面在滋滋作响的锅中翻炒，蒸汽升腾，香草在空中慢动作散落，
温暖的厨房顶光，微距特写然后拉远展示厨师，滋滋声效
```

### 社交媒体提示词

**6. 抖音风格转场**
```
一位穿着街头风的女性打了个响指，服装瞬间变换，城市天台黄金时段背景，
活力满满，镜头在响指时推进然后拉远展示新造型，9:16竖版，流行音乐
```

### 提示词编写要点

- **具体描述镜头运动**："镜头缓慢推进"比"镜头移动"效果更好
- **包含灯光细节**："温暖的黄金时段侧光"能营造氛围
- **使用 @引用系统**："@image1 中的角色走向 @image2，风格参考 @image3"
- **按层次描述**：主体 → 动作 → 环境 → 镜头 → 氛围 → 音频

---

## 💡 Seedance 2.0 使用技巧

### 获取最佳质量输出

1. **迭代用 720p，最终用 2K** — 低分辨率迭代节省时间和额度，满意后用 2K 重新生成
2. **始终描述镜头运动** — Seedance 2.0 的镜头控制是所有模型中最好的（9/10），充分利用它
3. **策略性启用音频** — 音频丰富效果但增加生成时间，快速迭代时可关闭
4. **真实主题用联网搜索** — 提示特定地点、名人或品牌内容时设置 `web_search: true`

### 进阶技巧

5. **多参考合成** — 用 @image1 控制角色、@image2 控制画风、@image3 控制背景
6. **视频链接** — 使用 `return_last_frame: true` 获取尾帧，输入到图生视频实现多镜头序列
7. **快速模型做分镜** — 用 Fast 模型生成 6-8 个变体，选最佳方向后用标准模型重新生成
8. **人像库批量工作流** — 注册多个人像，在同一场景中引用实现多角色场景

### 常见错误

- **不要直接上传真人面部** — 必须通过人像库
- **不要使用过短的提示词** — "一只猫"会得到通用结果，需要添加环境、灯光、镜头和氛围
- **不要对简单场景设置过长时长** — 单动作片段 4-6 秒最佳，长内容用链接
- **不要忘记宽高比** — 匹配平台需求（抖音用 9:16，YouTube 用 16:9）

---

## 📊 Seedance 2.0 与竞品对比

| 功能 | Seedance 2.0 | Kling 3.0 | Sora 2 | Veo 3.1 | Wan 2.7 |
|------|-------------|-----------|--------|---------|---------|
| **架构** | DiT | — | DiT | — | DiT |
| **综合评分** | **8.2/10** | 8.1/10 | — | 7.0/10 | — |
| **人像库** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **原生音频** | ✅ | ❌ | ✅ | ✅ | ✅ |
| **声音克隆** | ✅（3声音）| ❌ | ❌ | ❌ | ✅ |
| **联网搜索** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **最大分辨率** | **2K** | 4K/60fps | 1080p | 4K | 720p |
| **最大时长** | 15秒 | 2分钟 | 20秒 | 8秒 | 15秒 |
| **多参考** | **9图+3视频** | 1图 | N/A | 1参考 | 5参考 |
| **镜头控制** | **9/10** | 8/10 | 7/10 | 7/10 | — |
| **价格（10秒）** | **~$0.60** | ~$0.50 | ~$1.00 | ~$2.50 | ~$0.40 |

---

## 🔥 Seedance 2.0 与 Kling 3.0 详细对比

Seedance 2.0 和 Kling 3.0 是 2026 年两大领先的中国 AI 视频模型。

### 画面质量
- **Kling 3.0** 在原始画面保真度上更胜一筹，支持 4K/60fps 输出，画面质量评分 8.4/10
- **Seedance 2.0** 综合评分 8.2/10，但在多镜头生成中提供更好的一致性

### 镜头与可控性
- **Seedance 2.0** 以 9/10 的镜头控制评分遥遥领先——所有视频模型中最高
- Kling 3.0 镜头控制评分 8/10，表现出色但缺乏 Seedance 的精细导演控制

### 各自优势
- **Seedance 2.0**：人像库保持身份一致、联网搜索真实参考、12 路多模态输入、3 角色声音克隆
- **Kling 3.0**：更长视频（最长 2 分钟）、更高分辨率（4K/60fps）、运动笔刷精确控制

### 最佳使用场景
- 选择 **Seedance 2.0**：需要真人面部身份保持、复杂多参考场景、音视频联合生成、最大化镜头控制
- 选择 **Kling 3.0**：需要最高画面分辨率、长视频（>15秒）、简单单主体生成

---

## 📊 Seedance 2.0 与 1.5 Pro 对比

| 功能 | 2.0 | 1.5 Pro |
|------|-----|---------|
| 架构 | DiT | 上一代 |
| 分辨率 | **原生 2K** | 1080p |
| 人像库 | ✅ | ❌ |
| 联网搜索 | ✅ | ❌ |
| 声音克隆 | ✅（3 声音）| ❌ |
| 多参考 | 9图+3视频+音频 | 有限 |
| 视频编辑 | ✅ | ❌ |
| 时长 | 4-15秒 | 4-12秒 |
| 宽高比 | 7种+自适应 | 有限 |
| 镜头控制 | 9/10 | 基础 |
| NSFW | ❌ | ✅ |
| 价格 | $0.10/次 | $0.15-0.72 |

> NSFW 内容请在 Atlas Cloud 上使用 `bytedance/seedance-v1.5-pro/image-to-video-spicy`。

---

## 🔄 从 Seedance 1.5 迁移到 2.0

### API 变更

**模型 ID 更新：**
```python
# Seedance 1.5
"model": "bytedance/seedance-v1.5-pro/text-to-video"

# Seedance 2.0
"model": "bytedance/seedance-2.0/text-to-video"
```

**2.0 新增参数：**
```python
{
    "web_search": True,          # 新增：联网搜索
    "generate_audio": True,       # 新增：音视频联合生成
    "resolution": "2k",          # 新增：原生 2K
    "reference_images": [...],   # 新增：最多 9 张参考图
    "reference_videos": [...],   # 新增：最多 3 段参考视频
    "reference_audio": "...",    # 新增：音频驱动生成
}
```

### 需要修改的部分

1. **真人面部输入** — 需要先在人像库中注册，再通过 `asset://` URI 引用
2. **模型 ID** — 所有调用从 `seedance-v1.5-pro` 更新为 `seedance-2.0`
3. **NSFW 内容** — 2.0 不支持 Spicy 模式，继续使用 1.5 Pro

### 向后兼容

- 基本请求/响应结构不变
- 提示词格式不变
- 异步结果轮询机制相同
- 认证方式和 API 密钥格式不变

---

## 🎯 使用场景

- 🎭 **AI 代言人** — 注册面部，生成无限视频变体
- 📱 **社交媒体** — 抖音/YouTube/Instagram 的一致 AI 形象
- 🎓 **教育** — 跨语言声音克隆虚拟讲师
- 🛒 **电商** — 品牌代表的产品演示
- 📰 **新闻** — 使用注册人像资产的 AI 主播
- 🎬 **短片** — 导演级镜头控制下的一致角色
- 🎮 **游戏** — 从概念设定图生成角色介绍
- 🌐 **多语言** — 同一面部+不同语言声音克隆

---

## 📚 资源

### 官方
- 🌐 [Seedance 2.0 官方页面](https://seed.bytedance.com/en/seedance2_0)
- 📄 [发布博客](https://seed.bytedance.com/en/blog/official-launch-of-seedance-2-0)
- 📚 [维基百科](https://en.wikipedia.org/wiki/Seedance_2.0)
- 🎬 [CapCut/剪映集成](https://www.capcut.com/newsroom/dreamina-seedance-2)

### Atlas Cloud
- 🚀 [Seedance 2.0 文生视频](https://www.atlascloud.ai/models/bytedance/seedance-2.0/text-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0)
- 🚀 [Seedance 2.0 图生视频](https://www.atlascloud.ai/models/bytedance/seedance-2.0/image-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0)
- 🚀 [Seedance 2.0 参考生视频](https://www.atlascloud.ai/models/bytedance/seedance-2.0/reference-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0)

### 评测与分析
- 📰 [TechCrunch: Seedance 2.0 登陆 CapCut](https://techcrunch.com/2026/03/26/bytedances-new-ai-video-generation-model-dreamina-seedance-2-0-comes-to-capcut/)
- 📊 [WaveSpeedAI: SD 2.0 vs Kling vs Sora vs Veo](https://wavespeed.ai/blog/posts/seedance-2-0-vs-kling-3-0-sora-2-veo-3-1-video-generation-comparison-2026/)
- 📝 [BuildFastWithAI: SD 2.0 评测](https://www.buildfastwithai.com/blogs/seedance-2-bytedance-ai-video-2026)
- 📊 [Artificial Analysis 排行榜](https://artificialanalysis.ai/video/leaderboard/image-to-video)
- 🔬 [HuggingFace 技术分析](https://discuss.huggingface.co/t/seedance-2-0-technical-analysis-of-bytedances-multimodal-video-generation-model/174924)

---

## 常见问题

### 1. 为什么不能直接上传真人面部照片？

Seedance 2.0 执行内容安全策略。真人面部图片必须通过**人像库**进行预处理和验证。这既防止滥用，又支持合法的面部驱动内容创作。

### 2. Seedance 2.0 是 2026 年最好的视频模型吗？

在 Artificial Analysis 上综合评分 **8.2/10**——发布时最高。镜头控制最佳（9/10），多模态输入系统最强（12 路参考）。Kling 3.0 在画面保真度（8.4/10）和最大时长（2分钟）上领先。

### 3. 支持 NSFW 内容吗？

不支持。Seedance 2.0 通过人像库执行内容安全。如需无审查内容，请在 Atlas Cloud 上使用 **Seedance 1.5 Pro Spicy**（`bytedance/seedance-v1.5-pro/image-to-video-spicy`）。

### 4. 关于迪士尼版权争议？

2026 年 2 月 13 日，迪士尼向字节跳动发送了关于训练数据使用的停止侵权函。字节跳动回应表示尊重知识产权并将加强保护。用户应避免生成侵犯版权的内容。

### 5. 标准版与快速版——何时使用？

**快速版**：30-60 秒生成，适合预览和迭代。面部和高速运动场景有轻微质量损失。**标准版**：完整质量，需要数分钟。用于最终成品输出。

### 6. 可以拼接多个视频吗？

可以！设置 `return_last_frame: true` 获取尾帧，然后用它作为下一个 `image-to-video` 调用的首帧。

### 7. 如何获得最佳 API 生成效果？

编写详细提示词，包含主体、动作、环境、镜头运动、灯光和音频描述。使用 @引用系统进行多元素控制。先用 Fast 模型迭代，再用标准模型生成最终输出。

### 8. 可以用于商业项目吗？

可以。通过 API 生成的内容可商业使用，需遵守字节跳动服务条款。确保你对上传的参考图片拥有权利，尤其是在人像库中使用真人面部时。

---

<div align="center">

### [👉 在 Atlas Cloud 上试用 Seedance 2.0 — $0.10/视频，免费额度 👈](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0)

**由开源社区用 ❤️ 制作**

[⬆ 返回顶部](#-awesome-seedance-20--字节跳动影院级视频模型含人像库功能)

</div>
