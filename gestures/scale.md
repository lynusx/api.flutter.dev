# kDefaultMouseScrollToScaleFactor

```dart
double kDefaultMouseScrollToScaleFactor
```

The default conversion factor when treating mouse scrolling as scaling.

The value was arbitrarily chosen to feel natural for most mousewheels on all supported platforms.

# kDefaultTrackpadScrollToScaleFactor

```dart
Offset kDefaultTrackpadScrollToScaleFactor
```

The default conversion factor when treating trackpad scrolling as scaling.

This factor matches the default [kDefaultMouseScrollToScaleFactor] of 200 to feel natural for most trackpads, and the convention that scrolling up means zooming in.

# ScaleStartDetails

```dart
class ScaleStartDetails with Diagnosticable {}
```

Details for [GestureScaleStartCallback].

### ScaleStartDetails()

```dart
ScaleStartDetails({Offset focalPoint = Offset.zero, Offset? localFocalPoint, int pointerCount = 0, Duration? sourceTimeStamp, PointerDeviceKind? kind})
```

Creates details for [GestureScaleStartCallback].

### focalPoint

```dart
Offset focalPoint
```

The initial focal point of the pointers in contact with the screen.

Reported in global coordinates.

See also:

- [localFocalPoint], which is the same value reported in local coordinates.

### localFocalPoint

```dart
Offset localFocalPoint
```

The initial focal point of the pointers in contact with the screen.

Reported in local coordinates. Defaults to [focalPoint] if not set in the constructor.

See also:

- [focalPoint], which is the same value reported in global coordinates.

### pointerCount

```dart
int pointerCount
```

The number of pointers being tracked by the gesture recognizer.

Typically this is the number of fingers being used to pan the widget using the gesture recognizer.

### sourceTimeStamp

```dart
Duration? sourceTimeStamp
```

Recorded timestamp of the source pointer event that triggered the scale event.

Could be null if triggered from proxied events such as accessibility.

### kind

```dart
PointerDeviceKind? kind
```

The kind of the device that initiated the event.

If multiple pointers are touching the screen, the kind of the pointer device that first initiated the event is used.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ScaleUpdateDetails

```dart
class ScaleUpdateDetails with Diagnosticable {}
```

Details for [GestureScaleUpdateCallback].

### ScaleUpdateDetails()

```dart
ScaleUpdateDetails({Offset focalPoint = Offset.zero, Offset? localFocalPoint, double scale = 1.0, double horizontalScale = 1.0, double verticalScale = 1.0, double rotation = 0.0, int pointerCount = 0, Offset focalPointDelta = Offset.zero, Duration? sourceTimeStamp})
```

Creates details for [GestureScaleUpdateCallback].

The [scale], [horizontalScale], and [verticalScale] arguments must be greater than or equal to zero.

### focalPointDelta

```dart
Offset focalPointDelta
```

The amount the gesture's focal point has moved in the coordinate space of the event receiver since the previous update.

Defaults to zero if not specified in the constructor.

### focalPoint

```dart
Offset focalPoint
```

The focal point of the pointers in contact with the screen.

Reported in global coordinates.

See also:

- [localFocalPoint], which is the same value reported in local coordinates.

### localFocalPoint

```dart
Offset localFocalPoint
```

The focal point of the pointers in contact with the screen.

Reported in local coordinates. Defaults to [focalPoint] if not set in the constructor.

See also:

- [focalPoint], which is the same value reported in global coordinates.

### scale

```dart
double scale
```

The scale implied by the average distance between the pointers in contact with the screen.

This value must be greater than or equal to zero.

See also:

- [horizontalScale], which is the scale along the horizontal axis.
- [verticalScale], which is the scale along the vertical axis.

### horizontalScale

```dart
double horizontalScale
```

The scale implied by the average distance along the horizontal axis between the pointers in contact with the screen.

This value must be greater than or equal to zero.

See also:

- [scale], which is the general scale implied by the pointers.
- [verticalScale], which is the scale along the vertical axis.

### verticalScale

```dart
double verticalScale
```

The scale implied by the average distance along the vertical axis between the pointers in contact with the screen.

This value must be greater than or equal to zero.

See also:

- [scale], which is the general scale implied by the pointers.
- [horizontalScale], which is the scale along the horizontal axis.

### rotation

```dart
double rotation
```

The angle implied by the first two pointers to enter in contact with the screen.

Expressed in radians.

### pointerCount

```dart
int pointerCount
```

The number of pointers being tracked by the gesture recognizer.

Typically this is the number of fingers being used to pan the widget using the gesture recognizer. Due to platform limitations, trackpad gestures count as two fingers even if more than two fingers are used.

### sourceTimeStamp

```dart
Duration? sourceTimeStamp
```

Recorded timestamp of the source pointer event that triggered the scale event.

Could be null if triggered from proxied events such as accessibility.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ScaleEndDetails

```dart
class ScaleEndDetails with Diagnosticable {}
```

Details for [GestureScaleEndCallback].

### ScaleEndDetails()

```dart
ScaleEndDetails({Velocity velocity = Velocity.zero, double scaleVelocity = 0, int pointerCount = 0})
```

