# Ari IME 2.6.4

This release improves candidate editing, configuration usability, and
cross-distribution build tooling.

## Fixes and options

- Candidate picks keep the caret after the rewritten text. Set
  `CaretAfterPick=EndOfText` to resume appending at the end instead.
- `CandidateArrowKeys` selects whether Left and Right move between characters
  or cycle candidate pages while a candidate window is open.
- `LiteralKeyReinterpret=BopomofoSymbol` makes Up turn one literal Bopomofo key
  into its symbol, such as `1` into ㄅ.
- Configuration labels fit KDE System Settings; the detailed explanations are
  available as tooltips and in the README.

## Tooling

`scripts/build-from-source.sh` builds and tests Ari on Debian, Ubuntu, Arch,
and Fedora. Its package installation path restarts Fcitx5 and fails if the
replacement daemon cannot be confirmed.

## Credit

The candidate-editing, configuration, and cross-distribution tooling work in
this release was contributed by @leafpmpmp (Morikon).

## Packaging

CMake, Arch, Debian, and `@ari-ime/wasm` metadata are synchronized at 2.6.4.
