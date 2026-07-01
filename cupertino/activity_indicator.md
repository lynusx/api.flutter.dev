# CupertinoActivityIndicator

```dart
class CupertinoActivityIndicator extends StatefulWidget {}
```

An iOS-style activity indicator that spins clockwise.

{@youtube 560 315 https://www.youtube.com/watch?v=AENVH-ZqKDQ}

{@tool dartpad} This example shows how [CupertinoActivityIndicator] can be customized.

** See code in examples/api/lib/cupertino/activity_indicator/cupertino_activity_indicator.0.dart ** {@end-tool}

See also:

- [CupertinoLinearActivityIndicator], which displays progress along a line.
- <https://developer.apple.com/design/human-interface-guidelines/progress-indicators/>

### CupertinoActivityIndicator()

```dart
CupertinoActivityIndicator({dynamic key, Color? color, bool animating = true, double radius = _kDefaultIndicatorRadius})
```

Creates an iOS-style activity indicator that spins clockwise.

### CupertinoActivityIndicator.partiallyRevealed()

```dart
CupertinoActivityIndicator.partiallyRevealed({dynamic key, Color? color, double radius = _kDefaultIndicatorRadius, double progress = 1.0})
```

Creates a non-animated iOS-style activity indicator that displays a partial count of ticks based on the value of [progress].

When provided, the value of [progress] must be between 0.0 (zero ticks will be shown) and 1.0 (all ticks will be shown) inclusive. Defaults to 1.0.

### color

```dart
Color? color
```

Color of the activity indicator.

Defaults to color extracted from native iOS.

### animating

```dart
bool animating
```

Whether the activity indicator is running its animation.

Defaults to true.

### radius

```dart
double radius
```

Radius of the spinner widget.

Defaults to 10 pixels. Must be positive.

### progress

```dart
double progress
```

Determines the percentage of spinner ticks that will be shown. Typical usage would display all ticks, however, this allows for more fine-grained control such as during pull-to-refresh when the drag-down action shows one tick at a time as the user continues to drag down.

Defaults to one. Must be between zero and one, inclusive.

### createState()

```dart
State<CupertinoActivityIndicator> createState()
```

# CupertinoLinearActivityIndicator

```dart
class CupertinoLinearActivityIndicator extends StatelessWidget {}
```

An iOS-style linear activity indicator.

The [CupertinoLinearActivityIndicator] is a linear progress bar that displays a colored bar to indicate the progress of an ongoing task.

{@tool dartpad} This example shows how [CupertinoLinearActivityIndicator] can be customized.

** See code in examples/api/lib/cupertino/activity_indicator/cupertino_linear_activity_indicator.0.dart ** {@end-tool}

See also:

- [CupertinoActivityIndicator], which is an iOS-style activity indicator that spins clockwise.
- <https://developer.apple.com/design/human-interface-guidelines/progress-indicators/>

### CupertinoLinearActivityIndicator()

```dart
CupertinoLinearActivityIndicator({dynamic key, required double progress, double height = 4.5, Color? color})
```

Creates a linear iOS-style activity indicator.

### progress

```dart
double progress
```

The current progress of the linear activity indicator.

This value must be between 0.0 and 1.0. A value of 0.0 means no progress and 1.0 means that progress is complete.

### height

```dart
double height
```

The height of the line used to draw the linear activity indicator.

Defaults to 4.5 units. Must be positive.

### color

```dart
Color? color
```

The color of the progress bar.

This color represents the portion of the bar that indicates progress.

Defaults to [CupertinoColors.activeBlue] if no color is specified.

### build()

```dart
Widget build(BuildContext context)
```
