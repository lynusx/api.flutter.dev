# DragTargetWillAccept

```dart
typedef DragTargetWillAccept<T> = bool Function(T? data)
```

用于确定给定数据是否会被 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 接受的签名。

由 [DragTarget.onWillAccept] 使用。

# DragTargetWillAcceptWithDetails

```dart
typedef DragTargetWillAcceptWithDetails<T> = bool Function(DragTargetDetails<T> details)
```

根据提供的信息确定给定数据是否会被 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 接受的签名。

由 [DragTarget.onWillAcceptWithDetails] 使用。

# DragTargetAccept

```dart
typedef DragTargetAccept<T> = void Function(T data)
```

使 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 接受给定数据的签名。

由 [DragTarget.onAccept] 使用。

# DragTargetAcceptWithDetails

```dart
typedef DragTargetAcceptWithDetails<T> = void Function(DragTargetDetails<T> details)
```

确定 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 接受相关信息的签名。

由 [DragTarget.onAcceptWithDetails] 使用。

# DragTargetBuilder

```dart
typedef DragTargetBuilder<T> = Widget Function(BuildContext context, List<T?> candidateData, List<dynamic> rejectedData)
```

用于构建 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 子组件的签名。

`candidateData` 参数包含当前悬停在此 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 上、且已通过 [DragTarget.onWillAcceptWithDetails] 检查的拖拽数据列表。`rejectedData` 参数包含当前悬停在此 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 上、但不会被该 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 接受的拖拽数据列表。

由 [DragTarget.builder] 使用。

# DragUpdateCallback

```dart
typedef DragUpdateCallback = void Function(DragUpdateDetails details)
```

