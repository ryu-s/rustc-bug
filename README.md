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
# Output
```
>set RUST_BACKTRACE=1
>cargo test
   Compiling bindings v0.0.0 (D:\workspace\rustc-bug\bug-reproducer\bindings)
thread 'rustc' panicked at 'compiler\rustc_codegen_ssa\src\back\link.rs:2029:17: raw_dylib feature not yet implemented', compiler\rustc_middle\src\util\bug.rs:35:26
stack backtrace:
note: Some details are omitted, run with `RUST_BACKTRACE=full` for a verbose backtrace.

error: internal compiler error: unexpected panic

note: the compiler unexpectedly panicked. this is a bug.

note: we would appreciate a bug report: https://github.com/rust-lang/rust/issues/new?labels=C-bug%2C+I-ICE%2C+T-compiler&template=ice.md

note: rustc 1.56.0-nightly (4e282795d 2021-07-31) running on x86_64-pc-windows-msvc

note: compiler flags: -C embed-bitcode=no -C debuginfo=2 -C incremental

note: some of the compiler flags provided by cargo are hidden

query stack during panic:
end of query stack
error: could not compile `bindings`
```

```
>set RUST_BACKTRACE=full
>cargo test
   Compiling bindings v0.0.0 (D:\workspace\rustc-bug\bug-reproducer\bindings)
thread 'rustc' panicked at 'compiler\rustc_codegen_ssa\src\back\link.rs:2029:17: raw_dylib feature not yet implemented', compiler\rustc_middle\src\util\bug.rs:35:26
stack backtrace:
   0:     0x7ffdbea6728f - <std::sys_common::backtrace::_print::DisplayBacktrace as core::fmt::Display>::fmt::hf9e32b6dfefb4bf0
   1:     0x7ffdbea903fa - core::fmt::write::h7e004fee938dc3bd
   2:     0x7ffdbea5aba8 - <std::io::IoSliceMut as core::fmt::Debug>::fmt::h926a9055db352f4c
   3:     0x7ffdbea6aec6 - std::panicking::take_hook::haac17a6660a92eb0
   4:     0x7ffdbea6a9a9 - std::panicking::take_hook::haac17a6660a92eb0
   5:     0x7ffdb24d418e - <sha2::sha512::Sha512Trunc224 as std::io::Write>::flush::h10b1a1277f16abaa
   6:     0x7ffdbea6b7c0 - std::panicking::rust_panic_with_hook::h20443e7eacb1d822
   7:     0x7ffdb667ada8 - rustc_middle::ty::sty::_DERIVE_rustc_middle_ty_Lift_lifted_FOR_TypeAndMut::<impl rustc_middle::ty::context::Lift for rustc_middle::ty::sty::TypeAndMut>::lift_to_tcx::hd923dec70538de76        
   8:     0x7ffdb667ad2f - rustc_middle::ty::sty::_DERIVE_rustc_middle_ty_Lift_lifted_FOR_TypeAndMut::<impl rustc_middle::ty::context::Lift for rustc_middle::ty::sty::TypeAndMut>::lift_to_tcx::hd923dec70538de76        
   9:     0x7ffdb6a45de6 - rustc_query_impl::on_disk_cache::OnDiskCache::store_side_effects_for_anon_node::h4268c57c38e03d3f
  10:     0x7ffdb667ad66 - rustc_middle::ty::sty::_DERIVE_rustc_middle_ty_Lift_lifted_FOR_TypeAndMut::<impl rustc_middle::ty::context::Lift for rustc_middle::ty::sty::TypeAndMut>::lift_to_tcx::hd923dec70538de76        
  11:     0x7ffdb6685ddc - rustc_middle::ty::walk::<impl rustc_middle::ty::subst::GenericArg>::walk_shallow::h0b9fc192ea9e590a
  12:     0x7ffdb66856c1 - rustc_middle::ty::walk::<impl rustc_middle::ty::subst::GenericArg>::walk_shallow::h0b9fc192ea9e590a
  13:     0x7ffdb6685640 - rustc_middle::ty::walk::<impl rustc_middle::ty::subst::GenericArg>::walk_shallow::h0b9fc192ea9e590a
  14:     0x7ffdb6685d39 - rustc_middle::ty::walk::<impl rustc_middle::ty::subst::GenericArg>::walk_shallow::h0b9fc192ea9e590a
  15:     0x7ffdb6a4c9c7 - rustc_middle::util::bug::bug_fmt::h0eab77266e8cdca1
  16:     0x7ffdb5bb280d - rustc_codegen_ssa::back::link::add_local_native_libraries::hb597c2da8c53a98d
  17:     0x7ffdb279a647 - <rustc_codegen_llvm::llvm_::ffi::PassKind as core::fmt::Debug>::fmt::h500865f587760ee8
  18:     0x7ffdb2799bf9 - <rustc_codegen_llvm::llvm_::ffi::PassKind as core::fmt::Debug>::fmt::h500865f587760ee8
  19:     0x7ffdb2792a85 - <rustc_codegen_llvm::LlvmCodegenBackend as rustc_codegen_ssa::traits::backend::CodegenBackend>::link::h06f2032f386eebc4
  20:     0x7ffdb26116b4 - rustc_interface::queries::Linker::link::h4300de0cadfa0663
  21:     0x7ffdb24ed435 - rustc_driver::pretty::print_after_hir_lowering::h719f1de8cc07cdad
  22:     0x7ffdb252c019 - <rustc_middle::ty::SymbolName as core::fmt::Display>::fmt::h0d3ec2b4cea43d42
  23:     0x7ffdb24fa74a - rustc_driver::pretty::print_after_hir_lowering::h719f1de8cc07cdad
  24:     0x7ffdb24ef898 - rustc_driver::pretty::print_after_hir_lowering::h719f1de8cc07cdad
  25:     0x7ffdb24e7c7d - <rustc_driver::Compilation as core::fmt::Debug>::fmt::h5ecec55c67b97d95
  26:     0x7ffdbea7930c - std::sys::windows::thread::Thread::new::hd6348cb9d27ecf91
  27:     0x7ffe63337034 - BaseThreadInitThunk
  28:     0x7ffe634a2651 - RtlUserThreadStart

error: internal compiler error: unexpected panic

note: the compiler unexpectedly panicked. this is a bug.

note: we would appreciate a bug report: https://github.com/rust-lang/rust/issues/new?labels=C-bug%2C+I-ICE%2C+T-compiler&template=ice.md

note: rustc 1.56.0-nightly (4e282795d 2021-07-31) running on x86_64-pc-windows-msvc

note: compiler flags: -C embed-bitcode=no -C debuginfo=2 -C incremental

note: some of the compiler flags provided by cargo are hidden

query stack during panic:
end of query stack
error: could not compile `bindings`
```
