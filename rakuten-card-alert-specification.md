# 楽天カードフレームワーク Alert コンポーネント仕様書

## 概要

楽天カードフレームワークのAlertコンポーネントは、ユーザーに重要な情報を視覚的に伝えるためのUIコンポーネントです。
成功、危険、警告、情報、プロモーションなど、異なるレベルの重要度を色分けで表現できます。

## 必要な依存関係

### CSS
```html
<link rel="stylesheet" href="https://static.card.jp.rakuten-static.com/card_corp/pc/css/common/framework/rakuten-card-framework-4.0.0.min.css">
<link rel="stylesheet" href="https://static.card.jp.rakuten-static.com/card_corp/pc/css/common/iconfont/rakuten-card-icon-5.0.0.min.css">
```

### JavaScript（機能別）
#### Deletableアラート用
```html
<script src="https://static.card.jp.rakuten-static.com/card_corp/pc/js/common/framework/5.0.0/alert.min.js"></script>
```

#### Openableアラート用
```html
<script src="https://static.card.jp.rakuten-static.com/card_corp/pc/js/common/framework/5.0.0/accordion.min.js"></script>
```

## アラートタイプ

### 1. Basic Alert（基本アラート）
ユーザーに情報を伝える静的なアラート

### 2. Openable Alert（開閉可能アラート）
クリックで詳細を展開・折りたたみできるアラート

### 3. Deletable Alert（削除可能アラート）
ユーザーが閉じることができるアラート（Cookie制御）

## アラートの重要度レベル

### 色分けとアイコン
- **success**: 成功・完了 (緑) - `check`アイコン
- **danger**: 危険・エラー (赤) - `warning-l`アイコン
- **warning**: 警告 (黄) - `info-l`アイコン
- **info**: 情報 (青) - `info-l`アイコン
- **promotion**: プロモーション (紫) - `point-l` / `campaign-l`アイコン

## 基本的なHTML構造

### シンプルなアラート
```html
<div class="alert alert-success">
  <div class="alert-heading">
    <span class="rakuten-card-icon alert-icon check"></span>
    <div class="alert-title">メッセージテキスト</div>
  </div>
</div>
```

### クリック可能なアラート
```html
<a href="#" class="alert alert-success">
  <div class="alert-heading">
    <span class="rakuten-card-icon alert-icon check"></span>
    <div class="alert-title">メッセージテキスト</div>
    <span class="rakuten-card-icon chevron-right alert-icon"></span>
  </div>
</a>
```

### 詳細付きアラート
```html
<div class="alert alert-success">
  <div class="alert-heading">
    <span class="rakuten-card-icon alert-icon check"></span>
    <div class="alert-title font-weight-bold">タイトル</div>
  </div>
  <div class="alert-body alert-body-padding">
    詳細テキスト
  </div>
</div>
```

### アクション付きアラート
```html
<div class="alert alert-success">
  <div class="alert-heading">
    <span class="rakuten-card-icon alert-icon check"></span>
    <div class="alert-title font-weight-bold">タイトル</div>
  </div>
  <div class="alert-action text-right">
    <a href="#" class="d-inline-flex align-items-center">
      詳細はこちら<span class="rakuten-card-icon chevron-right"></span>
    </a>
  </div>
</div>
```

## Openable Alert（開閉可能）

### 基本構造
```html
<div class="accordion-alert-item alert-info">
  <div>
    <button
      type="button"
      data-toggle="accordion"
      data-target="#collapseAlert"
      aria-expanded="false"
      aria-controls="collapseAlert"
      class="accordion-alert-button alert-info collapsed"
    >
      <span class="rakuten-card-icon info-l alert-icon"></span>
      <div class="alert-title accordion-alert-title font-weight-bold">
        タイトル
      </div>
      <span class="accordion-alert-button-icon rakuten-card-icon chevron-up"></span>
    </button>
  </div>
  <div
    id="collapseAlert"
    aria-hidden="true"
    class="alert-body accordion-alert-body collapsed"
  >
    <div class="accordion-alert-body-text">
      詳細テキスト
    </div>
  </div>
</div>
```

