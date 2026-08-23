# Kaivor Webhook Connector

Official, verified Webhook connector package for [Kaivor](https://kaivorai.com).

This repository distributes the prebuilt `.kaivor-plugin` asset used by Kaivor's local plugin manager. Users install it with one click inside the desktop application and do not need Git, Node.js, Python, or another package manager.

## Current status

Version `1.0.0` is the first declarative package used to validate the complete Kaivor plugin lifecycle:

- discovery in the official catalog;
- HTTPS download from an immutable GitHub Release;
- SHA-256 integrity verification;
- manifest and permission validation;
- atomic local installation;
- enable, disable, and uninstall operations;
- persistence in the current user's Kaivor profile.

> [!IMPORTANT]
> Version `1.0.0` is a declarative foundation package. It registers the Webhook connector metadata but does not send webhook requests yet. An executable connector runtime will be delivered separately after process isolation and permission brokering are available in Kaivor.

## Install

1. Open the Kaivor desktop application.
2. Go to **Settings → Plugins**.
3. Find **Webhook Connector**.
4. Select **Install**.

Kaivor downloads the release asset, validates it, and installs it into the local user profile. The plugin never invokes a system installer.

## Release

The current package is available from [Webhook Connector v1.0.0](https://github.com/rafaelduarteamaral/kaivor-plugin-webhook/releases/tag/v1.0.0).

| Property | Value |
| --- | --- |
| Package | `kaivor.connector.webhook-1.0.0.kaivor-plugin` |
| Format | Kaivor plugin envelope v1 |
| Size | 702 bytes |
| SHA-256 | `9661e4221a25685ab85fd783ae3e8ad244ecfd77e836f706e10e060404b9b1c5` |
| Permission | `network:https` |
| Publisher | Kaivor |

The package is also indexed by the [official Kaivor plugin catalog](https://kaivorai.com/plugins/catalog.json).

## Package manifest

The v1 package declares the following identity and contribution:

```json
{
  "id": "kaivor.connector.webhook",
  "name": "Webhook Connector",
  "version": "1.0.0",
  "kind": "connector",
  "publisher": "Kaivor",
  "permissions": ["network:https"],
  "contributes": {
    "connectors": [
      {
        "id": "webhook",
        "name": "Webhook"
      }
    ]
  }
}
```

## Security model

Kaivor applies these controls before activating the package:

- remote assets must use HTTPS;
- package bytes must match the SHA-256 digest pinned by the catalog;
- package ID and version must match the selected catalog release;
- absolute paths and path traversal segments are rejected;
- package and individual-file size limits are enforced;
- v1 packages cannot execute JavaScript, native binaries, shell commands, or lifecycle hooks;
- package-provided strings are rendered as text, not executable HTML.

Never place webhook credentials, tokens, signing secrets, or customer URLs in this repository or inside a release package.

## Local installation paths

Installed content is managed by Kaivor under the operating-system user-data directory:

- macOS: `~/Library/Application Support/Kaivor/plugins/`
- Windows: `%APPDATA%\Kaivor\plugins\`
- Linux: `~/.config/Kaivor/plugins/`

## Roadmap

- isolated connector host process;
- versioned Kaivor plugin API;
- per-destination permission grants;
- secret storage through the operating-system credential vault;
- request signing and configurable headers;
- retries, timeouts, delivery history, and redacted diagnostics;
- automated package build, integrity generation, tests, and GitHub Releases.

## Related resources

- [Kaivor website](https://kaivorai.com)
- [Official plugin catalog](https://kaivorai.com/plugins/catalog.json)
- [Latest release](https://github.com/rafaelduarteamaral/kaivor-plugin-webhook/releases/latest)

## License

Copyright © Kaivor. Licensing terms for the plugin runtime and source distribution will be published with the executable implementation.