Creates details for [GestureScaleEndCallback].

### velocity

```dart
Velocity velocity
```

The velocity of the last pointer to be lifted off of the screen.

### scaleVelocity

```dart
double scaleVelocity
```

The final velocity of the scale factor reported by the gesture.

### pointerCount

```dart
int pointerCount
```

The number of pointers being tracked by the gesture recognizer.

Typically this is the number of fingers being used to pan the widget using the gesture recognizer.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# GestureScaleStartCallback

```dart
typedef GestureScaleStartCallback = void Function(ScaleStartDetails details)
```

Signature for when the pointers in contact with the screen have established a focal point and initial scale of 1.0.

# GestureScaleUpdateCallback

```dart
typedef GestureScaleUpdateCallback = void Function(ScaleUpdateDetails details)
```

Signature for when the pointers in contact with the screen have indicated a new focal point and/or scale.

# GestureScaleEndCallback

```dart
typedef GestureScaleEndCallback = void Function(ScaleEndDetails details)
```

Signature for when the pointers are no longer in contact with the screen.

# ScaleGestureRecognizer

```dart
class ScaleGestureRecognizer extends OneSequenceGestureRecognizer {}
```

Recognizes a scale gesture.

[ScaleGestureRecognizer] tracks the pointers in contact with the screen and calculates their focal point, indicated scale, and rotation. When a focal point is established, the recognizer calls [onStart]. As the focal point, scale, and rotation change, the recognizer calls [onUpdate]. When the pointers are no longer in contact with the screen, the recognizer calls [onEnd].

### ScaleGestureRecognizer()

```dart
ScaleGestureRecognizer({Object? debugOwner, Set<InvalidType>? supportedDevices, bool Function(int) allowedButtonsFilter, DragStartBehavior dragStartBehavior = DragStartBehavior.down, bool trackpadScrollCausesScale = false, Offset trackpadScrollToScaleFactor = kDefaultTrackpadScrollToScaleFactor})
```

Create a gesture recognizer for interactions intended for scaling content.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

Determines what point is used as the starting point in all calculations involving this gesture.

When set to [DragStartBehavior.down], the scale is calculated starting from the position where the pointer first contacted the screen.

When set to [DragStartBehavior.start], the scale is calculated starting from the position where the scale gesture began. The scale gesture may begin after the time that the pointer first contacted the screen if there are multiple listeners competing for the gesture. In that case, the gesture arena waits to determine whether or not the gesture is a scale gesture before giving the gesture to this GestureRecognizer. This happens in the case of nested GestureDetectors, for example.

Defaults to [DragStartBehavior.down].

See also:

- https://flutter.dev/to/gesture-disambiguation, which provides more information about the gesture arena.

### onStart

```dart
GestureScaleStartCallback? onStart
```

The pointers in contact with the screen have established a focal point and initial scale of 1.0.

This won't be called until the gesture arena has determined that this GestureRecognizer has won the gesture.

See also:

- https://flutter.dev/to/gesture-disambiguation, which provides more information about the gesture arena.

### onUpdate

```dart
GestureScaleUpdateCallback? onUpdate
```

The pointers in contact with the screen have indicated a new focal point and/or scale.

### onEnd

```dart
GestureScaleEndCallback? onEnd
```

The pointers are no longer in contact with the screen.

### trackpadScrollCausesScale

```dart
bool trackpadScrollCausesScale
```

{@template flutter.gestures.scale.trackpadScrollCausesScale} Whether scrolling up/down on a trackpad should cause scaling instead of panning.

Defaults to false. {@endtemplate}

### trackpadScrollToScaleFactor

```dart
Offset trackpadScrollToScaleFactor
```

{@template flutter.gestures.scale.trackpadScrollToScaleFactor} A factor to control the direction and magnitude of scale when converting trackpad scrolling.

Incoming trackpad pan offsets will be divided by this factor to get scale values. Increasing this offset will reduce the amount of scaling caused by a fixed amount of trackpad scrolling.

Defaults to [kDefaultTrackpadScrollToScaleFactor]. {@endtemplate}

### pointerCount

```dart
int get pointerCount
```

The number of pointers being tracked by the gesture recognizer.

Typically this is the number of fingers being used to pan the widget using the gesture recognizer.

### addAllowedPointer()

```dart
void addAllowedPointer(PointerDownEvent event)
```

### isPointerPanZoomAllowed()

```dart
bool isPointerPanZoomAllowed(PointerPanZoomStartEvent event)
```

### addAllowedPointerPanZoom()

```dart
void addAllowedPointerPanZoom(PointerPanZoomStartEvent event)
```

### handleEvent()

```dart
void handleEvent(PointerEvent event)
```

### acceptGesture()

```dart
void acceptGesture(int pointer)
```

### rejectGesture()

```dart
void rejectGesture(int pointer)
```

### didStopTrackingLastPointer()

```dart
void didStopTrackingLastPointer(int pointer)
```

### dispose()

```dart
void dispose()
```

### debugDescription

```dart
String get debugDescription
```
