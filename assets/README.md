# lp/assets/ — Quickry AI Kit LP 画像配置先

**最終更新**: 2026-05-05 / 佐川睦男（Phase 3 画像配線）
**Phase 2 初版**: 2026-05-05（坪井CEO 16:51 hero / 20:30 experience 配置完了）

## 配置済ファイル（坪井CEO 配置）

| ファイル名 | サイズ | 状態 | 備考 |
|---|---|---|---|
| `hero_main_raw.png` | 原画 | 配置済（2026-05-05 18:59） | ChatGPT 4o image P-001 D案 B-bright |
| `section_experience_raw.png` | 原画 | 配置済（2026-05-05 20:30） | ChatGPT 4o image P-002 D案 B-bright |

## 里見デザイナー切り出し予定（5/8 中・Phase 3 と並行）

依頼文（2026-05-05 十兵衛経由）に基づき以下サイズへ切り出し。**サイズは依頼文を正本として確定**（旧 README の 1920×960 / 750×1334 表記から更新）。

| ファイル名 | サイズ | 元プロンプト | 用途 | HTML 配線 |
|---|---|---|---|---|
| `hero_main_1920x1080.jpg` | 1920×1080 | P-001 D案 | LP Hero Desktop（JPEGフォールバック） | `index.html#hero` `<picture><img>` |
| `hero_main_1920x1080.webp` | 1920×1080 | 同上 | LP Hero Desktop（軽量配信優先） | `index.html#hero` `<picture><source type="image/webp">` |
| `hero_main_mobile_750x420.jpg` | 750×420 | P-001 D案 横長クロップ | LP Hero Mobile JPEG fallback（≤768px） | `index.html#hero` `<source media="(max-width: 768px)" type="image/jpeg">` |
| `hero_main_mobile_750x420.webp` | 750×420 | P-001 D案 横長クロップ | LP Hero Mobile WebP優先（≤768px） | `index.html#hero` `<source media="(max-width: 768px)" type="image/webp">` |
| `ogp_1200x630.jpg` | 1200×630 | P-001 D案 OGP切り出し | OGP（X / Facebook / LINE） | `<meta property="og:image">` `<meta name="twitter:image">` |
| `x_header_1500x500.jpg` | 1500×500 | P-001 D案 横ワイドクロップ | X (Twitter) プロフィール背景 | X account（LP外配信） |
| `section_experience_1600x900.jpg` | 1600×900 | P-002 D案 | 体験セクション（JPEGフォールバック） | `index.html#experience` `<picture><img>` |
| `section_experience_1600x900.webp` | 1600×900 | 同上 | 体験セクション（軽量配信優先） | `index.html#experience` `<picture><source type="image/webp">` |
| `youtube_thumbnail_1280x720.jpg` | 1280×720 | P-002 D案 + テキスト | YouTubeサムネ | YouTube（LP外配信） |

## 生成プロンプト

`01_プロダクト/ai_os_distribution/報告/20260505_提案_LPトーン親しみ寄り画像調整_里見.md` §2 / `20260505_提案_LP_AI社員ミニチュア化D案_里見.md` §3-1 を参照。

詳細は `画像メタデータ.md` §2（P-001 / P-002）参照。

## 受領後の作業（里見デザイナー担当・5/8）

1. ChatGPT 4o生成画像（_raw.png）配置済 ✓
2. 観点A/B/C 目視チェック実施（→ `画像メタデータ.md` §3 にチェックボックス埋め）
3. Photoshop/Affinity Photo で Deep Teal カラーバランス調整（±5-10度の青→青緑シフト）
4. 各サイズへの切り出し（上記表参照）
5. JPEG/WebP 両形式で書き出し（picture要素のsrcsetで優先配信）
6. lp/assets/ へ配置 → 佐川睦男（梶原CTO配下）に動作確認依頼

## HTML 配線状態（Phase 3 完了 2026-05-05 佐川睦男）

| 配線箇所 | ステータス | 備考 |
|---|---|---|
| Hero `<picture>` | 配線済 | WebP優先 → JPEG フォールバック → モバイル分岐（≤768px） |
| Experience `<picture>` | 配線済 | WebP優先 → JPEG フォールバック / lazy loading |
| OGP `og:image` | 配線済 | `/assets/ogp_1200x630.jpg`（Phase 2 で更新済） |
| Twitter Card `twitter:image` | 配線済 | `/assets/ogp_1200x630.jpg`（Phase 2 で更新済） |
| JSON-LD `image` | 配線済 | `/assets/ogp_1200x630.jpg`（Phase 2 で更新済） |

里見の切り出しファイル配置後にローカルサーバーで実画像表示確認を行う（5/8-5/9）。

## 商用利用

ChatGPT画像のLP/OGP商用利用可否は田島法務並行確認中（2026-05-05時点）。確認OKまでローンチ画像差し替えは保留可。

## 元画像（_raw.png）取扱い

- `hero_main_raw.png` / `section_experience_raw.png` の **削除禁止**（5/15 ローンチまで保管）
- 切り出しファイル再生成のソースとして必要
- 田島法務 5/9 レビュー指摘で再切り出しが発生する場合の原本となる
