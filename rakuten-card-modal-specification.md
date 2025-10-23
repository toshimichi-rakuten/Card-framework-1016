# 楽天カードフレームワーク Modal コンポーネント仕様書

## 概要

楽天カードフレームワークのModalコンポーネントは、Magnific Popupライブラリをベースとした高機能なモーダルシステムです。
基本的なモーダル表示から自動表示、Cookie制御まで、様々な機能を提供し、完全なアクセシビリティ対応を実装しています。

## 必要な依存関係

### CSS
```html
<link rel="stylesheet" href="https://static.card.jp.rakuten-static.com/card_corp/pc/css/common/framework/rakuten-card-framework-4.0.0.min.css">
<link rel="stylesheet" href="https://static.card.jp.rakuten-static.com/card_corp/pc/css/common/iconfont/rakuten-card-icon-5.0.0.min.css">
```

### JavaScript
```html
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<script src="https://static.card.jp.rakuten-static.com/card_corp/pc/js/common/framework/5.0.0/modal.min.js"></script>
<script src="https://static.card.jp.rakuten-static.com/card_corp/pc/js/common/framework/5.0.0/magnific-popup.min.js"></script>
```

## 基本的なHTML構造

### 基本モーダル
```html
<div>
  <a href="#modal1" class="popup-modal btn btn-primary">モーダルを表示</a>
  <div id="modal1" class="js-modal-content mfp-hide modal__content" role="dialog" aria-modal="true" aria-labelledby="modal__title">
    <div class="modal__content--header border-bottom">
      <p id="modal__title" class="mb-0 text-center h4 font-weight-bold">モーダルタイトル</p>
      <button type="button" aria-label="close Modal" class="js-mfp-close mfp-close modal__close-circle-btn"></button>
    </div>
    <div class="modal__content--main">
      <div class="modal__content--inner">
        <!-- モーダルコンテンツ -->
      </div>
    </div>
  </div>
</div>
```

## 実装ルール（重要）

### 必須要件
1. **モーダル表示ボタン**: `<a>`タグで実装し、`popup-modal`クラスを付与
2. **モーダルコンテンツ**: `js-modal-content`クラスを付与
3. **href属性との紐付け**: ボタンの`href`属性とモーダルの`id`を一致させる
4. **閉じるボタン**: `mfp-close`クラスで閉じる機能を付与（`<button>`タグ推奨）
5. **基本クラス**: `mfp-hide modal__content`をモーダルコンテンツに付与
6. **メイン部分**: `modal__content--main`クラスを付与

### クラス構造
```html
<!-- 表示ボタン -->
<a href="#modalId" class="popup-modal btn btn-primary">ボタンテキスト</a>

<!-- モーダルコンテンツ -->
<div id="modalId" class="js-modal-content mfp-hide modal__content" role="dialog" aria-modal="true">
  <div class="modal__content--main">
    <!-- コンテンツ -->
  </div>
</div>
```

## 自動表示モーダル

### 基本構造
```html
<div
  id="modalId"
  class="js-modal-content js-auto-disp-mfp mfp-hide modal__content"
  role="dialog"
  aria-modal="true"
  aria-labelledby="modal__title"
>
  <!-- モーダルコンテンツ -->
  <div class="js-mfp-checkbox-wrap">
    <div class="d-flex position-absolute justify-content-center modal__checkbox">
      <input
        id="checkbox-id"
        type="checkbox"
        class="modal__checkbox-dummy"
        data-duration="7"
      />
      <label for="checkbox-id" class="modal__checkbox-text">
        <span class="modal__checkbox-square"></span>
        次回から表示しない
      </label>
    </div>
  </div>
</div>
```

### 自動表示の仕組み
1. **判定クラス**: `js-auto-disp-mfp`で自動表示判定が実行される
2. **Cookie制御**: `{モーダルID}-auto-mfp`がCookieキーとして使用される
3. **チェックボックス**: `js-mfp-checkbox-wrap`内の`input`にCookie登録イベントが付与
4. **保存期間**: `data-duration`属性で指定（最大値・デフォルト：7日）
5. **一意ID**: 他のモーダルと重複しないよう一意のIDを設定

### 自動表示専用モーダル
```html
<!-- ボタンなし、自動表示のみ -->
<div
  id="auto-modal"
  class="js-modal-content js-auto-disp-mfp mfp-hide modal__content"
  role="dialog"
  aria-modal="true"
>
  <!-- コンテンツ -->
</div>
```
- 遷移時の自動表示のみの場合、ボタン設置は不要
- ボタンクリックでも表示させたい場合は設置する

## オプション設定

### data属性でのオプション指定
モーダルコンテンツ（`.js-modal-content`）に以下の属性でオプション指定可能：

#### data-bg-close
```html
<div class="js-modal-content" data-bg-close="false">
```
- **デフォルト**: `true`
- **`true`**: 背景オーバーレイクリックでモーダルが閉じる
- **`false`**: 背景クリックでは閉じない

#### data-auto-focus-last
```html
<div class="js-modal-content" data-auto-focus-last="false">
```
- **デフォルト**: `true`
- **`true`**: モーダルが閉じた際にボタンにフォーカスが戻る
- **`false`**: フォーカスが戻らない（ページ内リンクがある場合に推奨）

## アクセシビリティ要件

### 必須ARIA属性

#### モーダルコンテナ
```html
<div
  class="js-modal-content modal__content"
  role="dialog"
  aria-modal="true"
  aria-labelledby="modal__title"
>
```
- **`role="dialog"`**: 要素がモーダルであることを伝達
- **`aria-modal="true"`**: モーダル状態であることを示す
- **`aria-labelledby`**: タイトル要素のIDと紐付け

