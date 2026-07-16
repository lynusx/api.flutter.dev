# ScrollableWidgetBuilder

```dart
typedef ScrollableWidgetBuilder = Widget Function(BuildContext context, ScrollController scrollController)
```

一种方法的签名，该方法提供 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 和 [ScrollController](https://www.yuque.com/thyname/flutter.widgets/scrollcontroller)，用于构建一个可能溢出所在区域可拖拽 [Axis](https://www.yuque.com/thyname/flutter.painting/axis)（轴向）的组件。

当某个组件预期包含可滚动的子组件，且需要在同一手势中通过垂直手势同时触发滚动和其他行为时，会使用此 builder。

例如，[DraggableScrollableSheet](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablesheet) 的使用者应将 [scrollController] 应用于某个 [ScrollView](https://www.yuque.com/thyname/flutter.widgets/scrollview) 的子类，如 [SingleChildScrollView](https://www.yuque.com/thyname/flutter.widgets/singlechildscrollview)、[ListView](https://www.yuque.com/thyname/flutter.widgets/listview) 或 [GridView](https://www.yuque.com/thyname/flutter.widgets/gridview)，以使整个面板可拖拽。

# DraggableScrollableController

```dart
class DraggableScrollableController extends ChangeNotifier {}
```

控制一个 [DraggableScrollableSheet](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablesheet)。

DraggableScrollableController 通常作为成员变量存储在 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象中，并在每次 [State.build] 中重复使用。控制器一次只能用于控制一个面板。如果之前的面板已被释放（dispose），控制器可以与新的面板一起重新使用。

在控制器被传入 [DraggableScrollableSheet](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablesheet) 且该面板完成 initState 之前，无法使用该控制器的方法。

[DraggableScrollableController](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablecontroller) 是一个 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable)。当已附加的面板改变大小时，它会通知其监听器。当面板首次附加，或已附加面板的参数发生变化但不影响面板当前大小时，它不会通知监听器。当 [pixels] 发生变化但 [size] 未变化时（例如提供给已附加面板的约束发生变化时），它也不会触发。

### DraggableScrollableController()

```dart
DraggableScrollableController()
```

为 [DraggableScrollableSheet](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablesheet) 创建一个控制器。

### size

```dart
double get size
```

获取当前已附加面板的大小（占父容器高度的比例）。

### pixels

```dart
double get pixels
```

获取当前已附加面板的像素高度。

### sizeToPixels()

```dart
double sizeToPixels(double size)
```

将面板的大小（父容器高度的比例值）转换为像素值。

### isAttached

```dart
bool get isAttached
```

返回是否有任何 [DraggableScrollableController](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablecontroller) 对象已附加到 [DraggableScrollableSheet](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablesheet)。

如果此值为 false，则不得调用与 [ScrollPosition](https://www.yuque.com/thyname/flutter.widgets/scrollposition) 交互的成员，例如 [sizeToPixels]、[size]、[animateTo] 和 [jumpTo]。

### pixelsToSize()

```dart
double pixelsToSize(double pixels)
```

将面板的像素高度转换为大小（父容器高度的比例值）。

### animateTo()

```dart
Future<void> animateTo(double size, {required Duration duration, required Curve curve})
```

将已附加的面板从当前大小动画过渡到给定的 [size]（父容器高度的比例值）。

任何正在进行的面板动画都会被取消。如果面板内部的可滚动组件当前正在进行动画（例如响应用户的快速滑动），该动画也会被取消。

当用户尝试手动滚动、启动了其他活动，或面板达到其最大或最小大小时（例如，如果目标动画到 1，但面板最大大小为 .8，则动画会在达到 .8 时停止），动画将被中断。

duration 不能为零。若要在不产生动画的情况下直接跳转到某个值，请使用 [jumpTo]。

即使 [DraggableScrollableSheet.snap] 为 true，调用 [animateTo] 后面板也不会发生吸附。吸附仅在用户拖拽后发生。

在 widget 测试中调用 [animateTo] 时，`await` 返回的 [Future](https://www.yuque.com/thyname/dart.async/future) 可能会导致测试挂起并超时。此时应改用 [WidgetTester.pumpAndSettle]。

### jumpTo()

```dart
void jumpTo(double size)
```

将已附加的面板从当前大小直接跳转到给定的 [size]（父容器高度的比例值）。

如果 [size] 超出已附加面板的最小或最大大小范围，[jumpTo] 会将面板跳转到最接近的有效大小。

任何正在进行的面板动画都会被取消。如果面板内部的可滚动组件当前正在进行动画（例如响应用户的快速滑动），该动画也会被取消。

即使 [DraggableScrollableSheet.snap] 为 true，调用 [jumpTo] 后面板也不会发生吸附。吸附仅在用户拖拽后发生。

### reset()

```dart
void reset()
```

将已附加的面板重置为其初始大小（参见 [DraggableScrollableSheet.initialChildSize]）。

# DraggableScrollableSheet

```dart
class DraggableScrollableSheet extends StatefulWidget {}
```

一个用于 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 的容器，通过调整大小来响应拖拽手势，直到达到限制后开始滚动。

{@youtube 560 315 https://www.youtube.com/watch?v=Hgw819mL_78}

此组件可以沿垂直轴在 [minChildSize]（默认值为 `0.25`）和 [maxChildSize]（默认值为 `1.0`）之间拖动。这些大小是相对于父容器高度的百分比。

该组件负责在用户沿水平轴拖动时，协调 builder 返回的组件的大小调整与滚动。

该组件最初会以 initialChildSize（默认值为 `0.5`，即父容器高度的一半）显示。只要 builder 创建的组件使用了所提供的 [ScrollController](https://www.yuque.com/thyname/flutter.widgets/scrollcontroller)，拖拽就能在 minChildSize 与 maxChildSize（均为父容器高度的百分比）之间的范围内生效。如果 [ScrollableWidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/scrollablewidgetbuilder) 创建的组件未使用所提供的 [ScrollController](https://www.yuque.com/thyname/flutter.widgets/scrollcontroller)，面板将保持在 initialChildSize 大小不变。

默认情况下，该组件会保持在用户拖动到的任意大小。若要使组件在用户抬起手指时吸附到特定大小，请将 [snap] 设为 `true`。面板将在 [minChildSize] 与 [maxChildSize] 之间吸附。使用 [snapSizes] 可添加更多供面板吸附的大小。

吸附效果仅在用户拖拽时生效。通过 [DraggableScrollableController.animateTo] 或 [DraggableScrollableController.jumpTo] 以编程方式操作面板大小时，将忽略 [snap] 和 [snapSizes]。

默认情况下，该组件会将其未占用的区域扩展以填充父容器中的可用空间。如果不需要此行为——例如父组件希望根据面板所占空间来定位该面板——可以将 [expand] 属性设为 false。

{@tool dartpad}

这是一个示例组件，展示了一个包含 25 个 [ListTile](https://www.yuque.com/thyname/flutter.material/listtile) 的 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview)。它最初占据 [Scaffold](https://www.yuque.com/thyname/flutter.material/scaffold) 主体的一半，可以向上拖动到 scaffold 的全部高度，或向下拖动到 scaffold 高度的 25%。达到全部高度后，列表内容将向上或向下滚动，直到再次到达列表顶部，此时用户可将面板重新拖回。

在桌面和运行于桌面平台的 Web 上，默认禁用通过鼠标拖动来滚动的功能，以与其他桌面应用程序的自然行为保持一致。

此行为由 [ScrollBehavior](https://www.yuque.com/thyname/flutter.widgets/scrollbehavior) 决定，可以通过向 [ScrollBehavior.dragDevices] 添加 [PointerDeviceKind.mouse] 来更改。有关更多信息，请参阅 https://docs.flutter.dev/release/breaking-changes/default-scroll-behavior-drag

另外，此示例演示了如何为桌面应用程序添加拖拽手柄。

** 参见 examples/api/lib/widgets/draggable_scrollable_sheet/draggable_scrollable_sheet.0.dart 中的代码 ** {@end-tool}

### DraggableScrollableSheet()

```dart
DraggableScrollableSheet({dynamic key, double initialChildSize = 0.5, double minChildSize = 0.25, double maxChildSize = 1.0, bool expand = true, bool snap = false, List<double>? snapSizes, Duration? snapAnimationDuration, DraggableScrollableController? controller, bool shouldCloseOnMinExtent = true, required ScrollableWidgetBuilder builder})
```

创建一个可在单次手势中拖拽和滚动的组件。

### initialChildSize

```dart
double initialChildSize
```

显示该组件时使用的初始大小，为父容器高度的比例值。

如果自首次构建面板或自上次调用 [DraggableScrollableActuator.reset] 以来尚未对该面板进行过拖拽，则使用新的 [initialChildSize] 重新构建面板时，才会将面板移动到该新值。

默认值为 `0.5`。

### minChildSize

```dart
double minChildSize
```

显示该组件时使用的最小大小，为父容器高度的比例值。

默认值为 `0.25`。

### maxChildSize

```dart
double maxChildSize
```

显示该组件时使用的最大大小，为父容器高度的比例值。

默认值为 `1.0`。

### expand

```dart
bool expand
```

该组件是否应扩展以填充其父容器中的可用空间。

大多数情况下应设为 true。但是，如果父组件将根据其期望大小来定位此组件（例如 [Center](https://www.yuque.com/thyname/flutter.widgets/center)），则应将此值设为 false。

默认值为 true。

### snap

```dart
bool snap
```

当用户在拖拽过程中抬起手指时，该组件是否应在 [snapSizes] 之间吸附。

如果用户抬起手指时手指仍在移动，该组件将吸附到拖拽方向上的下一个吸附大小（参见 [snapSizes]）。如果手指是静止的，该组件将吸附到最近的吸附大小。

当通过调用 [DraggableScrollableController.animateTo] 或 [DraggableScrollableController.jumpTo] 以编程方式移动面板时，不会应用吸附。

在面板首次构建后或自上次调用 [DraggableScrollableActuator.reset] 以来尚未从 [initialChildSize] 拖离的前提下，重新构建面板并新启用 snap 将立即触发一次吸附。

### snapSizes

```dart
List<double>? snapSizes
```

该组件应吸附到的目标大小列表。

吸附大小是相对于父容器高度的比例值。它们必须按递增顺序排列，且介于 [minChildSize] 与 [maxChildSize] 之间。

[minChildSize] 和 [maxChildSize] 隐式包含在吸附大小中，无需在此处指定。例如，`snapSizes = [.5]` 将使面板在 [minChildSize]、`.5` 和 [maxChildSize] 之间吸附。

对 [snapSizes] 列表的任何修改，只有在包含此组件的 `build` 函数再次运行时才会生效。

在面板首次构建后或自上次调用 [DraggableScrollableActuator.reset] 以来尚未从 [initialChildSize] 拖离的前提下，使用经过修改或全新的列表重新构建将触发一次吸附。

### snapAnimationDuration

```dart
Duration? snapAnimationDuration
```

定义吸附动画的持续时间。

如果未设置，则动画持续时间等于到吸附目标的距离除以组件的移动速度。

### controller

```dart
DraggableScrollableController? controller
```

可用于以编程方式控制此面板的控制器。

### shouldCloseOnMinExtent

```dart
bool shouldCloseOnMinExtent
```

当面板被拖动（或快速滑动）到其最小大小时，是否应导致其父面板关闭。

此值会被设置到所发出的 [DraggableScrollableNotification](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablenotification) 上。具体是否正确读取和处理该值，由父类自行决定。

### builder

```dart
ScrollableWidgetBuilder builder
```

用于创建在此组件中显示的子组件的 builder，该子组件将使用所提供的 [ScrollController](https://www.yuque.com/thyname/flutter.widgets/scrollcontroller) 以支持内容的拖拽和滚动。

### createState()

```dart
State<DraggableScrollableSheet> createState()
```

# DraggableScrollableNotification

```dart
class DraggableScrollableNotification extends Notification with ViewportNotificationMixin {}
```

一种与 [DraggableScrollableSheet](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablesheet) 的范围（extent，即大小）和滚动偏移量（即子列表的位置）相关的 [Notification](https://www.yuque.com/thyname/flutter.widgets/notification)。

当面板大小发生变化时，[DraggableScrollableSheet](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablesheet) 组件会通知其祖先组件。当面板范围通过拖拽发生变化时，此通知会沿组件树向上冒泡，这意味着给定的 [NotificationListener](https://www.yuque.com/thyname/flutter.widgets/notificationlistener) 将接收到所有后代 [DraggableScrollableSheet](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablesheet) 组件发出的通知。若只关注最近的 [DraggableScrollableSheet](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablesheet) 后代发出的通知，请检查该通知的 [depth] 属性是否为零。

当 [NotificationListener](https://www.yuque.com/thyname/flutter.widgets/notificationlistener) 收到范围变化通知时，该监听器已经完成了构建和布局，因此此时再调用 [State.setState] 来调整构建或布局已为时过晚。基于范围变化通知调整构建或布局的任何尝试，都会导致布局滞后一帧，带来较差的用户体验。范围变化通知主要用于驱动动画。[Scaffold](https://www.yuque.com/thyname/flutter.material/scaffold) 组件会监听范围变化通知，并据此驱动 [FloatingActionButton](https://www.yuque.com/thyname/flutter.material/floatingactionbutton) 随面板上滑而产生的动画。

### DraggableScrollableNotification()

```dart
DraggableScrollableNotification({required double extent, required double minExtent, required double maxExtent, required double initialExtent, required BuildContext context, bool shouldCloseOnMinExtent = true})
```

创建一个通知，表示 [DraggableScrollableSheet](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablesheet) 的范围已发生变化。

所有参数均为必需。[minExtent] 必须 >= 0。[maxExtent] 必须 <= 1.0。[extent] 必须介于 [minExtent] 和 [maxExtent] 之间。

### extent

```dart
double extent
```

范围的当前值，介于 [minExtent] 和 [maxExtent] 之间。

### minExtent

```dart
double minExtent
```

[extent] 的最小值，>= 0。

### maxExtent

```dart
double maxExtent
```

[extent] 的最大值。

### initialExtent

```dart
double initialExtent
```

最初请求的 [extent] 值。

### context

```dart
BuildContext context
```

触发此通知的组件的构建上下文。

可用于查找面板的渲染对象，以确定视口的大小等信息。监听器只能在首次收到通知时认为此上下文是有效的。

### shouldCloseOnMinExtent

```dart
bool shouldCloseOnMinExtent
```

触发此通知的组件被拖动（或快速滑动）到最小范围时，是否应导致其父面板关闭。

具体是否正确读取和处理该值，由父类自行决定。

### debugFillDescription()

```dart
void debugFillDescription(List<String> description)
```

# DraggableScrollableActuator

```dart
class DraggableScrollableActuator extends StatefulWidget {}
```

一个可以通知后代 [DraggableScrollableSheet](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablesheet) 将其位置重置为初始状态的组件。

[Scaffold](https://www.yuque.com/thyname/flutter.material/scaffold) 使用此组件来通知持久化的底部面板：当该面板开始覆盖比其初始位置更多的主体内容，且用户点击了返回按钮时，应将其重置。这对于使用辅助技术的用户尤为重要，因为对他们来说拖拽操作可能较难传达。

这只是对 [DraggableScrollableController](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablecontroller) 的一层封装。它主要适用于控制当前代码无法控制的组件树的某一部分中的面板（例如库代码尝试影响库使用者代码中的面板）。通常，直接创建一个控制器并将其传递给面板的构造函数（参见 [DraggableScrollableSheet.controller]）会更容易实现控制。

### DraggableScrollableActuator()

```dart
DraggableScrollableActuator({dynamic key, required Widget child})
```

创建一个可以通知后代 [DraggableScrollableSheet](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablesheet) 重置到其初始位置的组件。

[child] 参数为必需项。

### child

```dart
Widget child
```

当对包含此组件的上下文应用 [reset] 方法时，此 child 的 [DraggableScrollableSheet](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablesheet) 后代将被重置。

### reset()

```dart
bool reset(BuildContext context)
```

通知任何后代 [DraggableScrollableSheet](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablesheet) 应将其重置为初始位置。

如果存在可用的 [DraggableScrollableActuator](https://www.yuque.com/thyname/flutter.widgets/draggablescrollableactuator)，且有某个 [DraggableScrollableSheet](https://www.yuque.com/thyname/flutter.widgets/draggablescrollablesheet) 正在监听更新，则返回 `true`，否则返回 `false`。
