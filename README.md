# How to reproduce the bug
```
>rustc --version --verbose
rustc 1.56.0-nightly (4e282795d 2021-07-31)
binary: rustc
commit-hash: 4e282795d7d1d28a4c6c1c6521045ae2b59f3519
commit-date: 2021-07-31
host: x86_64-pc-windows-msvc
release: 1.56.0-nightly
LLVM version: 12.0.1
```


```
git clone https://github.com/ryu-s/rustc-bug.git
cd rustc-bug
cargo test
```