#### タイトルなしモーダル
```html
<div
  class="js-modal-content modal__content"
  role="dialog"
  aria-modal="true"
  aria-label="モーダルのコンテンツ概要"
>
```
- タイトルがない場合は`aria-label`でコンテンツ概要を説明

#### 閉じるボタン
```html
<button type="button" aria-label="close Modal" class="js-mfp-close mfp-close">
  閉じる
</button>
```
- **`aria-label="close Modal"`**: スクリーンリーダーに役割を伝達
- **`<button>`タグ推奨**: セマンティクスとキーボード操作
- やむを得ず`<div>`等を使用する場合は`tabindex`属性でフォーカス可能にする

### 実装済みアクセシビリティ機能
1. **フォーカス制御**: モーダル開閉時の適切なフォーカス管理
2. **タブ制限**: モーダル内のみでタブキーが循環
3. **Escapeキー**: Escapeキーでモーダルを閉じる
4. **フォーカス復帰**: モーダル閉時にボタンにフォーカスが戻る

## クラス一覧

### 基本クラス
- `popup-modal`: モーダル表示ボタン（`<a>`タグ用）
- `js-modal-content`: モーダルコンテンツ識別クラス
- `mfp-hide`: 初期非表示設定
- `modal__content`: モーダルコンテンツベースクラス

### 構造クラス
- `modal__content--header`: ヘッダー部分
- `modal__content--main`: メイン部分
- `modal__content--inner`: 内容部分
- `modal__content--banner`: バナー部分
- `modal__content--footer`: フッター部分

### 閉じるボタンクラス
- `mfp-close`: 閉じる機能を付与
- `js-mfp-close`: 閉じる機能を付与（追加）
- `modal__close-circle-btn`: 円形閉じるボタン
- `modal__close-text-link`: テキストリンク形式の閉じるボタン

### 自動表示関連クラス
- `js-auto-disp-mfp`: 自動表示判定クラス
- `js-mfp-checkbox-wrap`: チェックボックスコンテナ
- `modal__checkbox`: チェックボックス部分
- `modal__checkbox-dummy`: チェックボックスinput
- `modal__checkbox-text`: チェックボックスラベル
- `modal__checkbox-square`: チェックボックス表示部分

### フッター関連クラス
- `modal__footer-button-wrapper`: フッターボタンコンテナ
- `modal__footer-button`: フッターボタン
- `modal__close-text-link-wrapper`: テキストリンクコンテナ

## Cookie制御システム

### Cookie命名規則
```
{モーダルID}-auto-mfp
```
例：`modal2-auto-mfp`、`auto-modal-auto-mfp`

### 保存期間設定
```html
<input data-duration="7" />
```
- **最大値**: 7日
- **デフォルト**: 7日
- 7日を超える値を指定しても強制的に7日となる

### 動作仕様
1. チェックボックスにチェック → Cookieが保存される
2. 次回訪問時 → Cookieが存在する場合、モーダルは非表示
3. 保存期間経過後 → Cookieが削除され、再び自動表示される

## アニメーション設定

### アニメーション速度の変更
アニメーション速度を変更する場合は以下を同時に修正：
1. **CSS**: `mfp-content`, `mfp-bg`の`transition-duration`
2. **JavaScript**: `modal.js`の`DURATION_DEFAULT`

## 実装時の注意点

### 必須チェックリスト
- [ ] 表示ボタンは`<a>`タグで`popup-modal`クラスを付与
- [ ] `href`属性とモーダルの`id`が一致している
- [ ] モーダルに`js-modal-content`、`mfp-hide`、`modal__content`クラスを付与
- [ ] 適切なARIA属性（`role="dialog"`、`aria-modal="true"`）を設定
- [ ] 閉じるボタンに`aria-label`を設定
- [ ] 自動表示モーダルには一意のIDを設定

### 自動表示モーダルの注意点
- [ ] `js-auto-disp-mfp`クラスを付与
- [ ] チェックボックス構造を`js-mfp-checkbox-wrap`内に配置
- [ ] `data-duration`で適切な保存期間を設定
- [ ] 他のモーダルと重複しない一意のIDを設定

### アクセシビリティチェック
- [ ] タイトルがある場合は`aria-labelledby`で紐付け
- [ ] タイトルがない場合は`aria-label`で説明
- [ ] 閉じるボタンは`<button>`タグで実装
- [ ] キーボード操作（Tab、Escape）が正常に動作

## トラブルシューティング

### よくある問題
1. **モーダルが表示されない**
   - 必要なJavaScriptファイルの読み込み確認
   - `href`属性とモーダルIDの一致確認
   - 必須クラス（`popup-modal`、`js-modal-content`）の確認

2. **自動表示が動作しない**
   - `js-auto-disp-mfp`クラスの確認
   - Cookieの確認（開発者ツールで削除して再テスト）
   - 一意IDの確認

3. **閉じるボタンが動作しない**
   - `mfp-close`または`js-mfp-close`クラスの確認
   - `<button>`タグの使用確認

4. **アクセシビリティエラー**
   - ARIA属性の設定確認
   - `aria-label`の設定確認
   - フォーカス可能要素の確認

## パフォーマンス考慮事項

### 最適化ポイント
- 不要な自動表示モーダルは削除
- 画像などのメディアコンテンツは適切に最適化
- 大量のモーダルを配置する場合は遅延読み込みを検討

### Cookie管理
- 適切な保存期間の設定
- 不要なCookieの定期削除
- プライバシーポリシーでのCookie使用の明記