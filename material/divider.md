@docImport 'color_scheme.dart'; @docImport 'drawer.dart'; @docImport 'list_tile.dart'; @docImport 'popup_menu.dart';

# Divider

```dart
class Divider extends StatelessWidget {}
```

A thin horizontal line, with padding on either side.

In the Material Design language, this represents a divider. Dividers can be used in lists, [Drawer]s, and elsewhere to separate content.

To create a divider between [ListTile] items, consider using [ListTile.divideTiles], which is optimized for this case.

{@youtube 560 315 https://www.youtube.com/watch?v=_liUC641Nmk}

The box's total height is controlled by [height]. The appropriate padding is automatically computed from the height.

{@tool dartpad} This sample shows how to display a Divider between an orange and blue box inside a column. The Divider is 20 logical pixels in height and contains a vertically centered black line that is 5 logical pixels thick. The black line is indented by 20 logical pixels.

![](https://flutter.github.io/assets-for-api-docs/assets/material/divider.png)

** See code in examples/api/lib/material/divider/divider.0.dart ** {@end-tool}

{@tool dartpad} This sample shows the creation of [Divider] widget, as described in: https://m3.material.io/components/divider/overview

** See code in examples/api/lib/material/divider/divider.1.dart ** {@end-tool}

See also:

- [PopupMenuDivider], which is the equivalent but for popup menus.
- [ListTile.divideTiles], another approach to dividing widgets in a list.
- [VerticalDivider], which is the vertical analog of this widget.
- <https://material.io/design/components/dividers.html>

### Divider()

```dart
Divider({dynamic key, double? height, double? thickness, double? indent, double? endIndent, Color? color, BorderRadiusGeometry? radius})
```

Creates a Material Design divider.

The [height], [thickness], [indent], and [endIndent] must be null or non-negative.

### height

```dart
double? height
```

The divider's height extent.

The divider itself is always drawn as a horizontal line that is centered within the height specified by this value.

If this is null, then the [DividerThemeData.space] is used. If that is also null, then this defaults to 16.0.

### thickness

```dart
double? thickness
```

The thickness of the line drawn within the divider.

{@template flutter.material.Divider.thickness} A divider with a [thickness] of 0.0 is always drawn as a line with a height of exactly one device pixel.

If this is null, then the [DividerThemeData.thickness] is used. If that is also null, then this defaults to 0.0. {@endtemplate}

### indent

```dart
double? indent
```

The amount of empty space to the leading edge of the divider.

{@template flutter.material.Divider.indent} If this is null, then the [DividerThemeData.indent] is used. If that is also null, then this defaults to 0.0. {@endtemplate}

### endIndent

```dart
double? endIndent
```

The amount of empty space to the trailing edge of the divider.

{@template flutter.material.Divider.endIndent} If this is null, then the [DividerThemeData.endIndent] is used. If that is also null, then this defaults to 0.0. {@endtemplate}

### radius

```dart
BorderRadiusGeometry? radius
```

{@template flutter.material.Divider.radius} The amount of radius for the border of the divider.

If this is null, then [DividerThemeData.radius] is used. If that is also null, then the default radius of [BoxDecoration] is used. {@endtemplate}

### color

```dart
Color? color
```

{@template flutter.material.Divider.color} The color to use when painting the line.

If this is null, then the [DividerThemeData.color] is used. If that is also null, then [ThemeData.dividerColor] is used. {@endtemplate}

{@tool snippet}

```dart
const Divider(
  color: Colors.deepOrange,
)
```

{@end-tool}

### createBorderSide()

```dart
BorderSide createBorderSide(BuildContext? context, {Color? color, double? width})
```

Computes the [BorderSide] that represents a divider.

If [color] is null, then [DividerThemeData.color] is used. If that is also null, then if [ThemeData.useMaterial3] is true then it defaults to [ThemeData.colorScheme]'s [ColorScheme.outlineVariant]. Otherwise [ThemeData.dividerColor] is used.

If [width] is null, then [DividerThemeData.thickness] is used. If that is also null, then this defaults to 0.0 (a hairline border).

If [context] is null, the default color of [BorderSide] is used and the default width of 0.0 is used.

{@tool snippet}

This example uses this method to create a box that has a divider above and below it. This is sometimes useful with lists, for instance, to separate a scrollable section from the rest of the interface.

```dart
DecoratedBox(
  decoration: BoxDecoration(
    border: Border(
      top: Divider.createBorderSide(context),
      bottom: Divider.createBorderSide(context),
    ),
  ),
  // child: ...
)
```

{@end-tool}

### build()

```dart
Widget build(BuildContext context)
```

# VerticalDivider

```dart
class VerticalDivider extends StatelessWidget {}
```

A thin vertical line, with padding on either side.

In the Material Design language, this represents a divider. Vertical dividers can be used in horizontally scrolling lists, such as a [ListView] with [ListView.scrollDirection] set to [Axis.horizontal].

The box's total width is controlled by [width]. The appropriate padding is automatically computed from the width.

{@tool dartpad} This sample shows how to display a [VerticalDivider] between a purple and orange box inside a [Row]. The [VerticalDivider] is 20 logical pixels in width and contains a horizontally centered black line that is 1 logical pixels thick. The grey line is indented by 20 logical pixels.

** See code in examples/api/lib/material/divider/vertical_divider.0.dart ** {@end-tool}

{@tool dartpad} This sample shows the creation of [VerticalDivider] widget, as described in: https://m3.material.io/components/divider/overview

** See code in examples/api/lib/material/divider/vertical_divider.1.dart ** {@end-tool}

See also:

- [ListView.separated], which can be used to generate vertical dividers.
- [Divider], which is the horizontal analog of this widget.
- <https://material.io/design/components/dividers.html>

### VerticalDivider()

```dart
VerticalDivider({dynamic key, double? width, double? thickness, double? indent, double? endIndent, Color? color, BorderRadiusGeometry? radius})
```

Creates a Material Design vertical divider.

The [width], [thickness], [indent], and [endIndent] must be null or non-negative.

### width

```dart
double? width
```

The divider's width.

The divider itself is always drawn as a vertical line that is centered within the width specified by this value.

If this is null, then the [DividerThemeData.space] is used. If that is also null, then this defaults to 16.0.

### thickness

```dart
double? thickness
```

The thickness of the line drawn within the divider.

A divider with a [thickness] of 0.0 is always drawn as a line with a width of exactly one device pixel.

If this is null, then the [DividerThemeData.thickness] is used which defaults to 0.0.

### indent

```dart
double? indent
```

The amount of empty space on top of the divider.

If this is null, then the [DividerThemeData.indent] is used. If that is also null, then this defaults to 0.0.

### endIndent

```dart
double? endIndent
```

The amount of empty space under the divider.

If this is null, then the [DividerThemeData.endIndent] is used. If that is also null, then this defaults to 0.0.

### color

```dart
Color? color
```

The color to use when painting the line.

If this is null, then the [DividerThemeData.color] is used. If that is also null, then [ThemeData.dividerColor] is used.

{@tool snippet}

```dart
const Divider(
  color: Colors.deepOrange,
)
```

{@end-tool}

### radius

```dart
BorderRadiusGeometry? radius
```

The amount of radius for the border of the divider.

If this is null, then the default radius of [BoxDecoration] will be used.

### build()

```dart
Widget build(BuildContext context)
```
