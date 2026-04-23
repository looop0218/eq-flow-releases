# Changelog

All notable changes to EQ-Flow will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Release automation (`.github/workflows/release.yml`) extracts the section
matching the pushed tag and uses it as the GitHub Release body. Keep each
version heading in the exact form `## [X.Y.Z] - YYYY-MM-DD` (or
`## [X.Y.Z-rc1] - YYYY-MM-DD`) so the extractor can find it.

## [Unreleased]

## [0.5.3] - 2026-04-23

### Changed
- Auto-updater endpoint migrated to a dedicated public distribution repository (`looop0218/eq-flow-releases`). This is the first step of a two-phase repo split: source code stays in the existing `looop0218/eq-flow` (transitioning to private after this release), while binary releases move to the new `eq-flow-releases` repo. Existing v0.5.2 clients receive this release through the current endpoint and, from v0.5.3 onward, poll the new location for further updates.

### CI / tooling
- No workflow changes in this release. `release.yml` continues to publish to `looop0218/eq-flow` so existing users can auto-migrate via the established update path. A subsequent release (v0.5.4+) will switch the workflow to cross-repo publishing targeting `eq-flow-releases`, at which point `eq-flow` will be made private.

## [0.5.2] - 2026-04-23

### Fixed
- Auto Layout no longer teleports the graph when the viewport is panned or zoomed. The prior offset formula mixed screen-space pan (`viewport.x`) with flow-space coordinates and ignored zoom entirely, so panning caused the laid-out graph to fly off-screen in the opposite direction of the pan.
- Selection-mode Auto Layout now preserves the selected subgraph's original top-left corner instead of dragging it to the viewport origin, so surgical re-alignment of a few nodes stays inside the user's selected area.

### Changed
- `runAutoLayout` anchor policy: result is translated so the top-left corner of the laid-out subgraph matches its own ORIGINAL top-left corner. Viewport state is no longer consulted by the layout path — the viewport is a camera concern owned by `useViewControls`. Documented in `src/hooks/useGraphArrangement.ts` JSDoc with a history note.

### Tests
- Added `src/hooks/__tests__/useGraphArrangement.test.tsx` with 6 invariants: no pan, viewport pan invariance, zoom invariance, combined pan+zoom, selection-mode anchor preservation, and the empty-positions guard.

### CI / tooling
- No workflow changes; `.github/workflows/release.yml` continues to drive the signed Windows NSIS build on tag push.

## [0.5.1] - 2026-04-23

### Added
- Peer edge feature: visual same-depth connections between sibling nodes, classified as `peer` type and excluded from depth computation.
- Peer candidate badge: UI hint on non-peer edges that look like they should be peers, based on a 4-condition heuristic (depth reduction, depth alignment, multi-parent target, attached source).
- Conversion popover (`🔄` / `↔`) with LR/RL cycle pre-check so each direction can be independently blocked on cycle risk.
- Store actions: `convertEdgeToPeer`, `convertEdgeToNormal`, `dismissPeerCandidate`, with peer-migration metadata persisted in `.eqflow` files.
- Auto-layout trigger after peer conversion so the graph re-aligns around the new same-depth relationship.

### Changed
- Peer candidate heuristic refined from 3 to 4 conditions: relaxed condition 3 (source needs another outgoing **OR** ≥1 incoming) admits chain-middle nodes as peer sources; added condition 2a (target needs ≥2 non-peer incoming) to reject orphan-collapse false positives.
- Dropped the "target.outgoing ≥ 1" requirement once condition 2a took over its orphan-rejection role — lets real-world leaf sibling patterns like van Genuchten `m → n` surface their candidate badges (9/9 flagged on the khu save file).

### CI / tooling
- No workflow changes; `.github/workflows/release.yml` from v0.5.0 continues to drive the signed Windows NSIS build and draft release on tag push.

## [0.5.0] - 2026-04-20

### Added
- Tauri v2 desktop bundle (Windows x64 NSIS installer).
- Auto-updater integration via `tauri-plugin-updater` with minisign signature verification.
- `UpdateDialog` modal with download progress, cancel, skip-version, and retry controls.
- `useAutoUpdater` hook: 4-hour startup throttle, 15-second check timeout, skip-version persistence.
- Menubar download button for manual update checks (bypasses throttle and skip).
- KO/EN i18n strings for updater UI.
- File associations for `.eqflow` project files.
- Documentation: `docs/AUTO_UPDATE.md` covering deployment, rollback, and security.

### Changed
- Major `App.tsx` refactor (53% reduction) — extracted shortcut hooks, graph visibility, smart layout.
- Refined highlight controls and node library UI.

### Removed
- Native OS menubar experiment (reverted to HTML menubar + JS shortcuts for v0.5).

### CI / tooling
- Bumped `rust-toolchain.toml` to `1.88.0` (dependency manifests require `edition2024`, stabilized in Rust 1.85).
- Validated the release pipeline via a `v0.5.0-rc1` dry-run on `looop0218/eq-flow` before publishing this version.
