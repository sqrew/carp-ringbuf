# carp-ringbuf

A generic fixed-capacity circular buffer for the [Carp language](https://github.com/carp-lang/Carp).

## Features

- **Generic Support:** Store any Carp type.
- **Fixed Capacity:** Pre-allocate memory for performance and predictability.
- **Automatic Overwrite:** Pushing to a full buffer automatically overwrites the oldest element.
- **Order Preserving:** Access elements in FIFO order.
- **Conversion:** Easily convert the buffer to a standard Carp Array.

## Installation

Add this to your project by loading `ringbuf.carp`.

```clojure
(load "path/to/carp-ringbuf/ringbuf.carp")
(use RingBuf)
```

## Usage

```clojure
(use RingBuf)

(defn main []
  (let [rb (RingBuf.new 3 0)] ; capacity of 3, default value 0
    (do
      (RingBuf.push! &rb 1)
      (RingBuf.push! &rb 2)
      (RingBuf.push! &rb 3)
      (RingBuf.push! &rb 4) ; overwrites 1
      (println* (str &(RingBuf.pop! &rb))) ; Just 2
      (println* (str &(RingBuf.to-array &rb)))))) ; [3 4]
```

## Running Tests

```bash
carp -x test/ringbuf_test.carp
```

## License

MIT
