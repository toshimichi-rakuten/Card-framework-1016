# 楽天カードフレームワーク Button コンポーネント仕様書

## 概要

楽天カードフレームワークのButtonコンポーネントは、様々なHTML要素で使用できる柔軟なボタンシステムです。
複数のスタイルバリエーション、サイズオプション、状態管理機能を提供し、アクセシビリティ要件にも対応しています。

## 必要な依存関係

### CSS
```html
<link rel="stylesheet" href="https://static.card.jp.rakuten-static.com/card_corp/pc/css/common/framework/rakuten-card-framework-4.0.0.min.css">
<link rel="stylesheet" href="https://static.card.jp.rakuten-static.com/card_corp/pc/css/common/iconfont/rakuten-card-icon-5.0.0.min.css">
```

## 基本的なHTML構造

### 基本ボタン
```html
<button type="button" class="btn btn-primary">Primary</button>
<button type="button" class="btn btn-secondary">Secondary</button>
<button type="button" class="btn btn-link">Link</button>
```

## ボタンタグの使い分け

### 1. button要素（推奨）
```html
<button class="btn btn-primary" type="submit">Button</button>
<button class="btn btn-primary" type="button">Button</button>
```
- `.btn`クラスの本来の設計対象
- 最も適切なセマンティクス

### 2. a要素
```html
<a class="btn btn-primary" href="#" role="button">Link</a>
```
**重要な注意事項**
- **必ず`role="button"`を追加する**
- 機能のトリガーとして使用する場合のアクセシビリティ要件

### 3. input要素
```html
<input class="btn btn-primary" type="button" value="Input" />
<input class="btn btn-primary" type="submit" value="Submit" />
<input class="btn btn-primary" type="reset" value="Reset" />
```
- ブラウザによってレンダリングに差異が生じる可能性あり

## スタイルバリエーション

### 1. 基本スタイル
```html
<button type="button" class="btn btn-primary">Primary</button>
<button type="button" class="btn btn-secondary">Secondary</button>
<button type="button" class="btn btn-link">Link</button>
```

### 2. アウトラインスタイル
```html
<button type="button" class="btn btn-outline-primary">Primary</button>
<button type="button" class="btn btn-outline-secondary">Secondary</button>
```
- `.btn-outline-*`：枠線を残して背景色を透過

### 3. アイコン付きボタン
```html
<button type="button" class="btn btn-primary btn-icon">
  With Icon<span class="rakuten-card-icon chevron-right"></span>
</button>
<button type="button" class="btn btn-outline-primary btn-icon">
  With Icon<span class="rakuten-card-icon chevron-right"></span>
</button>
<button type="button" class="btn btn-outline-secondary btn-icon text-link">
  With Icon and Text<br />With Icon and Text<span
    class="rakuten-card-icon arrow-down"
  ></span>
</button>
```

## サイズオプション

### サイズクラス一覧
```html
<button type="button" class="btn btn-primary btn-large">Large button</button>
<button type="button" class="btn btn-primary btn-medium">Medium button</button>
<button type="button" class="btn btn-primary">Default button</button>
<button type="button" class="btn btn-primary btn-small">Small button</button>
<button type="button" class="btn btn-primary btn-xsmall">X-Small button</button>
```

### ブロックレベルボタン
```html
<button type="button" class="btn btn-primary btn-block">
  Block level button
</button>
<button type="button" class="btn btn-outline-primary btn-block">
  Block level button
</button>
```
- `.btn-block`：幅いっぱいに広がるボタン

## 状態管理

### 1. アクティブ状態
```html
<!-- リンクボタンのアクティブ状態 -->
<a href="#" class="btn btn-primary active" role="button" aria-pressed="true">
  Primary active link
</a>

<!-- ボタン要素のアクティブ状態 -->
<button type="button" class="btn btn-primary active">
  Primary active button
</button>
```

### 2. 無効状態
```html
<!-- リンクボタンの無効状態 -->
<a
  href="#"
  class="btn btn-outline-primary disabled"
  tabindex="-1"
  role="button"
  aria-disabled="true"
>Primary disabled link</a>

<!-- ボタン要素の無効状態 -->
<button type="button" class="btn btn-primary" disabled="disabled">
  Primary disabled button
</button>

<!-- リンクボタンの無効状態 -->
<button type="button" class="btn btn-link disabled">Disabled Link</button>
```

## 特殊ボタン

### アンカーボタン
```html
<a href="#" class="anchor anchor-btn">カテゴリから探す</a>
```
- `.anchor.anchor-btn`：特別なアンカーボタンスタイル

