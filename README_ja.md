# 🎬 Awesome Seedance 2.0 — ByteDanceのシネマグレード動画生成モデル（ポートレートライブラリ搭載）

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Seedance 2.0](https://img.shields.io/badge/Seedance-2.0-blue.svg)](https://www.atlascloud.ai/models/bytedance/seedance-2.0/text-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0)
[![Try on Atlas Cloud](https://img.shields.io/badge/Try-Atlas%20Cloud-green.svg)](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

**Language / 言語:** [English](README.md) | [中文](README_zh.md) | 日本語 | [한국어](README_ko.md)

---

> 🔥 **Seedance 2.0** — ByteDanceのフラグシップ動画生成モデル。**Diffusion Transformer (DiT)** アーキテクチャ採用。総合スコア **8.2/10**（Veo 3、Wan、Klingを上回る）。ポートレートライブラリ（実在顔対応）、ネイティブ2K、音声動画同時生成、ボイスクローン、ウェブ検索、12入力マルチモーダル制御に対応。**Atlas Cloudで$0.10/リクエスト。**

---

## 目次

- [Seedance 2.0の新機能](#seedance-20の新機能)
- [ベンチマーク・ランキング](#-ベンチマークランキング)
- [ポートレートライブラリ — 実在顔サポート](#-ポートレートライブラリ--実在顔サポート)
- [コア機能の詳細](#-コア機能の詳細)
- [Atlas Cloudのモデル一覧](#-atlas-cloudのモデル一覧)
- [APIクイックスタート](#-apiクイックスタート)
- [完全APIチュートリアル](#-完全apiチュートリアル)
- [ポートレートライブラリAPI](#-ポートレートライブラリapi)
- [プロンプトエンジニアリングガイド](#-プロンプトエンジニアリングガイド)
- [Seedance 2.0 vs 競合モデル](#-seedance-20-vs-競合モデル)
- [Seedance 2.0 vs 1.5 Pro](#-seedance-20-vs-15-pro)
- [ユースケース](#-ユースケース)
- [リソース](#-リソース)
- [FAQ](#faq)

---

## Seedance 2.0の新機能

ByteDanceが**2026年2月12日**にリリースしたSeedance 2.0は、動画AIにおける世代交代を象徴するモデルです：

- **アーキテクチャ**：Diffusion Transformer (DiT) — U-Netに代わり、優れたスケーラビリティを実現
- **統合マルチモーダル**：テキスト・画像・動画・音声からの音声動画同時生成
- **ネイティブ2K**：2048×1080（横）/ 1080×2048（縦）— 1080pからアップグレード
- **ポートレートライブラリ**：専用の実在顔アセット管理システムを搭載した初の主要モデル
- **ボイスクローン**：シーンあたり最大3つのカスタムキャラクターボイス
- **ウェブ検索**：生成中にリアルタイムでインターネット参照を取得
- **CapCut統合**：2026年3月26日よりCapCutでグローバルに利用可能
- **内部ベンチマーク**：SeedVideoBench-2.0（指示遵守、動き品質、美学、音声をカバー）

---

## 📊 ベンチマーク・ランキング

### Artificial Analysisリーダーボード

| 指標 | スコア | ランキング |
|------|--------|-----------|
| **テキスト→動画 Elo** | 1,273 | Top 3（720p） |
| **画像→動画 Elo** | 1,355 | Top 3（720p） |
| **総合スコア** | **8.2/10** | リリース時1位 |
| **カメラ制御** | **9/10** | 全モデル1位 |
| **クリエイティブ制御** | 5/5 | トップティア |
| **音声同期** | 5/5 | トップティア |

### モデル比較

| モデル | 総合 | カメラ | 音声 |
|--------|------|--------|------|
| **Seedance 2.0** | **8.2** | **9/10** | **5/5** |
| Google Veo 3 | 7.0 | 7/10 | 5/5 |
| Alibaba Wan 2.2 | 5.6 | — | — |
| Kuaishou Kling 2.1 | 4.4 | — | — |

> Seedance 2.0は**VBench-2.0**に収録され、Veo 3、Vidu、Wan、Klingと共に評価されています。

---

## 🎭 ポートレートライブラリ — 実在顔サポート

### 課題
Seedance 2.0は安全性コンプライアンスのため、**標準入力で送信された実在顔画像をブロック**します。実在人物の写真を直接ペーストすることはできません。

### 解決策：ポートレートライブラリ
専用のアセット管理システムです：

1. ポートレート画像を**登録** → 前処理と検証
2. ステータスを**確認**：`Processing → Active`
3. 任意の画像フィールドで `asset://<asset_id>` を使用して**参照**
4. **アイデンティティ一貫性のある**動画結果を生成

### 画像要件

| 仕様 | 値 |
|------|-----|
| フォーマット | JPEG、PNG、WebP、BMP、TIFF、GIF、HEIC |
| サイズ | 各辺 300 – 6,000 px |
| アスペクト比 | 0.4 – 2.5 |
| 最大サイズ | 30 MB |

### Playgroundでの使用方法

1. 画像入力エリアの**ポートレートライブラリ**を開く
2. ポートレートを**アップロード**し、前処理を待つ
3. 処理済みポートレートを**選択** → 参照として利用可能
4. プロンプトを記述して生成！

> **ヒント**：Playground横の**「API」タブ**でリクエスト例とSDKスニペットを確認できます。**「Copy for LLM」**でAIコーディングアシスタント経由の統合を素早く構築できます。

---

## ✨ コア機能の詳細

### 🔊 ネイティブ音声動画同時生成
単一推論で動画＋同期音声（セリフ、効果音、音楽）を生成。中国語、英語、スペイン語などでの自動リップシンクに対応。ステレオ出力。

### 🗣️ ボイスクローン
実際の音声サンプルをアップロードしてトーン、アクセント、表情をガイド。シーンあたり最大**3つのカスタムキャラクターボイス**に対応。

### 🌐 ウェブ検索（Seedance 2.0限定）
`web_search: true` でリアルタイムのインターネット参照を取得。モデルが学習していない特定の人物、場所、スタイルに最適。

### 🖼️ 12入力マルチモーダル制御（@参照システム）
`@` システムで参照をプロンプト要素にバインド：
- 最大**9枚の参照画像**（キャラクター、スタイル、シーン）
- 最大**3本の参照動画**（合計≤15秒）で編集/延長
- **1つの参照音声**で音声駆動生成
- プロンプト例：「@image1のキャラクターが@image2のスタイルで@audio1に合わせて踊る」

### 🎬 ディレクターレベルのカメラ制御
本物の映画監督のようにカメラを制御：
- プッシュ/プルズーム、フォーカスプル
- トラッキングショット、POV切替
- 手持ち揺れエフェクト
- カメラ制御スコア **9/10**（全モデル中最高）

### ✂️ 動画編集
- 既存動画の延長
- モーション参照の適用
- オブジェクト除去
- ビジュアルエフェクトの追加

### 📐 出力仕様
- **解像度**：ネイティブ2K（2048×1080 / 1080×2048）、720p、480p
- **長さ**：4-15秒、マルチショットで自然なトランジション
- **アスペクト比**：16:9、4:3、1:1、3:4、9:16、21:9、アダプティブ
- **最終フレーム返却**：動画のシームレスなチェーン

---

## 💰 Atlas Cloudのモデル一覧

| モデル | ID | 価格 |
|--------|-----|------|
| **テキスト→動画** | `bytedance/seedance-2.0/text-to-video` | $0.10/回 |
| **画像→動画** | `bytedance/seedance-2.0/image-to-video` | $0.10/回 |
| **参照→動画** | `bytedance/seedance-2.0/reference-to-video` | $0.10/回 |
| **高速 T2V** | `bytedance/seedance-2.0-fast/text-to-video` | $0.10/回 |
| **高速 I2V** | `bytedance/seedance-2.0-fast/image-to-video` | $0.10/回 |
| **高速 Ref2V** | `bytedance/seedance-2.0-fast/reference-to-video` | $0.10/回 |

> 高速モデルは30-60秒で5-10秒の動画を生成（標準は数分）。他プラットフォームより約33%安く、Atlas Cloudでは統一価格。

---

## ⚡ APIクイックスタート

### テキスト→動画（Python）

```python
import requests, time

API_KEY = "your-atlas-cloud-api-key"
H = {"Authorization": f"Bearer {API_KEY}", "Content-Type": "application/json"}

r = requests.post("https://api.atlascloud.ai/api/v1/model/prediction", headers=H, json={
    "model": "bytedance/seedance-2.0/text-to-video",
    "prompt": "若い映画製作者がヴィンテージモニターで映像を確認する、温かいスタジオ照明、映画的なグレイン",
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
        print("動画URL:", res["data"]["outputs"][0])
        break
    elif res["data"]["status"] == "failed":
        print("エラー:", res["data"].get("error"))
        break
    time.sleep(5)
```

### ポートレート参照→動画

```python
# ポートレートライブラリに登録後（asset_id = "ark-xxxxx"）
r = requests.post("https://api.atlascloud.ai/api/v1/model/prediction", headers=H, json={
    "model": "bytedance/seedance-2.0/reference-to-video",
    "reference_images": ["asset://ark-xxxxx"],
    "prompt": "画像1の人物がTEDトークで登壇、自信あるジェスチャー、聴衆の拍手",
    "duration": 12,
    "generate_audio": True
})
```

> 💡 **[Atlas CloudでAPIキーを取得](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0) — 無料クレジット、クレジットカード不要！**

---

## 📘 完全APIチュートリアル

### ステップ1：APIキーを取得

1. [Atlas Cloud](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0)に登録
2. **Settings → API Keys** に移動
3. **Create API Key** をクリックして安全に保存
4. 無料クレジットですぐに実験開始可能

### ステップ2：依存関係をインストール

```bash
pip install requests python-dotenv
```

### ステップ3：再利用可能なクライアントを構築

```python
import requests, time, os
from dotenv import load_dotenv

load_dotenv()

class SeedanceClient:
    """Seedance 2.0 APIクライアント"""
    
    BASE_URL = "https://api.atlascloud.ai/api/v1/model/prediction"
    
    def __init__(self):
        self.api_key = os.getenv("ATLASCLOUD_API_KEY")
        self.headers = {
            "Authorization": f"Bearer {self.api_key}",
            "Content-Type": "application/json"
        }
    
    def text_to_video(self, prompt, duration=10, resolution="720p",
                      ratio="16:9", audio=True):
        """テキストプロンプトから動画を生成"""
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
        """静止画像を動画に変換"""
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
        """リクエスト送信と完了までポーリング"""
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
                raise Exception(f"生成失敗：{result['data'].get('error')}")
            time.sleep(interval)
            elapsed += interval
        raise TimeoutError(f"生成タイムアウト（{timeout}秒）")
```

> 💡 **[Atlas Cloudで完全なAPIを試す](https://www.atlascloud.ai/models/bytedance/seedance-2.0/text-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0) — インタラクティブPlaygroundとコードスニペット付き。**

---

## 🔧 ポートレートライブラリAPI

**ベースURL**：`https://console.atlascloud.ai/api/v1`

| メソッド | パス | 説明 |
|---------|------|------|
| POST | `/sd/assets` | 画像URLからポートレートを作成 |
| GET | `/sd/assets/:id` | アセットを取得（処理中は自動ポーリング）|
| GET | `/sd/assets` | アセット一覧（ページネーション、フィルター対応）|
| PUT | `/sd/assets/:id` | アセットの名前変更 |
| DELETE | `/sd/assets/:id` | ゴミ箱に移動（復元可能）|
| GET | `/sd/assets/trash` | ゴミ箱のアセット一覧 |
| POST | `/sd/assets/:id/restore` | ゴミ箱から復元 |

---

## 🎨 プロンプトエンジニアリングガイド

### シネマティックスタイル

**1. フィルムノワール探偵シーン**
```
深夜、雨粒が窓を伝う事務所で一人座る私立探偵、煙草の煙が漂う、
ブラインドの影がデスクに落ちる、カメラがゆっくりドリーイン、
フィルムノワールの高コントラスト照明、1940年代の美学、憂鬱なジャズスコア
```

**2. 壮大な風景ショット**
```
日の出の霧に包まれた山々の上空をドローンが上昇、雲が谷間を流れる、
金色の光が雪を被った山頂を照らす、カメラが見下ろしてから前進、
壮大なオーケストラスコア、映画級の品質
```

**3. 商品紹介**
```
反射する黒い表面でスマートフォンがゆっくり回転、ソフトなリムライトの
スタジオ照明、光の粒子がデバイスの周りを漂う、カメラが滑らかに周回、
ミニマリストスタイル、プレミアムテック美学
```

### プロンプト作成のコツ

- **カメラの動きを具体的に記述**：「カメラがゆっくりドリーフォワード」は「カメラが動く」よりはるかに効果的
- **照明の詳細を含める**：「温かいゴールデンアワーのサイドライト」でムードを演出
- **@参照システムを活用**：「@image1のキャラクターが@image2のスタイルで歩く」
- **レイヤーで記述**：被写体 → 動作 → 環境 → カメラ → ムード → 音声

---

## 📊 Seedance 2.0 vs 競合モデル

| 機能 | Seedance 2.0 | Kling 3.0 | Sora 2 | Veo 3.1 | Wan 2.7 |
|------|-------------|-----------|--------|---------|---------|
| **アーキテクチャ** | DiT | — | DiT | — | DiT |
| **総合スコア** | **8.2/10** | 8.1/10 | — | 7.0/10 | — |
| **ポートレートライブラリ** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **ネイティブ音声** | ✅ | ❌ | ✅ | ✅ | ✅ |
| **ボイスクローン** | ✅（3声） | ❌ | ❌ | ❌ | ✅ |
| **ウェブ検索** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **最大解像度** | **2K** | 4K/60fps | 1080p | 4K | 720p |
| **最大長さ** | 15秒 | 2分 | 20秒 | 8秒 | 15秒 |
| **マルチ参照** | **9画像+3動画** | 1画像 | N/A | 1参照 | 5参照 |
| **カメラ制御** | **9/10** | 8/10 | 7/10 | 7/10 | — |
| **価格（10秒）** | **~$0.60** | ~$0.50 | ~$1.00 | ~$2.50 | ~$0.40 |

---

## 📊 Seedance 2.0 vs 1.5 Pro

| 機能 | 2.0 | 1.5 Pro |
|------|-----|---------|
| アーキテクチャ | DiT | 前世代 |
| 解像度 | **ネイティブ2K** | 1080p |
| ポートレートライブラリ | ✅ | ❌ |
| ウェブ検索 | ✅ | ❌ |
| ボイスクローン | ✅（3声） | ❌ |
| マルチ参照 | 9画像+3動画+音声 | 限定的 |
| 動画編集 | ✅ | ❌ |
| 長さ | 4-15秒 | 4-12秒 |
| アスペクト比 | 7種+アダプティブ | 限定的 |
| カメラ制御 | 9/10 | 基本 |
| NSFW | ❌ | ✅ |
| 価格 | $0.10/回 | $0.15-0.72 |

> NSFW：Atlas Cloudで `bytedance/seedance-v1.5-pro/image-to-video-spicy` を使用。

---

## 🎯 ユースケース

- 🎭 **AIスポークスパーソン** — 顔を登録して無制限の動画バリエーションを生成
- 📱 **ソーシャルメディア** — TikTok/YouTube/Instagram向けの一貫したAIアバター
- 🎓 **教育** — 多言語ボイスクローン対応のバーチャル講師
- 🛒 **EC** — ブランド担当者による商品デモ
- 📰 **ニュース** — ポートレートアセットを使用したAIアンカー
- 🎬 **短編映画** — ディレクターレベルのカメラ制御による一貫したキャラクター
- 🎮 **ゲーム** — コンセプトアートからキャラクター紹介
- 🌐 **多言語** — 同じ顔＋異なる言語でのボイスクローン

---

## 📚 リソース

### 公式
- 🌐 [Seedance 2.0公式ページ](https://seed.bytedance.com/en/seedance2_0)
- 📄 [リリースブログ](https://seed.bytedance.com/en/blog/official-launch-of-seedance-2-0)
- 📚 [Wikipedia](https://en.wikipedia.org/wiki/Seedance_2.0)
- 🎬 [CapCut統合](https://www.capcut.com/newsroom/dreamina-seedance-2)

### Atlas Cloud
- 🚀 [Seedance 2.0 T2V](https://www.atlascloud.ai/models/bytedance/seedance-2.0/text-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0)
- 🚀 [Seedance 2.0 I2V](https://www.atlascloud.ai/models/bytedance/seedance-2.0/image-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0)
- 🚀 [Seedance 2.0 Ref2V](https://www.atlascloud.ai/models/bytedance/seedance-2.0/reference-to-video?utm_source=github&utm_campaign=awesome-seedance-2.0)

### レビュー・分析
- 📰 [TechCrunch: Seedance 2.0がCapCutに](https://techcrunch.com/2026/03/26/bytedances-new-ai-video-generation-model-dreamina-seedance-2-0-comes-to-capcut/)
- 📊 [WaveSpeedAI: SD 2.0 vs Kling vs Sora vs Veo](https://wavespeed.ai/blog/posts/seedance-2-0-vs-kling-3-0-sora-2-veo-3-1-video-generation-comparison-2026/)
- 📝 [BuildFastWithAI: SD 2.0レビュー](https://www.buildfastwithai.com/blogs/seedance-2-bytedance-ai-video-2026)
- 📊 [Artificial Analysisリーダーボード](https://artificialanalysis.ai/video/leaderboard/image-to-video)

---

## FAQ

### 1. なぜ実在の顔写真を直接アップロードできないのですか？

Seedance 2.0はコンテンツ安全ポリシーを適用しています。実在顔画像は**ポートレートライブラリ**で前処理と検証が必要です。これにより悪用を防ぎつつ、正当な顔駆動コンテンツの作成を可能にしています。

### 2. Seedance 2.0は2026年最高の動画モデルですか？

Artificial Analysisで総合スコア**8.2/10**を記録——リリース時点で最高。カメラ制御が最高（9/10）、マルチモーダル入力が最強（12参照）。Kling 3.0は映像品質（8.4/10）と最大長さ（2分）でリード。

### 3. NSFWコンテンツに対応していますか？

いいえ。Seedance 2.0はポートレートライブラリによるコンテンツ安全を適用。無制限コンテンツにはAtlas Cloudの**Seedance 1.5 Pro Spicy**（`bytedance/seedance-v1.5-pro/image-to-video-spicy`）を使用してください。

### 4. 標準版 vs 高速版 — どちらを使うべき？

**高速版**：30-60秒で生成、プレビューやイテレーションに最適。顔やハイモーションシーンに若干の品質低下。**標準版**：フル品質、数分かかります。最終出力に使用。

### 5. 複数の動画をチェーンできますか？

はい！`return_last_frame: true` で最終フレームを取得し、次の `image-to-video` 呼び出しの最初のフレームとして使用してください。

### 6. 商業プロジェクトに使えますか？

はい。APIを通じて生成されたコンテンツは、ByteDanceの利用規約に従って商業利用可能です。参照画像の権利を確認してください。

---

<div align="center">

### [👉 Atlas CloudでSeedance 2.0を試す — $0.10/動画、無料クレジット 👈](https://www.atlascloud.ai?utm_source=github&utm_campaign=awesome-seedance-2.0)

**オープンソースコミュニティが❤️で制作**

[⬆ トップに戻る](#-awesome-seedance-20--bytedanceのシネマグレード動画生成モデルポートレートライブラリ搭載)

</div>
