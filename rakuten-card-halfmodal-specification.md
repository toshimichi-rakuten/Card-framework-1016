# 楽天カードフレームワーク HalfModal コンポーネント仕様書

## 概要

楽天カードフレームワークのHalfModalコンポーネントは、画面下部から表示されるモーダルUIコンポーネントです。
モバイルフレンドリーなユーザーインターフェースを提供し、完全なアクセシビリティサポートとカスタマイズオプションを備えています。

## 必要な依存関係

### CSS
```html
<link rel="stylesheet" href="https://static.card.jp.rakuten-static.com/card_corp/pc/css/common/framework/rakuten-card-framework-4.0.0.min.css">
<link rel="stylesheet" href="https://static.card.jp.rakuten-static.com/card_corp/pc/css/common/iconfont/rakuten-card-icon-5.0.0.min.css">
```

### JavaScript
```html
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<script src="https://static.card.jp.rakuten-static.com/card_corp/pc/js/common/framework/5.0.0/half-modal.min.js"></script>
```

## ⚠️ 重要なバージョン変更注意事項

### CSS 3.1.0未満 ⇨ それ以降
- **CSS適用クラス名・DOM構造が大幅変更**されています
- 既存のハーフモーダルの表示が崩れる可能性があります
- **デザインシステムCSSのバージョン変更時は必須チェック**
- ハーフモーダル存在時は**必ず最新のDOM構造に更新**してください

## 基本的なHTML構造

### 基本ハーフモーダル
```html
<div>
  <button class="js-half-modal-open btn btn-primary" data-target-modal="#modalId">
    モーダルを表示
  </button>
  <div id="modalId" class="js-half-modal design-system-half-modal" data-modal-speed="250" data-bg-close="true">
    <div class="js-half-modal-bg design-system-half-modal__bg"></div>
    <div class="js-half-modal-content design-system-half-modal__content" role="dialog" aria-modal="true" aria-labelledby="titleId">
      <div class="design-system-half-modal__main">
        <div class="design-system-half-modal__header">
          <p id="titleId" class="design-system-half-modal__title">タイトル</p>
          <button type="button" class="js-half-modal-close design-system-half-modal__close" aria-label="close Modal"></button>
        </div>
        <div class="design-system-half-modal__inner">
          <!-- コンテンツ -->
        </div>
        <div class="design-system-half-modal__footer text-center">
          <div class="design-system-half-modal__btn-wrapper">
            <button type="button" class="design-system-half-modal__btn btn btn-primary">ボタン</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
```

## 実装ルール（必須）

### 1. モーダル表示ボタン
```html
<button class="js-half-modal-open btn btn-primary" data-target-modal="#modalId">
```
- **tabbable要素（基本`<button>`タグ）**で実装
- **`js-half-modal-open`クラス必須**
- **`data-target-modal`属性でモーダルIDと紐付け**

### 2. モーダルコンテンツ
```html
<div id="modalId" class="js-half-modal design-system-half-modal">
```
- **`js-half-modal`クラス必須**
- **一意のID必須**（ボタンの`data-target-modal`と一致）

### 3. 必須DOM構造
```html
<div class="js-half-modal design-system-half-modal">
  <!-- 背景（必須） -->
  <div class="js-half-modal-bg design-system-half-modal__bg"></div>
  
  <!-- コンテンツ（必須） -->
  <div class="js-half-modal-content design-system-half-modal__content" role="dialog" aria-modal="true">
    <!-- モーダル内容 -->
  </div>
</div>
```
- モーダルコンテンツ直下に**背景**（`js-half-modal-bg`）と**コンテンツ**（`js-half-modal-content`）を配置

### 4. 閉じるボタン（必須）
```html
<button type="button" class="js-half-modal-close design-system-half-modal__close" aria-label="close Modal">
</button>
```
- **アクセシビリティの観点から必須**
- **tabbable要素**（`<button>`タグ推奨）
- **`js-half-modal-close`クラス必須**
- **`aria-label`属性必須**

## レイアウトバリエーション

### 1. Default（標準レイアウト）
```html
<div class="js-half-modal-content design-system-half-modal__content">
  <div class="design-system-half-modal__main">
    <div class="design-system-half-modal__header">
      <!-- ヘッダー -->
    </div>
    <div class="design-system-half-modal__inner">
      <!-- メインコンテンツ -->
    </div>
    <div class="design-system-half-modal__footer">
      <!-- フッター -->
    </div>
  </div>
</div>
```
- ヘッダー・コンテンツ・フッターが一体でスクロール

