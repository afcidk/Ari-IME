# Ari IME 2.6.3

This is a bug-fix release for mixed Bopomofo and English input. It adds
conservative typo correction for common repeated-key and invalid-prefix input
without changing ordinary English, URL, or version-number text.

## Fixes

- Repeated Bopomofo keys are filtered when removing one occurrence makes the
  remaining sequence a valid, Han-producing syllable. For example, `HHK$G$`
  produces `測試`.
- A single invalid leading key is removed when the following keys independently
  form a valid, Han-producing syllable. For example, `GHK$G$` produces `測試`.
  The correction is deferred until conversion succeeds, so an ordinary literal
  such as `price$` remains unchanged.
- Shifted number-row symbols such as `$` are recognized as tone keys when a
  frontend reports the resulting punctuation keysym instead of the physical
  number key. The mapping remains layout-aware and only applies in an active
  composition context.
- Raw-key recovery preserves the original input case, so a converted `I` is
  restored as `I` rather than the layout-normalized `i`.
- Backspace now restores a converted out-of-order syllable using the original
  key sequence (`140` → 辦 → `140`), rather than libchewing's canonical order
  (`104`).
- Phrase candidate lookup starts at the focused character and only considers
  following text. It no longer adds candidates formed by combining with text
  before the focused character.
- Modifier-only key events no longer close candidate or caret editing. This
  keeps `Shift+Delete` available for forgetting a highlighted personal
  candidate when Wayland delivers the standalone Shift event first.

## Packaging

CMake, Arch (`PKGBUILD`, `.SRCINFO`), Debian changelog, and the
`@ari-ime/wasm` package metadata are synchronized at `2.6.3`.

The checked-in WebAssembly runtime artifacts still need to be regenerated with
the project's Emscripten toolchain before publishing the npm package. The
headless WASM source target was compiled successfully with the local
compatibility shim during this release preparation.

## Validation

- Full CTest suite: 5/5 tests passed
- Release build, install, package metadata, and shell syntax checks passed
- Native build of the WASM headless source target passed
