@docImport 'package:flutter/material.dart';

# ParametricCurve

```dart
abstract class ParametricCurve<T> {}
```

一个抽象类，提供用于计算参数曲线的接口。

参数曲线将沿曲线的参数（因此得名）`t` 转换为该 `t` 值处曲线的值。曲线可以是任意维度的，但通常是一维、二维或三维曲线。

另请参阅：

- [Curve](https://www.yuque.com/thyname/flutter.animation/curve)，一种一维动画缓动曲线，起始于 0.0，结束于 1.0。
- [Curve2D](https://www.yuque.com/thyname/flutter.animation/curve2d)，一种将参数转换为二维点的参数曲线。

### ParametricCurve()

```dart
ParametricCurve()
```

抽象的 const 构造函数，使子类能够提供 const 构造函数，以便在 const 表达式中使用。

### transform()

```dart
T transform(double t)
```

返回曲线在点 `t` 处的值。

此方法在委托给 [transformInternal] 之前，会断言 t 处于 0 到 1 之间。

建议子类重写 [transformInternal] 而不是此函数，因为上述情况已在 [transform] 的默认实现中处理，该实现会将剩余逻辑委托给 [transformInternal]。

### transformInternal()

```dart
T transformInternal(double t)
```

返回曲线在点 `t` 处的值。

给定的参数值 `t` 将处于 0.0 到 1.0 之间（包含两端）。

# Curve

```dart
abstract class Curve extends ParametricCurve<double> {}
```

一种参数化的动画缓动曲线，即单位区间到单位区间的映射。

缓动曲线用于调整动画随时间变化的速率，使动画可以加速和减速，而不是以恒定速率运动。

[Curve](https://www.yuque.com/thyname/flutter.animation/curve) 必须将 t=0.0 映射为 0.0，将 t=1.0 映射为 1.0。

另请参阅：

- [Curves](https://www.yuque.com/thyname/flutter.animation/curves)，常用动画缓动曲线的集合。
- [CurveTween](https://www.yuque.com/thyname/flutter.animation/curvetween)，可用于将 [Curve](https://www.yuque.com/thyname/flutter.animation/curve) 应用于 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)。
- [Canvas.drawArc]，用于绘制圆弧，与缓动曲线无关。
- [Animatable](https://www.yuque.com/thyname/flutter.animation/animatable)，提供更灵活的接口，将分数值映射为任意值。

### Curve()

```dart
Curve()
```

抽象的 const 构造函数，使子类能够提供 const 构造函数，以便在 const 表达式中使用。

### transform()

```dart
double transform(double t)
```

返回曲线在点 `t` 处的值。

此函数必须确保以下几点：

- `t` 的值必须处于 0.0 到 1.0 之间
- `t`=0.0 和 `t`=1.0 必须分别映射为 0.0 和 1.0。

建议子类重写 [transformInternal] 而不是此函数，因为上述情况已在 [transform] 的默认实现中处理，该实现会将剩余逻辑委托给 [transformInternal]。

### flipped

```dart
Curve get flipped
```

返回一条新曲线，它是此曲线的反转（reversed inversion）。

这通常与 [CurvedAnimation.reverseCurve] 一起使用会很有用。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_bounce_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_flipped.mp4}

另请参阅：

- [FlippedCurve](https://www.yuque.com/thyname/flutter.animation/flippedcurve)，用于实现此获取器的类。
- [ReverseAnimation](https://www.yuque.com/thyname/flutter.animation/reverseanimation)，用于反转 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 而非 [Curve](https://www.yuque.com/thyname/flutter.animation/curve)。
- [CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation)，可以接受单独的曲线和反转曲线。

# SawTooth

```dart
class SawTooth extends Curve {}
```

一种在单位区间内重复给定次数的锯齿曲线。

该曲线在每次迭代中从 0.0 线性上升到 1.0，然后不连续地跌回 0.0。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_sawtooth.mp4}

### SawTooth()

```dart
SawTooth(int count)
```

创建一条锯齿曲线。

### count

```dart
int count
```

锯齿图案在单位区间内的重复次数。

# Interval

```dart
class Interval extends Curve {}
```

一种曲线，在 [begin] 之前保持为 0.0，然后（根据 [curve]）从 [begin] 处的 0.0 曲线变化到 [end] 处的 1.0，此后在 [end] 之后保持为 1.0。

[Interval](https://www.yuque.com/thyname/flutter.animation/interval) 可用于延迟动画。例如，一个六秒的动画如果使用 [begin] 设置为 0.5、[end] 设置为 1.0 的 [Interval](https://www.yuque.com/thyname/flutter.animation/interval)，实际上会变成一个延迟三秒后开始的三秒动画。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_interval.mp4}

### Interval()

```dart
Interval(double begin, double end, {Curve curve = Curves.linear})
```

创建一条区间曲线。

### begin

```dart
double begin
```

此区间为 0.0 的最大值。

从 t=0.0 到 t=[begin]，此区间的值为 0.0。

### end

```dart
double end
```

此区间为 1.0 的最小值。

从 t=[end] 到 t=1.0，此区间的值为 1.0。

### curve

```dart
Curve curve
```

在 [begin] 和 [end] 之间应用的曲线。

### transformInternal()

```dart
double transformInternal(double t)
```

### toString()

```dart
String toString()
```

# Split

```dart
class Split extends Curve {}
```

一种曲线，在 [split] 之前按照 [beginCurve] 变化，之后按照 [endCurve] 变化。

Split 曲线适用于组件必须跟踪用户手指（这需要线性动画）的情形，但手指释放后又可以使用 [endCurve] 参数指定的曲线来进行快速滑动（fling）的情形。在这种情况下，[split] 的值即为手指释放时刻的动画进度。

例如，如果 [split] 设置为 0.5，[beginCurve] 为 [Curves.linear]，[endCurve] 为 [Curves.easeOutCubic]，那么曲线的左下四分之一部分将是一条直线，而右上四分之一部分将包含整条 [Curves.easeOutCubic] 曲线。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_split.mp4}

### Split()

```dart
Split(double split, {Curve beginCurve = Curves.linear, Curve endCurve = Curves.easeOutCubic})
```

创建一条 split 曲线。

### split

```dart
double split
```

用于分隔 [beginCurve] 和 [endCurve] 的进度值。

在此值之前，曲线按照 [beginCurve] 变化；在此值之后，曲线按照 [endCurve] 变化。

当 t 恰好等于 `split` 时，曲线的值为 `split`。

必须处于 0 到 1.0 之间（包含两端）。

### beginCurve

```dart
Curve beginCurve
```

在到达 [split] 之前使用的曲线。

默认为 [Curves.linear]。

### endCurve

```dart
Curve endCurve
```

在到达 [split] 之后使用的曲线。

默认为 [Curves.easeOutCubic]。

### transform()

```dart
double transform(double t)
```

### toString()

```dart
String toString()
```

# Threshold

```dart
class Threshold extends Curve {}
```

一种曲线，在到达阈值之前保持为 0.0，此后跳变为 1.0。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_threshold.mp4}

### Threshold()

```dart
Threshold(double threshold)
```

创建一条阈值曲线。

### threshold

```dart
double threshold
```

在此值之前，曲线为 0.0；在此值之后，曲线为 1.0。

当 t 恰好等于 [threshold] 时，曲线的值为 1.0。

### transformInternal()

```dart
double transformInternal(double t)
```

# Cubic

```dart
class Cubic extends Curve {}
```

单位区间的三次多项式映射。

[Curves](https://www.yuque.com/thyname/flutter.animation/curves) 类包含一些常用的三次曲线：

- [Curves.fastLinearToSlowEaseIn]
- [Curves.ease]
- [Curves.easeIn]
- [Curves.easeInToLinear]
- [Curves.easeInSine]
- [Curves.easeInQuad]
- [Curves.easeInCubic]
- [Curves.easeInQuart]
- [Curves.easeInQuint]
- [Curves.easeInExpo]
- [Curves.easeInCirc]
- [Curves.easeInBack]
- [Curves.easeOut]
- [Curves.linearToEaseOut]
- [Curves.easeOutSine]
- [Curves.easeOutQuad]
- [Curves.easeOutCubic]
- [Curves.easeOutQuart]
- [Curves.easeOutQuint]
- [Curves.easeOutExpo]
- [Curves.easeOutCirc]
- [Curves.easeOutBack]
- [Curves.easeInOut]
- [Curves.easeInOutSine]
- [Curves.easeInOutQuad]
- [Curves.easeInOutCubic]
- [Curves.easeInOutQuart]
- [Curves.easeInOutQuint]
- [Curves.easeInOutExpo]
- [Curves.easeInOutCirc]
- [Curves.easeInOutBack]
- [Curves.fastOutSlowIn]
- [Curves.slowMiddle]

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_fast_linear_to_slow_ease_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_to_linear.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_sine.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quad.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_cubic.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quart.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quint.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_expo.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_circ.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_back.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_linear_to_ease_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_sine.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quad.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_cubic.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quart.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quint.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_expo.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_circ.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_back.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_sine.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quad.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_cubic.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quart.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quint.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_expo.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_circ.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_back.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_fast_out_slow_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_slow_middle.mp4}

[Cubic](https://www.yuque.com/thyname/flutter.animation/cubic) 类实现了三阶贝塞尔曲线。

另请参阅：

- [Curves](https://www.yuque.com/thyname/flutter.animation/curves)，其中提供了更多预定义曲线。
- [CatmullRomCurve](https://www.yuque.com/thyname/flutter.animation/catmullromcurve)，一种经过特定值的曲线。

### Cubic()

```dart
Cubic(double a, double b, double c, double d)
```

创建一条三次曲线。

建议使用 [Curves](https://www.yuque.com/thyname/flutter.animation/curves) 中的常用三次曲线，而不是创建新实例。

### a

```dart
double a
```

第一个控制点的 x 坐标。

经过点 (0, 0) 和第一个控制点的直线，在点 (0, 0) 处与曲线相切。

### b

```dart
double b
```

第一个控制点的 y 坐标。

经过点 (0, 0) 和第一个控制点的直线，在点 (0, 0) 处与曲线相切。

### c

```dart
double c
```

第二个控制点的 x 坐标。

经过点 (1, 1) 和第二个控制点的直线，在点 (1, 1) 处与曲线相切。

### d

```dart
double d
```

第二个控制点的 y 坐标。

经过点 (1, 1) 和第二个控制点的直线，在点 (1, 1) 处与曲线相切。

### transformInternal()

```dart
double transformInternal(double t)
```

### toString()

```dart
String toString()
```

# ThreePointCubic

```dart
class ThreePointCubic extends Curve {}
```

由两条共享公共中心点的曲线组成的三次多项式。

该曲线经过三个点：(0,0)、[midpoint] 和 (1,1)。

[Curves](https://www.yuque.com/thyname/flutter.animation/curves) 类中包含一条使用此类定义的曲线：[Curves.easeInOutCubicEmphasized]。

[ThreePointCubic](https://www.yuque.com/thyname/flutter.animation/threepointcubic) 类实现了三阶贝塞尔曲线，其中两条曲线共享一个曲线所经过的内部 [midpoint]。如果围绕中间点的控制点（[b1] 和 [a2]）与中间点不共线，那么曲线的导数将在共享的中间点处出现不连续（一个尖点）。

另请参阅：

- [Curves](https://www.yuque.com/thyname/flutter.animation/curves)，其中提供了更多预定义曲线。
- [Cubic](https://www.yuque.com/thyname/flutter.animation/cubic)，用于定义单条三次多项式。
- [CatmullRomCurve](https://www.yuque.com/thyname/flutter.animation/catmullromcurve)，一种经过特定值的曲线。

### ThreePointCubic()

```dart
ThreePointCubic(Offset a1, Offset b1, Offset midpoint, Offset a2, Offset b2)
```

创建两条共享公共控制点的三次曲线。

建议使用 [Curves](https://www.yuque.com/thyname/flutter.animation/curves) 中的常用三点三次曲线，而不是创建新实例。

这些参数对应于两条曲线的控制点，包括 [midpoint]，但不包括固定的两个隐含端点 (0,0) 和 (1,1)。

### a1

```dart
Offset a1
```

第一条曲线的第一个控制点的坐标。

经过点 (0, 0) 和此控制点的直线，在点 (0, 0) 处与曲线相切。

### b1

```dart
Offset b1
```

第一条曲线的第二个控制点的坐标。

经过 [midpoint] 和此控制点的直线，在曲线接近 [midpoint] 处与曲线相切。

### midpoint

```dart
Offset midpoint
```

共享中间点的坐标。

曲线将经过此点。如果围绕此中间点的控制点（[b1] 和 [a2]）与此点不共线，那么曲线的导数将在此点处出现不连续（一个尖点）。

### a2

```dart
Offset a2
```

第二条曲线的第一个控制点的坐标。

经过 [midpoint] 和此控制点的直线，在曲线接近 [midpoint] 处与曲线相切。

### b2

```dart
Offset b2
```

第二条曲线的第二个控制点的坐标。

经过点 (1, 1) 和此控制点的直线，在点 (1, 1) 处与曲线相切。

### transformInternal()

```dart
double transformInternal(double t)
```

### toString()

```dart
String toString()
```

# Curve2D

```dart
abstract class Curve2D extends ParametricCurve<Offset> {}
```

定义了用于计算二维参数曲线的 API 的抽象类。

[Curve2D](https://www.yuque.com/thyname/flutter.animation/curve2d) 与 [Curve](https://www.yuque.com/thyname/flutter.animation/curve) 的不同之处在于，其插值得到的是 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 值而不是 [double](https://www.yuque.com/thyname/dart.core/double) 值，因此名称中带有 "2D"。两者都以单个范围为 0.0 到 1.0（包含两端）的 double 类型 `t` 作为 [transform] 函数的输入。与 [Curve](https://www.yuque.com/thyname/flutter.animation/curve) 不同，[Curve2D](https://www.yuque.com/thyname/flutter.animation/curve2d) 不要求将 `t=0.0` 和 `t=1.0` 映射为特定的输出值。

传递给 [transform] 的插值 `t` 值表示沿曲线的进度，但它不一定以恒定速度前进，因此根据曲线的定义，将 `t` 增加，比如说，0.1，在曲线的某一部分可能会沿曲线移动相当多，而在曲线的另一部分则几乎不移动。

{@tool dartpad} 此示例展示了如何使用 [Curve2D](https://www.yuque.com/thyname/flutter.animation/curve2d) 来修改组件的位置，使其可以沿任意路径移动。

** 参见代码：examples/api/lib/animation/curves/curve2_d.0.dart ** {@end-tool}

### Curve2D()

```dart
Curve2D()
```

抽象的 const 构造函数，使子类能够提供 const 构造函数，以便在 const 表达式中使用。

### generateSamples()

```dart
Iterable<Curve2DSample> generateSamples({double start = 0.0, double end = 1.0, double tolerance = 1e-10})
```

通过递归细分生成样本列表，直至达到 `tolerance` 所指定的容差。

样本按顺序生成。

样本可用于高效地渲染曲线，因为这些样本构成的线段大小会随曲线的曲率而变化。它们还可用于通过在 X 方向上搜索所需范围，并在样本之间进行线性插值，从而快速得到所需 X 值处 Y 的近似值，来快速逼近曲线的值。[CatmullRomCurve](https://www.yuque.com/thyname/flutter.animation/catmullromcurve) 的实现内部就是出于此目的使用样本的。

容差是通过新点与其前后相邻点所构成三角形的面积来计算的。

另请参阅：

- Luiz Henrique de Figueire 关于[该算法](http://ariel.chronotext.org/dd/defigueiredo93adaptive.pdf)的 Graphics Gem 文章。

### samplingSeed

```dart
int get samplingSeed
```

返回一个种子值，[generateSamples] 使用它为随机数生成器提供种子，以避免样本混叠。

子类应重写此项并提供自定义种子。

除非曲线定义发生变化，否则每次调用返回的值应保持一致。

### findInverse()

```dart
double findInverse(double x)
```

返回与样条曲线给定 x 值相对应的参数 `t`。

这仅对在 x 方向上单值的曲线（即每个 `x` 值仅映射到一个 'y' 值，也就是曲线不会自我循环或折返）才能正常工作。对于非单值曲线，它只会返回给定 `x` 位置处其中一个值所对应的参数。

# Curve2DSample

```dart
class Curve2DSample {}
```

一个用于保存二维参数曲线样本的类，包含曲线在参数值 [t] 处的 [value]（X、Y 坐标）。

另请参阅：

- [Curve2D.generateSamples]，用于生成此类型的样本。
- [Curve2D](https://www.yuque.com/thyname/flutter.animation/curve2d)，一种将 double 类型参数映射为二维位置的参数曲线。

### Curve2DSample()

```dart
Curve2DSample(double t, Offset value)
```

创建一个用于保存样本的对象；与 [Curve2D](https://www.yuque.com/thyname/flutter.animation/curve2d) 子类配合使用。

### t

```dart
double t
```

此样本点沿曲线的参数位置。

### value

```dart
Offset value
```

曲线在参数值 [t] 处的值（X、Y 坐标）。

### toString()

```dart
String toString()
```

# CatmullRomSpline

```dart
class CatmullRomSpline extends Curve2D {}
```

使用向心 Catmull-Rom 样条平滑经过给定控制点的二维样条曲线。

当使用 [transform] 计算该曲线时，输出值将平滑地从一个控制点移动到下一个控制点，并经过这些控制点。

{@template flutter.animation.CatmullRomSpline} 与大多数三次样条不同，Catmull-Rom 样条的优势在于其曲线会经过给定的控制点。它们是三次多项式表示，事实上，Catmull-Rom 样条在数学上可以转换为三次样条。此类实现了“向心”（centripetal）Catmull-Rom 样条。“向心”一词意味着它不会在单个线段内形成循环或自相交。{@endtemplate}

另请参阅：

- 维基百科上的[向心 Catmull-Rom 样条](https://en.wikipedia.org/wiki/Centripetal_Catmull%E2%80%93Rom_spline)。
- [Catmull-Rom 曲线的参数化及应用](http://faculty.cs.tamu.edu/schaefer/research/cr_cad.pdf)，一篇关于使用 Catmull-Rom 样条的论文。
- [CatmullRomCurve](https://www.yuque.com/thyname/flutter.animation/catmullromcurve)，一种以 [CatmullRomSpline](https://www.yuque.com/thyname/flutter.animation/catmullromspline) 作为内部表示的动画曲线。

### CatmullRomSpline()

```dart
CatmullRomSpline(List<Offset> controlPoints, {double tension = 0.0, Offset? startHandle, Offset? endHandle})
```

构造一条向心 Catmull-Rom 样条曲线。

`controlPoints` 参数是一个由四个或更多点组成的列表，描述了曲线必须经过的点。

可选的 `tension` 参数用于控制曲线逼近给定 `controlPoints` 的紧密程度。它必须处于 0.0 到 1.0 之间（包含两端）。默认值为 0.0，可提供最平滑的曲线。值为 1.0 时，会在各点之间产生线性插值。

可选的 `endHandle` 和 `startHandle` 点分别是起始和结束的控制柄位置。如果未指定，则会分别通过延伸 `controlPoints` 中第一条和/或最后一条线段所构成的直线来自动创建。样条不会经过这些控制柄点，但它们会影响样条起点和终点处直线的斜率。样条将尝试匹配由起始或结束控制柄与相邻的第一个或最后一个控制点所构成直线的斜率。默认值的选择方式，使得两端直线的斜率与控制点中第一条或最后一条线段的斜率相匹配。

内部曲线数据结构会在首次调用 [transform] 时惰性计算。如果你希望预先计算这些结构，请改用 [CatmullRomSpline.precompute]。

### CatmullRomSpline.precompute()

```dart
CatmullRomSpline.precompute(List<Offset> controlPoints, {double tension = 0.0, Offset? startHandle, Offset? endHandle})
```

构造一条向心 Catmull-Rom 样条曲线。

与 [CatmullRomSpline.new] 相同，只是内部数据结构是预先计算好的，而不是惰性计算。

### samplingSeed

```dart
int get samplingSeed
```

### transformInternal()

```dart
Offset transformInternal(double t)
```

# CatmullRomCurve

```dart
class CatmullRomCurve extends Curve {}
```

一种动画缓动曲线，使用向心 Catmull-Rom 样条平滑经过给定的控制点。

当使用 [transform] 计算此曲线时，其值将平滑地从一个控制点插值到下一个控制点，依次经过 (0.0, 0.0)、给定的各点，然后是 (1.0, 1.0)。

{@macro flutter.animation.CatmullRomSpline}

此类使用向心 Catmull-Rom 曲线（即 [CatmullRomSpline](https://www.yuque.com/thyname/flutter.animation/catmullromspline)）作为其内部表示。“向心”一词意味着它不会在单个线段内形成循环或自相交，对应于 Catmull-Rom α（alpha）值为 0.5 的情形。

另请参阅：

- [CatmullRomSpline](https://www.yuque.com/thyname/flutter.animation/catmullromspline)，此曲线用于生成其值的二维样条。
- 维基百科上一篇关于[向心 Catmull-Rom 样条](https://en.wikipedia.org/wiki/Centripetal_Catmull%E2%80%93Rom_spline)的文章。
- [CatmullRomCurve.new]，其中描述了对输入控制点的约束条件。
- 这篇[关于使用 Catmull-Rom 样条的论文](http://faculty.cs.tamu.edu/schaefer/research/cr_cad.pdf)。

### CatmullRomCurve()

```dart
CatmullRomCurve(List<Offset> controlPoints, {double tension = 0.0})
```

构造一条向心 [CatmullRomCurve](https://www.yuque.com/thyname/flutter.animation/catmullromcurve)。

它接受一个由两个或更多点组成的列表，描述曲线必须经过的点。关于对控制点所施加限制的说明，请参见 [controlPoints]。除了给定的 [controlPoints] 之外，曲线还会以 (0.0, 0.0) 处的隐式控制点开始，并以 (1.0, 1.0) 处的隐式控制点结束，从而使曲线在这些点处开始和结束。

可选的 [tension] 参数用于控制曲线逼近给定 `controlPoints` 的紧密程度。它必须处于 0.0 到 1.0 之间（包含两端）。默认值为 0.0，可提供最平滑的曲线。值为 1.0 时相当于在各点之间进行线性插值。

内部曲线数据结构会在首次调用 [transform] 时惰性计算。如果你希望预先计算此曲线，请改用 [CatmullRomCurve.precompute]。

另请参阅：

- 这篇[关于使用 Catmull-Rom 样条的论文](http://faculty.cs.tamu.edu/schaefer/research/cr_cad.pdf)。

### CatmullRomCurve.precompute()

```dart
CatmullRomCurve.precompute(List<Offset> controlPoints, {double tension = 0.0})
```

构造一条向心 [CatmullRomCurve](https://www.yuque.com/thyname/flutter.animation/catmullromcurve)。

与 [CatmullRomCurve.new] 相同，但它会预先计算内部曲线数据结构，以获得更可预测的计算负载。

### controlPoints

```dart
List<Offset> controlPoints
```

用于创建此曲线的控制点。

[controlPoints] 中每个 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 的 `dx` 值表示曲线应经过同一控制点 `dy` 值时所对应的动画值。

[controlPoints] 列表必须满足以下条件：

- 该列表必须至少包含两个点。
- 每个点的 X 值必须大于 0.0 且小于 1.0。
- 每个点的 X 值必须大于前一个点的 X 值（即单调递增）。Y 值不受限制。
- 生成的样条在 X 方向上必须是单值的。也就是说，对于每个 X 值，必须恰好对应一个 Y 值。这意味着这些控制点不能生成会自我循环或重叠的样条。

静态函数 [validateControlPoints] 可用于检查是否满足这些条件，如果满足则返回 true。在调试模式下，它还可以选择以文本形式返回原因列表。在调试模式下，构造函数会断言这些条件已满足，若断言失败则会打印相应原因。

当使用 [transform] 计算此曲线时，其值将平滑地从一个控制点插值到下一个控制点，依次经过 (0.0, 0.0)、给定的控制点，以及 (1.0, 1.0)。

### tension

```dart
double tension
```

曲线的“张力”（tension）。

[tension] 属性用于控制曲线逼近给定 [controlPoints] 的紧密程度。它必须处于 0.0 到 1.0 之间（包含两端）。该属性可选，默认值为 0.0，可提供最平滑的曲线。值为 1.0 时相当于在各控制点之间进行线性插值。

### validateControlPoints()

```dart
bool validateControlPoints(List<Offset>? controlPoints, {double tension = 0.0, List<String>? reasons})
```

验证给定的一组 [CatmullRomCurve](https://www.yuque.com/thyname/flutter.animation/catmullromcurve) 控制点是否格式正确，并且不会生成自相交的样条。

此方法也在调试模式下用于验证曲线，以确保其不会违反 [CatmullRomCurve.new] 构造函数的约定。

在调试模式下，如果 `reasons` 非空，此函数会将遇到的问题描述填入 `reasons` 中。在发布模式下，`reasons` 参数将被忽略。

在发布模式下，此函数可用于判断对曲线提出的修改是否会生成一条有效的曲线。

如果样本中的第一个点和最后一个点分别不在 (0,0) 或 (1,1) 处，那么该曲线在两端是多值的。

### transformInternal()

```dart
double transformInternal(double t)
```

# FlippedCurve

```dart
class FlippedCurve extends Curve {}
```

一种曲线，是其给定曲线的反转（reversed inversion）。

此曲线以相反的方式计算给定曲线（即当 t 从 0.0 增加到 1.0 时，从 1.0 变化到 0.0），并返回给定曲线值的倒数（即 1.0 减去给定曲线的值）。

此类用于实现曲线上的 [flipped] 获取器。

这通常与 [CurvedAnimation.reverseCurve] 一起使用会很有用。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_bounce_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_flipped.mp4}

另请参阅：

- [Curve.flipped]，用于提供 [Curve](https://www.yuque.com/thyname/flutter.animation/curve) 的 [FlippedCurve](https://www.yuque.com/thyname/flutter.animation/flippedcurve)。
- [ReverseAnimation](https://www.yuque.com/thyname/flutter.animation/reverseanimation)，用于反转 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 而非 [Curve](https://www.yuque.com/thyname/flutter.animation/curve)。
- [CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation)，可以接受单独的曲线和反转曲线。

### FlippedCurve()

```dart
FlippedCurve(Curve curve)
```

创建一条翻转曲线。

### curve

```dart
Curve curve
```

被翻转的曲线。

### transformInternal()

```dart
double transformInternal(double t)
```

### toString()

```dart
String toString()
```

# ElasticInCurve

```dart
class ElasticInCurve extends Curve {}
```

一种振荡曲线，其幅度不断增大，同时超出其边界。

使用默认周期 0.4 的此类实例可通过 [Curves.elasticIn] 获得。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_in.mp4}

### ElasticInCurve()

```dart
ElasticInCurve([double period = 0.4])
```

创建一条弹入（elastic-in）曲线。

建议使用 [Curves.elasticIn]，而不是创建新实例。

### period

```dart
double period
```

振荡的持续时间。

### transformInternal()

```dart
double transformInternal(double t)
```

### toString()

```dart
String toString()
```

# ElasticOutCurve

```dart
class ElasticOutCurve extends Curve {}
```

一种振荡曲线，其幅度不断减小，同时超出其边界。

使用默认周期 0.4 的此类实例可通过 [Curves.elasticOut] 获得。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_out.mp4}

### ElasticOutCurve()

```dart
ElasticOutCurve([double period = 0.4])
```

创建一条弹出（elastic-out）曲线。

建议使用 [Curves.elasticOut]，而不是创建新实例。

### period

```dart
double period
```

振荡的持续时间。

### transformInternal()

```dart
double transformInternal(double t)
```

### toString()

```dart
String toString()
```

# ElasticInOutCurve

```dart
class ElasticInOutCurve extends Curve {}
```

一种振荡曲线，其幅度先增大后减小，同时超出其边界。

使用默认周期 0.4 的此类实例可通过 [Curves.elasticInOut] 获得。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_in_out.mp4}

### ElasticInOutCurve()

```dart
ElasticInOutCurve([double period = 0.4])
```

创建一条弹入弹出（elastic-in-out）曲线。

建议使用 [Curves.elasticInOut]，而不是创建新实例。

### period

```dart
double period
```

振荡的持续时间。

### transformInternal()

```dart
double transformInternal(double t)
```

### toString()

```dart
String toString()
```

# Curves

```dart
abstract final class Curves {}
```

常用动画曲线的集合。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_bounce_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_bounce_in_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_bounce_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_decelerate.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_sine.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quad.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_cubic.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quart.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quint.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_expo.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_circ.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_back.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_sine.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quad.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_cubic.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quart.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quint.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_expo.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_circ.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_back.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_sine.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quad.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_cubic.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quart.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quint.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_expo.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_circ.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_back.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_in_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_fast_out_slow_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_slow_middle.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_linear.mp4}

另请参阅：

- [Curve](https://www.yuque.com/thyname/flutter.animation/curve)，[Curves](https://www.yuque.com/thyname/flutter.animation/curves) 类所提供常量实现的接口。
- [Easing](https://www.yuque.com/thyname/flutter.material/easing)，用于 Material 动画曲线。

### linear

```dart
Curve linear
```

一条线性动画曲线。

这是单位区间上的恒等映射：其 [Curve.transform] 方法会原样返回输入值。这在需要 [Curve](https://www.yuque.com/thyname/flutter.animation/curve) 但又不希望实际应用曲线效果的情形下，可作为默认曲线使用。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_linear.mp4}

### decelerate

```dart
Curve decelerate
```

一种曲线，其变化速率先快后减速；是一条倒置的 `f(t) = t²` 抛物线。

这等价于系数为 1（默认系数）的 Android `DecelerateInterpolator` 类。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_decelerate.mp4}

### fastLinearToSlowEaseIn

```dart
Cubic fastLinearToSlowEaseIn
```

一种在开始阶段非常陡峭且呈线性的曲线，但很快趋于平缓，并非常缓慢地缓入。

默认情况下，此曲线用于在滑动手势中途结束时，为 iOS 上页面返回原始位置的动画提供效果。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_fast_linear_to_slow_ease_in.mp4}

### fastEaseInToSlowEaseOut

```dart
ThreePointCubic fastEaseInToSlowEaseOut
```

一种先缓慢开始、随后迅速加速、最后缓慢结束的曲线。

默认情况下，此曲线用于 [CupertinoPageRoute](https://www.yuque.com/thyname/flutter.cupertino/cupertinopageroute) 所使用的页面过渡动画。

此曲线源自 iPhone 14 Pro Max 上原生 iOS 16.3 动画帧的绘图数据。具体而言，每一帧都测量了过渡动画的位置，并绘制成随时间变化的图像，然后对测得的数据点进行了严格的三次曲线拟合。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_fast_ease_in_to_slow_ease_out.mp4}

### ease

```dart
Cubic ease
```

一种三次动画曲线，快速加速后缓慢结束。

这与 CSS 缓动函数 `ease` 相同。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease.mp4}

### easeIn

```dart
Cubic easeIn
```

一种三次动画曲线，缓慢开始并快速结束。

这与 CSS 缓动函数 `ease-in` 相同。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in.mp4}

### easeInToLinear

```dart
Cubic easeInToLinear
```

一种三次动画曲线，缓慢开始并以线性方式结束。

与 [linearToEaseOut](https://www.yuque.com/thyname/flutter.animation/lineartoeaseout) 对称的动画曲线。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_to_linear.mp4}

### easeInSine

```dart
Cubic easeInSine
```

一种三次动画曲线，缓慢开始并快速结束。这与 [Curves.easeIn] 类似，但采用正弦缓动，使起止过渡略微不那么突兀。尽管如此，其效果相当平缓，乍看之下很难与 [Curves.linear] 区分开来。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_sine.mp4}

### easeInQuad

```dart
Cubic easeInQuad
```

一种三次动画曲线，缓慢开始并快速结束。基于方程 `f(t) = t²` 的二次曲线，实际上是 [Curves.decelerate] 的反函数。

与 [Curves.easeInSine] 相比，此曲线略微更陡峭。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quad.mp4}

### easeInCubic

```dart
Cubic easeInCubic
```

一种三次动画曲线，缓慢开始并快速结束。此曲线基于方程 `f(t) = t³` 的三次曲线。对于为移出视口的组件动画选择曲线而言，这是一个安全的理想选择。

与 [Curves.easeInQuad] 相比，此曲线略微更陡峭。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_cubic.mp4}

### easeInQuart

```dart
Cubic easeInQuart
```

一种三次动画曲线，缓慢开始并快速结束。此曲线基于方程 `f(t) = t⁴` 的四次曲线。

使用此曲线或更陡峭曲线的动画，采用更长的持续时间会有所裨益，以避免运动显得不自然。

与 [Curves.easeInCubic] 相比，此曲线略微更陡峭。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quart.mp4}

### easeInQuint

```dart
Cubic easeInQuint
```

一种三次动画曲线，缓慢开始并快速结束。此曲线基于方程 `f(t) = t⁵` 的五次曲线。

与 [Curves.easeInQuart] 相比，此曲线略微更陡峭。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quint.mp4}

### easeInExpo

```dart
Cubic easeInExpo
```

一种三次动画曲线，缓慢开始并快速结束。此曲线基于方程 `f(t) = 2¹⁰⁽ᵗ⁻¹⁾` 的指数曲线。

使用此曲线可以为动画增添额外的效果，但可能需要使用更长的持续时间来弥补曲线的陡峭程度。

与 [Curves.easeInQuint] 相比，此曲线略微更陡峭。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_expo.mp4}

### easeInCirc

```dart
Cubic easeInCirc
```

一种三次动画曲线，缓慢开始并快速结束。此曲线实际上是圆的右下四分之一部分。

与 [Curves.easeInExpo] 类似，此曲线效果相当强烈，如果不设置更长的持续时间，会降低动画的清晰度。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_circ.mp4}

### easeInBack

```dart
Cubic easeInBack
```

一种三次动画曲线，缓慢开始并快速结束。此曲线与 [Curves.elasticIn] 类似，都会在到达终点前超出其边界。不过，此曲线并非在上升前反复摆动，而是超出一次后便持续上升。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_back.mp4}

### easeOut

```dart
Cubic easeOut
```

一种三次动画曲线，快速开始并缓慢结束。

这与 CSS 缓动函数 `ease-out` 相同。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out.mp4}

### linearToEaseOut

```dart
Cubic linearToEaseOut
```

一种三次动画曲线，以线性方式开始并缓慢结束。

与 [easeInToLinear](https://www.yuque.com/thyname/flutter.animation/easeintolinear) 对称的动画曲线。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_linear_to_ease_out.mp4}

### easeOutSine

```dart
Cubic easeOutSine
```

一种三次动画曲线，快速开始并缓慢结束。这与 [Curves.easeOut] 类似，但采用正弦缓动，使起止过渡略微不那么突兀。尽管如此，其效果相当平缓，乍看之下很难与 [Curves.linear] 区分开来。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_sine.mp4}

### easeOutQuad

```dart
Cubic easeOutQuad
```

一种三次动画曲线，快速开始并缓慢结束。这实际上与 [Curves.decelerate] 相同，只是使用三次贝塞尔函数进行了模拟。

与 [Curves.easeOutSine] 相比，此曲线略微更陡峭。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quad.mp4}

### easeOutCubic

```dart
Cubic easeOutCubic
```

一种三次动画曲线，快速开始并缓慢结束。此曲线是 [Curves.easeInCubic] 的翻转版本。

对于为进入视口或已在视口内的组件位置动画选择曲线而言，这是一个安全的理想选择。

与 [Curves.easeOutQuad] 相比，此曲线略微更陡峭。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_cubic.mp4}

### easeOutQuart

```dart
Cubic easeOutQuart
```

一种三次动画曲线，快速开始并缓慢结束。此曲线是 [Curves.easeInQuart] 的翻转版本。

使用此曲线或更陡峭曲线的动画，采用更长的持续时间会有所裨益，以避免运动显得不自然。

与 [Curves.easeOutCubic] 相比，此曲线略微更陡峭。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quart.mp4}

### easeOutQuint

```dart
Cubic easeOutQuint
```

一种三次动画曲线，快速开始并缓慢结束。此曲线是 [Curves.easeInQuint] 的翻转版本。

与 [Curves.easeOutQuart] 相比，此曲线略微更陡峭。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quint.mp4}

### easeOutExpo

```dart
Cubic easeOutExpo
```

一种三次动画曲线，快速开始并缓慢结束。此曲线是 [Curves.easeInExpo] 的翻转版本。使用此曲线可以为动画增添额外的效果，但可能需要使用更长的持续时间来弥补曲线的陡峭程度。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_expo.mp4}

### easeOutCirc

```dart
Cubic easeOutCirc
```

一种三次动画曲线，快速开始并缓慢结束。此曲线实际上是圆的左上四分之一部分。

与 [Curves.easeOutExpo] 类似，此曲线效果相当强烈，如果不设置更长的持续时间，会降低动画的清晰度。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_circ.mp4}

### easeOutBack

```dart
Cubic easeOutBack
```

一种三次动画曲线，快速开始并缓慢结束。此曲线与 [Curves.elasticOut] 类似，都会在到达终点前超出其边界。不过，此曲线在上升后并不会反复摆动，而只会超出一次。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_back.mp4}

### easeInOut

```dart
Cubic easeInOut
```

一种三次动画曲线，缓慢开始，加速后又缓慢结束。

这与 CSS 缓动函数 `ease-in-out` 相同。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out.mp4}

### easeInOutSine

```dart
Cubic easeInOutSine
```

一种三次动画曲线，缓慢开始，加速后又缓慢结束。这与 [Curves.easeInOut] 类似，但采用正弦缓动，使起止过渡略微不那么突兀。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_sine.mp4}

### easeInOutQuad

```dart
Cubic easeInOutQuad
```

一种三次动画曲线，缓慢开始，加速后又缓慢结束。此曲线可以理解为前半段是 [Curves.easeInQuad]，后半段是 [Curves.easeOutQuad]。

与 [Curves.easeInOutSine] 相比，此曲线略微更陡峭。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quad.mp4}

### easeInOutCubic

```dart
Cubic easeInOutCubic
```

一种三次动画曲线，缓慢开始，加速后又缓慢结束。此曲线可以理解为前半段是 [Curves.easeInCubic]，后半段是 [Curves.easeOutCubic]。

对于为初始和最终位置都在视口内的组件选择曲线而言，这是一个安全的理想选择。

与 [Curves.easeInOutQuad] 相比，此曲线略微更陡峭。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_cubic.mp4}

### easeInOutCubicEmphasized

```dart
ThreePointCubic easeInOutCubicEmphasized
```

一种三次动画曲线，缓慢开始，随后不久加速，然后又缓慢结束。此曲线可以理解为 [easeInOutCubic](https://www.yuque.com/thyname/flutter.animation/easeinoutcubic) 的更陡峭版本。

对于为初始和最终位置都在视口内的组件选择曲线而言，这提供了一种更为强调的缓动效果。

与 [Curves.easeInOutCubic] 相比，此曲线略微更陡峭。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_cubic_emphasized.mp4}

### easeInOutQuart

```dart
Cubic easeInOutQuart
```

一种三次动画曲线，缓慢开始，加速后又缓慢结束。此曲线可以理解为前半段是 [Curves.easeInQuart]，后半段是 [Curves.easeOutQuart]。

使用此曲线或更陡峭曲线的动画，采用更长的持续时间会有所裨益，以避免运动显得不自然。

与 [Curves.easeInOutCubic] 相比，此曲线略微更陡峭。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quart.mp4}

### easeInOutQuint

```dart
Cubic easeInOutQuint
```

一种三次动画曲线，缓慢开始，加速后又缓慢结束。此曲线可以理解为前半段是 [Curves.easeInQuint]，后半段是 [Curves.easeOutQuint]。

与 [Curves.easeInOutQuart] 相比，此曲线略微更陡峭。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quint.mp4}

### easeInOutExpo

```dart
Cubic easeInOutExpo
```

一种三次动画曲线，缓慢开始，加速后又缓慢结束。

由于此曲线是通过指数函数得到的，其中点处异常陡峭。使用此曲线设计动画时应格外注意。

与 [Curves.easeInOutQuint] 相比，此曲线略微更陡峭。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_expo.mp4}

### easeInOutCirc

```dart
Cubic easeInOutCirc
```

一种三次动画曲线，缓慢开始，加速后又缓慢结束。此曲线可以理解为前半段是 [Curves.easeInCirc]，后半段是 [Curves.easeOutCirc]。

与 [Curves.easeInOutExpo] 类似，此曲线效果相当强烈，如果不设置更长的持续时间，会降低动画的清晰度。

与 [Curves.easeInOutExpo] 相比，此曲线略微更陡峭。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_circ.mp4}

### easeInOutBack

```dart
Cubic easeInOutBack
```

一种三次动画曲线，缓慢开始，加速后又缓慢结束。此曲线可以理解为前半段是 [Curves.easeInBack]，后半段是 [Curves.easeOutBack]。

由于此曲线以两条曲线为基础，所得动画在到达终点之前会两次超出其边界——先是超出下边界，然后超出上边界，最后再回落到最终位置。

源自 Robert Penner 的缓动函数。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_back.mp4}

### fastOutSlowIn

```dart
Cubic fastOutSlowIn
```

一种快速开始并缓入其最终位置的曲线。

在动画过程中，对象会在其最终目的地附近停留更长时间。因此，用户不会因等待动画结束而感到不耐烦，且运动带来的负面影响也被降到最低。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_fast_out_slow_in.mp4}

另请参阅：

- [Easing.legacy]，此曲线在 Material 规范中的名称。

### slowMiddle

```dart
Cubic slowMiddle
```

一种三次动画曲线，快速开始，减速后又快速结束。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_slow_middle.mp4}

### bounceIn

```dart
Curve bounceIn
```

一种振荡曲线，幅度不断增大。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_bounce_in.mp4}

### bounceOut

```dart
Curve bounceOut
```

一种振荡曲线，幅度先增大后减小。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_bounce_out.mp4}

### bounceInOut

```dart
Curve bounceInOut
```

一种振荡曲线，幅度先增大后减小。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_bounce_in_out.mp4}

### elasticIn

```dart
ElasticInCurve elasticIn
```

一种振荡曲线，其幅度不断增大，同时超出其边界。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_in.mp4}

### elasticOut

```dart
ElasticOutCurve elasticOut
```

一种振荡曲线，其幅度不断减小，同时超出其边界。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_out.mp4}

### elasticInOut

```dart
ElasticInOutCurve elasticInOut
```

一种振荡曲线，其幅度先增大后减小，同时超出其边界。

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_in_out.mp4}
