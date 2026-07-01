@docImport 'dart:ui';

# ValueChanged

```dart
typedef ValueChanged<T> = void Function(T value)
```

Signature for callbacks that report that an underlying value has changed.

See also:

- [ValueSetter], for callbacks that report that a value has been set.

# ValueSetter

```dart
typedef ValueSetter<T> = void Function(T value)
```

Signature for callbacks that report that a value has been set.

This is the same signature as [ValueChanged], but is used when the callback is called even if the underlying value has not changed. For example, service extensions use this callback because they call the callback whenever the extension is called with a value, regardless of whether the given value is new or not.

See also:

- [ValueGetter], the getter equivalent of this signature.
- [AsyncValueSetter], an asynchronous version of this signature.

# ValueGetter

```dart
typedef ValueGetter<T> = T Function()
```

Signature for callbacks that are to report a value on demand.

See also:

- [ValueSetter], the setter equivalent of this signature.
- [AsyncValueGetter], an asynchronous version of this signature.

# IterableFilter

```dart
typedef IterableFilter<T> = Iterable<T> Function(Iterable<T> input)
```

Signature for callbacks that filter an iterable.

# AsyncCallback

```dart
typedef AsyncCallback = Future<void> Function()
```

Signature of callbacks that have no arguments and return no data, but that return a [Future] to indicate when their work is complete.

See also:

- [VoidCallback], a synchronous version of this signature.
- [AsyncValueGetter], a signature for asynchronous getters.
- [AsyncValueSetter], a signature for asynchronous setters.

# AsyncValueSetter

```dart
typedef AsyncValueSetter<T> = Future<void> Function(T value)
```

Signature for callbacks that report that a value has been set and return a [Future] that completes when the value has been saved.

See also:

- [ValueSetter], a synchronous version of this signature.
- [AsyncValueGetter], the getter equivalent of this signature.

# AsyncValueGetter

```dart
typedef AsyncValueGetter<T> = Future<T> Function()
```

Signature for callbacks that are to asynchronously report a value on demand.

See also:

- [ValueGetter], a synchronous version of this signature.
- [AsyncValueSetter], the setter equivalent of this signature.

# CachingIterable

```dart
class CachingIterable<E> extends IterableBase<E> {}
```

A lazy caching version of [Iterable].

This iterable is efficient in the following ways:

- It will not walk the given iterator more than you ask for.

- If you use it twice (e.g. you check [isNotEmpty], then use [single]), it will only walk the given iterator once. This caching will even work efficiently if you are running two side-by-side iterators on the same iterable.

- [toList] uses its EfficientLength variant to create its list quickly.

It is inefficient in the following ways:

- The first iteration through has caching overhead.

- It requires more memory than a non-caching iterator.

- The [length] and [toList] properties immediately pre-cache the entire list. Using these fields therefore loses the laziness of the iterable. However, it still gets cached.

The caching behavior is propagated to the iterators that are created by [map], [where], [expand], [take], [takeWhile], [skip], and [skipWhile], and is used by the built-in methods that use an iterator like [isNotEmpty] and [single].

Because a CachingIterable only walks the underlying data once, it cannot be used multiple times with the underlying data changing between each use. You must create a new iterable each time. This also applies to any iterables derived from this one, e.g. as returned by `where`.

### CachingIterable()

```dart
CachingIterable(Iterator<E> _prefillIterator)
```

Creates a [CachingIterable] using the given [Iterator] as the source of data.

The iterator must not throw exceptions.

Since the argument is an [Iterator], not an [Iterable], it is guaranteed that the underlying data set will only be walked once. If you have an [Iterable], you can pass its [iterator] field as the argument to this constructor.

You can this with an existing `sync*` function as follows:

```dart
Iterable<int> range(int start, int end) sync* {
  for (int index = start; index <= end; index += 1) {
    yield index;
  }
}

Iterable<int> i = CachingIterable<int>(range(1, 5).iterator);
print(i.length); // walks the list
print(i.length); // efficient
```

Beware that this will eagerly evaluate the `range` iterable, and because of that it would be better to just implement `range` as something that returns a `List` to begin with if possible.

### iterator

```dart
Iterator<E> get iterator
```

### map()

```dart
Iterable<T> map<T>(T Function(E e) toElement)
```

### where()

```dart
Iterable<E> where(bool Function(E element) test)
```

### expand()

```dart
Iterable<T> expand<T>(Iterable<T> Function(E element) toElements)
```

### take()

```dart
Iterable<E> take(int count)
```

### takeWhile()

```dart
Iterable<E> takeWhile(bool Function(E value) test)
```

### skip()

```dart
Iterable<E> skip(int count)
```

### skipWhile()

```dart
Iterable<E> skipWhile(bool Function(E value) test)
```

### length

```dart
int get length
```

### elementAt()

```dart
E elementAt(int index)
```

### toList()

```dart
List<E> toList({bool growable = true})
```

# Factory

```dart
class Factory<T> {}
```

A factory interface that also reports the type of the created objects.

### Factory()

```dart
Factory(ValueGetter<T> constructor)
```

Creates a new factory.

### constructor

```dart
ValueGetter<T> constructor
```

Creates a new object of type T.

### type

```dart
Type get type
```

The type of the objects created by this factory.

### toString()

```dart
String toString()
```

# lerpDuration()

```dart
Duration lerpDuration(Duration a, Duration b, double t)
```

Linearly interpolate between two `Duration`s.
