# SynchronousFuture

```dart
class SynchronousFuture<T> implements Future<T> {}
```

A [Future] whose [then] implementation calls the callback immediately.

This is similar to [Future.value], except that the value is available in the same event-loop iteration.

⚠ This class is useful in cases where you want to expose a single API, where you normally want to have everything execute synchronously, but where on rare occasions you want the ability to switch to an asynchronous model. **In general use of this class should be avoided as it is very difficult to debug such bimodal behavior.**

A [SynchronousFuture] will never complete with an error.

### SynchronousFuture()

```dart
SynchronousFuture(T _value)
```

Creates a synchronous future.

See also:

- [Future.value] for information about creating a regular [Future] that completes with a value.

### asStream()

```dart
Stream<T> asStream()
```

### catchError()

```dart
Future<T> catchError(Function onError, {bool Function(Object error)? test})
```

### then()

```dart
Future<R> then<R>(FutureOr<R> Function(T value) onValue, {Function? onError})
```

### timeout()

```dart
Future<T> timeout(Duration timeLimit, {FutureOr<T> Function()? onTimeout})
```

### whenComplete()

```dart
Future<T> whenComplete(FutureOr<dynamic> Function() action)
```
