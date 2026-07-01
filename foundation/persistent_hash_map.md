# PersistentHashMap

```dart
class PersistentHashMap<K extends Object, V> {}
```

A collection of key/value pairs which provides efficient retrieval of value by key.

This class implements a persistent map: extending this map with a new key/value pair does not modify an existing instance but instead creates a new instance.

Unlike [Map], this class does not support `null` as a key value and implements only a functionality needed for a specific use case at the core of the framework.

Underlying implementation uses a variation of _hash array mapped trie_ data structure with compressed (bitmap indexed) nodes.

See also:

- [Bagwell, Phil. Ideal hash trees.](https://infoscience.epfl.ch/record/64398);
- [Steindorfer, Michael J., and Jurgen J. Vinju. "Optimizing hash-array mapped tries for fast and lean immutable JVM collections."](https://dl.acm.org/doi/abs/10.1145/2814270.2814312);
- [Clojure's `PersistentHashMap`](https://github.com/clojure/clojure/blob/master/src/jvm/clojure/lang/PersistentHashMap.java).

### PersistentHashMap.empty()

```dart
PersistentHashMap.empty()
```

Creates an empty hash map.

### put()

```dart
PersistentHashMap<K, V> put(K key, V value)
```

If this map does not already contain the given [key] to [value] mapping then create a new version of the map which contains all mappings from the current one plus the given [key] to [value] mapping.

### operator []()

```dart
V? operator [](K key)
```

Returns value associated with the given [key] or `null` if [key] is not in the map.
