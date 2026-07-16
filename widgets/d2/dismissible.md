@docImport 'scroll_view.dart';

# DismissDirectionCallback

```dart
typedef DismissDirectionCallback = void Function(DismissDirection direction)
```

用于 [Dismissible](https://www.yuque.com/thyname/flutter.widgets/dismissible) 指示其已经被朝给定的 `direction` 方向消除的回调签名。

由 [Dismissible.onDismissed] 使用。

# ConfirmDismissCallback

```dart
typedef ConfirmDismissCallback = Future<bool?> Function(DismissDirection direction)
```

用于 [Dismissible](https://www.yuque.com/thyname/flutter.widgets/dismissible) 让应用程序有机会确认或否决消除手势的回调签名。

由 [Dismissible.confirmDismiss] 使用。

# DismissUpdateCallback

```dart
typedef DismissUpdateCallback = void Function(DismissUpdateDetails details)
```

用于 [Dismissible](https://www.yuque.com/thyname/flutter.widgets/dismissible) 指示该可消除组件已被拖动的回调签名。

由 [Dismissible.onUpdate] 使用。

# DismissDirection

```dart
enum DismissDirection {}
```

[Dismissible](https://www.yuque.com/thyname/flutter.widgets/dismissible) 可被消除的方向。

[Dismissible](https://www.yuque.com/thyname/flutter.widgets/dismissible) 可以通过向上或向下拖动来消除。

[Dismissible](https://www.yuque.com/thyname/flutter.widgets/dismissible) 可以通过向左或向右拖动来消除。

[Dismissible](https://www.yuque.com/thyname/flutter.widgets/dismissible) 可以通过沿阅读方向的反方向拖动来消除（例如，在从左到右的语言中，从右向左拖动）。

[Dismissible](https://www.yuque.com/thyname/flutter.widgets/dismissible) 可以通过沿阅读方向拖动来消除（例如，在从左到右的语言中，从左向右拖动）。

[Dismissible](https://www.yuque.com/thyname/flutter.widgets/dismissible) 只能通过向上拖动来消除。

[Dismissible](https://www.yuque.com/thyname/flutter.widgets/dismissible) 只能通过向下拖动来消除。

[Dismissible](https://www.yuque.com/thyname/flutter.widgets/dismissible) 不能通过拖动来消除。

# Dismissible

```dart
class Dismissible extends StatefulWidget {}
```

一个可以通过沿指定 [direction] 拖动来消除的 Widget。

在此 Widget 沿 [DismissDirection](https://www.yuque.com/thyname/flutter.widgets/dismissdirection) 方向拖动或滑动时，其子组件会滑出视图。滑动动画结束后，如果 [resizeDuration] 不为空，Dismissible Widget 会在 [resizeDuration] 时间内将其高度（或宽度，取决于与消除方向垂直的那个轴）动画过渡为零。

{@youtube 560 315 https://www.youtube.com/watch?v=iEMgjrfuc58}

{@tool dartpad} 此示例展示了如何使用 [Dismissible](https://www.yuque.com/thyname/flutter.widgets/dismissible) Widget 通过滑动手势移除列表项。滑动任意列表项的左侧或右侧即可将其从 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview) 中消除。

** See code in examples/api/lib/widgets/dismissible/dismissible.0.dart ** {@end-tool}

背景组件可用于实现“留白提示”（leave-behind）的交互模式。如果指定了背景组件，它会堆叠在 Dismissible 子组件的后面，并在子组件移动时显现出来。

当此 Widget 的尺寸已收缩为零时（如果 [resizeDuration] 不为空），或者在滑动动画结束后立即（如果 [resizeDuration] 为空），此 Widget 会调用 [onDismissed] 回调。如果 Dismissible 是一个列表项，它必须拥有一个区别于其他列表项的键（key），并且其 [onDismissed] 回调必须将该列表项从列表中移除。

### Dismissible()

```dart
Dismissible({required Key key, required Widget child, Widget? background, Widget? secondaryBackground, ConfirmDismissCallback? confirmDismiss, VoidCallback? onResize, DismissUpdateCallback? onUpdate, DismissDirectionCallback? onDismissed, DismissDirection direction = DismissDirection.horizontal, Duration? resizeDuration = const Duration(milliseconds: 300), Map<DismissDirection, double> dismissThresholds = const <DismissDirection, double>{}, Duration movementDuration = const Duration(milliseconds: 200), double crossAxisEndOffset = 0.0, DragStartBehavior dragStartBehavior = DragStartBehavior.start, HitTestBehavior behavior = HitTestBehavior.opaque})
```

创建一个可被消除的 Widget。

[key] 参数是必需的，因为 [Dismissible](https://www.yuque.com/thyname/flutter.widgets/dismissible) 通常用于列表中，并在被消除后从列表中移除。如果没有键，默认行为是根据列表中的索引来同步 Widget，这意味着被消除项之后的项会同步为被消除项的状态。使用键可使 Widget 根据键进行同步，从而避免此问题。

### child

```dart
Widget child
```

此 Widget 树中位于此 Widget 下方的 Widget。

{@macro flutter.widgets.ProxyWidget.child}

### background

```dart
Widget? background
```

堆叠在子组件后面的 Widget。如果同时指定了 secondaryBackground，则此 Widget 仅在子组件被向下或向右拖动时显示。

### secondaryBackground

```dart
Widget? secondaryBackground
```

堆叠在子组件后面的 Widget，在子组件被向上或向左拖动时显现。仅当同时指定了 background 时才能指定此参数。

### confirmDismiss

```dart
ConfirmDismissCallback? confirmDismiss
```

让应用程序有机会确认或否决即将发生的消除操作。

在返回的 future 完成之前，无法再次拖动此 Widget。

如果返回的 `Future<bool>` 结果为 true，则此 Widget 将被消除，否则它将被移回原位置。

如果返回的 `Future<bool?>` 结果为 false 或 null，则不会运行 [onResize] 和 [onDismissed] 回调。

### onResize

```dart
VoidCallback? onResize
```

当此 Widget 改变尺寸时（即在被消除前收缩时）调用。

### onDismissed

```dart
DismissDirectionCallback? onDismissed
```

在此 Widget 被消除、完成收缩后调用。

### direction

```dart
DismissDirection direction
```

此 Widget 可被消除的方向。

### resizeDuration

```dart
Duration? resizeDuration
```

此 Widget 在调用 [onDismissed] 之前收缩所花费的时间。

如果为空，此 Widget 将不会收缩，[onDismissed] 将在此 Widget 被消除后立即被调用。

### dismissThresholds

```dart
Map<DismissDirection, double> dismissThresholds
```

某一项被视为已消除时所需拖动的偏移阈值。

以比例表示，例如若为 0.4（默认值），则该项必须朝某个方向至少拖动 40% 才会被视为已消除。调用方可以为每个消除方向定义不同的阈值。

滑动（fling）操作等同于将该项拖动至接近 1.0 的位置，因此滑动可以消除任何小于 1.0 的阈值所对应的项。

将阈值设置为 1.0（或更大）会阻止在给定的 [DismissDirection](https://www.yuque.com/thyname/flutter.widgets/dismissdirection) 方向上进行拖动，即使 [direction] 属性允许该方向。

另请参阅：

- [direction]，用于控制这些项可被消除的方向。

### movementDuration

```dart
Duration movementDuration
```

定义卡片消除的动画时长，或在未被消除时返回原位置的动画时长。

### crossAxisEndOffset

```dart
double crossAxisEndOffset
```

定义卡片消除后沿主轴交叉方向的结束偏移量。

如果给定非零值，则 Widget 会根据该值的正负沿交叉方向移动。

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

确定拖动开始行为的处理方式。

如果设置为 [DragStartBehavior.start]，用于消除 Dismissible 的拖动手势将从该手势在竞技场（arena）中获胜的位置开始。如果设置为 [DragStartBehavior.down]，则将从首次检测到按下事件的位置开始。

通常，将此项设置为 [DragStartBehavior.start] 会使拖动动画更加流畅，而设置为 [DragStartBehavior.down] 会使拖动行为感觉更加灵敏。

默认情况下，拖动开始行为为 [DragStartBehavior.start]。

另请参阅：

- [DragGestureRecognizer.dragStartBehavior]，其中给出了不同行为方式的示例。

### behavior

```dart
HitTestBehavior behavior
```

在命中测试（hit test）期间的行为方式。

默认值为 [HitTestBehavior.opaque]。

### onUpdate

```dart
DismissUpdateCallback? onUpdate
```

在该可消除 Widget 被拖动时调用。

如果 [onUpdate] 不为空，则会针对每个指针事件调用它，以传递拖动的最新状态。例如，此回调可用于根据是否已达到消除阈值来改变背景组件的颜色。

### createState()

```dart
State<Dismissible> createState()
```

# DismissUpdateDetails

```dart
class DismissUpdateDetails {}
```

[DismissUpdateCallback](https://www.yuque.com/thyname/flutter.widgets/dismissupdatecallback) 的详细信息。

另请参阅：

- [Dismissible.onUpdate]，接收此信息的回调。

### DismissUpdateDetails()

```dart
DismissUpdateDetails({DismissDirection direction = DismissDirection.horizontal, bool reached = false, bool previousReached = false, double progress = 0.0})
```

创建一个新的 [DismissUpdateDetails](https://www.yuque.com/thyname/flutter.widgets/dismissupdatedetails) 实例。

### direction

```dart
DismissDirection direction
```

该可消除组件正在被拖动的方向。

### reached

```dart
bool reached
```

当前是否已达到消除阈值。

### previousReached

```dart
bool previousReached
```

上一次调用此回调时是否已达到消除阈值。

此属性可与 [DismissUpdateDetails.reached] 结合使用，以捕捉 [Dismissible](https://www.yuque.com/thyname/flutter.widgets/dismissible) 被拖过阈值的那一刻。

### progress

```dart
double progress
```

该可消除组件在其父容器中的偏移比例。

值为 0.0 表示正常位置，1.0 表示子组件已完全移出其父容器。

此值可用于将屏幕上的其他元素与可消除组件的动作同步，例如利用此值设置透明度，从而在可消除组件被拖离屏幕时使其淡出。
