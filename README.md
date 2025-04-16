# 街と珈琲 EC

## 📖 プロジェクト概要

"街と珈琲" は愛知・名古屋にあるスペシャルティコーヒー専門店の EC サイトです。

* 商品一覧・詳細、カート、決済（Stripe Checkout）
* 定期便サブスクリプション
* CMS（microCMS）でのコンテンツ管理
* 会員認証・アカウント管理（Better Auth + Drizzle + Cloudflare D1）
* メール送信（Resend）
* 画像ストレージ（Cloudflare R2）
* SSR（React Router v7 Framework Mode） + Edge デプロイ（Cloudflare Workers）
* UI コンポーネント（Base UI） + テーマトークン（青空ブルー／白背景）
* コード品質（Biome）・テスト（Vitest + Playwright）

## 🏗️ システム構成図

```
      ブラウザ
         │
   Vite SSR │ (Streaming SSR via React Router v7)
         ▼
Cloudflare Workers ──┐
        │             │
  ┌─────┴─────┐   ┌───┴────┐   ┌──────────┐
  │ Cloudflare│   │  D1 DB │   │ microCMS │
  │   R2      │   │        │   │  (API)   │
  └───────────┘   └────────┘   └──────────┘
         │             │              │
         ▼             ▼              ▼
    商品画像       ユーザ／認証      コンテンツ
                    (Better Auth)

外部サービス:
- Stripe (決済)
- Resend (メール)
```

## ⚙️ 技術スタック

| レイヤー       | 主な技術                                        |
|---------------|------------------------------------------------|
| フレームワーク | Vite + React Router v7 (Framework Mode, SSR)    |
| UI             | Base UI, Tailwind CSS (テーマトークン管理)       |
| CMS            | microCMS (Freeプラン)                           |
| 認証・DB       | Better Auth + Drizzle ORM + Cloudflare D1       |
| ストレージ     | Cloudflare R2 (商品画像)                        |
| 決済           | Stripe Checkout + Webhook                      |
| メール         | Resend 無料枠                                    |
| テスト         | Vitest (ユニット/コンポーネント) + Playwright (E2E) |
| コード品質     | Biome (Lint / Formatter)                        |
| CI/CD          | GitHub Actions → Cloudflare Pages/Workers       |

## 🗺️ 実装ロードマップ（Issue 化予定）

1. プロジェクトスキャフォールド
   - Vite + React Router v7 Framework Mode テンプレート
   - GitHub リポジトリに初期コミット & CI 設定
2. テーマ設計
   - カラートークン（青空ブルー / 白背景）定義
   - Tailwind / Base UI 連携
3. ルート＆ページ構成
   - `src/routes/index.tsx` (ホーム)
   - `src/routes/products/[slug].tsx` (商品詳細)
4. microCMS クライアント実装
   - 認証ヘッダー管理
   - 商品リスト・スラッグ取得
5. 認証基盤構築
   - Better Auth + Drizzle + D1 セットアップ
   - メールテンプレート (Resend)
6. 決済フロー実装
   - Stripe Checkout → Webhook ハンドラ
   - 注文情報 D1 保存 → 確定メール送信
7. 画像管理
   - R2 バケット運用／キャッシュ設定
8. テスト基盤整備
   - Biome, Vitest, Playwright の設定
9. キャッシュ戦略設計
   - Cloudflare Cache API / SWR リフェッチ制御
10. 国際化・通貨フォーマット設計

## 🚀 開発環境

```bash
git clone git@github.com:YOUR_ORG/machi-to-coffee-ec.git
cd machi-to-coffee-ec
pnpm install
cp .env.example .env
# 必要変数を設定:
# VITE_MICROCMS_API_KEY, VITE_MICROCMS_SERVICE_DOMAIN
# RESEND_API_KEY, STRIPE_PUBLISHABLE_KEY, STRIPE_SECRET_KEY
# D1 の接続設定
pnpm dev
```
