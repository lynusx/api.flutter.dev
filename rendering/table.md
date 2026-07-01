# TableCellParentData

```dart
class TableCellParentData extends BoxParentData {}
```

Parent data used by [RenderTable] for its children.

### verticalAlignment

```dart
TableCellVerticalAlignment? verticalAlignment
```

Where this cell should be placed vertically.

When using [TableCellVerticalAlignment.baseline], the text baseline must be set as well.

### x

```dart
int? x
```

The column that the child was in the last time it was laid out.

### y

```dart
int? y
```

The row that the child was in the last time it was laid out.

### toString()

```dart
String toString()
```

# TableColumnWidth

```dart
abstract class TableColumnWidth {}
```

Base class to describe how wide a column in a [RenderTable] should be.

To size a column to a specific number of pixels, use a [FixedColumnWidth]. This is the cheapest way to size a column.

Other algorithms that are relatively cheap include [FlexColumnWidth], which distributes the space equally among the flexible columns, [FractionColumnWidth], which sizes a column based on the size of the table's container.

### TableColumnWidth()

```dart
TableColumnWidth()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### minIntrinsicWidth()

```dart
double minIntrinsicWidth(Iterable<RenderBox> cells, double containerWidth)
```

The smallest width that the column can have.

The `cells` argument is an iterable that provides all the cells in the table for this column. Walking the cells is by definition O(N), so algorithms that do that should be considered expensive.

The `containerWidth` argument is the `maxWidth` of the incoming constraints for the table, and might be infinite.

### maxIntrinsicWidth()

```dart
double maxIntrinsicWidth(Iterable<RenderBox> cells, double containerWidth)
```

The ideal width that the column should have. This must be equal to or greater than the [minIntrinsicWidth]. The column might be bigger than this width, e.g. if the column is flexible or if the table's width ends up being forced to be bigger than the sum of all the maxIntrinsicWidth values.

The `cells` argument is an iterable that provides all the cells in the table for this column. Walking the cells is by definition O(N), so algorithms that do that should be considered expensive.

The `containerWidth` argument is the `maxWidth` of the incoming constraints for the table, and might be infinite.

### flex()

```dart
double? flex(Iterable<RenderBox> cells)
```

The flex factor to apply to the cell if there is any room left over when laying out the table. The remaining space is distributed to any columns with flex in proportion to their flex value (higher values get more space).

The `cells` argument is an iterable that provides all the cells in the table for this column. Walking the cells is by definition O(N), so algorithms that do that should be considered expensive.

### toString()

```dart
String toString()
```

# IntrinsicColumnWidth

```dart
class IntrinsicColumnWidth extends TableColumnWidth {}
```

Sizes the column according to the intrinsic dimensions of all the cells in that column.

This is a very expensive way to size a column.

A flex value can be provided. If specified (and non-null), the column will participate in the distribution of remaining space once all the non-flexible columns have been sized.

### IntrinsicColumnWidth()

```dart
IntrinsicColumnWidth({double? flex})
```

Creates a column width based on intrinsic sizing.

This sizing algorithm is very expensive.

The `flex` argument specifies the flex factor to apply to the column if there is any room left over when laying out the table. If `flex` is null (the default), the table will not distribute any extra space to the column.

### minIntrinsicWidth()

```dart
double minIntrinsicWidth(Iterable<RenderBox> cells, double containerWidth)
```

### maxIntrinsicWidth()

```dart
double maxIntrinsicWidth(Iterable<RenderBox> cells, double containerWidth)
```

### flex()

```dart
double? flex(Iterable<RenderBox> cells)
```

### toString()

```dart
String toString()
```

# FixedColumnWidth

```dart
class FixedColumnWidth extends TableColumnWidth {}
```

Sizes the column to a specific number of pixels.

This is the cheapest way to size a column.

### FixedColumnWidth()

```dart
FixedColumnWidth(double value)
```

Creates a column width based on a fixed number of logical pixels.

### value

```dart
double value
```

The width the column should occupy in logical pixels.

### minIntrinsicWidth()

```dart
double minIntrinsicWidth(Iterable<RenderBox> cells, double containerWidth)
```

### maxIntrinsicWidth()

```dart
double maxIntrinsicWidth(Iterable<RenderBox> cells, double containerWidth)
```

### toString()

```dart
String toString()
```

# FractionColumnWidth

```dart
class FractionColumnWidth extends TableColumnWidth {}
```

Sizes the column to a fraction of the table's constraints' maxWidth.

This is a cheap way to size a column.

### FractionColumnWidth()

```dart
FractionColumnWidth(double value)
```

Creates a column width based on a fraction of the table's constraints' maxWidth.

### value

```dart
double value
```

The fraction of the table's constraints' maxWidth that this column should occupy.

### minIntrinsicWidth()

```dart
double minIntrinsicWidth(Iterable<RenderBox> cells, double containerWidth)
```

### maxIntrinsicWidth()

```dart
double maxIntrinsicWidth(Iterable<RenderBox> cells, double containerWidth)
```

### toString()

```dart
String toString()
```

# FlexColumnWidth

```dart
class FlexColumnWidth extends TableColumnWidth {}
```

Sizes the column by taking a part of the remaining space once all the other columns have been laid out.

For example, if two columns have a [FlexColumnWidth], then half the space will go to one and half the space will go to the other.

This is a cheap way to size a column.

### FlexColumnWidth()

```dart
FlexColumnWidth([double value = 1.0])
```

Creates a column width based on a fraction of the remaining space once all the other columns have been laid out.

### value

```dart
double value
```

The fraction of the remaining space once all the other columns have been laid out that this column should occupy.

### minIntrinsicWidth()

```dart
double minIntrinsicWidth(Iterable<RenderBox> cells, double containerWidth)
```

### maxIntrinsicWidth()

```dart
double maxIntrinsicWidth(Iterable<RenderBox> cells, double containerWidth)
```

### flex()

```dart
double flex(Iterable<RenderBox> cells)
```

### toString()

```dart
String toString()
```

# MaxColumnWidth

```dart
class MaxColumnWidth extends TableColumnWidth {}
```

Sizes the column such that it is the size that is the maximum of two column width specifications.

For example, to have a column be 10% of the container width or 100px, whichever is bigger, you could use:

const MaxColumnWidth(const FixedColumnWidth(100.0), FractionColumnWidth(0.1))

Both specifications are evaluated, so if either specification is expensive, so is this.

### MaxColumnWidth()

```dart
MaxColumnWidth(TableColumnWidth a, TableColumnWidth b)
```

Creates a column width that is the maximum of two other column widths.

### a

```dart
TableColumnWidth a
```

A lower bound for the width of this column.

### b

```dart
TableColumnWidth b
```

Another lower bound for the width of this column.

### minIntrinsicWidth()

```dart
double minIntrinsicWidth(Iterable<RenderBox> cells, double containerWidth)
```

### maxIntrinsicWidth()

```dart
double maxIntrinsicWidth(Iterable<RenderBox> cells, double containerWidth)
```

### flex()

```dart
double? flex(Iterable<RenderBox> cells)
```

### toString()

```dart
String toString()
```

# MinColumnWidth

```dart
class MinColumnWidth extends TableColumnWidth {}
```

Sizes the column such that it is the size that is the minimum of two column width specifications.

For example, to have a column be 10% of the container width but never bigger than 100px, you could use:

const MinColumnWidth(const FixedColumnWidth(100.0), FractionColumnWidth(0.1))

Both specifications are evaluated, so if either specification is expensive, so is this.

### MinColumnWidth()

```dart
MinColumnWidth(TableColumnWidth a, TableColumnWidth b)
```

Creates a column width that is the minimum of two other column widths.

### a

```dart
TableColumnWidth a
```

An upper bound for the width of this column.

### b

```dart
TableColumnWidth b
```

Another upper bound for the width of this column.

### minIntrinsicWidth()

```dart
double minIntrinsicWidth(Iterable<RenderBox> cells, double containerWidth)
```

### maxIntrinsicWidth()

```dart
double maxIntrinsicWidth(Iterable<RenderBox> cells, double containerWidth)
```

### flex()

```dart
double? flex(Iterable<RenderBox> cells)
```

### toString()

```dart
String toString()
```

# TableCellVerticalAlignment

```dart
enum TableCellVerticalAlignment {}
```

Vertical alignment options for cells in [RenderTable] objects.

This is specified using [TableCellParentData] objects on the [RenderObject.parentData] of the children of the [RenderTable].

Cells with this alignment are placed with their top at the top of the row.

Cells with this alignment are vertically centered in the row.

Cells with this alignment are placed with their bottom at the bottom of the row.

Cells with this alignment are aligned such that they all share the same baseline. Cells with no baseline are top-aligned instead. The baseline used is specified by [RenderTable.textBaseline]. It is not valid to use the baseline value if [RenderTable.textBaseline] is not specified.

This vertical alignment is relatively expensive because it causes the table to compute the baseline for each cell in the row.

Cells with this alignment are sized to be as tall as the row, then made to fit the row. If all the cells have this alignment, then the row will have zero height.

Cells with this alignment are sized to be the same height as the tallest cell in the row.

# RenderTable

```dart
class RenderTable extends RenderBox {}
```

A table where the columns and rows are sized to fit the contents of the cells.

### RenderTable()

```dart
RenderTable({int? columns, int? rows, Map<int, TableColumnWidth>? columnWidths, TableColumnWidth defaultColumnWidth = const FlexColumnWidth(), required TextDirection textDirection, TableBorder? border, List<Decoration?>? rowDecorations, ImageConfiguration configuration = ImageConfiguration.empty, TableCellVerticalAlignment defaultVerticalAlignment = TableCellVerticalAlignment.top, TextBaseline? textBaseline, List<List<RenderBox>>? children})
```

Creates a table render object.

- `columns` must either be null or non-negative. If `columns` is null, the number of columns will be inferred from length of the first sublist of `children`.
- `rows` must either be null or non-negative. If `rows` is null, the number of rows will be inferred from the `children`. If `rows` is not null, then `children` must be null.
- `children` must either be null or contain lists of all the same length. if `children` is not null, then `rows` must be null.
- [columnWidths] may be null, in which case it defaults to an empty map.

### columns

```dart
int get columns
```

The number of vertical alignment lines in this table.

Changing the number of columns will remove any children that no longer fit in the table.

Changing the number of columns is an expensive operation because the table needs to rearrange its internal representation.

### columns

```dart
set columns(int value)
```

### rows

```dart
int get rows
```

The number of horizontal alignment lines in this table.

Changing the number of rows will remove any children that no longer fit in the table.

### rows

```dart
set rows(int value)
```

### columnWidths

```dart
Map<int, TableColumnWidth>? get columnWidths
```

How the horizontal extents of the columns of this table should be determined.

If the [Map] has a null entry for a given column, the table uses the [defaultColumnWidth] instead.

The layout performance of the table depends critically on which column sizing algorithms are used here. In particular, [IntrinsicColumnWidth] is quite expensive because it needs to measure each cell in the column to determine the intrinsic size of the column.

This property can never return null. If it is set to null, and the existing map is not empty, then the value is replaced by an empty map. (If it is set to null while the current value is an empty map, the value is not changed.)

### columnWidths

```dart
set columnWidths(Map<int, TableColumnWidth>? value)
```

### setColumnWidth()

```dart
void setColumnWidth(int column, TableColumnWidth value)
```

Determines how the width of column with the given index is determined.

### defaultColumnWidth

```dart
TableColumnWidth get defaultColumnWidth
```

How to determine with widths of columns that don't have an explicit sizing algorithm.

Specifically, the [defaultColumnWidth] is used for column `i` if `columnWidths[i]` is null.

### defaultColumnWidth

```dart
set defaultColumnWidth(TableColumnWidth value)
```

### textDirection

```dart
TextDirection get textDirection
```

The direction in which the columns are ordered.

### textDirection

```dart
set textDirection(TextDirection value)
```

### border

```dart
TableBorder? get border
```

The style to use when painting the boundary and interior divisions of the table.

### border

```dart
set border(TableBorder? value)
```

### rowDecorations

```dart
List<Decoration?> get rowDecorations
```

The decorations to use for each row of the table.

Row decorations fill the horizontal and vertical extent of each row in the table, unlike decorations for individual cells, which might not fill either.

### rowDecorations

```dart
set rowDecorations(List<Decoration?>? value)
```

### configuration

```dart
ImageConfiguration get configuration
```

The settings to pass to the [rowDecorations] when painting, so that they can resolve images appropriately. See [ImageProvider.resolve] and [BoxPainter.paint].

### configuration

```dart
set configuration(ImageConfiguration value)
```

### defaultVerticalAlignment

```dart
TableCellVerticalAlignment get defaultVerticalAlignment
```

How cells that do not explicitly specify a vertical alignment are aligned vertically.

### defaultVerticalAlignment

```dart
set defaultVerticalAlignment(TableCellVerticalAlignment value)
```

### textBaseline

```dart
TextBaseline? get textBaseline
```

The text baseline to use when aligning rows using [TableCellVerticalAlignment.baseline].

### textBaseline

```dart
set textBaseline(TextBaseline? value)
```

### setupParentData()

```dart
void setupParentData(RenderObject child)
```

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

### clearSemantics()

```dart
void clearSemantics()
```

### assembleSemanticsNode()

```dart
void assembleSemanticsNode(SemanticsNode node, SemanticsConfiguration config, Iterable<SemanticsNode> children)
```

Provides custom semantics for tables by generating nodes for rows and maybe cells.

Table rows are not RenderObjects, so their semantics nodes must be created separately. And if a cell has multiple semantics node or has a different semantic role, we create a new semantics node to wrap it.

### setFlatChildren()

```dart
void setFlatChildren(int columns, List<RenderBox?> cells)
```

Replaces the children of this table with the given cells.

The cells are divided into the specified number of columns before replacing the existing children.

If the new cells contain any existing children of the table, those children are moved to their new location in the table rather than removed from the table and re-added.

### setChildren()

```dart
void setChildren(List<List<RenderBox>>? cells)
```

Replaces the children of this table with the given cells.

### addRow()

```dart
void addRow(List<RenderBox?> cells)
```

Adds a row to the end of the table.

The newly added children must not already have parents.

### setChild()

```dart
void setChild(int x, int y, RenderBox? value)
```

Replaces the child at the given position with the given child.

If the given child is already located at the given position, this function does not modify the table. Otherwise, the given child must not already have a parent.

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### visitChildren()

```dart
void visitChildren(RenderObjectVisitor visitor)
```

### redepthChildren()

```dart
void redepthChildren()
```

### computeMinIntrinsicWidth()

```dart
double computeMinIntrinsicWidth(double height)
```

### computeMaxIntrinsicWidth()

```dart
double computeMaxIntrinsicWidth(double height)
```

### computeMinIntrinsicHeight()

```dart
double computeMinIntrinsicHeight(double width)
```

### computeMaxIntrinsicHeight()

```dart
double computeMaxIntrinsicHeight(double width)
```

### computeDistanceToActualBaseline()

```dart
double? computeDistanceToActualBaseline(TextBaseline baseline)
```

### column()

```dart
Iterable<RenderBox> column(int x)
```

Returns the list of [RenderBox] objects that are in the given column, in row order, starting from the first row.

This is a lazily-evaluated iterable.

### row()

```dart
Iterable<RenderBox> row(int y)
```

Returns the list of [RenderBox] objects that are on the given row, in column order, starting with the first column.

This is a lazily-evaluated iterable.

### getRowBox()

```dart
Rect getRowBox(int row)
```

Returns the position and dimensions of the box that the given row covers, in this render object's coordinate space (so the left coordinate is always 0.0).

The row being queried must exist.

This is only valid after layout.

### computeDryBaseline()

```dart
double? computeDryBaseline(BoxConstraints constraints, TextBaseline baseline)
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### performLayout()

```dart
void performLayout()
```

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```
