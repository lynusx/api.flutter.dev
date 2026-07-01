@docImport 'scroll_view.dart'; @docImport 'sliver.dart';

# TableRow

```dart
class TableRow {}
```

A horizontal group of cells in a [Table].

Every row in a table must have the same number of children.

The alignment of individual cells in a row can be controlled using a [TableCell].

### TableRow()

```dart
TableRow({LocalKey? key, Decoration? decoration, List<Widget> children = const <Widget>[]})
```

Creates a row in a [Table].

### key

```dart
LocalKey? key
```

An identifier for the row.

### decoration

```dart
Decoration? decoration
```

A decoration to paint behind this row.

Row decorations fill the horizontal and vertical extent of each row in the table, unlike decorations for individual cells, which might not fill either.

### children

```dart
List<Widget> children
```

The widgets that comprise the cells in this row.

Children may be wrapped in [TableCell] widgets to provide per-cell configuration to the [Table], but children are not required to be wrapped in [TableCell] widgets.

### toString()

```dart
String toString()
```

# Table

```dart
class Table extends RenderObjectWidget {}
```

A widget that uses the table layout algorithm for its children.

{@youtube 560 315 https://www.youtube.com/watch?v=_lbE0wsVZSw}

{@tool dartpad} This sample shows a [Table] with borders, multiple types of column widths and different vertical cell alignments.

** See code in examples/api/lib/widgets/table/table.0.dart ** {@end-tool}

If you only have one row, the [Row] widget is more appropriate. If you only have one column, the [SliverList] or [Column] widgets will be more appropriate.

Rows size vertically based on their contents. To control the individual column widths, use the [columnWidths] property to specify a [TableColumnWidth] for each column. If [columnWidths] is null, or there is a null entry for a given column in [columnWidths], the table uses the [defaultColumnWidth] instead.

By default, [defaultColumnWidth] is a [FlexColumnWidth]. This [TableColumnWidth] divides up the remaining space in the horizontal axis to determine the column width. If wrapping a [Table] in a horizontal [ScrollView], choose a different [TableColumnWidth], such as [FixedColumnWidth].

For more details about the table layout algorithm, see [RenderTable]. To control the alignment of children, see [TableCell].

See also:

- The [catalog of layout widgets](https://flutter.dev/widgets/layout/).

### Table()

```dart
Table({dynamic key, List<TableRow> children = const <TableRow>[], Map<int, TableColumnWidth>? columnWidths, TableColumnWidth defaultColumnWidth = const FlexColumnWidth(), TextDirection? textDirection, TableBorder? border, TableCellVerticalAlignment defaultVerticalAlignment = TableCellVerticalAlignment.top, TextBaseline? textBaseline})
```

Creates a table.

### children

```dart
List<TableRow> children
```

The rows of the table.

Every row in a table must have the same number of children.

### columnWidths

```dart
Map<int, TableColumnWidth>? columnWidths
```

How the horizontal extents of the columns of this table should be determined.

If the [Map] has a null entry for a given column, the table uses the [defaultColumnWidth] instead. By default, that uses flex sizing to distribute free space equally among the columns.

The [FixedColumnWidth] class can be used to specify a specific width in pixels. That is the cheapest way to size a table's columns.

The layout performance of the table depends critically on which column sizing algorithms are used here. In particular, [IntrinsicColumnWidth] is quite expensive because it needs to measure each cell in the column to determine the intrinsic size of the column.

The keys of this map (column indexes) are zero-based.

If this is set to null, then an empty map is assumed.

### defaultColumnWidth

```dart
TableColumnWidth defaultColumnWidth
```

How to determine with widths of columns that don't have an explicit sizing algorithm.

Specifically, the [defaultColumnWidth] is used for column `i` if `columnWidths[i]` is null. Defaults to [FlexColumnWidth], which will divide the remaining horizontal space up evenly between columns of the same type [TableColumnWidth].

A [Table] in a horizontal [ScrollView] must use a [FixedColumnWidth], or an [IntrinsicColumnWidth] as the horizontal space is infinite.

### textDirection

```dart
TextDirection? textDirection
```

The direction in which the columns are ordered.

Defaults to the ambient [Directionality].

### border

```dart
TableBorder? border
```

The style to use when painting the boundary and interior divisions of the table.

### defaultVerticalAlignment

```dart
TableCellVerticalAlignment defaultVerticalAlignment
```

How cells that do not explicitly specify a vertical alignment are aligned vertically.

Cells may specify a vertical alignment by wrapping their contents in a [TableCell] widget.

### textBaseline

```dart
TextBaseline? textBaseline
```

The text baseline to use when aligning rows using [TableCellVerticalAlignment.baseline].

This must be set if using baseline alignment. There is no default because there is no way for the framework to know the correct baseline _a priori_.

### createElement()

```dart
RenderObjectElement createElement()
```

### createRenderObject()

```dart
RenderTable createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderTable renderObject)
```

# TableCell

```dart
class TableCell extends StatelessWidget {}
```

A widget that controls how a child of a [Table] is aligned.

A [TableCell] widget must be a descendant of a [Table], and the path from the [TableCell] widget to its enclosing [Table] must contain only [TableRow]s, [StatelessWidget]s, or [StatefulWidget]s (not other kinds of widgets, like [RenderObjectWidget]s).

To create an empty [TableCell], provide a [SizedBox.shrink] as the [child].

### TableCell()

```dart
TableCell({dynamic key, TableCellVerticalAlignment? verticalAlignment, required Widget child})
```

Creates a widget that controls how a child of a [Table] is aligned.

### verticalAlignment

```dart
TableCellVerticalAlignment? verticalAlignment
```

How this cell is aligned vertically.

### child

```dart
Widget child
```

The child of this cell.

### build()

```dart
Widget build(BuildContext context)
```
