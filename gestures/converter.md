@docImport 'dart:ui';

# DevicePixelRatioGetter

```dart
typedef DevicePixelRatioGetter = double? Function(int viewId)
```

Signature for a callback that returns the device pixel ratio of a [FlutterView] identified by the provided `viewId`.

Returns null if no view with the provided ID exists.

Used by [PointerEventConverter.expand].

See also:

- [FlutterView.devicePixelRatio] for an explanation of device pixel ratio.

# PointerEventConverter

```dart
abstract final class PointerEventConverter {}
```

Converts from engine pointer data to framework pointer events.

This takes [PointerDataPacket] objects, as received from the engine via [dart:ui.PlatformDispatcher.onPointerDataPacket], and converts them to [PointerEvent] objects.

### expand()

```dart
Iterable<PointerEvent> expand(Iterable<ui.PointerData> data, DevicePixelRatioGetter devicePixelRatioForView)
```

Expand the given packet of pointer data into a sequence of framework pointer events.

The `devicePixelRatioForView` is used to obtain the device pixel ratio for the view a particular event occurred in to convert its data from physical coordinates to logical pixels. See the discussion at [PointerEvent] for more details on the [PointerEvent] coordinate space.
