# Minimal FreeBSD bindgen Issue

This is a test repo to demonstrate a bug in either cross-rs or bindgen.

We should be able to cross compile rust code to freebsd using cross, but currently there is a bug when
using bindgen on c code that relies on `time.h`.

# To reproduce



``` sh
cargo install cross
# should compile without any issues
cross build
cross build --target x86_64-unknown-freebsd
```

The build for target `x86_64-unknown-freebsd` fails with the following error.

```
error: failed to run custom build command for `bindgen-test v0.1.0 (/project)`

Caused by:
  process didn't exit successfully: `/target/debug/build/bindgen-test-edf9d34ad68016d2/build-script-build` (exit status: 101)
  --- stderr
  wrapper.h:1:10: fatal error: 'time.h' file not found
  thread 'main' panicked at 'Unable to generate bindings: ClangDiagnostic("wrapper.h:1:10: fatal error: 'time.h' file not found\n")', build.rs:11:10
  note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```
