# ActivityPub-test for Deno

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

This project provides a simple ActivityPub server built with Deno.

## Features

- Implements the ActivityPub protocol
- Supports creating, sharing, and receiving ActivityPub notes
- Customizable entrypoint URL
- Serves key endpoints like WebFinger, NodeInfo, inbox, and outbox
- Paginates the outbox collection

## Requirements

- [Deno](https://deno.land/)

## Usage

1.  Set your entrypoint URL in the `entrypoint.txt` file. This URL will be used to replace the `https://example.com/` placeholder in responses.
    ```
    https://your-domain.example/
    ```

2.  Run the server with the desired port number:
    ```sh
    deno run -A server.js 8015
    ```

## API / Endpoints

To inspect the server's endpoints, you can use the provided `client.js` script, which fetches a URL with the required `Accept: application/activity+json` header.

```sh
deno run -A client.js http://localhost:8015/
```

The server provides the following main endpoints:

-   `/`: The main actor (`Person`) object.
-   `/.well-known/host-meta`: Host metadata for discovery.
-   `/.well-known/webfinger`: WebFinger endpoint to find the actor profile.
-   `/inbox`: The inbox for receiving activities from other servers.
-   `/outbox`: A collection of the user's activities (notes). Supports pagination via the `?page=` query parameter.
-   `/followers`: A collection of the actor's followers.
-   `/following`: A collection of actors the actor is following.
-   `/nodeinfo/2.1`: NodeInfo data describing the server.

## License

This project is available under the MIT License.

Copyright (c) 2024 Taisuke Fukuno