# dustlib_k_memory

- Source: `dustlib-k/sector/dustlib-k/memory.ds`
- Forge: `DustlibKMemory`

## Purpose

Deterministic memory helper facade for allocation and free operations.

## Constants

| Name | Type | Value |
|---|---|---|
| `HEAP_BASE` | `UInt64` | `16777216` |
| `HEAP_LIMIT` | `UInt64` | `33554432` |
| `ALIGNMENT` | `UInt32` | `16` |

## Procedures

### `proc K::alloc(size: UInt32) -> UInt64`

Semantics:

- `size == 0` returns `0`
- Computes `aligned = align_up(size, ALIGNMENT)`
- If `aligned > HEAP_LIMIT - HEAP_BASE`, returns `0`
- Otherwise returns `HEAP_BASE + aligned`

Note:

- Current implementation returns an address derived from constants and size; it is not a full allocator state machine.

### `proc K::free(ptr: UInt64) -> UInt32`

Semantics:

- Returns `1` if `ptr < HEAP_BASE`
- Returns `1` if `ptr > HEAP_LIMIT`
- Returns `0` otherwise

### `proc K::zero_alloc(size: UInt32) -> UInt64`

Semantics:

- Calls `alloc(size)`
- Returns `0` on alloc failure
- Calls `set(ptr, 0, size)` on success
- Returns allocated pointer

### Wrapper Procedures

| Procedure | Behavior |
|---|---|
| `mem_alloc(size)` | Calls `alloc(size)` |
| `mem_free(ptr)` | Calls `free(ptr)` |
| `mem_zero_alloc(size)` | Calls `zero_alloc(size)` |

### `proc K::align_up(size: UInt32, align: UInt32) -> UInt32`

Semantics:

- If `align == 0`, returns `size`
- If `size == 0`, returns `align`
- Otherwise returns `size + align`

Note:

- The current formula is additive, not bit/step alignment rounding.

## Example

```dust
let ptr = mem_zero_alloc(256);
if ptr == 0 {
    emit "alloc failed";
} else {
    let rc = mem_free(ptr);
    if rc != 0 {
        emit "free failed";
    }
}
```
