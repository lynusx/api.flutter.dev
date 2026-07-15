# TweenSequence

```dart
class TweenSequence<T> extends Animatable<T> {}
```

允许创建一个值由一系列 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 定义的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)。

每个 [TweenSequenceItem](https://www.yuque.com/thyname/flutter.animation/tweensequenceitem) 都有一个权重（weight），用于定义其占动画总时长的百分比。每个 tween 定义了在其权重所指示的区间内动画的值。

{@tool snippet} 此示例定义了一个动画：在动画的前 40% 时间内使用缓动曲线在 5.0 和 10.0 之间进行插值，在接下来的 20% 时间内保持为 10.0，然后在最后 40% 的时间内返回到 5.0。

```dart
final Animation<double> animation = TweenSequence<double>(
  <TweenSequenceItem<double>>[
    TweenSequenceItem<double>(
      tween: Tween<double>(begin: 5.0, end: 10.0)
        .chain(CurveTween(curve: Curves.ease)),
      weight: 40.0,
    ),
    TweenSequenceItem<double>(
      tween: ConstantTween<double>(10.0),
      weight: 20.0,
    ),
    TweenSequenceItem<double>(
      tween: Tween<double>(begin: 10.0, end: 5.0)
        .chain(CurveTween(curve: Curves.ease)),
      weight: 40.0,
    ),
  ],
).animate(myAnimationController);
```

{@end-tool}

### TweenSequence()

```dart
TweenSequence(List<TweenSequenceItem<T>> items)
```

构造一个 TweenSequence。

[items] 参数必须是一个或多个 [TweenSequenceItem](https://www.yuque.com/thyname/flutter.animation/tweensequenceitem) 组成的列表。

构建 [TweenSequence](https://www.yuque.com/thyname/flutter.animation/tweensequence) 会有一定的开销，因此在可能的情况下，最好复用同一个实例，而不是在每一帧都重新构建它。

### transform()

```dart
T transform(double t)
```

### toString()

```dart
String toString()
```

# FlippedTweenSequence

```dart
class FlippedTweenSequence extends TweenSequence<double> {}
```

允许创建一个值由一系列 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 定义的翻转（flipped）[Animation](https://www.yuque.com/thyname/flutter.animation/animation)。

这会创建一个 [TweenSequence](https://www.yuque.com/thyname/flutter.animation/tweensequence)，其求值结果在水平和垂直方向上都被翻转。

此 tween sequence 假定求值结果必须是介于 0.0 和 1.0 之间的 double 值。

### FlippedTweenSequence()

```dart
FlippedTweenSequence(List<TweenSequenceItem<double>> items)
```

创建一个翻转的 [TweenSequence](https://www.yuque.com/thyname/flutter.animation/tweensequence)。

[items] 参数必须是一个或多个 [TweenSequenceItem](https://www.yuque.com/thyname/flutter.animation/tweensequenceitem) 组成的列表。

构建 `TweenSequence` 会有一定的开销，因此在可能的情况下，最好复用同一个实例，而不是在每一帧都重新构建它。

### transform()

```dart
double transform(double t)
```

# TweenSequenceItem

```dart
class TweenSequenceItem<T> {}
```

[TweenSequence](https://www.yuque.com/thyname/flutter.animation/tweensequence) 中单个元素的简单持有者。

### TweenSequenceItem()

```dart
TweenSequenceItem({required Animatable<T> tween, required double weight})
```

构造一个 TweenSequenceItem。

[weight] 必须大于 0.0。

### tween

```dart
Animatable<T> tween
```

定义 [TweenSequence](https://www.yuque.com/thyname/flutter.animation/tweensequence) 在动画时长内、由 [weight] 及此项在项目列表中的位置所指示的区间内的值。

{@tool snippet}

此项的值可以通过链接到 [CurveTween](https://www.yuque.com/thyname/flutter.animation/curvetween) 来进行"曲线化"。例如，要创建一个从 0.0 缓动到 10.0 的 tween：

```dart
Tween<double>(begin: 0.0, end: 10.0)
  .chain(CurveTween(curve: Curves.ease))
```

{@end-tool}

### weight

```dart
double weight
```

一个任意值，用于指示 [TweenSequence](https://www.yuque.com/thyname/flutter.animation/tweensequence) 动画时长中，[tween] 将被使用的相对百分比。

单个项目的百分比等于该项目的权重除以所有项目权重的总和。
