@docImport 'paginated_data_table.dart'; @docImport 'text_theme.dart';

# DataColumnSortCallback

```dart
typedef DataColumnSortCallback = void Function(int columnIndex, bool ascending)
```

Signature for [DataColumn.onSort] callback.

# DataColumn

```dart
class DataColumn {}
```

Column configuration for a [DataTable].

One column configuration must be provided for each column to display in the table. The list of [DataColumn] objects is passed as the `columns` argument to the [DataTable.new] constructor.

### DataColumn()

```dart
DataColumn({required Widget label, TableColumnWidth? columnWidth, String? tooltip, bool numeric = false, DataColumnSortCallback? onSort, WidgetStateProperty<MouseCursor?>? mouseCursor, MainAxisAlignment? headingRowAlignment})
```

Creates the configuration for a column of a [DataTable].

### label

```dart
Widget label
```

The column heading.

Typically, this will be a [Text] widget. It could also be an [Icon] (typically using size 18), or a [Row] with an icon and some text.

The [label] is placed within a [Row] along with the sort indicator (if applicable). By default, [label] only occupy minimal space. It is recommended to place the label content in an [Expanded] or [Flexible] as [label] to control how the content flexes. Otherwise, an exception will occur when the available space is insufficient.

By default, [DefaultTextStyle.softWrap] of this subtree will be set to false. Use [DefaultTextStyle.merge] to override it if needed.

The label should not include the sort indicator.

### columnWidth

```dart
TableColumnWidth? columnWidth
```

How the horizontal extents of this column of the table should be determined.

The [FixedColumnWidth] class can be used to specify a specific width in pixels. This is the cheapest way to size a table's columns.

The layout performance of the table depends critically on which column sizing algorithms are used here. In particular, [IntrinsicColumnWidth] is quite expensive because it needs to measure each cell in the column to determine the intrinsic size of the column.

If this property is `null`, the table applies a default behavior:

- If the table has exactly one column identified as the only text column (i.e., all the rest are numeric), that column uses `IntrinsicColumnWidth(flex: 1.0)`.
- All other columns use `IntrinsicColumnWidth()`.

### tooltip

```dart
String? tooltip
```

The column heading's tooltip.

This is a longer description of the column heading, for cases where the heading might have been abbreviated to keep the column width to a reasonable size.

### numeric

```dart
bool numeric
```

Whether this column represents numeric data or not.

The contents of cells of columns containing numeric data are right-aligned.

### onSort

```dart
DataColumnSortCallback? onSort
```

Called when the user asks to sort the table using this column.

If non-null, space is reserved in the column header for the sort indicator (the arrow icon), even when this column is not currently the active sort column and no arrow is painted. This can affect the layout and width of the column.

If null, the column will not be considered sortable.

See [DataTable.sortColumnIndex] and [DataTable.sortAscending].

### mouseCursor

```dart
WidgetStateProperty<MouseCursor?>? mouseCursor
```

The cursor for a mouse pointer when it enters or is hovering over the heading row.

[WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.disabled].

If this is null, then the value of [DataTableThemeData.headingCellCursor] is used. If that's null, then [WidgetStateMouseCursor.clickable] is used.

See also:

- [WidgetStateMouseCursor], which can be used to create a [MouseCursor].

### headingRowAlignment

```dart
MainAxisAlignment? headingRowAlignment
```

Defines the horizontal layout of the [label] and sort indicator in the heading row.

If [headingRowAlignment] value is [MainAxisAlignment.center] and [onSort] is not null, then a [SizedBox] with a width of sort arrow icon size and sort arrow padding will be placed before the [label] to ensure the label is centered in the column.

If null, then defaults to [MainAxisAlignment.start].

# DataRow

```dart
class DataRow {}
```

Row configuration and cell data for a [DataTable].

One row configuration must be provided for each row to display in the table. The list of [DataRow] objects is passed as the `rows` argument to the [DataTable.new] constructor.

The data for this row of the table is provided in the [cells] property of the [DataRow] object.

### DataRow()

