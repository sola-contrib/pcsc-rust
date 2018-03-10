# 1.0.1 (2018-02-25)

* **BREAKING CHANGE** (`pcsc-sys`) Fix the types of `SCARDCONTEXT` and
  `SCARDHANDLE` on Windows.

  Previously they were (effectively) defined as `i32`, but the correct
  definition is `usize`. Hence on all Windows platforms, the sign is
  different (not really a problem); and on 64 bits, the width is
  different (wouldn't work).

  While this is technically a breaking change, this should be transparent
  and binaries for Windows 64 bits wouldn't have worked anyway, so we
  avoid a major version bump which is a headache for FFI crates.

  Reported and debugged by @ndusart in
  [issue #6](https://github.com/bluetech/pcsc-rust/issues/6).

* (`pcsc`) Depend on `pcsc-sys >= 1.0.1` to discourage using the broken
  `1.0.0`.


# 1.0.0 (2017-12-05)

* **BREAKING CHANGE** Update bitflags to version 1. This makes the flag
  types easier to use, and improves the documentation.

  Since bitflags now uses associated constants, Rust >= 1.20 is required.

  Example for updating: `STATE_UNAWARE` -> `State::UNAWARE`.

* The `pcsc-sys` crate is also promoted to 1.0.0, without changes.


# 0.1.2 (2017-08-16)

* `pcsc-sys`: Added `SCardControl()` bindings.

* Added `Card::control()`, a wrapper over `SCardControl()`.

* `pcsc-sys`: Improved build target detection in the build script.


# 0.1.1 (2017-06-15)

* Fixed errors in the macOS bindings. In particular, wrong integer types
  were used, and some structs had incorrect padding.

  All discovered problems were fixed; the library now works correctly on
  macOS.

  Reported and debugged by @RokLenarcic in
  [issue #4](https://github.com/bluetech/pcsc-rust/issues/4).

* The function `ReaderState::new()` now takes `Into<CString>` instead of
  `&CStr`. Previously the `&CStr` was turned into a `CString` internally;
  the new form is more explicit and can avoid an allocation if a `CString`
  is passed directly.


# 0.1.0 - 2017-02-06

Initial stable release.