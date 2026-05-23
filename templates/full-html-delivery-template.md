# full-html-delivery-template

> このテンプレートは、CMS本文貼り付けを前提としたHTML納品用です。  
> html / head / body タグは基本的に使用しません。  
> title / meta description / meta keywords は本文HTMLに含めません（管理画面入力で対応）。

---

## A. 納品パッケージ（必須）

1. ダウンロードできるHTMLファイル（`*.html`）
2. 管理画面入力用
   - タイトル
   - H1
   - ディスクリプション
   - キーワード
   - 短めの商品グループコメント
3. 本文HTML
4. 画像プレースホルダー一覧
5. 内部リンク設計メモ
6. 重複確認メモ
7. 公開前チェックリスト

---

## B. ページ基本情報（記入欄）

- ページID：
- 対象カテゴリー：
- 想定URL：
- ページ種別（親/子）：
- 想定読者：
- 目的：
- 関連既存ページ：
- 作成日：
- 更新日：
- 作成者：
- 確認者：

---

## C. 管理画面入力用（記入欄）

- タイトル：
- H1：
- ディスクリプション：
- キーワード：
- 短めの商品グループコメント：

補足ルール：
- 料金に関する詳細案内は`/price`へ誘導する。
- 店舗選択は`/salon`または3店舗カードへ誘導する。
- 予約導線は`/app`へ誘導する。
- 予約可否は断定しない。  
  例：「空き状況は予約画面または公式アプリでご確認ください。」

---

## D. 本文構成（設計メモ）

1. 導入（悩み・目的の明確化）
2. 結論・選び方の要点
3. 比較・詳細説明
4. よくある質問（FAQ）
5. 店舗案内（3店舗均等）
6. 料金確認導線（`/price`）
7. 予約導線（`/app`）

---

## E. 本文HTML（貼り付け用）

注意：
- 本文HTMLに `html/head/body` タグは入れない。
- 本文HTMLに `title/meta description/meta keywords` は入れない。
- H1は管理画面入力用。本文HTMLに `<h1>` は入れない。
- ファーストビュー大見出しは必要に応じて `role="heading" aria-level="1"` を利用する。
- class名はページ固有プレフィックスを使用する（例：`spc-`）。
- CSSとJSON-LDは `{literal}` と `{/literal}` で囲む。
- JSON-LDは表示本文と矛盾しない場合のみ使う。
- FAQPageを使う場合は、ページ内に実際に表示しているFAQと一致させる。

```html
<!-- 例：ページ固有プレフィックス spc-（SignPost Catalogの例） -->

<section class="spc-wrap">
  <div class="spc-hero">
    <div class="spc-hero-title" role="heading" aria-level="1">
      ここにファーストビューの大見出し
    </div>
    <p class="spc-hero-lead">
      ここに導入文（お客様向けの自然な表現）
    </p>
  </div>

  <section class="spc-section">
    <h2>ここに見出し</h2>
    <p>ここに本文。</p>
  </section>

  <section class="spc-faq">
    <h2>よくあるご質問</h2>
    <dl>
      <dt>質問テキスト</dt>
      <dd>回答テキスト</dd>
    </dl>
  </section>

  <section class="spc-shop-cards">
    <h2>店舗を選ぶ</h2>
    <div class="spc-shop-grid">
      <article class="spc-shop-card">
        <h3>池袋東口店</h3>
        <p>店舗案内テキスト</p>
      </article>
      <article class="spc-shop-card">
        <h3>志木店</h3>
        <p>店舗案内テキスト</p>
      </article>
      <article class="spc-shop-card">
        <h3>ふじみ野店</h3>
        <p>店舗案内テキスト</p>
      </article>
    </div>
  </section>

  <section class="spc-cta">
    <p>料金はメニュー・料金ページでご確認いただけます。</p>
    <p>空き状況は予約画面または公式アプリでご確認ください。</p>
    <ul>
      <li><a href="/price">メニュー・料金を見る</a></li>
      <li><a href="/salon">店舗を選ぶ</a></li>
      <li><a href="/app">予約・公式アプリ</a></li>
    </ul>
  </section>
</section>

{literal}
<style>
  .spc-wrap { max-width: 960px; margin: 0 auto; padding: 24px 16px; }
  .spc-hero-title { font-size: 32px; line-height: 1.4; font-weight: 700; margin-bottom: 12px; }
  .spc-shop-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; }
  .spc-shop-card { border: 1px solid #ddd; border-radius: 12px; padding: 16px; }
  .spc-cta ul { list-style: none; margin: 0; padding: 0; display: grid; gap: 8px; }

  /* PC想定: 1440px / SP想定: 390px */
  @media (max-width: 768px) {
    .spc-hero-title { font-size: 24px; }
    .spc-shop-grid { grid-template-columns: 1fr; } /* スマホで1カラム */
  }
</style>
{/literal}

{literal}
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "質問テキスト",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "回答テキスト"
      }
    }
  ]
}
</script>
{/literal}
```

