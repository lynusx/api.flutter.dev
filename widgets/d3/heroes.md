@docImport 'package:flutter/material.dart';

# CreateRectTween

```dart
typedef CreateRectTween = Tween<Rect?> Function(Rect? begin, Rect? end)
```

用于接收两个 [Rect](https://www.yuque.com/thyname/dart.ui/rect) 实例并返回一个在两者之间过渡的 [RectTween](https://www.yuque.com/thyname/flutter.animation/recttween) 的函数签名。

通常与 [HeroController](https://www.yuque.com/thyname/flutter.widgets/herocontroller) 搭配使用，为 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 的位置提供比线性移动更美观的动画效果。例如，参见 [MaterialRectArcTween](https://www.yuque.com/thyname/flutter.material/materialrectarctween)。

# HeroPlaceholderBuilder

```dart
typedef HeroPlaceholderBuilder = Widget Function(BuildContext context, Size heroSize, Widget child)
```

用于根据一个子 widget 和一个 [Size](https://www.yuque.com/thyname/dart.ui/size) 构建 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 占位 widget 的函数签名。

子 widget 可以选择性地作为返回的 widget 树的一部分。如果返回的 widget 没有隐式地按照 [heroSize] 进行约束，则通常应显式约束为该尺寸。

另请参阅：

- [TransitionBuilder](https://www.yuque.com/thyname/flutter.widgets/transitionbuilder)，与此类似，但只接收一个 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 和一个子 widget。

# HeroFlightShuttleBuilder

```dart
typedef HeroFlightShuttleBuilder = Widget Function(BuildContext flightContext, Animation<double> animation, HeroFlightDirection flightDirection, BuildContext fromHeroContext, BuildContext toHeroContext)
```

一个函数，使 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 能够自行提供在从一个路由飞跃到另一个路由期间显示的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)，以替代默认行为（默认行为是显示目标路由中该 Hero 的实例）。

# HeroFlightDirection

```dart
enum HeroFlightDirection {}
```

基于导航操作确定的 hero 飞跃方向。

由路由入栈（push）触发的飞跃。

动画从 0 到 1 进行。

如果未提供自定义的 [HeroFlightShuttleBuilder](https://www.yuque.com/thyname/flutter.widgets/heroflightshuttlebuilder)，飞跃过程中将显示顶层路由的 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 子 widget。

由路由出栈（pop）触发的飞跃。

动画从 1 到 0 进行。

如果未提供自定义的 [HeroFlightShuttleBuilder](https://www.yuque.com/thyname/flutter.widgets/heroflightshuttlebuilder)，飞跃过程中将显示底层路由的 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 子 widget。

# Hero

```dart
class Hero extends StatefulWidget {}
```

将其子 widget 标记为 [hero 动画](https://docs.flutter.dev/ui/animations/hero-animations) 候选对象的 widget。

当使用 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 入栈或出栈一个 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute) 时，整个屏幕的内容会被替换：旧路由消失，新路由出现。如果两个路由上存在某个共同的视觉特征，那么在路由过渡期间让该特征从一个页面物理移动到另一个页面，有助于为用户提供方向感。这种动画被称为 _hero 动画_。hero widget 会在过渡期间于 Navigator 的 overlay 中“飞跃”，在飞跃期间，默认情况下它们不会显示在旧路由和新路由中的原始位置上。

要将某个 widget 标记为此类特征，请将其包装在 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) widget 中。导航发生时，[HeroController](https://www.yuque.com/thyname/flutter.widgets/herocontroller) 会识别各路由上的 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) widget。对于每一对具有相同 [tag] 的 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) widget，都会触发一次 hero 动画。

如果某个 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 在导航发生时已经处于飞跃状态，其飞跃动画会被重定向到新的目的地。飞跃过渡期间显示的 widget，默认情况下是目标路由中该 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 的子 widget。

要使 Hero 动画得以触发，该 Hero 必须在新页面动画的第一帧就已存在。

每个路由中，同一 [tag] 对应的 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 不得超过一个。

{@youtube 560 315 https://www.youtube.com/watch?v=Be9UH1kXFDw}

{@tool dartpad} 此示例展示了在 [ListTile](https://www.yuque.com/thyname/flutter.material/listtile) 中使用的 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero)。

点击被 Hero 包装的矩形，会在推入新的 [MaterialPageRoute](https://www.yuque.com/thyname/flutter.material/materialpageroute) 时触发 hero 动画。矩形的尺寸和位置都会产生动画效果。

两个 widget 使用了相同的 [Hero.tag]。

Hero widget 使用匹配的 tag 来识别并执行此动画。

** See code in examples/api/lib/widgets/heroes/hero.0.dart ** {@end-tool}

{@tool dartpad} 此示例展示了使用默认补间动画（tween）和自定义矩形补间动画（rect tween）的 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 飞跃动画。

** See code in examples/api/lib/widgets/heroes/hero.1.dart ** {@end-tool}

## 讨论

要使这一切正常工作，hero 与 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 必须沿坐标轴对齐。每个动画中的 Hero 的左上角和右下角坐标都会被转换为全局坐标，然后再从那里转换为该 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的坐标空间；在动画期间，整个 Hero 子树会被从其原始位置中取出，并定位到该 stack 上。如果 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 未沿坐标轴对齐，这个过程会以相当难看的方式失败。请不要旋转你的 hero！

为使动画效果良好，两个位置中 hero 的 widget 树必须基本相同。默认情况下，_目标_（target）的 widget 会被用于执行过渡：当从路由 A 前往路由 B 时，路由 B 中 hero 的 widget 会被放置在路由 A 中 hero 的 widget 之上。此外，如果 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 子树的外观依赖于某个 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)（例如 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 或 [Theme](https://www.yuque.com/thyname/flutter.material/theme)），那么由于路由 A 和路由 B 提供的此类 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 不同，hero 动画在开始或结束时可能会出现不连续的情况。可以考虑提供自定义的 [flightShuttleBuilder] 以确保过渡平滑。默认的 [flightShuttleBuilder] 会对 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的内边距进行插值。如果你的 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) widget 使用了自定义的 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 并且动画中出现了不连续现象，请尝试通过 [flightShuttleBuilder] 提供自定义的飞跃过渡。

默认情况下，在过渡 widget 于两个路由上方进行飞跃动画的过程中，路由 A 和路由 B 中的 hero 都会被隐藏。可以使用 [placeholderBuilder] 在飞跃开始后，于它们原本的位置显示自定义 widget。

在过渡期间，过渡 widget 会动画移动到路由 B 中 hero 的位置，然后该 widget 会被插入到路由 B 中。当从 B 返回 A 时，默认情况下路由 A 的 hero widget 会被放置在路由 B 的 hero widget 原来所在的位置，然后动画朝相反方向进行。

### 嵌套 Navigator

如果任一路由或两者都包含嵌套的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，则只有包含在这些嵌套 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的顶层路由（由 [Route.isCurrent] 定义）中的 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 才会被纳入动画考虑范围。与非嵌套情形一样，嵌套 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 中包含这些 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 的顶层路由必须是 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute)。

## Hero 过渡的组成部分

![Diagrams with parts of the Hero transition.](https://flutter.github.io/assets-for-api-docs/assets/interaction/heroes.png)

### Hero()

```dart
Hero({dynamic key, required Object tag, CreateRectTween? createRectTween, HeroFlightShuttleBuilder? flightShuttleBuilder, HeroPlaceholderBuilder? placeholderBuilder, bool transitionOnUserGestures = false, Curve curve = Curves.fastOutSlowIn, Curve? reverseCurve, required Widget child})
```

创建一个 hero。

[child] 参数及其所有后代都不得是 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero)。

### tag

```dart
Object tag
```

此特定 hero 的标识符。如果此 hero 的 tag 与我们正要前往或离开的 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute) 上某个 hero 的 tag 相匹配，则会触发 hero 动画。

### createRectTween

```dart
CreateRectTween? createRectTween
```

定义目标 hero 的边界在从起始路由飞往目标路由过程中如何变化。

hero 飞跃开始时，目标 hero 的 [child] 会与起始 hero 的子 widget 对齐。此回调返回的 [Tween<Rect>] 用于在飞跃动画的值从 0.0 变化到 1.0 时计算 hero 的边界。

如果此属性为 null（默认值），则会使用 [HeroController.createRectTween] 的值。由 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 创建的 [HeroController](https://www.yuque.com/thyname/flutter.widgets/herocontroller) 会创建一个 [MaterialRectArcTween](https://www.yuque.com/thyname/flutter.material/materialrectarctween)。

### child

```dart
Widget child
```

在 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 入栈或出栈过渡期间，从一个路由“飞往”另一个路由的 widget 子树。

此子树的外观应与应用中所有具有相同 [tag] 的其他 hero 子树的外观相似。缩放和宽高比的变化在 hero 动画中效果良好，而布局或组合方式的变化则效果不佳。

{@macro flutter.widgets.ProxyWidget.child}

### flightShuttleBuilder

```dart
HeroFlightShuttleBuilder? flightShuttleBuilder
```

可选的重写，用于提供在 hero 飞跃期间显示的 widget。

此飞跃中的 widget 可以依赖于路由过渡的动画，以及即将进入和离开的路由中 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 后代的 widget 与布局。

当源 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 和目标 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 都提供了 [flightShuttleBuilder] 时，目标的 [flightShuttleBuilder] 优先。

如果都未提供，默认会在飞跃期间显示目标路由的 Hero 子 widget。

## 限制

如果 [flightShuttleBuilder] 构建的 widget 参与了 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的入栈过渡，则该 widget 及其后代不得包含任何在源 Hero 的后代 widget 中已使用的 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey)。这是因为在 Hero 飞跃动画期间，这两个子树都会包含在 widget 树中，而 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 在整个 widget 树中必须是唯一的。

如果上述 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 对你的应用至关重要，可以考虑为源 Hero 提供一个自定义的 [placeholderBuilder]，以避免 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 冲突，例如构建一个空的 [SizedBox](https://www.yuque.com/thyname/flutter.widgets/sizedbox)，以保持 Hero [child] 的原始尺寸。

### placeholderBuilder

```dart
HeroPlaceholderBuilder? placeholderBuilder
```

在 Hero 飞跃开始后，留在 Hero 的 [child] 原位置的占位 widget。

默认情况下，占位 widget 是一个保持 Hero 子 widget 原始尺寸的空 [SizedBox](https://www.yuque.com/thyname/flutter.widgets/sizedbox)；但如果此 Hero 是 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 入栈过渡中的源 Hero，则 [child] 会成为该占位 widget 的后代，并在 Hero 飞跃期间保持 [Offstage](https://www.yuque.com/thyname/flutter.widgets/offstage) 状态。

### transitionOnUserGestures

```dart
bool transitionOnUserGestures
```

当 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute) 过渡是由用户手势触发时（例如 iOS 上的返回滑动手势），是否执行 hero 过渡。

如果从路由和到路由上具有相同 [tag] 的 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 的 [transitionOnUserGestures] 均设置为 true，返回滑动手势将触发与程序化触发的入栈或出栈相同的 hero 动画。

被弹出到的路由或底层路由还必须将 [PageRoute.maintainState] 设置为 true，手势触发的 hero 过渡才能生效。

默认为 false。

### curve

```dart
Curve curve
```

正向使用的曲线。

默认为 [Curves.fastOutSlowIn]。

### reverseCurve

```dart
Curve? reverseCurve
```

反向使用的曲线。

如果此属性为 null，则使用 [Hero.curve].flipped。

### createState()

```dart
State<Hero> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# HeroController

```dart
class HeroController extends NavigatorObserver {}
```

管理 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 过渡的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 观察者。

应在 [Navigator.observers] 中使用 [HeroController](https://www.yuque.com/thyname/flutter.widgets/herocontroller) 的实例。[MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 会自动完成此操作。

### HeroController()

```dart
HeroController({CreateRectTween? createRectTween})
```

使用给定的 [RectTween](https://www.yuque.com/thyname/flutter.animation/recttween) 构造函数（如果有）创建一个 hero 控制器。

[createRectTween] 参数是可选的。如果为 null，控制器将使用线性的 [Tween<Rect>]。

### createRectTween

```dart
CreateRectTween? createRectTween
```

用于创建对飞跃中 hero 的位置进行插值的 [RectTween](https://www.yuque.com/thyname/flutter.animation/recttween)。

如果为 null，控制器将使用线性的 [RectTween](https://www.yuque.com/thyname/flutter.animation/recttween)。

### didChangeTop()

```dart
void didChangeTop(Route<dynamic> topRoute, Route<dynamic>? previousTopRoute)
```

### didStartUserGesture()

```dart
void didStartUserGesture(Route<dynamic> route, Route<dynamic>? previousRoute)
```

### didStopUserGesture()

```dart
void didStopUserGesture()
```

### dispose()

```dart
void dispose()
```

释放资源。

# HeroMode

```dart
class HeroMode extends StatelessWidget {}
```

启用或禁用 widget 子树中的 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero)。

{@youtube 560 315 https://www.youtube.com/watch?v=AaIASk2u1C0}

当 [enabled] 为 false 时，此子树中的所有 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) widget 都不会参与 hero 动画。

当 [enabled] 为 true（默认值）时，[Hero](https://www.yuque.com/thyname/flutter.widgets/hero) widget 可以照常参与 hero 动画。

### HeroMode()

```dart
HeroMode({dynamic key, required Widget child, bool enabled = true})
```

创建一个用于启用或禁用 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 的 widget。

### child

```dart
Widget child
```

放置在此 [HeroMode](https://www.yuque.com/thyname/flutter.widgets/heromode) 内的子树。

### enabled

```dart
bool enabled
```

此子树中是否启用 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero)。

如果此属性为 false，此子树中的 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 在路由切换时将不会产生动画。否则，它们将照常产生动画。

默认为 true。
