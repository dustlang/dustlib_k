# dustlib_k_io

- Source: `dustlib-k/sector/dustlib-k/io.ds`
- Forge: `DustlibKIo`

## Purpose

I/O facade covering file operations, I/O ports, and MMIO helpers.

## Constants

| Name | Type | Value |
|---|---|---|
| `IO_OK` | `UInt32` | `0` |
| `IO_ERR` | `UInt32` | `1` |

## Procedures

### `proc K::file_open(path: UInt64, mode: UInt32) -> UInt64`

Semantics:

- Returns `0` when `path == 0`
- Otherwise returns `open(path, mode)`

### `proc K::file_read(handle: UInt64, buffer: UInt64, length: UInt32) -> UInt32`

Semantics:

- Returns `IO_ERR` when `handle == 0`
- Otherwise returns `read(handle, buffer, length)`

### `proc K::file_write(handle: UInt64, buffer: UInt64, length: UInt32) -> UInt32`

Semantics:

- Returns `IO_ERR` when `handle == 0`
- Otherwise returns `write(handle, buffer, length)`

### `proc K::file_close(handle: UInt64) -> UInt32`

Semantics:

- Returns `IO_ERR` when `handle == 0`
- Otherwise returns `close(handle)`

### `proc K::io_read(port: UInt16) -> UInt32`

Semantics:

- Returns `inb(port)`

### `proc K::io_write(port: UInt16, value: UInt8) -> UInt32`

Semantics:

- Calls `outb(port, value)`
- Returns `IO_OK`

### `proc K::mmio_read(addr: UInt64) -> UInt64`

Semantics:

- Returns `0` when `addr == 0`
- Otherwise returns `addr` (placeholder behavior)

### `proc K::mmio_write(addr: UInt64, value: UInt32) -> UInt32`

Semantics:

- Returns `IO_ERR` when `addr == 0`
- Returns `IO_OK` otherwise

Note:

- `value` is currently accepted but not otherwise used in return calculation.

## Example

```dust
let h = file_open(path_ptr, 0);
if h != 0 {
    let wr = file_write(h, buf_ptr, len);
    let cr = file_close(h);
}
let status = io_write(0x3F8, 65);
```
