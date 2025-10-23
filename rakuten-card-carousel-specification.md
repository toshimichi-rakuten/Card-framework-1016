# 楽天カードフレームワーク Carousel コンポーネント仕様書

## 概要

楽天カードフレームワークのCarouselコンポーネントは、複数のコンテンツをスライド表示するUIコンポーネントです。
Slickライブラリをベースとしており、様々なオプションを組み合わせることで柔軟なカルーセル機能を実装できます。

## 必要な依存関係

### CSS
```html
<link rel="stylesheet" href="https://static.card.jp.rakuten-static.com/card_corp/pc/css/common/framework/rakuten-card-framework-4.0.0.min.css">
<link rel="stylesheet" href="https://static.card.jp.rakuten-static.com/card_corp/pc/css/common/iconfont/rakuten-card-icon-5.0.0.min.css">
```

### JavaScript
```html
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<script src="https://static.card.jp.rakuten-static.com/card_corp/pc/js/common/framework/5.0.0/slick.min.js"></script>
<script src="https://static.card.jp.rakuten-static.com/card_corp/pc/js/common/framework/5.0.0/carousel.min.js"></script>
```

## 基本的なHTML構造

### 基本カルーセル
```html
<div
  class="carousel"
  data-toggle="carousel"
  aria-roledescription="carousel"
  aria-label="カルーセルの説明"
  aria-live="polite"
>
  <div class="carousel-item" role="group" aria-roledescription="slide">
    <!-- スライドコンテンツ -->
  </div>
  <div class="carousel-item" role="group" aria-roledescription="slide">
    <!-- スライドコンテンツ -->
  </div>
</div>
```

## カルーセルオプション

### 1. Dot（ドットインディケーター）
ページネーション用のドットを表示

**データ属性**
- `data-dots="true"`

**例**
```html
<div
  class="carousel"
  data-toggle="carousel"
  data-dots="true"
  aria-roledescription="carousel"
  aria-label="Dotカルーセル"
>
  <!-- スライドアイテム -->
</div>
```

### 2. Arrow（矢印ナビゲーション）
左右の矢印ボタンを表示

**データ属性**
- `data-arrows="true"`

**重要な注意事項**
- Arrowオプション使用時は**必ず`id`属性を指定する**

**例**
```html
<div
  id="carousel-arrow"
  class="carousel"
  data-toggle="carousel"
  data-arrows="true"
  aria-roledescription="carousel"
  aria-label="Arrowカルーセル"
>
  <!-- スライドアイテム -->
</div>
```

### 3. AutoPlay（自動再生）
スライドを自動で切り替え

**データ属性**
- `data-autoplay="true"`
- `data-autoplay-speed="3000"`（ミリ秒、デフォルト：3000ms）

**重要な注意事項**
- 自動再生使用時は**必ず停止ボタンを設置する**（アクセシビリティ要件）
- カルーセルの`id`と停止ボタンの`data-carousel-id`を一致させる

**例**
```html
<div
  id="carousel-autoplay"
  class="carousel"
  data-toggle="carousel"
  data-autoplay="true"
  data-autoplay-speed="3000"
  aria-roledescription="carousel"
  aria-label="AutoPlayカルーセル"
>
  <!-- スライドアイテム -->
</div>
<button
  class="js-toggle-autoplay carousel-autoplay-button"
  data-carousel-id="carousel-autoplay"
  aria-label="自動再生停止ボタン"
>
  停止/開始
</button>
```

### 4. Center Mode（センターモード）
現在のスライドを中央に配置し、前後のスライドを部分的に表示

**データ属性**
- `data-center="true"`

**例**
```html
<div
  class="carousel"
  data-toggle="carousel"
  data-center="true"
  aria-roledescription="carousel"
  aria-label="Centerカルーセル"
>
  <!-- スライドアイテム -->
</div>
```

### 5. Show Multiple Slides（複数スライド表示）
一度に複数のスライドを表示

**データ属性**
- `data-show="4"`（表示するスライド数）

**例**
```html
<div
  class="carousel"
  data-toggle="carousel"
  data-show="4"
  aria-roledescription="carousel"
  aria-label="ShowSlideカルーセル"
>
  <!-- スライドアイテム -->
</div>
```

### 6. Scroll Multiple Slides（複数スライドスクロール）
スライド送り時に移動するスライド数を指定

**データ属性**
- `data-scroll="2"`（スクロールするスライド数）
- 通常`data-show`と組み合わせて使用

