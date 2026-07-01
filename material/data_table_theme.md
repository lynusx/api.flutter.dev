@docImport 'data_table.dart';

# DataTableThemeData

```dart
class DataTableThemeData with Diagnosticable {}
```

Defines default property values for descendant [DataTable] widgets.

Descendant widgets obtain the current [DataTableThemeData] object using [DataTableTheme.of]. Instances of [DataTableThemeData] can be customized with [DataTableThemeData.copyWith].

Typically a [DataTableThemeData] is specified as part of the overall [Theme] with [ThemeData.dataTableTheme].

All [DataTableThemeData] properties are `null` by default. When null, the [DataTable] will use the values from [ThemeData] if they exist, otherwise it will provide its own defaults based on the overall [Theme]'s textTheme and colorScheme. See the individual [DataTable] properties for details.

See also:

- [ThemeData], which describes the overall theme information for the application.

### DataTableThemeData()

```dart
DataTableThemeData({Decoration? decoration, WidgetStateProperty<Color?>? dataRowColor, double? dataRowHeight, double? dataRowMinHeight, double? dataRowMaxHeight, TextStyle? dataTextStyle, WidgetStateProperty<Color?>? headingRowColor, double? headingRowHeight, TextStyle? headingTextStyle, double? horizontalMargin, double? columnSpacing, double? dividerThickness, double? checkboxHorizontalMargin, WidgetStateProperty<MouseCursor?>? headingCellCursor, WidgetStateProperty<MouseCursor?>? dataRowCursor, MainAxisAlignment? headingRowAlignment})
```

Creates a theme that can be used for [ThemeData.dataTableTheme].

### decoration

```dart
Decoration? decoration
```

{@macro flutter.material.dataTable.decoration}

### dataRowColor

```dart
WidgetStateProperty<Color?>? dataRowColor
```

{@macro flutter.material.dataTable.dataRowColor} {@macro flutter.material.DataTable.dataRowColor}

### dataRowHeight

```dart
double? get dataRowHeight
```

{@macro flutter.material.dataTable.dataRowHeight}

### dataRowMinHeight

```dart
double? dataRowMinHeight
```

{@macro flutter.material.dataTable.dataRowMinHeight}

### dataRowMaxHeight

```dart
double? dataRowMaxHeight
```

{@macro flutter.material.dataTable.dataRowMaxHeight}

### dataTextStyle

```dart
TextStyle? dataTextStyle
```

{@macro flutter.material.dataTable.dataTextStyle}

### headingRowColor

```dart
WidgetStateProperty<Color?>? headingRowColor
```

{@macro flutter.material.dataTable.headingRowColor} {@macro flutter.material.DataTable.headingRowColor}

### headingRowHeight

```dart
double? headingRowHeight
```

{@macro flutter.material.dataTable.headingRowHeight}

### headingTextStyle

```dart
TextStyle? headingTextStyle
```

{@macro flutter.material.dataTable.headingTextStyle}

### horizontalMargin

```dart
double? horizontalMargin
```

{@macro flutter.material.dataTable.horizontalMargin}

### columnSpacing

```dart
double? columnSpacing
```

{@macro flutter.material.dataTable.columnSpacing}

### dividerThickness

```dart
double? dividerThickness
```

{@macro flutter.material.dataTable.dividerThickness}

### checkboxHorizontalMargin

```dart
double? checkboxHorizontalMargin
```

{@macro flutter.material.dataTable.checkboxHorizontalMargin}

### headingCellCursor

```dart
WidgetStateProperty<MouseCursor?>? headingCellCursor
```

If specified, overrides the default value of [DataColumn.mouseCursor].

### dataRowCursor

```dart
WidgetStateProperty<MouseCursor?>? dataRowCursor
```

If specified, overrides the default value of [DataRow.mouseCursor].

### headingRowAlignment

```dart
MainAxisAlignment? headingRowAlignment
```

If specified, overrides the default value of [DataColumn.headingRowAlignment].

### copyWith()

```dart
DataTableThemeData copyWith({Decoration? decoration, WidgetStateProperty<Color?>? dataRowColor, double? dataRowHeight, double? dataRowMinHeight, double? dataRowMaxHeight, TextStyle? dataTextStyle, WidgetStateProperty<Color?>? headingRowColor, double? headingRowHeight, TextStyle? headingTextStyle, double? horizontalMargin, double? columnSpacing, double? dividerThickness, double? checkboxHorizontalMargin, WidgetStateProperty<MouseCursor?>? headingCellCursor, WidgetStateProperty<MouseCursor?>? dataRowCursor, MainAxisAlignment? headingRowAlignment})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
DataTableThemeData lerp(DataTableThemeData a, DataTableThemeData b, double t)
```

Linearly interpolate between two [DataTableThemeData]s.

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

# DataTableTheme

```dart
class DataTableTheme extends InheritedWidget {}
```

Applies a data table theme to descendant [DataTable] widgets.

Descendant widgets obtain the current theme's [DataTableTheme] object using [DataTableTheme.of]. When a widget uses [DataTableTheme.of], it is automatically rebuilt if the theme later changes.

A data table theme can be specified as part of the overall Material theme using [ThemeData.dataTableTheme].

See also:

- [DataTableThemeData], which describes the actual configuration of a data table theme.

### DataTableTheme()

```dart
DataTableTheme({dynamic key, required DataTableThemeData data, required dynamic child})
```

Constructs a data table theme that configures all descendant [DataTable] widgets.

### data

```dart
DataTableThemeData data
```

The properties used for all descendant [DataTable] widgets.

### of()

```dart
DataTableThemeData of(BuildContext context)
```

Returns the configuration [data] from the closest [DataTableTheme] ancestor. If there is no ancestor, it returns [ThemeData.dataTableTheme]. Applications can assume that the returned value will not be null.

Typical usage is as follows:

```dart
DataTableThemeData theme = DataTableTheme.of(context);
```

### updateShouldNotify()

```dart
bool updateShouldNotify(DataTableTheme oldWidget)
```
