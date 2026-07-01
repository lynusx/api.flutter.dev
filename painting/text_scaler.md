# TextScaler

```dart
abstract class TextScaler {}
```

A class that describes how textual contents should be scaled for better readability.

The [scale] function computes the scaled font size given the original unscaled font size specified by app developers.

The [==] operator defines the equality of 2 [TextScaler]s, which the framework uses to determine whether text widgets should rebuild when their [TextScaler] changes. Consider overriding the [==] operator if applicable to avoid unnecessary rebuilds.

### TextScaler()

```dart
TextScaler()
```

Creates a TextScaler.

### TextScaler.linear()

```dart
TextScaler.linear(double textScaleFactor)
```

Creates a proportional [TextScaler] that scales the incoming font size by multiplying it with the given `textScaleFactor`.

### noScaling

```dart
TextScaler noScaling
```

A [TextScaler] that doesn't scale the input font size.

This is equivalent to `TextScaler.linear(1.0)`, the [TextScaler.scale] implementation always returns the input font size as-is.

### scale()

```dart
double scale(double fontSize)
```

Computes the scaled font size (in logical pixels) with the given unscaled `fontSize` (in logical pixels).

The input `fontSize` must be finite and non-negative.

When given the same `fontSize` input, this method returns the same value. The output of a larger input `fontSize` is typically larger than that of a smaller input, but on unusual occasions they may produce the same output. For example, some platforms use single-precision floats to represent font sizes, as a result of truncation two different unscaled font sizes can be scaled to the same value.

### textScaleFactor

```dart
double get textScaleFactor
```

The estimated number of font pixels for each logical pixel. This property exists only for backward compatibility purposes, and will be removed in a future version of Flutter.

The value of this property is only an estimate, so it may not reflect the exact text scaling strategy this [TextScaler] represents, especially when this [TextScaler] is not linear. Consider using [TextScaler.scale] instead.

### clamp()

```dart
TextScaler clamp({double minScaleFactor = 0, double maxScaleFactor = double.infinity})
```

Returns a new [TextScaler] that restricts the scaled font size to within the range `[minScaleFactor * fontSize, maxScaleFactor * fontSize]`.
