@docImport 'segmented_button.dart';

# SegmentedButtonThemeData

```dart
class SegmentedButtonThemeData with Diagnosticable {}
```

Overrides the default values of visual properties for descendant [SegmentedButton] widgets.

Descendant widgets obtain the current [SegmentedButtonThemeData] object with [SegmentedButtonTheme.of]. Instances of [SegmentedButtonThemeData] can be customized with [SegmentedButtonThemeData.copyWith].

Typically a [SegmentedButtonThemeData] is specified as part of the overall [Theme] with [ThemeData.segmentedButtonTheme].

All [SegmentedButtonThemeData] properties are null by default. When null, the [SegmentedButton] computes its own default values, typically based on the overall theme's [ThemeData.colorScheme], [ThemeData.textTheme], and [ThemeData.iconTheme].

### SegmentedButtonThemeData()

```dart
SegmentedButtonThemeData({ButtonStyle? style, Widget? selectedIcon})
```

Creates a [SegmentedButtonThemeData] that can be used to override default properties in a [SegmentedButtonTheme] widget.

### style

```dart
ButtonStyle? style
```

Overrides the [SegmentedButton]'s default style.

Non-null properties or non-null resolved [WidgetStateProperty] values override the default values used by [SegmentedButton].

If [style] is null, then this theme doesn't override anything.

If [ButtonStyle.side] is provided, [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.focused].
- [WidgetState.hovered].
- [WidgetState.disabled].
- [WidgetState.selected].

### selectedIcon

```dart
Widget? selectedIcon
```

Override for [SegmentedButton.selectedIcon] property.

If non-null, then [selectedIcon] will be used instead of default value for [SegmentedButton.selectedIcon].

### copyWith()

```dart
SegmentedButtonThemeData copyWith({ButtonStyle? style, Widget? selectedIcon})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
SegmentedButtonThemeData lerp(SegmentedButtonThemeData? a, SegmentedButtonThemeData? b, double t)
```

Linearly interpolates between two segmented button themes.

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

# SegmentedButtonTheme

```dart
class SegmentedButtonTheme extends InheritedTheme {}
```

An inherited widget that defines the visual properties for [SegmentedButton]s in this widget's subtree.

Values specified here are used for [SegmentedButton] properties that are not given an explicit non-null value.

### SegmentedButtonTheme()

```dart
SegmentedButtonTheme({dynamic key, required SegmentedButtonThemeData data, required dynamic child})
```

Creates a [SegmentedButtonTheme] that controls visual parameters for descendent [SegmentedButton]s.

### data

```dart
SegmentedButtonThemeData data
```

Specifies the visual properties used by descendant [SegmentedButton] widgets.

### of()

```dart
SegmentedButtonThemeData of(BuildContext context)
```

The [data] from the closest instance of this class that encloses the given context.

If there is no [SegmentedButtonTheme] in scope, this will return [ThemeData.segmentedButtonTheme] from the ambient [Theme].

Typical usage is as follows:

```dart
SegmentedButtonThemeData theme = SegmentedButtonTheme.of(context);
```

See also:

- [maybeOf], which returns null if it doesn't find a [SegmentedButtonTheme] ancestor.

### maybeOf()

```dart
SegmentedButtonThemeData? maybeOf(BuildContext context)
```

The data from the closest instance of this class that encloses the given context, if any.

Use this function if you want to allow situations where no [SegmentedButtonTheme] is in scope. Prefer using [SegmentedButtonTheme.of] in situations where a [SegmentedButtonThemeData] is expected to be non-null.

If there is no [SegmentedButtonTheme] in scope, then this function will return null.

Typical usage is as follows:

```dart
SegmentedButtonThemeData? theme = SegmentedButtonTheme.maybeOf(context);
if (theme == null) {
  // Do something else instead.
}
```

See also:

- [of], which will return [ThemeData.segmentedButtonTheme] if it doesn't find a [SegmentedButtonTheme] ancestor, instead of returning null.

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(SegmentedButtonTheme oldWidget)
```
