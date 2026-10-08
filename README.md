# FoxParkour Pack (public distribution)

Public download mirror for the **Foxcraft parkour resource pack** — hats, plushies, balloons,
backpacks and offhand cosmetics. This repo holds **only the built pack zip**, published as GitHub
Releases so Minecraft clients can fetch it anonymously over GitHub's Fastly CDN.

The pack **source** (models, textures, sounds, item definitions, build tooling) lives in the
private `mcfoxcraft/FoxParkour-Resource-Pack` repo. Don't edit anything here by hand — releases are
produced from that source by `./release-pack.sh vX.Y.Z`.

## Current release

**[v1.5.0](https://github.com/mcfoxcraft/FoxParkour-Pack/releases/tag/v1.5.0)** — SHA-1
`18ff57bccc3c49f36e53c134e2354d7bb308ccba`

Seats the six original backpacks on the wearer's back (they sat from the shoulders to above the head),
puts the planet balloons' string knot on the stand's axis, and centres the six floating balloons
(clouds, crescent moon, octopus, pufferfish) over the leash's end. Adds the 40 other backpacks from
the Foxcraft pack (`custom_model_data` 184–223); they show once the server's `cosmetics.yml` lists them.
Serve it with the five planet balloons at `offsets.forward: 0.0` in FoxParkour's `cosmetics.yml`
(FoxParkour 0.5 before this pack), ideally with FoxParkour
[#1441](https://github.com/mcfoxcraft/FoxParkour/pull/1441).

The **[latest release](https://github.com/mcfoxcraft/FoxParkour-Pack/releases/latest)** page always
carries the URL, the SHA-1 and a ready-to-paste `server.properties` block.

Pin the tag rather than using `/latest` in `server.properties`: clients cache by hash, so the URL
and `resource-pack-sha1` must move together. A stale hash makes every client keep its cached copy
of the previous pack, which looks exactly like the update doing nothing.

## Serving it

```properties
resource-pack=https://github.com/mcfoxcraft/FoxParkour-Pack/releases/download/v1.0.0/foxparkour-resourcepack.zip
resource-pack-sha1=6e410de1a0fe07fc0861c4e5a79c03590f8ccd54
resource-pack-id=b48ba020-7fdd-3439-bcb9-18ea951b9392
require-resource-pack=false
```

> **Do not point a live server at v1.0.0 on its own.** Cosmetics in this pack are addressed by the
> `minecraft:item_model` component, which only FoxParkour with
> [PR #909](https://github.com/mcfoxcraft/FoxParkour/pull/909) writes, and only when the live
> `cosmetics.yml` carries the `itemModel` keys. Pack, jar and config must land in the same restart —
> either half alone leaves cosmetics unresolved on 1.21.4+ clients.

`resource-pack-id` is deliberately **the same value oneblock uses**. With it blank, the client
derives a pack's identity from its URL, so parkour's pack and the Foxcraft pack land in different
slots and both stay loaded at once — a Bungee server switch never drops the previous server's pack.
Matching ids make each server's pack *replace* the other instead.
