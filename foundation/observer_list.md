# ObserverList

```dart
class ObserverList<T> extends Iterable<T> {}
```

A list optimized for the observer pattern when there are small numbers of observers.

Consider using an [ObserverList] instead of a [List] when the number of [contains] calls dominates the number of [add] and [remove] calls.

This class will include in the [iterator] each added item in the order it was added, as many times as it was added.

If there will be a large number of observers, consider using [HashedObserverList] instead. It has slightly different iteration semantics, but serves a similar purpose, while being more efficient for large numbers of observers.

See also:

- [HashedObserverList] for a list that is optimized for larger numbers of observers.

### add()

```dart
void add(T item)
```

Adds an item to the end of this list.

This operation has constant time complexity.

### remove()

```dart
bool remove(T item)
```

Removes an item from the list.

This is O(N) in the number of items in the list.

Returns whether the item was present in the list.

### clear()

```dart
void clear()
```

Removes all items from the [ObserverList].

### contains()

```dart
bool contains(Object? element)
```

### iterator

```dart
Iterator<T> get iterator
```

### isEmpty

```dart
bool get isEmpty
```

### isNotEmpty

```dart
bool get isNotEmpty
```

### toList()

```dart
List<T> toList({bool growable = true})
```

Creates a List containing the elements of the [ObserverList].

Overrides the default implementation of the [Iterable] to reduce number of allocations.

# HashedObserverList

```dart
class HashedObserverList<T> extends Iterable<T> {}
```

A list optimized for the observer pattern, but for larger numbers of observers.

For small numbers of observers (e.g. less than 10), use [ObserverList] instead.

The iteration semantics of the this class are slightly different from [ObserverList]. This class will only return an item once in the [iterator], no matter how many times it was added, although it does require that an item be removed as many times as it was added for it to stop appearing in the [iterator]. It will return them in the order the first instance of an item was originally added.

See also:

- [ObserverList] for a list that is fast for small numbers of observers.

### add()

```dart
void add(T item)
```

Adds an item to the end of this list.

This has constant time complexity.

### remove()

```dart
bool remove(T item)
```

Removes an item from the list.

This operation has constant time complexity.

Returns whether the item was present in the list.

### clear()

```dart
void clear()
```

Removes all items from the [HashedObserverList].

### contains()

```dart
bool contains(Object? element)
```

### iterator

```dart
Iterator<T> get iterator
```

### isEmpty

```dart
bool get isEmpty
```

### isNotEmpty

```dart
bool get isNotEmpty
```

### toList()

```dart
List<T> toList({bool growable = true})
```

Creates a List containing the elements of the [HashedObserverList].

Overrides the default implementation of [Iterable] to reduce number of allocations.