**例**
```html
<div
  class="carousel"
  data-toggle="carousel"
  data-show="4"
  data-scroll="2"
  aria-roledescription="carousel"
  aria-label="ScrollSlideカルーセル"
>
  <!-- スライドアイテム -->
</div>
```

## クラス一覧

### メインクラス
- `carousel`: カルーセルのメインコンテナ
- `carousel-item`: 個別のスライドアイテム

### 自動再生関連クラス
- `js-toggle-autoplay`: 自動再生停止/開始ボタン
- `carousel-autoplay-button`: 自動再生ボタンのスタイリング

## 重要なデータ属性

### 基本属性
- `data-toggle="carousel"`: カルーセル機能を有効化（必須）

### オプション属性
- `data-dots="true"`: ドット表示
- `data-arrows="true"`: 矢印表示
- `data-autoplay="true"`: 自動再生
- `data-autoplay-speed="3000"`: 自動再生速度（ミリ秒）
- `data-center="true"`: センターモード
- `data-show="4"`: 表示スライド数
- `data-scroll="2"`: スクロールスライド数

### 制御属性
- `data-carousel-id="carousel-id"`: 自動再生停止ボタン用のターゲットID

## アクセシビリティ要件

### 必須のARIA属性

#### カルーセルコンテナ
```html
<div
  class="carousel"
  data-toggle="carousel"
  aria-roledescription="carousel"
  aria-label="カルーセルの説明"
  aria-live="polite"
>
```

- `aria-roledescription="carousel"`: スクリーンリーダーにカルーセルの役割を伝える
- `aria-label`: 何に関するカルーセルかを説明
- `aria-live="polite"`: スライド切り替えをスクリーンリーダーに伝える

#### スライドアイテム
```html
<div class="carousel-item" role="group" aria-roledescription="slide">
```

- `role="group"`: スライドが一つのグループであることを伝える
- `aria-roledescription="slide"`: スクリーンリーダーにスライドであることを伝える

### 自動再生のアクセシビリティ
- 自動再生を使用する場合は**必ず停止ボタンを設置する**
- 停止ボタンには適切な`aria-label`を設定する

### aria-live属性の注意事項
- 自動再生カルーセルに`aria-live="polite"`を設定すると、自動切り替えのたびに読み上げが発生する
- 自動再生の場合は`aria-live`の設定を慎重に検討する

## オプション組み合わせ例

### 基本的な組み合わせ
```html
<!-- ドット + 矢印 -->
<div
  id="carousel-basic"
  class="carousel"
  data-toggle="carousel"
  data-dots="true"
  data-arrows="true"
  aria-roledescription="carousel"
  aria-label="基本カルーセル"
>

<!-- 複数表示 + スクロール -->
<div
  class="carousel"
  data-toggle="carousel"
  data-show="3"
  data-scroll="1"
  data-dots="true"
  aria-roledescription="carousel"
  aria-label="マルチスライドカルーセル"
>

<!-- 全機能 -->
<div
  id="carousel-full"
  class="carousel"
  data-toggle="carousel"
  data-arrows="true"
  data-dots="true"
  data-autoplay="true"
  data-autoplay-speed="4000"
  data-show="2"
  data-scroll="1"
  aria-roledescription="carousel"
  aria-label="全機能カルーセル"
>
```

## 実装時の重要な注意事項

### 必須要件
1. **ID指定**: ArrowまたはAutoPlayオプション使用時は必ず`id`を指定
2. **自動再生停止ボタン**: 自動再生使用時は必ず停止ボタンを設置
3. **アクセシビリティ属性**: 適切なARIA属性を設定

### 推奨事項
1. **適切なaria-label**: カルーセルの内容を説明する分かりやすいラベル
2. **レスポンシブ対応**: 異なる画面サイズでの表示を考慮
3. **パフォーマンス**: 大量のスライドがある場合の読み込み速度を考慮

## トラブルシューティング

### よくある問題
1. **カルーセルが動作しない**
   - `data-toggle="carousel"`が設定されているか確認
   - 必要なJavaScriptファイルが読み込まれているか確認

2. **自動再生が停止しない**
   - 停止ボタンの`data-carousel-id`とカルーセルの`id`が一致しているか確認

3. **アクセシビリティエラー**
   - ARIA属性が適切に設定されているか確認
   - 自動再生使用時に停止ボタンが設置されているか確認

## パフォーマンス考慮事項

- 大量のスライドを持つカルーセルでは遅延読み込みを検討
- 自動再生の速度は適切に設定（あまり速すぎないように）
- 画像などのメディアコンテンツは適切に最適化する