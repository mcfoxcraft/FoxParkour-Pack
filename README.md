# FoxParkour Pack (public distribution)

Public download mirror for the **Foxcraft parkour resource pack** — hats, plushies, balloons,
backpacks and offhand cosmetics. This repo holds **only the built pack zip**, published as GitHub
Releases so Minecraft clients can fetch it anonymously over GitHub's Fastly CDN.

The pack **source** (models, textures, sounds, item definitions, build tooling) lives in the
private `mcfoxcraft/FoxParkour-Resource-Pack` repo. Don't edit anything here by hand — releases are
produced from that source by `./release-pack.sh vX.Y.Z`.

## Current release

**[v1.9.0](https://github.com/mcfoxcraft/FoxParkour-Pack/releases/tag/v1.9.0)** — SHA-1
`a9c0102617fca806d449ad30163cfecd9e7a56df`

The menu theme's button icons are redrawn flat (no slab behind the pictures, centred, clearer keys and states), and
the notification panel gets its headline-only pieces and a smaller headline font (`foxparkour:toast_small`), which
FoxParkour builds with the small-headline toasts need. Every cosmetic model now names a particle texture (no more
"Missing texture references" warnings on 26.3). Otherwise unchanged from v1.8.1.

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
