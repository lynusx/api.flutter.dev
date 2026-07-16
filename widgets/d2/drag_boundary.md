# DragBoundaryDelegate

```dart
abstract class DragBoundaryDelegate<T> {}
```

用于定义一个边界（拖拽对象被限制在其中）算法的接口。

参见：

- [DragBoundary](https://www.yuque.com/thyname/flutter.widgets/dragboundary)，一个 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)，为其子孙组件提供 [DragBoundaryDelegate](https://www.yuque.com/thyname/flutter.widgets/dragboundarydelegate)。

`T` 是一个定义被拖拽形状的数据类。例如，当在边界内拖拽一个矩形时，`T` 应为 `Rect`。

### isWithinBoundary()

```dart
bool isWithinBoundary(T draggedObject)
```

返回指定的被拖拽对象是否在边界内。

### nearestPositionWithinBoundary()

```dart
T nearestPositionWithinBoundary(T draggedObject)
```

返回将给定的被拖拽对象以最短距离完全移动到边界内后的结果。

如果边界无法容纳被拖拽对象，则会抛出异常。

# DragBoundary

```dart
class DragBoundary extends InheritedWidget {}
```

为其子孙组件提供一个 [DragBoundaryDelegate](https://www.yuque.com/thyname/flutter.widgets/dragboundarydelegate)，其边界由此组件定义。

[forRectOf] 和 [forRectMaybeOf] 返回一个用于类型为 [Rect](https://www.yuque.com/thyname/dart.ui/rect) 的拖拽对象的委托（delegate）。

{@tool dartpad} 此示例演示了在一个绿色方框的边界内拖拽一个红色方框。

** 请参阅 examples/api/lib/widgets/gesture_detector/gesture_detector.3.dart 中的代码 ** {@end-tool}

### DragBoundary()

```dart
DragBoundary({required Widget child, dynamic key})
```

创建一个为其子孙组件提供边界的组件。

### forRectOf()

```dart
DragBoundaryDelegate<Rect> forRectOf(BuildContext context, {bool useGlobalPosition = true})
```

{@template flutter.widgets.DragBoundary.forRectOf} 从最近的祖先组件获取 [DragBoundary](https://www.yuque.com/thyname/flutter.widgets/dragboundary)，以得到其 [Rect](https://www.yuque.com/thyname/dart.ui/rect) 类型的 [DragBoundaryDelegate](https://www.yuque.com/thyname/flutter.widgets/dragboundarydelegate)。

[useGlobalPosition] 指定是否获取全局坐标系下的 [Rect](https://www.yuque.com/thyname/dart.ui/rect) 类型 [DragBoundaryDelegate](https://www.yuque.com/thyname/flutter.widgets/dragboundarydelegate)。若为 false，则使用边界的本地坐标系。默认为 true。{@endtemplate}

如果没有找到 [DragBoundary](https://www.yuque.com/thyname/flutter.widgets/dragboundary) 祖先组件，返回的委托将允许拖拽对象自由移动。

### forRectMaybeOf()

```dart
DragBoundaryDelegate<Rect>? forRectMaybeOf(BuildContext context, {bool useGlobalPosition = true})
```

{@macro flutter.widgets.DragBoundary.forRectOf}

如果没有找到祖先组件，返回 null。
