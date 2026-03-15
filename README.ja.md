# ActivityPub-test for Deno

ActivityPubのテストプロジェクトです。Deno上でActivityPubサーバを簡単に構築できます。

## 使い方

`entrypoint.txt`にドメイン名を設定してください。
```
https://example.com/
```

サーバを起動します。
```sh
deno run -A server.js 8015
```

## 動作確認

`Accept: application/activity+json`ヘッダを付けてフェッチします。
```sh
deno run -A client.js [url]
```

## ライセンス

MIT License

Copyright (c) 2024 Taisuke Fukuno