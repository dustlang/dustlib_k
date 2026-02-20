# dustlib-k Overview

- Project path: `dustlib-k/`
- Manifest: `dustlib-k/Dust.toml`
- Primary sector path: `dustlib-k/sector/dustlib-k`
- Current package name in manifest: `dustlib_k`

## Purpose

`dustlib-k` provides K-domain oriented systems primitives for Dust programs, including:

- Memory helper operations
- Threading helper operations
- Synchronization helper operations
- File and device I/O helpers
- Unsafe operation gates/wrappers

The current implementation is a deterministic facade designed to provide stable signatures and integration points for runtime and OS layers.

## Forge Inventory

| Forge | Source | Constants | Procedures |
|---|---|---:|---:|
| `DustlibK` | `lib.ds` | 1 | 2 |
| `DustlibKMemory` | `memory.ds` | 3 | 7 |
| `DustlibKThreading` | `threading.ds` | 2 | 7 |
| `DustlibKSync` | `sync.ds` | 2 | 4 |
| `DustlibKIo` | `io.ds` | 2 | 8 |
| `DustlibKUnsafe` | `unsafe.ds` | 2 | 3 |

## Integration Pattern

In dependent workspaces, `dustlib-k` is normally referenced by path while using `dust_runtime` and higher-level runtime libraries.

Example dependency stanza:

```toml
[dependencies]
dustlib_k = { path = "../dustlib-k" }
```

## Import Pattern

The codebase currently uses forge-scoped calls and wrapper naming conventions tied to `dustlib_k` semantics.

```dust
// Conceptual usage
let ptr = mem_alloc(4096);
let tid = thread_spawn(entry, seed);
let ok = file_close(handle);
```

## Status

- API surface is implemented.
- Several procedures are lightweight wrappers or deterministic placeholders, intended to be expanded as runtime internals mature.
- Return codes and semantics are documented in each module doc.
