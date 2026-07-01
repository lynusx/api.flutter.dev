# kFlutterMemoryAllocationsEnabled

```dart
bool kFlutterMemoryAllocationsEnabled
```

If true, Flutter objects dispatch the memory allocation events.

By default, the constant is true for debug mode and false for profile and release modes. To enable the dispatching for release mode, pass the compilation flag `--dart-define=flutter.memory_allocations=true`.

# ObjectEvent

```dart
abstract class ObjectEvent {}
```

A lifecycle event of an object.

### ObjectEvent()

```dart
ObjectEvent({required Object object})
```

Creates an instance of [ObjectEvent].

### object

```dart
Object object
```

Reference to the object.

The reference should not be stored in any long living place as it will prevent garbage collection.

### toMap()

```dart
Map<Object, Map<String, Object>> toMap()
```

The representation of the event in a form, acceptable by a pure dart library, that cannot depend on Flutter.

The method enables code like:

```dart
void myDartMethod(Map<Object, Map<String, Object>> event) {}
FlutterMemoryAllocations.instance
  .addListener((ObjectEvent event) => myDartMethod(event.toMap()));
```

# ObjectEventListener

```dart
typedef ObjectEventListener = void Function(ObjectEvent event)
```

A listener of [ObjectEvent].

# ObjectCreated

```dart
class ObjectCreated extends ObjectEvent {}
```

An event that describes creation of an object.

### ObjectCreated()

```dart
ObjectCreated({required String library, required String className, required Object object})
```

Creates an instance of [ObjectCreated].

### library

```dart
String library
```

Name of the instrumented library.

The format of this parameter should be a library Uri. For example: `'package:flutter/rendering.dart'`.

### className

```dart
String className
```

Name of the instrumented class.

### toMap()

```dart
Map<Object, Map<String, Object>> toMap()
```

# ObjectDisposed

```dart
class ObjectDisposed extends ObjectEvent {}
```

An event that describes disposal of an object.

### ObjectDisposed()

```dart
ObjectDisposed({required Object object})
```

Creates an instance of [ObjectDisposed].

### toMap()

```dart
Map<Object, Map<String, Object>> toMap()
```

# MemoryAllocations

```dart
typedef MemoryAllocations = FlutterMemoryAllocations
```

An interface for listening to object lifecycle events.

# FlutterMemoryAllocations

```dart
class FlutterMemoryAllocations {}
```

An interface for listening to object lifecycle events.

If [kFlutterMemoryAllocationsEnabled] is true, [FlutterMemoryAllocations] listens to creation and disposal events for disposable objects in Flutter Framework. To dispatch other events objects, invoke [FlutterMemoryAllocations.dispatchObjectEvent].

Use this class with condition `kFlutterMemoryAllocationsEnabled`, to make sure not to increase size of the application by the code of the class, if memory allocations are disabled.

The class is optimized for massive event flow and small number of added or removed listeners.

### instance

```dart
FlutterMemoryAllocations instance
```

The shared instance of [FlutterMemoryAllocations].

Only call this when [kFlutterMemoryAllocationsEnabled] is true.

### addListener()

```dart
void addListener(ObjectEventListener listener)
```

Register a listener that is called every time an object event is dispatched.

Listeners can be removed with [removeListener].

Only call this when [kFlutterMemoryAllocationsEnabled] is true.

### removeListener()

```dart
void removeListener(ObjectEventListener listener)
```

Stop calling the given listener every time an object event is dispatched.

Listeners can be added with [addListener].

Only call this when [kFlutterMemoryAllocationsEnabled] is true.

### hasListeners

```dart
bool get hasListeners
```

Return true if there are listeners.

If there is no listeners, the app can save on creating the event object.

Only call this when [kFlutterMemoryAllocationsEnabled] is true.

### dispatchObjectEvent()

```dart
void dispatchObjectEvent(ObjectEvent event)
```

Dispatch a new object event to listeners.

Exceptions thrown by listeners will be caught and reported using [FlutterError.reportError].

Listeners added during an event dispatching, will start being invoked for next events, but will be skipped for this event.

Listeners, removed during an event dispatching, will not be invoked after the removal.

Only call this when [kFlutterMemoryAllocationsEnabled] is true.

### dispatchObjectCreated()

```dart
void dispatchObjectCreated({required String library, required String className, required Object object})
```

Create [ObjectCreated] and invoke [dispatchObjectEvent] if there are listeners.

This method is more efficient than [dispatchObjectEvent] if the event object is not created yet.

### dispatchObjectDisposed()

```dart
void dispatchObjectDisposed({required Object object})
```

Create [ObjectDisposed] and invoke [dispatchObjectEvent] if there are listeners.

This method is more efficient than [dispatchObjectEvent] if the event object is not created yet.
