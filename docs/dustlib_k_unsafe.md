# dustlib_k_unsafe

- Source: `dustlib-k/sector/dustlib-k/unsafe.ds`
- Forge: `DustlibKUnsafe`

## Purpose

Unsafe operation wrappers with explicit capability gating.

## Constants

| Name | Type | Value |
|---|---|---|
| `UNSAFE_ALLOWED` | `UInt32` | `1` |
| `UNSAFE_DENIED` | `UInt32` | `0` |

## Procedures

### `proc K::block(reason: UInt64, capability: UInt32) -> UInt32`

Semantics:

- If `capability == UNSAFE_ALLOWED`:
  - Emits `unsafe block entered`
  - Calls `puts(reason)` then `putchar(10)`
  - Returns `0`
- Otherwise:
  - Emits `unsafe block denied`
  - Returns `1`

### `proc K::read_volatile(addr: UInt64) -> UInt32`

Semantics:

- Returns `0` when `addr == 0`
- Returns `1` otherwise

### `proc K::write_volatile(addr: UInt64, value: UInt32) -> UInt32`

Semantics:

- Returns `1` when `addr == 0`
- Returns `0` otherwise

Note:

- `value` is currently accepted but not otherwise used in return calculation.

## Example

```dust
let guard = block(message_ptr, UNSAFE_ALLOWED);
if guard == 0 {
    let r = read_volatile(mmio_addr);
    let w = write_volatile(mmio_addr, 1);
}
```
