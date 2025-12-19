Khutulun Development Environment
================================

Setup a local development environment for [Khutulun](https://khutulun.org), [Floria](https://floria.khutulun.org),  [Puccini](https://puccini.cloud), and related libraries.

Based on [git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) with added local development configurations.

Installation
------------

```sh
git clone https://github.com/tliron/khutulun-dev.git
cd khutulun-dev
./initialize
```

Build Prerequisites
-------------------

We assume Linux for the build environment. Note that you can crosscompile from Linux to all of Rust's supported architectures and targets.

You need the [Rust](https://rust-lang.org) compiler and standard library as well as its [Cargo](https://doc.rust-lang.org/cargo/) build system. You can get everything at once via [rustup](https://rustup.rs).

We'll also need the [WASI](https://wasi.dev) (preview 2) target libraries for Rust in order to build our Wasm plugins.

Finally, we need either [gcc](https://gcc.gnu.org) or [Clang](https://clang.llvm.org). We recommend also installing the [Wild linker](https://github.com/davidlattimore/wild), which Puccini can detect and use for faster building of debug builds.

To install everything:

```sh
# Rust:
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Configure PATH (you might want to add this to your ~/.bashrc):
. ~/.cargo/env

# Add WASI target:
rustup target add wasm32-wasip2
rustup +nightly target add wasm32-wasip2

# Compiler requirements:
#  Fedora world:
#    sudo dnf install gcc clang openssl-devel
#  Debian world:
#    sudo apt install build-essential clang libssl-dev
#  Arch world:
#    sudo pacman -S base-devel clang openssl

# Wild linker:
cargo install --locked wild-linker
```

Usage
-----

You can then work with individual repositories, e.g.:

```sh
cd puccini
scripts/build
```

To update all the repositories to their latest upstream versions:

```sh
./update
```
