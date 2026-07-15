@docImport 'package:flutter/material.dart';

# AnimatableCallback

```dart
typedef AnimatableCallback<T> = T Function(double value)
```

用于 [Animatable.fromCallback] 的 typedef，用于通过回调创建一个 [Animatable](https://www.yuque.com/thyname/flutter.animation/animatable)。

# Animatable

```dart
abstract class Animatable<T> {}
```

一个可以根据输入的 [Animation<double>] 生成 [T] 类型值的对象。

通常情况下，输入动画的值名义上处于 0.0 到 1.0 的范围内。但原则上，可以提供任何值。

[Animatable](https://www.yuque.com/thyname/flutter.animation/animatable) 的主要子类是 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。

### Animatable()

```dart
Animatable()
```

抽象的 const 构造函数。此构造函数使子类能够提供 const 构造函数，从而可以在 const 表达式中使用。

### Animatable.fromCallback()

```dart
Animatable.fromCallback(AnimatableCallback<T> callback)
```

根据提供的 [callback] 创建一个新的 [Animatable](https://www.yuque.com/thyname/flutter.animation/animatable)。

另请参阅：

- [Animation.drive]，其中提供了一个说明如何使用此构造函数的示例。

### transform()

```dart
T transform(double t)
```

返回该对象在 `t` 点处的值。

`t` 的值名义上是 0.0 到 1.0 范围内的一个分数，但实际上可能会超出此范围。

另请参阅：

- [evaluate]，它是将 [transform] 应用于 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 值的简写形式。
- [Curve.transform]，缓动曲线的类似方法。

### evaluate()

```dart
T evaluate(Animation<double> animation)
```

此对象针对给定 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 的当前值。

此函数通过委托给 [transform] 实现。想要提供自定义行为的子类应重写 [transform]，而不是 [evaluate]。

另请参阅：

- [transform]，与此类似，但直接接受一个 `t` 值，而非 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)。
- [animate]，根据此对象创建一个 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)，持续地应用 [evaluate]。

### animate()

```dart
Animation<T> animate(Animation<double> parent)
```

返回一个新的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)，它由给定的动画驱动，但取值由此对象决定。

本质上，这会返回一个自动将 [evaluate] 方法应用于父动画值的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)。

另请参阅：

- [AnimationController.drive]，从相反的起点执行相同的操作。

### chain()

```dart
Animatable<T> chain(Animatable<double> parent)
```

