# xfeed-assets — durable public media host

Agent-managed public repository used as a **durable** host for scheduled-post media
(xFeed / MaHeaven Buffer queue). This repository is **not** subject to
`minio-daily-cleanup` on Server Inti and has no TTL.

## Why this exists

`s3.freeat.me/xfeed` and `/xfeed-video` are a **short-lived render cache** (~24 h TTL):
the Inti cron `minio-daily-cleanup` (`0 0 * * *`) wipes `xfeed` (keeping the avatar)
and empties `xfeed-video`. A Buffer queue item with a future `dueAt` needs its asset
URL fetchable **until publish time** (days later), so that host cannot serve scheduled
posts. (MAH-122; study §7 of MAH-66.)

## Public base URLs

Two independent public routes serve the same bytes with `Content-Type: video/mp4`,
HTTP 200, `Accept-Ranges: bytes` (Range → 206):

| Route | Base URL | Notes |
|---|---|---|
| GitHub Pages | `https://alifmaheaven.github.io/xfeed-assets/` | primary |
| jsDelivr (pinned tag) | `https://cdn.jsdelivr.net/gh/alifmaheaven/xfeed-assets@v2026-09-30/` | immutable CDN mirror |

## Cycle-1 TikTok edits (MAH-122 / MAH-81)

| Path | Bytes | sha256 |
|---|---|---|
| `assets/tiktok-native-1-tue-0400.mp4` | 5295144 | `ef63a30478d24ed425161262be85005ea468a19b8a02282edd7c17fcfc3777d7` |
| `assets/tiktok-native-2-sat-0400.mp4` | 3973026 | `c25ff2e1e669e0f7dc378712e9a25f657117da4ad83dfdac3c19efcaee37cb65` |

Slots: Tue 2026-10-06 04:00 UTC and Sat 2026-10-10 04:00 UTC (MAH-81 pilot window).

Direct:
- https://alifmaheaven.github.io/xfeed-assets/assets/tiktok-native-1-tue-0400.mp4
- https://alifmaheaven.github.io/xfeed-assets/assets/tiktok-native-2-sat-0400.mp4

## MAH-105 week-1 set (35 assets, unblocks MAH-87 / MAH-82)

Prefix: `mah105-w1/` — 28 IG Reels + 7 YT Shorts, each byte-identical to the
MAH-105 manifest sha256. Per-file hashes: `mah105-w1/MANIFEST.json`.

Example:
- https://alifmaheaven.github.io/xfeed-assets/mah105-w1/mah77-2026-w41-ig-reels-20261005T10.mp4

## Durability

- GitHub Pages and jsDelivr are third-party-hosted, **not** touched by any Inti cron.
- The `v2026-09-30` tag pins the jsDelivr mirror; that URL keeps serving these exact
  bytes even if `main` is later changed.
- No credential value is stored in this repository.
