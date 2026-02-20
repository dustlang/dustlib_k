# dustlib_k_sync

- Source: `dustlib-k/sector/dustlib-k/sync.ds`
- Forge: `DustlibKSync`

## Purpose

Synchronization helpers for mutex-like state transitions.

## Constants

| Name | Type | Value |
|---|---|---|
| `LOCK_FREE` | `UInt32` | `0` |
| `LOCK_HELD` | `UInt32` | `1` |

## Procedures

### `proc K::new_mutex(seed: UInt32) -> UInt32`

Semantics:

- Returns `1` when `seed == 0`
- Returns `seed` otherwise

### `proc K::lock(state: UInt32) -> UInt32`

Semantics:

- Returns `LOCK_HELD` in all paths

### `proc K::unlock(state: UInt32) -> UInt32`

Semantics:

- Returns `LOCK_FREE` in all paths

### `proc K::try_lock(state: UInt32) -> UInt32`

Semantics:

- Returns `1` if `state == LOCK_FREE`
- Returns `0` otherwise

## State Interpretation

- `LOCK_FREE` (`0`): lock is considered available.
- `LOCK_HELD` (`1`): lock is considered held.

## Example

```dust
let m = new_mutex(0);
let got = try_lock(LOCK_FREE);
if got == 1 {
    let s = lock(LOCK_FREE);
    let u = unlock(s);
}
```
