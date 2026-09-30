# xfeed-assets — durable public media host

Agent-managed public repository used as a **durable** host for scheduled-post media
(xFeed / MaHeaven Buffer queue). This repository is **not** subject to
`minio-daily-cleanup` on Server Inti and has no TTL.

## Why this exists

`s3.freeat.me/xfeed` and `/xfeed-video` are a **short-lived render cache** (~24 h TTL):
the Inti cron `minio-daily-cleanup` (`0 0 * * *`) wipes `xfeed` (keeping the avatar)
and empties `xfeed-video`. A Buffer queue item with a future `dueAt` needs its asset
URL fetchable **until publish time** (days later), so that host cannot serve scheduled
posts.

## Contents

| Path | Bytes | sha256 |
|---|---|---|
| `assets/tiktok-native-1-tue-0400.mp4` | 5295144 | `ef63a30478d24ed425161262be85005ea468a19b8a02282edd7c17fcfc3777d7` |
| `assets/tiktok-native-2-sat-0400.mp4` | 3973026 | `c25ff2e1e669e0f7dc378712e9a25f657117da4ad83dfdac3c19efcaee37cb65` |

Slots: Tue 2026-10-06 04:00 UTC and Sat 2026-10-10 04:00 UTC (MAH-81 pilot window).

## Public base URL

```
https://raw.githubusercontent.com/alifmaheaven/xfeed-assets/main/assets/
```

Direct:
- https://raw.githubusercontent.com/alifmaheaven/xfeed-assets/main/assets/tiktok-native-1-tue-0400.mp4
- https://raw.githubusercontent.com/alifmaheaven/xfeed-assets/main/assets/tiktok-native-2-sat-0400.mp4

No credential value is stored in this repository.
