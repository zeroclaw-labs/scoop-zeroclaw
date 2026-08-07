# scoop-zeroclaw

Scoop bucket for [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw) — the fastest, smallest AI assistant.

## Installation

```powershell
scoop bucket add zeroclaw https://github.com/zeroclaw-labs/scoop-zeroclaw
scoop install zeroclaw
```

## Updating

```powershell
scoop update zeroclaw
```

## Automation

`bucket/zeroclaw.json` is kept current by two independent layers:

1. **Push on release.** `pub-scoop.yml` in
   [zeroclaw-labs/zeroclaw](https://github.com/zeroclaw-labs/zeroclaw) pushes the
   manifest as part of a stable release, so a new version lands here
   immediately. This path needs a cross-repo token.
2. **Excavator self-heals.** `.github/workflows/excavator.yml` runs here every
   4 hours, reads the manifest's `checkver` and `autoupdate` blocks, recomputes
   `version`, `url`, and `hash` from the GitHub release, and commits using this
   repository's own `GITHUB_TOKEN`. No cross-repo credential is involved, so if
   layer 1 fails the bucket still catches up on its own.

Because excavator drives `checkver` and `autoupdate`, those blocks are
load-bearing. Do not remove them when editing the manifest.
