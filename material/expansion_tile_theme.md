@docImport 'expansion_tile.dart';

# ExpansionTileThemeData

```dart
class ExpansionTileThemeData with Diagnosticable {}
```

Used with [ExpansionTileTheme] to define default property values for descendant [ExpansionTile] widgets.

Descendant widgets obtain the current [ExpansionTileThemeData] object using [ExpansionTileTheme.of]. Instances of [ExpansionTileThemeData] can be customized with [ExpansionTileThemeData.copyWith].

A [ExpansionTileThemeData] is often specified as part of the overall [Theme] with [ThemeData.expansionTileTheme].

All [ExpansionTileThemeData] properties are `null` by default. When a theme property is null, the [ExpansionTile] will provide its own default based on the overall [Theme]'s textTheme and colorScheme. See the individual [ExpansionTile] properties for details.

See also:

- [ThemeData], which describes the overall theme information for the application.
- [ExpansionTileTheme] which overrides the default [ExpansionTileTheme] of its [ExpansionTile] descendants.
- [ThemeData.textTheme], text with a color that contrasts with the card and canvas colors.
- [ThemeData.colorScheme], the thirteen colors that most Material widget default colors are based on.

### ExpansionTileThemeData()

```dart
ExpansionTileThemeData({Color? backgroundColor, Color? collapsedBackgroundColor, EdgeInsetsGeometry? tilePadding, AlignmentGeometry? expandedAlignment, EdgeInsetsGeometry? childrenPadding, Color? iconColor, Color? collapsedIconColor, Color? textColor, Color? collapsedTextColor, ShapeBorder? shape, ShapeBorder? collapsedShape, Clip? clipBehavior, AnimationStyle? expansionAnimationStyle})
```

Creates a [ExpansionTileThemeData].

### backgroundColor

```dart
Color? backgroundColor
```

Overrides the default value of [ExpansionTile.backgroundColor].

### collapsedBackgroundColor

```dart
Color? collapsedBackgroundColor
```

Overrides the default value of [ExpansionTile.collapsedBackgroundColor].

### tilePadding

```dart
EdgeInsetsGeometry? tilePadding
```

Overrides the default value of [ExpansionTile.tilePadding].

### expandedAlignment

```dart
AlignmentGeometry? expandedAlignment
```

Overrides the default value of [ExpansionTile.expandedAlignment].

### childrenPadding

```dart
EdgeInsetsGeometry? childrenPadding
```

Overrides the default value of [ExpansionTile.childrenPadding].

### iconColor

```dart
Color? iconColor
```

Overrides the default value of [ExpansionTile.iconColor].

### collapsedIconColor

```dart
Color? collapsedIconColor
```

Overrides the default value of [ExpansionTile.collapsedIconColor].

### textColor

```dart
Color? textColor
```

Overrides the default value of [ExpansionTile.textColor].

### collapsedTextColor

```dart
Color? collapsedTextColor
```

Overrides the default value of [ExpansionTile.collapsedTextColor].

### shape

```dart
ShapeBorder? shape
```

Overrides the default value of [ExpansionTile.shape].

### collapsedShape

```dart
ShapeBorder? collapsedShape
```

Overrides the default value of [ExpansionTile.collapsedShape].

### clipBehavior

```dart
Clip? clipBehavior
```

Overrides the default value of [ExpansionTile.clipBehavior].

### expansionAnimationStyle

```dart
AnimationStyle? expansionAnimationStyle
```

Overrides the default value of [ExpansionTile.expansionAnimationStyle].

### copyWith()

```dart
ExpansionTileThemeData copyWith({Color? backgroundColor, Color? collapsedBackgroundColor, EdgeInsetsGeometry? tilePadding, AlignmentGeometry? expandedAlignment, EdgeInsetsGeometry? childrenPadding, Color? iconColor, Color? collapsedIconColor, Color? textColor, Color? collapsedTextColor, ShapeBorder? shape, ShapeBorder? collapsedShape, Clip? clipBehavior, AnimationStyle? expansionAnimationStyle})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
ExpansionTileThemeData? lerp(ExpansionTileThemeData? a, ExpansionTileThemeData? b, double t)
```

Linearly interpolate between ExpansionTileThemeData objects.

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

# ExpansionTileTheme

```dart
class ExpansionTileTheme extends InheritedTheme {}
```

Overrides the default [ExpansionTileTheme] of its [ExpansionTile] descendants.

See also:

- [ExpansionTileThemeData], which is used to configure this theme.
- [ThemeData.expansionTileTheme], which can be used to override the default [ExpansionTileTheme] for [ExpansionTile]s below the overall [Theme].

### ExpansionTileTheme()

```dart
ExpansionTileTheme({dynamic key, required ExpansionTileThemeData data, required dynamic child})
```

Applies the given theme [data] to [child].

### data

```dart
ExpansionTileThemeData data
```

Specifies color, alignment, and text style values for descendant [ExpansionTile] widgets.

### of()

```dart
ExpansionTileThemeData of(BuildContext context)
```

Retrieves the [ExpansionTileThemeData] from the closest ancestor [ExpansionTileTheme].

If there is no enclosing [ExpansionTileTheme] widget, then [ThemeData.expansionTileTheme] is used.

Typical usage is as follows:

```dart
ExpansionTileThemeData theme = ExpansionTileTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(ExpansionTileTheme oldWidget)
```
