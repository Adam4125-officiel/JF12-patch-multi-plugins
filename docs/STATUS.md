# Plugin Status

Snapshot taken 2026-09-10. Scaffolding + first patching pass in progress (custom-tabs, editors-choice, skinmanager).

| Plugin | Upstream repo | Current targetAbi | JF12 status | Notes |
|---|---|---|---|---|
| anilist | [jellyfin/jellyfin-plugin-anilist](https://github.com/jellyfin/jellyfin-plugin-anilist) | `12.0.0.0` (net10.0, `Jellyfin.Controller 12.*-*`) | upstream shipped it | build.yaml and .csproj already target JF12 on the default branch. No patch needed — just track upstream releases. |
| custom-tabs | [IAmParadox27/jellyfin-plugin-custom-tabs](https://github.com/IAmParadox27/jellyfin-plugin-custom-tabs) | `12.0.0.0` (net10.0, `Jellyfin.Controller/Model/Common/Data 12.0.0`) | patched — build OK, NOT YET tested live | Re-checked upstream 2026-09-10, no JF12 release since scaffolding. GUID unchanged: `fbacd0b6-fd46-4a05-b0a4-2045d6a135b0`. Retargeted via the existing `JellyfinVersion` MSBuild property (now `12.0.0`); added a `JellyfinVersionSpecific/12.0/StartupServiceHelper.cs` (copy of the 10.11 variant — it already used the modern enum-based `TaskTriggerInfoType` API, not the removed string-const one) since the csproj's per-version conditionals would otherwise strip the helper class entirely and fail to compile. Zero other code changes needed — plugin doesn't touch any of the JF12 breaking APIs (search/user-manager/item-repository/subtitles/etc). Built clean, 0 errors. Packaged: `dist/custom-tabs/custom-tabs-0.2.0.0-jf12.zip`. manifest.json entry added. |
| editors-choice | [lachlandcp/jellyfin-editors-choice-plugin](https://github.com/lachlandcp/jellyfin-editors-choice-plugin) | no build.yaml/meta.json — csproj: net9.0, `Jellyfin.Controller 10.11.0` | needs patch | GUID (in `Plugin.cs`): `70bb2ec1-f19e-46b5-b49a-942e6b96ebae`. |
| opds | [jellyfin/jellyfin-plugin-opds](https://github.com/jellyfin/jellyfin-plugin-opds) | `12.0.0.0` (net10.0, `Jellyfin.Controller 12.*-*`) | upstream shipped it | build.yaml and .csproj already target JF12 on the default branch. No patch needed — just track upstream releases. |
| opensubtitles | [jellyfin/jellyfin-plugin-opensubtitles](https://github.com/jellyfin/jellyfin-plugin-opensubtitles) | `12.0.0.0` (net10.0, `Jellyfin.Controller 12.*-*`) | upstream shipped it | build.yaml and .csproj already target JF12 on the default branch. No patch needed — just track upstream releases. |
| playbackreporting | [jellyfin/jellyfin-plugin-playbackreporting](https://github.com/jellyfin/jellyfin-plugin-playbackreporting) | `12.0.0.0` (net10.0, `Jellyfin.Controller 12.*-*`) | upstream shipped it | build.yaml and .csproj already target JF12 on the default branch. No patch needed — just track upstream releases. |
| reports | [jellyfin/jellyfin-plugin-reports](https://github.com/jellyfin/jellyfin-plugin-reports) | `12.0.0.0` (net10.0, `Jellyfin.Controller 12.*-*`) | upstream shipped it | build.yaml and .csproj already target JF12 on the default branch. No patch needed — just track upstream releases. |
| skinmanager | [danieladov/jellyfin-plugin-skin-manager](https://github.com/danieladov/jellyfin-plugin-skin-manager) | build.yaml is **stale/wrong** (unchanged since the first commit in 2020 — it describes an unrelated plugin, "jellyfin-plugin-tmdbboxsets", with `jellyfin_version: 10.5.0`, `netstandard2.1`, and a GUID that doesn't match the actual plugin code). Real current target per `.csproj`: net8.0, `Jellyfin.Controller 10.10.0`. | needs patch | Don't trust build.yaml for this repo. Real GUID is in `Jellyfin.Plugin.SkinManager/Plugin.cs`: `e9ca8b8e-ca6d-40e7-85dc-58e536df8eb3` — use **this** one when patching, never the one in build.yaml. |
| jellybulletin | [skijk/jellyfin-plugin-jellybulletin](https://github.com/skijk/jellyfin-plugin-jellybulletin) | `12.0.0.0` (net10.0, `Jellyfin.Controller 12.0.0`) | upstream shipped it | build.yaml and .csproj already target JF12 natively. No patch needed — just track upstream releases (and still worth a functional smoke test before fully trusting it, since it's a small community plugin rather than an official jellyfin org one). |

## Legend (JF12 status column)

- **needs patch** — not yet started.
- **in progress** — actively being patched.
- **patched — build OK, NOT YET tested live** (aka patched-untested) — compiles against JF12 but has not been loaded/tested on a real server.
- **patched-tested-live** — loaded and functionally verified against a real Jellyfin 12 server.
- **upstream shipped it** — upstream already publishes a JF12-compatible build; no fork/patch needed, just consume upstream.
