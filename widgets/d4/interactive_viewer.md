@docImport 'editable_text.dart'; @docImport 'scroll_view.dart'; @docImport 'table.dart';

# InteractiveViewerWidgetBuilder

```dart
typedef InteractiveViewerWidgetBuilder = Widget Function(BuildContext context, Quad viewport)
```

一种 Widget 构建器的签名，接收当前视口（viewport）的 [Quad]。

另请参阅：

- [InteractiveViewer.builder]：其 builder 就是此类型。
- [WidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/widgetbuilder)：与之类似，但不接收视口参数。

# InteractiveViewer

```dart
class InteractiveViewer extends StatefulWidget {}
```

一个使其 child 能够进行平移和缩放交互的组件。

{@youtube 560 315 https://www.youtube.com/watch?v=zrn7V3bMJvg}

用户可以通过拖动来平移或通过双指捏合来缩放，从而对 child 进行变换。

默认情况下，InteractiveViewer 会使用 [Clip.hardEdge] 对其 child 进行裁剪。要阻止此行为，可以考虑将 [clipBehavior] 设置为 [Clip.none]。当 [clipBehavior] 为 [Clip.none] 时，InteractiveViewer 可能会绘制到其原始屏幕区域之外，例如当 child 被放大而尺寸增加时。但是，它不会接收原始区域之外的手势。为避免出现 InteractiveViewer 无法接收手势的死区，请不要设置 [clipBehavior]，或者确保 InteractiveViewer 组件的尺寸就是需要具备交互性的区域尺寸。

另请参阅：

- [Flutter Gallery 变换演示](https://github.com/flutter/gallery/blob/main/lib/demos/reference/transformations_demo.dart)，其中包含 InteractiveViewer 的用法。
- [flutter-go 演示](https://github.com/justinmc/flutter-go)，其中包含针对所有屏幕尺寸和 child 尺寸都适用的 InteractiveViewer child 健壮定位方式。
- [Lazy Flutter 性能专场](https://www.youtube.com/watch?v=qax_nOpgz7E)，其中包含使用 InteractiveViewer 及其 builder 构造函数高效查看大规模 Widget 集合子集的用法。

{@tool dartpad} 此示例展示了一个可以平移和缩放的简单 Container。

** 请参阅 examples/api/lib/widgets/interactive_viewer/interactive_viewer.0.dart 中的代码 ** {@end-tool}

### InteractiveViewer()

```dart
InteractiveViewer({dynamic key, Clip clipBehavior = Clip.hardEdge, PanAxis panAxis = PanAxis.free, EdgeInsets boundaryMargin = EdgeInsets.zero, bool constrained = true, double maxScale = 2.5, double minScale = 0.8, double interactionEndFrictionCoefficient = _kDrag, GestureScaleEndCallback? onInteractionEnd, GestureScaleStartCallback? onInteractionStart, GestureScaleUpdateCallback? onInteractionUpdate, bool panEnabled = true, bool scaleEnabled = true, double scaleFactor = kDefaultMouseScrollToScaleFactor, TransformationController? transformationController, Alignment? alignment, bool trackpadScrollCausesScale = false, required Widget? child})
```

创建一个 InteractiveViewer。

### InteractiveViewer.builder()

```dart
InteractiveViewer.builder({dynamic key, Clip clipBehavior = Clip.hardEdge, PanAxis panAxis = PanAxis.free, EdgeInsets boundaryMargin = EdgeInsets.zero, double maxScale = 2.5, double minScale = 0.8, double interactionEndFrictionCoefficient = _kDrag, GestureScaleEndCallback? onInteractionEnd, GestureScaleStartCallback? onInteractionStart, GestureScaleUpdateCallback? onInteractionUpdate, bool panEnabled = true, bool scaleEnabled = true, double scaleFactor = 200.0, TransformationController? transformationController, Alignment? alignment, bool trackpadScrollCausesScale = false, required InteractiveViewerWidgetBuilder? builder})
```

为按需创建的 child 创建一个 InteractiveViewer。

可用于渲染随当前变换而变化的 child。

有关如何使用它来优化大型 child 的示例，请参阅 [builder] 属性文档。

### alignment

```dart
Alignment? alignment
```

child 原点相对于盒子尺寸的对齐方式。

### clipBehavior

```dart
Clip clipBehavior
```

如果设置为 [Clip.none]，child 可能会超出 InteractiveViewer 的尺寸范围，但在这些区域内不会接收手势。使用 [Clip.none] 时，请确保 InteractiveViewer 的尺寸符合预期。

默认为 [Clip.hardEdge]。

### panAxis

```dart
PanAxis panAxis
```

当设置为 [PanAxis.aligned] 时，平移仅允许沿水平轴或垂直轴进行，不允许对角平移。

当设置为 [PanAxis.vertical] 或 [PanAxis.horizontal] 时，平移仅允许沿指定轴进行。例如，如果设置为 [PanAxis.vertical]，则只允许在垂直轴上平移；如果设置为 [PanAxis.horizontal]，则只允许在水平轴上平移。

当设置为 [PanAxis.free] 时，允许沿任意方向自由平移。

默认为 [PanAxis.free]。

### boundaryMargin

```dart
EdgeInsets boundaryMargin
```

child 可见边界的外边距。

任何会导致视口能够看到边界之外内容的变换都会在边界处被停止。边界不会随场景的其余部分一起旋转，因此它们始终与视口对齐。

要生成完全没有边界的效果，请传入无穷大的 [EdgeInsets](https://www.yuque.com/thyname/flutter.painting/edgeinsets)，例如 `EdgeInsets.all(double.infinity)`。

任何一条边都不能为 NaN。

默认为 [EdgeInsets.zero]，即边界与 [child] 的尺寸和位置完全一致。

### builder

```dart
InteractiveViewerWidgetBuilder? builder
```

构建此 Widget 的 child。

通过 [InteractiveViewer.builder] 构造函数传入。否则必须直接传入 [child] 参数，此时该属性为 null。

{@tool dartpad} 此示例展示了如何使用 builder 创建一个 [Table](https://www.yuque.com/thyname/flutter.widgets/table)，其单元格内容仅在可见时才会被构建。构建和移除的单元格会被记录到控制台以作说明。

** 请参阅 examples/api/lib/widgets/interactive_viewer/interactive_viewer.builder.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [ListView.builder]：遵循类似的模式。

### child

```dart
Widget? child
```

由 InteractiveViewer 进行变换的子 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)。

如果使用 [InteractiveViewer.builder] 构造函数，则此属性为 null，否则为必需属性。

### constrained

```dart
bool constrained
```

是否对 child 应用 Widget 树中此位置处的常规尺寸约束。

如果设置为 false，则会为 child 提供无限约束。当 child 应该比 InteractiveViewer 更大时，这通常很有用。

例如，对于一个比视口更大但可以通过平移显示初始屏幕外部分的 child，必须将 [constrained] 设置为 false，以使其能够正确确定自身尺寸。如果 [constrained] 为 true 且 child 只能将自身尺寸设置为视口大小，那么初始位于视口之外的区域将无法接收用户交互事件。如果发现 child 的某些区域无法响应用户手势，请确保 [constrained] 为 false 且 child 的尺寸设置正确。

默认为 true。

{@tool dartpad} 此示例展示了如何创建一个可平移的表格。由于该表格比整个屏幕更大，因此需要将 [constrained] 设置为 false 才能使其以完整尺寸绘制。随后可以通过平移查看超出屏幕尺寸的表格部分。

** 请参阅 examples/api/lib/widgets/interactive_viewer/interactive_viewer.constrained.0.dart 中的代码 ** {@end-tool}

### panEnabled

```dart
bool panEnabled
```

如果为 false，则会阻止用户进行平移。

默认为 true。

另请参阅：

- [scaleEnabled]：与之类似，但针对缩放。

### scaleEnabled

```dart
bool scaleEnabled
```

如果为 false，则会阻止用户进行缩放。

默认为 true。

另请参阅：

- [panEnabled]：与之类似，但针对平移。

### trackpadScrollCausesScale

```dart
bool trackpadScrollCausesScale
```

{@macro flutter.gestures.scale.trackpadScrollCausesScale}

### scaleFactor

```dart
double scaleFactor
```

确定每次指针滚动所执行的缩放量。

默认为 [kDefaultMouseScrollToScaleFactor](https://www.yuque.com/thyname/flutter.gestures/kdefaultmousescrolltoscalefactor)。

将此值增大到默认值以上会使缩放感觉变慢，而减小该值会使缩放感觉变快。

缩放量的计算方式是 [PointerScrollEvent.scrollDelta] 与 [scaleFactor] 之比的指数函数。在 Flutter 引擎中，鼠标滚轮的 [PointerScrollEvent.scrollDelta] 被硬编码为每次滚动 20，而触控板滚动的量可以是任意值。

仅影响指针设备的滚动，不影响双指捏合缩放。

### maxScale

```dart
double maxScale
```

允许的最大缩放比例。

缩放比例将被限制在此值与 [minScale] 之间（包含边界值）。

默认为 2.5。

必须大于零且大于 [minScale]。

### minScale

```dart
double minScale
```

允许的最小缩放比例。

缩放比例将被限制在此值与 [maxScale] 之间（包含边界值）。

缩放比例还受 [boundaryMargin] 影响。如果某个缩放比例会导致视图超出边界，则不允许该缩放。默认情况下，boundaryMargin 为 EdgeInsets.zero，因此在大多数情况下，若不先增大 boundaryMargin，则不允许缩小到 1.0 以下。

默认为 0.8。

必须是大于零且小于 [maxScale] 的有限数值。

### interactionEndFrictionCoefficient

```dart
double interactionEndFrictionCoefficient
```

改变手势结束后的减速行为。

默认为 0.0000135。

必须是大于零的有限数值。

### onInteractionEnd

```dart
GestureScaleEndCallback? onInteractionEnd
```

当用户在此 Widget 上结束平移或缩放手势时调用。

在调用此方法时，[TransformationController](https://www.yuque.com/thyname/flutter.widgets/transformationcontroller) 已经更新完毕，以反映此次交互所引起的变化，尽管平移操作之后可能仍会触发惯性动画。

{@template flutter.widgets.InteractiveViewer.onInteractionEnd} 即使通过 [panEnabled] 或 [scaleEnabled] 禁用了交互，无论是触摸手势还是鼠标交互，此回调都会被调用。

包裹 InteractiveViewer 的 [GestureDetector](https://www.yuque.com/thyname/flutter.widgets/gesturedetector) 不会响应 [GestureDetector.onScaleStart]、[GestureDetector.onScaleUpdate] 和 [GestureDetector.onScaleEnd]。请使用 [onInteractionStart]、[onInteractionUpdate] 和 [onInteractionEnd] 来响应这些手势。{@endtemplate}

另请参阅：

- [onInteractionStart]：处理同一交互的开始阶段。
- [onInteractionUpdate]：处理同一交互的更新阶段。

### onInteractionStart

```dart
GestureScaleStartCallback? onInteractionStart
```

当用户在此 Widget 上开始平移或缩放手势时调用。

在调用此方法时，[TransformationController](https://www.yuque.com/thyname/flutter.widgets/transformationcontroller) 尚未因此次交互而发生变化。

{@macro flutter.widgets.InteractiveViewer.onInteractionEnd}

details 中提供的 `focalPoint` 和 `localFocalPoint` 坐标是常规的 Flutter 事件坐标，而不是 InteractiveViewer 的场景坐标。有关如何将这些坐标转换为相对于 child 的场景坐标，请参阅 [TransformationController.toScene]。

另请参阅：

- [onInteractionUpdate]：处理同一交互的更新阶段。
- [onInteractionEnd]：处理同一交互的结束阶段。

### onInteractionUpdate

```dart
GestureScaleUpdateCallback? onInteractionUpdate
```

当用户更新平移或缩放手势时调用。

在调用此方法时，如果此次交互导致了矩阵发生变化，[TransformationController](https://www.yuque.com/thyname/flutter.widgets/transformationcontroller) 已经更新完毕，以反映此次交互所引起的变化。

{@macro flutter.widgets.InteractiveViewer.onInteractionEnd}

details 中提供的 `focalPoint` 和 `localFocalPoint` 坐标是常规的 Flutter 事件坐标，而不是 InteractiveViewer 的场景坐标。有关如何将这些坐标转换为相对于 child 的场景坐标，请参阅 [TransformationController.toScene]。

另请参阅：

- [onInteractionStart]：处理同一交互的开始阶段。
- [onInteractionEnd]：处理同一交互的结束阶段。

### transformationController

```dart
TransformationController? transformationController
```

用于对 child 执行变换的 [TransformationController](https://www.yuque.com/thyname/flutter.widgets/transformationcontroller)。

每当 child 被变换时，[Matrix4] 值都会更新，并通知所有监听者。如果设置了该值，InteractiveViewer 会更新以匹配新值。

{@tool dartpad} 此示例展示了如何使用 transformationController 将变换动画返回到其起始位置。

** 请参阅 examples/api/lib/widgets/interactive_viewer/interactive_viewer.transformation_controller.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [ValueNotifier](https://www.yuque.com/thyname/flutter.foundation/valuenotifier)：TransformationController 的父类。
- [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller)：另一个类似模式的示例。

### getNearestPointOnLine()

```dart
Vector3 getNearestPointOnLine(Vector3 point, Vector3 l1, Vector3 l2)
```

返回给定线段上离给定点最近的点。

### getAxisAlignedBoundingBox()

```dart
Quad getAxisAlignedBoundingBox(Quad quad)
```

给定一个四边形（quad），返回其轴对齐包围盒。

### pointIsInside()

```dart
bool pointIsInside(Vector3 point, Quad quad)
```

如果该点位于由 Quad 给出的矩形内部（包含边界），则返回 true。算法来自 https://math.stackexchange.com/a/190373。

### getNearestPointInside()

```dart
Vector3 getNearestPointInside(Vector3 point, Quad quad)
```

获取给定 Quad 内部（包含边界）离给定 Vector3 最近的点。

### createState()

```dart
State<InteractiveViewer> createState()
```

# TransformationController

```dart
class TransformationController extends ValueNotifier<Matrix4> {}
```

对 [ValueNotifier](https://www.yuque.com/thyname/flutter.foundation/valuenotifier) 的一个简单包装，其值是表示某种变换的 [Matrix4]。

[value] 默认值为单位矩阵，对应于无变换状态。

另请参阅：

- [InteractiveViewer.transformationController]：有关如何在 InteractiveViewer 中使用 TransformationController 的详细文档。

### TransformationController()

```dart
TransformationController([Matrix4? value])
```

创建一个 [TransformationController](https://www.yuque.com/thyname/flutter.widgets/transformationcontroller) 实例。

[value] 默认值为单位矩阵，对应于无变换状态。

### toScene()

```dart
Offset toScene(Offset viewportPoint)
```

返回给定视口点对应的场景点。

视口点是相对于父级的，而场景点是相对于 child 的，与变换无关。使用视口点调用 toScene 本质上会返回在给定变换下、位于该视口点下方的场景坐标。

视口的变换是 child 变换的逆过程（即，将 child 向左移动等同于将视口向右移动）。

在确定父级上的某个事件发生在 child 上的什么位置时，此方法通常很有用。以下示例展示了如何确定在父级上的一次点击发生在 child 上的位置。

```dart
@override
Widget build(BuildContext context) {
  return GestureDetector(
    onTapUp: (TapUpDetails details) {
      _childWasTappedAt = _transformationController.toScene(
        details.localPosition,
      );
    },
    child: InteractiveViewer(
      transformationController: _transformationController,
      child: child,
    ),
  );
}
```

# PanAxis

```dart
enum PanAxis {}
```

此枚举用于指定用户拖动视口时 [InteractiveViewer](https://www.yuque.com/thyname/flutter.widgets/interactiveviewer) 的行为。

用户只能沿水平轴平移视口。

用户只能沿垂直轴平移视口。

用户可以沿水平轴和垂直轴平移视口，但不能沿对角线方向平移。

用户可以沿任意方向自由平移视口。