当 [Draggable](https://www.yuque.com/thyname/flutter.widgets/draggable) 在屏幕上被拖动时触发的签名。

由 [Draggable.onDragUpdate] 使用。

# DraggableCanceledCallback

```dart
typedef DraggableCanceledCallback = void Function(Velocity velocity, Offset offset)
```

当 [Draggable](https://www.yuque.com/thyname/flutter.widgets/draggable) 被放下但未被任何 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 接受时触发的签名。

由 [Draggable.onDraggableCanceled] 使用。

# DragEndCallback

```dart
typedef DragEndCallback = void Function(DraggableDetails details)
```

当可拖拽组件被放下时触发的签名。

指针在可拖拽组件被放下时的移动速度和偏移量可在 [DraggableDetails](https://www.yuque.com/thyname/flutter.widgets/draggabledetails) 中获取。`details` 中还包含该可拖拽组件是否被其 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 接受的信息。

由 [Draggable.onDragEnd] 使用。

# DragTargetLeave

```dart
typedef DragTargetLeave<T> = void Function(T? data)
```

当 [Draggable](https://www.yuque.com/thyname/flutter.widgets/draggable) 离开 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 时触发的签名。

由 [DragTarget.onLeave] 使用。

# DragTargetMove

```dart
typedef DragTargetMove<T> = void Function(DragTargetDetails<T> details)
```

当 [Draggable](https://www.yuque.com/thyname/flutter.widgets/draggable) 在 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 内部移动时触发的签名。

由 [DragTarget.onMove] 使用。

# DragAnchorStrategy

```dart
typedef DragAnchorStrategy = Offset Function(Draggable<Object> draggable, BuildContext context, Offset position)
```

用于确定 [Draggable](https://www.yuque.com/thyname/flutter.widgets/draggable) 拖拽起始点的策略签名。

由 [Draggable.dragAnchorStrategy] 使用。

内置两种策略：

- [childDragAnchorStrategy](https://www.yuque.com/thyname/flutter.widgets/childdraganchorstrategy)：将反馈组件锚定显示在原始子组件的位置。

- [pointerDragAnchorStrategy](https://www.yuque.com/thyname/flutter.widgets/pointerdraganchorstrategy)：将反馈组件锚定显示在启动拖拽的触摸点位置。

# childDragAnchorStrategy()

```dart
Offset childDragAnchorStrategy(Draggable<Object> draggable, BuildContext context, Offset position)
```

将反馈组件锚定显示在原始子组件的位置。

如果反馈组件（feedback）与子组件（child）相同，这意味着在拖拽开始时，反馈组件将与原始子组件完全重合。

这是默认的 [DragAnchorStrategy](https://www.yuque.com/thyname/flutter.widgets/draganchorstrategy)。

另请参阅：

- [DragAnchorStrategy](https://www.yuque.com/thyname/flutter.widgets/draganchorstrategy)，此函数所实现的类型定义。
- [Draggable.dragAnchorStrategy]，该属性的内置取值之一。

# pointerDragAnchorStrategy()

```dart
Offset pointerDragAnchorStrategy(Draggable<Object> draggable, BuildContext context, Offset position)
```

将反馈组件锚定显示在启动拖拽的触摸点位置。

如果反馈组件与子组件相同，这意味着拖拽开始时反馈组件的左上角将位于手指下方，这通常不会与原始子组件完全重合，例如当子组件较大且触摸点不在其中心时。当反馈组件经过变换（例如向左偏移其宽度的一半，向上偏移其宽度的一半加上手指高度）时，这种模式非常有用，因为这样一来，手指按下时反馈组件看起来就像出现在手指上方。（如果反馈组件锚定在子组件而不是手指上，却显示为偏离原始子组件的位置，会让人感觉很奇怪。）

另请参阅：

- [DragAnchorStrategy](https://www.yuque.com/thyname/flutter.widgets/draganchorstrategy)，此函数所实现的类型定义。
- [Draggable.dragAnchorStrategy]，该属性的内置取值之一。

# Draggable

```dart
class Draggable<T extends Object> extends StatefulWidget {}
```

一个可以从中拖拽到 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 的组件。

当可拖拽组件识别到拖拽手势开始时，会显示一个 [feedback] 组件，跟随用户手指在屏幕上移动。如果用户在 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 上方松开手指，该目标将有机会接受可拖拽组件携带的 [data]。

[ignoringFeedbackPointer] 默认为 true，这意味着 [feedback] 组件在命中测试（hit testing）时会忽略指针事件。类似地，[ignoringFeedbackSemantics] 默认为 true，[feedback] 在构建语义树时也会忽略语义信息。

在多点触控设备上，由于同一时刻设备上可能存在多个触点，因此可以同时进行多个拖拽操作。要限制同时进行的拖拽数量，可使用 [maxSimultaneousDrags] 属性。默认情况下不限制同时拖拽的数量。

当没有拖拽正在进行时，此组件显示 [child]。如果 [childWhenDragging] 非空，则在一个或多个拖拽正在进行时，此组件将显示 [childWhenDragging]。否则，此组件将始终显示 [child]。

{@youtube 560 315 https://www.youtube.com/watch?v=q4x2G_9-Mu0}

{@tool dartpad} 以下示例展示了一行中包含 [Draggable](https://www.yuque.com/thyname/flutter.widgets/draggable) 组件与 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 组件，演示了将元素拖到目标位置后，`acceptedData` 整数值递增的效果。

** 参见 examples/api/lib/widgets/drag_target/draggable.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget)
- [LongPressDraggable](https://www.yuque.com/thyname/flutter.widgets/longpressdraggable)

### Draggable()

```dart
Draggable({dynamic key, required Widget child, required Widget feedback, T? data, Axis? axis, Widget? childWhenDragging, Offset feedbackOffset = Offset.zero, DragAnchorStrategy dragAnchorStrategy = childDragAnchorStrategy, Axis? affinity, int? maxSimultaneousDrags, VoidCallback? onDragStarted, DragUpdateCallback? onDragUpdate, DraggableCanceledCallback? onDraggableCanceled, DragEndCallback? onDragEnd, VoidCallback? onDragCompleted, bool ignoringFeedbackSemantics = true, bool ignoringFeedbackPointer = true, bool rootOverlay = false, HitTestBehavior hitTestBehavior = HitTestBehavior.deferToChild, AllowedButtonsFilter? allowedButtonsFilter})
```

创建一个可以拖拽到 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 的组件。

如果 [maxSimultaneousDrags] 非空，其值必须为非负数。

### data

```dart
T? data
```

此可拖拽组件被放下时将传递的数据。

### axis

```dart
Axis? axis
```

限制此可拖拽组件移动方向的 [Axis](https://www.yuque.com/thyname/flutter.painting/axis)（如果指定）。

当 axis 设置为 [Axis.horizontal] 时，此组件只能水平拖动。[Axis.vertical] 时行为类似。

默认允许在 [Axis.horizontal] 和 [Axis.vertical] 两个方向上拖动。

为 null 时，允许在 [Axis.horizontal] 和 [Axis.vertical] 两个方向上拖动。

关于此组件与哪些手势竞争以启动拖拽事件的方向，请参阅 [Draggable.affinity]。

### child

```dart
Widget child
```

此组件在组件树中的下级组件。

当没有拖拽正在进行时，此组件显示 [child]。如果 [childWhenDragging] 非空，则在一个或多个拖拽正在进行时，此组件将显示 [childWhenDragging]。否则，此组件将始终显示 [child]。

[feedback] 组件会在拖拽进行中显示在指针下方。

关于限制多点触控设备上同时拖拽的数量，请参阅 [maxSimultaneousDrags]。

{@macro flutter.widgets.ProxyWidget.child}

### childWhenDragging

```dart
Widget? childWhenDragging
```

当一个或多个拖拽正在进行时，用于替代 [child] 显示的组件。

如果此值为 null，则此组件将始终显示 [child]（因此在拖拽进行期间，拖拽源的外观不会发生变化）。

[feedback] 组件会在拖拽进行中显示在指针下方。

关于限制多点触控设备上同时拖拽的数量，请参阅 [maxSimultaneousDrags]。

### feedback

```dart
Widget feedback
```

拖拽进行期间显示在指针下方的组件。

关于拖拽进行期间 [Draggable](https://www.yuque.com/thyname/flutter.widgets/draggable) 自身位置处显示的内容，请参阅 [child] 和 [childWhenDragging]。

### feedbackOffset

```dart
Offset feedbackOffset
```

feedbackOffset 可用于设置查找拖拽目标时的命中测试点。当反馈组件相对于子组件经过变换时，该属性尤其有用。

### dragAnchorStrategy

```dart
DragAnchorStrategy dragAnchorStrategy
```

此可拖拽组件在被拖动时用于获取锚点偏移量的策略。

锚点偏移量是指此可拖拽组件被拖动时，用户手指与 [feedback] 组件之间的距离。

此属性的值是一个实现 [DragAnchorStrategy](https://www.yuque.com/thyname/flutter.widgets/draganchorstrategy) 的函数。有两个内置函数可供使用：

- [childDragAnchorStrategy](https://www.yuque.com/thyname/flutter.widgets/childdraganchorstrategy)：将反馈组件锚定显示在原始子组件的位置。

- [pointerDragAnchorStrategy](https://www.yuque.com/thyname/flutter.widgets/pointerdraganchorstrategy)：将反馈组件锚定显示在启动拖拽的触摸点位置。

默认为 [childDragAnchorStrategy](https://www.yuque.com/thyname/flutter.widgets/childdraganchorstrategy)。

### ignoringFeedbackSemantics

```dart
bool ignoringFeedbackSemantics
```

构建语义树时是否忽略 [feedback] 组件的语义信息。

当 [feedback] 组件与 [child] 是同一个对象时，应将此值设为 false。在此组件上放置 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 将确保该元素在移入和移出反馈位置时保持语义焦点。

默认为 true。

### ignoringFeedbackPointer

```dart
bool ignoringFeedbackPointer
```

命中测试期间是否忽略 [feedback] 组件。

无论此组件在命中测试期间是否被忽略，它在布局阶段仍会占用空间，在绘制阶段仍然可见。

默认为 true。

### affinity

```dart
Axis? affinity
```

控制此组件如何与其他手势竞争以发起拖拽。

如果 affinity 为 null，此组件会在识别到按下手势时立即开始拖拽，无论方向如何。如果 affinity 为水平方向（或垂直方向），则此组件将与其他水平（或垂直）手势竞争。

例如，如果此组件放置在一个垂直滚动区域内，并具有水平方向的 affinity，则指针在垂直方向上的移动将导致滚动，而在水平方向上的移动将导致拖拽。相反，如果此组件的 affinity 为 null 或垂直方向，则指针在任何方向上的移动都会导致拖拽而不是滚动，因为可拖拽组件作为更具体的组件，将在垂直手势上胜过 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable)。

关于拖拽事件开始后此组件可被拖动的方向，请参阅 [Draggable.axis]。

### maxSimultaneousDrags

```dart
int? maxSimultaneousDrags
```

支持同时进行的拖拽数量。

为 null 时不施加任何限制。如果只希望拖拽源一次只能拖动一个项目，请将此值设为 1。如果希望阻止可拖拽组件实际被拖动，请将此值设为 0。

如果将此属性设为 1，可考虑为 [childWhenDragging] 提供一个"空"组件，以营造 [child] 真正在移动的错觉。

### onDragStarted

```dart
VoidCallback? onDragStarted
```

当可拖拽组件开始被拖动时调用。

### onDragUpdate

```dart
DragUpdateCallback? onDragUpdate
```

当可拖拽组件被拖动时调用。

此函数仅在此组件仍挂载于组件树中时（即 [State.mounted] 为 true）才会被调用，且仅当此组件确实发生了移动时才会调用。

### onDraggableCanceled

```dart
DraggableCanceledCallback? onDraggableCanceled
```

当可拖拽组件被放下但未被 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 接受时调用。

此函数可能在此组件已从组件树中移除后仍被调用。例如，如果在此组件从树中移除时拖拽正在进行，且该拖拽最终被取消，此回调仍会被调用。因此，此回调的实现可能需要检查 [State.mounted]，以确认接收回调的 State 是否仍在树中。

### onDragCompleted

```dart
VoidCallback? onDragCompleted
```

当可拖拽组件被放下并被 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 接受时调用。

此函数可能在此组件已从组件树中移除后仍被调用。例如，如果在此组件从树中移除时拖拽正在进行，且该拖拽最终完成，此回调仍会被调用。因此，此回调的实现可能需要检查 [State.mounted]，以确认接收回调的 State 是否仍在树中。

### onDragEnd

```dart
DragEndCallback? onDragEnd
```

当可拖拽组件被放下时调用。

指针在放下时的移动速度和偏移量可在 [DraggableDetails](https://www.yuque.com/thyname/flutter.widgets/draggabledetails) 中获取。`details` 中还包含该可拖拽组件的 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 是否接受了它的信息。

此函数仅在此组件仍挂载于组件树中时（即 [State.mounted] 为 true）才会被调用。

### rootOverlay

```dart
bool rootOverlay
```

反馈组件是否放置在根 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 上。

为 false 时，反馈组件将放置在最近的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 上。为 true 时，[feedback] 组件将放置在最远（即根）的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 上。

默认为 false。

### hitTestBehavior

```dart
HitTestBehavior hitTestBehavior
```

命中测试期间的行为方式。

默认为 [HitTestBehavior.deferToChild]。

### allowedButtonsFilter

```dart
AllowedButtonsFilter? allowedButtonsFilter
```

{@macro flutter.gestures.multidrag.\_allowedButtonsFilter}

### createRecognizer()

```dart
MultiDragGestureRecognizer createRecognizer(GestureMultiDragStartCallback onStart)
```

创建一个用于识别拖拽开始的手势识别器。

子类可以重写此函数，以自定义开始识别拖拽的时机。

### createState()

```dart
State<Draggable<T>> createState()
```

# LongPressDraggable

```dart
class LongPressDraggable<T extends Object> extends Draggable<T> {}
```

使其子组件从长按开始变为可拖拽。

另请参阅：

- [Draggable](https://www.yuque.com/thyname/flutter.widgets/draggable)，与 [LongPressDraggable](https://www.yuque.com/thyname/flutter.widgets/longpressdraggable) 类似的组件，但会立即开始拖拽。
- [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget)，一个在 [Draggable](https://www.yuque.com/thyname/flutter.widgets/draggable) 组件被放下时接收数据的组件。

### LongPressDraggable()

```dart
LongPressDraggable({dynamic key, required Widget child, required Widget feedback, T? data, dynamic axis, Widget? childWhenDragging, dynamic feedbackOffset, InvalidType Function(Draggable<Object>, BuildContext, InvalidType) dragAnchorStrategy, int? maxSimultaneousDrags, dynamic onDragStarted, void Function(InvalidType)? onDragUpdate, void Function(InvalidType, InvalidType)? onDraggableCanceled, void Function(DraggableDetails)? onDragEnd, dynamic onDragCompleted, bool hapticFeedbackOnStart = true, bool ignoringFeedbackSemantics, bool ignoringFeedbackPointer, Duration delay = kLongPressTimeout, dynamic allowedButtonsFilter, dynamic hitTestBehavior, bool rootOverlay})
```

创建一个可从长按开始拖拽的组件。

如果 [maxSimultaneousDrags] 非空，其值必须为非负数。

### hapticFeedbackOnStart

```dart
bool hapticFeedbackOnStart
```

拖拽开始时是否应触发触觉反馈。

### delay

```dart
Duration delay
```

用户需要按住多久才会被识别为长按。

默认为 [kLongPressTimeout](https://www.yuque.com/thyname/flutter.gestures/klongpresstimeout)。

### createRecognizer()

```dart
DelayedMultiDragGestureRecognizer createRecognizer(GestureMultiDragStartCallback onStart)
```

# DraggableDetails

```dart
class DraggableDetails {}
```

表示某个指针事件发生在 [Draggable](https://www.yuque.com/thyname/flutter.widgets/draggable) 上时的详细信息。

包含指针事件发生时的移动 [Velocity](https://www.yuque.com/thyname/flutter.gestures/velocity)（速度）和 [Offset](https://www.yuque.com/thyname/dart.ui/offset)（偏移量），以及其 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 是否接受了该操作。

同时，这也是使用 [DragEndCallback](https://www.yuque.com/thyname/flutter.widgets/dragendcallback) 的回调所对应的详情对象。

### DraggableDetails()

```dart
DraggableDetails({bool wasAccepted = false, required Velocity velocity, required Offset offset})
```

为 [DraggableDetails](https://www.yuque.com/thyname/flutter.widgets/draggabledetails) 创建详情对象。

如果未指定 [wasAccepted]，默认为 `false`。

[velocity] 和 [offset] 参数不能为 `null`。

### wasAccepted

```dart
bool wasAccepted
```

确定 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 是否接受了此可拖拽组件。

### velocity

```dart
Velocity velocity
```

指针事件发生在可拖拽组件上时，指针移动的速度。

### offset

```dart
Offset offset
```

指定指针事件发生在可拖拽组件上时的全局位置。

# DragTargetDetails

```dart
class DragTargetDetails<T> {}
```

表示某个指针事件发生在 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 上时的详细信息。

### DragTargetDetails()

```dart
DragTargetDetails({required T data, required Offset offset})
```

为 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 回调创建详情对象。

### data

```dart
T data
```

放置到此 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 上的数据。

### offset

```dart
Offset offset
```

指定指针事件发生在可拖拽组件上时的全局位置。

# DragTarget

```dart
class DragTarget<T extends Object> extends StatefulWidget {}
```

一个在 [Draggable](https://www.yuque.com/thyname/flutter.widgets/draggable) 组件被放下时接收数据的组件。

当可拖拽组件被拖到拖拽目标上方时，会询问该拖拽目标是否愿意接受可拖拽组件携带的数据。如果用户确实将可拖拽组件放到了拖拽目标上（且该拖拽目标已表明愿意接受该数据），则会要求拖拽目标接受该数据。

另请参阅：

- [Draggable](https://www.yuque.com/thyname/flutter.widgets/draggable)
- [LongPressDraggable](https://www.yuque.com/thyname/flutter.widgets/longpressdraggable)

### DragTarget()

```dart
DragTarget({dynamic key, required DragTargetBuilder<T> builder, DragTargetWillAccept<T>? onWillAccept, DragTargetWillAcceptWithDetails<T>? onWillAcceptWithDetails, DragTargetAccept<T>? onAccept, DragTargetAcceptWithDetails<T>? onAcceptWithDetails, DragTargetLeave<T>? onLeave, DragTargetMove<T>? onMove, HitTestBehavior hitTestBehavior = HitTestBehavior.translucent})
```

创建一个接收拖拽的组件。

### builder

```dart
DragTargetBuilder<T> builder
```

用于构建此组件内容的回调。

builder 可以根据被拖入此拖拽目标的内容构建不同的组件。

当可拖拽组件进入目标时，会调用 [onWillAccept] 或 [onWillAcceptWithDetails]。如果返回 true，则该数据将出现在 `candidateData` 中，否则出现在 `rejectedData` 中。

通常，builder 会检查 `candidateData` 和 `rejectedData`，并构建一个组件来表明将 `candidateData` 放到此目标上的结果。

`candidateData` 和 `rejectedData` 是 [List](https://www.yuque.com/thyname/dart.core/list) 类型，以支持多个同时进行的拖拽。

如果 `candidateData` 或 `rejectedData` 中出现意外的 `null` 值，请确保 [Draggable](https://www.yuque.com/thyname/flutter.widgets/draggable) 的 `data` 参数不为 `null`。

### onWillAccept

```dart
DragTargetWillAccept<T>? onWillAccept
```

用于确定此组件是否有兴趣接收被拖到此拖拽目标上方的给定数据。

当数据进入目标时调用。如果数据被放下，之后会依次调用 [onAccept] 和 [onAcceptWithDetails]；如果拖拽离开目标，则会调用 [onLeave]。

与 [onWillAcceptWithDetails] 等效，但仅包含数据本身。

如果已提供 [onWillAcceptWithDetails]，则不得再提供此项。

### onWillAcceptWithDetails

```dart
DragTargetWillAcceptWithDetails<T>? onWillAcceptWithDetails
```

用于确定此组件是否有兴趣接收被拖到此拖拽目标上方的给定数据。

当数据进入目标时调用。如果数据被放下，之后会依次调用 [onAccept] 和 [onAcceptWithDetails]；如果拖拽离开目标，则会调用 [onLeave]。

与 [onWillAccept] 等效，但会在 [DragTargetDetails](https://www.yuque.com/thyname/flutter.widgets/dragtargetdetails) 中提供包括数据在内的更多信息。

如果已提供 [onWillAccept]，则不得再提供此项。

### onAccept

```dart
DragTargetAccept<T>? onAccept
```

当一个可接受的数据被放到此拖拽目标上时调用。如果 `data` 为 `null`，则不会调用。

与 [onAcceptWithDetails] 等效，但仅包含数据本身。

### onAcceptWithDetails

```dart
DragTargetAcceptWithDetails<T>? onAcceptWithDetails
```

当一个可接受的数据被放到此拖拽目标上时调用。如果 `data` 为 `null`，则不会调用。

与 [onAccept] 等效，但会在 [DragTargetDetails](https://www.yuque.com/thyname/flutter.widgets/dragtargetdetails) 中提供包括数据在内的更多信息。

### onLeave

```dart
DragTargetLeave<T>? onLeave
```

当被拖到此目标上方的给定数据离开目标时调用。

### onMove

```dart
DragTargetMove<T>? onMove
```

当 [Draggable](https://www.yuque.com/thyname/flutter.widgets/draggable) 在此 [DragTarget](https://www.yuque.com/thyname/flutter.widgets/dragtarget) 内移动时调用。如果 `data` 为 `null`，则不会调用。

这包括进入和离开目标的情况。

### hitTestBehavior

```dart
HitTestBehavior hitTestBehavior
```

命中测试期间的行为方式。

默认为 [HitTestBehavior.translucent]。
