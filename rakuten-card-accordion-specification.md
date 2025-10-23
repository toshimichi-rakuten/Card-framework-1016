# 楽天カードフレームワーク Accordion コンポーネント仕様書

## 概要

楽天カードフレームワークのAccordionコンポーネントは、展開・折りたたみ可能なコンテンツパネルを提供するUIコンポーネントです。
ユーザーがヘッダーをクリックすることで、関連するコンテンツを表示/非表示できます。

## 必要な依存関係

### CSS
```html
<link rel="stylesheet" href="https://static.card.jp.rakuten-static.com/card_corp/pc/css/common/framework/rakuten-card-framework-4.0.0.min.css">
<link rel="stylesheet" href="https://static.card.jp.rakuten-static.com/card_corp/pc/css/common/iconfont/rakuten-card-icon-5.0.0.min.css">
```

### JavaScript
```html
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<script src="https://static.card.jp.rakuten-static.com/card_corp/pc/js/common/framework/5.0.0/accordion.min.js"></script>
```

## 基本的なHTML構造

### Accordionコンテナ
```html
<div class="accordion" id="accordionExample">
  <!-- アコーディオンアイテム -->
</div>
```

### Accordion Item（基本構造）
```html
<div class="accordion-item">
  <h2 class="accordion-header">
    <button
      class="accordion-button"
      type="button"
      data-toggle="accordion"
      data-target="#collapseId"
      aria-controls="collapseId"
      aria-expanded="false"
    >
      <span class="accordion-button-text">アコーディオンタイトル</span>
      <span class="accordion-button-icon rakuten-card-icon chevron-up"></span>
    </button>
  </h2>
  <div id="collapseId" class="accordion-collapse" aria-hidden="true">
    <div class="accordion-body">
      <!-- コンテンツ -->
    </div>
  </div>
</div>
```

## クラス一覧

### メインクラス
- `accordion`: アコーディオンのメインコンテナ
- `accordion-flush`: フラッシュスタイル（境界線と角丸を削除）
- `accordion-item`: 個別のアコーディオンアイテム
- `accordion-header`: アコーディオンのヘッダー部分
- `accordion-button`: クリック可能なボタン要素
- `accordion-collapse`: 展開/折りたたみされるコンテンツ部分
- `accordion-body`: コンテンツの本体

### 状態クラス
- `expanded`: 展開状態のアコーディオン
- `collapsed`: 折りたたみ状態のアコーディオン

### テキスト・アイコンクラス
- `accordion-button-text`: ボタンテキストのコンテナ
- `accordion-button-icon`: アイコンのコンテナ
- `accordion-title`: メインタイトル
- `accordion-subtitle`: サブタイトル
- `rakuten-card-icon chevron-up`: 楽天カードの矢印アイコン

## 重要なデータ属性

### ボタン要素
- `data-toggle="accordion"`: アコーディオン機能を有効化
- `data-target="#targetId"`: 制御対象のコンテンツIDを指定

## アクセシビリティ属性

### ボタン要素（必須）
- `aria-controls`: 制御するコンテンツのIDを指定（data-targetと同じ値）
- `aria-expanded`: 展開状態を示す
  - `true`: 展開状態
  - `false`: 折りたたみ状態

### コンテンツ要素（必須）
- `aria-hidden`: 表示/非表示状態を示す
  - `true`: 非表示状態
  - `false`: 表示状態

## バリエーション

### 1. Basic Accordion
標準的なアコーディオンスタイル

```html
<div class="accordion" id="accordionExample">
  <!-- アイテム -->
</div>
```

### 2. Flush Accordion
境界線と角丸を削除したスタイル

```html
<div class="accordion accordion-flush" id="accordionFlushExample">
  <!-- アイテム -->
</div>
```

## 初期状態の設定

### 展開状態で開始
```html
<button class="accordion-button expanded" aria-expanded="true">
<div class="accordion-collapse" aria-hidden="false">
```

### 折りたたみ状態で開始
```html
<button class="accordion-button collapsed" aria-expanded="false">
<div class="accordion-collapse collapsed" aria-hidden="true">
```

## サブタイトル付きアコーディオン

```html
<span class="accordion-button-text">
  <span class="accordion-title">メインタイトル</span>
  <span class="accordion-subtitle d-block">サブタイトル</span>
</span>
```

## 実装時の注意点

1. **一意のID**: 各アコーディオンアイテムには一意のIDを付与する
2. **アクセシビリティ**: aria属性は必ず適切に設定する
3. **アイコン**: chevron-upアイコンはiconfontライブラリが必要
4. **jQuery依存**: アコーディオンスクリプトはjQueryに依存している
5. **初期状態**: 展開/折りたたみの初期状態を適切に設定する

## 動作

- ボタンクリック時にコンテンツが展開/折りたたみされる
- アニメーション付きで滑らかに動作する
- アクセシビリティ属性が自動的に更新される
- 複数のアコーディオンアイテムを同時に開くことが可能

## トラブルシューティング

- 正しく動作しない場合はページをリロードしてください
- 必要なCSS/JSファイルが読み込まれているか確認してください
- data-target属性とIDが一致しているか確認してください
