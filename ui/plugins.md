# CallbackHandle

```dart
class CallbackHandle {}
```

A wrapper for a raw callback handle.

This is the return type for [PluginUtilities.getCallbackHandle].

### CallbackHandle.fromRawHandle()

```dart
CallbackHandle.fromRawHandle(int _handle)
```

Create an instance using a raw callback handle.

Only values produced by a call to [CallbackHandle.toRawHandle] should be used, otherwise this object will be an invalid handle.

### toRawHandle()

```dart
int toRawHandle()
```

Get the raw callback handle to pass over a [MethodChannel] or [SendPort] (to pass to another [Isolate]).

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# PluginUtilities

```dart
abstract final class PluginUtilities {}
```

Functionality for Flutter plugin authors.

See also:

- [IsolateNameServer], which provides utilities for dealing with [Isolate]s.

### getCallbackHandle()

```dart
CallbackHandle? getCallbackHandle(Function callback)
```

Get a handle to a named top-level or static callback function which can be easily passed between isolates.

The `callback` argument must not be null.

Returns a [CallbackHandle] that can be provided to [PluginUtilities.getCallbackFromHandle] to retrieve a tear-off of the original callback. If `callback` is not a top-level or static function, null is returned.

### getCallbackFromHandle()

```dart
Function? getCallbackFromHandle(CallbackHandle handle)
```

Get a tear-off of a named top-level or static callback represented by a handle.

The `handle` argument must not be null.

If `handle` is not a valid handle returned by [PluginUtilities.getCallbackHandle], null is returned. Otherwise, a tear-off of the callback associated with `handle` is returned.