## Deletable Alert（削除可能）

### 基本構造
```html
<div
  id="unique_id"
  class="alert alert-promotion alert-delete js-hide-alert"
  data-duration="2"
>
  <button class="alert-delete__btn js-hide-alert-botton">
    <div class="alert-delete__btn--contents"></div>
  </button>
  <div class="alert-heading">
    <span class="rakuten-card-icon point-l alert-icon"></span>
    <div class="alert-title">削除可能なアラートメッセージ</div>
  </div>
</div>
```

## クラス一覧

### メインクラス
- `alert`: アラートのベースクラス
- `alert-success`: 成功アラート
- `alert-danger`: 危険アラート
- `alert-warning`: 警告アラート
- `alert-info`: 情報アラート
- `alert-promotion`: プロモーションアラート

### 構造クラス
- `alert-heading`: ヘッダー部分
- `alert-title`: タイトルテキスト
- `alert-body`: 本文部分
- `alert-body-padding`: 本文のパディング
- `alert-action`: アクション部分
- `alert-icon`: アイコン
- `alert-box`: リンク全体をクリック可能にする
- `alert-delete`: 削除機能付きアラート

### Openable専用クラス
- `accordion-alert-item`: 開閉可能アラートのコンテナ
- `accordion-alert-button`: 開閉ボタン
- `accordion-alert-title`: 開閉可能アラートのタイトル
- `accordion-alert-body`: 開閉可能な本文部分
- `accordion-alert-body-text`: 本文テキスト
- `accordion-alert-button-icon`: 開閉アイコン

### Deletable専用クラス
- `js-hide-alert`: 削除機能を有効化
- `js-hide-alert-botton`: 削除ボタン
- `alert-delete__btn`: 削除ボタンスタイル
- `alert-delete__btn--contents`: 削除ボタンのコンテンツ

## 重要なデータ属性

### Openable Alert
- `data-toggle="accordion"`: 開閉機能を有効化
- `data-target="#targetId"`: 開閉対象のID指定

### Deletable Alert
- `data-duration`: Cookie保存期間（最大7日）
- `id`: Cookie制御用の一意識別子

## アクセシビリティ要件

### テキスト強調の使い分け
- **danger（重要度高）**: `<strong>`タグで囲む
- **その他**: 重要度に応じて`<strong>`や`<em>`タグを使用

### Openable Alertのアクセシビリティ
- `aria-expanded`: 展開状態を示す（`true`/`false`）
- `aria-controls`: 制御対象の要素IDを指定
- `aria-hidden`: コンテンツの表示状態を示す（`true`/`false`）

## アイコン一覧

### 標準アイコン
- `check`: チェックマーク（成功）
- `warning-l`: 警告（危険・警告）
- `info-l`: 情報（情報・警告）
- `point-l`: ポイント（プロモーション）
- `campaign-l`: キャンペーン（プロモーション）
- `chevron-right`: 右矢印（リンク表示）
- `chevron-up`: 上矢印（開閉表示）

## Cookie制御（Deletable Alert）

### 仕様
- IDが`cookie`のキー名になる
- `data-duration`で保存期間を指定（最大7日）
- Cookie存在時は該当アラートが非表示になる
- ページリロード後も状態が保持される

## 実装時の注意点

1. **一意のID**: Deletable AlertとOpenable Alertには一意のIDを付与
2. **アクセシビリティ**: 重要度に応じた適切なHTMLタグを使用
3. **アイコン**: 各アラートタイプに適切なアイコンを設定
4. **Cookie制御**: Deletable Alertのdata-duration設定を忘れずに
5. **JavaScript依存**: 機能に応じた適切なJSファイルを読み込む

## トラブルシューティング

- 正しく動作しない場合はページをリロードしてください
- Deletable AlertはCookie（hide_a）が保存されていない時のみ表示されます
- 必要なCSS/JSファイルが読み込まれているか確認してください