返回一个新的 [Animatable](https://www.yuque.com/thyname/flutter.animation/animatable)，其值的确定方式是：先对给定的父对象求值，再以其结果对此对象求值。

此方法表示对 [transform] 的函数组合：返回的 [Animatable](https://www.yuque.com/thyname/flutter.animation/animatable) 的 [transform] 方法是将此对象的 [transform] 方法与给定父对象的 [transform] 方法组合的结果。

这使得 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 可以在获取 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 之前进行链式组合，而无需为中间结果分配 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)。

# Tween

```dart
class Tween<T extends Object?> extends Animatable<T> {}
```

在起始值和结束值之间进行线性插值。

如果你想在一个范围内进行插值，[Tween](https://www.yuque.com/thyname/flutter.animation/tween) 会很有用。

要将 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 对象与动画一起使用，请调用 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 对象的 [animate] 方法，并将你想要修改的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 对象传给它。

你可以使用 [chain] 方法将多个 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 对象链接在一起，从而生成它们各自 [transform] 方法的函数组合。通过在生成的 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 上调用 [animate] 来配置单个 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 对象，其效果与依次在每个 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 上单独调用 [animate] 方法相同，但效率更高，因为它避免了为中间结果创建 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 对象。

{@tool snippet}

假设 `_controller` 是一个 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)，我们想要创建一个由该控制器控制的 [Animation<Offset>]，并将其保存在 `_animation` 中。以下是两种可能的实现方式：

```dart
_animation = _controller.drive(
  Tween<Offset>(
    begin: const Offset(100.0, 50.0),
    end: const Offset(200.0, 300.0),
  ),
);
```

{@end-tool} {@tool snippet}

```dart
_animation = Tween<Offset>(
  begin: const Offset(100.0, 50.0),
  end: const Offset(200.0, 300.0),
).animate(_controller);
```

{@end-tool}

在这两种情况下，`_animation` 变量都持有一个对象，在 `_controller` 动画的生命周期内，该对象返回一个值（`_animation.value`），描绘出上述两个偏移量之间连线上的一个点。如果在上面的代码中使用 [MaterialPointArcTween](https://www.yuque.com/thyname/flutter.material/materialpointarctween) 而不是 [Tween<Offset>]，这些点将沿着一条优美的曲线移动，而不是直线，且无需进行其他更改。

## Performance optimizations

Tween 是可变的；具体来说，其 [begin] 和 [end] 值可以在运行时更改。使用 [Animation.drive] 基于某个 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 创建的对象，会立即响应该底层 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 发生的更改（不过只有在 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 正在进行动画时才会触发监听器）。这可用于即时更改动画，而无需重新创建从 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 到最终 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 这一整条链上的所有对象。

但是，如果一个 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 的值永远不会改变，则可以应用进一步的优化：将该对象存储在 `static final` 变量中，这样每当需要该 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 时都会使用完全相同的实例。例如，这比每次调用 [State.build] 方法时都重新创建一个相同的 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 更可取。

## Types with special considerations

拥有 [lerp] 静态方法的类通常有相应的专用 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 子类来调用该方法。例如，[ColorTween](https://www.yuque.com/thyname/flutter.animation/colortween) 使用 [Color.lerp] 来实现 [ColorTween.lerp] 方法。

定义了用于组合值的 `+` 和 `-` 运算符（`T + T → T` 以及 `T - T → T`），以及用于通过与 double 相乘进行缩放的 `*` 运算符（`T * double → T`）的类型，可以直接与 `Tween<T>` 一起使用。

这并不适用于所有具有 `+`、`-` 和 `*` 运算符的类型。特别是，[int](https://www.yuque.com/thyname/dart.core/int) 并不满足这一精确的约定（`int * double` 实际上返回的是 [num](https://www.yuque.com/thyname/dart.core/num)，而不是 [int](https://www.yuque.com/thyname/dart.core/int)）。因此，有两个专门的类可用于对整数进行插值：

- [IntTween](https://www.yuque.com/thyname/flutter.animation/inttween)，它是线性插值的近似（使用 [double.round]）。
- [StepTween](https://www.yuque.com/thyname/flutter.animation/steptween)，它使用 [double.floor]，以确保结果永远不会大于使用 `Tween<double>` 时的结果。

[Size](https://www.yuque.com/thyname/dart.ui/size) 上的相关运算符同样不满足这一约定，因此 [SizeTween](https://www.yuque.com/thyname/flutter.animation/sizetween) 使用 [Size.lerp]。

此外，一些确实拥有合适的 `+`、`-` 和 `*` 运算符的类型，仍然拥有专用的 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 子类，以更专门的方式执行插值。上文提到的 [MaterialPointArcTween](https://www.yuque.com/thyname/flutter.material/materialpointarctween) 就是这样一个类。[AlignmentTween](https://www.yuque.com/thyname/flutter.rendering/alignmenttween)、[AlignmentGeometryTween](https://www.yuque.com/thyname/flutter.rendering/alignmentgeometrytween) 和 [FractionalOffsetTween](https://www.yuque.com/thyname/flutter.rendering/fractionaloffsettween) 是另一组使用专用 `lerp` 方法而非仅仅依赖运算符的 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)（特别是，这使它们能够以更有效的方式处理空值）。

## Nullability

[begin] 和 [end] 字段是可空的；创建 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 时不必指定非空值。

如果 `T` 是可空的，那么 [lerp] 和 [transform] 可能会返回 null。这通常出现在 [begin] 为 null 且 `t` 为 0.0，或 [end] 为 null 且 `t` 为 1.0，或两者都为 null（在任意 `t` 值下）的情况。

如果 `T` 是非空的，那么在使用 [lerp] 或 [transform] 之前，必须将 [begin] 和 [end] 都设置为非空值，否则会抛出异常。

## Implementing a Tween

要针对新类型特化此类，子类应实现 [lerp] 方法（以及一个构造函数）。此类的其他方法都是基于 [lerp] 定义的。

### Tween()

```dart
Tween({T? begin, T? end})
```

创建一个 tween。

在首次使用该 tween 之前，[begin] 和 [end] 属性必须为非空，但如果这些值将在之后填入，则构造函数的参数可以为 null。

### begin

```dart
T? begin
```

该变量在动画开始时的值。

有关此属性是否可为 null 的详细信息，请参阅构造函数（不同子类情况不同）。

### end

```dart
T? end
```

该变量在动画结束时的值。

有关此属性是否可为 null 的详细信息，请参阅构造函数（不同子类情况不同）。

### lerp()

```dart
T lerp(double t)
```

返回该变量在给定动画时钟值下的值。

此方法的默认实现使用 `T` 上的 `+`、`-` 和 `*` 运算符。因此，在调用此方法时，[begin] 和 [end] 属性必须为非空。

不过，一般来说，此方法可能返回 null，特别是当 `t`=0.0 且 [begin] 为 null，或 `t`=1.0 且 [end] 为 null 时。

### transform()

```dart
T transform(double t)
```

返回给定动画当前值所对应的插值结果。

当动画值分别为 0.0 或 1.0 时，此方法分别返回 `begin` 和 `end`。

此函数通过委托给 [lerp] 实现。想要提供自定义行为的子类应重写 [lerp]，而不是 [transform]（也不是 [evaluate]）。

有关调用此方法时 [begin] 和 [end] 属性是否可为 null 的详细信息，请参阅构造函数。不同子类情况不同。

### toString()

```dart
String toString()
```

# ReverseTween

```dart
class ReverseTween<T extends Object?> extends Tween<T> {}
```

一个反向求值其 [parent] 的 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。

### ReverseTween()

```dart
ReverseTween(Tween<T> parent)
```

构造一个反向求值其 [parent] 的 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。

### parent

```dart
Tween<T> parent
```

此 tween 的值与其父 tween 反向求值后的值相同。

此 tween 的 [begin] 是父 tween 的 [end]，其 [end] 是父 tween 的 [begin]。[lerp] 方法返回 `parent.lerp(1.0 - t)`，其 [evaluate] 方法与之类似。

### lerp()

```dart
T lerp(double t)
```

# ColorTween

```dart
class ColorTween extends Tween<Color?> {}
```

两种颜色之间的插值。

此类将 [Tween<Color>] 的插值特化为使用 [Color.lerp]。

这些值可以为 null，表示没有颜色（这与 [Colors.transparent] 所表示的透明黑色不同）。

有关如何使用插值对象的讨论，请参阅 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。

### ColorTween()

```dart
ColorTween({dynamic begin, dynamic end})
```

创建一个 [Color](https://www.yuque.com/thyname/dart.ui/color) tween。

[begin] 和 [end] 属性可以为 null；null 值将被视为透明。

如果你想要实现淡入或淡出透明的效果，我们建议不要将 [Colors.transparent] 作为 [begin] 或 [end] 传入，而应优先使用 null。[Colors.transparent] 指的是透明的黑色，因此淡入淡出的效果会趋向黑色，这可能并非你想要的效果。

### lerp()

```dart
Color? lerp(double t)
```

返回该变量在给定动画时钟值下的值。

# SizeTween

```dart
class SizeTween extends Tween<Size?> {}
```

两个尺寸之间的插值。

此类将 [Tween<Size>] 的插值特化为使用 [Size.lerp]。

这些值可以为 null，表示 [Size.zero]。

有关如何使用插值对象的讨论，请参阅 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。

### SizeTween()

```dart
SizeTween({dynamic begin, dynamic end})
```

创建一个 [Size](https://www.yuque.com/thyname/dart.ui/size) tween。

[begin] 和 [end] 属性可以为 null；null 值将被视为空尺寸。

### lerp()

```dart
Size? lerp(double t)
```

返回该变量在给定动画时钟值下的值。

# RectTween

```dart
class RectTween extends Tween<Rect?> {}
```

两个矩形之间的插值。

此类将 [Tween<Rect>] 的插值特化为使用 [Rect.lerp]。

这些值可以为 null，表示原点处一个大小为零的矩形（[Rect.zero]）。

有关如何使用插值对象的讨论，请参阅 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。

### RectTween()

```dart
RectTween({dynamic begin, dynamic end})
```

创建一个 [Rect](https://www.yuque.com/thyname/dart.ui/rect) tween。

[begin] 和 [end] 属性可以为 null；null 值将被视为左上角的一个空矩形。

### lerp()

```dart
Rect? lerp(double t)
```

返回该变量在给定动画时钟值下的值。

# IntTween

```dart
class IntTween extends Tween<int> {}
```

两个整数之间的插值，结果四舍五入。

此类通过在给定的起始值和结束值之间进行插值，然后将结果四舍五入为最接近的整数，从而将 [Tween<int>] 的插值特化为适用于整数的形式。

这是整数所能实现的最接近线性 tween 的近似方式。可与 [StepTween](https://www.yuque.com/thyname/flutter.animation/steptween) 和 [Tween<double>] 进行比较。

在调用 [lerp] 或 [transform] 之前，必须将 [begin] 和 [end] 的值设置为非空值。

有关如何使用插值对象的讨论，请参阅 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。

### IntTween()

```dart
IntTween({int? begin, int? end})
```

创建一个 int tween。

在首次使用该 tween 之前，[begin] 和 [end] 属性必须为非空，但如果这些值将在之后填入，则构造函数的参数可以为 null。

### lerp()

```dart
int lerp(double t)
```

# StepTween

```dart
class StepTween extends Tween<int> {}
```

两个整数之间的插值，结果向下取整。

此类通过在给定的起始值和结束值之间进行插值，然后使用 [double.floor] 返回当前的整数部分、舍去小数部分，从而将 [Tween<int>] 的插值特化为适用于整数的形式。

这样得到的值永远不会大于线性 double 插值所得到的等效值。可与 [IntTween](https://www.yuque.com/thyname/flutter.animation/inttween) 进行比较。

在调用 [lerp] 或 [transform] 之前，必须将 [begin] 和 [end] 的值设置为非空值。

有关如何使用插值对象的讨论，请参阅 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。

### StepTween()

```dart
StepTween({int? begin, int? end})
```

创建一个向下取整的 [int](https://www.yuque.com/thyname/dart.core/int) tween。

在首次使用该 tween 之前，[begin] 和 [end] 属性必须为非空，但如果这些值将在之后填入，则构造函数的参数可以为 null。

### lerp()

```dart
int lerp(double t)
```

# ConstantTween

```dart
class ConstantTween<T> extends Tween<T> {}
```

一个具有恒定值的 tween。

### ConstantTween()

```dart
ConstantTween(T value)
```

创建一个 [begin] 和 [end] 值都等于 [value] 的 tween。

### lerp()

```dart
T lerp(double t)
```

此 tween 不进行插值，始终返回相同的值。

### toString()

```dart
String toString()
```

# CurveTween

```dart
class CurveTween extends Animatable<double> {}
```

通过给定的曲线来变换给定动画的值。

此类与 [CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation) 的不同之处在于：[CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation) 将曲线应用于已有的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 对象，而 [CurveTween](https://www.yuque.com/thyname/flutter.animation/curvetween) 可以在接收底层 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 之前先与另一个 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 链接在一起。与 [CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation) 不同，[CurveTween](https://www.yuque.com/thyname/flutter.animation/curvetween) 不会添加监听器或持有状态，因此无需释放（dispose）。

（[CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation) 还具有额外的能力，即在动画正向进行与反向进行时可以使用不同的曲线，这在某些场景下会很有用。）

{@tool snippet}

以下代码片段展示了如何将曲线应用于由 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) `controller` 产生的线性动画：

```dart
final Animation<double> animation = _controller.drive(
  CurveTween(curve: Curves.ease),
);
```

{@end-tool}

另请参阅：

- [CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation)，是表达上述示例的另一种方式。
- [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)，其中有创建和释放 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 的示例。

### CurveTween()

```dart
CurveTween({required Curve curve})
```

创建一个曲线 tween。

### curve

```dart
Curve curve
```

变换动画值时所使用的曲线。
