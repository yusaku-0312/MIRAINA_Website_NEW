# MIRAINA 設計定義書
## フレームワーク
プレーンなHTML, CSS, 一部JavaScript（ページネーションなど動的処理が必要な場合のみ）
## ファイルについて
### フォルダ構成
./
    index.html
    services.html
    about.html
    works.html
    blogs.html
    contact.html
    privacy_policy.html
    LLMO_Insight資料.pdf
    sitemap.xml
    robots.txt
    llms.txt
    services/
        ai_consulting.html
        ai_training.html
        ai_develop.html
        llmo_insight.html
    blogs/
        blog001.html
        blog002.html
    works/
        work001.html
        work002.html
        work003.html
        work004.html
    css/
        reset.css
        common.css
        index.css
        services.css
        about.css
        works.css
        blogs.css
        listing.css
        contact.css
        ai_consulting.css
        ai_training.css
        ai_develop.css
        llmo_insight.css
        work_article.css # works.html内で記載する事例紹介ページ（worksフォルダに格納されるファイル）に適用
        column_article.css # blogs.html内で記載する事例紹介ページ（blogsフォルダに格納されるファイル）に適用
        privacy_policy.css
    images/
				hero-mainimg.webp
				service-card004.webp
				llmo_insight_004.webp
				company-logo.webp # ヘッダー用アイコン
				service-card002.webp
				llmo_insight_003.webp
				llmo_insight_002.webp
				service-card003.webp
				original_ai_solution.webp
				llmo_insight_001.webp
				instagram-icon.webp
				column_background.webp
				ai-consulting-feature.webp
				ai-consulting-hero.webp
				suzuki.webp
				strategic_ai_implementation_service.webp
				ai_training_service.webp
				threads-icon.webp
				blogs/
				    blog-card001.webp
				    blog001-1.webp
				    blog001-2.webp
        works_images/
            work-card001.webp
            work001-1.webp
            work001-2.webp
    js/
        works.js
        listing.js
        services.js
        index.js
        llmo_search.js
        common.js
        hero-animation.js
    data/
        data.json # ページネーションのためのデータ（事例紹介記事とブログ記事）を格納
### data.json内のデータ構造
{
  "type": "object",
  "required": ["categories"],
  "properties": {
    "categories": {
      "type": "object",
      "additionalProperties": {
        "type": "array",
        "items": { "$ref": "#/$defs/ContentItem" }
      }
    }
  },
  "$defs": {
    "ContentItem": {
      "type": "object",
      "required": ["id", "title", "description", "thumbnail", "alt", "link", "date"],
      "properties": {
        "id": { "type": "integer" },
        "title": { "type": "string" },
        "description": { "type": "string" },
        "thumbnail": { "type": "string" },
        "alt": { "type": "string" },
        "link": { "type": "string" },
        "date": { "type": "string" }
      }
    }
  }
}
### ファイル命名規則
- blogs/以下のブログファイルについてはblog00X.htmlというファイル表記にする。
- works/以下の事例紹介ページついてはwork00X.htmlというファイル表記にする。
- imagesについて
	- blogs.html, works.html内に配置されるブログ紹介カードと事例紹介カードはblog-card00X.webp, work-card00X.wepbとする
## headタグ
### 実装目的
- 検索エンジンに正しく情報を伝え、SEO評価を最適化する。
- SNS共有時の表示品質を高め、クリック率を向上させる。
- ブランドの信頼性（E-E-A-T）を補強する。
- ページ表示の高速化とユーザビリティ向上を図る。
---
### 必須要件（HTML基本設定）
#### 文字コードの指定
- `meta charset="UTF-8"` を設定し、日本語が正常に表示されるようにする。
#### モバイル最適化
- `meta name="viewport" content="width=device-width, initial-scale=1.0"` を含め、モバイルでの表示を最適化する。
#### robots指示の明示
- `meta name="robots" content="index, follow"` を指定し、検索エンジンがページをクロールできる状態にする。
---
### SEOメタ情報の実装要件
#### タイトル設定
- `<title>` にブランド名＋主要サービスを記述。
- 文字数は30〜60文字程度を推奨。
#### メタディスクリプション
- `meta name="description"` にページ要点を簡潔（120〜150文字程度）で書く。
- 検索結果のCTR向上を目的とする。
#### keywords（補助的）
- `meta name="keywords"` にターゲットキーワードを設定（SEO直接効果は限定的）。
---
### URL正規化（Canonical）
#### 重複URLの評価統合
- `<link rel="canonical" href="https://miraina-ai.com/">` のように、正規URLを必ず明示する。
- パラメータ付きURL対策にもなる。
---
### SNS向けメタデータ（OGP / Twitter Card）
#### OGP設定
以下を必須で設定する：
- `og:title`
- `og:description`
- `og:type`（website）
- `og:url`
- `og:site_name`
※ SNSでリンクを共有した際の自動生成カードの品質向上が目的。
#### Twitter Card設定
- `twitter:card`（summary_large_image 推奨）
- `twitter:title`
- `twitter:description`
- `twitter:image`
SNSシェア時のクリック率向上に繋がる。
---
### 構造化データ（JSON-LD）
#### Organization Schema 要件
目的：企業の正式情報を検索エンジンに伝える（E-E-A-T向上）
- `@context`: "https://schema.org"
- `@type`: "Organization"
- `name`: 企業名
- `url`: 公式サイトURL
- `logo`: 正式ロゴURL
- `sameAs`: SNSリンク
- `contactPoint`:  
  - email  
  - contactType  
  - availableLanguage  
