# ActivityPub-test for Deno

このプロジェクトは、Denoで実装されたシンプルなActivityPubサーバーです。

## 機能

- ActivityPubの基本的なサーバー機能
- WebFinger、host-meta、NodeInfoに対応
- 投稿 (`Note`) の作成と配信 (`outbox`)
- ページネーション付きの `outbox`
- アクティビティの受信 (`inbox`) とログ保存
- `entrypoint.txt` によるドメインのカスタマイズ

## 必要環境

- [Deno](https://deno.com/)

## 使い方

### 1. サーバーのセットアップ

`entrypoint.txt` ファイルを作成し、サーバーを公開するURL（末尾にスラッシュ `/` を含む）を記述します。

```
https://your-domain.example/
```

### 2. サーバーの実行

以下のコマンドでサーバーを起動します。ポート番号は任意に指定できます（デフォルト: 8000）。

```sh
deno run -A server.js 8015
```

### 3. 動作確認

付属のクライアントスクリプトを使って、サーバーからデータを取得できます。取得したデータはJSONファイルとして保存されます。

```sh
# ユーザー情報を取得
deno run -A client.js http://localhost:8015/

# outboxを取得
deno run -A client.js http://localhost:8015/outbox
```

## 主要なエンドポイント

- `GET /`: Personオブジェクト (プロフィール)
- `GET /.well-known/host-meta`: host-meta情報
- `GET /.well-known/webfinger`: WebFinger情報
- `GET /nodeinfo/2.1`: NodeInfo情報
- `POST /inbox`: アクティビティを受信し、`inbox/` ディレクトリにJSONファイルとして保存します。
- `GET /outbox`: 投稿の一覧 (OrderedCollection)。ページネーションに対応しています (`?page=1`)。
- `GET /followers`: フォロワーの一覧
- `GET /following`: フォロー中の一覧

## ライセンス

このプロジェクトはMITライセンスの下で提供されています。

Copyright (c) 2024 Taisuke Fukuno