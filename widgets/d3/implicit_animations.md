@docImport 'package:flutter/material.dart';

@docImport 'animated_cross_fade.dart'; @docImport 'animated_size.dart'; @docImport 'animated_switcher.dart'; @docImport 'scroll_view.dart'; @docImport 'sliver.dart'; @docImport 'tween_animation_builder.dart';

# BoxConstraintsTween

```dart
class BoxConstraintsTween extends Tween<BoxConstraints> {}
```

两个 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints) 之间的插值。

此类将 [Tween<BoxConstraints>] 的插值特化为使用 [BoxConstraints.lerp]。

有关如何使用插值对象的讨论，请参阅 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。

### BoxConstraintsTween()

```dart
BoxConstraintsTween({dynamic begin, dynamic end})
```

创建一个 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints) 补间动画（tween）。

[begin] 和 [end] 属性可以为 null；null 值会被视为尺寸为零的紧约束（tight constraint）。

### lerp()

```dart
BoxConstraints lerp(double t)
```

返回此变量在给定动画时钟值下的取值。

# DecorationTween

```dart
class DecorationTween extends Tween<Decoration> {}
```

两个 [Decoration](https://www.yuque.com/thyname/flutter.painting/decoration) 之间的插值。

此类将 [Tween<BoxConstraints>] 的插值特化为使用 [Decoration.lerp]。

对于知道如何通过 [ShapeDecoration.lerpTo] 或 [ShapeDecoration.lerpFrom] 相互插值的 [ShapeDecoration](https://www.yuque.com/thyname/flutter.painting/shapedecoration)，此类将在装饰之间生成平滑的插值。

另请参阅：

- 有关如何使用插值对象的讨论，请参阅 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。
- [ShapeDecoration](https://www.yuque.com/thyname/flutter.painting/shapedecoration)、[RoundedRectangleBorder](https://www.yuque.com/thyname/flutter.painting/roundedrectangleborder)、[CircleBorder](https://www.yuque.com/thyname/flutter.painting/circleborder) 和 [StadiumBorder](https://www.yuque.com/thyname/flutter.painting/stadiumborder)，它们是可以平滑插值的形状边框（shape border）示例。
- [BoxBorder](https://www.yuque.com/thyname/flutter.painting/boxborder)，一种只能在其他 [BoxBorder](https://www.yuque.com/thyname/flutter.painting/boxborder) 之间平滑插值的边框。

### DecorationTween()

```dart
DecorationTween({dynamic begin, dynamic end})
```

创建一个装饰补间动画。

[begin] 和 [end] 属性可以为 null。如果两者都为 null，则结果始终为 null。如果 [end] 不为 null，则使用其插值逻辑（通过 [Decoration.lerpTo]）；否则，使用 [begin] 的插值逻辑（通过 [Decoration.lerpFrom]）。

### lerp()

```dart
Decoration lerp(double t)
```

返回此变量在给定动画时钟值下的取值。

# EdgeInsetsTween

```dart
class EdgeInsetsTween extends Tween<EdgeInsets> {}
```

两个 [EdgeInsets](https://www.yuque.com/thyname/flutter.painting/edgeinsets) 之间的插值。

此类将 [Tween<EdgeInsets>] 的插值特化为使用 [EdgeInsets.lerp]。

有关如何使用插值对象的讨论，请参阅 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。

另请参阅：

- [EdgeInsetsGeometryTween](https://www.yuque.com/thyname/flutter.widgets/edgeinsetsgeometrytween)，用于在两个 [EdgeInsetsGeometry](https://www.yuque.com/thyname/flutter.painting/edgeinsetsgeometry) 对象之间进行插值。

### EdgeInsetsTween()

```dart
EdgeInsetsTween({dynamic begin, dynamic end})
```

创建一个 [EdgeInsets](https://www.yuque.com/thyname/flutter.painting/edgeinsets) 补间动画。

[begin] 和 [end] 属性可以为 null；null 值会被视为没有内边距的 [EdgeInsets](https://www.yuque.com/thyname/flutter.painting/edgeinsets)。

### lerp()

```dart
EdgeInsets lerp(double t)
```

返回此变量在给定动画时钟值下的取值。

# EdgeInsetsGeometryTween

```dart
class EdgeInsetsGeometryTween extends Tween<EdgeInsetsGeometry> {}
```

两个 [EdgeInsetsGeometry](https://www.yuque.com/thyname/flutter.painting/edgeinsetsgeometry) 之间的插值。

此类将 [Tween<EdgeInsetsGeometry>] 的插值特化为使用 [EdgeInsetsGeometry.lerp]。

有关如何使用插值对象的讨论，请参阅 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。

另请参阅：

- [EdgeInsetsTween](https://www.yuque.com/thyname/flutter.widgets/edgeinsetstween)，用于在两个 [EdgeInsets](https://www.yuque.com/thyname/flutter.painting/edgeinsets) 对象之间进行插值。

### EdgeInsetsGeometryTween()

```dart
EdgeInsetsGeometryTween({dynamic begin, dynamic end})
```

创建一个 [EdgeInsetsGeometry](https://www.yuque.com/thyname/flutter.painting/edgeinsetsgeometry) 补间动画。

[begin] 和 [end] 属性可以为 null；null 值会被视为没有内边距的 [EdgeInsetsGeometry](https://www.yuque.com/thyname/flutter.painting/edgeinsetsgeometry)。

### lerp()

```dart
EdgeInsetsGeometry lerp(double t)
```

返回此变量在给定动画时钟值下的取值。

# BorderRadiusTween

```dart
class BorderRadiusTween extends Tween<BorderRadius?> {}
```

两个 [BorderRadius](https://www.yuque.com/thyname/flutter.painting/borderradius) 之间的插值。

此类将 [Tween<BorderRadius>] 的插值特化为使用 [BorderRadius.lerp]。

有关如何使用插值对象的讨论，请参阅 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。

### BorderRadiusTween()

```dart
BorderRadiusTween({dynamic begin, dynamic end})
```

创建一个 [BorderRadius](https://www.yuque.com/thyname/flutter.painting/borderradius) 补间动画。

[begin] 和 [end] 属性可以为 null；null 值会被视为直角（无半径）。

### lerp()

```dart
BorderRadius? lerp(double t)
```

返回此变量在给定动画时钟值下的取值。

# BorderTween

```dart
class BorderTween extends Tween<Border?> {}
```

两个 [Border](https://www.yuque.com/thyname/flutter.painting/border) 之间的插值。

此类将 [Tween<Border>] 的插值特化为使用 [Border.lerp]。

有关如何使用插值对象的讨论，请参阅 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。

### BorderTween()

```dart
BorderTween({dynamic begin, dynamic end})
```

创建一个 [Border](https://www.yuque.com/thyname/flutter.painting/border) 补间动画。

[begin] 和 [end] 属性可以为 null；null 值会被视为没有边框。

### lerp()

```dart
Border? lerp(double t)
```

返回此变量在给定动画时钟值下的取值。

# Matrix4Tween

```dart
class Matrix4Tween extends Tween<Matrix4> {}
```

两个 [Matrix4] 之间的插值。

此类将 [Tween<Matrix4>] 的插值特化为适用于变换矩阵。

目前此类仅适用于平移变换。

有关如何使用插值对象的讨论，请参阅 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。

### Matrix4Tween()

```dart
Matrix4Tween({dynamic begin, dynamic end})
```

创建一个 [Matrix4] 补间动画。

在首次使用该补间动画之前，[begin] 和 [end] 属性必须非 null，但如果这些值将在之后填入，则构造函数参数可以为 null。

### lerp()

```dart
Matrix4 lerp(double t)
```

# TextStyleTween

```dart
class TextStyleTween extends Tween<TextStyle> {}
```

两个 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 之间的插值。

此类将 [Tween<TextStyle>] 的插值特化为使用 [TextStyle.lerp]。

如果两种样式没有设置相同的字段，此类的效果将不理想。

有关如何使用插值对象的讨论，请参阅 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。

### TextStyleTween()

```dart
TextStyleTween({dynamic begin, dynamic end})
```

创建一个文本样式补间动画。

在首次使用该补间动画之前，[begin] 和 [end] 属性必须非 null，但如果这些值将在之后填入，则构造函数参数可以为 null。

### lerp()

```dart
TextStyle lerp(double t)
```

返回此变量在给定动画时钟值下的取值。

# ImplicitlyAnimatedWidget

```dart
abstract class ImplicitlyAnimatedWidget extends StatefulWidget {}
```

用于构建能够对其自身属性变化进行动画处理的组件的抽象类。

此类型的组件在首次添加到组件树时不会进行动画处理。相反，当它们以不同的值重建时，会通过在指定的 [duration] 内对这些变化进行动画处理来做出响应。

具体动画哪些属性由子类决定。子类的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 必须继承 [ImplicitlyAnimatedWidgetState](https://www.yuque.com/thyname/flutter.widgets/implicitlyanimatedwidgetstate)，并提供一种访问需要进行动画处理的相关字段的方式。

## 与 [AnimatedWidget](https://www.yuque.com/thyname/flutter.widgets/animatedwidget) 的关系

[ImplicitlyAnimatedWidget](https://www.yuque.com/thyname/flutter.widgets/implicitlyanimatedwidget)（及其子类）会在其属性发生变化时自动对变化进行动画处理。为此，它们会创建并管理自己内部的 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 来驱动动画。虽然这些组件使用简单，且不需要你手动管理 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 的生命周期，但它们也存在一定的局限性：除了被动画处理的属性的目标值外，开发者只能选择动画的 [duration] 和 [curve]。如果你需要对动画进行更精细的控制（例如，希望在动画进行到一半时将其停止），可以考虑使用 [AnimatedWidget](https://www.yuque.com/thyname/flutter.widgets/animatedwidget) 或其子类之一。这些组件接收一个 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 作为参数来驱动动画，这使开发者能够完全控制动画，但代价是需要手动管理底层 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 的生命周期。

## 常见的隐式动画组件

框架自带许多隐式动画组件。它们通常命名为 `AnimatedFoo`，其中 `Foo` 是该组件非动画版本的名称。常用的隐式动画组件包括：

- [TweenAnimationBuilder](https://www.yuque.com/thyname/flutter.widgets/tweenanimationbuilder)，可以对任何由 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 表示的属性进行动画处理，使其过渡到指定的目标值。
- [AnimatedAlign](https://www.yuque.com/thyname/flutter.widgets/animatedalign)，[Align](https://www.yuque.com/thyname/flutter.widgets/align) 的隐式动画版本。
- [AnimatedContainer](https://www.yuque.com/thyname/flutter.widgets/animatedcontainer)，[Container](https://www.yuque.com/thyname/flutter.widgets/container) 的隐式动画版本。
- [AnimatedDefaultTextStyle](https://www.yuque.com/thyname/flutter.widgets/animateddefaulttextstyle)，[DefaultTextStyle](https://www.yuque.com/thyname/flutter.widgets/defaulttextstyle) 的隐式动画版本。
- [AnimatedScale](https://www.yuque.com/thyname/flutter.widgets/animatedscale)，[Transform.scale] 的隐式动画版本。
- [AnimatedRotation](https://www.yuque.com/thyname/flutter.widgets/animatedrotation)，[Transform.rotate] 的隐式动画版本。
- [AnimatedSlide](https://www.yuque.com/thyname/flutter.widgets/animatedslide)，对组件相对于其正常位置的位移进行隐式动画处理。
- [AnimatedOpacity](https://www.yuque.com/thyname/flutter.widgets/animatedopacity)，[Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity) 的隐式动画版本。
- [AnimatedPadding](https://www.yuque.com/thyname/flutter.widgets/animatedpadding)，[Padding](https://www.yuque.com/thyname/flutter.widgets/padding) 的隐式动画版本。
- [AnimatedPhysicalModel](https://www.yuque.com/thyname/flutter.widgets/animatedphysicalmodel)，[PhysicalModel](https://www.yuque.com/thyname/flutter.widgets/physicalmodel) 的隐式动画版本。
- [AnimatedPositioned](https://www.yuque.com/thyname/flutter.widgets/animatedpositioned)，[Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned) 的隐式动画版本。
- [AnimatedPositionedDirectional](https://www.yuque.com/thyname/flutter.widgets/animatedpositioneddirectional)，[PositionedDirectional](https://www.yuque.com/thyname/flutter.widgets/positioneddirectional) 的隐式动画版本。
- [AnimatedTheme](https://www.yuque.com/thyname/flutter.material/animatedtheme)，[Theme](https://www.yuque.com/thyname/flutter.material/theme) 的隐式动画版本。
- [AnimatedCrossFade](https://www.yuque.com/thyname/flutter.widgets/animatedcrossfade)，在两个给定的子组件之间交叉淡入淡出，并对自身在二者尺寸之间的变化进行动画处理。
- [AnimatedSize](https://www.yuque.com/thyname/flutter.widgets/animatedsize)，在给定的时长内自动对其尺寸变化进行动画处理。
- [AnimatedSwitcher](https://www.yuque.com/thyname/flutter.widgets/animatedswitcher)，从一个组件淡出并淡入另一个组件。

### ImplicitlyAnimatedWidget()

```dart
ImplicitlyAnimatedWidget({dynamic key, Curve curve = Curves.linear, required Duration duration, VoidCallback? onEnd})
```

为子类初始化字段。

### curve

```dart
Curve curve
```

对此容器的参数进行动画处理时所应用的曲线。

### duration

```dart
Duration duration
```

对此容器的参数进行动画处理所需的时长。

### onEnd

```dart
VoidCallback? onEnd
```

每次动画完成时调用。

这在需要于当前动画结束时触发额外操作（例如另一个动画）时很有用。

### createState()

```dart
ImplicitlyAnimatedWidgetState<ImplicitlyAnimatedWidget> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# TweenConstructor

```dart
typedef TweenConstructor<T extends Object> = Tween<T> Function(T targetValue)
```

[Tween](https://www.yuque.com/thyname/flutter.animation/tween) 工厂的函数签名。

这是 [TweenVisitor](https://www.yuque.com/thyname/flutter.widgets/tweenvisitor) 的其中一个参数的类型，[TweenVisitor](https://www.yuque.com/thyname/flutter.widgets/tweenvisitor) 是 [AnimatedWidgetBaseState.forEachTween] 所使用的函数签名。

此函数的实例应接收一个值，并返回一个从该值开始的补间动画。

# TweenVisitor

```dart
typedef TweenVisitor<T extends Object> = Tween<T>? Function(Tween<T>? tween, T targetValue, TweenConstructor<T> constructor)
```

传递给 [ImplicitlyAnimatedWidgetState.forEachTween] 的回调函数签名。

{@template flutter.widgets.TweenVisitor.arguments} `tween` 参数应包含当前的补间动画值。当 State 首次初始化时，该值最初为 null。

`targetValue` 参数应包含 State 正在向其进行动画过渡的目标值。例如，如果 State 正在对其组件的 opacity 值进行动画处理，则此参数应包含该组件当前的 opacity 值。

`constructor` 参数应包含一个函数，该函数接收一个值（即正在被动画处理的组件的值），并返回一个从该值开始的补间动画。

{@endtemplate}

`forEachTween()` 应将其补间动画值更新为此访问者（visitor）的返回值。

`<T>` 参数指定正在被动画处理的值的类型。

# ImplicitlyAnimatedWidgetState

```dart
abstract class ImplicitlyAnimatedWidgetState<T extends ImplicitlyAnimatedWidget> extends State<T> with SingleTickerProviderStateMixin<T> {}
```

带有隐式动画的组件的 `State` 基类。

[ImplicitlyAnimatedWidgetState](https://www.yuque.com/thyname/flutter.widgets/implicitlyanimatedwidgetstate) 要求子类自行响应动画。如果你希望在动画变化时自动调用 `setState()`，请使用 [AnimatedWidgetBaseState](https://www.yuque.com/thyname/flutter.widgets/animatedwidgetbasestate)。

子类选择进行动画处理的属性由 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 实例表示。子类必须实现 [forEachTween] 方法，以允许 [ImplicitlyAnimatedWidgetState](https://www.yuque.com/thyname/flutter.widgets/implicitlyanimatedwidgetstate) 遍历组件的字段并对其进行动画处理。

### controller

```dart
AnimationController controller
```

驱动此组件隐式动画的动画控制器。

### animation

```dart
Animation<double> get animation
```

驱动此组件隐式动画的 animation。

### initState()

```dart
void initState()
```

### didUpdateWidget()

```dart
void didUpdateWidget(T oldWidget)
```

### dispose()

```dart
void dispose()
```

### forEachTween()

```dart
void forEachTween(TweenVisitor<dynamic> visitor)
```

使用指定的 `visitor` 函数访问此 State 所控制的每个补间动画。

### 子类职责

要进行动画处理的属性由 State 中的 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 成员变量表示。对于每个这样的补间动画，[forEachTween] 的实现应使用适当的参数调用 `visitor`，并将结果存回该成员变量。传递给 `visitor` 的参数如下：

{@macro flutter.widgets.TweenVisitor.arguments}

### 此方法何时被调用

[forEachTween] 最初会在 [initState] 期间被调用。此时，visitor 的 `tween` 参数预期会被设为 null，从而使 visitor 调用其 `constructor` 参数来首次构造补间动画。生成的补间动画的 `begin` 值将被设为目标值，而 `end` 值将被设为 null。此时动画不会启动。

当此 State 的 [widget] 被更新时（从而触发 [didUpdateWidget] 方法被调用），[forEachTween] 将再次被调用，以检查目标值是否发生了变化。如果目标值发生了变化（表明 [animation](https://www.yuque.com/thyname/flutter.animation) 应该启动），则 visitor 会相应地更新补间动画的 `start` 和 `end` 值，并启动动画。

### 其他成员变量

包含基于 [forEachTween] 所创建的补间动画的属性的子类，应重写 [didUpdateTweens] 以更新这些属性。依赖属性不应在 [forEachTween] 中更新。

{@tool snippet}

此示例实现了一个隐式动画组件的 `State`。每当 `widget.targetColor` 发生变化时，该组件都会在颜色之间进行动画过渡。

```dart
class MyWidgetState extends AnimatedWidgetBaseState<MyWidget> {
  ColorTween? _colorTween;

  @override
  Widget build(BuildContext context) {
    return Text(
      'Hello World',
      // Computes the value of the text color at any given time.
      style: TextStyle(color: _colorTween?.evaluate(animation)),
    );
  }

  @override
  void forEachTween(TweenVisitor<dynamic> visitor) {
    // Update the tween using the provided visitor function.
    _colorTween = visitor(
      // The latest tween value. Can be `null`.
      _colorTween,
      // The color value toward which we are animating.
      widget.targetColor,
      // A function that takes a color value and returns a tween
      // beginning at that value.
      (dynamic value) => ColorTween(begin: value as Color?),
    ) as ColorTween?;

    // We could have more tweens than one by using the visitor
    // multiple times.
  }
}
```

{@end-tool}

### didUpdateTweens()

```dart
void didUpdateTweens()
```

供子类使用的可选钩子，会在所有补间动画通过 [forEachTween] 更新完成之后运行。

任何依赖于 [forEachTween] 所创建的补间动画的属性都应在 [didUpdateTweens] 中更新，而不是在 [forEachTween] 中更新。

此方法会在以下两种情况下被调用：

1. 在补间动画最初被构造之后（通过传递给 [forEachTween] 的 [TweenVisitor](https://www.yuque.com/thyname/flutter.widgets/tweenvisitor) 的 `constructor` 参数构造）。在这种情况下，这些补间动画很可能只包含一个 [Tween.begin] 值，而不包含 [Tween.end] 值。

2. 当 State 的 [widget] 被更新，且 [forEachTween] 所访问的一个或多个补间动画指定了与组件当前值不同的目标值时（表明 [animation](https://www.yuque.com/thyname/flutter.animation) 应该运行）。在这种情况下，每个补间动画的 [Tween.begin] 值将是根据当前 [animation](https://www.yuque.com/thyname/flutter.animation) 对该补间动画求值的结果，而 [Tween.end] 值将是目标值。

# AnimatedWidgetBaseState

```dart
abstract class AnimatedWidgetBaseState<T extends ImplicitlyAnimatedWidget> extends ImplicitlyAnimatedWidgetState<T> {}
```

带有隐式动画、且需要在动画运行时重建其组件树的组件的 State 基类。

此类会在动画每次 tick 时调用 [build]。对于不需要每帧都重建的变体，可以考虑直接继承 [ImplicitlyAnimatedWidgetState](https://www.yuque.com/thyname/flutter.widgets/implicitlyanimatedwidgetstate)。

子类必须实现 [forEachTween] 方法，以允许 [AnimatedWidgetBaseState](https://www.yuque.com/thyname/flutter.widgets/animatedwidgetbasestate) 遍历子类组件的字段并对其进行动画处理。

### initState()

```dart
void initState()
```

# AnimatedContainer

```dart
class AnimatedContainer extends ImplicitlyAnimatedWidget {}
```

[Container](https://www.yuque.com/thyname/flutter.widgets/container) 的动画版本，会在一段时间内逐渐改变其值。

当属性发生变化时，[AnimatedContainer](https://www.yuque.com/thyname/flutter.widgets/animatedcontainer) 会使用所提供的曲线和时长，自动在属性的新旧值之间进行动画过渡。为 null 的属性不会被动画处理。它的子组件及后代不会被动画处理。

此类可用于借助其内部的 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)，为 Container 的不同参数之间生成简单的隐式过渡动画。对于更复杂的动画，你可能需要使用 [AnimatedWidget](https://www.yuque.com/thyname/flutter.widgets/animatedwidget) 的子类，例如 [DecoratedBoxTransition](https://www.yuque.com/thyname/flutter.widgets/decoratedboxtransition)，或使用你自己的 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)。

{@youtube 560 315 https://www.youtube.com/watch?v=yI-8QHpGIP4}

{@tool dartpad} 以下示例（如上图所示）在两种状态之间对 AnimatedContainer 进行过渡。点按时会调整 `height`、`width`、`color` 和 [alignment] 属性。

** See code in examples/api/lib/widgets/implicit_animations/animated_container.0.dart ** {@end-tool}

另请参阅：

- [AnimatedPadding](https://www.yuque.com/thyname/flutter.widgets/animatedpadding)，此组件的一个子集，仅支持对 [padding] 进行动画处理。
- [布局组件目录](https://flutter.dev/widgets/layout/)。
- [AnimatedPositioned](https://www.yuque.com/thyname/flutter.widgets/animatedpositioned)，作为 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的子组件时，每当给定的位置发生变化，都会自动对子组件的位置进行动画过渡。
- [AnimatedAlign](https://www.yuque.com/thyname/flutter.widgets/animatedalign)，每当给定的 [AnimatedAlign.alignment] 发生变化，都会自动对子组件的位置进行动画过渡。
- [AnimatedSwitcher](https://www.yuque.com/thyname/flutter.widgets/animatedswitcher)，将一个子组件替换为一个新的子组件，并支持自定义过渡效果。
- [AnimatedCrossFade](https://www.yuque.com/thyname/flutter.widgets/animatedcrossfade)，在两个子组件之间淡入淡出，并对它们的尺寸进行插值。

### AnimatedContainer()

```dart
AnimatedContainer({dynamic key, AlignmentGeometry? alignment, EdgeInsetsGeometry? padding, Color? color, Decoration? decoration, Decoration? foregroundDecoration, double? width, double? height, BoxConstraints? constraints, EdgeInsetsGeometry? margin, Matrix4? transform, AlignmentGeometry? transformAlignment, Widget? child, Clip clipBehavior = Clip.none, dynamic curve, required Duration duration, dynamic onEnd})
```

创建一个隐式对其参数进行动画处理的 container。

### child

```dart
Widget? child
```

此 container 所包含的 [child]。

如果为 null，且 [constraints] 为无界（unbounded）或同样为 null，则此 container 将扩展以填充其父组件中所有的可用空间，除非父组件提供了无界约束，此时该 container 将尝试尽可能小。

{@macro flutter.widgets.ProxyWidget.child}

### alignment

```dart
AlignmentGeometry? alignment
```

在 container 内部对齐 [child]。

如果非 null，该 container 将扩展以填充其父组件，并根据给定值在其内部定位子组件。如果传入的约束是无界的，则子组件将改为进行收缩包裹（shrink-wrapped）。

如果 [child] 为 null，则忽略此项。

另请参阅：

- [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，一个包含常用便捷常量的类，通常用于指定 [AlignmentGeometry](https://www.yuque.com/thyname/flutter.painting/alignmentgeometry)。
- [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)，与 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 类似，但用于指定相对于文本方向的对齐方式。

### padding

```dart
EdgeInsetsGeometry? padding
```

在 [decoration] 内部预留的空白空间。如果存在 [child]，它会被放置在此内边距之内。

### decoration

```dart
Decoration? decoration
```

在 [child] 后方绘制的装饰。

若只需指定纯色，可以在构造函数中使用一种简写方式：设置 `color` 参数以代替 `decoration` 参数。

### foregroundDecoration

```dart
Decoration? foregroundDecoration
```

在子组件前方绘制的装饰。

### constraints

```dart
BoxConstraints? constraints
```

施加于子组件的附加约束。

构造函数中的 `width` 和 `height` 参数会与 `constraints` 参数相结合，以设置此属性。

[padding] 位于约束内部。

### margin

```dart
EdgeInsetsGeometry? margin
```

围绕 [decoration] 和 [child] 的空白空间。

### transform

```dart
Matrix4? transform
```

在绘制 container 之前应用的变换矩阵。

### transformAlignment

```dart
AlignmentGeometry? transformAlignment
```

如果指定了 [transform]，则表示原点相对于 container 尺寸的对齐方式。

当 [transform] 为 null 时，此属性的值会被忽略。

另请参阅：

- [Transform.alignment]，由此属性设置。

### clipBehavior

```dart
Clip clipBehavior
```

当 [AnimatedContainer.decoration] 非 null 时的裁剪行为。

默认值为 [Clip.none]。如果 [decoration] 为 null，则此值必须为 [Clip.none]。

与 AnimatedContainer 的其他属性不同，此属性的变化会立即生效，不会进行动画处理。

如果需要应用裁剪，所提供的装饰的 [Decoration.getClipPath] 方法必须返回一个裁剪路径。（并非所有装饰都支持此项；该方法的默认实现会抛出 [UnsupportedError](https://www.yuque.com/thyname/dart.core/unsupportederror)。）

### createState()

```dart
AnimatedWidgetBaseState<AnimatedContainer> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedPadding

```dart
class AnimatedPadding extends ImplicitlyAnimatedWidget {}
```

[Padding](https://www.yuque.com/thyname/flutter.widgets/padding) 的动画版本，每当给定的内边距发生变化，会在给定的时长内自动过渡其缩进量。

{@youtube 560 315 https://www.youtube.com/watch?v=PY2m0fhGNz4}

以下展示了使用此组件、并配合 [Curves.fastOutSlowIn] 这一 [curve] 时的效果。 {@animation 250 266 https://flutter.github.io/assets-for-api-docs/assets/widgets/animated_padding.mp4}

{@tool dartpad} 以下代码实现了 [AnimatedPadding](https://www.yuque.com/thyname/flutter.widgets/animatedpadding) 组件，使用 [Curves.easeInOut] 作为 [curve]。

** See code in examples/api/lib/widgets/implicit_animations/animated_padding.0.dart ** {@end-tool}

另请参阅：

- [AnimatedContainer](https://www.yuque.com/thyname/flutter.widgets/animatedcontainer)，可以一次性过渡更多的值。
- [AnimatedAlign](https://www.yuque.com/thyname/flutter.widgets/animatedalign)，每当给定的 [AnimatedAlign.alignment] 发生变化，都会自动对子组件的位置进行动画过渡。

### AnimatedPadding()

```dart
AnimatedPadding({dynamic key, required EdgeInsetsGeometry padding, Widget? child, dynamic curve, required Duration duration, dynamic onEnd})
```

创建一个组件，对其子组件的内边距进行隐式动画处理。

### padding

```dart
EdgeInsetsGeometry padding
```

用于内缩子组件的空间量。

### child

```dart
Widget? child
```

此组件在组件树中的下一级子组件。

{@macro flutter.widgets.ProxyWidget.child}

### createState()

```dart
AnimatedWidgetBaseState<AnimatedPadding> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedAlign

```dart
class AnimatedAlign extends ImplicitlyAnimatedWidget {}
```

[Align](https://www.yuque.com/thyname/flutter.widgets/align) 的动画版本，每当给定的 [alignment] 发生变化，会在给定的时长内自动过渡子组件的位置。

以下展示了使用 [Curves.fastOutSlowIn] 这一 [curve] 时的效果。 {@animation 250 266 https://flutter.github.io/assets-for-api-docs/assets/widgets/animated_align.mp4}

对于动画效果，你可以选择 [curve] 及 [duration]，该组件将自动向新的目标 [alignment] 进行动画过渡。如果你需要对动画进行更精细的控制（例如希望在动画中途停止），可以考虑改用 [AlignTransition](https://www.yuque.com/thyname/flutter.widgets/aligntransition)，它接收一个由调用方提供的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 作为参数。虽然这样可以对动画进行精细调整，但也需要更多的开发工作，因为你必须手动管理底层 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 的生命周期。

{@tool dartpad} 以下代码实现了 [AnimatedAlign](https://www.yuque.com/thyname/flutter.widgets/animatedalign) 组件，使用 [Curves.fastOutSlowIn] 作为 [curve]。

** See code in examples/api/lib/widgets/implicit_animations/animated_align.0.dart ** {@end-tool}

另请参阅：

- [AnimatedContainer](https://www.yuque.com/thyname/flutter.widgets/animatedcontainer)，可以一次性过渡更多的值。
- [AnimatedPadding](https://www.yuque.com/thyname/flutter.widgets/animatedpadding)，可以对内边距而非对齐方式进行动画处理。
- [AnimatedSlide](https://www.yuque.com/thyname/flutter.widgets/animatedslide)，可以按照相对于子组件自身尺寸的给定偏移量，对子组件的平移进行动画处理。
- [AnimatedPositioned](https://www.yuque.com/thyname/flutter.widgets/animatedpositioned)，作为 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的子组件时，每当给定的位置发生变化，都会自动对子组件的位置进行动画过渡。

### AnimatedAlign()

```dart
AnimatedAlign({dynamic key, required AlignmentGeometry alignment, Widget? child, double? heightFactor, double? widthFactor, dynamic curve, required Duration duration, dynamic onEnd})
```

创建一个组件，对其子组件按照可隐式过渡的对齐方式进行定位。

### alignment

```dart
AlignmentGeometry alignment
```

如何对齐子组件。

[Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 的 x 值和 y 值分别控制水平和垂直方向的对齐方式。x 值为 -1.0 表示子组件的左边缘与父组件的左边缘对齐，而 x 值为 1.0 表示子组件的右边缘与父组件的右边缘对齐。其他值将进行线性插值（及外插）。例如，值为 0.0 表示子组件的中心与父组件的中心对齐。

另请参阅：

- [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，包含更多细节以及一些用于常见位置的便捷常量。
- [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)，其水平坐标方向取决于 [TextDirection](https://www.yuque.com/thyname/dart.ui/textdirection)。

### child

```dart
Widget? child
```

此组件在组件树中的下一级子组件。

{@macro flutter.widgets.ProxyWidget.child}

### heightFactor

```dart
double? heightFactor
```

如果非 null，会将其高度设置为子组件高度乘以此系数。

必须大于或等于 0.0，默认值为 null。

### widthFactor

```dart
double? widthFactor
```

如果非 null，会将其宽度设置为子组件宽度乘以此系数。

必须大于或等于 0.0，默认值为 null。

### createState()

```dart
AnimatedWidgetBaseState<AnimatedAlign> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedPositioned

```dart
class AnimatedPositioned extends ImplicitlyAnimatedWidget {}
```

[Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned) 的动画版本，每当给定的位置发生变化，会在给定的时长内自动过渡子组件的位置。

{@youtube 560 315 https://www.youtube.com/watch?v=hC3s2YdtWt8}

仅当它是 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的子组件时才生效。

如果子组件的*尺寸*会因此动画而发生变化，此组件是一个不错的选择。如果尺寸应保持不变，仅*位置*随时间变化，则可考虑改用 [SlideTransition](https://www.yuque.com/thyname/flutter.widgets/slidetransition)。[SlideTransition](https://www.yuque.com/thyname/flutter.widgets/slidetransition) 在动画的每一帧只会触发重绘（repaint），而 [AnimatedPositioned](https://www.yuque.com/thyname/flutter.widgets/animatedpositioned) 还会触发重新布局（relayout）。

以下展示了使用此组件、并配合 [Curves.fastOutSlowIn] 这一 [curve] 时的效果。 {@animation 250 266 https://flutter.github.io/assets-for-api-docs/assets/widgets/animated_positioned.mp4}

对于动画效果，你可以选择 [curve] 及 [duration]，该组件将自动向新的目标位置进行动画过渡。如果你需要对动画进行更精细的控制（例如希望在动画中途停止），可以考虑改用 [PositionedTransition](https://www.yuque.com/thyname/flutter.widgets/positionedtransition)，它接收一个由调用方提供的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 作为参数。虽然这样可以对动画进行精细调整，但也需要更多的开发工作，因为你必须手动管理底层 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 的生命周期。

{@tool dartpad} 以下示例在两种状态之间对 AnimatedPositioned 进行过渡。点按时会调整 `height`、`width` 及 [Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned) 属性。

** See code in examples/api/lib/widgets/implicit_animations/animated_positioned.0.dart ** {@end-tool}

另请参阅：

- [AnimatedPositionedDirectional](https://www.yuque.com/thyname/flutter.widgets/animatedpositioneddirectional)，适应环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)（与此组件相同，但用于对 [PositionedDirectional](https://www.yuque.com/thyname/flutter.widgets/positioneddirectional) 进行动画处理）。

### AnimatedPositioned()

```dart
AnimatedPositioned({dynamic key, required Widget child, double? left, double? top, double? right, double? bottom, double? width, double? height, dynamic curve, required Duration duration, dynamic onEnd})
```

创建一个组件，对其位置进行隐式动画处理。

三个水平方向值（[left]、[right]、[width]）中只能设置两个，三个垂直方向值（[top]、[bottom]、[height]）中也只能设置两个。在每种情况下，三者中至少有一个必须为 null。

### AnimatedPositioned.fromRect()

```dart
AnimatedPositioned.fromRect({dynamic key, required Widget child, required Rect rect, dynamic curve, required Duration duration, dynamic onEnd})
```

创建一个组件，对其所占据的矩形区域进行隐式动画处理。

### child

```dart
Widget child
```

此组件在组件树中的下一级子组件。

{@macro flutter.widgets.ProxyWidget.child}

### left

```dart
double? left
```

子组件左边缘相对于 stack 左边缘的偏移量。

### top

```dart
double? top
```

子组件顶部边缘相对于 stack 顶部边缘的偏移量。

### right

```dart
double? right
```

子组件右边缘相对于 stack 右边缘的偏移量。

### bottom

```dart
double? bottom
```

子组件底部边缘相对于 stack 底部边缘的偏移量。

### width

```dart
double? width
```

子组件的宽度。

三个水平方向值（[left]、[right]、[width]）中只能设置两个，第三个必须为 null。

### height

```dart
double? height
```

子组件的高度。

三个垂直方向值（[top]、[bottom]、[height]）中只能设置两个，第三个必须为 null。

### createState()

```dart
AnimatedWidgetBaseState<AnimatedPositioned> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedPositionedDirectional

```dart
class AnimatedPositionedDirectional extends ImplicitlyAnimatedWidget {}
```

[PositionedDirectional](https://www.yuque.com/thyname/flutter.widgets/positioneddirectional) 的动画版本，每当给定的位置发生变化，会在给定的时长内自动过渡子组件的位置。

环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 用于确定 [start] 位于左侧还是右侧。

仅当它是 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的子组件时才生效。

如果子组件的*尺寸*会因此动画而发生变化，此组件是一个不错的选择。如果尺寸应保持不变，仅*位置*随时间变化，则可考虑改用 [SlideTransition](https://www.yuque.com/thyname/flutter.widgets/slidetransition)。[SlideTransition](https://www.yuque.com/thyname/flutter.widgets/slidetransition) 在动画的每一帧只会触发重绘，而 [AnimatedPositionedDirectional](https://www.yuque.com/thyname/flutter.widgets/animatedpositioneddirectional) 还会触发重新布局。（[SlideTransition](https://www.yuque.com/thyname/flutter.widgets/slidetransition) 同时也能感知文本方向。）

以下展示了使用此组件、并配合 [Curves.fastOutSlowIn] 这一 [curve] 时的效果。 {@animation 250 266 https://flutter.github.io/assets-for-api-docs/assets/widgets/animated_positioned_directional.mp4}

另请参阅：

- [AnimatedPositioned](https://www.yuque.com/thyname/flutter.widgets/animatedpositioned)，以视觉方式指定组件的位置（与此组件相同，但用于对 [Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned) 进行动画处理）。

### AnimatedPositionedDirectional()

```dart
AnimatedPositionedDirectional({dynamic key, required Widget child, double? start, double? top, double? end, double? bottom, double? width, double? height, dynamic curve, required Duration duration, dynamic onEnd})
```

创建一个组件，对其位置进行隐式动画处理。

三个水平方向值（[start]、[end]、[width]）中只能设置两个，三个垂直方向值（[top]、[bottom]、[height]）中也只能设置两个。在每种情况下，三者中至少有一个必须为 null。

### child

```dart
Widget child
```

此组件在组件树中的下一级子组件。

{@macro flutter.widgets.ProxyWidget.child}

### start

```dart
double? start
```

子组件起始边缘相对于 stack 起始边缘的偏移量。

### top

```dart
double? top
```

子组件顶部边缘相对于 stack 顶部边缘的偏移量。

### end

```dart
double? end
```

子组件结束边缘相对于 stack 结束边缘的偏移量。

### bottom

```dart
double? bottom
```

子组件底部边缘相对于 stack 底部边缘的偏移量。

### width

```dart
double? width
```

子组件的宽度。

三个水平方向值（[start]、[end]、[width]）中只能设置两个，第三个必须为 null。

### height

```dart
double? height
```

子组件的高度。

三个垂直方向值（[top]、[bottom]、[height]）中只能设置两个，第三个必须为 null。

### createState()

```dart
AnimatedWidgetBaseState<AnimatedPositionedDirectional> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedScale

```dart
class AnimatedScale extends ImplicitlyAnimatedWidget {}
```

[Transform.scale] 的动画版本，每当给定的缩放比例发生变化，会在给定的时长内自动过渡子组件的缩放比例。

{@tool snippet}

以下代码定义了一个组件，它使用 [AnimatedScale](https://www.yuque.com/thyname/flutter.widgets/animatedscale) 在每次按下按钮时，将 [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 的尺寸逐渐变化为一个新的缩放比例。

```dart
class LogoScale extends StatefulWidget {
  const LogoScale({super.key});

  @override
  State<LogoScale> createState() => LogoScaleState();
}

class LogoScaleState extends State<LogoScale> {
  double scale = 1.0;

  void _changeScale() {
    setState(() => scale = scale == 1.0 ? 3.0 : 1.0);
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        ElevatedButton(
          onPressed: _changeScale,
          child: const Text('Scale Logo'),
        ),
        Padding(
          padding: const EdgeInsets.all(50),
          child: AnimatedScale(
            scale: scale,
            duration: const Duration(seconds: 2),
            child: const FlutterLogo(),
          ),
        ),
      ],
    );
  }
}
```

{@end-tool}

另请参阅：

- [AnimatedRotation](https://www.yuque.com/thyname/flutter.widgets/animatedrotation)，用于对子组件的旋转进行动画处理。
- [AnimatedSize](https://www.yuque.com/thyname/flutter.widgets/animatedsize)，用于根据布局变化对子组件的尺寸调整进行动画处理。
- [AnimatedSlide](https://www.yuque.com/thyname/flutter.widgets/animatedslide)，用于按照相对于子组件自身尺寸的给定偏移量，对子组件的平移进行动画处理。
- [ScaleTransition](https://www.yuque.com/thyname/flutter.widgets/scaletransition)，此组件的显式动画版本，其中 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 由调用方提供，而非内置。

### AnimatedScale()

```dart
AnimatedScale({dynamic key, Widget? child, required double scale, Alignment alignment = Alignment.center, FilterQuality? filterQuality, dynamic curve, required Duration duration, dynamic onEnd})
```

创建一个组件，对其缩放比例进行隐式动画处理。

### child

```dart
Widget? child
```

此组件在组件树中的下一级子组件。

{@macro flutter.widgets.ProxyWidget.child}

### scale

```dart
double scale
```

目标缩放比例。

### alignment

```dart
Alignment alignment
```

缩放操作所在坐标系原点的对齐方式，相对于盒子的尺寸而言。

例如，要将缩放原点设置为底部居中，可以使用对齐值 (0.0, 1.0)。

### filterQuality

```dart
FilterQuality? filterQuality
```

以位图操作方式应用此变换时所使用的过滤质量。

{@macro flutter.widgets.Transform.optional.FilterQuality}

### createState()

```dart
ImplicitlyAnimatedWidgetState<AnimatedScale> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedRotation

```dart
class AnimatedRotation extends ImplicitlyAnimatedWidget {}
```

[Transform.rotate] 的动画版本，每当给定的旋转角度发生变化，会在给定的时长内自动过渡子组件的旋转。

{@tool snippet}

以下代码定义了一个组件，它使用 [AnimatedRotation](https://www.yuque.com/thyname/flutter.widgets/animatedrotation)，每次按下按钮时将 [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 逐渐旋转八分之一圈（45 度）。

```dart
class LogoRotate extends StatefulWidget {
  const LogoRotate({super.key});

  @override
  State<LogoRotate> createState() => LogoRotateState();
}

class LogoRotateState extends State<LogoRotate> {
  double turns = 0.0;

  void _changeRotation() {
    setState(() => turns += 1.0 / 8.0);
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        ElevatedButton(
          onPressed: _changeRotation,
          child: const Text('Rotate Logo'),
        ),
        Padding(
          padding: const EdgeInsets.all(50),
          child: AnimatedRotation(
            turns: turns,
            duration: const Duration(seconds: 1),
            child: const FlutterLogo(),
          ),
        ),
      ],
    );
  }
}
```

{@end-tool}

另请参阅：

- [AnimatedScale](https://www.yuque.com/thyname/flutter.widgets/animatedscale)，用于对子组件的缩放进行动画处理。
- [RotationTransition](https://www.yuque.com/thyname/flutter.widgets/rotationtransition)，此组件的显式动画版本，其中 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 由调用方提供，而非内置。

### AnimatedRotation()

```dart
AnimatedRotation({dynamic key, Widget? child, required double turns, Alignment alignment = Alignment.center, FilterQuality? filterQuality, dynamic curve, required Duration duration, dynamic onEnd})
```

创建一个组件，对其旋转进行隐式动画处理。

### child

```dart
Widget? child
```

此组件在组件树中的下一级子组件。

{@macro flutter.widgets.ProxyWidget.child}

### turns

```dart
double turns
```

控制子组件旋转的动画。

如果当前 turns 动画的值为 v，则子组件在绘制之前将旋转 v _ 2 _ pi 弧度。

### alignment

```dart
Alignment alignment
```

旋转操作所在坐标系原点的对齐方式，相对于盒子的尺寸而言。

例如，要将旋转原点设置为底部居中，可以使用对齐值 (0.0, 1.0)。

### filterQuality

```dart
FilterQuality? filterQuality
```

以位图操作方式应用此变换时所使用的过滤质量。

{@macro flutter.widgets.Transform.optional.FilterQuality}

### createState()

```dart
ImplicitlyAnimatedWidgetState<AnimatedRotation> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedSlide

```dart
class AnimatedSlide extends ImplicitlyAnimatedWidget {}
```

一个组件，每当给定的偏移量发生变化，会自动过渡子组件相对于其正常位置的偏移。

此平移以一个相对于子组件尺寸进行缩放的 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 表示。例如，`dx` 为 0.25 的 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 将导致水平方向上平移子组件宽度的四分之一。

{@tool dartpad} 以下代码定义了一个组件，它使用 [AnimatedSlide](https://www.yuque.com/thyname/flutter.widgets/animatedslide)，通过拖动 X 轴和 Y 轴滑块，将 [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 沿上下和左右方向进行平移。

** See code in examples/api/lib/widgets/implicit_animations/animated_slide.0.dart ** {@end-tool}

另请参阅：

- [AnimatedPositioned](https://www.yuque.com/thyname/flutter.widgets/animatedpositioned)，作为 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的子组件时，每当给定的位置发生变化，都会自动对子组件的位置进行动画过渡。
- [AnimatedAlign](https://www.yuque.com/thyname/flutter.widgets/animatedalign)，每当给定的 [AnimatedAlign.alignment] 发生变化，都会自动对子组件的位置进行动画过渡。

### AnimatedSlide()

```dart
AnimatedSlide({dynamic key, Widget? child, required Offset offset, dynamic curve, required Duration duration, dynamic onEnd})
```

创建一个组件，对其偏移平移进行隐式动画处理。

### child

```dart
Widget? child
```

此组件在组件树中的下一级子组件。

{@macro flutter.widgets.ProxyWidget.child}

### offset

```dart
Offset offset
```

目标偏移量。子组件将水平方向平移 `width * dx`，垂直方向平移 `height * dy`。

### createState()

```dart
ImplicitlyAnimatedWidgetState<AnimatedSlide> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedOpacity

```dart
class AnimatedOpacity extends ImplicitlyAnimatedWidget {}
```

[Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity) 的动画版本，每当给定的不透明度发生变化，会在给定的时长内自动过渡子组件的不透明度。

{@youtube 560 315 https://www.youtube.com/watch?v=QZAvjqOqiLY}

对不透明度进行动画处理的开销相对较大，因为这需要将子组件绘制到一个中间缓冲区中。

以下展示了使用此组件、并配合 [Curves.fastOutSlowIn] 这一 [curve] 时的效果。 {@animation 250 266 https://flutter.github.io/assets-for-api-docs/assets/widgets/animated_opacity.mp4}

{@tool snippet}

```dart
class LogoFade extends StatefulWidget {
  const LogoFade({super.key});

  @override
  State<LogoFade> createState() => LogoFadeState();
}

class LogoFadeState extends State<LogoFade> {
  double opacityLevel = 1.0;

  void _changeOpacity() {
    setState(() => opacityLevel = opacityLevel == 0 ? 1.0 : 0.0);
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        AnimatedOpacity(
          opacity: opacityLevel,
          duration: const Duration(seconds: 3),
          child: const FlutterLogo(),
        ),
        ElevatedButton(
          onPressed: _changeOpacity,
          child: const Text('Fade Logo'),
        ),
      ],
    );
  }
}
```

{@end-tool}

## 命中测试（Hit testing）

将 [opacity] 设置为零并不会阻止对 [AnimatedOpacity](https://www.yuque.com/thyname/flutter.widgets/animatedopacity) 后代组件进行命中测试。这可能会使用户感到困惑，因为用户可能看不到任何内容，却可能误以为界面中 [AnimatedOpacity](https://www.yuque.com/thyname/flutter.widgets/animatedopacity) 隐藏组件所在的区域是不可交互的。

对于某些仅在绘制时才计算其位置的组件（例如 [Flow](https://www.yuque.com/thyname/flutter.widgets/flow)），这实际上可能导致错误（从意外的几何形状到异常），因为当 opacity 动画达到零时，这些组件根本不会被 [AnimatedOpacity](https://www.yuque.com/thyname/flutter.widgets/animatedopacity) 组件绘制。

为避免此类问题，通常建议在将 [opacity] 设置为零时使用 [IgnorePointer](https://www.yuque.com/thyname/flutter.widgets/ignorepointer) 组件。这样可以在 [child] 消失动画期间阻止与该子树中任何子组件的交互。

另请参阅：

- [AnimatedCrossFade](https://www.yuque.com/thyname/flutter.widgets/animatedcrossfade)，用于在两个子组件之间淡入淡出。
- [AnimatedSwitcher](https://www.yuque.com/thyname/flutter.widgets/animatedswitcher)，用于在多个子组件之间依次淡入淡出。
- [FadeTransition](https://www.yuque.com/thyname/flutter.widgets/fadetransition)，此组件的显式动画版本，其中 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 由调用方提供，而非内置。
- [SliverAnimatedOpacity](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedopacity)，用于在给定的时长内自动过渡 _sliver_ 的不透明度（每当给定的不透明度发生变化）。

### AnimatedOpacity()

```dart
AnimatedOpacity({dynamic key, Widget? child, required double opacity, dynamic curve, required Duration duration, dynamic onEnd, bool alwaysIncludeSemantics = false})
```

创建一个组件，对其不透明度进行隐式动画处理。

[opacity] 参数必须在零到一之间（含边界值）。

### child

```dart
Widget? child
```

此组件在组件树中的下一级子组件。

{@macro flutter.widgets.ProxyWidget.child}

### opacity

```dart
double opacity
```

目标不透明度。

不透明度为 1.0 表示完全不透明；不透明度为 0.0 表示完全透明（即不可见）。

### alwaysIncludeSemantics

```dart
bool alwaysIncludeSemantics
```

是否始终包含子组件的语义信息。

默认值为 false。

如果为 true，则无论不透明度设置如何，子组件的语义信息都会被暴露，就像该组件完全可见一样。这在某些标签可能在动画过程中被隐藏、但仍需暴露相关语义的场景中很有用。

### createState()

```dart
ImplicitlyAnimatedWidgetState<AnimatedOpacity> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SliverAnimatedOpacity

```dart
class SliverAnimatedOpacity extends ImplicitlyAnimatedWidget {}
```

[SliverOpacity](https://www.yuque.com/thyname/flutter.widgets/sliveropacity) 的动画版本，每当给定的不透明度发生变化，会在给定的时长内自动过渡 sliver 子组件的不透明度。

对不透明度进行动画处理的开销相对较大，因为这需要将 sliver 子组件绘制到一个中间缓冲区中。

以下展示了使用此组件、并配合 [Curves.fastOutSlowIn] 这一 [curve] 时的效果。

{@tool dartpad} 创建一个包含 [SliverFixedExtentList](https://www.yuque.com/thyname/flutter.widgets/sliverfixedextentlist) 和 [FloatingActionButton](https://www.yuque.com/thyname/flutter.material/floatingactionbutton) 的 [CustomScrollView](https://www.yuque.com/thyname/flutter.widgets/customscrollview)。按下按钮会对列表的不透明度进行动画处理。

** See code in examples/api/lib/widgets/implicit_animations/sliver_animated_opacity.0.dart ** {@end-tool}

## 命中测试（Hit testing）

将 [opacity] 设置为零并不会阻止对 [SliverAnimatedOpacity](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedopacity) 后代组件进行命中测试。这可能会使用户感到困惑，因为用户可能看不到任何内容，却可能误以为界面中 [SliverAnimatedOpacity](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedopacity) 隐藏组件所在的区域是不可交互的。

对于某些仅在绘制时才计算其位置的组件（例如 [Flow](https://www.yuque.com/thyname/flutter.widgets/flow)），这实际上可能导致错误（从意外的几何形状到异常），因为当 opacity 动画达到零时，这些组件根本不会被 [SliverAnimatedOpacity](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedopacity) 组件绘制。

为避免此类问题，通常建议在将 [opacity] 设置为零时使用 [SliverIgnorePointer](https://www.yuque.com/thyname/flutter.widgets/sliverignorepointer) 组件。这样可以在 [sliver] 消失动画期间阻止与该子树中任何子组件的交互。

另请参阅：

- [SliverFadeTransition](https://www.yuque.com/thyname/flutter.widgets/sliverfadetransition)，此组件的显式动画版本，其中 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 由调用方提供，而非内置。
- [AnimatedOpacity](https://www.yuque.com/thyname/flutter.widgets/animatedopacity)，用于在给定的时长内自动过渡盒子子组件的不透明度（每当给定的不透明度发生变化）。

### SliverAnimatedOpacity()

```dart
SliverAnimatedOpacity({dynamic key, Widget? sliver, required double opacity, dynamic curve, required Duration duration, dynamic onEnd, bool alwaysIncludeSemantics = false})
```

创建一个组件，对其不透明度进行隐式动画处理。

[opacity] 参数必须在零到一之间（含边界值）。

### sliver

```dart
Widget? sliver
```

此组件在组件树中的下一级 sliver 子组件。

### opacity

```dart
double opacity
```

目标不透明度。

不透明度为 1.0 表示完全不透明；不透明度为 0.0 表示完全透明（即不可见）。

### alwaysIncludeSemantics

```dart
bool alwaysIncludeSemantics
```

是否始终包含 sliver 子组件的语义信息。

默认值为 false。

如果为 true，则无论不透明度设置如何，sliver 子组件的语义信息都会被暴露，就像该组件完全可见一样。这在某些标签可能在动画过程中被隐藏、但仍需暴露相关语义的场景中很有用。

### createState()

```dart
ImplicitlyAnimatedWidgetState<SliverAnimatedOpacity> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedDefaultTextStyle

```dart
class AnimatedDefaultTextStyle extends ImplicitlyAnimatedWidget {}
```

[DefaultTextStyle](https://www.yuque.com/thyname/flutter.widgets/defaulttextstyle) 的动画版本，每当给定的样式发生变化，会在给定的时长内自动过渡默认文本样式（即应用于未显式指定样式的后代 [Text](https://www.yuque.com/thyname/flutter.widgets/text) 组件的文本样式）。

[textAlign]、[softWrap]、[overflow]、[maxLines]、[textWidthBasis] 和 [textHeightBehavior] 属性不会被动画处理，变化时会立即生效。

以下展示了使用 [Curves.elasticInOut] 这一 [curve] 时的效果。 {@animation 250 266 https://flutter.github.io/assets-for-api-docs/assets/widgets/animated_default_text_style.mp4}

对于动画效果，你可以选择 [curve] 及 [duration]，该组件将自动向新的默认文本样式进行动画过渡。如果你需要对动画进行更精细的控制（例如希望在动画中途停止），可以考虑改用 [DefaultTextStyleTransition](https://www.yuque.com/thyname/flutter.widgets/defaulttextstyletransition)，它接收一个由调用方提供的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 作为参数。虽然这样可以对动画进行精细调整，但也需要更多的开发工作，因为你必须手动管理底层 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 的生命周期。

### AnimatedDefaultTextStyle()

```dart
AnimatedDefaultTextStyle({dynamic key, required Widget child, required TextStyle style, TextAlign? textAlign, bool softWrap = true, TextOverflow overflow = TextOverflow.clip, int? maxLines, TextWidthBasis textWidthBasis = TextWidthBasis.parent, ui.TextHeightBehavior? textHeightBehavior, dynamic curve, required Duration duration, dynamic onEnd})
```

创建一个组件，对默认文本样式进行隐式动画处理。

### child

```dart
Widget child
```

此组件在组件树中的下一级子组件。

{@macro flutter.widgets.ProxyWidget.child}

### style

```dart
TextStyle style
```

目标文本样式。

当此属性发生变化时，该样式将在 [duration] 时间内进行动画过渡。

### textAlign

```dart
TextAlign? textAlign
```

文本应如何进行水平对齐。

此属性变化时会立即生效，不会进行动画处理。

### softWrap

```dart
bool softWrap
```

文本是否应在软换行处断行。

此属性变化时会立即生效，不会进行动画处理。

更多细节请参阅 [DefaultTextStyle.softWrap]。

### overflow

```dart
TextOverflow overflow
```

应如何处理视觉溢出。

此属性变化时会立即生效，不会进行动画处理。

### maxLines

```dart
int? maxLines
```

文本可跨越的最大行数（可选），如有必要则进行换行。

此属性变化时会立即生效，不会进行动画处理。

更多细节请参阅 [DefaultTextStyle.maxLines]。

### textWidthBasis

```dart
TextWidthBasis textWidthBasis
```

计算 Text 宽度时所使用的策略。

可能的取值及其含义请参阅 [TextWidthBasis](https://www.yuque.com/thyname/flutter.painting/textwidthbasis)。

### textHeightBehavior

```dart
ui.TextHeightBehavior? textHeightBehavior
```

{@macro dart.ui.textHeightBehavior}

### createState()

```dart
AnimatedWidgetBaseState<AnimatedDefaultTextStyle> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedPhysicalModel

```dart
class AnimatedPhysicalModel extends ImplicitlyAnimatedWidget {}
```

[PhysicalModel](https://www.yuque.com/thyname/flutter.widgets/physicalmodel) 的动画版本。

[borderRadius] 和 [elevation] 会被动画处理。

如果设置了 [animateColor] 属性，则 [color] 会被动画处理；否则，颜色会在其他两个属性的动画开始时立即改变。这使得颜色可以被独立地动画处理（例如，因为它是由 [AnimatedTheme](https://www.yuque.com/thyname/flutter.material/animatedtheme) 驱动的）。

[shape] 不会被动画处理。

以下展示了使用此组件、并配合 [Curves.fastOutSlowIn] 这一 [curve] 时的效果。 {@animation 250 266 https://flutter.github.io/assets-for-api-docs/assets/widgets/animated_physical_model.mp4}

### AnimatedPhysicalModel()

```dart
AnimatedPhysicalModel({dynamic key, required Widget child, BoxShape shape = BoxShape.rectangle, Clip clipBehavior = Clip.none, BorderRadius? borderRadius, double elevation = 0.0, required Color color, bool animateColor = true, required Color shadowColor, bool animateShadowColor = true, dynamic curve, required Duration duration, dynamic onEnd})
```

创建一个组件，对 [PhysicalModel](https://www.yuque.com/thyname/flutter.widgets/physicalmodel) 的属性进行动画处理。

[elevation] 必须为非负值。

是否对 [color] 进行动画处理是可选的，由 [animateColor] 标志控制。

是否对 [shadowColor] 进行动画处理是可选的，由 [animateShadowColor] 标志控制。

### child

```dart
Widget child
```

此组件在组件树中的下一级子组件。

{@macro flutter.widgets.ProxyWidget.child}

### shape

```dart
BoxShape shape
```

形状的类型。

此属性不会被动画处理。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

默认值为 [Clip.none]。

### borderRadius

```dart
BorderRadius? borderRadius
```

矩形形状圆角的目标边框半径。

如果为 null，则视为 [BorderRadius.zero]。

### elevation

```dart
double elevation
```

放置此物理对象的目标 z 坐标，相对于父组件而言。

该值始终为非负值。

### color

```dart
Color color
```

目标背景颜色。

### animateColor

```dart
bool animateColor
```

颜色是否应被动画处理。

### shadowColor

```dart
Color shadowColor
```

目标阴影颜色。

### animateShadowColor

```dart
bool animateShadowColor
```

阴影颜色是否应被动画处理。

### createState()

```dart
AnimatedWidgetBaseState<AnimatedPhysicalModel> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedFractionallySizedBox

```dart
class AnimatedFractionallySizedBox extends ImplicitlyAnimatedWidget {}
```

[FractionallySizedBox](https://www.yuque.com/thyname/flutter.widgets/fractionallysizedbox) 的动画版本，每当给定的 [widthFactor] 或 [heightFactor] 发生变化，会在给定的时长内自动过渡子组件的尺寸；每当给定的 [alignment] 发生变化，也会过渡其位置。

对于动画效果，你可以选择 [curve] 及 [duration]，该组件将自动向新的目标 [widthFactor] 或 [heightFactor] 进行动画过渡。

{@tool dartpad} 以下示例在两种状态之间对 [AnimatedFractionallySizedBox](https://www.yuque.com/thyname/flutter.widgets/animatedfractionallysizedbox) 进行过渡。点按时会使用 [Curves.fastOutSlowIn] 这一 [curve] 调整 [heightFactor]、[widthFactor] 及 [alignment] 属性。

** See code in examples/api/lib/widgets/implicit_animations/animated_fractionally_sized_box.0.dart ** {@end-tool}

另请参阅：

- [AnimatedAlign](https://www.yuque.com/thyname/flutter.widgets/animatedalign)，[Align](https://www.yuque.com/thyname/flutter.widgets/align) 的隐式动画版本。
- [AnimatedContainer](https://www.yuque.com/thyname/flutter.widgets/animatedcontainer)，可以一次性过渡更多的值。
- [AnimatedSlide](https://www.yuque.com/thyname/flutter.widgets/animatedslide)，可以按照相对于子组件自身尺寸的给定偏移量，对子组件的平移进行动画处理。
- [AnimatedPositioned](https://www.yuque.com/thyname/flutter.widgets/animatedpositioned)，作为 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的子组件时，每当给定的位置发生变化，都会自动对子组件的位置进行动画过渡。

### AnimatedFractionallySizedBox()

```dart
AnimatedFractionallySizedBox({dynamic key, AlignmentGeometry alignment = Alignment.center, Widget? child, double? heightFactor, double? widthFactor, dynamic curve, required Duration duration, dynamic onEnd})
```

创建一个组件，将其子组件的尺寸调整为可用空间的某一比例（可隐式过渡该比例），并按照可隐式过渡的对齐方式定位其子组件。

如果非 null，[widthFactor] 和 [heightFactor] 参数必须为非负值。

### child

```dart
Widget? child
```

此组件在组件树中的下一级子组件。

{@macro flutter.widgets.ProxyWidget.child}

### heightFactor

```dart
double? heightFactor
```

{@macro flutter.widgets.basic.fractionallySizedBox.heightFactor}

### widthFactor

```dart
double? widthFactor
```

{@macro flutter.widgets.basic.fractionallySizedBox.widthFactor}

### alignment

```dart
AlignmentGeometry alignment
```

{@macro flutter.widgets.basic.fractionallySizedBox.alignment}
