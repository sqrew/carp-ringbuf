# Examples

## Basic Usage

```clojure
(use RingBuf)

(defn main []
  (let [rb (RingBuf.new 5 0)]
    (do
      (for [i 0 10]
        (RingBuf.push! &rb i))
      (println* "Buffer content: " (str &(RingBuf.to-array &rb)))
      (println* "Current length: " (RingBuf.length &rb)))))
```

## Using with Custom Types

```clojure
(deftype Point [x Int, y Int])

(use RingBuf)

(defn main []
  (let [rb (RingBuf.new 2 (Point.init 0 0))]
    (do
      (RingBuf.push! &rb (Point.init 10 20))
      (RingBuf.push! &rb (Point.init 30 40))
      (match (RingBuf.pop! &rb)
        (Maybe.Just p) (println* "Popped: " (str &p))
        (Maybe.Nothing) (println* "Empty!")))))
```

## Peeking and Clearing

```clojure
(let [rb (RingBuf.new 3 "empty")]
  (do
    (RingBuf.push! &rb "hello")
    (println* "Peek: " (str &(RingBuf.peek &rb)))
    (RingBuf.clear! &rb)
    (println* "Is empty? " (RingBuf.empty? &rb))))
```
