@docImport 'search_anchor.dart'; @docImport 'search_bar_theme.dart';

# SearchViewThemeData

```dart
class SearchViewThemeData with Diagnosticable {}
```

Defines the configuration of the search views created by the [SearchAnchor] widget.

Descendant widgets obtain the current [SearchViewThemeData] object using [SearchViewTheme.of].

Typically, a [SearchViewThemeData] is specified as part of the overall [Theme] with [ThemeData.searchViewTheme]. Otherwise, [SearchViewTheme] can be used to configure its own widget subtree.

All [SearchViewThemeData] properties are `null` by default. If any of these properties are null, the search view will provide its own defaults.

See also:

- [ThemeData], which describes the overall theme for the application.
- [SearchBarThemeData], which describes the theme for the search bar itself in a [SearchBar] widget.
- [SearchAnchor], which is used to open a search view route.

### SearchViewThemeData()

```dart
SearchViewThemeData({Color? backgroundColor, double? elevation, Color? surfaceTintColor, BoxConstraints? constraints, EdgeInsetsGeometry? padding, EdgeInsetsGeometry? barPadding, bool? shrinkWrap, BorderSide? side, OutlinedBorder? shape, double? headerHeight, TextStyle? headerTextStyle, TextStyle? headerHintStyle, Color? dividerColor})
```

Creates a theme that can be used for [ThemeData.searchViewTheme].

### backgroundColor

```dart
Color? backgroundColor
```

Overrides the default value of the [SearchAnchor.viewBackgroundColor].

### elevation

```dart
double? elevation
```

Overrides the default value of the [SearchAnchor.viewElevation].

### surfaceTintColor

```dart
Color? surfaceTintColor
```

Overrides the default value of the [SearchAnchor.viewSurfaceTintColor].

### side

```dart
BorderSide? side
```

Overrides the default value of the [SearchAnchor.viewSide].

### shape

```dart
OutlinedBorder? shape
```

Overrides the default value of the [SearchAnchor.viewShape].

### headerHeight

```dart
double? headerHeight
```

Overrides the default value of the [SearchAnchor.headerHeight].

### headerTextStyle

```dart
TextStyle? headerTextStyle
```

Overrides the default value for [SearchAnchor.headerTextStyle].

### headerHintStyle

```dart
TextStyle? headerHintStyle
```

Overrides the default value for [SearchAnchor.headerHintStyle].

### constraints

```dart
BoxConstraints? constraints
```

Overrides the value of size constraints for [SearchAnchor.viewConstraints].

### padding

```dart
EdgeInsetsGeometry? padding
```

Overrides the value of the padding for [SearchAnchor.viewPadding].

### barPadding

```dart
EdgeInsetsGeometry? barPadding
```

Overrides the value of the padding for [SearchAnchor.viewBarPadding]

### shrinkWrap

```dart
bool? shrinkWrap
```

Overrides the value of the shrink wrap for [SearchAnchor.shrinkWrap].

### dividerColor

```dart
Color? dividerColor
```

Overrides the value of the divider color for [SearchAnchor.dividerColor].

### copyWith()

```dart
SearchViewThemeData copyWith({Color? backgroundColor, double? elevation, Color? surfaceTintColor, BorderSide? side, OutlinedBorder? shape, double? headerHeight, TextStyle? headerTextStyle, TextStyle? headerHintStyle, BoxConstraints? constraints, EdgeInsetsGeometry? padding, EdgeInsetsGeometry? barPadding, bool? shrinkWrap, Color? dividerColor})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
SearchViewThemeData? lerp(SearchViewThemeData? a, SearchViewThemeData? b, double t)
```

Linearly interpolate between two [SearchViewThemeData]s.

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

# SearchViewTheme

```dart
class SearchViewTheme extends InheritedTheme {}
```

An inherited widget that defines the configuration in this widget's descendants for search view created by the [SearchAnchor] widget.

A search view theme can be specified as part of the overall Material theme using [ThemeData.searchViewTheme].

See also:

- [SearchViewThemeData], which describes the actual configuration of a search view theme.

### SearchViewTheme()

```dart
SearchViewTheme({dynamic key, required SearchViewThemeData data, required dynamic child})
```

Creates a const theme that controls the configurations for the search view created by the [SearchAnchor] widget.

### data

```dart
SearchViewThemeData data
```

The properties used for all descendant [SearchAnchor] widgets.

### of()

```dart
SearchViewThemeData of(BuildContext context)
```

Returns the configuration [data] from the closest [SearchViewTheme] ancestor. If there is no ancestor, it returns [ThemeData.searchViewTheme].

Typical usage is as follows:

```dart
SearchViewThemeData theme = SearchViewTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(SearchViewTheme oldWidget)
```
