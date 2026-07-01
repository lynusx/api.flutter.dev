# OrientationWidgetBuilder

```dart
typedef OrientationWidgetBuilder = Widget Function(BuildContext context, Orientation orientation)
```

Signature for a function that builds a widget given an [Orientation].

Used by [OrientationBuilder.builder].

# OrientationBuilder

```dart
class OrientationBuilder extends StatelessWidget {}
```

Builds a widget tree that can depend on the parent widget's orientation (distinct from the device orientation).

See also:

- [LayoutBuilder], which exposes the complete constraints, not just the orientation.
- [CustomSingleChildLayout], which positions its child during layout.
- [CustomMultiChildLayout], with which you can define the precise layout of a list of children during the layout phase.
- [MediaQueryData.orientation], which exposes whether the device is in landscape or portrait mode.

### OrientationBuilder()

```dart
OrientationBuilder({dynamic key, required OrientationWidgetBuilder builder})
```

Creates an orientation builder.

### builder

```dart
OrientationWidgetBuilder builder
```

Builds the widgets below this widget given this widget's orientation.

A widget's orientation is a factor of its width relative to its height. For example, a [Column] widget will have a landscape orientation if its width exceeds its height, even though it displays its children in a vertical array.

### build()

```dart
Widget build(BuildContext context)
```

# DeviceOrientationBuilder

```dart
class DeviceOrientationBuilder extends StatelessWidget {}
```

Builds a widget tree that can depend on the device's orientation.

The orientation is obtained from [MediaQuery.orientationOf], which reflects the actual device orientation as reported by the platform. This ensures consistency with [MediaQueryData.orientation] and correct behavior on foldable devices and other scenarios where the device orientation may differ from layout dimensions.

This is different from [OrientationBuilder], which determines orientation based on the parent widget's layout constraints (width vs height), not the device's physical orientation.

{@tool snippet} This example shows how to use [DeviceOrientationBuilder] to display different widgets based on the device orientation.

```dart
DeviceOrientationBuilder(
  builder: (BuildContext context, Orientation orientation) {
    return Text(orientation == Orientation.portrait
        ? 'Device is in Portrait'
        : 'Device is in Landscape');
  },
)
```

{@end-tool}

This widget requires a [MediaQuery] ancestor to obtain the orientation. Typically, this is provided by [MaterialApp] or [WidgetsApp].

See also:

- [OrientationBuilder], which builds based on parent widget's layout constraints rather than device orientation.
- [MediaQueryData.orientation], which provides the device orientation directly from [MediaQuery].
- [LayoutBuilder], which exposes the complete layout constraints.

### DeviceOrientationBuilder()

```dart
DeviceOrientationBuilder({dynamic key, required OrientationWidgetBuilder builder})
```

Creates a device orientation builder.

### builder

```dart
OrientationWidgetBuilder builder
```

Builds the widgets below this widget given the device's orientation.

The orientation is obtained from [MediaQuery.orientationOf], which reflects the actual device orientation as reported by the platform.

### build()

```dart
Widget build(BuildContext context)
```
