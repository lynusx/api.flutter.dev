@docImport 'package:flutter/material.dart';

@docImport 'animated_switcher.dart'; @docImport 'implicit_animations.dart';

# CrossFadeState

```dart
enum CrossFadeState {}
```

指定要显示两个子组件中的哪一个。参见 [AnimatedCrossFade](https://www.yuque.com/thyname/flutter.widgets/animatedcrossfade)。

被显示的子组件将淡入，而另一个则会淡出。

显示第一个子组件（[AnimatedCrossFade.firstChild]）并隐藏第二个子组件（[AnimatedCrossFade.secondChild]）。

显示第二个子组件（[AnimatedCrossFade.secondChild]）并隐藏第一个子组件（[AnimatedCrossFade.firstChild]）。

# AnimatedCrossFadeBuilder

```dart
typedef AnimatedCrossFadeBuilder = Widget Function(Widget topChild, Key topChildKey, Widget bottomChild, Key bottomChildKey)
```

[AnimatedCrossFade.layoutBuilder] 回调的签名。

`topChild` 是正在淡入的子组件，通常绘制在顶层。`bottomChild` 是正在淡出的子组件，通常绘制在底层。

为了获得良好的性能，返回的组件树应同时包含 `topChild` 和 `bottomChild`；从返回的组件到每个子组件之间，组件树的深度以及组件树中各组件的类型都应保持一致；如果存在具有多个子组件的组件，则应分别使用提供的 `topChildKey` 和 `bottomChildKey` 键对顶部子组件和底部子组件进行标记。

{@tool snippet}

```dart
Widget defaultLayoutBuilder(Widget topChild, Key topChildKey, Widget bottomChild, Key bottomChildKey) {
  return Stack(
    children: <Widget>[
      Positioned(
        key: bottomChildKey,
        left: 0.0,
        top: 0.0,
        right: 0.0,
        child: bottomChild,
      ),
      Positioned(
        key: topChildKey,
        child: topChild,
      )
    ],
  );
}
```

{@end-tool}

# AnimatedCrossFade

```dart
class AnimatedCrossFade extends StatefulWidget {}
```

一个在两个给定子组件之间进行交叉淡化（cross-fade），并在二者大小之间进行动画过渡的组件。

{@youtube 560 315 https://www.youtube.com/watch?v=PGK2UUAyE54}

该动画通过 [crossFadeState] 参数进行控制。[firstCurve] 和 [secondCurve] 表示两个子组件的透明度曲线。[firstCurve] 是反转的，也就是说，当提供一条递增曲线（如 [Curves.linear]）时，它会呈现淡出效果。[sizeCurve] 是用于在淡出子组件的大小和淡入子组件的大小之间进行动画过渡的曲线。

此组件用于在一对宽度相同的组件之间进行淡化过渡。如果两个子组件的高度不同，动画会在过渡期间通过对齐它们的顶部边缘来裁剪溢出的子组件，这意味着底部会被裁剪掉。

当现有的 [AnimatedCrossFade](https://www.yuque.com/thyname/flutter.widgets/animatedcrossfade) 以不同的 [crossFadeState] 属性值重建时，会自动触发该动画。

{@tool snippet}

此代码在 Flutter 徽标的两种表现形式之间进行淡化过渡。它依赖于一个布尔字段 `_first`：当 `_first` 为 true 时，显示第一个徽标，否则显示第二个徽标。当该字段的状态发生变化时，[AnimatedCrossFade](https://www.yuque.com/thyname/flutter.widgets/animatedcrossfade) 组件会在三秒内于两种徽标形式之间进行交叉淡化。

```dart
AnimatedCrossFade(
  duration: const Duration(seconds: 3),
  firstChild: const FlutterLogo(style: FlutterLogoStyle.horizontal, size: 100.0),
  secondChild: const FlutterLogo(style: FlutterLogoStyle.stacked, size: 100.0),
  crossFadeState: _first ? CrossFadeState.showFirst : CrossFadeState.showSecond,
)
```

{@end-tool}

另请参阅：

- [AnimatedOpacity](https://www.yuque.com/thyname/flutter.widgets/animatedopacity)，在无内容和单个子组件之间进行淡化过渡。
- [AnimatedSwitcher](https://www.yuque.com/thyname/flutter.widgets/animatedswitcher)，以可自定义的过渡效果将子组件替换为新的子组件，支持同时进行多个交叉淡化。
- [AnimatedSize](https://www.yuque.com/thyname/flutter.widgets/animatedsize)，[AnimatedCrossFade](https://www.yuque.com/thyname/flutter.widgets/animatedcrossfade) 用于自动改变大小的底层组件。

### AnimatedCrossFade()

```dart
AnimatedCrossFade({dynamic key, required Widget firstChild, required Widget secondChild, Curve firstCurve = Curves.linear, Curve secondCurve = Curves.linear, Curve sizeCurve = Curves.linear, AlignmentGeometry alignment = Alignment.topCenter, required CrossFadeState crossFadeState, required Duration duration, Duration? reverseDuration, AnimatedCrossFadeBuilder layoutBuilder = defaultLayoutBuilder, bool excludeBottomFocus = true, Clip clipBehavior = Clip.hardEdge, VoidCallback? onEnd})
```

创建一个交叉淡化动画组件。

该动画的 [duration] 对所有组成部分（淡入、淡出和大小变化）都是相同的，你可以传入 [Interval](https://www.yuque.com/thyname/flutter.animation/interval) 而非 [Curve](https://www.yuque.com/thyname/flutter.animation/curve) 以获得更精细的控制，例如让淡入淡出之间产生重叠。

### firstChild

```dart
Widget firstChild
```

当 [crossFadeState] 为 [CrossFadeState.showFirst] 时可见的子组件。当 [crossFadeState] 从 [CrossFadeState.showFirst] 过渡到 [CrossFadeState.showSecond] 时，它会淡出；反之亦然。

### secondChild

```dart
Widget secondChild
```

当 [crossFadeState] 为 [CrossFadeState.showSecond] 时可见的子组件。当 [crossFadeState] 从 [CrossFadeState.showFirst] 过渡到 [CrossFadeState.showSecond] 时，它会淡入；反之亦然。

### crossFadeState

```dart
CrossFadeState crossFadeState
```

动画完成后将显示的子组件。

### duration

```dart
Duration duration
```

整个编排动画的时长。

### reverseDuration

```dart
Duration? reverseDuration
```

反向运行时整个编排动画的时长。

如果未提供，则默认为 [duration]。

### firstCurve

```dart
Curve firstCurve
```

第一个子组件的淡化曲线。

默认为 [Curves.linear]。

### secondCurve

```dart
Curve secondCurve
```

第二个子组件的淡化曲线。

默认为 [Curves.linear]。

### sizeCurve

```dart
Curve sizeCurve
```

在两个子组件大小之间进行动画过渡所使用的曲线。

默认为 [Curves.linear]。

### alignment

```dart
AlignmentGeometry alignment
```

在大小变化的动画过程中，子组件应如何对齐。

默认为 [Alignment.topCenter]。

另请参阅：

- [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，一个包含常用常量的类，通常用于指定 [AlignmentGeometry](https://www.yuque.com/thyname/flutter.painting/alignmentgeometry)。
- [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)，与 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 类似，用于指定相对于文本方向的对齐方式。

### layoutBuilder

```dart
AnimatedCrossFadeBuilder layoutBuilder
```

一个用于定位 [firstChild] 和 [secondChild] 组件的 builder。

此方法返回的组件被包裹在一个 [AnimatedSize](https://www.yuque.com/thyname/flutter.widgets/animatedsize) 中。

默认情况下，此参数使用 [AnimatedCrossFade.defaultLayoutBuilder]，它使用一个 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack)，将 `bottomChild` 对齐到该 stack 的顶部，同时将 `topChild` 作为未定位的子组件以填充所提供的约束。当 [AnimatedCrossFade](https://www.yuque.com/thyname/flutter.widgets/animatedcrossfade) 可以改变大小，且子组件不具有弹性时，这种方式表现良好。但是，如果子组件对其大小不太敏感（例如 [Center](https://www.yuque.com/thyname/flutter.widgets/center) 内的 [CircularProgressIndicator](https://www.yuque.com/thyname/flutter.material/circularprogressindicator)），或者 [AnimatedCrossFade](https://www.yuque.com/thyname/flutter.widgets/animatedcrossfade) 被强制设置为特定大小，则在交叉淡化状态改变时，可能会导致组件发生跳动。

### excludeBottomFocus

```dart
bool excludeBottomFocus
```

当此值为 true 时，其效果等同于在底部组件位于交叉淡化 stack 底层期间，用一个 [ExcludeFocus](https://www.yuque.com/thyname/flutter.widgets/excludefocus) 组件将其包裹。

默认为 true。当其为 false 时，交叉淡化 stack 中的底部组件可以保持焦点，直到顶部组件请求获得焦点。这对于在不同的 [TextField](https://www.yuque.com/thyname/flutter.material/textfield) 之间进行动画过渡非常有用，可使键盘在交叉淡化动画期间保持打开状态。

### clipBehavior

```dart
Clip clipBehavior
```

控制在交叉淡化过渡期间是否裁剪内容。

在 [firstChild] 和 [secondChild] 之间进行大小过渡的期间，默认会裁剪内容，以防止其溢出正在执行动画的组件的边界框。

将此值设置为 [Clip.none] 可完全禁用裁剪。这对于带有阴影或视觉效果延伸到其边界之外的组件非常有用。

默认为 [Clip.hardEdge]。

### onEnd

```dart
VoidCallback? onEnd
```

每次动画完成时调用。

这在当前动画结束时触发其他操作（例如另一个动画）时非常有用。

### defaultLayoutBuilder()

```dart
Widget defaultLayoutBuilder(Widget topChild, Key topChildKey, Widget bottomChild, Key bottomChildKey)
```

[AnimatedCrossFade](https://www.yuque.com/thyname/flutter.widgets/animatedcrossfade) 使用的默认布局算法。

顶部子组件被放置在一个 stack 中，该 stack 的大小会与顶部子组件相匹配。底部子组件被定位在同一 stack 的顶层，其大小会适配自身宽度但不会强制设定高度。随后该 stack 会被裁剪。

这是 [layoutBuilder] 的默认值。它实现了 [AnimatedCrossFadeBuilder](https://www.yuque.com/thyname/flutter.widgets/animatedcrossfadebuilder)。

### createState()

```dart
State<AnimatedCrossFade> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
