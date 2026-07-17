# GridPaper

```dart
class GridPaper extends StatelessWidget {}
```

绘制一个由宽度为 1 像素的直线组成的矩形网格的 widget。

可与 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 搭配使用，用于沿网格可视化你的布局。

网格的原点（第一条主水平线与第一条主垂直线的交点）位于该 widget 的左上角。

网格绘制在 [child] widget 之上。

### GridPaper()

```dart
GridPaper({dynamic key, Color color = const Color(0x7FC3E8F3), double interval = 100.0, int divisions = 2, int subdivisions = 5, Widget? child})
```

创建一个绘制由宽度为 1 像素的直线组成的矩形网格的 widget。

### color

```dart
Color color
```

用于绘制网格线的颜色。

默认为传统方格纸上常见的浅蓝色。

### interval

```dart
double interval
```

网格中主线之间的距离，以逻辑像素为单位。

每条主线的宽度为 1 逻辑像素。

### divisions

```dart
int divisions
```

每个主网格单元内主要分区的数量。

即每个 [interval] 内的主要分区数量（包括主网格线本身）。

第一条线之后的线宽为半个逻辑像素。

如果此值设置为 2（默认值），则每个 [interval] 内会有：左侧 1 像素宽的线、中间半像素宽的线，以及右侧 1 像素宽的线（该线同时也是下一个 [interval] 左侧的 1 像素线）。

### subdivisions

```dart
int subdivisions
```

每个主要分区内次要分区的数量，包括主要分区本身。

如果 [subdivisions] 为 5（默认值），意味着每个主要（[divisions]）分区之间会有四条线。

第一条线之后的次要分区线宽为四分之一逻辑像素。

### child

```dart
Widget? child
```

此 widget 下方的 widget 树。

{@macro flutter.widgets.ProxyWidget.child}
