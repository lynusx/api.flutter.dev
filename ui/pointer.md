# PointerChange

```dart
enum PointerChange {}
```

How the pointer has changed since the last report.

The input from the pointer is no longer directed towards this receiver.

The device has started tracking the pointer.

For example, the pointer might be hovering above the device, having not yet made contact with the surface of the device.

The device is no longer tracking the pointer.

For example, the pointer might have drifted out of the device's hover detection range or might have been disconnected from the system entirely.

The pointer has moved with respect to the device while not in contact with the device.

The pointer has made contact with the device.

The pointer has moved with respect to the device while in contact with the device.

The pointer has stopped making contact with the device.

A pan/zoom has started on this pointer.

This type of event will always have kind [PointerDeviceKind.trackpad].

The pan/zoom on this pointer has updated.

This type of event will always have kind [PointerDeviceKind.trackpad].

The pan/zoom on this pointer has ended.

This type of event will always have kind [PointerDeviceKind.trackpad].

# PointerDeviceKind

```dart
enum PointerDeviceKind {}
```

The kind of pointer device.

A touch-based pointer device.

The most common case is a touch screen.

When the user is operating with a trackpad on iOS, clicking will also dispatch events with kind [touch] if `UIApplicationSupportsIndirectInputEvents` is not present in `Info.plist` or returns NO.

See also:

