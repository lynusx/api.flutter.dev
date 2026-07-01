@docImport 'package:flutter/widgets.dart';

@docImport 'material.dart';

# kElevationToShadow

```dart
Map<int, List<BoxShadow>> kElevationToShadow
```

Map of elevation offsets used by Material Design to [BoxShadow] definitions.

The following elevations have defined shadows: 1, 2, 3, 4, 6, 8, 9, 12, 16, 24.

Each entry has three shadows which must be combined to obtain the defined effect for that elevation.

This is useful when simulating a shadow with a [BoxDecoration] or other class that uses a list of [BoxShadow] objects.

Shadows defined by [kElevationToShadow] use [BlurStyle.normal]. To convert a shadow from [kElevationToShadow] to use a different [BlurStyle] (e.g. to use it in a [MagnifierDecoration]), consider an expression such as the following:

```dart
kElevationToShadow[12]!.map((BoxShadow shadow) => shadow.copyWith(blurStyle: BlurStyle.outer)).toList(),
```

See also:

- [Material], which takes an arbitrary double for its elevation and generates a shadow dynamically.
- <https://material.io/design/environment/elevation.html>
