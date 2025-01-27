# v0.1.1

- Fixed UB in `FixedVec::fill`. This would drop uninitialized instances while
  filling the vector, potentially leading to arbitrary code execution.
  Thanks @danielhenrymantilla for the report.

## v0.1.0

- Added `Uninit::from_maybe_uninit_slice`, slice variant of `from_maybe_uninit`.
- Added `Uninit::into_maybe_uninit` as the inverse of the constructor.
- Added `FixedVec::drain` and `Drain`: work just like the standard ones.
- Renamed `FixedVec::from_available` to `FixedVec::from_unaligned`
- Added `FixedVec::split_borrowed` to split without affecting capacity.

## v0.0.7

- Introduces `Rc`, a reference counter owned value.
- Improves `FixedVec` by adding many standard trait impls.
- Added `Slab` methods: `rc` and `fixed_vec` to create respective containers.
- Added `FixedVec` methods: `truncate` and `clear`.
- Added `Uninit::fits` to test if a `cast` would succeed without performing it.

## v0.0.6

- Introduces `Box`, an owned value within an `Uninit` allocation
- Fixed `Uninit` to never rely on references internally. Unfortunately, this
  means that unsized `Uninit` currently do no track the size of their pointer.
  That will return sooner or later when the resolution of Rust #36925 provides
  `ptr::slice_from_raw_parts`.

## v0.0.5

- Introduces `Uninit`, a lifetime tracked pointed to uninitialized memory.
- Introduces `FixedVec`, a capacity bound `Vec` equivalent built on the above.

## v0.0.4

- Fixed a bug where ZSTs had their Drop impl executed while leaking them
- Provides a new interface: `level`, `alloc_at` and `leak_at`. It ensures that
  an allocation is the first allocation to happen after a particular point in
  time, and no other allocation is placed between it and the preceding one.

## v0.0.3

- Added `Slab::leak`, a new interface to directly allocate values. Avoid
  requiring `Box` and `Box::leak` from `alloc` and allows usage a `Slab` with
  limited lifetime such as on the stack.

## v0.0.2

- `Slab::take` has been renamed to `Slab::alloc`.
- Added `uninit` and `zeroed` constructors as available for `MaybeUninit`
- Made the `new` constructor safe as no uninitialized bytes are read
- The nightly `try_reserve` feature is now called `nightly_try_reserve`
  Note: It is only used in a test and has no influence on the api
