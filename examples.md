# Examples

## Basic Usage and Overwriting

```clojure
(use RingBuf)

(defn main []
  (let [rb (RingBuf.new 5 0)]
    (do
      ; push! will silently discard oldest elements
      (for [i 0 10]
        (RingBuf.push! &rb i))
      (println* "Buffer content (last 5): " (str &(RingBuf.to-array &rb)))
      (println* "Current length: " (RingBuf.length &rb)))))
```

## Safe Pushing

```clojure
(let [rb (RingBuf.new 2 0)]
  (do
    (if (RingBuf.try-push! &rb 1)
        (println* "Pushed 1")
        (println* "Buffer full!"))
    (if (RingBuf.try-push! &rb 2)
        (println* "Pushed 2")
        (println* "Buffer full!"))
    (if (RingBuf.try-push! &rb 3)
        (println* "Pushed 3")
        (println* "Buffer full!")))) ; prints "Buffer full!"
```

## Relative Indexing (get)

```clojure
(let [rb (RingBuf.new 10 0)]
  (do
    (RingBuf.push! &rb 100)
    (RingBuf.push! &rb 200)
    (println* "Oldest: " (str &(RingBuf.get &rb 0))) ; Just 100
    (println* "Newest: " (str &(RingBuf.get &rb 1))))) ; Just 200
```

## Deque-like behavior

```clojure
(let [rb (RingBuf.new 5 0)]
  (do
    (RingBuf.push! &rb 1)
    (RingBuf.push! &rb 2)
    (println* (str &(RingBuf.pop-back! &rb))) ; Just 2
    (println* (str &(RingBuf.pop! &rb))))) ; Just 1
```

## Efficient Traversal

```clojure
(let [rb (RingBuf.new 3 0)]
  (do
    (RingBuf.push! &rb 10)
    (RingBuf.push! &rb 20)
    (RingBuf.foreach &rb &(fn [x] (println* "Element: " (str x))))))
```
