@docImport 'checkbox_list_tile.dart'; @docImport 'drawer.dart'; @docImport 'expansion_tile.dart'; @docImport 'radio_list_tile.dart'; @docImport 'switch_list_tile.dart';

# ListTileThemeData

```dart
class ListTileThemeData with Diagnosticable {}
```

Used with [ListTileTheme] to define default property values for descendant [ListTile] widgets, as well as classes that build [ListTile]s, like [CheckboxListTile], [RadioListTile], and [SwitchListTile].

Descendant widgets obtain the current [ListTileThemeData] object using [ListTileTheme.of]. Instances of [ListTileThemeData] can be customized with [ListTileThemeData.copyWith].

A [ListTileThemeData] is often specified as part of the overall [Theme] with [ThemeData.listTileTheme].

All [ListTileThemeData] properties are `null` by default. When a theme property is null, the [ListTile] will provide its own default based on the overall [Theme]'s textTheme and colorScheme. See the individual [ListTile] properties for details.

The [Drawer] widget specifies a list tile theme for its children that defines [style] to be [ListTileStyle.drawer].

See also:

- [ThemeData], which describes the overall theme information for the application.

### ListTileThemeData()

```dart
ListTileThemeData({bool? dense, ShapeBorder? shape, ListTileStyle? style, Color? selectedColor, Color? iconColor, Color? textColor, TextStyle? titleTextStyle, TextStyle? subtitleTextStyle, TextStyle? leadingAndTrailingTextStyle, EdgeInsetsGeometry? contentPadding, Color? tileColor, Color? selectedTileColor, double? horizontalTitleGap, double? minVerticalPadding, double? minLeadingWidth, bool? enableFeedback, WidgetStateProperty<MouseCursor?>? mouseCursor, VisualDensity? visualDensity, double? minTileHeight, ListTileTitleAlignment? titleAlignment, ListTileControlAffinity? controlAffinity, bool? isThreeLine})
```

Creates a [ListTileThemeData].

### dense

```dart
bool? dense
```

Overrides the default value of [ListTile.dense].

### shape

```dart
ShapeBorder? shape
```

Overrides the default value of [ListTile.shape].

### style

```dart
ListTileStyle? style
```

Overrides the default value of [ListTile.style].

### selectedColor

```dart
Color? selectedColor
```

Overrides the default value of [ListTile.selectedColor].

### iconColor

```dart
Color? iconColor
```

Overrides the default value of [ListTile.iconColor].

### textColor

```dart
Color? textColor
```

Overrides the default value of [ListTile.textColor].

### titleTextStyle

```dart
TextStyle? titleTextStyle
```

Overrides the default value of [ListTile.titleTextStyle].

### subtitleTextStyle

```dart
TextStyle? subtitleTextStyle
```

Overrides the default value of [ListTile.subtitleTextStyle].

### leadingAndTrailingTextStyle

```dart
TextStyle? leadingAndTrailingTextStyle
```

Overrides the default value of [ListTile.leadingAndTrailingTextStyle].

### contentPadding

```dart
EdgeInsetsGeometry? contentPadding
```

Overrides the default value of [ListTile.contentPadding].

### tileColor

```dart
Color? tileColor
```

Overrides the default value of [ListTile.tileColor].

### selectedTileColor

```dart
Color? selectedTileColor
```

Overrides the default value of [ListTile.selectedTileColor].

### horizontalTitleGap

```dart
double? horizontalTitleGap
```

Overrides the default value of [ListTile.horizontalTitleGap].

### minVerticalPadding

```dart
double? minVerticalPadding
```

Overrides the default value of [ListTile.minVerticalPadding].

### minLeadingWidth

```dart
double? minLeadingWidth
```

Overrides the default value of [ListTile.minLeadingWidth].

### minTileHeight

```dart
double? minTileHeight
```

Overrides the default value of [ListTile.minTileHeight].

### enableFeedback

```dart
bool? enableFeedback
```

Overrides the default value of [ListTile.enableFeedback].

### mouseCursor

```dart
WidgetStateProperty<MouseCursor?>? mouseCursor
```

If specified, overrides the default value of [ListTile.mouseCursor].

### visualDensity

```dart
VisualDensity? visualDensity
```

If specified, overrides the default value of [ListTile.visualDensity].

### titleAlignment

```dart
ListTileTitleAlignment? titleAlignment
```

If specified, overrides the default value of [ListTile.titleAlignment].

### controlAffinity

```dart
ListTileControlAffinity? controlAffinity
```

If specified, overrides the default value of [CheckboxListTile.controlAffinity] or [ExpansionTile.controlAffinity] or [SwitchListTile.controlAffinity] or [RadioListTile.controlAffinity].

### isThreeLine

```dart
bool? isThreeLine
```

If specified, overrides the default value of [ListTile.isThreeLine] or [CheckboxListTile.isThreeLine] or [RadioListTile.isThreeLine] or [SwitchListTile.isThreeLine].

### copyWith()

```dart
ListTileThemeData copyWith({bool? dense, ShapeBorder? shape, ListTileStyle? style, Color? selectedColor, Color? iconColor, Color? textColor, TextStyle? titleTextStyle, TextStyle? subtitleTextStyle, TextStyle? leadingAndTrailingTextStyle, EdgeInsetsGeometry? contentPadding, Color? tileColor, Color? selectedTileColor, double? horizontalTitleGap, double? minVerticalPadding, double? minLeadingWidth, double? minTileHeight, bool? enableFeedback, WidgetStateProperty<MouseCursor?>? mouseCursor, bool? isThreeLine, VisualDensity? visualDensity, ListTileTitleAlignment? titleAlignment, ListTileControlAffinity? controlAffinity})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
ListTileThemeData? lerp(ListTileThemeData? a, ListTileThemeData? b, double t)
```

