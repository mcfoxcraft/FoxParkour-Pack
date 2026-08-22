# FoxParkour Pack (public distribution)

Public download mirror for the **Foxcraft parkour resource pack** — hats, plushies, balloons,
backpacks and offhand cosmetics. This repo holds **only the built pack zip**, published as GitHub
Releases so Minecraft clients can fetch it anonymously over GitHub's Fastly CDN.

The pack **source** (models, textures, sounds, item definitions, build tooling) lives in the
private `mcfoxcraft/FoxParkour-Resource-Pack` repo. Don't edit anything here by hand — releases are
produced from that source by `./release-pack.sh vX.Y.Z`.

## Current release

None yet — parkour is still served the legacy pack. The **[latest
release](https://github.com/mcfoxcraft/FoxParkour-Pack/releases/latest)** page always carries the
URL, the SHA-1 and a ready-to-paste `server.properties` block.

Pin the tag rather than using `/latest` in `server.properties`: clients cache by hash, so the URL
and `resource-pack-sha1` must move together. A stale hash makes every client keep its cached copy
of the previous pack, which looks exactly like the update doing nothing.

## Serving it

```properties
resource-pack=https://github.com/mcfoxcraft/FoxParkour-Pack/releases/download/<tag>/foxparkour-resourcepack.zip
resource-pack-sha1=<sha1 from the release notes>
resource-pack-id=b48ba020-7fdd-3439-bcb9-18ea951b9392
require-resource-pack=false
```

`resource-pack-id` is deliberately **the same value oneblock uses**. With it blank, the client
derives a pack's identity from its URL, so parkour's pack and the Foxcraft pack land in different
slots and both stay loaded at once — a Bungee server switch never drops the previous server's pack.
Matching ids make each server's pack *replace* the other instead.
