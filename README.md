# Quickry AI Kit — 販売LP

**作成**: 2026-04-19 / 佐川睦男（AIエンジニア・LP/Web担当）
**最終更新**: 2026-04-29（AI幹部 → AI Kit リブランド対応・Phase 1）
**URL想定**: `ai-kit.quickry.jp`（サブドメイン推奨・坪井判断待ち） / 旧候補 `ai-os.quickry.jp` `ai-kanbu.quickry.jp`
**技術スタック**: 静的HTML + CSS + 素のJavaScript（フレームワークなし）

---

## ディレクトリ構成

```
lp/
├── index.html       ← メインLP（8セクション構成・草案v1準拠）
├── legal.html       ← 特定商取引法に基づく表記
├── privacy.html     ← プライバシーポリシー
├── style.css        ← 共通スタイル（ダークテーマ・レスポンシブ）
├── assets/          ← 画像素材（里見さんから受領後に配置）
└── README.md        ← このファイル
```

## 実装方針

- **静的HTML** で実装。Next.jsほど重い構成は不要なため、単一ファイルで完結させて高速デプロイ可能に
- **レスポンシブ対応**（モバイル360px〜、タブレット768px、PC1120px）を `style.css` 内でメディアクエリ実装
- **CTA設計**
  - Tier 1: `data-stripe-tier="1"` 属性で Stripe Checkout にフック可能。現状はプレースホルダ（決済リンク確定後に `window.location.href` を設定）
  - Tier 2 / Tier 3: `mailto:` でお問い合わせフォームに誘導（将来的にformsへ差し替え予定）
- **フォント**: Noto Sans JP（Google Fonts）＋ システムフォント fallback
- **アクセシビリティ**: `prefers-reduced-motion` 対応、セマンティックHTML、`aria-label`を必要箇所に付与

## 草案からの変更点（2026-04-19 オーナー確定分）

1. **返金保証の記載を削除** — Heroの「30日間返金保証」バッジを撤去。FAQの該当Q&Aは「ダウンロード販売のため原則返金不可」の文言に差し替え
2. FAQ 7問体制に再構成（景表法リスクのある断定表現を削除）
3. 特商法の返品・キャンセル条項を「デジタルコンテンツのため原則返金不可」「瑕疵対応は14日以内」の標準文言に統一

## 画像プレースホルダ（里見さんから受領予定）

- Hero背景ビジュアル（AI社員が会議している抽象イメージ・1920x1080）
- Overview「これがQuickry AI Kitです」スクリーンショット（Claude Code画面）
- Owner Card の坪井さん写真（160x160）→ 現状は「Y」のイニシャルSVG代替
- OGP画像（`assets/ogp.png`・1200x630）

**受領フォルダ想定**: `01_プロダクト/ai_os_distribution/lp/assets/`

## デプロイ手順（想定）

### 案A: Vercel（サブドメイン `ai-kit.quickry.jp` 推奨・坪井判断待ち）

```bash
cd lp
vercel --prod
# ドメイン設定でCNAMEを ai-kit.quickry.jp → cname.vercel-dns.com に
# ※旧URL候補 ai-os.quickry.jp / ai-kanbu.quickry.jp からのリダイレクト設定が必要
```

### 案B: Netlify

```bash
cd lp
netlify deploy --prod --dir=.
```

### 案C: Quickry Book LP と同じホスティングに相乗り

既存 `quickry.jp` の構成に `/ai-package` として組み込む（要・梶原CTO相談）。

## 今後のタスク

- [ ] 里見さんデザイン素材の受領 → 差し替え
- [ ] Stripe Checkout URL を Tier 1 CTAに配線（文学CFO管轄）
- [ ] お問い合わせフォーム（Google Forms or HubSpot）をTier 2/3 CTAに配線
- [ ] 田島法務の最終レビュー（景表法・返金ポリシー・ライセンス条項）
- [ ] OGP画像作成
- [ ] 本番デプロイ・DNS設定
- [ ] Google Analytics / Tag Manager 計測導入
- [ ] note記事・X発信との導線設計（佐川徳夫CMO協業）

## ローカル確認方法（2026-05-05 追記）

**重要**: `open lp/index.html` で直接開くと `file://` プロトコルになり、ブラウザによっては `<picture>` タグの画像読み込みが制限される場合があります。**必ず HTTPサーバー経由で確認してください**。

```bash
cd "01_プロダクト/ai_os_distribution/lp"
python3 -m http.server 8765
# ブラウザで http://localhost:8765/ を開く
```

本番Vercel公開後（`https://ai-kit.quickry.jp`）は HTTPS 配信なので、本問題は発生しません。

## 関連ドキュメント

- `01_プロダクト/ai_os_distribution/20260419_販売LP草案v1.md` — 原稿元
- `01_プロダクト/ai_os_distribution/_archive/履歴_仕様書/20260419_商品仕様書v1.md` — 商品仕様書
- `01_プロダクト/ai_os_distribution/CLAUDE.md` — 事業方針
