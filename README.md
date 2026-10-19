# thumbbreak-rules

Screen-detection rules for the Thumbbreak Android app. The app downloads [`rules.json`](rules.json) once a day, so a fix ships here when Instagram or YouTube rename their Reels/Shorts screens, without a new app release.

The app only reads this file. No user data is ever sent.

## Format

```json
{
  "version": 2,
  "minAppVersion": 1,
  "apps": {
    "instagram": { "viewIds": ["clips_viewer_view_pager"], "tabLabels": ["Reels"] }
  }
}
```

- `version` must go up with every change, or the app ignores the file.
- `minAppVersion` is the lowest app `versionCode` that understands this file.
- `apps` keys are app ids (`instagram`, `youtube`, `facebook`, `snapchat`). An entry replaces that app's built-in rule.
- `viewIds` are resource names after `:id/`. `tabLabels` are bottom-tab labels that mean "on the surface" when selected. Generic tabs like "Home" or "Search" are rejected.

The app validates everything and falls back to its built-in rule for any entry it rejects.
