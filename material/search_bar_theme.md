@docImport 'search_anchor.dart';

# SearchBarThemeData

```dart
class SearchBarThemeData with Diagnosticable {}
```

Defines default property values for descendant [SearchBar] widgets.

Descendant widgets obtain the current [SearchBarThemeData] object using [SearchBarTheme.of]. Instances of [SearchBarThemeData] can be customized with [SearchBarThemeData.copyWith].

Typically a [SearchBarThemeData] is specified as part of the overall [Theme] with [ThemeData.searchBarTheme].

All [SearchBarThemeData] properties are `null` by default. When null, the [SearchBar] will use the values from [ThemeData] if they exist, otherwise it will provide its own defaults based on the overall [Theme]'s colorScheme. See the individual [SearchBar] properties for details.

See also:

- [ThemeData], which describes the overall theme information for the application.

### SearchBarThemeData()

```dart
SearchBarThemeData({WidgetStateProperty<double?>? elevation, WidgetStateProperty<Color?>? backgroundColor, WidgetStateProperty<Color?>? shadowColor, WidgetStateProperty<Color?>? surfaceTintColor, WidgetStateProperty<Color?>? overlayColor, WidgetStateProperty<BorderSide?>? side, WidgetStateProperty<OutlinedBorder?>? shape, WidgetStateProperty<EdgeInsetsGeometry?>? padding, WidgetStateProperty<TextStyle?>? textStyle, WidgetStateProperty<TextStyle?>? hintStyle, BoxConstraints? constraints, TextCapitalization? textCapitalization})
```

Creates a theme that can be used for [ThemeData.searchBarTheme].

### elevation

```dart
WidgetStateProperty<double?>? elevation
```

Overrides the default value of the [SearchBar.elevation].

### backgroundColor

```dart
WidgetStateProperty<Color?>? backgroundColor
```

Overrides the default value of the [SearchBar.backgroundColor].

### shadowColor

```dart
WidgetStateProperty<Color?>? shadowColor
```

Overrides the default value of the [SearchBar.shadowColor].

### surfaceTintColor

```dart
WidgetStateProperty<Color?>? surfaceTintColor
```

Overrides the default value of the [SearchBar.surfaceTintColor].

### overlayColor

```dart
WidgetStateProperty<Color?>? overlayColor
```

Overrides the default value of the [SearchBar.overlayColor].

### side

```dart
WidgetStateProperty<BorderSide?>? side
```

Overrides the default value of the [SearchBar.side].

### shape

```dart
WidgetStateProperty<OutlinedBorder?>? shape
```

Overrides the default value of the [SearchBar.shape].

### padding

```dart
WidgetStateProperty<EdgeInsetsGeometry?>? padding
```

Overrides the default value for [SearchBar.padding].

### textStyle

```dart
WidgetStateProperty<TextStyle?>? textStyle
```

Overrides the default value for [SearchBar.textStyle].

### hintStyle

```dart
WidgetStateProperty<TextStyle?>? hintStyle
```

Overrides the default value for [SearchBar.hintStyle].

### constraints

```dart
BoxConstraints? constraints
```

Overrides the value of size constraints for [SearchBar].

### textCapitalization

```dart
TextCapitalization? textCapitalization
```

Overrides the value of [SearchBar.textCapitalization].

### copyWith()

```dart
SearchBarThemeData copyWith({WidgetStateProperty<double?>? elevation, WidgetStateProperty<Color?>? backgroundColor, WidgetStateProperty<Color?>? shadowColor, WidgetStateProperty<Color?>? surfaceTintColor, WidgetStateProperty<Color?>? overlayColor, WidgetStateProperty<BorderSide?>? side, WidgetStateProperty<OutlinedBorder?>? shape, WidgetStateProperty<EdgeInsetsGeometry?>? padding, WidgetStateProperty<TextStyle?>? textStyle, WidgetStateProperty<TextStyle?>? hintStyle, BoxConstraints? constraints, TextCapitalization? textCapitalization})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
SearchBarThemeData? lerp(SearchBarThemeData? a, SearchBarThemeData? b, double t)
```

Linearly interpolate between two [SearchBarThemeData]s.

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

# SearchBarTheme

```dart
class SearchBarTheme extends InheritedWidget {}
```

Applies a search bar theme to descendant [SearchBar] widgets.

Descendant widgets obtain the current theme's [SearchBarTheme] object using [SearchBarTheme.of]. When a widget uses [SearchBarTheme.of], it is automatically rebuilt if the theme later changes.

A search bar theme can be specified as part of the overall Material theme using [ThemeData.searchBarTheme].

See also:

- [SearchBarThemeData], which describes the actual configuration of a search bar theme.

### SearchBarTheme()

```dart
SearchBarTheme({dynamic key, required SearchBarThemeData data, required dynamic child})
```

Constructs a search bar theme that configures all descendant [SearchBar] widgets.

### data

```dart
SearchBarThemeData data
```

The properties used for all descendant [SearchBar] widgets.

### of()

```dart
SearchBarThemeData of(BuildContext context)
```

Returns the configuration [data] from the closest [SearchBarTheme] ancestor. If there is no ancestor, it returns [ThemeData.searchBarTheme].

Typical usage is as follows:

```dart
SearchBarThemeData theme = SearchBarTheme.of(context);
```

### updateShouldNotify()

```dart
bool updateShouldNotify(SearchBarTheme oldWidget)
```
