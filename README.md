# FoxParkour Pack (public distribution)

Public download mirror for the **Foxcraft parkour resource pack** — hats, plushies, balloons,
backpacks and offhand cosmetics. This repo holds **only the built pack zip**, published as GitHub
Releases so Minecraft clients can fetch it anonymously over GitHub's Fastly CDN.

The pack **source** (models, textures, sounds, item definitions, build tooling) lives in the
private `mcfoxcraft/FoxParkour-Resource-Pack` repo. Don't edit anything here by hand — releases are
produced from that source by `./release-pack.sh vX.Y.Z`.

## Current release

**[v1.7.0](https://github.com/mcfoxcraft/FoxParkour-Pack/releases/tag/v1.7.0)** — SHA-1
`1f3ebd84556d06dd3e48ddf277e0c6030148c679`

Adds FoxGear's Vladimir set (`foxgear:` weapons and the wings' equipment asset, for FoxParkour's FoxGear
cosmetics), ten animal balloons, the sulfur set, the bard and assassin helmets and ten Foxcraft backpacks
(custom_model_data 228-234 and 238-270; Bedrock pack 1.5.0). They show once `cosmetics.yml` lists them.
Otherwise unchanged from v1.6.1.

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
