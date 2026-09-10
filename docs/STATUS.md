# Plugin Status

Snapshot taken 2026-09-10, right after scaffolding. No patching has happened yet.

| Plugin | Upstream repo | Current targetAbi | JF12 status | Notes |
|---|---|---|---|---|
| anilist | [jellyfin/jellyfin-plugin-anilist](https://github.com/jellyfin/jellyfin-plugin-anilist) | `12.0.0.0` (net10.0, `Jellyfin.Controller 12.*-*`) | upstream shipped it | build.yaml and .csproj already target JF12 on the default branch. No patch needed — just track upstream releases. |
| custom-tabs | [IAmParadox27/jellyfin-plugin-custom-tabs](https://github.com/IAmParadox27/jellyfin-plugin-custom-tabs) | no build.yaml/meta.json — csproj drives target via a `JellyfinVersion` MSBuild property, currently `10.11.2` → net9.0 | needs patch | No manifest file at all; targetAbi isn't declared the usual way. GUID (in `CustomTabsPlugin.cs`): `fbacd0b6-fd46-4a05-b0a4-2045d6a135b0`. Multi-version build logic (10.10.7 / 10.11.0 / 10.11 conditionals) will need a JF12 branch added carefully without breaking the GUID or existing targets. |
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
- **patched-untested** — compiles against JF12 but has not been loaded/tested on a real server.
- **patched-tested-live** — loaded and functionally verified against a real Jellyfin 12 server.
- **upstream shipped it** — upstream already publishes a JF12-compatible build; no fork/patch needed, just consume upstream.
