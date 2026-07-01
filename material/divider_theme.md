@docImport 'data_table.dart'; @docImport 'divider.dart'; @docImport 'list_tile.dart';

# DividerThemeData

```dart
class DividerThemeData with Diagnosticable {}
```

Defines the visual properties of [Divider], [VerticalDivider], dividers between [ListTile]s, and dividers between rows in [DataTable]s.

Descendant widgets obtain the current [DividerThemeData] object using [DividerTheme.of]. Instances of [DividerThemeData] can be customized with [DividerThemeData.copyWith].

Typically a [DividerThemeData] is specified as part of the overall [Theme] with [ThemeData.dividerTheme].

All [DividerThemeData] properties are `null` by default. When null, the widgets will provide their own defaults.

See also:

- [ThemeData], which describes the overall theme information for the application.

### DividerThemeData()

```dart
DividerThemeData({Color? color, double? space, double? thickness, double? indent, double? endIndent, BorderRadiusGeometry? radius})
```

Creates a theme that can be used for [DividerTheme] or [ThemeData.dividerTheme].

### color

```dart
Color? color
```

The color of [Divider]s and [VerticalDivider]s, also used between [ListTile]s, between rows in [DataTable]s, and so forth.

### space

```dart
double? space
```

The [Divider]'s height or the [VerticalDivider]'s width.

This represents the amount of horizontal or vertical space the divider takes up.

### thickness

```dart
double? thickness
```

The thickness of the line drawn within the divider.

### indent

```dart
double? indent
```

The amount of empty space at the leading edge of [Divider] or top edge of [VerticalDivider].

### endIndent

```dart
double? endIndent
```

The amount of empty space at the trailing edge of [Divider] or bottom edge of [VerticalDivider].

### radius

```dart
BorderRadiusGeometry? radius
```

The border radius applied to the [Divider] or [VerticalDivider].

If non-null, this radius will be used to round the corners of the divider.

### copyWith()

```dart
DividerThemeData copyWith({Color? color, double? space, double? thickness, double? indent, double? endIndent, BorderRadiusGeometry? radius})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
DividerThemeData lerp(DividerThemeData? a, DividerThemeData? b, double t)
```

Linearly interpolate between two Divider themes.

{@macro dart.ui.shadow.lerp}

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# DividerTheme

```dart
class DividerTheme extends InheritedTheme {}
```

An inherited widget that defines the configuration for [Divider]s, [VerticalDivider]s, dividers between [ListTile]s, and dividers between rows in [DataTable]s in this widget's subtree.

### DividerTheme()

```dart
DividerTheme({dynamic key, required DividerThemeData data, required dynamic child})
```

Creates a divider theme that controls the configurations for [Divider]s, [VerticalDivider]s, dividers between [ListTile]s, and dividers between rows in [DataTable]s in its widget subtree.

### data

```dart
DividerThemeData data
```

The properties for descendant [Divider]s, [VerticalDivider]s, dividers between [ListTile]s, and dividers between rows in [DataTable]s.

### of()

```dart
DividerThemeData of(BuildContext context)
```

The closest instance of this class's [data] value that encloses the given context.

If there is no ancestor, it returns [ThemeData.dividerTheme]. Applications can assume that the returned value will not be null.

Typical usage is as follows:

```dart
DividerThemeData theme = DividerTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(DividerTheme oldWidget)
```
