# Changelog

## 2026-11-23

### Fixed
- `rename_files`: `1942.nes` became `nes`, and `mv` silently overwrote files that ended up with the same name. Both are now skipped.
- `rename_files` now also strips `01 Title` and `01 - Title`, as the README promised, not only `01. Title`.
