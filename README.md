# JF12-patch-multi-plugins

Personal mono-repo of Jellyfin plugin forks, patched to run on Jellyfin
12.0 (.NET 10) while waiting for each plugin's official maintainers to
ship their own compatible releases. Each plugin lives as a git
submodule under [`plugins/`](plugins/), forked from its upstream repo
with the original plugin GUID **deliberately preserved** — so Jellyfin
keeps treating it as "the same plugin" and this repo's build can be
swapped back out for the official one the moment upstream ships JF12
support. See [`docs/STATUS.md`](docs/STATUS.md) for per-plugin status,
and [`CLAUDE.md`](CLAUDE.md) for the patching rules this project
follows.

**This is personal use only**, for my own Jellyfin server. It is not
meant to be published, redistributed, or used as a general-purpose
plugin repository by anyone else.

## Using this as a plugin repository (not yet available)

Once a `manifest.json` exists at the root of this repo (it does not
yet — this is scaffolding only, no plugins have been built), compiled
plugin `.zip` files in [`dist/`](dist/) will be servable straight from
GitHub via `raw.githubusercontent.com`, and this repo could then be
added as a plugin repository in Jellyfin:

1. In Jellyfin, go to **Dashboard → Plugins → Repositories → Add**.
2. Paste the raw URL to this repo's `manifest.json`, e.g.:
   `https://raw.githubusercontent.com/<owner>/JF12-patch-multi-plugins/main/manifest.json`
3. Go to **Catalog**, find the patched plugin, and install it.

This step doesn't work yet — `manifest.json` hasn't been generated.