Linearly interpolate between ListTileThemeData objects.

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

# ListTileTheme

```dart
class ListTileTheme extends InheritedTheme {}
```

An inherited widget that defines color and style parameters for [ListTile]s in this widget's subtree.

Values specified here are used for [ListTile] properties that are not given an explicit non-null value.

The [Drawer] widget specifies a tile theme for its children which sets [style] to [ListTileStyle.drawer].

### ListTileTheme()

```dart
ListTileTheme({dynamic key, ListTileThemeData? data, bool? dense, ShapeBorder? shape, ListTileStyle? style, Color? selectedColor, Color? iconColor, Color? textColor, EdgeInsetsGeometry? contentPadding, Color? tileColor, Color? selectedTileColor, bool? enableFeedback, WidgetStateProperty<MouseCursor?>? mouseCursor, double? horizontalTitleGap, double? minVerticalPadding, double? minLeadingWidth, ListTileControlAffinity? controlAffinity, required dynamic child})
```

Creates a list tile theme that defines the color and style parameters for descendant [ListTile]s.

Only the [data] parameter should be used. The other parameters are redundant (are now obsolete) and will be deprecated in a future update.

### data

```dart
ListTileThemeData get data
```

The configuration of this theme.

### dense

```dart
bool? get dense
```

Overrides the default value of [ListTile.dense].

This property is obsolete: please use the [data] [ListTileThemeData.dense] property instead.

### shape

```dart
ShapeBorder? get shape
```

Overrides the default value of [ListTile.shape].

This property is obsolete: please use the [data] [ListTileThemeData.shape] property instead.

### style

```dart
ListTileStyle? get style
```

Overrides the default value of [ListTile.style].

This property is obsolete: please use the [data] [ListTileThemeData.style] property instead.

### selectedColor

```dart
Color? get selectedColor
```

Overrides the default value of [ListTile.selectedColor].

This property is obsolete: please use the [data] [ListTileThemeData.selectedColor] property instead.

### iconColor

```dart
Color? get iconColor
```

Overrides the default value of [ListTile.iconColor].

This property is obsolete: please use the [data] [ListTileThemeData.iconColor] property instead.

### textColor

```dart
Color? get textColor
```

Overrides the default value of [ListTile.textColor].

This property is obsolete: please use the [data] [ListTileThemeData.textColor] property instead.

### contentPadding

```dart
EdgeInsetsGeometry? get contentPadding
```

Overrides the default value of [ListTile.contentPadding].

This property is obsolete: please use the [data] [ListTileThemeData.contentPadding] property instead.

### tileColor

```dart
Color? get tileColor
```

Overrides the default value of [ListTile.tileColor].

This property is obsolete: please use the [data] [ListTileThemeData.tileColor] property instead.

### selectedTileColor

```dart
Color? get selectedTileColor
```

Overrides the default value of [ListTile.selectedTileColor].

This property is obsolete: please use the [data] [ListTileThemeData.selectedTileColor] property instead.

### horizontalTitleGap

```dart
double? get horizontalTitleGap
```

Overrides the default value of [ListTile.horizontalTitleGap].

This property is obsolete: please use the [data] [ListTileThemeData.horizontalTitleGap] property instead.

### minVerticalPadding

```dart
double? get minVerticalPadding
```

Overrides the default value of [ListTile.minVerticalPadding].

This property is obsolete: please use the [data] [ListTileThemeData.minVerticalPadding] property instead.

### minLeadingWidth

```dart
double? get minLeadingWidth
```

Overrides the default value of [ListTile.minLeadingWidth].

This property is obsolete: please use the [data] [ListTileThemeData.minLeadingWidth] property instead.

### enableFeedback

```dart
bool? get enableFeedback
```

Overrides the default value of [ListTile.enableFeedback].

This property is obsolete: please use the [data] [ListTileThemeData.enableFeedback] property instead.

### controlAffinity

```dart
ListTileControlAffinity? get controlAffinity
```

Overrides the default value of [CheckboxListTile.controlAffinity] or [ExpansionTile.controlAffinity] or [SwitchListTile.controlAffinity] or [RadioListTile.controlAffinity]

This property is obsolete: please use the [ListTileThemeData.controlAffinity] property instead.

### of()

```dart
ListTileThemeData of(BuildContext context)
```

The [data] property of the closest instance of this class that encloses the given context.

If there is no enclosing [ListTileTheme] widget, then [ThemeData.listTileTheme] is used (see [Theme.of]).

Typical usage is as follows:

```dart
ListTileThemeData theme = ListTileTheme.of(context);
```

### merge()

```dart
Widget merge({Key? key, bool? dense, ShapeBorder? shape, ListTileStyle? style, Color? selectedColor, Color? iconColor, Color? textColor, TextStyle? titleTextStyle, TextStyle? subtitleTextStyle, TextStyle? leadingAndTrailingTextStyle, EdgeInsetsGeometry? contentPadding, Color? tileColor, Color? selectedTileColor, bool? enableFeedback, double? horizontalTitleGap, double? minVerticalPadding, double? minLeadingWidth, double? minTileHeight, ListTileTitleAlignment? titleAlignment, WidgetStateProperty<MouseCursor?>? mouseCursor, VisualDensity? visualDensity, ListTileControlAffinity? controlAffinity, bool? isThreeLine, required Widget child})
```

Creates a list tile theme that controls the color and style parameters for [ListTile]s, and merges in the current list tile theme, if any.

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(ListTileTheme oldWidget)
```