#### WebPage Schema 要件
目的：ページ内容を明確化し検索理解を向上
- `@type`: "WebPage"
- `name`: ページタイトル
- `description`: ページ説明
- `publisher`: Organization を紐づける
---
### 表示品質とブランド識別
#### ファビコン実装
- `<link rel="icon" href="/images/favicon.ico">`
- ブラウザタブ・検索結果でのブランド想起性を高める。
---
### スタイル関連（表示速度・UI安定）
#### CSS外部ファイル読み込み
- `reset.css`  
- `common.css`  
- 各ファイルに対応するcssファイル 
目的：レイアウト安定化と表示速度改善。
---
### セキュリティ・整合性要件（任意）
- OGP画像・ロゴURLは HTTPS を使用すること。
- JSON-LDは必ず `<script type="application/ld+json">` で記述する。
- 相対パスと絶対URLを混在させない（特に OGP 画像・canonical）。
---
### 運用上の要件
- 各ページごとに **title / description / WebPage schema の内容をページ固有のものに変更すること**。
- トップページだけでなく下層ページも canonical を適切に設定する。
- og:image はシェア時に重要なため明確に設定（最低 1200×630 推奨）。
## 挿入画像
- ファイルはwebpに統一
- altタグを必ず設定
- 画像は余白をしっかりと作った上で配置する
## ヘッダー構成
### ヘッダー項目
- サービス
	- 生成AI活用支援
	- AI研修
	- AI開発
	- LLMO Insight
- MIRAINAについて
- 事例紹介
- ブログ
- お問い合わせ
- ロボット系アイコン（llms.txtリンク埋め込み）
### その他要件
- ヘッダーはデスクトップ版では全て上記項目を全て露出
- モバイル版ではハンバーガーメニューにする
- ヘッダーのサービス項目はマウスオーバーで階層下の各サービスがプルダウン形式で降りてくるようにする
## フッター構成
### フッター項目
デスクトップ版
左：
MIRAINA
真ん中：
空欄
右：
サイトメニュー
- 私たちについて
- 事例紹介
- ブログ
- お問い合わせ
- プライバシーポリシー
SNS：
- Instagram
- Threads
右下端
- ロボットアイコン（llms.txtリンク埋め込み）
真ん中最下部
- MIRAINA All Rights Reserved.
## hタグ
- ページ内にh1タグは必ず一つ
- h1→h2→h3の流れで構造化された設計
## aタグ
- 文章中にリンクを埋め込む場合は、下線をつけてリンクであることを分かりやすくする。
- ヘッダー・フッター・CTAボタンなどにリンクを埋め込む場合は下線をつけずにデザインとしての綺麗さのみ優先する。
## common.cssについて
- このファイルではカラーパレットのプロパティ、フォントサイズの(rem単位が原則)プロパティ、CTAボタンのデザイン設定など全ページで基本的に共通のものを記述していく
- 各ファイルごとに異なる要件は各cssファイルに記述する
## ページネーションについて
- worksページとblogsページではページネーションを設ける
- ページネーションは各ページの上部と下部に設ける
- ページネーションのJSファイルはjsフォルダ内で実装する
## カードとは
- この定義書におけるカードとは事例紹介の各記事と各ブログ記事を指す
- このカードはindex.html, works.html, blogs.htmlに設ける
- カードのCSSコードは共通のものなので、common.cssに記述する
- works.html, blogs.htmlでは、ページネーションで遷移する各ページにこのカードを設置する。
- カードに関する情報はdata.jsonに記述する。
## 非機能要件
- メディアクエリでモバイルにも最適化する
- 可読性の高いクラス名・ID定義
- クラス名・IDは被らないようにする 
    - common.cssに書かれるクラス・ID以外は原則として先頭にindex-やservices-などそのファイル固有の役割を示す単語をつける