# Akka Arrh port changes

These entries describe this port. Historical notes for the inherited runtime
remain in `docs/legacy/CHANGELOG.md`. No game files are included in releases.

## v0.2

- Fix jumping text and stretched geometry on Retroid by disabling speculative draw preparation; Linux uses the same default.
- Keep serial draw recording enabled by default to prevent overlapping title text.
- Preserve L3 + R3 access to Settings and its bundled/system/import-ZIP graphics-driver selector.
- Verify the installed Android update preserves saves, and record Linux and Retroid rendering checks in the port status report.
- Restore this repository's changelog so its release-note checks work in a fresh Git checkout.

## v0.1

- Add Linux x86-64 and Android ARM64 support for the verified Akka Arrh CUSA36609 v1.00 executable.
- Resolve the shipped Assets/assets path mismatch without modifying the game dump.
- Add separate app/save identities, bundled Turnip, driver ZIP import, build instructions and source-build CI.
