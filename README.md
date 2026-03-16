# ActivityPub-test for Deno

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

This project provides a simple ActivityPub server built with Deno.

## Features

- Implements the ActivityPub protocol
- Supports creating, sharing, and receiving ActivityPub notes
- Customizable entrypoint URL

## Usage

1. Set your entrypoint URL in the `entrypoint.txt` file:
   ```
   https://your-domain.example/
   ```

2. Run the server with the desired port number:
   ```sh
   deno run -A server.js 8015
   ```

## Fetching Data

To check the server's behavior, fetch content with the `Accept: application/activity+json` header:
```sh
deno run -A client.js [url]
```

## License

MIT License — see [LICENSE](LICENSE).