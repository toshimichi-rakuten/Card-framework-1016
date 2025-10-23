# 楽天カードフレームワーク Card コンポーネント仕様書

## 概要

楽天カードフレームワークのCardコンポーネントは、柔軟で拡張可能なコンテナを提供するUIコンポーネントです。
複数のバリエーションとオプションで、様々なコンテンツタイプに対応できます。

## 必要な依存関係

### CSS
```html
<link rel="stylesheet" href="https://static.card.jp.rakuten-static.com/card_corp/pc/css/common/framework/rakuten-card-framework-4.0.0.min.css">
<link rel="stylesheet" href="https://static.card.jp.rakuten-static.com/card_corp/pc/css/common/iconfont/rakuten-card-icon-5.0.0.min.css">
```

## 基本的なHTML構造

### 基本カード
```html
<div class="card">
  <img src="..." class="card-img-top">
  <div class="card-body">
    <h4 class="card-title">Card title</h4>
    <p class="card-text">Card text content</p>
    <a href="#" class="btn btn-primary card-link">Go somewhere</a>
    <a href="#" class="card-link">Another link</a>
  </div>
</div>
```

## カードバリエーション

### 1. Basic Card（基本カード）
標準的なカードレイアウト

### 2. Small Card（スモールカード）
```html
<div class="card card-small">
  <!-- コンテンツ -->
</div>
```
- `.card-small`を追加することで、テキストサイズと余白が縮小される
- より小さくコンパクトなカードスタイル

## コンテンツタイプ

### 1. Body（本文）
```html
<div class="card">
  <div class="card-body">
    This is some text within a card body.
  </div>
</div>
```
- `.card-body`：カードの基本構築クラス
- paddingが必要なセクションで使用

### 2. Titles, text, and links（タイトル・テキスト・リンク）
```html
<div class="card">
  <div class="card-body">
    <h3 class="card-title">Card title</h3>
    <h4 class="card-subtitle mb-2 text-muted">Card subtitle</h4>
    <p class="card-text">Some quick example text...</p>
    <a href="#" class="card-link">Card link</a>
    <a href="#" class="card-link">Another link</a>
  </div>
</div>
```

### 3. Image（画像）
#### 上部画像キャップ
```html
<div class="card">
  <img src="..." class="card-img-top">
  <div class="card-body">
    <p class="card-text">Content</p>
  </div>
</div>
```

#### 下部画像キャップ
```html
<div class="card">
  <div class="card-body">
    <p class="card-text">Content</p>
  </div>
  <img src="..." class="card-img-bottom">
</div>
```

### 4. Horizontal（水平レイアウト）
```html
<div class="card mb-3">
  <div class="row no-gutters">
    <div class="col-md-4">
      <img src="..." class="card-img-top">
    </div>
    <div class="col-md-8">
      <div class="card-body">
        <h4 class="card-title">Card title</h4>
        <p class="card-text">Content</p>
        <a href="#" class="card-link">Card link</a>
      </div>
    </div>
  </div>
</div>
```
- グリッドとユーティリティクラスを組み合わせて実装
- `.no-gutters`でグリッドの溝を削除
- レスポンシブ対応（mdブレークポイントで水平化）

### 5. Image overlays（画像オーバーレイ）
```html
<div class="card text-white">
  <img src="..." class="card-img-top">
  <div class="card-img-overlay">
    <h3 class="card-title">Card title</h3>
    <p class="card-text">Content</p>
  </div>
</div>
```
- 画像をカードの背景として使用
- テキストを画像の上に重ねて表示

### 6. Icon Card（アイコンカード）
```html
<div class="card card-icon">
  <img src="..." class="card-img-top">
  <div class="card-body">
    <div class="card-icon-img">
      <img src="...">
    </div>
    <h4 class="card-title">Card title</h4>
    <p class="card-text">Content</p>
    <a href="#" class="btn btn-primary">Go somewhere</a>
    <a href="#" class="card-link">Another link</a>
  </div>
</div>
```
- `.card-icon`：アイコン付きカードのベースクラス
- `.card-icon-img`：アイコン画像のコンテナ

