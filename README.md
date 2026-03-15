# ActivityPub-test for Deno

This project provides a simple ActivityPub server built with Deno.

## Features

- Implements the ActivityPub protocol
- Supports creating, sharing, and receiving ActivityPub notes
- Customizable entrypoint URL

## Usage

1. Set your entrypoint URL in the `entrypoint.txt` file:
   ```
   https://example.com/
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

This project is licensed under the MIT License.

Copyright (c) 2024 Taisuke Fukuno