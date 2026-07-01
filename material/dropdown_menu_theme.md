@docImport 'dropdown_menu.dart'; @docImport 'text_field.dart';

# DropdownMenuThemeData

```dart
class DropdownMenuThemeData with Diagnosticable {}
```

Overrides the default values of visual properties for descendant [DropdownMenu] widgets.

Descendant widgets obtain the current [DropdownMenuThemeData] object with [DropdownMenuTheme.of]. Instances of [DropdownMenuThemeData] can be customized with [DropdownMenuThemeData.copyWith].

Typically a [DropdownMenuTheme] is specified as part of the overall [Theme] with [ThemeData.dropdownMenuTheme].

All [DropdownMenuThemeData] properties are null by default. When null, the [DropdownMenu] computes its own default values, typically based on the overall theme's [ThemeData.colorScheme], [ThemeData.textTheme], and [ThemeData.iconTheme].

### DropdownMenuThemeData()

```dart
DropdownMenuThemeData({TextStyle? textStyle, Object? inputDecorationTheme, MenuStyle? menuStyle, Color? disabledColor})
```

Creates a [DropdownMenuThemeData] that can be used to override default properties in a [DropdownMenuTheme] widget.

### textStyle

```dart
TextStyle? textStyle
```

Overrides the default value for [DropdownMenu.textStyle].

### inputDecorationTheme

```dart
InputDecorationThemeData? get inputDecorationTheme
```

The input decoration theme for the [TextField]s in a [DropdownMenu].

If this is null, the [DropdownMenu] provides its own defaults.

### menuStyle

```dart
MenuStyle? menuStyle
```

Overrides the menu's default style in a [DropdownMenu].

Any values not set in the [MenuStyle] will use the menu default for that property.

### disabledColor

```dart
Color? disabledColor
```

The color used for disabled DropdownMenu. This color is applied to the text of the selected item on TextField.

### copyWith()

```dart
DropdownMenuThemeData copyWith({TextStyle? textStyle, Object? inputDecorationTheme, MenuStyle? menuStyle, Color? disabledColor})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
DropdownMenuThemeData lerp(DropdownMenuThemeData? a, DropdownMenuThemeData? b, double t)
```

Linearly interpolates between two dropdown menu themes.

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

# DropdownMenuTheme

```dart
class DropdownMenuTheme extends InheritedTheme {}
```

An inherited widget that defines the visual properties for [DropdownMenu]s in this widget's subtree.

Values specified here are used for [DropdownMenu] properties that are not given an explicit non-null value.

### DropdownMenuTheme()

```dart
DropdownMenuTheme({dynamic key, required DropdownMenuThemeData data, required dynamic child})
```

Creates a [DropdownMenuTheme] that controls visual parameters for descendant [DropdownMenu]s.

### data

```dart
DropdownMenuThemeData data
```

Specifies the visual properties used by descendant [DropdownMenu] widgets.

### of()

```dart
DropdownMenuThemeData of(BuildContext context)
```

Retrieves the [DropdownMenuThemeData] from the closest ancestor [DropdownMenuTheme].

If there is no enclosing [DropdownMenuTheme] widget, then [ThemeData.dropdownMenuTheme] is used.

Typical usage is as follows:

```dart
DropdownMenuThemeData theme = DropdownMenuTheme.of(context);
```

See also:

- [maybeOf], which returns null if it doesn't find a [DropdownMenuTheme] ancestor.

### maybeOf()

```dart
DropdownMenuThemeData? maybeOf(BuildContext context)
```

The data from the closest instance of this class that encloses the given context, if any.

Use this function if you want to allow situations where no [DropdownMenuTheme] is in scope. Prefer using [DropdownMenuTheme.of] in situations where a [DropdownMenuThemeData] is expected to be non-null.

If there is no [DropdownMenuTheme] in scope, then this function will return null.

Typical usage is as follows:

```dart
DropdownMenuThemeData? theme = DropdownMenuTheme.maybeOf(context);
if (theme == null) {
  // Do something else instead.
}
```

See also:

- [of], which will return [ThemeData.dropdownMenuTheme] if it doesn't find a [DropdownMenuTheme] ancestor, instead of returning null.

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(DropdownMenuTheme oldWidget)
```
