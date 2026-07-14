# OffsetBase

```dart
abstract class OffsetBase {}
```

[Size](https://www.yuque.com/thyname/dart.ui/size) 和 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 的基类，这两者都是用于以二维轴对齐向量描述距离的方式。

### OffsetBase()

```dart
OffsetBase(double _dx, double _dy)
```

抽象的 const 构造函数。此构造函数使子类能够提供 const 构造函数，从而可以在 const 表达式中使用。

第一个参数设置水平分量，第二个参数设置垂直分量。

### isInfinite

```dart
bool get isInfinite
```

如果任一分量为 [double.infinity]，则返回 true；如果两个分量都是有限的（或为负无穷，或为 NaN），则返回 false。

这与判断两个分量是否都等于 [double.infinity] 的相等性比较不同。

另请参阅：

- [isFinite]，当两个分量都是有限值（且不为 NaN）时返回 true。

### isFinite

```dart
bool get isFinite
```

两个分量是否都是有限值（既非无穷大也非 NaN）。

另请参阅：

- [isInfinite]，当任一分量等于正无穷时返回 true。

### operator <()

```dart
bool operator <(OffsetBase other)
```

小于运算符。将一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 或 [Size](https://www.yuque.com/thyname/dart.ui/size) 与另一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 或 [Size](https://www.yuque.com/thyname/dart.ui/size) 进行比较，如果左操作数的水平值和垂直值分别都小于右操作数的水平值和垂直值，则返回 true。否则返回 false。

这是一种偏序关系。两个值有可能既不小于、不大于，也不等于另一个值。

### operator <=()

```dart
bool operator <=(OffsetBase other)
```

小于等于运算符。将一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 或 [Size](https://www.yuque.com/thyname/dart.ui/size) 与另一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 或 [Size](https://www.yuque.com/thyname/dart.ui/size) 进行比较，如果左操作数的水平值和垂直值分别都小于或等于右操作数的水平值和垂直值，则返回 true。否则返回 false。

这是一种偏序关系。两个值有可能既不小于、不大于，也不等于另一个值。

### operator >()

```dart
bool operator >(OffsetBase other)
```

大于运算符。将一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 或 [Size](https://www.yuque.com/thyname/dart.ui/size) 与另一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 或 [Size](https://www.yuque.com/thyname/dart.ui/size) 进行比较，如果左操作数的水平值和垂直值分别都大于右操作数的水平值和垂直值，则返回 true。否则返回 false。

这是一种偏序关系。两个值有可能既不小于、不大于，也不等于另一个值。

### operator >=()

```dart
bool operator >=(OffsetBase other)
```

大于等于运算符。将一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 或 [Size](https://www.yuque.com/thyname/dart.ui/size) 与另一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 或 [Size](https://www.yuque.com/thyname/dart.ui/size) 进行比较，如果左操作数的水平值和垂直值分别都大于或等于右操作数的水平值和垂直值，则返回 true。否则返回 false。

这是一种偏序关系。两个值有可能既不小于、不大于，也不等于另一个值。

### operator ==()

```dart
bool operator ==(Object other)
```

相等运算符。将一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 或 [Size](https://www.yuque.com/thyname/dart.ui/size) 与另一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 或 [Size](https://www.yuque.com/thyname/dart.ui/size) 进行比较，如果左操作数的水平值和垂直值分别与右操作数的水平值和垂直值相等，则返回 true。否则返回 false。

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# Offset

```dart
class Offset extends OffsetBase {}
```

一个不可变的二维浮点偏移量。

通常来说，Offset 可以用两种方式解释：

1.  表示笛卡尔空间中某一点相对于单独维护的原点的位置。例如，在 [RenderBox](https://www.yuque.com/thyname/flutter.rendering/renderbox) 协议中，子组件的左上角位置通常表示为相对于父级盒子左上角的一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset)。

2.  作为可应用于坐标的向量。例如，在绘制 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 时，会向父级传递一个相对于屏幕原点的 [Offset](https://www.yuque.com/thyname/dart.ui/offset)，父级可将其与子组件的偏移量相加，从而得到从屏幕原点到各子组件的 [Offset](https://www.yuque.com/thyname/dart.ui/offset)。

由于同一个特定的 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 可能在某一时刻按一种含义解释，而在之后的时刻按另一种含义解释，因此这两种含义使用同一个类来表示。

另请参阅：

- [Size](https://www.yuque.com/thyname/dart.ui/size)，表示描述矩形尺寸的向量。

### Offset()

```dart
Offset(double dx, double dy)
```

创建一个偏移量。第一个参数设置 [dx]（水平分量），第二个参数设置 [dy]（垂直分量）。

### Offset.fromDirection()

```dart
Offset.fromDirection(double direction, [double distance = 1.0])
```

根据 [direction]（方向）和 [distance]（距离）创建一个偏移量。

方向以弧度表示，从正 x 轴顺时针方向计算。

distance 参数可以省略，此时将创建一个单位向量（distance = 1.0）。

### dx

```dart
double get dx
```

偏移量的 x 分量。

y 分量由 [dy] 给出。

### dy

```dart
double get dy
```

偏移量的 y 分量。

x 分量由 [dx] 给出。

### distance

```dart
double get distance
```

偏移量的大小（模）。

如果需要用此值与另一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 的 distance 进行比较，建议改用 [distanceSquared]，因为它的计算成本更低。

### distanceSquared

```dart
double get distanceSquared
```

偏移量大小（模）的平方。

其计算成本比 [distance] 本身更低。

### direction

```dart
double get direction
```

此偏移量的角度，以弧度表示，从正 x 轴顺时针方向计算，取值范围为 -[pi] 到 [pi]，假设 x 轴正方向朝右，y 轴正方向朝下。

零表示 [dy] 为零且 [dx] 为零或正值。

从零到 [pi]/2 的值表示 [dx] 和 [dy] 均为正值，即右下象限。

从 [pi]/2 到 [pi] 的值表示 [dx] 为负值而 [dy] 为正值，即左下象限。

从零到 -[pi]/2 的值表示 [dx] 为正值而 [dy] 为负值，即右上象限。

从 -[pi]/2 到 -[pi] 的值表示 [dx] 和 [dy] 均为负值，即左上象限。

当 [dy] 为零且 [dx] 为负值时，[direction] 为 [pi]。

当 [dx] 为零时，若 [dy] 为正值，[direction] 为 [pi]/2；若 [dy] 为负值，则为 -[pi]/2。

另请参阅：

- [distance]，用于计算向量的大小。
- [Canvas.rotate]，其角度采用相同的约定。

### zero

```dart
Offset zero
```

一个大小为零的偏移量。

可用于表示坐标空间的原点。

### infinite

```dart
Offset infinite
```

x 和 y 分量均为无穷大的偏移量。

另请参阅：

- [isInfinite]，用于检查任一分量是否为无穷大。
- [isFinite]，用于检查两个分量是否都是有限值。

### scale()

```dart
Offset scale(double scaleX, double scaleY)
```

返回一个新的偏移量，其 x 分量按 `scaleX` 缩放，y 分量按 `scaleY` 缩放。

如果两个缩放参数相同，建议改用 `*` 运算符：

```dart
Offset a = const Offset(10.0, 10.0);
Offset b = a * 2.0; // 等同于：a.scale(2.0, 2.0)
```

如果两个参数均为 -1，建议改用一元 `-` 运算符：

```dart
Offset a = const Offset(10.0, 10.0);
Offset b = -a; // 等同于：a.scale(-1.0, -1.0)
```

### translate()

```dart
Offset translate(double translateX, double translateY)
```

返回一个新的偏移量，将 translateX 加到 x 分量上，将 translateY 加到 y 分量上。

如果参数来自另一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset)，建议改用 `+` 或 `-` 运算符：

```dart
Offset a = const Offset(10.0, 10.0);
Offset b = const Offset(10.0, 10.0);
Offset c = a + b; // 等同于：a.translate(b.dx, b.dy)
Offset d = a - b; // 等同于：a.translate(-b.dx, -b.dy)
```

### operator -()

```dart
Offset operator -()
```

一元取负运算符。

返回坐标取负后的偏移量。

如果该 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 表示平面上的一个箭头，此运算符返回指向相反方向的相同箭头。

### operator -()

```dart
Offset operator -(Offset other)
```

二元减法运算符。

返回一个偏移量，其 [dx] 值为左操作数的 [dx] 减去右操作数的 [dx]，其 [dy] 值为左操作数的 [dy] 减去右操作数的 [dy]。

另请参阅 [translate]。

### operator +()

```dart
Offset operator +(Offset other)
```

二元加法运算符。

返回一个偏移量，其 [dx] 值为两个操作数的 [dx] 值之和，其 [dy] 值为两个操作数的 [dy] 值之和。

另请参阅 [translate]。

### operator \*()

```dart
Offset operator *(double operand)
```

乘法运算符。

返回一个偏移量，其坐标为左操作数（一个 Offset）的坐标乘以标量右操作数（一个 double）。

另请参阅 [scale]。

### operator /()

```dart
Offset operator /(double operand)
```

除法运算符。

返回一个偏移量，其坐标为左操作数（一个 Offset）的坐标除以标量右操作数（一个 double）。

另请参阅 [scale]。

### operator ~/()

```dart
Offset operator ~/(double operand)
```

整除（向零取整）运算符。

返回一个偏移量，其坐标为左操作数（一个 Offset）的坐标除以标量右操作数（一个 double）并向零方向取整后的结果。

### operator %()

```dart
Offset operator %(double operand)
```

取模（求余）运算符。

返回一个偏移量，其坐标为左操作数（一个 Offset）的坐标除以标量右操作数（一个 double）的余数。

### operator &()

```dart
Rect operator &(Size other)
```

矩形构造运算符。

将一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 与一个 [Size](https://www.yuque.com/thyname/dart.ui/size) 组合成一个 [Rect](https://www.yuque.com/thyname/dart.ui/rect)，其左上角坐标为将左操作数（此偏移量）加到原点得到的点，其尺寸为右操作数。

```dart
Rect myRect = Offset.zero & const Size(100.0, 100.0);
// 等同于：Rect.fromLTWH(0.0, 0.0, 100.0, 100.0)
```

### lerp()

```dart
Offset? lerp(Offset? a, Offset? b, double t)
```

在两个偏移量之间进行线性插值。

如果任一偏移量为 null，此函数将从 [Offset.zero] 开始插值。

`t` 参数表示在时间线上的位置：0.0 表示插值尚未开始，返回 `a`（或与 `a` 等效的值）；1.0 表示插值已完成，返回 `b`（或与 `b` 等效的值）；介于两者之间的值表示插值位于 `a` 与 `b` 之间时间线上的相应位置。插值可外推到 0.0 和 1.0 之外，因此负值和大于 1.0 的值都是有效的（这类值很容易通过诸如 [Curves.elasticInOut] 之类的曲线生成）。

`t` 的值通常从 [Animation<double>]（例如 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)）获取。

### operator ==()

```dart
bool operator ==(Object other)
```

比较两个 Offset 是否相等。

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# Size

```dart
class Size extends OffsetBase {}
```

保存一个二维浮点尺寸。

可以将其视为从原点出发的一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset)。

### Size()

```dart
Size(double width, double height)
```

使用给定的 [width] 和 [height] 创建一个 [Size](https://www.yuque.com/thyname/dart.ui/size)。

### Size.copy()

```dart
Size.copy(Size source)
```

创建一个与另一个 [Size](https://www.yuque.com/thyname/dart.ui/size) 值相同的实例。

### Size.square()

```dart
Size.square(double dimension)
```

创建一个正方形 [Size](https://www.yuque.com/thyname/dart.ui/size)，其 [width] 和 [height] 均为给定的 dimension。

另请参阅：

- [Size.fromRadius]，当已知尺寸为圆的半径时使用更方便。

### Size.fromWidth()

```dart
Size.fromWidth(double width)
```

创建一个具有给定 [width] 且 [height] 为无穷大的 [Size](https://www.yuque.com/thyname/dart.ui/size)。

### Size.fromHeight()

```dart
Size.fromHeight(double height)
```

创建一个具有给定 [height] 且 [width] 为无穷大的 [Size](https://www.yuque.com/thyname/dart.ui/size)。

### Size.fromRadius()

```dart
Size.fromRadius(double radius)
```

创建一个正方形 [Size](https://www.yuque.com/thyname/dart.ui/size)，其 [width] 和 [height] 均为给定 dimension 的两倍。

这是一个包含给定半径的圆的正方形。

另请参阅：

- [Size.square]，用给定的边长创建一个正方形。

### width

```dart
double get width
```

此尺寸的水平范围。

### height

```dart
double get height
```

此尺寸的垂直范围。

### aspectRatio

```dart
double get aspectRatio
```

此尺寸的宽高比。

返回 [width] 除以 [height] 的结果。

如果 [width] 为零，结果将为零。如果 [height] 为零（而 [width] 不为零），结果将根据 [width] 的符号为 [double.infinity] 或 [double.negativeInfinity]。

另请参阅：

- [AspectRatio](https://www.yuque.com/thyname/flutter.widgets/aspectratio)，一个用于为子组件指定特定宽高比的组件。
- [FittedBox](https://www.yuque.com/thyname/flutter.widgets/fittedbox)，一个组件，在大多数模式下会尝试在改变子组件尺寸的同时保持其宽高比。

### zero

```dart
Size zero
```

一个空尺寸，宽度和高度均为零。

### infinite

```dart
Size infinite
```

[width] 和 [height] 均为无穷大的尺寸。

另请参阅：

- [isInfinite]，用于检查任一维度是否为无穷大。
- [isFinite]，用于检查两个维度是否都是有限值。

### isEmpty

```dart
bool get isEmpty
```

此尺寸的面积是否为零。

负面积会被视为空。

### operator -()

```dart
OffsetBase operator -(OffsetBase other)
```

[Size](https://www.yuque.com/thyname/dart.ui/size) 的二元减法运算符。

用一个 [Size](https://www.yuque.com/thyname/dart.ui/size) 减去另一个 [Size](https://www.yuque.com/thyname/dart.ui/size)，返回描述左操作数比右操作数大多少的 [Offset](https://www.yuque.com/thyname/dart.ui/offset)。将得到的 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 与作为右操作数的 [Size](https://www.yuque.com/thyname/dart.ui/size) 相加，会得到一个等于作为左操作数的 [Size](https://www.yuque.com/thyname/dart.ui/size) 的结果。（即，如果 `sizeA - sizeB -> offsetA`，那么 `offsetA + sizeB -> sizeA`）

用一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 减去一个 [Size](https://www.yuque.com/thyname/dart.ui/size)，返回一个比 [Size](https://www.yuque.com/thyname/dart.ui/size) 操作数小的 [Size](https://www.yuque.com/thyname/dart.ui/size)，差值由 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 操作数给出。换句话说，返回的 [Size](https://www.yuque.com/thyname/dart.ui/size) 的 [width] 为左操作数的 [width] 减去右操作数的 [Offset.dx] 维度，[height] 为左操作数的 [height] 减去右操作数的 [Offset.dy] 维度。

### operator +()

```dart
Size operator +(Offset other)
```

将 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 加到 [Size](https://www.yuque.com/thyname/dart.ui/size) 上的二元加法运算符。

返回一个 [Size](https://www.yuque.com/thyname/dart.ui/size)，其 [width] 为左操作数（一个 [Size](https://www.yuque.com/thyname/dart.ui/size)）的 [width] 与右操作数（一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset)）的 [Offset.dx] 维度之和，其 [height] 为左操作数的 [height] 与右操作数的 [Offset.dy] 维度之和。

### operator \*()

```dart
Size operator *(double operand)
```

乘法运算符。

返回一个 [Size](https://www.yuque.com/thyname/dart.ui/size)，其各维度为左操作数（一个 [Size](https://www.yuque.com/thyname/dart.ui/size)）的维度乘以标量右操作数（一个 [double](https://www.yuque.com/thyname/dart.core/double)）。

### operator /()

```dart
Size operator /(double operand)
```

除法运算符。

返回一个 [Size](https://www.yuque.com/thyname/dart.ui/size)，其各维度为左操作数（一个 [Size](https://www.yuque.com/thyname/dart.ui/size)）的维度除以标量右操作数（一个 [double](https://www.yuque.com/thyname/dart.core/double)）。

### operator ~/()

```dart
Size operator ~/(double operand)
```

整除（向零取整）运算符。

返回一个 [Size](https://www.yuque.com/thyname/dart.ui/size)，其各维度为左操作数（一个 [Size](https://www.yuque.com/thyname/dart.ui/size)）的维度除以标量右操作数（一个 [double](https://www.yuque.com/thyname/dart.core/double)）并向零方向取整后的结果。

### operator %()

```dart
Size operator %(double operand)
```

取模（求余）运算符。

返回一个 [Size](https://www.yuque.com/thyname/dart.ui/size)，其各维度为左操作数（一个 [Size](https://www.yuque.com/thyname/dart.ui/size)）除以标量右操作数（一个 [double](https://www.yuque.com/thyname/dart.core/double)）的余数。

### shortestSide

```dart
double get shortestSide
```

[width] 与 [height] 中数值较小的一个。

### longestSide

```dart
double get longestSide
```

[width] 与 [height] 中数值较大的一个。

### topLeft()

```dart
Offset topLeft(Offset origin)
```

由给定的 [Offset](https://www.yuque.com/thyname/dart.ui/offset)（视为左上角）和此 [Size](https://www.yuque.com/thyname/dart.ui/size) 所描述的矩形中，顶边与左边交点的偏移量。

另请参阅 [Rect.topLeft]。

### topCenter()

```dart
Offset topCenter(Offset origin)
```

由给定偏移量（视为左上角）和此尺寸所描述的矩形中，顶边中点的偏移量。

另请参阅 [Rect.topCenter]。

### topRight()

```dart
Offset topRight(Offset origin)
```

由给定偏移量（视为左上角）和此尺寸所描述的矩形中，顶边与右边交点的偏移量。

另请参阅 [Rect.topRight]。

### centerLeft()

```dart
Offset centerLeft(Offset origin)
```

由给定偏移量（视为左上角）和此尺寸所描述的矩形中，左边中点的偏移量。

另请参阅 [Rect.centerLeft]。

### center()

```dart
Offset center(Offset origin)
```

由给定偏移量（视为左上角）和此尺寸所描述的矩形中，左右边及上下边中间点的偏移量。

另请参阅 [Rect.center]。

### centerRight()

```dart
Offset centerRight(Offset origin)
```

由给定偏移量（视为左上角）和此尺寸所描述的矩形中，右边中点的偏移量。

另请参阅 [Rect.centerRight]。

### bottomLeft()

```dart
Offset bottomLeft(Offset origin)
```

由给定偏移量（视为左上角）和此尺寸所描述的矩形中，底边与左边交点的偏移量。

另请参阅 [Rect.bottomLeft]。

### bottomCenter()

```dart
Offset bottomCenter(Offset origin)
```

由给定偏移量（视为左上角）和此尺寸所描述的矩形中，底边中点的偏移量。

另请参阅 [Rect.bottomCenter]。

### bottomRight()

```dart
Offset bottomRight(Offset origin)
```

由给定偏移量（视为左上角）和此尺寸所描述的矩形中，底边与右边交点的偏移量。

另请参阅 [Rect.bottomRight]。

### contains()

```dart
bool contains(Offset offset)
```

由给定偏移量（假定相对于此尺寸的左上角）指定的点，是否位于矩形的左右边和上下边之间。

矩形包含其顶边和左边，但不包含其底边和右边。

### flipped

```dart
Size get flipped
```

一个 [width] 和 [height] 互换后的 [Size](https://www.yuque.com/thyname/dart.ui/size)。

### lerp()

```dart
Size? lerp(Size? a, Size? b, double t)
```

在两个尺寸之间进行线性插值

如果任一尺寸为 null，此函数将从 [Size.zero] 开始插值。

`t` 参数表示在时间线上的位置：0.0 表示插值尚未开始，返回 `a`（或与 `a` 等效的值）；1.0 表示插值已完成，返回 `b`（或与 `b` 等效的值）；介于两者之间的值表示插值位于 `a` 与 `b` 之间时间线上的相应位置。插值可外推到 0.0 和 1.0 之外，因此负值和大于 1.0 的值都是有效的（这类值很容易通过诸如 [Curves.elasticInOut] 之类的曲线生成）。

`t` 的值通常从 [Animation<double>]（例如 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)）获取。

### operator ==()

```dart
bool operator ==(Object other)
```

比较两个 Size 是否相等。

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# Rect

```dart
class Rect {}
```

一个不可变的二维轴对齐浮点矩形，其坐标相对于给定的原点。

可以使用 Rect 的某个构造函数创建它，也可以使用 `&` 运算符从 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 和 [Size](https://www.yuque.com/thyname/dart.ui/size) 创建：

```dart
Rect myRect = const Offset(1.0, 2.0) & const Size(3.0, 4.0);
```

### Rect.fromLTRB()

```dart
Rect.fromLTRB(double left, double top, double right, double bottom)
```

根据矩形的左边、顶边、右边和底边构造矩形。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_ltrb.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_ltrb_dark.png#gh-dark-mode-only)

### Rect.fromLTWH()

```dart
Rect.fromLTWH(double left, double top, double width, double height)
```

根据矩形的左边、顶边、宽度和高度构造矩形。

要从一个 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 和一个 [Size](https://www.yuque.com/thyname/dart.ui/size) 构造 [Rect](https://www.yuque.com/thyname/dart.ui/rect)，可以使用矩形构造运算符 `&`。参见 [Offset.&]。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_ltwh.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_ltwh_dark.png#gh-dark-mode-only)

### Rect.fromCircle()

```dart
Rect.fromCircle({required Offset center, required double radius})
```

构造一个包围给定圆的矩形。

`center` 参数被假定为相对于原点的偏移量。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_circle.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_circle_dark.png#gh-dark-mode-only)

### Rect.fromCenter()

```dart
Rect.fromCenter({required Offset center, required double width, required double height})
```

根据矩形的中心点、宽度和高度构造矩形。

`center` 参数被假定为相对于原点的偏移量。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_center.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_center_dark.png#gh-dark-mode-only)

### Rect.fromPoints()

```dart
Rect.fromPoints(Offset a, Offset b)
```

构造能包含给定偏移量（视为相对于原点的向量）的最小矩形。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_points.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_points_dark.png#gh-dark-mode-only)

### left

```dart
double left
```

此矩形左边相对于 x 轴的偏移。

### top

```dart
double top
```

此矩形顶边相对于 y 轴的偏移。

### right

```dart
double right
```

此矩形右边相对于 x 轴的偏移。

### bottom

```dart
double bottom
```

此矩形底边相对于 y 轴的偏移。

### width

```dart
double get width
```

此矩形左边与右边之间的距离。

### height

```dart
double get height
```

此矩形顶边与底边之间的距离。

### size

```dart
Size get size
```

此矩形左上角与右下角之间的距离。

### hasNaN

```dart
bool get hasNaN
```

是否有任一维度为 `NaN`。

### zero

```dart
Rect zero
```

左边、顶边、右边和底边均为零的矩形。

### largest

```dart
Rect largest
```

覆盖整个坐标空间的矩形。

其覆盖范围为 -1e9,-1e9 到 1e9,1e9。这是图形操作有效的空间范围。

### isInfinite

```dart
bool get isInfinite
```

此矩形的坐标中是否有任一等于正无穷。

### isFinite

```dart
bool get isFinite
```

此矩形的所有坐标是否都是有限值。

### isEmpty

```dart
bool get isEmpty
```

此矩形所包围的面积是否为非零值。负面积会被视为空。

### shift()

```dart
Rect shift(Offset offset)
```

返回一个按给定偏移量平移后的新矩形。

若要按单独的 x 和 y 分量而非按 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 平移矩形，可考虑使用 [translate]。

### translate()

```dart
Rect translate(double translateX, double translateY)
```

返回一个新矩形，其 x 分量加上 translateX，y 分量加上 translateY。

若要按 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 而非单独的 x、y 分量平移矩形，可考虑使用 [shift]。

### inflate()

```dart
Rect inflate(double delta)
```

返回一个各边向外移动给定 delta 值后的新矩形。

### deflate()

```dart
Rect deflate(double delta)
```

返回一个各边向内移动给定 delta 值后的新矩形。

### intersect()

```dart
Rect intersect(Rect other)
```

返回给定矩形与此矩形的交集所构成的新矩形。这两个矩形必须重叠，此操作才有意义。如果两个矩形不重叠，则结果 Rect 的宽度或高度将为负值。

### expandToInclude()

```dart
Rect expandToInclude(Rect other)
```

返回一个包含此矩形和给定矩形的边界框构成的新矩形。

### overlaps()

```dart
bool overlaps(Rect other)
```

`other` 与此矩形是否存在非零面积的重叠。

### shortestSide

```dart
double get shortestSide
```

此矩形的 [width] 与 [height] 中数值较小的一个。

### longestSide

```dart
double get longestSide
```

此矩形的 [width] 与 [height] 中数值较大的一个。

### topLeft

```dart
Offset get topLeft
```

此矩形顶边与左边交点的偏移量。

另请参阅 [Size.topLeft]。

### topCenter

```dart
Offset get topCenter
```

此矩形顶边中点的偏移量。

另请参阅 [Size.topCenter]。

### topRight

```dart
Offset get topRight
```

此矩形顶边与右边交点的偏移量。

另请参阅 [Size.topRight]。

### centerLeft

```dart
Offset get centerLeft
```

此矩形左边中点的偏移量。

另请参阅 [Size.centerLeft]。

### center

```dart
Offset get center
```

此矩形左右边及上下边中间点的偏移量。

另请参阅 [Size.center]。

### centerRight

```dart
Offset get centerRight
```

此矩形右边中点的偏移量。

另请参阅 [Size.centerRight]。

### bottomLeft

```dart
Offset get bottomLeft
```

此矩形底边与左边交点的偏移量。

另请参阅 [Size.bottomLeft]。

### bottomCenter

```dart
Offset get bottomCenter
```

此矩形底边中点的偏移量。

另请参阅 [Size.bottomCenter]。

### bottomRight

```dart
Offset get bottomRight
```

此矩形底边与右边交点的偏移量。

另请参阅 [Size.bottomRight]。

### contains()

```dart
bool contains(Offset offset)
```

由给定偏移量（假定相对于原点）指定的点，是否位于此矩形的左右边和上下边之间。

矩形包含其顶边和左边，但不包含其底边和右边。

### lerp()

```dart
Rect? lerp(Rect? a, Rect? b, double t)
```

在两个矩形之间进行线性插值。

如果任一矩形为 null，则使用 [Rect.zero] 作为替代。

`t` 参数表示在时间线上的位置：0.0 表示插值尚未开始，返回 `a`（或与 `a` 等效的值）；1.0 表示插值已完成，返回 `b`（或与 `b` 等效的值）；介于两者之间的值表示插值位于 `a` 与 `b` 之间时间线上的相应位置。插值可外推到 0.0 和 1.0 之外，因此负值和大于 1.0 的值都是有效的（这类值很容易通过诸如 [Curves.elasticInOut] 之类的曲线生成）。

`t` 的值通常从 [Animation<double>]（例如 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)）获取。

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# Radius

```dart
class Radius {}
```

用于圆形或椭圆形状的半径。

### Radius.circular()

```dart
Radius.circular(double radius)
```

构造一个圆形半径。[x] 和 [y] 的半径值相同。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/radius_circular.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/radius_circular_dark.png#gh-dark-mode-only)

### Radius.elliptical()

```dart
Radius.elliptical(double x, double y)
```

用给定的半径构造一个椭圆形半径。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/radius_elliptical.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/radius_elliptical_dark.png#gh-dark-mode-only)

### x

```dart
double x
```

水平轴上的半径值。

### y

```dart
double y
```

垂直轴上的半径值。

### zero

```dart
Radius zero
```

[x] 和 [y] 值均为零的半径。

可将 [Radius.zero] 与 [RRect](https://www.yuque.com/thyname/dart.ui/rrect) 或 [RSuperellipse](https://www.yuque.com/thyname/dart.ui/rsuperellipse) 搭配使用，以得到直角边角。

### clamp()

```dart
Radius clamp({Radius? minimum, Radius? maximum})
```

返回此 [Radius](https://www.yuque.com/thyname/dart.ui/radius) 的值在给定的最小和最大 [Radius](https://www.yuque.com/thyname/dart.ui/radius) 值范围内进行限制后的结果。

`min` 值默认为 `Radius.circular(-double.infinity)`，`max` 值默认为 `Radius.circular(double.infinity)`。

### clampValues()

```dart
Radius clampValues({double? minimumX, double? minimumY, double? maximumX, double? maximumY})
```

返回此 [Radius](https://www.yuque.com/thyname/dart.ui/radius) 的值在各维度上按给定的最小值和最大值进行限制后的结果

`minimumX` 和 `minimumY` 默认为 `-double.infinity`，`maximumX` 和 `maximumY` 默认为 `double.infinity`。

### operator -()

```dart
Radius operator -()
```

一元取负运算符。

返回距离取负后的 Radius。

具有负值的 Radius 在几何上没有意义，但可能作为表达式的一部分出现。例如，将一个像素的半径取负后再加到另一个半径上，等同于从另一个半径中减去一个像素的半径。

### operator -()

```dart
Radius operator -(Radius other)
```

二元减法运算符。

返回一个半径，其 [x] 值为左操作数的 [x] 减去右操作数的 [x]，其 [y] 值为左操作数的 [y] 减去右操作数的 [y]。

### operator +()

```dart
Radius operator +(Radius other)
```

二元加法运算符。

返回一个半径，其 [x] 值为两个操作数的 [x] 值之和，其 [y] 值为两个操作数的 [y] 值之和。

### operator \*()

```dart
Radius operator *(double operand)
```

乘法运算符。

返回一个半径，其坐标为左操作数（一个半径）的坐标乘以标量右操作数（一个 double）。

### operator /()

```dart
Radius operator /(double operand)
```

除法运算符。

返回一个半径，其坐标为左操作数（一个半径）的坐标除以标量右操作数（一个 double）。

### operator ~/()

```dart
Radius operator ~/(double operand)
```

整除（向零取整）运算符。

返回一个半径，其坐标为左操作数（一个半径）的坐标除以标量右操作数（一个 double）并向零方向取整后的结果。

### operator %()

```dart
Radius operator %(double operand)
```

取模（求余）运算符。

返回一个半径，其坐标为左操作数（一个半径）除以标量右操作数（一个 double）的余数。

### lerp()

```dart
Radius? lerp(Radius? a, Radius? b, double t)
```

在两个半径之间进行线性插值。

如果任一值为 null，此函数将改用 [Radius.zero] 替代。

`t` 参数表示在时间线上的位置：0.0 表示插值尚未开始，返回 `a`（或与 `a` 等效的值）；1.0 表示插值已完成，返回 `b`（或与 `b` 等效的值）；介于两者之间的值表示插值位于 `a` 与 `b` 之间时间线上的相应位置。插值可外推到 0.0 和 1.0 之外，因此负值和大于 1.0 的值都是有效的（这类值很容易通过诸如 [Curves.elasticInOut] 之类的曲线生成）。

`t` 的值通常从 [Animation<double>]（例如 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)）获取。

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# RRect

```dart
class RRect extends _RRectLike<RRect> {}
```

一个具有四个圆角自定义半径的不可变圆角矩形。

### RRect.fromLTRBXY()

```dart
RRect.fromLTRBXY(double left, double top, double right, double bottom, double radiusX, double radiusY)
```

根据矩形的左边、顶边、右边、底边，以及沿水平轴和垂直轴的相同半径，构造一个圆角矩形。

若 `radiusX` 或 `radiusY` 为负值，将在调试模式下触发断言。

### RRect.fromLTRBR()

```dart
RRect.fromLTRBR(double left, double top, double right, double bottom, Radius radius)
```

根据矩形的左边、顶边、右边、底边，以及每个圆角相同的半径，构造一个圆角矩形。

若 `radius` 在 x 或 y 方向上为负值，将在调试模式下触发断言。

### RRect.fromRectXY()

```dart
RRect.fromRectXY(Rect rect, double radiusX, double radiusY)
```

根据矩形的边界框，以及沿水平轴和垂直轴的相同半径，构造一个圆角矩形。

若 `radiusX` 或 `radiusY` 为负值，将在调试模式下触发断言。

### RRect.fromRectAndRadius()

```dart
RRect.fromRectAndRadius(Rect rect, Radius radius)
```

根据矩形的边界框，以及每个圆角相同的半径，构造一个圆角矩形。

若 `radius` 在 x 或 y 方向上为负值，将在调试模式下触发断言。

### RRect.fromLTRBAndCorners()

```dart
RRect.fromLTRBAndCorners(double left, double top, double right, double bottom, {Radius topLeft = Radius.zero, Radius topRight = Radius.zero, Radius bottomRight = Radius.zero, Radius bottomLeft = Radius.zero})
```

根据矩形的左边、顶边、右边、底边，以及 topLeft、topRight、bottomRight 和 bottomLeft 半径，构造一个圆角矩形。

各圆角半径默认为 [Radius.zero]，即直角。若任一半径在 x 或 y 方向上为负值，将在调试模式下触发断言。

### RRect.fromRectAndCorners()

```dart
RRect.fromRectAndCorners(Rect rect, {Radius topLeft = Radius.zero, Radius topRight = Radius.zero, Radius bottomRight = Radius.zero, Radius bottomLeft = Radius.zero})
```

根据矩形的边界框，以及 topLeft、topRight、bottomRight 和 bottomLeft 半径，构造一个圆角矩形。

各圆角半径默认为 [Radius.zero]，即直角。若任一半径在 x 或 y 方向上为负值，将在调试模式下触发断言。

### zero

```dart
RRect zero
```

所有值均为零的圆角矩形。

### contains()

```dart
bool contains(Offset point)
```

由给定偏移量（假定相对于原点）指定的点是否位于此圆角矩形内部。

此方法可能会分配（并缓存）一个具有规范化半径的对象副本，且仅在特定 [RRect](https://www.yuque.com/thyname/dart.ui/rrect) 实例首次调用此方法时进行。使用此方法时，建议复用现有的 [RRect](https://www.yuque.com/thyname/dart.ui/rrect)，而不是每次都重新创建对象。

### lerp()

```dart
RRect? lerp(RRect? a, RRect? b, double t)
```

在两个圆角矩形之间进行线性插值。

如果任一值为 null，此函数将改用 [RRect.zero] 替代。

`t` 参数表示在时间线上的位置：0.0 表示插值尚未开始，返回 `a`（或与 `a` 等效的值）；1.0 表示插值已完成，返回 `b`（或与 `b` 等效的值）；介于两者之间的值表示插值位于 `a` 与 `b` 之间时间线上的相应位置。插值可外推到 0.0 和 1.0 之外，因此负值和大于 1.0 的值都是有效的（这类值很容易通过诸如 [Curves.elasticInOut] 之类的曲线生成）。

`t` 的值通常从 [Animation<double>]（例如 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)）获取。

### toString()

```dart
String toString()
```

# RSuperellipse

```dart
class RSuperellipse extends _RRectLike<RSuperellipse> {}
```

一个不可变的圆角超椭圆。

圆角超椭圆（不要与标准超椭圆混淆）是一种通过将超椭圆的四个弯曲圆角替换为圆弧而形成的形状。（标准）超椭圆遵循公式 x^n + y^n = a^n，虽然 n > 2 会使其具有圆角，但这些圆角往往过于尖锐和明显。用圆弧替换它们能使形状显得更柔和、更自然。

从视觉上看，圆角超椭圆与常见的圆角矩形（[RRect](https://www.yuque.com/thyname/dart.ui/rrect)）相似，但直边与圆角之间的过渡更加平滑。它与 SwiftUI 中采用 `.continuous` 圆角样式的 `RoundedRectangle` 形状非常接近。

### RSuperellipse.fromLTRBXY()

```dart
RSuperellipse.fromLTRBXY(double left, double top, double right, double bottom, double radiusX, double radiusY)
```

根据矩形的左边、顶边、右边、底边，以及沿水平轴和垂直轴的相同半径，构造一个圆角矩形。

若 `radiusX` 或 `radiusY` 为负值，将在调试模式下触发断言。

### RSuperellipse.fromLTRBR()

```dart
RSuperellipse.fromLTRBR(double left, double top, double right, double bottom, Radius radius)
```

根据矩形的左边、顶边、右边、底边，以及每个圆角相同的半径，构造一个圆角矩形。

若 `radius` 在 x 或 y 方向上为负值，将在调试模式下触发断言。

### RSuperellipse.fromRectXY()

```dart
RSuperellipse.fromRectXY(Rect rect, double radiusX, double radiusY)
```

根据矩形的边界框，以及沿水平轴和垂直轴的相同半径，构造一个圆角矩形。

若 `radiusX` 或 `radiusY` 为负值，将在调试模式下触发断言。

### RSuperellipse.fromRectAndRadius()

```dart
RSuperellipse.fromRectAndRadius(Rect rect, Radius radius)
```

根据矩形的边界框，以及每个圆角相同的半径，构造一个圆角矩形。

若 `radius` 在 x 或 y 方向上为负值，将在调试模式下触发断言。

### RSuperellipse.fromLTRBAndCorners()

```dart
RSuperellipse.fromLTRBAndCorners(double left, double top, double right, double bottom, {Radius topLeft = Radius.zero, Radius topRight = Radius.zero, Radius bottomRight = Radius.zero, Radius bottomLeft = Radius.zero})
```

根据矩形的左边、顶边、右边、底边，以及 topLeft、topRight、bottomRight 和 bottomLeft 半径，构造一个圆角矩形。

各圆角半径默认为 [Radius.zero]，即直角。若任一半径在 x 或 y 方向上为负值，将在调试模式下触发断言。

### RSuperellipse.fromRectAndCorners()

```dart
RSuperellipse.fromRectAndCorners(Rect rect, {Radius topLeft = Radius.zero, Radius topRight = Radius.zero, Radius bottomRight = Radius.zero, Radius bottomLeft = Radius.zero})
```

根据矩形的边界框，以及 topLeft、topRight、bottomRight 和 bottomLeft 半径，构造一个圆角矩形。

各圆角半径默认为 [Radius.zero]，即直角。若任一半径在 x 或 y 方向上为负值，将在调试模式下触发断言。

### contains()

```dart
bool contains(Offset point)
```

由给定偏移量（假定相对于原点）指定的点是否位于此圆角超椭圆内部。

### zero

```dart
RSuperellipse zero
```

所有值均为零的圆角矩形。

### lerp()

```dart
RSuperellipse? lerp(RSuperellipse? a, RSuperellipse? b, double t)
```

在两个圆角超椭圆之间进行线性插值。

如果任一值为 null，此函数将改用 [RSuperellipse.zero] 替代。

`t` 参数表示在时间线上的位置：0.0 表示插值尚未开始，返回 `a`（或与 `a` 等效的值）；1.0 表示插值已完成，返回 `b`（或与 `b` 等效的值）；介于两者之间的值表示插值位于 `a` 与 `b` 之间时间线上的相应位置。插值可外推到 0.0 和 1.0 之外，因此负值和大于 1.0 的值都是有效的（这类值很容易通过诸如 [Curves.elasticInOut] 之类的曲线生成）。

`t` 的值通常从 [Animation<double>]（例如 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)）获取。

### toString()

```dart
String toString()
```

# RSTransform

```dart
class RSTransform {}
```

一个由平移、旋转和统一缩放组成的变换。

被 [Canvas.drawAtlas] 使用。相比完整矩阵，这是一种表示这些简单变换更高效的方式。

### RSTransform()

```dart
RSTransform(double scos, double ssin, double tx, double ty)
```

创建一个 RSTransform。

一个 [RSTransform](https://www.yuque.com/thyname/dart.ui/rstransform) 表示平移、绕特定点的旋转与缩放系数的组合。

第一个参数 `scos` 是旋转角的余弦值乘以缩放系数。

第二个参数 `ssin` 是旋转角的正弦值乘以相同的缩放系数。

第三个参数是平移的 x 坐标，减去 `scos` 参数乘以旋转点 x 坐标的值，再加上 `ssin` 参数乘以旋转点 y 坐标的值。

第四个参数是平移的 y 坐标，减去 `ssin` 参数乘以旋转点 x 坐标的值，再减去 `scos` 参数乘以旋转点 y 坐标的值。

[RSTransform.fromComponents] 方法可能是构造这些值的更简单方式。但是，如果有办法将旋转的正弦和余弦计算提取出来，以便在多次调用此构造函数时复用，那么直接使用此构造函数可能效率更高。

### RSTransform.fromComponents()

```dart
RSTransform.fromComponents({required double rotation, required double scale, required double anchorX, required double anchorY, required double translateX, required double translateY})
```

根据各个分量创建一个 RSTransform。

`rotation` 参数以弧度给出旋转角度。

`scale` 参数描述统一缩放系数。

`anchorX` 和 `anchorY` 参数给出旋转所绕点的坐标。

`translateX` 和 `translateY` 参数给出平移偏移量的坐标。

此构造函数计算出 [RSTransform.new] 构造函数所需的参数，然后委托该构造函数实际创建对象。如果需要创建多个 [RSTransform](https://www.yuque.com/thyname/dart.ui/rstransform) 对象，并且有办法将旋转的正弦和余弦计算（每次调用此构造函数时都会计算）提取出来并在多个 [RSTransform](https://www.yuque.com/thyname/dart.ui/rstransform) 对象间复用，那么直接使用更直接的 [RSTransform.new] 构造函数可能效率更高。

### scos

```dart
double get scos
```

旋转角的余弦值乘以缩放系数。

### ssin

```dart
double get ssin
```

旋转角的正弦值乘以相同的缩放系数。

### tx

```dart
double get tx
```

平移的 x 坐标，减去 [scos] 乘以旋转点 x 坐标的值，再加上 [ssin] 乘以旋转点 y 坐标的值。

### ty

```dart
double get ty
```

平移的 y 坐标，减去 [ssin] 乘以旋转点 x 坐标的值，再减去 [scos] 乘以旋转点 y 坐标的值。
