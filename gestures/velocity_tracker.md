# Velocity

```dart
class Velocity {}
```

A velocity in two dimensions.

### Velocity()

```dart
Velocity({required Offset pixelsPerSecond})
```

Creates a [Velocity].

### zero

```dart
Velocity zero
```

A velocity that isn't moving at all.

### pixelsPerSecond

```dart
Offset pixelsPerSecond
```

The number of pixels per second of velocity in the x and y directions.

### operator -()

```dart
Velocity operator -()
```

Return the negation of a velocity.

### operator -()

```dart
Velocity operator -(Velocity other)
```

Return the difference of two velocities.

### operator +()

```dart
Velocity operator +(Velocity other)
```

Return the sum of two velocities.

### clampMagnitude()

```dart
Velocity clampMagnitude(double minValue, double maxValue)
```

Return a velocity whose magnitude has been clamped to [minValue] and [maxValue].

If the magnitude of this Velocity is less than minValue then return a new Velocity with the same direction and with magnitude [minValue]. Similarly, if the magnitude of this Velocity is greater than maxValue then return a new Velocity with the same direction and magnitude [maxValue].

If the magnitude of this Velocity is within the specified bounds then just return this.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# VelocityEstimate

```dart
class VelocityEstimate {}
```

A two dimensional velocity estimate.

VelocityEstimates are computed by [VelocityTracker.getVelocityEstimate]. An estimate's [confidence] measures how well the velocity tracker's position data fit a straight line, [duration] is the time that elapsed between the first and last position sample used to compute the velocity, and [offset] is similarly the difference between the first and last positions.

See also:

- [VelocityTracker], which computes [VelocityEstimate]s.
- [Velocity], which encapsulates (just) a velocity vector and provides some useful velocity operations.

### VelocityEstimate()

```dart
VelocityEstimate({required Offset pixelsPerSecond, required double confidence, required Duration duration, required Offset offset})
```

Creates a dimensional velocity estimate.

### pixelsPerSecond

```dart
Offset pixelsPerSecond
```

The number of pixels per second of velocity in the x and y directions.

### confidence

```dart
double confidence
```

A value between 0.0 and 1.0 that indicates how well [VelocityTracker] was able to fit a straight line to its position data.

The value of this property is 1.0 for a perfect fit, 0.0 for a poor fit.

### duration

```dart
Duration duration
```

The time that elapsed between the first and last position sample used to compute [pixelsPerSecond].

### offset

```dart
Offset offset
```

The difference between the first and last position sample used to compute [pixelsPerSecond].

### toString()

```dart
String toString()
```

# VelocityTracker

```dart
class VelocityTracker {}
```

Computes a pointer's velocity based on data from [PointerMoveEvent]s.

The input data is provided by calling [addPosition]. Adding data is cheap.

To obtain a velocity, call [getVelocity] or [getVelocityEstimate]. This will compute the velocity based on the data added so far. Only call these when you need to use the velocity, as they are comparatively expensive.

The quality of the velocity estimation will be better if more data points have been received.

### VelocityTracker.withKind()

```dart
VelocityTracker.withKind(PointerDeviceKind kind)
```

Create a new velocity tracker for a pointer [kind].

### kind

```dart
PointerDeviceKind kind
```

The kind of pointer this tracker is for.

### addPosition()

```dart
void addPosition(Duration time, Offset position)
```

Adds a position as the given time to the tracker.

### getVelocityEstimate()

```dart
VelocityEstimate? getVelocityEstimate()
```

Returns an estimate of the velocity of the object being tracked by the tracker given the current information available to the tracker.

Information is added using [addPosition].

Returns null if there is no data on which to base an estimate.

### getVelocity()

```dart
Velocity getVelocity()
```

Computes the velocity of the pointer at the time of the last provided data point.

This can be expensive. Only call this when you need the velocity.

Returns [Velocity.zero] if there is no data from which to compute an estimate or if the estimated velocity is zero.

# IOSScrollViewFlingVelocityTracker

```dart
class IOSScrollViewFlingVelocityTracker extends VelocityTracker {}
```

A [VelocityTracker] subclass that provides a close approximation of iOS scroll view's velocity estimation strategy.

The estimated velocity reported by this class is a close approximation of the velocity an iOS scroll view would report with the same [PointerMoveEvent]s, when the touch that initiates a fling is released.

This class differs from the [VelocityTracker] class in that it uses weighted average of the latest few velocity samples of the tracked pointer, instead of doing a linear regression on a relatively large amount of data points, to estimate the velocity of the tracked pointer. Adding data points and estimating the velocity are both cheap.

To obtain a velocity, call [getVelocity] or [getVelocityEstimate]. The estimated velocity is typically used as the initial flinging velocity of a `Scrollable`, when its drag gesture ends.

See also:

- [scrollViewWillEndDragging(_:withVelocity:targetContentOffset:)](https://developer.apple.com/documentation/uikit/uiscrollviewdelegate/1619385-scrollviewwillenddragging), the iOS method that reports the fling velocity when the touch is released.

### IOSScrollViewFlingVelocityTracker()

```dart
IOSScrollViewFlingVelocityTracker(dynamic kind)
```

Create a new IOSScrollViewFlingVelocityTracker.

### addPosition()

```dart
void addPosition(Duration time, Offset position)
```

### getVelocityEstimate()

```dart
VelocityEstimate getVelocityEstimate()
```

# MacOSScrollViewFlingVelocityTracker

```dart
class MacOSScrollViewFlingVelocityTracker extends IOSScrollViewFlingVelocityTracker {}
```

A [VelocityTracker] subclass that provides a close approximation of macOS scroll view's velocity estimation strategy.

The estimated velocity reported by this class is a close approximation of the velocity a macOS scroll view would report with the same [PointerMoveEvent]s, when the touch that initiates a fling is released.

This class differs from the [VelocityTracker] class in that it uses weighted average of the latest few velocity samples of the tracked pointer, instead of doing a linear regression on a relatively large amount of data points, to estimate the velocity of the tracked pointer. Adding data points and estimating the velocity are both cheap.

To obtain a velocity, call [getVelocity] or [getVelocityEstimate]. The estimated velocity is typically used as the initial flinging velocity of a `Scrollable`, when its drag gesture ends.

### MacOSScrollViewFlingVelocityTracker()

```dart
MacOSScrollViewFlingVelocityTracker(dynamic kind)
```

Create a new MacOSScrollViewFlingVelocityTracker.

### getVelocityEstimate()

```dart
VelocityEstimate getVelocityEstimate()
```