## クラス一覧

### ベースクラス
- `btn`: ボタンのベースクラス（必須）

### スタイルクラス
- `btn-primary`: プライマリボタン
- `btn-secondary`: セカンダリボタン
- `btn-link`: リンクスタイルボタン
- `btn-outline-primary`: アウトラインプライマリ
- `btn-outline-secondary`: アウトラインセカンダリ

### サイズクラス
- `btn-large`: 大サイズ
- `btn-medium`: 中サイズ
- （デフォルト）: 標準サイズ
- `btn-small`: 小サイズ
- `btn-xsmall`: 極小サイズ

### レイアウトクラス
- `btn-block`: ブロックレベル（幅100%）
- `btn-icon`: アイコン付きボタン

### 状態クラス
- `active`: アクティブ状態
- `disabled`: 無効状態

### 特殊クラス
- `anchor`: アンカー要素用
- `anchor-btn`: アンカーボタンスタイル
- `text-link`: テキストリンクスタイル

## アクセシビリティ要件

### 必須属性

#### aタグ使用時
```html
<a class="btn btn-primary" href="#" role="button">Link</a>
```
- **`role="button"`は必須**
- 機能のトリガーとして使用する場合のセマンティクス

#### 無効状態のaタグ
```html
<a
  href="#"
  class="btn btn-outline-primary disabled"
  tabindex="-1"
  role="button"
  aria-disabled="true"
>Disabled link</a>
```
- `tabindex="-1"`: キーボードフォーカスを無効化
- `aria-disabled="true"`: スクリーンリーダーに無効状態を伝達

#### アクティブ状態
```html
<a href="#" class="btn btn-primary active" role="button" aria-pressed="true">
  Active button
</a>
```
- `aria-pressed="true"`: 押下状態をスクリーンリーダーに伝達

### フローティングアンカーボタン
```html
<button type="button" class="btn btn-primary" aria-label="メニューを開く">
  <span class="rakuten-card-icon menu"></span>
</button>
```
**重要な注意事項**
- **`aria-label`属性は必須**
- スクリーンリーダーで読み上げられる
- コンテンツだと認識できるように必ず記載

### 状態を表すボタン
```html
<button type="button" class="btn btn-primary" aria-pressed="false">
  お気に入りに追加
</button>
<button type="button" class="btn btn-primary active" aria-pressed="true">
  お気に入り済み
</button>
```
- `aria-pressed`: トグル状態を表現

## アイコン使用方法

### 基本的なアイコン使用
```html
<button type="button" class="btn btn-primary btn-icon">
  Text<span class="rakuten-card-icon icon-name"></span>
</button>
```

### よく使用されるアイコン
- `chevron-right`: 右矢印
- `chevron-left`: 左矢印
- `arrow-down`: 下矢印
- `menu`: ハンバーガーメニュー
- `search`: 検索
- `download`: ダウンロード

## 実装時の注意点

### タグ選択のガイドライン
1. **一般的なボタン**: `<button>`要素を使用
2. **ページ遷移**: `<a>`要素を使用（`role="button"`必須）
3. **フォーム送信**: `<input type="submit">`または`<button type="submit">`

### アクセシビリティチェックリスト
- [ ] aタグには`role="button"`を設定
- [ ] 無効状態のaタグには`tabindex="-1"`と`aria-disabled="true"`を設定
- [ ] アイコンのみのボタンには`aria-label`を設定
- [ ] トグル状態のボタンには`aria-pressed`を設定

### レスポンシブ対応
- ブロックボタンは小画面で有効
- サイズクラスを画面サイズに応じて調整
- アイコン付きボタンのテキスト折り返しに注意

## パフォーマンス考慮事項

### アイコンフォント
- 必要なアイコンのみ読み込み
- アイコンフォントの読み込み完了を確認

### 状態管理
- JavaScriptでの状態変更時は適切なARIA属性の更新
- 動的な無効化の際は`disabled`属性とクラスの両方を制御

## トラブルシューティング

### よくある問題
1. **aタグのボタンが機能しない**
   - `role="button"`の設定を確認

2. **無効ボタンがクリックできる**
   - `disabled`属性または`tabindex="-1"`の設定を確認

3. **アイコンが表示されない**
   - アイコンフォントCSSの読み込みを確認
   - 正しいアイコンクラス名を確認

4. **スクリーンリーダーで読み上げられない**
   - `aria-label`または適切なテキストコンテンツの設定を確認