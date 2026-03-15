# ActivityPub-test for Deno

このプロジェクトは、Denoで構築したシンプルなActivityPubサーバを提供します。

## 機能

- ActivityPubプロトコルを実装
- ActivityPubノートの作成、共有、受信をサポート
- エントリポイントURLをカスタマイズ可能

## 使い方

1. `entrypoint.txt`にエントリポイントURLを設定します:
   ```
   https://your-domain.example/
   ```

2. 指定のポート番号でサーバを実行します:
   ```sh
   deno run -A server.js 8015
   ```

## データ・API

サーバの動作を確認するには、`Accept: application/activity+json`ヘッダを付けてフェッチします:
```sh
deno run -A client.js [url]
```

## ライセンス

このプロジェクトはMITライセンスの下で提供されています。

Copyright (c) 2024 Taisuke Fukuno