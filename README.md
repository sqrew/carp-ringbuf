# carp-ringbuf

A generic fixed-capacity circular buffer for the [Carp language](https://github.com/carp-lang/Carp).

## Features

- **Generic Support:** Store any Carp type.
- **Fixed Capacity:** Pre-allocate memory for performance and predictability.
- **Multiple Push Modes:**
    - `push!`: Automatically overwrites the oldest element when full (standard ring buffer behavior).
    - `push-strict!`: Asserts that the buffer is not full.
    - `try-push!`: Returns `true` if successful, `false` if full (no overwrite).
- **Deque-like Operations:** `pop!` (front) and `pop-back!`.
- **Random Access:** `get` for relative indexing (0 is oldest).
- **Order Preserving:** Access elements in FIFO order.
- **Conversion:** Convert the buffer to a standard Carp Array with `to-array`.
- **Iteration:** Efficiently traverse elements with `foreach`.

## Installation

Add this to your project by loading `ringbuf.carp`.

```clojure
(load "path/to/carp-ringbuf/ringbuf.carp")
(use RingBuf)
```


## Examples

See [examples.md](examples.md) for usage examples.
## Running Tests

```bash
carp -x test/ringbuf_test.carp
```

## License

MIT