```dart
DataRow({LocalKey? key, bool selected = false, ValueChanged<bool?>? onSelectChanged, GestureLongPressCallback? onLongPress, ValueChanged<bool>? onHover, WidgetStateProperty<Color?>? color, WidgetStateProperty<MouseCursor?>? mouseCursor, required List<DataCell> cells})
```

Creates the configuration for a row of a [DataTable].

### DataRow.byIndex()

```dart
DataRow.byIndex({int? index, bool selected = false, ValueChanged<bool?>? onSelectChanged, GestureLongPressCallback? onLongPress, ValueChanged<bool>? onHover, WidgetStateProperty<Color?>? color, WidgetStateProperty<MouseCursor?>? mouseCursor, required List<DataCell> cells})
```

Creates the configuration for a row of a [DataTable], deriving the key from a row index.

### key

```dart
LocalKey? key
```

A [Key] that uniquely identifies this row. This is used to ensure that if a row is added or removed, any stateful widgets related to this row (e.g. an in-progress checkbox animation) remain on the right row visually.

If the table never changes once created, no key is necessary.

### onSelectChanged

```dart
ValueChanged<bool?>? onSelectChanged
```

Called when the user selects or unselects a selectable row.

If this is not null, then the row is selectable. The current selection state of the row is given by [selected].

If any row is selectable, then the table's heading row will have a checkbox that can be checked to select all selectable rows (and which is checked if all the rows are selected), and each subsequent row will have a checkbox to toggle just that row.

A row whose [onSelectChanged] callback is null is ignored for the purposes of determining the state of the "all" checkbox, and its checkbox is disabled.

If a [DataCell] in the row has its [DataCell.onTap] callback defined, that callback behavior overrides the gesture behavior of the row for that particular cell.

### onLongPress

```dart
GestureLongPressCallback? onLongPress
```

Called if the row is long-pressed.

If a [DataCell] in the row has its [DataCell.onTap], [DataCell.onDoubleTap], [DataCell.onLongPress], [DataCell.onTapCancel] or [DataCell.onTapDown] callback defined, that callback behavior overrides the gesture behavior of the row for that particular cell.

### onHover

```dart
ValueChanged<bool>? onHover
```

Called when a pointer enters or exits the row.

The boolean value passed to the callback is true if a pointer has entered the row and false when a pointer has exited the row.

### selected

```dart
bool selected
```

Whether the row is selected.

If [onSelectChanged] is non-null for any row in the table, then a checkbox is shown at the start of each row. If the row is selected (true), the checkbox will be checked and the row will be highlighted.

Otherwise, the checkbox, if present, will not be checked.

### cells

```dart
List<DataCell> cells
```

The data for this row.

There must be exactly as many cells as there are columns in the table.

### color

```dart
WidgetStateProperty<Color?>? color
```

The color for the row.

By default, the color is transparent unless selected. Selected rows has a grey translucent color.

The effective color can depend on the [WidgetState] state, if the row is selected, pressed, hovered, focused, disabled or enabled. The color is painted as an overlay to the row. To make sure that the row's [InkWell] is visible (when pressed, hovered and focused), it is recommended to use a translucent color.

If [onSelectChanged] or [onLongPress] is null, the row's [InkWell] will be disabled.

```dart
DataRow(
  color: WidgetStateProperty.resolveWith<Color?>((Set<WidgetState> states) {
    if (states.contains(WidgetState.selected)) {
      return Theme.of(context).colorScheme.primary.withValues(alpha: 0.08);
    }
    return null;  // Use the default value.
  }),
  cells: const <DataCell>[
    // ...
  ],
)
```

See also:

- The Material Design specification for overlay colors and how they match a component's state: <https://material.io/design/interaction/states.html#anatomy>.

### mouseCursor

```dart
WidgetStateProperty<MouseCursor?>? mouseCursor
```

The cursor for a mouse pointer when it enters or is hovering over the data row.

[WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.selected].

If this is null, then the value of [DataTableThemeData.dataRowCursor] is used. If that's null, then [WidgetStateMouseCursor.clickable] is used.

See also:

- [WidgetStateMouseCursor], which can be used to create a [MouseCursor].

# DataCell

```dart
class DataCell {}
```

The data for a cell of a [DataTable].

One list of [DataCell] objects must be provided for each [DataRow] in the [DataTable], in the new [DataRow] constructor's `cells` argument.

