# dustlib_k – K‑Regime Library for Dust

**dustlib_k** is the K‑regime standard library for the Dust Programming
Language (DPL).  It builds upon the core library `dustlib` to provide
primitives for deterministic systems programming.  Where `dustlib`
defines general‑purpose abstractions, `dustlib_k` exposes memory
management, concurrency, synchronisation and I/O operations that are
specific to the classical K‑regime【709885362819930†L42-L64】.  The
APIs in this library wrap the low‑level effects defined in the DPL
specification and enforce safety and determinism through clear
interfaces.

## Directory Structure

```
dustlib_k/
├── README.md          # this file
├── LICENSE            # Dust Open Source License
├── Dust.toml          # manifest describing the library and its sectors
├── spec/              # specification documents for dustlib_k
│   └── 01-overview.md # overview of the K‑regime library
└── sector/
    └── dustlib_k/
        ├── lib.ds         # top‑level forge aggregating submodules
        ├── memory.ds      # memory management primitives
        ├── threading.ds   # thread creation and joining
        ├── sync.ds        # mutexes and synchronisation
        ├── io.ds          # file and device I/O
        └── unsafe.ds      # unsafe operations and hardware access
```

Each `.ds` file defines a `forge` containing shapes and processes.
These modules mirror the effects introduced in the v0.2 specification
draft.  Most process bodies are left as `TODO` stubs because the
underlying runtime support and compiler integration are still in
development.  However, the signatures and documentation provide
guidance on how the library will operate.

## Using dustlib_k

Programs written in the K‑regime can import `dustlib_k` to access
systems programming features.  For example, to allocate memory and
spawn a thread:

```dust
use dustlib_k::memory;
use dustlib_k::threading;

process main() -> Int = {
    let mem = memory.alloc(1024);
    let th = threading.spawn(|| {
        // do work
        return 42;
    }, 0);
    let result = threading.join(th);
    memory.free(mem);
    return result;
};
```

This example illustrates the intended API.  In v0.2 the actual
implementations may differ slightly, but the general pattern of
explicit allocation, spawning and synchronisation will remain.

## Specification

The `spec/` directory contains a draft normative specification for
dustlib_k.  It describes the semantics of each module and how they
interact with the K‑regime effects.  These documents will evolve as
implementation proceeds.

---

Copyright © 2026 Dust LLC