---

## F. 画像プレースホルダー一覧（記入欄）

ルール：
- 画像は自動生成しない。
- `img` の `src` は空（`src=""`）にする。
- `alt` は、どのような画像を入れるべきかを日本語で具体的に書く。
- 主要画像は3:2比率を基本とする。
- ファーストビュー画像は `loading="eager"`、それ以外は `loading="lazy"` を基本にする。
- 美容系ページでは、リアルな目元写真・人物写真・サロン写真の雰囲気を優先する。

```html
<!-- ファーストビュー画像 -->
<img
  src=""
  alt="自然光で撮影した、清潔感のあるサロン内観と笑顔の女性スタッフのイメージ写真（3:2）"
  width="1200"
  height="800"
  loading="eager"
/>

<!-- デザイン比較画像 -->
<img
  src=""
  alt="同じモデルでカールや長さの違いを比較できる、目元の仕上がり例コラージュ（3:2）"
  width="1200"
  height="800"
  loading="lazy"
/>

<!-- 店舗案内画像 -->
<img
  src=""
  alt="池袋東口店・志木店・ふじみ野店の外観または受付の雰囲気が分かる写真（3:2）"
  width="1200"
  height="800"
  loading="lazy"
/>
```

---

## G. 内部リンク設計メモ（記入欄）

- 主導線1（料金）：`/price`
- 主導線2（店舗）：`/salon`
- 主導線3（予約）：`/app`
- 関連導線：
- 置き場所（本文内のどこか）：
- アンカー文案：
- 設置理由：

---

## H. 重複確認メモ（記入欄）

- 競合候補URL：
- 本ページの主テーマ：
- 競合候補の主テーマ：
- 住み分け方針：
- 差別化要素：
- canonical/noindex検討メモ（実装指示は書かない）：

---

## I. 公開前チェックリスト（必須）

- [ ] 管理画面入力（タイトル/H1/説明/キーワード/コメント）が揃っている
- [ ] 本文HTMLに `<h1>` が入っていない
- [ ] html / head / body タグが入っていない
- [ ] title / meta情報が本文HTMLに入っていない
- [ ] CSSとJSON-LDが `{literal}` と `{/literal}` で囲まれている
- [ ] class名にページ固有プレフィックスを使用している
- [ ] 料金導線が`/price`に接続している
- [ ] 店舗導線が`/salon`または3店舗カードに接続している
- [ ] 予約導線が`/app`に接続している
- [ ] 予約可否を断定していない
- [ ] 「空き状況は予約画面または公式アプリでご確認ください」の案内がある
- [ ] 3店舗が均等に扱われている
- [ ] 禁止表現（安い/激安/必ず似合う/必ず改善する/当日予約できます等）がない
- [ ] 画像の`src`が空で、`alt`が具体的に記述されている
- [ ] ファーストビュー画像は`loading="eager"`、その他は`loading="lazy"`
- [ ] スマホ表示でカード・CTA・FAQ・店舗カードが1カラムになっている
