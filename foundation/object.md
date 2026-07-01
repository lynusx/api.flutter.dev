# objectRuntimeType()

```dart
String objectRuntimeType(Object? object, String optimizedValue)
```

Framework code should use this method in favor of calling `toString` on [Object.runtimeType].

Calling `toString` on a runtime type is a non-trivial operation that can negatively impact performance. If asserts are enabled, this method will return `object.runtimeType.toString()`; otherwise, it will return the [optimizedValue], which must be a simple constant string.
