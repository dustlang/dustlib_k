# dustlib_k Specification – Overview

## Purpose

`dustlib_k` is the K‑regime library for the Dust Programming
Language.  It supplements the core `dustlib` by exposing APIs that
wrap the K‑regime effects introduced in the v0.2 specification
additions.  These include memory management (`alloc`/`free`),
deterministic threading (`spawn`/`join` with seeds), synchronisation
(`mutex_new`/`mutex_lock`/`mutex_unlock`), file I/O and low‑level
device access【709885362819930†L42-L64】.  By providing these
operations in a structured library, dustlib_k makes it easier to
write systems programs while respecting the deterministic, constraint‑first
philosophy of DPL.

## Sectors and Modules

`dustlib_k` is organised into a single sector named `dustlib_k`.
Within that sector, the following forges are defined:

| Forge       | Description                                                            |
|------------|------------------------------------------------------------------------|
| `memory`    | Wraps `alloc` and `free` effects.  Provides safe constructors and
              destructors for `Mem` handles and convenience operations such as
              zero‑initialised allocation.                                             |
| `threading` | Wraps `spawn` and `join`.  Exposes a `Thread<T>` shape and
              enforces deterministic scheduling via optional seed parameters【548468680421956†L121-L129】. |
| `sync`      | Defines synchronisation primitives.  Wraps `mutex_new`,
              `mutex_lock` and `mutex_unlock` and may be extended with other
              K‑regime synchronisation mechanisms.                                      |
| `io`        | Provides file and device I/O.  Wraps `open`, `read`, `write`,
              `close`, `io_read`, `io_write`, `mmio_read` and `mmio_write` effects,
              handling error reporting and resource lifetime management.               |
| `unsafe`    | Contains declarations related to `unsafe` blocks and hardware
              access.  These operations remain dangerous and must be clearly
              annotated.                                                               |

All forges reside in the `sector/dustlib_k` directory and are written in
`.ds` files.

## Determinism and Safety

The operations provided by dustlib_k are deterministic in the sense
that, given the same inputs and scheduler seed, they produce the same
results and thread interleavings.  Memory and I/O effects declare
their resource and timing bounds, and synchronisation primitives
enforce proper usage patterns【709885362819930†L42-L64】.  Unsafe
operations are confined to the `unsafe` forge and must be justified
explicitly.

## Evolution

This document describes a draft design for dustlib_k.  Implementations
may refine the interfaces as the K‑regime runtime matures.  All
additions will adhere to the DPL minor versioning rules: changes are
additive and do not break existing code【587782563170635†L29-L34】.