## レイアウトオプション

### 1. Card decks（カードデッキ）
```html
<div class="card-deck">
  <div class="card">
    <div class="card-body d-flex flex-column">
      <h4 class="card-title">Card title</h4>
      <p class="card-text">Content</p>
      <a href="#" class="card-link text-right mt-auto">Card link</a>
    </div>
  </div>
  <!-- 他のカード -->
</div>
```
- 高さと幅が等しいカードを横並びで配置
- Flexboxを使用して要素の位置を揃える
- カード同士は接触しない

### 2. Card columns（カードコラム）
```html
<div class="card-columns">
  <div class="card">
    <!-- カードコンテンツ -->
  </div>
  <!-- 他のカード -->
</div>
```
- CSS columnsを使用したマルチカラムレイアウト
- カードが縦方向に流れるように配置される

### 3. Sizing（サイズ調整）
```html
<div class="row">
  <div class="col">
    <div class="card">
      <!-- カードコンテンツ -->
    </div>
  </div>
  <div class="col">
    <div class="card">
      <!-- カードコンテンツ -->
    </div>
  </div>
</div>
```
- グリッドシステムを使用してカードサイズを制御
- カードの幅は100%になるため、columnsとrowsで調整

### 4. Header & Footer（ヘッダー・フッター）
```html
<div class="card text-center">
  <div class="card-header">
    Featured
  </div>
  <div class="card-body">
    <h4 class="card-title">Special title treatment</h4>
    <p class="card-text">Content</p>
    <a href="#" class="btn btn-primary">Go somewhere</a>
  </div>
  <div class="card-footer text-muted">
    2 days ago
  </div>
</div>
```

## クラス一覧

### メインクラス
- `card`: カードのベースクラス
- `card-small`: スモールサイズのカード

### 構造クラス
- `card-body`: カード本文のコンテナ
- `card-header`: カードヘッダー
- `card-footer`: カードフッター

### コンテンツクラス
- `card-title`: カードタイトル（`<h*>`タグに適用）
- `card-subtitle`: カードサブタイトル（`<h*>`タグに適用）
- `card-text`: カードテキスト
- `card-link`: カードリンク（`<a>`タグに適用）

### 画像クラス
- `card-img-top`: 上部画像キャップ
- `card-img-bottom`: 下部画像キャップ
- `card-img`: 全体画像
- `card-img-overlay`: 画像オーバーレイコンテンツ

### 特殊クラス
- `card-icon`: アイコン付きカード
- `card-icon-img`: アイコン画像コンテナ

### レイアウトクラス
- `card-deck`: カードデッキレイアウト
- `card-columns`: カードコラムレイアウト

## 実装時の注意点

### レスポンシブ対応
- 水平カードでは適切なブレークポイントを使用
- グリッドシステムと組み合わせてレスポンシブ対応

### アクセシビリティ
- 画像には適切な`alt`属性を設定
- リンクには分かりやすいテキストを提供
- ヘッダー要素の階層を適切に設定

### パフォーマンス
- 画像は適切にサイズを最適化
- 大量のカードを表示する場合は遅延読み込みを検討

## カスタマイズ

### スタイリング
- Bootstrap系のユーティリティクラスと組み合わせ可能
- `.text-center`、`.text-white`、`.bg-*`などを活用

### Flexbox活用
```html
<div class="card-body d-flex flex-column">
  <h4 class="card-title">Title</h4>
  <p class="card-text">Content</p>
  <a href="#" class="card-link mt-auto">Link</a>
</div>
```
- `.d-flex flex-column`でFlexboxレイアウト
- `.mt-auto`で要素を下部に配置

## 使用例とベストプラクティス

### 統一感のあるカードデッキ
- 同じカード構造を使用
- Flexboxで高さを揃える
- 適切な余白設定

### レスポンシブカードレイアウト
- グリッドシステムを活用
- ブレークポイントに応じた表示調整
- モバイルファーストの設計

### アクセシブルなカード
- セマンティックなHTML構造
- 適切なヘッダー階層
- キーボードナビゲーション対応