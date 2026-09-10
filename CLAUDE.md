# CLAUDE.md

Standing rules for working in this repo. This is a personal collection
of Jellyfin plugin forks patched for Jellyfin 12.0 (.NET 10), for
personal use on one Jellyfin server only — not for publishing or
redistribution.

## Hard rule: never change a plugin's GUID

**Never** change a plugin's original GUID — wherever it's declared
(`build.yaml`, `meta.json`, a `.csproj`, or hardcoded in the plugin's
main class as `override Guid Id => ...`). Jellyfin identifies a plugin
by this GUID; it must keep seeing "the same plugin" so that switching
back to the official upstream build later is a clean swap, not a
reinstall. Before patching any plugin, confirm you know where its real
GUID lives — some repos' `build.yaml` is stale or wrong (see
[`docs/STATUS.md`](docs/STATUS.md) for a documented example) — and
verify the GUID is unchanged after patching.

## Research before patching, and before guessing at a compile error

Before patching any plugin, or when hitting an unfamiliar compile
error, research first. Never guess a replacement API. Check, in order:

1. The official Jellyfin 12.0 release notes:
   - https://jellyfin.org/posts/jellyfin-release-12.0/
   - https://github.com/jellyfin/jellyfin/releases/tag/v12.0
2. The current Jellyfin plugin development docs.
3. If still unresolved, search the `jellyfin/jellyfin` repo itself for
   the specific API/class that changed.

## What a "JF12 patch" is (and isn't)

A JF12 patch means:
- Bump the target framework to `net10.0`.
- Bump `Jellyfin.Controller` / `Jellyfin.Model` NuGet references to the
  latest 12.0.x.
- Fix whatever compile errors result from those two bumps.

Nothing more, unless it's proven necessary while actually building.
Don't refactor, modernize, or "improve" code beyond what's needed to
compile and run on JF12.

## "It compiles" is not "it works"

A plugin only gets marked `patched-tested-live` in
[`docs/STATUS.md`](docs/STATUS.md) after it has actually loaded and
been functionally tested against a real Jellyfin 12 server. A green
build alone only earns `patched-untested`.

## Check upstream before patching

Before starting work on any plugin, check its `upstream` git remote
for a JF12-compatible release published since the last check. If
upstream has already shipped JF12 support, don't patch — just update
that plugin's row in [`docs/STATUS.md`](docs/STATUS.md) to
`upstream shipped it` and move on to the next plugin.