- [UIApplicationSupportsIndirectInputEvents](https://developer.apple.com/documentation/bundleresources/information_property_list/uiapplicationsupportsindirectinputevents?language=objc).

A mouse-based pointer device.

The most common case is a mouse on the desktop or Web.

When the user is operating with a trackpad on iOS, moving the pointing cursor will also dispatch events with kind [mouse], and clicking will dispatch events with kind [mouse] if `UIApplicationSupportsIndirectInputEvents` is not present in `Info.plist` or returns NO.

See also:

- [UIApplicationSupportsIndirectInputEvents](https://developer.apple.com/documentation/bundleresources/information_property_list/uiapplicationsupportsindirectinputevents?language=objc).

A pointer device with a stylus.

A pointer device with a stylus that has been inverted.

Gestures from a trackpad.

A trackpad here is defined as a touch-based pointer device with an indirect surface (the user operates the screen by touching something that is not the screen).

When the user makes zoom, pan, scroll or rotate gestures with a physical trackpad, supporting platforms dispatch events with kind [trackpad].

Events with kind [trackpad] can only have a [PointerChange] of `add`, `remove`, and pan-zoom related values.

Some platforms don't support (or don't fully support) trackpad gestures, and might convert trackpad gestures into fake pointer events that simulate dragging. These events typically have kind [touch] or [mouse] instead of [trackpad]. This includes (but is not limited to) Web, and iOS when `UIApplicationSupportsIndirectInputEvents` isn't present in `Info.plist` or returns NO.

Moving the pointing cursor or clicking with a trackpad typically triggers [touch] or [mouse] events, but never triggers [trackpad] events.

See also:

- [UIApplicationSupportsIndirectInputEvents](https://developer.apple.com/documentation/bundleresources/information_property_list/uiapplicationsupportsindirectinputevents?language=objc).

An unknown pointer device.

# PointerSignalKind

```dart
enum PointerSignalKind {}
```

The kind of pointer signal event.

The event is not associated with a pointer signal.

A pointer-generated scroll (e.g., mouse wheel or trackpad scroll).

A pointer-generated scroll-inertia cancel.

A pointer-generated scale event (e.g. trackpad pinch).

An unknown pointer signal kind.

# PointerDataRespondCallback

```dart
typedef PointerDataRespondCallback = void Function({bool allowPlatformDefault})
```

A function that implements the [PointerData.respond] method.

# PointerData

```dart
class PointerData {}
```

Information about the state of a pointer.

### PointerData()

```dart
PointerData({int viewId = 0, int embedderId = 0, Duration timeStamp = Duration.zero, PointerChange change = PointerChange.cancel, PointerDeviceKind kind = PointerDeviceKind.touch, PointerSignalKind? signalKind, int device = 0, int pointerIdentifier = 0, double physicalX = 0.0, double physicalY = 0.0, double physicalDeltaX = 0.0, double physicalDeltaY = 0.0, int buttons = 0, bool obscured = false, bool synthesized = false, double pressure = 0.0, double pressureMin = 0.0, double pressureMax = 0.0, double distance = 0.0, double distanceMax = 0.0, double size = 0.0, double radiusMajor = 0.0, double radiusMinor = 0.0, double radiusMin = 0.0, double radiusMax = 0.0, double orientation = 0.0, double tilt = 0.0, int platformData = 0, double scrollDeltaX = 0.0, double scrollDeltaY = 0.0, double panX = 0.0, double panY = 0.0, double panDeltaX = 0.0, double panDeltaY = 0.0, double scale = 0.0, double rotation = 0.0, PointerDataRespondCallback? onRespond})
```

Creates an object that represents the state of a pointer.

### viewId

```dart
int viewId
```

The ID of the [FlutterView] this [PointerEvent] originated from.

### embedderId

```dart
int embedderId
```

Unique identifier that ties the [PointerEvent] to the embedder event that created it. it.

No two pointer events can have the same [embedderId]. This is different from [pointerIdentifier] - used for hit-testing, whereas [embedderId] is used to identify the platform event.

### timeStamp

```dart
Duration timeStamp
```

Time of event dispatch, relative to an arbitrary timeline.

### change

```dart
PointerChange change
```

How the pointer has changed since the last report.

### kind

```dart
PointerDeviceKind kind
```

The kind of input device for which the event was generated.

### signalKind

```dart
PointerSignalKind? signalKind
```

The kind of signal for a pointer signal event.

### device

```dart
int device
```

Unique identifier for the pointing device, reused across interactions.

### pointerIdentifier

```dart
int pointerIdentifier
```

Unique identifier for the pointer.

This field changes for each new pointer down event. Framework uses this identifier to determine hit test result.

### physicalX

```dart
double physicalX
```

X coordinate of the position of the pointer, in physical pixels in the global coordinate space.

### physicalY

```dart
double physicalY
```

Y coordinate of the position of the pointer, in physical pixels in the global coordinate space.

### physicalDeltaX

```dart
double physicalDeltaX
```

The distance of pointer movement on X coordinate in physical pixels.

### physicalDeltaY

```dart
double physicalDeltaY
```

The distance of pointer movement on Y coordinate in physical pixels.

### buttons

```dart
int buttons
```

Bit field using the \*Button constants (primaryMouseButton, secondaryStylusButton, etc). For example, if this has the value 6 and the [kind] is [PointerDeviceKind.invertedStylus], then this indicates an upside-down stylus with both its primary and secondary buttons pressed.

### obscured

```dart
bool obscured
```

Set if an application from a different security domain is in any way obscuring this application's window. (Aspirational; not currently implemented.)

### synthesized

```dart
bool synthesized
```

Set if this pointer data was synthesized by pointer data packet converter. pointer data packet converter will synthesize additional pointer datas if the input sequence of pointer data is illegal.

For example, a down pointer data will be synthesized if the converter receives a move pointer data while the pointer is not previously down.

### pressure

```dart
double pressure
```

The pressure of the touch as a number ranging from 0.0, indicating a touch with no discernible pressure, to 1.0, indicating a touch with "normal" pressure, and possibly beyond, indicating a stronger touch. For devices that do not detect pressure (e.g. mice), returns 1.0.

### pressureMin

```dart
double pressureMin
```

The minimum value that [pressure] can return for this pointer. For devices that do not detect pressure (e.g. mice), returns 1.0. This will always be a number less than or equal to 1.0.

### pressureMax

```dart
double pressureMax
```

The maximum value that [pressure] can return for this pointer. For devices that do not detect pressure (e.g. mice), returns 1.0. This will always be a greater than or equal to 1.0.

### distance

```dart
double distance
```

The distance of the detected object from the input surface (e.g. the distance of a stylus or finger from a touch screen), in arbitrary units on an arbitrary (not necessarily linear) scale. If the pointer is down, this is 0.0 by definition.

### distanceMax

```dart
double distanceMax
```

The maximum value that a distance can return for this pointer. If this input device cannot detect "hover touch" input events, then this will be 0.0.

### size

```dart
double size
```

The area of the screen being pressed, scaled to a value between 0 and 1. The value of size can be used to determine fat touch events. This value is only set on Android, and is a device specific approximation within the range of detectable values. So, for example, the value of 0.1 could mean a touch with the tip of the finger, 0.2 a touch with full finger, and 0.3 the full palm.

### radiusMajor

```dart
double radiusMajor
```

The radius of the contact ellipse along the major axis, in logical pixels.

### radiusMinor

```dart
double radiusMinor
```

The radius of the contact ellipse along the minor axis, in logical pixels.

### radiusMin

```dart
double radiusMin
```

The minimum value that could be reported for radiusMajor and radiusMinor for this pointer, in logical pixels.

### radiusMax

```dart
double radiusMax
```

The minimum value that could be reported for radiusMajor and radiusMinor for this pointer, in logical pixels.

### orientation

```dart
double orientation
```

For PointerDeviceKind.touch events:

The angle of the contact ellipse, in radius in the range:

-pi/2 < orientation <= pi/2

...giving the angle of the major axis of the ellipse with the y-axis (negative angles indicating an orientation along the top-left / bottom-right diagonal, positive angles indicating an orientation along the top-right / bottom-left diagonal, and zero indicating an orientation parallel with the y-axis).

For PointerDeviceKind.stylus and PointerDeviceKind.invertedStylus events:

The angle of the stylus, in radians in the range:

-pi < orientation <= pi

...giving the angle of the axis of the stylus projected onto the input surface, relative to the positive y-axis of that surface (thus 0.0 indicates the stylus, if projected onto that surface, would go from the contact point vertically up in the positive y-axis direction, pi would indicate that the stylus would go down in the negative y-axis direction; pi/4 would indicate that the stylus goes up and to the right, -pi/2 would indicate that the stylus goes to the left, etc).

### tilt

```dart
double tilt
```

For PointerDeviceKind.stylus and PointerDeviceKind.invertedStylus events:

The angle of the stylus, in radians in the range:

0 <= tilt <= pi/2

...giving the angle of the axis of the stylus, relative to the axis perpendicular to the input surface (thus 0.0 indicates the stylus is orthogonal to the plane of the input surface, while pi/2 indicates that the stylus is flat on that surface).

### platformData

```dart
int platformData
```

Opaque platform-specific data associated with the event.

### scrollDeltaX

```dart
double scrollDeltaX
```

For events with signalKind of PointerSignalKind.scroll:

The amount to scroll in the x direction, in physical pixels.

### scrollDeltaY

```dart
double scrollDeltaY
```

For events with signalKind of PointerSignalKind.scroll:

The amount to scroll in the y direction, in physical pixels.

### panX

```dart
double panX
```

For events with change of PointerChange.panZoomUpdate:

The current panning magnitude of the pan/zoom in the x direction, in physical pixels.

### panY

```dart
double panY
```

For events with change of PointerChange.panZoomUpdate:

The current panning magnitude of the pan/zoom in the y direction, in physical pixels.

### panDeltaX

```dart
double panDeltaX
```

For events with change of PointerChange.panZoomUpdate:

The difference in panning of the pan/zoom in the x direction since the latest panZoomUpdate event, in physical pixels.

### panDeltaY

```dart
double panDeltaY
```

For events with change of PointerChange.panZoomUpdate:

The difference in panning of the pan/zoom in the y direction since the last panZoomUpdate event, in physical pixels.

### scale

```dart
double scale
```

For events with change of PointerChange.panZoomUpdate:

The current scale of the pan/zoom (unitless), with 1.0 as the initial scale.

### rotation

```dart
double rotation
```

For events with change of PointerChange.panZoomUpdate:

The current angle of the pan/zoom in radians, with 0.0 as the initial angle.

### respond()

```dart
void respond({required bool allowPlatformDefault})
```

Method that the framework/app can call to respond to the native event that triggered this [PointerData].

The parameter [allowPlatformDefault] allows the platform to perform the default action associated with the native event when it's set to `true`.

This method can be called any number of times, but once `allowPlatformDefault` is set to `true`, it can't be set to `false` again.

If `allowPlatformDefault` is never set to `true`, the Flutter engine will consume the event, so it won't be seen by the platform. In the web, this means that `preventDefault` will be called in the DOM event that triggered the `PointerData`. See [Event: preventDefault() method in MDN][EpDmiMDN].

The implementation of this method is configured through the `onRespond` parameter of the [PointerData] constructor.

See also [PointerDataRespondCallback].

[EpDmiMDN]: https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault

### toString()

```dart
String toString()
```

### toStringFull()

```dart
String toStringFull()
```

Returns a complete textual description of the information in this object.

# PointerDataPacket

```dart
class PointerDataPacket {}
```

A sequence of reports about the state of pointers.

### PointerDataPacket()

```dart
PointerDataPacket({List<PointerData> data = const <PointerData>[]})
```

Creates a packet of pointer data reports.

### data

```dart
List<PointerData> data
```

Data about the individual pointers in this packet.

This list might contain multiple pieces of data about the same pointer.
