# GridPaper

```dart
class GridPaper extends StatelessWidget {}
```

A widget that draws a rectilinear grid of lines one pixel wide.

Useful with a [Stack] for visualizing your layout along a grid.

The grid's origin (where the first primary horizontal line and the first primary vertical line intersect) is at the top left of the widget.

The grid is drawn over the [child] widget.

### GridPaper()

```dart
GridPaper({dynamic key, Color color = const Color(0x7FC3E8F3), double interval = 100.0, int divisions = 2, int subdivisions = 5, Widget? child})
```

Creates a widget that draws a rectilinear grid of 1-pixel-wide lines.

### color

```dart
Color color
```

The color to draw the lines in the grid.

Defaults to a light blue commonly seen on traditional grid paper.

### interval

```dart
double interval
```

The distance between the primary lines in the grid, in logical pixels.

Each primary line is one logical pixel wide.

### divisions

```dart
int divisions
```

The number of major divisions within each primary grid cell.

This is the number of major divisions per [interval], including the primary grid's line.

The lines after the first are half a logical pixel wide.

If this is set to 2 (the default), then for each [interval] there will be a 1-pixel line on the left, a half-pixel line in the middle, and a 1-pixel line on the right (the latter being the 1-pixel line on the left of the next [interval]).

### subdivisions

```dart
int subdivisions
```

The number of minor divisions within each major division, including the major division itself.

If [subdivisions] is 5 (the default), it means that there will be four lines between each major ([divisions]) line.

The subdivision lines after the first are a quarter of a logical pixel wide.

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```
