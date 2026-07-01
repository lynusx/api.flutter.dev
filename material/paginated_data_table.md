@docImport 'card_theme.dart'; @docImport 'data_table_theme.dart'; @docImport 'text_button.dart';

# PaginatedDataTable

```dart
class PaginatedDataTable extends StatefulWidget {}
```

A table that follows the [Material 2](https://material.io/go/design-data-tables) design specification, using multiple pages to display data.

A paginated data table shows [rowsPerPage] rows of data per page and provides controls for showing other pages.

Data is read lazily from a [DataTableSource]. The widget is presented as a [Card].

If the [key] is a [PageStorageKey], the [initialFirstRowIndex] is persisted to [PageStorage].

{@tool dartpad}

This sample shows how to display a [DataTable] with three columns: name, age, and role. The columns are defined by three [DataColumn] objects. The table contains three rows of data for three example users, the data for which is defined by three [DataRow] objects.

** See code in examples/api/lib/material/paginated_data_table/paginated_data_table.0.dart ** {@end-tool}

{@tool dartpad}

This example shows how paginated data tables can supported sorted data.

** See code in examples/api/lib/material/paginated_data_table/paginated_data_table.1.dart ** {@end-tool}

See also:

- [DataTable], which is not paginated.
- `TableView` from the [two_dimensional_scrollables](https://pub.dev/packages/two_dimensional_scrollables) package, for displaying large amounts of data without pagination.
- <https://material.io/go/design-data-tables>

### PaginatedDataTable()

```dart
PaginatedDataTable({dynamic key, Widget? header, List<Widget>? actions, required List<DataColumn> columns, int? sortColumnIndex, bool sortAscending = true, ValueSetter<bool?>? onSelectAll, double? dataRowHeight, double? dataRowMinHeight, double? dataRowMaxHeight, double headingRowHeight = 56.0, double horizontalMargin = 24.0, double columnSpacing = 56.0, bool showCheckboxColumn = true, bool showFirstLastButtons = false, int? initialFirstRowIndex = 0, ValueChanged<int>? onPageChanged, int rowsPerPage = defaultRowsPerPage, List<int> availableRowsPerPage = const <int>[defaultRowsPerPage, defaultRowsPerPage * 2, defaultRowsPerPage * 5, defaultRowsPerPage * 10], ValueChanged<int?>? onRowsPerPageChanged, DragStartBehavior dragStartBehavior = DragStartBehavior.start, Color? arrowHeadColor, required DataTableSource source, double? checkboxHorizontalMargin, ScrollController? controller, bool? primary, WidgetStateProperty<Color?>? headingRowColor, double? dividerThickness, bool showEmptyRows = true})
```

Creates a widget describing a paginated [DataTable] on a [Card].

The [header] should give the card's header, typically a [Text] widget.

The [columns] argument must be a list of as many [DataColumn] objects as the table is to have columns, ignoring the leading checkbox column if any. The [columns] argument must have a length greater than zero and cannot be null.

If the table is sorted, the column that provides the current primary key should be specified by index in [sortColumnIndex], 0 meaning the first column in [columns], 1 being the next one, and so forth.

The actual sort order can be specified using [sortAscending]; if the sort order is ascending, this should be true (the default), otherwise it should be false.

The [source] should be a long-lived [DataTableSource]. The same source should be provided each time a particular [PaginatedDataTable] widget is created; avoid creating a new [DataTableSource] with each new instance of the [PaginatedDataTable] widget unless the data table really is to now show entirely different data from a new source.

Themed by [DataTableTheme]. [DataTableThemeData.decoration] is ignored. To modify the border or background color of the [PaginatedDataTable], use [CardTheme], since a [Card] wraps the inner [DataTable].

### header

```dart
Widget? header
```

The table card's optional header.

This is typically a [Text] widget, but can also be a [Row] of [TextButton]s. To show icon buttons at the top end side of the table with a header, set the [actions] property.

If items in the table are selectable, then, when the selection is not empty, the header is replaced by a count of the selected items. The [actions] are still visible when items are selected.

### actions

```dart
List<Widget>? actions
```

Icon buttons to show at the top end side of the table. The [header] must not be null to show the actions.

Typically, the exact actions included in this list will vary based on whether any rows are selected or not.

These should be size 24.0 with default padding (8.0).

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

See [DataTable.sortColumnIndex] for details.

The direction of the sort is specified using [sortAscending].

### sortAscending

```dart
bool sortAscending
```

Whether the column mentioned in [sortColumnIndex], if any, is sorted in ascending order.

See [DataTable.sortAscending] for details.

### onSelectAll

```dart
ValueSetter<bool?>? onSelectAll
```

Invoked when the user selects or unselects every row, using the checkbox in the heading row.

See [DataTable.onSelectAll].

### dataRowHeight

```dart
double? get dataRowHeight
```

The height of each row (excluding the row that contains column headings).

This value is optional and defaults to kMinInteractiveDimension if not specified.

### dataRowMinHeight

```dart
double? dataRowMinHeight
```

The minimum height of each row (excluding the row that contains column headings).

This value is optional and defaults to [kMinInteractiveDimension] if not specified.

### dataRowMaxHeight

```dart
double? dataRowMaxHeight
```

The maximum height of each row (excluding the row that contains column headings).

This value is optional and defaults to [kMinInteractiveDimension] if not specified.

### headingRowHeight

```dart
double headingRowHeight
```

The height of the heading row.

This value is optional and defaults to 56.0 if not specified.

### horizontalMargin

```dart
double horizontalMargin
```

The horizontal margin between the edges of the table and the content in the first and last cells of each row.

When a checkbox is displayed, it is also the margin between the checkbox the content in the first data column.

This value defaults to 24.0 to adhere to the Material Design specifications.

If [checkboxHorizontalMargin] is null, then [horizontalMargin] is also the margin between the edge of the table and the checkbox, as well as the margin between the checkbox and the content in the first data column.

### columnSpacing

```dart
double columnSpacing
```

The horizontal margin between the contents of each data column.

This value defaults to 56.0 to adhere to the Material Design specifications.

### showCheckboxColumn

```dart
bool showCheckboxColumn
```

{@macro flutter.material.dataTable.showCheckboxColumn}

### showFirstLastButtons

```dart
bool showFirstLastButtons
```

Flag to display the pagination buttons to go to the first and last pages.

### initialFirstRowIndex

```dart
int? initialFirstRowIndex
```

The index of the first row to display when the widget is first created.

### dividerThickness

```dart
double? dividerThickness
```

{@macro flutter.material.dataTable.dividerThickness}

If null, [DataTableThemeData.dividerThickness] is used. This value defaults to 1.0.

### onPageChanged

```dart
ValueChanged<int>? onPageChanged
```

Invoked when the user switches to another page.

The value is the index of the first row on the currently displayed page.

### rowsPerPage

```dart
int rowsPerPage
```

The number of rows to show on each page.

See also:

- [onRowsPerPageChanged]
- [defaultRowsPerPage]

### defaultRowsPerPage

```dart
int defaultRowsPerPage
```

The default value for [rowsPerPage].

Useful when initializing the field that will hold the current [rowsPerPage], when implemented [onRowsPerPageChanged].

### availableRowsPerPage

```dart
List<int> availableRowsPerPage
```

The options to offer for the rowsPerPage.

The current [rowsPerPage] must be a value in this list.

The values in this list should be sorted in ascending order.

### onRowsPerPageChanged

```dart
ValueChanged<int?>? onRowsPerPageChanged
```

Invoked when the user selects a different number of rows per page.

If this is null, then the value given by [rowsPerPage] will be used and no affordance will be provided to change the value.

### source

```dart
DataTableSource source
```

The data source which provides data to show in each row.

This object should generally have a lifetime longer than the [PaginatedDataTable] widget itself; it should be reused each time the [PaginatedDataTable] constructor is called.

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.widgets.scrollable.dragStartBehavior}

### checkboxHorizontalMargin

```dart
double? checkboxHorizontalMargin
```

Horizontal margin around the checkbox, if it is displayed.

If null, then [horizontalMargin] is used as the margin between the edge of the table and the checkbox, as well as the margin between the checkbox and the content in the first data column. This value defaults to 24.0.

### arrowHeadColor

```dart
Color? arrowHeadColor
```

Defines the color of the arrow heads in the footer.

### controller

```dart
ScrollController? controller
```

{@macro flutter.widgets.scroll_view.controller}

### primary

```dart
bool? primary
```

{@macro flutter.widgets.scroll_view.primary}

### headingRowColor

```dart
WidgetStateProperty<Color?>? headingRowColor
```

{@macro flutter.material.dataTable.headingRowColor}

### showEmptyRows

```dart
bool showEmptyRows
```

Controls the visibility of empty rows on the last page of a [PaginatedDataTable].

Defaults to `true`, which means empty rows will be populated on the last page of the table if there is not enough content. When set to `false`, empty rows will not be created.

### createState()

```dart
PaginatedDataTableState createState()
```

# PaginatedDataTableState

```dart
class PaginatedDataTableState extends State<PaginatedDataTable> {}
```

Holds the state of a [PaginatedDataTable].

The table can be programmatically paged using the [pageTo] method.

### initState()

```dart
void initState()
```

### didUpdateWidget()

```dart
void didUpdateWidget(PaginatedDataTable oldWidget)
```

### reassemble()

```dart
void reassemble()
```

### dispose()

```dart
void dispose()
```

### pageTo()

```dart
void pageTo(int rowIndex)
```

Ensures that the given row is visible.

### build()

```dart
Widget build(BuildContext context)
```
