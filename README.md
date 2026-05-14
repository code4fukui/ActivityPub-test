# ActivityPub-test for Deno

A minimal, file-based ActivityPub server built with Deno, designed for testing and learning the protocol.

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

## How It Works

This server operates by serving a collection of pre-defined JSON and XML files. When a request is made to a specific endpoint, the server:
1.  Reads the corresponding template file (e.g., a request to `/` reads `person.activity.json`).
2.  Dynamically replaces all instances of the placeholder URL `https://example.com/` with the real entrypoint URL you specify in `entrypoint.txt`.
3.  Serves the content with the appropriate `Content-Type` header.

The `/inbox` endpoint accepts POST requests and saves the received ActivityPub objects as timestamped JSON files in the `inbox/` directory. The `/outbox` is generated in-memory with hardcoded content from `server.js`.

## Features

-   **Serves Essential Endpoints**: Implements Actor, WebFinger, Host-Meta, NodeInfo, Inbox, Outbox, Followers, and Following.
-   **Customizable Identity**: Configure the server's public URL via a single `entrypoint.txt` file.
-   **Inbox Logging**: Logs all incoming activities to the `inbox/` directory for easy inspection.
-   **Simple Client**: Includes a `client.js` script for fetching ActivityPub objects from any server.

## Setup and Usage

### Prerequisites

-   [Deno](https://deno.land/) runtime

### Running the Server

1.  Create an `entrypoint.txt` file containing your server's public base URL. This URL must end with a `/`.

    ```sh
    echo "https://your-domain.example/" > entrypoint.txt
    ```

2.  Start the server, specifying a port number as an argument:

    ```sh
    deno run -A server.js 8015
    ```

## Interacting with the Server

A helper script, `client.js`, is provided to fetch content with the required `Accept: application/activity+json` header.

```sh
# Fetch the main actor profile
deno run -A client.js http://localhost:8015/

# Fetch the outbox
deno run -A client.js http://localhost:8015/outbox
```

The script will print the JSON response to the console and save it to a local file.

### Implemented Endpoints

| Path                      | Served File / Behavior             |
| ------------------------- | ---------------------------------- |
| `/`                       | `person.activity.json` (Actor)     |
| `/.well-known/host-meta`  | `host-meta.xml`                    |
| `/.well-known/webfinger`  | `webfinger.jrd.json`               |
| `/nodeinfo/2.1`           | `nodeinfo.json`                    |
| `/inbox`                  | `inbox.activity.json` (Logs POSTs) |
| `/outbox`                 | Dynamically generated from server  |
| `/followers`              | `followers.activity.json`          |
| `/following`              | `following.activity.json`          |

## License

MIT License — see [LICENSE](LICENSE).

Copyright (c) 2024 Taisuke Fukuno