### DataCell()

```dart
DataCell(Widget child, {bool placeholder = false, bool showEditIcon = false, GestureTapCallback? onTap, GestureLongPressCallback? onLongPress, GestureTapDownCallback? onTapDown, GestureTapCallback? onDoubleTap, GestureTapCancelCallback? onTapCancel})
```

Creates an object to hold the data for a cell in a [DataTable].

The first argument is the widget to show for the cell, typically a [Text] or [DropdownButton] widget.

If the cell has no data, then a [Text] widget with placeholder text should be provided instead, and then the [placeholder] argument should be set to true.

### empty

```dart
DataCell empty
```

A cell that has no content and has zero width and height.

### child

```dart
Widget child
```

The data for the row.

Typically a [Text] widget or a [DropdownButton] widget.

If the cell has no data, then a [Text] widget with placeholder text should be provided instead, and [placeholder] should be set to true.

{@macro flutter.widgets.ProxyWidget.child}

### placeholder

```dart
bool placeholder
```

Whether the [child] is actually a placeholder.

If this is true, the default text style for the cell is changed to be appropriate for placeholder text.

### showEditIcon

```dart
bool showEditIcon
```

Whether to show an edit icon at the end of the cell.

This does not make the cell actually editable; the caller must implement editing behavior if desired (initiated from the [onTap] callback).

If this is set, [onTap] should also be set, otherwise tapping the icon will have no effect.

### onTap

```dart
GestureTapCallback? onTap
```

Called if the cell is tapped.

If non-null, tapping the cell will call this callback. If null (including [onDoubleTap], [onLongPress], [onTapCancel] and [onTapDown]), tapping the cell will attempt to select the row (if [DataRow.onSelectChanged] is provided).

### onDoubleTap

```dart
GestureTapCallback? onDoubleTap
```

Called when the cell is double tapped.

If non-null, tapping the cell will call this callback. If null (including [onTap], [onLongPress], [onTapCancel] and [onTapDown]), tapping the cell will attempt to select the row (if [DataRow.onSelectChanged] is provided).

### onLongPress

```dart
GestureLongPressCallback? onLongPress
```

Called if the cell is long-pressed.

If non-null, tapping the cell will invoke this callback. If null (including [onDoubleTap], [onTap], [onTapCancel] and [onTapDown]), tapping the cell will attempt to select the row (if [DataRow.onSelectChanged] is provided).

### onTapDown

```dart
GestureTapDownCallback? onTapDown
```

Called if the cell is tapped down.

If non-null, tapping the cell will call this callback. If null (including [onTap] [onDoubleTap], [onLongPress] and [onTapCancel]), tapping the cell will attempt to select the row (if [DataRow.onSelectChanged] is provided).

### onTapCancel

```dart
GestureTapCancelCallback? onTapCancel
```

Called if the user cancels a tap was started on cell.

If non-null, canceling the tap gesture will invoke this callback. If null (including [onTap], [onDoubleTap] and [onLongPress]), tapping the cell will attempt to select the row (if [DataRow.onSelectChanged] is provided).

# DataTable

```dart
class DataTable extends StatelessWidget {}
```

