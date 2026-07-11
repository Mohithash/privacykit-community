# Privacy Kit — Community configs

Public, browsable spoofing configs for [Privacy Kit](https://github.com/Mohithash/Privacy_Kit). The app's
**Settings → Community** section reads this folder over `raw.githubusercontent.com` so users can browse and
apply configs shared by others.

## How it works

- **`index.json`** — the catalog the app lists. Each entry points at a config file under `configs/`.
- **`configs/*.json`** — one file per config (the full identifiers + custom hooks bundle).

## Config format

```json
{
  "formatVersion": 1,
  "id": "unique-kebab-id",
  "title": "Human title",
  "description": "What it does",
  "author": "your-handle",
  "scope": "app" | "universal",
  "packageName": "com.example.app",   // required for scope "app"
  "identifiers": { "android_id": "…", "build_model": "…" },  // overrides applied to the app's active profile
  "customHooks": [ /* method | field | substitute rules, same schema as the in-app Custom Hooks editor */ ]
}
```

- **universal** configs apply their `customHooks` globally (each hook should carry `"allowGlobal": true`).
- **app** configs apply `identifiers` onto the target app's active profile and merge app-scoped `customHooks`.

## Submitting a config (review queue)

Users submit from inside the app (**Community → Share your config → Build & submit for review**), which opens a
prefilled GitHub issue containing the config JSON. Maintainers review it and, if approved, add the file under
`configs/` and add an entry to `index.json` — after which it appears in everyone's app.

> ⚠️ Community configs are user-submitted. Review hooks before merging: a `substitute`/`method`/`field` rule can
> change what apps read. The app validates structure with `CustomHookValidator`, but semantics are on the reviewer.