### 2. Header/Footer Fixed（固定レイアウト）
```html
<div class="js-half-modal-content design-system-half-modal__content">
  <!-- ヘッダー（固定） -->
  <div class="design-system-half-modal__header">
    <!-- ヘッダー -->
  </div>
  
  <!-- メインコンテンツ（スクロール） -->
  <div class="design-system-half-modal__main">
    <div class="design-system-half-modal__inner">
      <!-- コンテンツ -->
    </div>
  </div>
  
  <!-- フッター（固定） -->
  <div class="design-system-half-modal__footer">
    <!-- フッター -->
  </div>
</div>
```
- ヘッダーとフッターが固定、メインコンテンツのみスクロール

## オプション設定

### data属性でのオプション指定
モーダルコンテンツ（`.js-half-modal`）に以下のdata属性でオプション指定：

#### data-bg-close
```html
<div class="js-half-modal" data-bg-close="false">
```
- **デフォルト**: `true`
- **`true`**: 背景クリックでモーダルが閉じる
- **`false`**: 背景クリックでは閉じない

#### data-modal-speed
```html
<div class="js-half-modal" data-modal-speed="500">
```
- **デフォルト**: `250`
- モーダル開閉スピード（ミリ秒）を指定
- 数値で指定（例：250, 500, 1000）

## アクセシビリティ要件

### 必須ARIA属性

#### モーダルコンテンツ
```html
<div class="js-half-modal-content" role="dialog" aria-modal="true" aria-labelledby="titleId">
```
- **`role="dialog"`**: モーダルダイアログであることを伝達
- **`aria-modal="true"`**: モーダル状態であることを示す
- **`aria-labelledby`**: タイトル要素のIDと紐付け

#### タイトルなしモーダル
```html
<div class="js-half-modal-content" role="dialog" aria-modal="true" aria-label="モーダルの説明">
```
- タイトルがない場合は**`aria-label`**でコンテンツ概要を説明

#### 閉じるボタン
```html
<button type="button" class="js-half-modal-close" aria-label="close Modal">
```
- **`aria-label`属性必須**: スクリーンリーダーにボタンの役割を伝達
- **`<button>`タグ推奨**: 適切なセマンティクス
- tabbableでない要素を使用する場合は**`tabindex`属性**でTab選択を可能にする

### 実装済みアクセシビリティ機能
1. **フォーカス制御**: モーダル開閉時の適切なフォーカス管理
2. **タブ制限**: モーダル内のみでTabキーが循環
3. **Escapeキー**: Escapeキーでモーダルを閉じる
4. **フォーカス復帰**: モーダル閉時にボタンにフォーカスが戻る

## クラス一覧

### 機能クラス
- `js-half-modal-open`: モーダル表示ボタン
- `js-half-modal`: モーダルコンテンツ
- `js-half-modal-bg`: モーダル背景
- `js-half-modal-content`: モーダルコンテンツ本体
- `js-half-modal-close`: 閉じるボタン

### デザインクラス
- `design-system-half-modal`: モーダルベーススタイル
- `design-system-half-modal__bg`: 背景スタイル
- `design-system-half-modal__content`: コンテンツベーススタイル
- `design-system-half-modal__main`: メイン部分
- `design-system-half-modal__header`: ヘッダー部分
- `design-system-half-modal__inner`: 内容部分
- `design-system-half-modal__footer`: フッター部分
- `design-system-half-modal__title`: タイトルスタイル
- `design-system-half-modal__close`: 閉じるボタンスタイル
- `design-system-half-modal__btn-wrapper`: ボタンコンテナ
- `design-system-half-modal__btn`: ボタンスタイル

## データ属性

### 必須属性
- `data-target-modal`: ボタンとモーダルの紐付け（ボタン側）

### オプション属性
- `data-bg-close`: 背景クリック制御（モーダル側）
- `data-modal-speed`: 開閉速度制御（モーダル側）

## 実装時のチェックリスト

