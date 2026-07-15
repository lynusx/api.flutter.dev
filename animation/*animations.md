@docImport 'package:flutter/widgets.dart';

# kAlwaysCompleteAnimation

```dart
Animation<double> kAlwaysCompleteAnimation
```

一个始终处于完成状态的动画。

使用此常量比构建一个初始值为 1.0 的 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 的开销更小。当某个 API 需要一个动画，但你实际上并不想执行任何动画时，这会很有用。

# kAlwaysDismissedAnimation

```dart
Animation<double> kAlwaysDismissedAnimation
```

一个始终处于关闭（dismissed）状态的动画。

使用此常量比构建一个初始值为 0.0 的 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 的开销更小。当某个 API 需要一个动画，但你实际上并不想执行任何动画时，这会很有用。

# AlwaysStoppedAnimation

```dart
class AlwaysStoppedAnimation<T> extends Animation<T> {}
```

一个始终停止在给定值上的动画。

其 [status] 始终为 [AnimationStatus.forward]。

### AlwaysStoppedAnimation()

```dart
AlwaysStoppedAnimation(T value)
```

使用给定的值创建一个 [AlwaysStoppedAnimation](https://www.yuque.com/thyname/flutter.animation/alwaysstoppedanimation)。

由于 [AlwaysStoppedAnimation](https://www.yuque.com/thyname/flutter.animation/alwaysstoppedanimation) 的 [value] 和 [status] 永远不会改变，因此其监听器永远不会被调用。所以可以安全地在多个位置复用同一个 [AlwaysStoppedAnimation](https://www.yuque.com/thyname/flutter.animation/alwaysstoppedanimation) 实例。如果要使用的 [value] 在编译期已知，则应将该构造函数调用为 `const` 构造函数。

### value

```dart
T value
```

### addListener()

```dart
void addListener(VoidCallback listener)
```

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

### addStatusListener()

```dart
void addStatusListener(AnimationStatusListener listener)
```

### removeStatusListener()

```dart
void removeStatusListener(AnimationStatusListener listener)
```

### status

```dart
AnimationStatus get status
```

### toStringDetails()

```dart
String toStringDetails()
```

# AnimationWithParentMixin

```dart
mixin AnimationWithParentMixin<T> {}
```

通过将行为委托给给定的父动画（[parent] Animation）来实现 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 接口的大部分内容。

要实现一个由父动画驱动的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)，只需混入（mix in）此类，实现 [parent]，并实现 `T get value` 即可。

如果要定义一个从 0..1 范围内数值到其他值的映射，请考虑改为子类化 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。

### parent

```dart
Animation<T> get parent
```

此动画将要代理其数值的动画。

该动画在此对象的生命周期内必须保持不变。如果希望在不同时间代理不同的动画，请考虑使用 [ProxyAnimation](https://www.yuque.com/thyname/flutter.animation/proxyanimation)。

### addListener()

```dart
void addListener(VoidCallback listener)
```

每当动画的值发生变化时调用该监听器。

可以使用 [removeListener] 移除监听器。

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

停止在动画值发生变化时调用该监听器。

可以使用 [addListener] 添加监听器。

### addStatusListener()

```dart
void addStatusListener(AnimationStatusListener listener)
```

每当动画的状态发生变化时调用该监听器。

可以使用 [removeStatusListener] 移除监听器。

### removeStatusListener()

```dart
void removeStatusListener(AnimationStatusListener listener)
```

停止在动画状态发生变化时调用该监听器。

可以使用 [addStatusListener] 添加监听器。

### status

```dart
AnimationStatus get status
```

此动画的当前状态。

# ProxyAnimation

```dart
class ProxyAnimation extends Animation<double> with AnimationLazyListenerMixin, AnimationLocalListenersMixin, AnimationLocalStatusListenersMixin {}
```

代理另一个动画的动画。

代理动画非常有用，因为父动画可以被修改。例如，一个对象可以创建一个代理动画，将该代理交给另一个对象，然后之后再更改该代理所获取值的来源动画。

### ProxyAnimation()

```dart
ProxyAnimation([Animation<double>? animation])
```

创建一个代理动画。

如果省略 animation 参数，则该代理动画的状态将为 [AnimationStatus.dismissed]，值为 0.0。

### parent

```dart
Animation<double>? get parent
```

此动画将要代理其数值的动画。

该值是可变的。当其被修改时，代理动画上的监听器将被透明地更新为监听新的父动画。

### parent

```dart
set parent(Animation<double>? value)
```

### didStartListening()

```dart
void didStartListening()
```

### didStopListening()

```dart
void didStopListening()
```

### status

```dart
AnimationStatus get status
```

### value

```dart
double get value
```

### toString()

```dart
String toString()
```

# ReverseAnimation

```dart
class ReverseAnimation extends Animation<double> with AnimationLazyListenerMixin, AnimationLocalStatusListenersMixin {}
```

另一个动画的反向动画。

如果父动画正在从 0.0 到 1.0 正向运行，则此动画将从 1.0 到 0.0 反向运行。

使用 [ReverseAnimation](https://www.yuque.com/thyname/flutter.animation/reverseanimation) 与使用 begin 为 1.0、end 为 0.0 的 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 不同，因为该 tween 不会改变动画的状态或方向。

另请参阅：

- [Curve.flipped] 和 [FlippedCurve](https://www.yuque.com/thyname/flutter.animation/flippedcurve)，它们为 [Curve](https://www.yuque.com/thyname/flutter.animation/curve) 提供了类似的效果。
- [CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation)，它可以在动画正向和反向运行时分别使用不同的曲线。

### ReverseAnimation()

```dart
ReverseAnimation(Animation<double> parent)
```

创建一个反向动画。

### parent

```dart
Animation<double> parent
```

此动画所反转其值和方向的动画。

### addListener()

```dart
void addListener(VoidCallback listener)
```

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

### didStartListening()

```dart
void didStartListening()
```

### didStopListening()

```dart
void didStopListening()
```

### status

```dart
AnimationStatus get status
```

### value

```dart
double get value
```

### toString()

```dart
String toString()
```

# CurvedAnimation

```dart
class CurvedAnimation extends Animation<double> with AnimationWithParentMixin<double> {}
```

将曲线应用于另一个动画的动画。

当你想对一个动画对象应用非线性 [Curve](https://www.yuque.com/thyname/flutter.animation/curve) 时，[CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation) 非常有用，尤其是当你想在动画正向和反向运行时使用不同的曲线时。

根据给定曲线的不同，[CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation) 的输出范围可能比其输入范围更宽。例如，像 [Curves.elasticIn] 这样的弹性曲线会显著超出或未达到默认的 0.0 到 1.0 范围。

如果你想对 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 应用 [Curve](https://www.yuque.com/thyname/flutter.animation/curve)，请考虑使用 [CurveTween](https://www.yuque.com/thyname/flutter.animation/curvetween)。

[CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation) 在不再需要时应当被 dispose，以清理它可能添加的所有监听器。dispose 父动画（通常是 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)）也会同时清理此对象。不要在 `build` 方法中创建 [CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation)，因为这会导致每次重建时都泄漏已添加的监听器。如果不需要 [reverseCurve]，建议使用 `parent.drive(CurveTween(curve: curve))`，它不需要单独的 dispose。

{@tool snippet}

以下代码示例展示了如何将曲线应用于由 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) `controller` 生成的线性动画。

```dart
final Animation<double> animation = CurvedAnimation(
  parent: controller,
  curve: Curves.ease,
);
```

{@end-tool} {@tool snippet}

第二个代码示例展示了如何在正向方向上应用与反向方向不同的曲线。这无法通过 [CurveTween](https://www.yuque.com/thyname/flutter.animation/curvetween) 实现（因为 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 在应用时并不知道动画的方向）。

```dart
final Animation<double> animation = CurvedAnimation(
  parent: controller,
  curve: Curves.easeIn,
  reverseCurve: Curves.easeOut,
);
```

{@end-tool}

默认情况下，[reverseCurve] 与正向的 [curve] 相同。

另请参阅：

- [CurveTween](https://www.yuque.com/thyname/flutter.animation/curvetween)，它是表达上面第一个示例的另一种方式。
- [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)，其中包含创建和 dispose [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 的示例。
- [Curve.flipped] 和 [FlippedCurve](https://www.yuque.com/thyname/flutter.animation/flippedcurve)，它们提供了 [Curve](https://www.yuque.com/thyname/flutter.animation/curve) 的反向效果。

### CurvedAnimation()

```dart
CurvedAnimation({required Animation<double> parent, required Curve curve, Curve? reverseCurve})
```

创建一个曲线动画。

### parent

```dart
Animation<double> parent
```

此动画所应用曲线的目标动画。

### curve

```dart
Curve curve
```

正向运行时使用的曲线。

### reverseCurve

```dart
Curve? reverseCurve
```

反向运行时使用的曲线。

如果父动画在未先到达 [AnimationStatus.completed] 或 [AnimationStatus.dismissed] 状态的情况下改变了方向，[CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation) 将保持在同一条曲线上（尽管方向相反），以避免视觉上的不连续。

由于 [CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation) 可能会向其父动画添加监听器，因此必须只创建一次（例如在 [State.initState] 中），并在 [State.dispose] 中 dispose。不要在每次 build 时重新创建它，因为这会导致每次重建时都泄漏已添加的监听器。如果不需要 [reverseCurve]，建议使用 `parent.drive(CurveTween(curve: curve))`，它不需要单独的 dispose。

如果此字段为 null，则在两个方向上都使用 [curve]。

### isDisposed

```dart
bool isDisposed
```

如果此 CurvedAnimation 已被 dispose，则为 true。

### dispose()

```dart
void dispose()
```

清理此 CurvedAnimation 添加的所有监听器。

### value

```dart
double get value
```

### toString()

```dart
String toString()
```

# TrainHoppingAnimation

```dart
class TrainHoppingAnimation extends Animation<double> with AnimationEagerListenerMixin, AnimationLocalListenersMixin, AnimationLocalStatusListenersMixin {}
```

此动画首先代理第一个动画，但当该动画的值与第二个动画的值交叉时（无论是因为第二个动画朝相反方向运行，还是因为其中一个超过了另一个），该动画会跳转（hop）到代理第二个动画。

当 [TrainHoppingAnimation](https://www.yuque.com/thyname/flutter.animation/trainhoppinganimation) 从代理第一个动画切换到代理第二个动画时，会调用 [onSwitchedTrain] 回调。

如果两个动画的起始值相同，则 [TrainHoppingAnimation](https://www.yuque.com/thyname/flutter.animation/trainhoppinganimation) 会立即跳转到第二个动画，并且不会调用 [onSwitchedTrain] 回调。如果只提供了一个动画（即第二个动画为 null），则 [TrainHoppingAnimation](https://www.yuque.com/thyname/flutter.animation/trainhoppinganimation) 只会代理第一个动画，永远不会跳转。

由于此对象必须持续跟踪这两个动画，即使它自身没有任何监听器时也是如此，因此它不会在所有监听器被移除时自动关闭，而是暴露了一个 [dispose()] 方法。调用此方法可以关闭此对象。

### TrainHoppingAnimation()

```dart
TrainHoppingAnimation(Animation<double>? _currentTrain, Animation<double>? _nextTrain, {VoidCallback? onSwitchedTrain})
```

创建一个 train-hopping 动画。

current train 参数不能为 null，但 next train 参数可以为 null。如果 next train 为 null，则此对象将只代理第一个动画，永远不会跳转。

### currentTrain

```dart
Animation<double>? get currentTrain
```

当前正在驱动此动画的动画。

当调用 [onSwitchedTrain] 时，此对象的身份将从第一个动画变为第二个动画。

### onSwitchedTrain

```dart
VoidCallback? onSwitchedTrain
```

当此动画切换为由第二个动画驱动时调用。

如果构造函数传入的两个动画在构造时具有相同的值，则不会调用此回调。在这种情况下，将从一开始就使用第二个动画，而忽略第一个动画。

### status

```dart
AnimationStatus get status
```

### value

```dart
double get value
```

### dispose()

```dart
void dispose()
```

释放此 performance 使用的所有资源。调用此方法后，此对象将不再可用。

### toString()

```dart
String toString()
```

# CompoundAnimation

```dart
abstract class CompoundAnimation<T> extends Animation<T> with AnimationLazyListenerMixin, AnimationLocalListenersMixin, AnimationLocalStatusListenersMixin {}
```

用于组合多个 Animation 的接口。子类只需实现 `value` 获取器，即可控制子动画的组合方式。可以进行链式调用以组合两个以上的动画。

例如，要创建一个值为另外两个动画之和的动画，可以子类化此类并定义 `T get value = first.value + second.value;`。

默认情况下，如果 [next] 正在运行，则 [CompoundAnimation](https://www.yuque.com/thyname/flutter.animation/compoundanimation) 的 [status] 为 [next] 动画的状态；否则为 [first] 动画的状态。

### CompoundAnimation()

```dart
CompoundAnimation({required Animation<T> first, required Animation<T> next})
```

创建一个 [CompoundAnimation](https://www.yuque.com/thyname/flutter.animation/compoundanimation)。

两个参数都可以是 [CompoundAnimation](https://www.yuque.com/thyname/flutter.animation/compoundanimation) 本身，以便组合多个动画。

### first

```dart
Animation<T> first
```

第一个子动画。如果两者都未在运行动画，则以其状态为准。

### next

```dart
Animation<T> next
```

第二个子动画。

### didStartListening()

```dart
void didStartListening()
```

### didStopListening()

```dart
void didStopListening()
```

### status

```dart
AnimationStatus get status
```

根据 [first] 和 [next] 的状态获取此动画的状态。

默认情况下，如果 [next] 动画正在运行，则使用其状态；否则默认使用 [first] 的状态。

### toString()

```dart
String toString()
```

# AnimationMean

```dart
class AnimationMean extends CompoundAnimation<double> {}
```

一个跟踪另外两个动画均值的 [double](https://www.yuque.com/thyname/dart.core/double) 动画。

此动画的 [status] 为 `right` 动画的状态（如果它正在运行），否则为 `left` 动画的状态。

此动画的 [value] 是表示 `left` 和 `right` 动画值的均值的 [double](https://www.yuque.com/thyname/dart.core/double)。

### AnimationMean()

```dart
AnimationMean({required Animation<double> left, required Animation<double> right})
```

创建一个跟踪另外两个动画均值的动画。

### value

```dart
double get value
```

# AnimationMax

```dart
class AnimationMax<T extends num> extends CompoundAnimation<T> {}
```

一个跟踪另外两个动画最大值的动画。

此动画的 [value] 是 [first] 和 [next] 值中的最大值。

### AnimationMax()

```dart
AnimationMax(Animation<T> first, Animation<T> next)
```

创建一个 [AnimationMax](https://www.yuque.com/thyname/flutter.animation/animationmax)。

两个参数都可以是 [AnimationMax](https://www.yuque.com/thyname/flutter.animation/animationmax) 本身，以便组合多个动画。

### value

```dart
T get value
```

# AnimationMin

```dart
class AnimationMin<T extends num> extends CompoundAnimation<T> {}
```

一个跟踪另外两个动画最小值的动画。

此动画的 [value] 是 [first] 和 [next] 值中的最小值。

### AnimationMin()

```dart
AnimationMin(Animation<T> first, Animation<T> next)
```

创建一个 [AnimationMin](https://www.yuque.com/thyname/flutter.animation/animationmin)。

两个参数都可以是 [AnimationMin](https://www.yuque.com/thyname/flutter.animation/animationmin) 本身，以便组合多个动画。

### value

```dart
T get value
```
