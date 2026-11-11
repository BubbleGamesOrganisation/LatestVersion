# LatestVersion
Latest version number for the app to fetch for the force update feature.

The app reads `version.json` from:

```
https://raw.githubusercontent.com/BubbleGamesOrganisation/LatestVersion/main/version.json
```

## Fields

Each platform has its own entry, because the App Store and Google Play approve
releases at different times.

| Field     | Meaning                                                                 |
|-----------|-------------------------------------------------------------------------|
| `latest`  | Newest version live in that store. Older apps show a dismissible "update available" prompt. |
| `minimum` | Oldest version allowed to run. Older apps show a blocking update screen. |

Versions are the `x.y.z` part of `version:` in the app's `pubspec.yaml`.

## Releasing

1. When a store **approves and publishes** a release, set that platform's
   `latest` to the new version. Do not change it before then: the update
   would not be downloadable yet.
2. Raise `minimum` only when a release breaks compatibility (the app's
   `contractVersion` changed) or an old version is broken, and only once that
   platform's `latest` is already at or above it.

Always keep `minimum <= latest` on each platform, otherwise players are locked
out with no update to install.

GitHub's raw CDN caches for a few minutes, so changes are not instant.
