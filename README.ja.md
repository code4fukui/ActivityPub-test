# ActivityPub-test for Deno

Denoで構築された、最小限のファイルベースのActivityPubサーバーです。プロトコルのテストや学習を目的として設計されています。

## 仕組み

このサーバーは、事前に定義されたJSONファイルおよびXMLファイルのコレクションを提供することで動作します。特定のエンドポイントにリクエストが行われると、サーバーは以下の処理を行います。
1. 対応するテンプレートファイルを読み込みます（例: `/` へのリクエストでは `person.activity.json` を読み込みます）。
2. プレースホルダーURLである `https://example.com/` のすべてのインスタンスを、`entrypoint.txt` で指定した実際のエントリーポイントURLに動的に置換します。
3. 適切な `Content-Type` ヘッダーを付与してコンテンツを提供します。

`/inbox` エンドポイントはPOSTリクエストを受け付け、受信したActivityPubオブジェクトをタイムスタンプ付きのJSONファイルとして `inbox/` ディレクトリに保存します。`/outbox` は、`server.js` にハードコードされた内容を用いてインメモリで生成されます。

## 特徴

- **必須エンドポイントの提供**: Actor、WebFinger、Host-Meta、NodeInfo、Inbox、Outbox、Followers、Followingを実装しています。
- **カスタマイズ可能なアイデンティティ**: 単一の `entrypoint.txt` ファイルを通じて、サーバーの公開URLを設定できます。
- **Inboxのログ記録**: すべての受信アクティビティを `inbox/` ディレクトリにログとして保存し、簡単に内容を確認できます。
- **シンプルなクライアント**: 任意のサーバーからActivityPubオブジェクトを取得するための `client.js` スクリプトが付属しています。

## セットアップと使い方

### 前提条件

- [Deno](https://deno.land/) ランタイム

### サーバーの実行

1. サーバーの公開ベースURLを記述した `entrypoint.txt` ファイルを作成します。このURLは必ず `/` で終わる必要があります。

    ```sh
    echo "https://your-domain.example/" > entrypoint.txt
    ```

2. ポート番号を引数に指定してサーバーを起動します。

    ```sh
    deno run -A server.js 8015
    ```

## サーバーとの通信

必要な `Accept: application/activity+json` ヘッダーを付与してコンテンツを取得するためのヘルパースクリプト `client.js` が用意されています。

```sh
# メインアクターのプロファイルを取得
deno run -A client.js http://localhost:8015/

# Outboxを取得
deno run -A client.js http://localhost:8015/outbox
```

このスクリプトは、JSONレスポンスをコンソールに出力するとともに、ローカルファイルに保存します。

### 実装されているエンドポイント

| パス                      | 提供されるファイル / 動作             |
| ------------------------- | ---------------------------------- |
| `/`                       | `person.activity.json` (Actor)     |
| `/.well-known/host-meta`  | `host-meta.xml`                    |
| `/.well-known/webfinger`  | `webfinger.jrd.json`               |
| `/nodeinfo/2.1`           | `nodeinfo.json`                    |
| `/inbox`                  | `inbox.activity.json` (POSTリクエストをログ記録) |
| `/outbox`                 | サーバー内で動的に生成               |
| `/followers`              | `followers.activity.json`          |
| `/following`              | `following.activity.json`          |

## ライセンス

MIT License — 詳細は [LICENSE](LICENSE) を参照してください。

Copyright (c) 2024 Taisuke Fukuno
