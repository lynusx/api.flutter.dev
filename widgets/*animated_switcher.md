@docImport 'animated_cross_fade.dart'; @docImport 'implicit_animations.dart';

# AnimatedSwitcherTransitionBuilder

```dart
typedef AnimatedSwitcherTransitionBuilder = Widget Function(Widget child, Animation<double> animation)
```

用于为 [AnimatedSwitcher](https://www.yuque.com/thyname/flutter.widgets/animatedswitcher) 生成自定义过渡效果的 builder 的签名。

当 `animation` 正向运行时，`child` 应当处于过渡进入（transitioning in）的状态。

该函数应返回一个包裹给定 `child` 的组件。它也可以使用 `animation` 来指导其过渡效果。该函数不得返回 null。

# AnimatedSwitcherLayoutBuilder

```dart
typedef AnimatedSwitcherLayoutBuilder = Widget Function(Widget? currentChild, List<Widget> previousChildren)
```

用于为 [AnimatedSwitcher](https://www.yuque.com/thyname/flutter.widgets/animatedswitcher) 生成自定义布局的 builder 的签名。

该 builder 应返回一个包含给定子组件、并按所需方式布局的组件。它不得返回 null。该 builder 应能够处理空的 `previousChildren` 列表，或为 null 的 `currentChild`。

`previousChildren` 列表是一个不可修改的列表，按最旧的排在开头、最新的排在末尾进行排序。它不包含 `currentChild`。

# AnimatedSwitcher

```dart
class AnimatedSwitcher extends StatefulWidget {}
```

一个默认情况下会在新组件与之前设置为 [AnimatedSwitcher](https://www.yuque.com/thyname/flutter.widgets/animatedswitcher) 子组件的组件之间进行交叉淡化的组件。

{@youtube 560 315 https://www.youtube.com/watch?v=2W7POjFb88g}

如果切换足够快（即在 [duration] 经过之前），可能会同时存在多个先前的子组件正在过渡淡出，而最新的子组件正在过渡淡入。

如果“新”子组件与“旧”子组件的组件类型和键（key）相同，但参数不同，那么 [AnimatedSwitcher](https://www.yuque.com/thyname/flutter.widgets/animatedswitcher) _不会_ 在它们之间进行过渡，因为就框架而言，它们是同一个组件，现有组件可以直接使用新参数进行更新。若要强制发生过渡，可以在你希望被视为唯一的每个子组件上设置一个 [Key](https://www.yuque.com/thyname/flutter.foundation/key)（通常是基于用于区分该子组件与其他子组件的数据的 [ValueKey](https://www.yuque.com/thyname/flutter.foundation/valuekey)）。

新子组件可以使用与某个正在淡出的子组件相同的键，二者不会被视为相关联。（例如，如果先显示一个键为 A 的进度指示器，然后显示一个键为 B 的图片，接着又快速显示另一个键为 A 的进度指示器，那么旧的进度指示器和图片会淡出，同时新的进度指示器会淡入。）

通过设置 [transitionBuilder]，可以将过渡类型从交叉淡化改为自定义过渡。

{@tool dartpad} 此示例展示了一个计数器，每当数值发生变化时，会对文本组件的缩放比例进行动画处理。

** 代码参见 examples/api/lib/widgets/animated_switcher/animated_switcher.0.dart ** {@end-tool}

另请参阅：

- [AnimatedCrossFade](https://www.yuque.com/thyname/flutter.widgets/animatedcrossfade)，仅在两个子组件之间进行淡化过渡，但同时也会对它们的大小进行插值，并且是可逆的。
- [AnimatedOpacity](https://www.yuque.com/thyname/flutter.widgets/animatedopacity)，可用于通过对子组件进行淡入淡出，在无内容和给定子组件之间切换。
- [FadeTransition](https://www.yuque.com/thyname/flutter.widgets/fadetransition)，[AnimatedSwitcher](https://www.yuque.com/thyname/flutter.widgets/animatedswitcher) 使用它来执行过渡。

### AnimatedSwitcher()

```dart
AnimatedSwitcher({dynamic key, Widget? child, required Duration duration, Duration? reverseDuration, Curve switchInCurve = Curves.linear, Curve switchOutCurve = Curves.linear, AnimatedSwitcherTransitionBuilder transitionBuilder = AnimatedSwitcher.defaultTransitionBuilder, AnimatedSwitcherLayoutBuilder layoutBuilder = AnimatedSwitcher.defaultLayoutBuilder})
```

创建一个 [AnimatedSwitcher](https://www.yuque.com/thyname/flutter.widgets/animatedswitcher)。

### child

```dart
Widget? child
```

要显示的当前子组件。如果存在先前的子组件，则该子组件将在 [duration] 内使用 [switchOutCurve] 淡出，而新的子组件则使用 [switchInCurve] 淡入。

如果不存在先前的子组件，则此子组件将在 [duration] 内使用 [switchInCurve] 淡入。

如果子组件具有不同的类型或 [Key](https://www.yuque.com/thyname/flutter.foundation/key)，则认为它是“新”的（参见 [Widget.canUpdate]）。

要更改所使用的过渡类型，请参见 [transitionBuilder]。

### duration

```dart
Duration duration
```

从旧的 [child] 值过渡到新值所需的时长。

当 [child] 属性被设置为新的子组件时，此时长会应用于给定的 [child]。除非设置了 [reverseDuration]，否则淡出时也使用相同的时长。更改 [duration] 不会影响已在进行中的过渡的时长。

### reverseDuration

```dart
Duration? reverseDuration
```

从新的 [child] 值过渡回旧值所需的时长。

当 [child] 属性被设置为新的子组件时，此时长会应用于给定的 [child]。更改 [reverseDuration] 不会影响已在进行中的过渡的时长。

如果未设置，则默认使用 [duration] 的值。

### switchInCurve

```dart
Curve switchInCurve
```

过渡进入新 [child] 时使用的动画曲线。

当 [child] 属性被设置为新的子组件时，此曲线会应用于给定的 [child]。更改 [switchInCurve] 不会影响已在进行中的过渡的曲线。

淡出时使用 [switchOutCurve]，但如果在当前子组件正处于淡入过程中时 [child] 发生了改变，则会从该点开始反向运行 [switchInCurve]，而不是直接跳转到 [switchOutCurve] 上的对应点。

### switchOutCurve

```dart
Curve switchOutCurve
```

过渡淡出先前 [child] 时使用的动画曲线。

当子组件淡入时（对于第一个子组件，则是在组件创建时），此曲线会应用于该 [child]。更改 [switchOutCurve] 不会影响已经可见的组件的曲线，它只会影响后续子组件的曲线。

如果在当前子组件正处于淡入过程中时 [child] 发生了改变，则会从该点开始反向运行 [switchInCurve]，而不是直接跳转到 [switchOutCurve] 上的对应点。

### transitionBuilder

```dart
AnimatedSwitcherTransitionBuilder transitionBuilder
```

一个用动画包裹新 [child] 的函数：当动画正向运行时，该动画使 [child] 过渡进入；当动画反向运行时，使其过渡退出。此函数仅在设置了新的 [child] 时被调用（而非每次构建都调用），或在设置了新的 [transitionBuilder] 时被调用。如果设置了新的 [transitionBuilder]，则会使用新的 [transitionBuilder] 为当前子组件和所有先前的子组件重建过渡效果。该函数不得返回 null。

默认值为 [AnimatedSwitcher.defaultTransitionBuilder]。

提供给该 builder 的动画，已应用了对应 [child] 首次提供时所设定的 [duration] 以及 [switchInCurve] 或 [switchOutCurve]。

另请参阅：

- [AnimatedSwitcherTransitionBuilder](https://www.yuque.com/thyname/flutter.widgets/animatedswitchertransitionbuilder)，了解有关过渡 builder 应如何工作的更多信息。

### layoutBuilder

```dart
AnimatedSwitcherLayoutBuilder layoutBuilder
```

一个函数，用一个可以布局所有子组件的组件，将所有正在过渡淡出的子组件以及正在过渡淡入的 [child] 包裹起来。此函数在该组件每次构建时都会被调用。该函数不得返回 null。

默认值为 [AnimatedSwitcher.defaultLayoutBuilder]。

另请参阅：

- [AnimatedSwitcherLayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/animatedswitcherlayoutbuilder)，了解有关布局 builder 应如何工作的更多信息。

### createState()

```dart
State<AnimatedSwitcher> createState()
```

### defaultTransitionBuilder()

```dart
Widget defaultTransitionBuilder(Widget child, Animation<double> animation)
```

作为 [transitionBuilder] 默认值使用的过渡 builder。

新的子组件会被赋予一个 [FadeTransition](https://www.yuque.com/thyname/flutter.widgets/fadetransition)，当动画从 0.0 变化到 1.0 时，其不透明度会增加；当动画反向运行时，其不透明度会降低。

这是一个 [AnimatedSwitcherTransitionBuilder](https://www.yuque.com/thyname/flutter.widgets/animatedswitchertransitionbuilder) 函数。

### defaultLayoutBuilder()

```dart
Widget defaultLayoutBuilder(Widget? currentChild, List<Widget> previousChildren)
```

作为 [layoutBuilder] 默认值使用的布局 builder。

新的子组件被放置在一个 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 中，该 Stack 的大小会与该子组件或先前子组件中最大的一个相匹配。各个子组件彼此居中对齐。

这是一个 [AnimatedSwitcherLayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/animatedswitcherlayoutbuilder) 函数。

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
