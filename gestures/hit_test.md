@docImport 'package:flutter/rendering.dart';

# HitTestable

```dart
abstract interface class HitTestable {}
```

An object that can hit-test pointers.

### hitTest()

```dart
void hitTest(HitTestResult result, Offset position)
```

Deprecated. Use [hitTestInView] instead.

### hitTestInView()

```dart
void hitTestInView(HitTestResult result, Offset position, int viewId)
```

Fills the provided [HitTestResult] with [HitTestEntry]s for objects that are hit at the given `position` in the view identified by `viewId`.

# HitTestDispatcher

```dart
abstract interface class HitTestDispatcher {}
```

An object that can dispatch events.

### dispatchEvent()

```dart
void dispatchEvent(PointerEvent event, HitTestResult result)
```

Override this method to dispatch events.

# HitTestTarget

```dart
abstract interface class HitTestTarget {}
```

An object that can handle events.

The type must implement [NativeHitTestTarget] if it represents a platform view.

### handleEvent()

```dart
void handleEvent(PointerEvent event, HitTestEntry<HitTestTarget> entry)
```

Override this method to receive events.

# NativeHitTestTarget

```dart
mixin NativeHitTestTarget {}
```

A mixin that represents a hit test target backed by a platform view.

See also:

- [HitTestTarget].

# HitTestEntry

```dart
class HitTestEntry<T extends HitTestTarget> {}
```

Data collected during a hit test about a specific [HitTestTarget].

Subclass this object to pass additional information from the hit test phase to the event propagation phase.

### HitTestEntry()

```dart
HitTestEntry(T target)
```

Creates a hit test entry.

### target

```dart
T target
```

The [HitTestTarget] encountered during the hit test.

### toString()

```dart
String toString()
```

### transform

```dart
Matrix4? get transform
```

Returns a matrix describing how [PointerEvent]s delivered to this [HitTestEntry] should be transformed from the global coordinate space of the screen to the local coordinate space of [target].

See also:

- [BoxHitTestResult.addWithPaintTransform], which is used during hit testing to build up this transform.

# HitTestResult

```dart
class HitTestResult {}
```

The result of performing a hit test.

### HitTestResult()

```dart
HitTestResult()
```

Creates an empty hit test result.

### HitTestResult.wrap()

```dart
HitTestResult.wrap(HitTestResult result)
```

Wraps `result` (usually a subtype of [HitTestResult]) to create a generic [HitTestResult].

The [HitTestEntry]s added to the returned [HitTestResult] are also added to the wrapped `result` (both share the same underlying data structure to store [HitTestEntry]s).

### path

```dart
Iterable<HitTestEntry> get path
```

An unmodifiable list of [HitTestEntry] objects recorded during the hit test.

The first entry in the path is the most specific, typically the one at the leaf of tree being hit tested. Event propagation starts with the most specific (i.e., first) entry and proceeds in order through the path.

### add()

```dart
void add(HitTestEntry entry)
```

Add a [HitTestEntry] to the path.

The new entry is added at the end of the path, which means entries should be added in order from most specific to least specific, typically during an upward walk of the tree being hit tested.

### pushTransform()

```dart
void pushTransform(Matrix4 transform)
```

Pushes a new transform matrix that is to be applied to all future [HitTestEntry]s added via [add] until it is removed via [popTransform].

This method is only to be used by subclasses, which must provide coordinate space specific public wrappers around this function for their users (see [BoxHitTestResult.addWithPaintTransform] for such an example).

The provided `transform` matrix should describe how to transform [PointerEvent]s from the coordinate space of the method caller to the coordinate space of its children. In most cases `transform` is derived from running the inverted result of [RenderObject.applyPaintTransform] through [PointerEvent.removePerspectiveTransform] to remove the perspective component.

If the provided `transform` is a translation matrix, it is much faster to use [pushOffset] with the translation offset instead.

[HitTestable]s need to call this method indirectly through a convenience method defined on a subclass before hit testing a child that does not have the same origin as the parent. After hit testing the child, [popTransform] has to be called to remove the child-specific `transform`.

See also:

- [pushOffset], which is similar to [pushTransform] but is limited to translations, and is faster in such cases.
- [BoxHitTestResult.addWithPaintTransform], which is a public wrapper around this function for hit testing on [RenderBox]s.

### pushOffset()

```dart
void pushOffset(Offset offset)
```

Pushes a new translation offset that is to be applied to all future [HitTestEntry]s added via [add] until it is removed via [popTransform].

This method is only to be used by subclasses, which must provide coordinate space specific public wrappers around this function for their users (see [BoxHitTestResult.addWithPaintOffset] for such an example).

The provided `offset` should describe how to transform [PointerEvent]s from the coordinate space of the method caller to the coordinate space of its children. Usually `offset` is the inverse of the offset of the child relative to the parent.

[HitTestable]s need to call this method indirectly through a convenience method defined on a subclass before hit testing a child that does not have the same origin as the parent. After hit testing the child, [popTransform] has to be called to remove the child-specific `transform`.

See also:

- [pushTransform], which is similar to [pushOffset] but allows general transform besides translation.
- [BoxHitTestResult.addWithPaintOffset], which is a public wrapper around this function for hit testing on [RenderBox]s.
- [SliverHitTestResult.addWithAxisOffset], which is a public wrapper around this function for hit testing on [RenderSliver]s.

### popTransform()

```dart
void popTransform()
```

Removes the last transform added via [pushTransform] or [pushOffset].

This method is only to be used by subclasses, which must provide coordinate space specific public wrappers around this function for their users (see [BoxHitTestResult.addWithPaintTransform] for such an example).

This method must be called after hit testing is done on a child that required a call to [pushTransform] or [pushOffset].

See also:

- [pushTransform] and [pushOffset], which describes the use case of this function pair in more details.

### toString()

```dart
String toString()
```
