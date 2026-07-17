@docImport 'animated_cross_fade.dart'; @docImport 'animated_switcher.dart'; @docImport 'implicit_animations.dart'; @docImport 'navigator.dart'; @docImport 'transitions.dart';

# IndexedStack

```dart
class IndexedStack extends StatelessWidget {}
```

一个 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack)，从子组件列表中只显示一个子组件。

显示的子组件是由给定的 [index] 指定的那个。堆叠的大小始终与最大的子组件相同。

如果该值为 null，则不显示任何内容。

{@youtube 560 315 https://www.youtube.com/watch?v=_O0PPD1Xfbk}

{@tool dartpad} 此示例展示了如何使用 [IndexedStack](https://www.yuque.com/thyname/flutter.widgets/indexedstack) 组件从一系列卡片中一次布局一张卡片，同时各卡片保留各自的状态。

** See code in examples/api/lib/widgets/basic/indexed_stack.0.dart ** {@end-tool}

另请参阅：

- [Stack](https://www.yuque.com/thyname/flutter.widgets/stack)，了解有关堆叠的更多详情。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### IndexedStack()

```dart
IndexedStack({dynamic key, AlignmentGeometry alignment = AlignmentDirectional.topStart, TextDirection? textDirection, Clip clipBehavior = Clip.hardEdge, StackFit sizing = StackFit.loose, int? index = 0, List<Widget> children = const <Widget>[]})
```

创建一个只绘制单个子组件的 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 组件。

### alignment

```dart
AlignmentGeometry alignment
```

如何对齐堆叠中未定位和部分定位的子组件。

默认为 [AlignmentDirectional.topStart]。

更多信息请参阅 [Stack.alignment]。

### textDirection

```dart
TextDirection? textDirection
```

用于解析 [alignment] 的文本方向。

默认为环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

默认为 [Clip.hardEdge]。

### sizing

```dart
StackFit sizing
```

如何设置堆叠中未定位子组件的大小。

默认为 [StackFit.loose]。

更多信息请参阅 [Stack.fit]。

### index

```dart
int? index
```

要显示的子组件的索引。

如果此值为 null，则不显示任何子组件。

### children

```dart
List<Widget> children
```

堆叠的子组件列表。

只有索引为 [index] 的子组件会被显示。

更多信息请参阅 [Stack.children]。

### build()

```dart
Widget build(BuildContext context)
```

# Visibility

```dart
class Visibility extends StatelessWidget {}
```

是否显示或隐藏子组件。

默认情况下，[visible] 属性控制 [child] 是否被包含在子树中；当其不 [visible] 时，将改为包含 [replacement] 子组件（通常是一个零尺寸的盒子）。

可以使用多种标志来调整隐藏子组件的具体方式。（不建议动态更改这些标志，因为这可能导致 [child] 子树被重建，从而丢失该子树中的任何状态。通常只应动态更改 [visible] 标志。）

以下组件提供了此组件的部分功能：

- [Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity)，可以阻止其子组件被绘制。
- [Offstage](https://www.yuque.com/thyname/flutter.widgets/offstage)，可以阻止其子组件被布局或绘制。
- [TickerMode](https://www.yuque.com/thyname/flutter.widgets/tickermode)，可以阻止其子组件被动画化。
- [ExcludeSemantics](https://www.yuque.com/thyname/flutter.widgets/excludesemantics)，可以对无障碍工具隐藏子组件。
- [IgnorePointer](https://www.yuque.com/thyname/flutter.widgets/ignorepointer)，可以禁用与子组件的触摸交互。

隐藏子组件并不一定需要使用此组件。隐藏子组件最简单的方式就是不包含它；但如果*必须*提供一个子组件（例如因为父组件是 [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget)），则可以用 [SizedBox.shrink] 代替原本要包含的子组件。

另请参阅：

- [AnimatedSwitcher](https://www.yuque.com/thyname/flutter.widgets/animatedswitcher)，可以在子树发生变化时，从一个子组件淡出到下一个子组件。
- [AnimatedCrossFade](https://www.yuque.com/thyname/flutter.widgets/animatedcrossfade)，可以在两个特定的子组件之间进行淡入淡出。
- [SliverVisibility](https://www.yuque.com/thyname/flutter.widgets/slivervisibility)，此组件对应的 Sliver 版本。

### Visibility()

```dart
Visibility({dynamic key, required Widget child, Widget replacement = const SizedBox.shrink(), bool visible = true, bool maintainState = false, bool maintainAnimation = false, bool maintainSize = false, bool maintainSemantics = false, bool maintainInteractivity = false, bool maintainFocusability = false})
```

控制给定的 [child] 是否 [visible]。

只有在设置了 [maintainSize] 的情况下，才能设置 [maintainSemantics] 和 [maintainInteractivity] 参数。

只有在设置了 [maintainAnimation] 的情况下，才能设置 [maintainSize] 参数。

只有在设置了 [maintainState] 的情况下，才能设置 [maintainAnimation] 参数。

### Visibility.maintain()

```dart
Visibility.maintain({dynamic key, required Widget child, bool visible = true})
```

控制给定的 [child] 是否 [visible]。

这等价于将默认的 [Visibility](https://www.yuque.com/thyname/flutter.widgets/visibility) 构造函数的所有 "maintain" 字段都设置为 true。此构造函数应替代仅取值 `0.0` 或 `1.0` 的 [Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity) 组件使用，因为它在完全不透明时可避免额外的合成开销。

### child

```dart
Widget child
```

由 [visible] 控制显示或隐藏的组件。

{@macro flutter.widgets.ProxyWidget.child}

### replacement

```dart
Widget replacement
```

当子组件不 [visible] 时使用的组件，前提是未设置任何 `maintain` 标志（尤其是 [maintainState]）。

默认行为是将组件替换为一个零乘零的盒子（[SizedBox.shrink]）。

另请参阅：

- [AnimatedCrossFade](https://www.yuque.com/thyname/flutter.widgets/animatedcrossfade)，可以在两个子组件之间进行动画切换。

### visible

```dart
bool visible
```

在显示 [child] 和隐藏它之间切换。

无论 [visible] 属性处于何种状态，`maintain` 标志都应设置为相同的值，否则它们将无法正常工作（具体来说，只要任何 `maintain` 标志被更改，无论 [maintainState] 的状态如何，都会导致状态丢失，因为这样做会使子树的结构发生变化）。

除非设置了 [maintainState]，否则 [child] 子树在隐藏时将被销毁（从树中移除）。

### maintainState

```dart
bool maintainState
```

当 [child] 子树不 [visible] 时，是否保持其 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象。

保持子树的状态可能代价较高（因为这意味着所有对象仍留在内存中，其资源不会被释放）。只有在无法按需重新创建时，才应保持状态。例如，如果子组件子树中包含 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，则应保持其状态，因为该组件维护着无法即时重新创建的复杂状态。

如果此属性为 true，则会使用 [Offstage](https://www.yuque.com/thyname/flutter.widgets/offstage) 组件来隐藏子组件，而不是用 [replacement] 替换它。

如果此属性为 false，则 [maintainAnimation] 也必须为 false。

如果此属性为 false，则 [maintainFocusability] 也必须为 false。

动态更改此值可能会导致子树的当前状态丢失（如果 [visible] 为 true，则会立即创建一个带有新 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的新子树实例）。

### maintainAnimation

```dart
bool maintainAnimation
```

当 [child] 子树不 [visible] 时，是否保持其中的动画运行。

要设置此项，必须同时设置 [maintainState]。

在组件不可见时保持动画运行，比仅保持状态的开销更大。

一个可能有用的场景是：子树正在以 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 的节奏对其布局进行动画处理，而该布局的结果被用于影响其他逻辑。如果此标志为 false，则托管在 [child] 子树内的所有 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 在 [visible] 标志为 false 时都会被静音。

如果此属性为 true，则不会使用 [TickerMode](https://www.yuque.com/thyname/flutter.widgets/tickermode) 组件。

如果此属性为 false，则 [maintainSize] 也必须为 false。

动态更改此值可能会导致子树的当前状态丢失（如果 [visible] 为 true，则会立即创建一个带有新 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的新子树实例）。

### maintainSize

```dart
bool maintainSize
```

是否为组件本应占据的位置保留空间。

要设置此项，必须同时设置 [maintainAnimation] 和 [maintainState]。

与仅保持动画运行而不保留尺寸相比，在组件不 [visible] 时保留尺寸的开销并不会明显更高；而且在某些情况下，如果子树较简单且 [visible] 属性频繁切换，保留尺寸甚至可能更划算一些，因为这样可以避免在 [visible] 属性切换时触发布局变化。但如果 [child] 子树并不简单，那么完全不保持状态（参见 [maintainState]）的开销会显著更低。

如果此属性为 false，则使用 [Offstage](https://www.yuque.com/thyname/flutter.widgets/offstage)。

如果此属性为 false，则 [maintainSemantics] 和 [maintainInteractivity] 也必须为 false。

动态更改此值可能会导致子树的当前状态丢失（如果 [visible] 为 true，则会立即创建一个带有新 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的新子树实例）。

另请参阅：

- [AnimatedOpacity](https://www.yuque.com/thyname/flutter.widgets/animatedopacity) 和 [FadeTransition](https://www.yuque.com/thyname/flutter.widgets/fadetransition)，它们对不透明度应用动画，以实现更细腻的效果。

### maintainSemantics

```dart
bool maintainSemantics
```

当组件被隐藏时，是否为其保留语义信息（例如用于无障碍功能）。

要设置此项，必须同时设置 [maintainSize]。

默认情况下，[maintainSemantics] 为 false 时，[child] 在被隐藏时对无障碍工具不可见。如果将此标志设置为 true，则无障碍工具会将该组件报告为仍然存在。

### maintainInteractivity

```dart
bool maintainInteractivity
```

是否允许组件在隐藏时仍具有交互性。

要设置此项，必须同时设置 [maintainSize]。

默认情况下，[maintainInteractivity] 为 false 时，触摸事件无法到达被用户隐藏的 [child]。如果将此标志设置为 true，则触摸事件仍然会被传递。

### maintainFocusability

```dart
bool maintainFocusability
```

是否允许组件在隐藏时仍能获得焦点。仅当 [visible] 为 false 时生效。

要将此项设置为 true，必须同时将 [maintainState] 设置为 true。

默认情况下，[maintainFocusability] 为 false 时，由于使用了 [ExcludeFocus](https://www.yuque.com/thyname/flutter.widgets/excludefocus) 组件将子树排除在焦点树之外，焦点事件无法到达不 [visible] 的组件的子树。如果将此标志设置为 true，则焦点事件将能到达该子树。

### of()

```dart
bool of(BuildContext context)
```

根据元素在树中的祖先 [Visibility](https://www.yuque.com/thyname/flutter.widgets/visibility) 元素，判断该元素的可见性状态。

如果祖先树中存在一个或多个 [Visibility](https://www.yuque.com/thyname/flutter.widgets/visibility) 组件，则当且仅当所有这些组件的 [visible] 均设置为 true 时，此方法才会返回 true。如果指定构建上下文的祖先树中不存在 [Visibility](https://www.yuque.com/thyname/flutter.widgets/visibility) 组件，则此方法将返回 true。

这将在指定的上下文与祖先树中的任何 [Visibility](https://www.yuque.com/thyname/flutter.widgets/visibility) 元素之间注册一个依赖关系，因此，如果它们中任何一个的可见性发生变化，指定的上下文都会被重建。

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SliverVisibility

```dart
class SliverVisibility extends StatelessWidget {}
```

是否显示或隐藏一个 sliver 子组件。

默认情况下，[visible] 属性控制 [sliver] 是否被包含在子树中；当其不 [visible] 时，将改为包含 [replacementSliver]。

可以使用多种标志来调整隐藏 sliver 的具体方式。（不建议动态更改这些标志，因为这可能导致 [sliver] 子树被重建，从而丢失该子树中的任何状态。通常只应动态更改 [visible] 标志。）

以下组件提供了此组件的部分功能：

- [SliverOpacity](https://www.yuque.com/thyname/flutter.widgets/sliveropacity)，可以阻止其 sliver 子组件被绘制。
- [SliverOffstage](https://www.yuque.com/thyname/flutter.widgets/sliveroffstage)，可以阻止其 sliver 子组件被布局或绘制。
- [TickerMode](https://www.yuque.com/thyname/flutter.widgets/tickermode)，可以阻止其子组件被动画化。
- [ExcludeSemantics](https://www.yuque.com/thyname/flutter.widgets/excludesemantics)，可以对无障碍工具隐藏子组件。
- [SliverIgnorePointer](https://www.yuque.com/thyname/flutter.widgets/sliverignorepointer)，可以禁用与 sliver 子组件的触摸交互。

隐藏子组件并不一定需要使用此组件。隐藏子组件最简单的方式就是不包含它。如果*必须*提供一个子组件（例如因为父组件是 [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget)），那么使用一个不含子组件的 [SliverToBoxAdapter](https://www.yuque.com/thyname/flutter.widgets/slivertoboxadapter) 来代替原本要包含的子组件，通常比使用 [SliverVisibility](https://www.yuque.com/thyname/flutter.widgets/slivervisibility) 更高效。

另请参阅：

- [Visibility](https://www.yuque.com/thyname/flutter.widgets/visibility)，此组件在盒模型（box）中的等效组件。

### SliverVisibility()

```dart
SliverVisibility({dynamic key, required Widget sliver, Widget replacementSliver = const SliverToBoxAdapter(), bool visible = true, bool maintainState = false, bool maintainAnimation = false, bool maintainSize = false, bool maintainSemantics = false, bool maintainInteractivity = false})
```

控制给定的 [sliver] 是否 [visible]。

只有在设置了 [maintainSize] 的情况下，才能设置 [maintainSemantics] 和 [maintainInteractivity] 参数。

只有在设置了 [maintainAnimation] 的情况下，才能设置 [maintainSize] 参数。

只有在设置了 [maintainState] 的情况下，才能设置 [maintainAnimation] 参数。

### SliverVisibility.maintain()

```dart
SliverVisibility.maintain({dynamic key, required Widget sliver, Widget replacementSliver = const SliverToBoxAdapter(), bool visible = true})
```

控制给定的 [sliver] 是否 [visible]。

这等价于将默认的 [SliverVisibility](https://www.yuque.com/thyname/flutter.widgets/slivervisibility) 构造函数的所有 "maintain" 字段都设置为 true。此构造函数应替代仅取值 `0.0` 或 `1.0` 的 [SliverOpacity](https://www.yuque.com/thyname/flutter.widgets/sliveropacity) 组件使用，因为它在完全不透明时可避免额外的合成开销。

### sliver

```dart
Widget sliver
```

由 [visible] 控制显示或隐藏的 sliver。

### replacementSliver

```dart
Widget replacementSliver
```

当 sliver 子组件不 [visible] 时使用的组件，前提是未设置任何 `maintain` 标志（尤其是 [maintainState]）。

默认行为是将组件替换为一个不含子组件的 [SliverToBoxAdapter](https://www.yuque.com/thyname/flutter.widgets/slivertoboxadapter)，其默认几何形状为 [SliverGeometry.zero]。

### visible

```dart
bool visible
```

在显示 [sliver] 和隐藏它之间切换。

无论 [visible] 属性处于何种状态，`maintain` 标志都应设置为相同的值，否则它们将无法正常工作（具体来说，只要任何 `maintain` 标志被更改，无论 [maintainState] 的状态如何，都会导致状态丢失，因为这样做会使子树的结构发生变化）。

除非设置了 [maintainState]，否则 [sliver] 子树在隐藏时将被销毁（从树中移除）。

### maintainState

```dart
bool maintainState
```

当 [sliver] 子树不 [visible] 时，是否保持其 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象。

保持子树的状态可能代价较高（因为这意味着所有对象仍留在内存中，其资源不会被释放）。只有在无法按需重新创建时，才应保持状态。例如，如果 sliver 子树中包含 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，则应保持其状态，因为该组件维护着无法即时重新创建的复杂状态。

如果此属性为 true，则会使用 [SliverOffstage](https://www.yuque.com/thyname/flutter.widgets/sliveroffstage) 组件来隐藏 sliver，而不是用 [replacementSliver] 替换它。

如果此属性为 false，则 [maintainAnimation] 也必须为 false。

动态更改此值可能会导致子树的当前状态丢失（如果 [visible] 为 true，则会立即创建一个带有新 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的新子树实例）。

### maintainAnimation

```dart
bool maintainAnimation
```

当 [sliver] 子树不 [visible] 时，是否保持其中的动画运行。

要设置此项，必须同时设置 [maintainState]。

在组件不可见时保持动画运行，比仅保持状态的开销更大。

一个可能有用的场景是：子树正在以 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 的节奏对其布局进行动画处理，而该布局的结果被用于影响其他逻辑。如果此标志为 false，则托管在 [sliver] 子树内的所有 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 在 [visible] 标志为 false 时都会被静音。

如果此属性为 true，则不会使用 [TickerMode](https://www.yuque.com/thyname/flutter.widgets/tickermode) 组件。

如果此属性为 false，则 [maintainSize] 也必须为 false。

动态更改此值可能会导致子树的当前状态丢失（如果 [visible] 为 true，则会立即创建一个带有新 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的新子树实例）。

### maintainSize

```dart
bool maintainSize
```

是否为 sliver 本应占据的位置保留空间。

要设置此项，必须同时设置 [maintainAnimation]。

与仅保持动画运行而不保留尺寸相比，在 sliver 不 [visible] 时保留尺寸的开销并不会明显更高；而且在某些情况下，如果子树较简单且 [visible] 属性频繁切换，保留尺寸甚至可能更划算一些，因为这样可以避免在 [visible] 属性切换时触发布局变化。但如果 [sliver] 子树并不简单，那么完全不保持状态（参见 [maintainState]）的开销会显著更低。

如果此属性为 false，则使用 [SliverOffstage](https://www.yuque.com/thyname/flutter.widgets/sliveroffstage)。

如果此属性为 false，则 [maintainSemantics] 和 [maintainInteractivity] 也必须为 false。

动态更改此值可能会导致子树的当前状态丢失（如果 [visible] 为 true，则会立即创建一个带有新 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的新子树实例）。

### maintainSemantics

```dart
bool maintainSemantics
```

当 sliver 被隐藏时，是否为其保留语义信息（例如用于无障碍功能）。

要设置此项，必须同时设置 [maintainSize]。

默认情况下，[maintainSemantics] 为 false 时，[sliver] 在被隐藏时对无障碍工具不可见。如果将此标志设置为 true，则无障碍工具会将该 sliver 报告为仍然存在。

### maintainInteractivity

```dart
bool maintainInteractivity
```

是否允许 sliver 在隐藏时仍具有交互性。

要设置此项，必须同时设置 [maintainSize]。

默认情况下，[maintainInteractivity] 为 false 时，触摸事件无法到达被用户隐藏的 [sliver]。如果将此标志设置为 true，则触摸事件仍然会被传递。
