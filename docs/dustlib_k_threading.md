# dustlib_k_threading

- Source: `dustlib-k/sector/dustlib-k/threading.ds`
- Forge: `DustlibKThreading`

## Purpose

Deterministic threading facade for spawn/join/sleep operations.

## Constants

| Name | Type | Value |
|---|---|---|
| `MAX_THREADS` | `UInt32` | `256` |
| `DEFAULT_STACK` | `UInt32` | `8192` |

## Procedures

### `proc K::spawn(entry: UInt32, seed: UInt32) -> UInt32`

Semantics:

- Returns `0` when `entry == 0`
- Otherwise returns `next_thread_id(entry, seed)`

### `proc K::join(thread_id: UInt32) -> UInt32`

Semantics:

- Returns `1` when `thread_id == 0`
- Returns `0` otherwise

### `proc K::sleep(ms: UInt32) -> UInt32`

Semantics:

- Returns `0` for all paths
- Current implementation is a placeholder/no-op status return

### Wrapper Procedures

| Procedure | Behavior |
|---|---|
| `thread_spawn(entry, seed)` | Calls `spawn(entry, seed)` |
| `thread_join(thread_id)` | Calls `join(thread_id)` |
| `thread_sleep(ms)` | Calls `sleep(ms)` |

### `proc K::next_thread_id(entry: UInt32, seed: UInt32) -> UInt32`

Semantics:

- `mixed = entry + seed`
- Returns `1` if `mixed == 0`
- Returns `mixed - MAX_THREADS` if `mixed >= MAX_THREADS`
- Otherwise returns `mixed`

## Example

```dust
let tid = thread_spawn(entry_point, 7);
if tid == 0 {
    emit "spawn failed";
} else {
    let jr = thread_join(tid);
    if jr != 0 {
        emit "join failed";
    }
}
```