### 必須要件
- [ ] 表示ボタンはtabbable要素（`<button>`推奨）で`js-half-modal-open`クラスを付与
- [ ] `data-target-modal`属性とモーダルの`id`が一致している
- [ ] モーダルに`js-half-modal`クラスを付与
- [ ] 背景（`js-half-modal-bg`）とコンテンツ（`js-half-modal-content`）を適切に配置
- [ ] 閉じるボタンに`js-half-modal-close`クラスと`aria-label`を設定

### アクセシビリティ要件
- [ ] コンテンツに`role="dialog"`と`aria-modal="true"`を設定
- [ ] タイトルがある場合は`aria-labelledby`で紐付け
- [ ] タイトルがない場合は`aria-label`で説明
- [ ] 閉じるボタンは`<button>`タグで実装
- [ ] 全てのインタラクティブ要素がキーボードでアクセス可能

### レイアウト確認
- [ ] 標準レイアウトか固定レイアウトかを適切に選択
- [ ] ボタンの配置（横並び・縦並び）を適切に設定
- [ ] 長いコンテンツでのスクロール動作を確認

## 使用例

### 基本的な確認ダイアログ
```html
<button class="js-half-modal-open btn btn-primary" data-target-modal="#confirmModal">
  削除する
</button>
<div id="confirmModal" class="js-half-modal design-system-half-modal" data-bg-close="false">
  <div class="js-half-modal-bg design-system-half-modal__bg"></div>
  <div class="js-half-modal-content design-system-half-modal__content" role="dialog" aria-modal="true" aria-label="削除確認">
    <div class="design-system-half-modal__main">
      <div class="design-system-half-modal__inner">
        <p class="text-center">本当に削除しますか？</p>
      </div>
      <div class="design-system-half-modal__footer text-center">
        <div class="design-system-half-modal__btn-wrapper">
          <button type="button" class="js-half-modal-close design-system-half-modal__btn btn btn-outline-secondary">キャンセル</button>
          <button type="button" class="design-system-half-modal__btn btn btn-danger">削除</button>
        </div>
      </div>
    </div>
  </div>
</div>
```

### 長いコンテンツの詳細表示
```html
<button class="js-half-modal-open btn btn-info" data-target-modal="#detailModal">
  詳細を見る
</button>
<div id="detailModal" class="js-half-modal design-system-half-modal" data-modal-speed="300">
  <div class="js-half-modal-bg design-system-half-modal__bg"></div>
  <div class="js-half-modal-content design-system-half-modal__content" role="dialog" aria-modal="true" aria-labelledby="detailTitle">
    <!-- ヘッダー固定 -->
    <div class="design-system-half-modal__header">
      <p id="detailTitle" class="design-system-half-modal__title">詳細情報</p>
      <button type="button" class="js-half-modal-close design-system-half-modal__close" aria-label="close Modal"></button>
    </div>
    <!-- スクロールコンテンツ -->
    <div class="design-system-half-modal__main">
      <div class="design-system-half-modal__inner">
        <!-- 長いコンテンツ -->
      </div>
    </div>
    <!-- フッター固定 -->
    <div class="design-system-half-modal__footer text-center">
      <div class="design-system-half-modal__btn-wrapper">
        <button type="button" class="js-half-modal-close design-system-half-modal__btn btn btn-primary">閉じる</button>
      </div>
    </div>
  </div>
</div>
```

## トラブルシューティング

### よくある問題
1. **モーダルが表示されない**
   - `data-target-modal`とモーダルIDの一致確認
   - 必要なJavaScriptファイルの読み込み確認
   - 必須クラス（`js-half-modal-open`, `js-half-modal`）の確認

2. **背景クリックで閉じない**
   - `data-bg-close="true"`の設定確認
   - 背景要素（`js-half-modal-bg`）の存在確認

3. **アクセシビリティエラー**
   - ARIA属性の設定確認
   - 閉じるボタンの`aria-label`確認
   - tabbable要素の確認

4. **レイアウトが崩れる**
   - CSSバージョンの確認（3.1.0以降）
   - DOM構造の確認
   - 必要なデザインクラスの確認

5. **フォーカスが正しく動作しない**
   - ボタンがtabbable要素か確認
   - モーダル内の要素がtabbableか確認
   - JavaScriptエラーの確認

## パフォーマンス考慮事項

### 最適化ポイント
- アニメーション速度の適切な設定
- 大量のコンテンツを含む場合の遅延読み込み検討
- 不要なモーダルの削除

### メモリ管理
- モーダルが不要になった場合の適切な削除
- イベントリスナーの適切な管理