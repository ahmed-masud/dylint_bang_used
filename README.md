# A lint rule for avoid if !bool and suggest if not_bool

When doing kernel development or filesystem development, or any security work for that matter.  Conditional statements that check for permissions are
a sore source of problems and errors.

I typically find that doing something `if !foo` can be easily missed at a glance compared to `if not_foo` or `if false == is_foo` or `if is_not_foo`
I want a lint that suggests that any statement like `!foo` be replaced by `not_foo` or `foo == false` anyhow that's just me. We'll see if it causes issues or creates more robust code.

# Template created from Dylint library

[Dylint](https://github.com/trailofbits/dylint) is a tool for running Rust lints from dynamic libraries. This repository is a "blank slate" Dylint library.

After forking this repository, run the following command, where `NEW_LINT_NAME` is your new lint's name:
```sh
./start_new_lint.sh NEW_LINT_NAME
```

Alternatively, you can try the experimental `start_from_clippy_lint.sh` script described below.

**Experimental**

Choose a [Clippy lint](https://rust-lang.github.io/rust-clippy/master/) and run the following two commands:

```sh
./start_from_clippy_lint.sh CLIPPY_LINT_NAME NEW_LINT_NAME
cargo build
```

If the first command fails: sorry. Perhaps try another Clippy lint.

If the first command succeeds, but the second fails: you are probably halfway to having a functional Dylint library.

If both commands succeed: hooray! You might then try the following:

```sh
DYLINT_LIBRARY_PATH=$PWD/target/debug cargo dylint NEW_LINT_NAME -- --manifest-path=PATH_TO_OTHER_PACKAGES_MANIFEST
```
