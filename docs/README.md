# dustlib-k Documentation

This directory contains complete markdown documentation for the `dustlib-k` library.

## Scope

- Project manifest and layout
- Top-level forge API
- Module-level APIs for memory, threading, sync, I/O, and unsafe operations
- Integration notes for using `dustlib-k` from K-domain Dust projects

## Library Structure

| Source File | Forge | Documentation |
|---|---|---|
| `sector/dustlib-k/lib.ds` | `DustlibK` | `dustlib_k_lib.md` |
| `sector/dustlib-k/memory.ds` | `DustlibKMemory` | `dustlib_k_memory.md` |
| `sector/dustlib-k/threading.ds` | `DustlibKThreading` | `dustlib_k_threading.md` |
| `sector/dustlib-k/sync.ds` | `DustlibKSync` | `dustlib_k_sync.md` |
| `sector/dustlib-k/io.ds` | `DustlibKIo` | `dustlib_k_io.md` |
| `sector/dustlib-k/unsafe.ds` | `DustlibKUnsafe` | `dustlib_k_unsafe.md` |

## Documents

- `dustlib_k_overview.md`: architecture, design intent, and integration model.
- `dustlib_k_lib.md`: top-level library bootstrap and self-test behavior.
- `dustlib_k_memory.md`: deterministic memory facade API and current semantics.
- `dustlib_k_threading.md`: thread creation/join/sleep facade and ID derivation.
- `dustlib_k_sync.md`: mutex-state helper API.
- `dustlib_k_io.md`: file, port, and MMIO-facing APIs.
- `dustlib_k_unsafe.md`: unsafe gate and volatile access helper semantics.

## Compatibility Note

Repository path is `dustlib-k`, while API naming in code remains `dustlib_k` for compatibility with existing imports and manifests.
