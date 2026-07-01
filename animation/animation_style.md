@docImport 'package:flutter/material.dart';

# AnimationStyle

```dart
class AnimationStyle with Diagnosticable {}
```

Used to override the default parameters of an animation.

Currently, this class is used by the following widgets:

- [Expansible]
- [ExpansionTile]
- [MaterialApp]
- [PopupMenuButton]
- [ScaffoldMessengerState.showSnackBar]
- [showBottomSheet]
- [showModalBottomSheet]

If [duration] and [reverseDuration] are set to [Duration.zero], the corresponding animation will be disabled.

All of the parameters are optional. If no parameters are specified, the default animation will be used.

### AnimationStyle()

```dart
AnimationStyle({Curve? curve, Duration? duration, Curve? reverseCurve, Duration? reverseDuration})
```

Creates an instance of Animation Style class.

### noAnimation

```dart
AnimationStyle noAnimation
```

Creates an instance of Animation Style class with no animation.

### curve

```dart
Curve? curve
```

When specified, the animation will use this curve.

### duration

```dart
Duration? duration
```

When specified, the animation will use this duration.

### reverseCurve

```dart
Curve? reverseCurve
```

When specified, the reverse animation will use this curve.

### reverseDuration

```dart
Duration? reverseDuration
```

When specified, the reverse animation will use this duration.

### copyWith()

```dart
AnimationStyle copyWith({Curve? curve, Duration? duration, Curve? reverseCurve, Duration? reverseDuration})
```

Creates a new [AnimationStyle] based on the current selection, with the provided parameters overridden.

### merge()

```dart
AnimationStyle merge(AnimationStyle? other)
```

Creates a new [AnimationStyle] that is a combination of this animation style and the given `other` animation style.

If `other` is non-null, its non-null properties are used to override the corresponding properties of this style.

Returns this animation style if `other` is null.

### lerp()

```dart
AnimationStyle? lerp(AnimationStyle? a, AnimationStyle? b, double t)
```

Linearly interpolate between two animation styles.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
