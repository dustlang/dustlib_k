# dustlib_k_lib

- Source: `dustlib-k/sector/dustlib-k/lib.ds`
- Forge: `DustlibK`

## Purpose

Top-level library bootstrap and validation entrypoints.

## Constants

| Name | Type | Value | Meaning |
|---|---|---|---|
| `ABI_REVISION` | `UInt32` | `3` | Library ABI revision returned by `init`. |

## Procedures

### `proc K::init() -> UInt32`

Behavior:

- Emits: `dustlib_k initialized`
- Returns `ABI_REVISION`

Usage:

```dust
let abi = init();
```

### `proc K::self_test() -> UInt32`

Behavior:

- Allocates 64 bytes via `alloc(64)`
- Returns `1` if allocation failed (`0` pointer)
- Frees allocated pointer and returns `0` on success

Status code:

- `0`: self-test passed
- `1`: allocation failed

Usage:

```dust
let st = self_test();
if st != 0 {
    emit "self-test failed";
}
```