A data table that follows the [Material 2](https://material.io/go/design-data-tables) design specification.

{@youtube 560 315 https://www.youtube.com/watch?v=ktTajqbhIcY}

## Performance considerations

Columns are sized automatically based on the table's contents. It's expensive to display large amounts of data with this widget, since it must be measured twice: once to negotiate each column's dimensions, and again when the table is laid out.

A [SingleChildScrollView] mounts and paints the entire child, even when only some of it is visible. For a table that effectively handles large amounts of data, here are some other options to consider:

- `TableView`, a widget from the [two_dimensional_scrollables](https://pub.dev/packages/two_dimensional_scrollables) package.
- [PaginatedDataTable], which automatically splits the data into multiple pages.
- [CustomScrollView], for greater control over scrolling effects.

{@tool dartpad} This sample shows how to display a [DataTable] with three columns: name, age, and role. The columns are defined by three [DataColumn] objects. The table contains three rows of data for three example users, the data for which is defined by three [DataRow] objects.

![](https://flutter.github.io/assets-for-api-docs/assets/material/data_table.png)

** See code in examples/api/lib/material/data_table/data_table.0.dart ** {@end-tool}

{@tool dartpad} This sample shows how to display a [DataTable] with alternate colors per row, and a custom color for when the row is selected.

** See code in examples/api/lib/material/data_table/data_table.1.dart ** {@end-tool}

[DataTable] can be sorted on the basis of any column in [columns] in ascending or descending order. If [sortColumnIndex] is non-null, then the table will be sorted by the values in the specified column. The boolean [sortAscending] flag controls the sort order.

See also:

- [DataColumn], which describes a column in the data table.
- [DataRow], which contains the data for a row in the data table.
- [DataCell], which contains the data for a single cell in the data table.
- [PaginatedDataTable], which shows part of the data in a data table and provides controls for paging through the remainder of the data.
- `TableView` from the [two_dimensional_scrollables](https://pub.dev/packages/two_dimensional_scrollables) package, for displaying large amounts of data without pagination.
- <https://material.io/go/design-data-tables>

### DataTable()

```dart
DataTable({dynamic key, required List<DataColumn> columns, int? sortColumnIndex, bool sortAscending = true, ValueSetter<bool?>? onSelectAll, Decoration? decoration, WidgetStateProperty<Color?>? dataRowColor, double? dataRowHeight, double? dataRowMinHeight, double? dataRowMaxHeight, TextStyle? dataTextStyle, WidgetStateProperty<Color?>? headingRowColor, double? headingRowHeight, TextStyle? headingTextStyle, double? horizontalMargin, double? columnSpacing, bool showCheckboxColumn = true, bool showBottomBorder = false, double? dividerThickness, required List<DataRow> rows, double? checkboxHorizontalMargin, TableBorder? border, Clip clipBehavior = Clip.none})
```

Creates a widget describing a data table.

The [columns] argument must be a list of as many [DataColumn] objects as the table is to have columns, ignoring the leading checkbox column if any. The [columns] argument must have a length greater than zero.

The [rows] argument must be a list of as many [DataRow] objects as the table is to have rows, ignoring the leading heading row that contains the column headings (derived from the [columns] argument). There may be zero rows, but the rows argument must not be null.

Each [DataRow] object in [rows] must have as many [DataCell] objects in the [DataRow.cells] list as the table has columns.

If the table is sorted, the column that provides the current primary key should be specified by index in [sortColumnIndex], 0 meaning the first column in [columns], 1 being the next one, and so forth.

The actual sort order can be specified using [sortAscending]; if the sort order is ascending, this should be true (the default), otherwise it should be false.

### columns

```dart
List<DataColumn> columns
```

The configuration and labels for the columns in the table.

### sortColumnIndex

```dart
int? sortColumnIndex
```

The current primary sort key's column.

If non-null, indicates that the indicated column is the column by which the data is sorted. The number must correspond to the index of the relevant column in [columns].

Setting this will cause the relevant column to have a sort indicator displayed.

When this is null, it implies that the table's sort order does not correspond to any of the columns.

The direction of the sort is specified using [sortAscending].

### sortAscending

```dart
bool sortAscending
```

Whether the column mentioned in [sortColumnIndex], if any, is sorted in ascending order.

If true, the order is ascending (meaning the rows with the smallest values for the current sort column are first in the table).

If false, the order is descending (meaning the rows with the smallest values for the current sort column are last in the table).

Ascending order is represented by an upwards-facing arrow.

### onSelectAll

```dart
ValueSetter<bool?>? onSelectAll
```

Invoked when the user selects or unselects every row, using the checkbox in the heading row.

If this is null, then the [DataRow.onSelectChanged] callback of every row in the table is invoked appropriately instead.

To control whether a particular row is selectable or not, see [DataRow.onSelectChanged]. This callback is only relevant if any row is selectable.

### decoration

```dart
Decoration? decoration
```

{@template flutter.material.dataTable.decoration} The background and border decoration for the table. {@endtemplate}

If null, [DataTableThemeData.decoration] is used. By default there is no decoration.

### dataRowColor

```dart
WidgetStateProperty<Color?>? dataRowColor
```

{@template flutter.material.dataTable.dataRowColor} The background color for the data rows.

The effective background color can be made to depend on the [WidgetState] state, i.e. if the row is selected, pressed, hovered, focused, disabled or enabled. The color is painted as an overlay to the row. To make sure that the row's [InkWell] is visible (when pressed, hovered and focused), it is recommended to use a translucent background color.

If [DataRow.onSelectChanged] or [DataRow.onLongPress] is null, the row's [InkWell] will be disabled. {@endtemplate}

If null, [DataTableThemeData.dataRowColor] is used. By default, the background color is transparent unless selected. Selected rows have a grey translucent color. To set a different color for individual rows, see [DataRow.color].

{@template flutter.material.DataTable.dataRowColor}

```dart
DataTable(
  dataRowColor: WidgetStateProperty.resolveWith<Color?>((Set<WidgetState> states) {
    if (states.contains(WidgetState.selected)) {
      return Theme.of(context).colorScheme.primary.withValues(alpha: 0.08);
    }
    return null;  // Use the default value.
  }),
  columns: _columns,
  rows: _rows,
)
```

See also:

- The Material Design specification for overlay colors and how they match a component's state: <https://material.io/design/interaction/states.html#anatomy>. {@endtemplate}

### dataRowHeight

```dart
double? get dataRowHeight
```

{@template flutter.material.dataTable.dataRowHeight} The height of each row (excluding the row that contains column headings). {@endtemplate}

If null, [DataTableThemeData.dataRowHeight] is used. This value defaults to [kMinInteractiveDimension] to adhere to the Material Design specifications.

### dataRowMinHeight

```dart
double? dataRowMinHeight
```

{@template flutter.material.dataTable.dataRowMinHeight} The minimum height of each row (excluding the row that contains column headings). {@endtemplate}

If null, [DataTableThemeData.dataRowMinHeight] is used. This value defaults to [kMinInteractiveDimension] to adhere to the Material Design specifications.

### dataRowMaxHeight

```dart
double? dataRowMaxHeight
```

{@template flutter.material.dataTable.dataRowMaxHeight} The maximum height of each row (excluding the row that contains column headings). {@endtemplate}

If null, [DataTableThemeData.dataRowMaxHeight] is used. This value defaults to [kMinInteractiveDimension] to adhere to the Material Design specifications.

### dataTextStyle

```dart
TextStyle? dataTextStyle
```

{@template flutter.material.dataTable.dataTextStyle} The text style for data rows. {@endtemplate}

If null, [DataTableThemeData.dataTextStyle] is used. By default, the text style is [TextTheme.bodyMedium].

### headingRowColor

```dart
WidgetStateProperty<Color?>? headingRowColor
```

{@template flutter.material.dataTable.headingRowColor} The background color for the heading row.

The effective background color can be made to depend on the [WidgetState] state, i.e. if the row is pressed, hovered, focused when sorted. The color is painted as an overlay to the row. To make sure that the row's [InkWell] is visible (when pressed, hovered and focused), it is recommended to use a translucent color. {@endtemplate}

If null, [DataTableThemeData.headingRowColor] is used.

{@template flutter.material.DataTable.headingRowColor}

```dart
DataTable(
  columns: _columns,
  rows: _rows,
  headingRowColor: WidgetStateProperty.resolveWith<Color?>((Set<WidgetState> states) {
    if (states.contains(WidgetState.hovered)) {
      return Theme.of(context).colorScheme.primary.withValues(alpha: 0.08);
    }
    return null;  // Use the default value.
  }),
)
```

See also:

- The Material Design specification for overlay colors and how they match a component's state: <https://material.io/design/interaction/states.html#anatomy>. {@endtemplate}

### headingRowHeight

```dart
double? headingRowHeight
```

{@template flutter.material.dataTable.headingRowHeight} The height of the heading row. {@endtemplate}

If null, [DataTableThemeData.headingRowHeight] is used. This value defaults to 56.0 to adhere to the Material Design specifications.

### headingTextStyle

```dart
TextStyle? headingTextStyle
```

{@template flutter.material.dataTable.headingTextStyle} The text style for the heading row. {@endtemplate}

If null, [DataTableThemeData.headingTextStyle] is used. By default, the text style is [TextTheme.titleSmall].

### horizontalMargin

```dart
double? horizontalMargin
```

{@template flutter.material.dataTable.horizontalMargin} The horizontal margin between the edges of the table and the content in the first and last cells of each row.

When a checkbox is displayed, it is also the margin between the checkbox the content in the first data column. {@endtemplate}

If null, [DataTableThemeData.horizontalMargin] is used. This value defaults to 24.0 to adhere to the Material Design specifications.

If [checkboxHorizontalMargin] is null, then [horizontalMargin] is also the margin between the edge of the table and the checkbox, as well as the margin between the checkbox and the content in the first data column.

### columnSpacing

```dart
double? columnSpacing
```

{@template flutter.material.dataTable.columnSpacing} The horizontal margin between the contents of each data column. {@endtemplate}

If null, [DataTableThemeData.columnSpacing] is used. This value defaults to 56.0 to adhere to the Material Design specifications.

### showCheckboxColumn

```dart
bool showCheckboxColumn
```

{@template flutter.material.dataTable.showCheckboxColumn} Whether the widget should display checkboxes for selectable rows.

If true, a [Checkbox] will be placed at the beginning of each row that is selectable. However, if [DataRow.onSelectChanged] is not set for any row, checkboxes will not be placed, even if this value is true.

If false, all rows will not display a [Checkbox]. {@endtemplate}

### rows

```dart
List<DataRow> rows
```

The data to show in each row (excluding the row that contains the column headings).

The list may be empty.

### dividerThickness

```dart
double? dividerThickness
```

{@template flutter.material.dataTable.dividerThickness} The width of the divider that appears between [TableRow]s.

Must be greater than or equal to zero. {@endtemplate}

If null, [DataTableThemeData.dividerThickness] is used. This value defaults to 1.0.

### showBottomBorder

```dart
bool showBottomBorder
```

Whether a border at the bottom of the table is displayed.

By default, a border is not shown at the bottom to allow for a border around the table defined by [decoration].

### checkboxHorizontalMargin

```dart
double? checkboxHorizontalMargin
```

{@template flutter.material.dataTable.checkboxHorizontalMargin} Horizontal margin around the checkbox, if it is displayed. {@endtemplate}

If null, [DataTableThemeData.checkboxHorizontalMargin] is used. If that is also null, then [horizontalMargin] is used as the margin between the edge of the table and the checkbox, as well as the margin between the checkbox and the content in the first data column. This value defaults to 24.0.

### border

```dart
TableBorder? border
```

The style to use when painting the boundary and interior divisions of the table.

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

This can be used to clip the content within the border of the [DataTable].

Defaults to [Clip.none].

### build()

```dart
Widget build(BuildContext context)
```

# TableRowInkWell

```dart
class TableRowInkWell extends InkResponse {}
```

A rectangular area of a Material that responds to touch but clips its ink splashes to the current table row of the nearest table.

Must have an ancestor [Material] widget in which to cause ink reactions and an ancestor [Table] widget to establish a row.

The [TableRowInkWell] must be in the same coordinate space (modulo translations) as the [Table]. If it's rotated or scaled or otherwise transformed, it will not be able to describe the rectangle of the row in its own coordinate system as a [Rect], and thus the splash will not occur. (In general, this is easy to achieve: just put the [TableRowInkWell] as the direct child of the [Table], and put the other contents of the cell inside it.)

See also:

- [DataTable], which makes use of [TableRowInkWell] when [DataRow.onSelectChanged] is defined and [DataCell.onTap] is not.

### TableRowInkWell()

```dart
TableRowInkWell({dynamic key, dynamic child, dynamic onTap, dynamic onDoubleTap, dynamic onLongPress, dynamic onHighlightChanged, dynamic onHover, dynamic onSecondaryTap, dynamic onSecondaryTapDown, dynamic overlayColor, dynamic mouseCursor})
```

Creates an ink well for a table row.

### getRectCallback()

```dart
RectCallback getRectCallback(RenderBox referenceBox)
```

### debugCheckContext()

```dart
bool debugCheckContext(BuildContext context)
```
