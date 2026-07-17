@docImport 'package:flutter/material.dart';

@docImport 'container.dart'; @docImport 'scrollable.dart';

# GestureRecognizerFactory

```dart
abstract class GestureRecognizerFactory<T extends GestureRecognizer> {}
```

用于创建手势识别器的工厂。

`T` 是此类所管理的手势识别器的类型。

由 [RawGestureDetector.gestures] 使用。

### GestureRecognizerFactory()

```dart
GestureRecognizerFactory()
```

抽象的 const 构造函数。此构造函数使子类能够提供 const 构造函数，从而可在 const 表达式中使用。

### constructor()

```dart
T constructor()
```

必须返回一个 T 的实例。

### initializer()

```dart
void initializer(T instance)
```

必须配置给定的实例（该实例由 `constructor` 创建）。

这通常意味着设置回调。

# GestureRecognizerFactoryConstructor

```dart
typedef GestureRecognizerFactoryConstructor<T extends GestureRecognizer> = T Function()
```

用于实现 [GestureRecognizerFactory.constructor] 的闭包的签名。

# GestureRecognizerFactoryInitializer

```dart
typedef GestureRecognizerFactoryInitializer<T extends GestureRecognizer> = void Function(T instance)
```

用于实现 [GestureRecognizerFactory.initializer] 的闭包的签名。

# GestureRecognizerFactoryWithHandlers

```dart
class GestureRecognizerFactoryWithHandlers<T extends GestureRecognizer> extends GestureRecognizerFactory<T> {}
```

用于创建委托给回调函数的手势识别器的工厂。

由 [RawGestureDetector.gestures] 使用。

### GestureRecognizerFactoryWithHandlers()

```dart
GestureRecognizerFactoryWithHandlers(GestureRecognizerFactoryConstructor<T> _constructor, GestureRecognizerFactoryInitializer<T> _initializer)
```

使用给定的回调创建一个手势识别器工厂。

### constructor()

```dart
T constructor()
```

### initializer()

```dart
void initializer(T instance)
```

# GestureDetector

```dart
class GestureDetector extends StatelessWidget {}
```

用于检测手势的 widget。

尝试识别与其非 null 回调相对应的手势。

如果此 widget 有子 widget，其尺寸行为将由该子 widget 决定。如果没有子 widget，则会扩展以填满父级。

{@youtube 560 315 https://www.youtube.com/watch?v=WhVXkCFPmK4}

默认情况下，带有不可见子 widget 的 GestureDetector 会忽略触摸；可以通过 [behavior] 控制此行为。

GestureDetector 还会监听无障碍事件，并将其映射到相应的回调。若要忽略无障碍事件，请将 [excludeFromSemantics] 设置为 true。

更多信息参见 <http://flutter.dev/to/gestures>。

Material Design 应用通常会以水波纹效果响应触摸。[InkWell](https://www.yuque.com/thyname/flutter.material/inkwell) 类实现了这种效果，可用于替代 [GestureDetector](https://www.yuque.com/thyname/flutter.widgets/gesturedetector) 来处理点击。

{@tool dartpad} 此示例包含一个被包装在 [GestureDetector](https://www.yuque.com/thyname/flutter.widgets/gesturedetector) 中的黑色灯泡。点击“TURN LIGHT ON”按钮时，通过设置 `_lights` 字段将灯泡变为黄色；再次点击“TURN LIGHT OFF”时则恢复原状。

** See code in examples/api/lib/widgets/gesture_detector/gesture_detector.0.dart ** {@end-tool}

{@tool dartpad} 此示例使用了一个包装 [GestureDetector](https://www.yuque.com/thyname/flutter.widgets/gesturedetector) widget 的 [Container](https://www.yuque.com/thyname/flutter.widgets/container)，该 [GestureDetector](https://www.yuque.com/thyname/flutter.widgets/gesturedetector) 用于检测点击。

由于 [GestureDetector](https://www.yuque.com/thyname/flutter.widgets/gesturedetector) 没有子 widget，它会呈现其父级的尺寸，从而使周围 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 的整个区域都可点击。点击时，通过设置 `_color` 字段使 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 变为黄色。再次点击时，会恢复为白色。

** See code in examples/api/lib/widgets/gesture_detector/gesture_detector.1.dart ** {@end-tool}

### 疑难解答

为什么父级的 [GestureDetector.onTap] 方法没有被调用？

假设有一个定义了 onTap 回调的父级 [GestureDetector](https://www.yuque.com/thyname/flutter.widgets/gesturedetector)，以及一个同样定义了 onTap 回调的子 GestureDetector，当点击内部的 GestureDetector 时，两个 GestureDetector 都会向手势竞技场（gesture arena）发送一个 [GestureRecognizer](https://www.yuque.com/thyname/flutter.gestures/gesturerecognizer)。这是因为指针坐标同时位于两个 GestureDetector 的边界内。在这种情况下，子 GestureDetector 获胜，因为它是第一个进入竞技场的。子 widget 的 onTap 会被调用，而父级的则不会，因为该手势已被消费。有关手势消歧的更多信息，请参见：[手势消歧](https://flutter.dev/to/gesture-disambiguation)。

将 [GestureDetector.behavior] 设置为 [HitTestBehavior.opaque] 或 [HitTestBehavior.translucent] 对父子关系没有影响：两个 GestureDetector 都会向手势竞技场发送一个 GestureRecognizer，但只有一个会获胜。

某些回调（例如 onTapDown）可能会在某个识别器赢得竞技场之前触发，而另一些回调（例如 onTapCancel）即使在识别器竞技失败时也会触发。因此，在上述示例中，父级检测器仍可能调用其部分回调，即使它在竞技场中落败。

{@tool dartpad} 此示例使用一个 [GestureDetector](https://www.yuque.com/thyname/flutter.widgets/gesturedetector) 包装了一个绿色的 [Container](https://www.yuque.com/thyname/flutter.widgets/container)，其中又包含另一个包装黄色 Container 的 GestureDetector。第二个 GestureDetector 是绿色 Container 的子 widget。两个 GestureDetector 都定义了 onTap 回调。回调被调用时，会为对应的 Container 添加红色边框。

当点击绿色 Container 时，其父级 GestureDetector 会进入手势竞技场。由于没有与之竞争的 GestureDetector，它会获胜，绿色 Container 随即显示红色边框。当点击黄色 Container 时，其父级 GestureDetector 会进入手势竞技场，而包装绿色 Container 的 GestureDetector 也会进入竞技场（因为指针事件坐标同时位于两个 GestureDetector 的边界内）。包装黄色 Container 的 GestureDetector 会获胜，因为它是第一个进入竞技场的检测器。

此示例将 [debugPrintGestureArenaDiagnostics](https://www.yuque.com/thyname/flutter.gestures/debugprintgesturearenadiagnostics) 设置为 true。此标志会打印有关手势竞技场的有用信息。

将 [GestureDetector.behavior] 属性更改为 [HitTestBehavior.translucent] 或 [HitTestBehavior.opaque] 不会产生影响：两个 GestureDetector 都会向手势竞技场发送一个 [GestureRecognizer](https://www.yuque.com/thyname/flutter.gestures/gesturerecognizer)，但只有一个会获胜。

** See code in examples/api/lib/widgets/gesture_detector/gesture_detector.2.dart ** {@end-tool}

## 调试

出于调试目的，若要查看 [GestureDetector](https://www.yuque.com/thyname/flutter.widgets/gesturedetector) 的命中测试范围大小，请将 [debugPaintPointersEnabled](https://www.yuque.com/thyname/flutter.rendering/debugpaintpointersenabled) 设置为 true。

另请参阅：

- [Listener](https://www.yuque.com/thyname/flutter.widgets/listener)，用于监听底层原始指针事件的 widget。
- [MouseRegion](https://www.yuque.com/thyname/flutter.widgets/mouseregion)，即使未按下任何按钮也能跟踪鼠标移动的 widget。
- [RawGestureDetector](https://www.yuque.com/thyname/flutter.widgets/rawgesturedetector)，用于检测自定义手势的 widget。

### GestureDetector()

```dart
GestureDetector({dynamic key, Widget? child, GestureTapDownCallback? onTapDown, GestureTapUpCallback? onTapUp, GestureTapCallback? onTap, GestureTapMoveCallback? onTapMove, GestureTapCancelCallback? onTapCancel, GestureTapCallback? onSecondaryTap, GestureTapDownCallback? onSecondaryTapDown, GestureTapUpCallback? onSecondaryTapUp, GestureTapCancelCallback? onSecondaryTapCancel, GestureTapDownCallback? onTertiaryTapDown, GestureTapUpCallback? onTertiaryTapUp, GestureTapCancelCallback? onTertiaryTapCancel, GestureTapDownCallback? onDoubleTapDown, GestureTapCallback? onDoubleTap, GestureTapCancelCallback? onDoubleTapCancel, GestureLongPressDownCallback? onLongPressDown, GestureLongPressCancelCallback? onLongPressCancel, GestureLongPressCallback? onLongPress, GestureLongPressStartCallback? onLongPressStart, GestureLongPressMoveUpdateCallback? onLongPressMoveUpdate, GestureLongPressUpCallback? onLongPressUp, GestureLongPressEndCallback? onLongPressEnd, GestureLongPressDownCallback? onSecondaryLongPressDown, GestureLongPressCancelCallback? onSecondaryLongPressCancel, GestureLongPressCallback? onSecondaryLongPress, GestureLongPressStartCallback? onSecondaryLongPressStart, GestureLongPressMoveUpdateCallback? onSecondaryLongPressMoveUpdate, GestureLongPressUpCallback? onSecondaryLongPressUp, GestureLongPressEndCallback? onSecondaryLongPressEnd, GestureLongPressDownCallback? onTertiaryLongPressDown, GestureLongPressCancelCallback? onTertiaryLongPressCancel, GestureLongPressCallback? onTertiaryLongPress, GestureLongPressStartCallback? onTertiaryLongPressStart, GestureLongPressMoveUpdateCallback? onTertiaryLongPressMoveUpdate, GestureLongPressUpCallback? onTertiaryLongPressUp, GestureLongPressEndCallback? onTertiaryLongPressEnd, GestureDragDownCallback? onVerticalDragDown, GestureDragStartCallback? onVerticalDragStart, GestureDragUpdateCallback? onVerticalDragUpdate, GestureDragEndCallback? onVerticalDragEnd, GestureDragCancelCallback? onVerticalDragCancel, GestureDragDownCallback? onHorizontalDragDown, GestureDragStartCallback? onHorizontalDragStart, GestureDragUpdateCallback? onHorizontalDragUpdate, GestureDragEndCallback? onHorizontalDragEnd, GestureDragCancelCallback? onHorizontalDragCancel, GestureForcePressStartCallback? onForcePressStart, GestureForcePressPeakCallback? onForcePressPeak, GestureForcePressUpdateCallback? onForcePressUpdate, GestureForcePressEndCallback? onForcePressEnd, GestureDragDownCallback? onPanDown, GestureDragStartCallback? onPanStart, GestureDragUpdateCallback? onPanUpdate, GestureDragEndCallback? onPanEnd, GestureDragCancelCallback? onPanCancel, GestureScaleStartCallback? onScaleStart, GestureScaleUpdateCallback? onScaleUpdate, GestureScaleEndCallback? onScaleEnd, HitTestBehavior? behavior, bool excludeFromSemantics = false, DragStartBehavior dragStartBehavior = DragStartBehavior.start, bool trackpadScrollCausesScale = false, Offset trackpadScrollToScaleFactor = kDefaultTrackpadScrollToScaleFactor, Set<PointerDeviceKind>? supportedDevices})
```

创建一个用于检测手势的 widget。

由于缩放（scale）是平移（pan）的超集，平移和缩放回调不能同时使用。请改用缩放回调。

由于水平和垂直拖动的组合即为平移，水平和垂直拖动回调不能同时使用。请改用平移回调。

{@youtube 560 315 https://www.youtube.com/watch?v=WhVXkCFPmK4}

默认情况下，手势检测器会为 widget 树贡献语义信息，供辅助技术使用。

### child

```dart
Widget? child
```

此 widget 下方的 widget 树。

{@macro flutter.widgets.ProxyWidget.child}

### onTapDown

```dart
GestureTapDownCallback? onTapDown
```

一个可能引发主按钮点击的指针已在屏幕上的某个特定位置接触。

此回调会在一小段超时后被调用，即使获胜的手势尚未确定。如果点击手势获胜，将调用 [onTapUp]；否则将调用 [onTapCancel]。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onTapUp

```dart
GestureTapUpCallback? onTapUp
```

一个将触发主按钮点击的指针已在屏幕上的某个特定位置停止接触。

如果点击手势获胜，此回调会在 [onTap] 之前立即触发。如果点击手势未获胜，则会改为调用 [onTapCancel]。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onTap

```dart
GestureTapCallback? onTap
```

已发生一次主按钮点击。

当点击手势获胜时触发。如果点击手势未获胜，则会改为调用 [onTapCancel]。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。
- [onTapUp]，与此同时触发，但包含有关指针位置的详细信息。

### onTapMove

```dart
GestureTapMoveCallback? onTapMove
```

触发了点击的指针发生了移动。

当点击手势被识别后指针发生移动时触发。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onTapCancel

```dart
GestureTapCancelCallback? onTapCancel
```

先前触发 [onTapDown] 的指针最终不会导致点击。

如果点击手势未获胜，此回调会在 [onTapDown] 之后被调用，以代替 [onTapUp] 和 [onTap]。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onSecondaryTap

```dart
GestureTapCallback? onSecondaryTap
```

已发生一次次要按钮点击。

当点击手势获胜时触发。如果点击手势未获胜，则会改为调用 [onSecondaryTapCancel]。

另请参阅：

- [kSecondaryButton](https://www.yuque.com/thyname/flutter.gestures/ksecondarybutton)，此回调所响应的按钮。
- [onSecondaryTapUp]，与此同时触发，但包含有关指针位置的详细信息。

### onSecondaryTapDown

```dart
GestureTapDownCallback? onSecondaryTapDown
```

一个可能引发次要按钮点击的指针已在屏幕上的某个特定位置接触。

此回调会在一小段超时后被调用，即使获胜的手势尚未确定。如果点击手势获胜，将调用 [onSecondaryTapUp]；否则将调用 [onSecondaryTapCancel]。

另请参阅：

- [kSecondaryButton](https://www.yuque.com/thyname/flutter.gestures/ksecondarybutton)，此回调所响应的按钮。

### onSecondaryTapUp

```dart
GestureTapUpCallback? onSecondaryTapUp
```

一个将触发次要按钮点击的指针已在屏幕上的某个特定位置停止接触。

如果点击手势获胜，此回调会触发。如果点击手势未获胜，则会改为调用 [onSecondaryTapCancel]。

另请参阅：

- [onSecondaryTap]，紧随此回调之后触发的处理程序，不传递有关点击的任何详细信息。
- [kSecondaryButton](https://www.yuque.com/thyname/flutter.gestures/ksecondarybutton)，此回调所响应的按钮。

### onSecondaryTapCancel

```dart
GestureTapCancelCallback? onSecondaryTapCancel
```

先前触发 [onSecondaryTapDown] 的指针最终不会导致点击。

如果点击手势未获胜，此回调会在 [onSecondaryTapDown] 之后被调用，以代替 [onSecondaryTapUp]。

另请参阅：

- [kSecondaryButton](https://www.yuque.com/thyname/flutter.gestures/ksecondarybutton)，此回调所响应的按钮。

### onTertiaryTapDown

```dart
GestureTapDownCallback? onTertiaryTapDown
```

一个可能引发第三按钮点击的指针已在屏幕上的某个特定位置接触。

此回调会在一小段超时后被调用，即使获胜的手势尚未确定。如果点击手势获胜，将调用 [onTertiaryTapUp]；否则将调用 [onTertiaryTapCancel]。

另请参阅：

- [kTertiaryButton](https://www.yuque.com/thyname/flutter.gestures/ktertiarybutton)，此回调所响应的按钮。

### onTertiaryTapUp

```dart
GestureTapUpCallback? onTertiaryTapUp
```

一个将触发第三按钮点击的指针已在屏幕上的某个特定位置停止接触。

如果点击手势获胜，此回调会触发。如果点击手势未获胜，则会改为调用 [onTertiaryTapCancel]。

另请参阅：

- [kTertiaryButton](https://www.yuque.com/thyname/flutter.gestures/ktertiarybutton)，此回调所响应的按钮。

### onTertiaryTapCancel

```dart
GestureTapCancelCallback? onTertiaryTapCancel
```

先前触发 [onTertiaryTapDown] 的指针最终不会导致点击。

如果点击手势未获胜，此回调会在 [onTertiaryTapDown] 之后被调用，以代替 [onTertiaryTapUp]。

另请参阅：

- [kTertiaryButton](https://www.yuque.com/thyname/flutter.gestures/ktertiarybutton)，此回调所响应的按钮。

### onDoubleTapDown

```dart
GestureTapDownCallback? onDoubleTapDown
```

一个可能引发双击的指针已在屏幕上的某个特定位置接触。

在第二次点击的按下事件后立即触发。

如果用户完成了双击且该手势获胜，此回调之后会调用 [onDoubleTap]；否则之后会调用 [onDoubleTapCancel]。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onDoubleTap

```dart
GestureTapCallback? onDoubleTap
```

用户在同一位置以主按钮快速连续点击了两次屏幕。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onDoubleTapCancel

```dart
GestureTapCancelCallback? onDoubleTapCancel
```

先前触发 [onDoubleTapDown] 的指针最终不会导致双击。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onLongPressDown

```dart
GestureLongPressDownCallback? onLongPressDown
```

指针已以主按钮接触屏幕，这可能是长按的开始。

在指针按下事件之后触发。

如果用户完成了长按且此手势获胜，此回调之后会调用 [onLongPressStart]；否则之后会调用 [onLongPressCancel]。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。
- [onSecondaryLongPressDown]，用于次要按钮的类似回调。
- [onTertiaryLongPressDown]，用于第三按钮的类似回调。
- [LongPressGestureRecognizer.onLongPressDown]，在手势层公开此回调。

### onLongPressCancel

```dart
GestureLongPressCancelCallback? onLongPressCancel
```

先前触发 [onLongPressDown] 的指针最终不会导致长按。

如果先前已触发 [onLongPressDown]，此回调会在该手势失败时触发。

如果用户完成了长按且该手势获胜，则会改为调用 [onLongPressStart] 和 [onLongPress]。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onLongPressCancel]，在手势层公开此回调。

### onLongPress

```dart
GestureLongPressCallback? onLongPress
```

当识别出以主按钮进行的长按手势时调用。

当指针在屏幕上同一位置保持接触较长时间时触发。

这等同于（并在其之后立即调用）[onLongPressStart]。两者的唯一区别在于，此回调不包含指针最初接触屏幕时的位置详情。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onLongPress]，在手势层公开此回调。

### onLongPressStart

```dart
GestureLongPressStartCallback? onLongPressStart
```

当识别出以主按钮进行的长按手势时调用。

当指针在屏幕上同一位置保持接触较长时间时触发。

这等同于（并在其之前立即调用）[onLongPress]。两者的唯一区别在于，此回调包含指针最初接触屏幕时的位置详情，而 [onLongPress] 则不包含。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onLongPressStart]，在手势层公开此回调。

### onLongPressMoveUpdate

```dart
GestureLongPressMoveUpdateCallback? onLongPressMoveUpdate
```

以主按钮长按后，指针被拖动移动。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onLongPressMoveUpdate]，在手势层公开此回调。

### onLongPressUp

```dart
GestureLongPressUpCallback? onLongPressUp
```

触发以主按钮长按的指针已停止接触屏幕。

这等同于（并在其之后立即调用）[onLongPressEnd]。两者的唯一区别在于，此回调不包含指针停止接触屏幕时的状态详情。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onLongPressUp]，在手势层公开此回调。

### onLongPressEnd

```dart
GestureLongPressEndCallback? onLongPressEnd
```

触发以主按钮长按的指针已停止接触屏幕。

这等同于（并在其之前立即调用）[onLongPressUp]。两者的唯一区别在于，此回调包含指针停止接触屏幕时的状态详情，而 [onLongPressUp] 则不包含。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onLongPressEnd]，在手势层公开此回调。

### onSecondaryLongPressDown

```dart
GestureLongPressDownCallback? onSecondaryLongPressDown
```

指针已以次要按钮接触屏幕，这可能是长按的开始。

在指针按下事件之后触发。

如果用户完成了长按且此手势获胜，此回调之后会调用 [onSecondaryLongPressStart]；否则之后会调用 [onSecondaryLongPressCancel]。

另请参阅：

- [kSecondaryButton](https://www.yuque.com/thyname/flutter.gestures/ksecondarybutton)，此回调所响应的按钮。
- [onLongPressDown]，用于主按钮的类似回调。
- [onTertiaryLongPressDown]，用于第三按钮的类似回调。
- [LongPressGestureRecognizer.onSecondaryLongPressDown]，在手势层公开此回调。

### onSecondaryLongPressCancel

```dart
GestureLongPressCancelCallback? onSecondaryLongPressCancel
```

先前触发 [onSecondaryLongPressDown] 的指针最终不会导致长按。

如果先前已触发 [onSecondaryLongPressDown]，此回调会在该手势失败时触发。

如果用户完成了长按且该手势获胜，则会改为调用 [onSecondaryLongPressStart] 和 [onSecondaryLongPress]。

另请参阅：

- [kSecondaryButton](https://www.yuque.com/thyname/flutter.gestures/ksecondarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onSecondaryLongPressCancel]，在手势层公开此回调。

### onSecondaryLongPress

```dart
GestureLongPressCallback? onSecondaryLongPress
```

当识别出以次要按钮进行的长按手势时调用。

当指针在屏幕上同一位置保持接触较长时间时触发。

这等同于（并在其之后立即调用）[onSecondaryLongPressStart]。两者的唯一区别在于，此回调不包含指针最初接触屏幕时的位置详情。

另请参阅：

- [kSecondaryButton](https://www.yuque.com/thyname/flutter.gestures/ksecondarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onSecondaryLongPress]，在手势层公开此回调。

### onSecondaryLongPressStart

```dart
GestureLongPressStartCallback? onSecondaryLongPressStart
```

当识别出以次要按钮进行的长按手势时调用。

当指针在屏幕上同一位置保持接触较长时间时触发。

这等同于（并在其之前立即调用）[onSecondaryLongPress]。两者的唯一区别在于，此回调包含指针最初接触屏幕时的位置详情，而 [onSecondaryLongPress] 则不包含。

另请参阅：

- [kSecondaryButton](https://www.yuque.com/thyname/flutter.gestures/ksecondarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onSecondaryLongPressStart]，在手势层公开此回调。

### onSecondaryLongPressMoveUpdate

```dart
GestureLongPressMoveUpdateCallback? onSecondaryLongPressMoveUpdate
```

以次要按钮长按后，指针被拖动移动。

另请参阅：

- [kSecondaryButton](https://www.yuque.com/thyname/flutter.gestures/ksecondarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onSecondaryLongPressMoveUpdate]，在手势层公开此回调。

### onSecondaryLongPressUp

```dart
GestureLongPressUpCallback? onSecondaryLongPressUp
```

触发以次要按钮长按的指针已停止接触屏幕。

这等同于（并在其之后立即调用）[onSecondaryLongPressEnd]。两者的唯一区别在于，此回调不包含指针停止接触屏幕时的状态详情。

另请参阅：

- [kSecondaryButton](https://www.yuque.com/thyname/flutter.gestures/ksecondarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onSecondaryLongPressUp]，在手势层公开此回调。

### onSecondaryLongPressEnd

```dart
GestureLongPressEndCallback? onSecondaryLongPressEnd
```

触发以次要按钮长按的指针已停止接触屏幕。

这等同于（并在其之前立即调用）[onSecondaryLongPressUp]。两者的唯一区别在于，此回调包含指针停止接触屏幕时的状态详情，而 [onSecondaryLongPressUp] 则不包含。

另请参阅：

- [kSecondaryButton](https://www.yuque.com/thyname/flutter.gestures/ksecondarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onSecondaryLongPressEnd]，在手势层公开此回调。

### onTertiaryLongPressDown

```dart
GestureLongPressDownCallback? onTertiaryLongPressDown
```

指针已以第三按钮接触屏幕，这可能是长按的开始。

在指针按下事件之后触发。

如果用户完成了长按且此手势获胜，此回调之后会调用 [onTertiaryLongPressStart]；否则之后会调用 [onTertiaryLongPressCancel]。

另请参阅：

- [kTertiaryButton](https://www.yuque.com/thyname/flutter.gestures/ktertiarybutton)，此回调所响应的按钮。
- [onLongPressDown]，用于主按钮的类似回调。
- [onSecondaryLongPressDown]，用于次要按钮的类似回调。
- [LongPressGestureRecognizer.onTertiaryLongPressDown]，在手势层公开此回调。

### onTertiaryLongPressCancel

```dart
GestureLongPressCancelCallback? onTertiaryLongPressCancel
```

先前触发 [onTertiaryLongPressDown] 的指针最终不会导致长按。

如果先前已触发 [onTertiaryLongPressDown]，此回调会在该手势失败时触发。

如果用户完成了长按且该手势获胜，则会改为调用 [onTertiaryLongPressStart] 和 [onTertiaryLongPress]。

另请参阅：

- [kTertiaryButton](https://www.yuque.com/thyname/flutter.gestures/ktertiarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onTertiaryLongPressCancel]，在手势层公开此回调。

### onTertiaryLongPress

```dart
GestureLongPressCallback? onTertiaryLongPress
```

当识别出以第三按钮进行的长按手势时调用。

当指针在屏幕上同一位置保持接触较长时间时触发。

这等同于（并在其之后立即调用）[onTertiaryLongPressStart]。两者的唯一区别在于，此回调不包含指针最初接触屏幕时的位置详情。

另请参阅：

- [kTertiaryButton](https://www.yuque.com/thyname/flutter.gestures/ktertiarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onTertiaryLongPress]，在手势层公开此回调。

### onTertiaryLongPressStart

```dart
GestureLongPressStartCallback? onTertiaryLongPressStart
```

当识别出以第三按钮进行的长按手势时调用。

当指针在屏幕上同一位置保持接触较长时间时触发。

这等同于（并在其之前立即调用）[onTertiaryLongPress]。两者的唯一区别在于，此回调包含指针最初接触屏幕时的位置详情，而 [onTertiaryLongPress] 则不包含。

另请参阅：

- [kTertiaryButton](https://www.yuque.com/thyname/flutter.gestures/ktertiarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onTertiaryLongPressStart]，在手势层公开此回调。

### onTertiaryLongPressMoveUpdate

```dart
GestureLongPressMoveUpdateCallback? onTertiaryLongPressMoveUpdate
```

以第三按钮长按后，指针被拖动移动。

另请参阅：

- [kTertiaryButton](https://www.yuque.com/thyname/flutter.gestures/ktertiarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onTertiaryLongPressMoveUpdate]，在手势层公开此回调。

### onTertiaryLongPressUp

```dart
GestureLongPressUpCallback? onTertiaryLongPressUp
```

触发以第三按钮长按的指针已停止接触屏幕。

这等同于（并在其之后立即调用）[onTertiaryLongPressEnd]。两者的唯一区别在于，此回调不包含指针停止接触屏幕时的状态详情。

另请参阅：

- [kTertiaryButton](https://www.yuque.com/thyname/flutter.gestures/ktertiarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onTertiaryLongPressUp]，在手势层公开此回调。

### onTertiaryLongPressEnd

```dart
GestureLongPressEndCallback? onTertiaryLongPressEnd
```

触发以第三按钮长按的指针已停止接触屏幕。

这等同于（并在其之前立即调用）[onTertiaryLongPressUp]。两者的唯一区别在于，此回调包含指针停止接触屏幕时的状态详情，而 [onTertiaryLongPressUp] 则不包含。

另请参阅：

- [kTertiaryButton](https://www.yuque.com/thyname/flutter.gestures/ktertiarybutton)，此回调所响应的按钮。
- [LongPressGestureRecognizer.onTertiaryLongPressEnd]，在手势层公开此回调。

### onVerticalDragDown

```dart
GestureDragDownCallback? onVerticalDragDown
```

指针已以主按钮接触屏幕，可能即将开始垂直移动。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onVerticalDragStart

```dart
GestureDragStartCallback? onVerticalDragStart
```

指针已以主按钮接触屏幕，并已开始垂直移动。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onVerticalDragUpdate

```dart
GestureDragUpdateCallback? onVerticalDragUpdate
```

以主按钮接触屏幕并进行垂直移动的指针，在垂直方向上又发生了移动。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onVerticalDragEnd

```dart
GestureDragEndCallback? onVerticalDragEnd
```

之前以主按钮接触屏幕并进行垂直移动的指针，已不再与屏幕接触，并且在停止接触屏幕时以特定速度移动。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onVerticalDragCancel

```dart
GestureDragCancelCallback? onVerticalDragCancel
```

先前触发 [onVerticalDragDown] 的指针未能完成。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onHorizontalDragDown

```dart
GestureDragDownCallback? onHorizontalDragDown
```

指针已以主按钮接触屏幕，可能即将开始水平移动。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onHorizontalDragStart

```dart
GestureDragStartCallback? onHorizontalDragStart
```

指针已以主按钮接触屏幕，并已开始水平移动。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onHorizontalDragUpdate

```dart
GestureDragUpdateCallback? onHorizontalDragUpdate
```

以主按钮接触屏幕并进行水平移动的指针，在水平方向上又发生了移动。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onHorizontalDragEnd

```dart
GestureDragEndCallback? onHorizontalDragEnd
```

之前以主按钮接触屏幕并进行水平移动的指针，已不再与屏幕接触，并且在停止接触屏幕时以特定速度移动。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onHorizontalDragCancel

```dart
GestureDragCancelCallback? onHorizontalDragCancel
```

先前触发 [onHorizontalDragDown] 的指针未能完成。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onPanDown

```dart
GestureDragDownCallback? onPanDown
```

指针已以主按钮接触屏幕，可能即将开始移动。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onPanStart

```dart
GestureDragStartCallback? onPanStart
```

指针已以主按钮接触屏幕，并已开始移动。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onPanUpdate

```dart
GestureDragUpdateCallback? onPanUpdate
```

以主按钮接触屏幕并进行移动的指针，又再次发生了移动。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onPanEnd

```dart
GestureDragEndCallback? onPanEnd
```

之前以主按钮接触屏幕并进行移动的指针，已不再与屏幕接触，并且在停止接触屏幕时以特定速度移动。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onPanCancel

```dart
GestureDragCancelCallback? onPanCancel
```

先前触发 [onPanDown] 的指针未能完成。

另请参阅：

- [kPrimaryButton](https://www.yuque.com/thyname/flutter.gestures/kprimarybutton)，此回调所响应的按钮。

### onScaleStart

```dart
GestureScaleStartCallback? onScaleStart
```

与屏幕接触的多个指针已建立一个焦点，且初始缩放比例为 1.0。

### onScaleUpdate

```dart
GestureScaleUpdateCallback? onScaleUpdate
```

与屏幕接触的多个指针指示出了新的焦点和/或缩放比例。

### onScaleEnd

```dart
GestureScaleEndCallback? onScaleEnd
```

多个指针均已不再与屏幕接触。

### onForcePressStart

```dart
GestureForcePressStartCallback? onForcePressStart
```

指针与屏幕接触，并以足够的力度按压以启动力度按压（force press）。力度至少达到 [ForcePressGestureRecognizer.startPressure]。

此回调仅在支持压力检测的设备屏幕上触发。

### onForcePressPeak

```dart
GestureForcePressPeakCallback? onForcePressPeak
```

指针与屏幕接触，并以最大力度按压。力度至少达到 [ForcePressGestureRecognizer.peakPressure]。

此回调仅在支持压力检测的设备屏幕上触发。

### onForcePressUpdate

```dart
GestureForcePressUpdateCallback? onForcePressUpdate
```

指针与屏幕接触，此前已超过 [ForcePressGestureRecognizer.startPressure]，且正在屏幕平面上移动、以不同力度按压屏幕，或两者同时发生。

此回调仅在支持压力检测的设备屏幕上触发。

### onForcePressEnd

```dart
GestureForcePressEndCallback? onForcePressEnd
```

由 [onForcePressStart] 跟踪的指针已不再与屏幕接触。

此回调仅在支持压力检测的设备屏幕上触发。

### behavior

```dart
HitTestBehavior? behavior
```

在决定命中测试如何传播到子 widget，以及是否考虑该 widget 之后的目标时，此手势检测器在命中测试期间应表现出的行为。

如果 [child] 不为 null，默认值为 [HitTestBehavior.deferToChild]；如果 child 为 null，默认值为 [HitTestBehavior.translucent]。

允许的值及其含义参见 [HitTestBehavior](https://www.yuque.com/thyname/flutter.rendering/hittestbehavior)。

### excludeFromSemantics

```dart
bool excludeFromSemantics
```

是否将这些手势从语义树中排除。例如，用于显示 tooltip 的长按手势会被排除，因为 tooltip 本身已直接包含在语义树中，若再加入用于显示它的手势会导致信息重复。

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

确定拖动起始行为的处理方式。

如果设置为 [DragStartBehavior.start]，拖动手势的动画行为将从拖动手势赢得竞技场的位置开始。如果设置为 [DragStartBehavior.down]，则会从首次检测到按下事件的位置开始。

一般而言，将此值设置为 [DragStartBehavior.start] 会使拖动动画更平滑，而设置为 [DragStartBehavior.down] 会使拖动行为感觉更灵敏。

默认情况下，拖动起始行为为 [DragStartBehavior.start]。

只有 [VerticalDragGestureRecognizer](https://www.yuque.com/thyname/flutter.gestures/verticaldraggesturerecognizer)、[HorizontalDragGestureRecognizer](https://www.yuque.com/thyname/flutter.gestures/horizontaldraggesturerecognizer) 和 [PanGestureRecognizer](https://www.yuque.com/thyname/flutter.gestures/pangesturerecognizer) 的 [DragGestureRecognizer.onStart] 回调会受此设置影响。

另请参阅：

- [DragGestureRecognizer.dragStartBehavior]，其中给出了不同行为的示例。

### supportedDevices

```dart
Set<PointerDeviceKind>? supportedDevices
```

允许被识别的设备种类。

如果设置为 null，则会识别所有设备类型的事件。默认为 null。

### trackpadScrollCausesScale

```dart
bool trackpadScrollCausesScale
```

{@macro flutter.gestures.scale.trackpadScrollCausesScale}

### trackpadScrollToScaleFactor

```dart
Offset trackpadScrollToScaleFactor
```

{@macro flutter.gestures.scale.trackpadScrollToScaleFactor}

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RawGestureDetector

```dart
class RawGestureDetector extends StatefulWidget {}
```

用于检测由给定手势工厂描述的手势的 widget。

对于常见手势，请使用 [GestureDetector](https://www.yuque.com/thyname/flutter.widgets/gesturedetector)。[RawGestureDetector](https://www.yuque.com/thyname/flutter.widgets/rawgesturedetector) 主要在开发自定义手势识别器时使用。

配置手势识别器需要精心构造一个映射（map），具体方法参见 [gestures](https://www.yuque.com/thyname/flutter.gestures) 以及下方示例。

{@tool snippet}

此示例展示了如何挂接一个 [TapGestureRecognizer](https://www.yuque.com/thyname/flutter.gestures/tapgesturerecognizer)。假定此代码在一个带有 `_last` 字段的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象内部使用，该字段随后会作为手势检测器的子 widget 显示。

```dart
RawGestureDetector(
  gestures: <Type, GestureRecognizerFactory>{
    TapGestureRecognizer: GestureRecognizerFactoryWithHandlers<TapGestureRecognizer>(
      () => TapGestureRecognizer(),
      (TapGestureRecognizer instance) {
        instance
          ..onTapDown = (TapDownDetails details) { setState(() { _last = 'down'; }); }
          ..onTapUp = (TapUpDetails details) { setState(() { _last = 'up'; }); }
          ..onTap = () { setState(() { _last = 'tap'; }); }
          ..onTapCancel = () { setState(() { _last = 'cancel'; }); };
      },
    ),
  },
  child: Container(width: 300.0, height: 300.0, color: Colors.yellow, child: Text(_last)),
)
```

{@end-tool}

另请参阅：

- [GestureDetector](https://www.yuque.com/thyname/flutter.widgets/gesturedetector)，一个灵活性较低但更简单的 widget，可实现相同的功能。
- [Listener](https://www.yuque.com/thyname/flutter.widgets/listener)，用于报告原始指针事件的 widget。
- [GestureRecognizer](https://www.yuque.com/thyname/flutter.gestures/gesturerecognizer)，用于创建自定义手势识别器时所继承的类。

### RawGestureDetector()

```dart
RawGestureDetector({dynamic key, Widget? child, Map<Type, GestureRecognizerFactory> gestures = const <Type, GestureRecognizerFactory>{}, HitTestBehavior? behavior, bool excludeFromSemantics = false, SemanticsGestureDelegate? semantics})
```

创建一个用于检测手势的 widget。

手势检测器可以为 widget 树贡献供辅助技术使用的语义信息。该行为可以通过 [semantics](https://www.yuque.com/thyname/flutter.semantics) 进行配置，或通过 [excludeFromSemantics] 禁用。

### child

```dart
Widget? child
```

此 widget 下方的 widget 树。

{@macro flutter.widgets.ProxyWidget.child}

### gestures

```dart
Map<Type, GestureRecognizerFactory> gestures
```

此 widget 将尝试识别的手势。

这应该是一个从 [GestureRecognizer](https://www.yuque.com/thyname/flutter.gestures/gesturerecognizer) 子类到使用相同类型特化的 [GestureRecognizerFactory](https://www.yuque.com/thyname/flutter.widgets/gesturerecognizerfactory) 子类的映射。

此值可以在布局阶段使用 [RawGestureDetectorState.replaceGestureRecognizers] 进行延迟绑定。

### behavior

```dart
HitTestBehavior? behavior
```

此手势检测器在命中测试期间应表现出的行为。

如果 [child] 不为 null，默认值为 [HitTestBehavior.deferToChild]；如果 child 为 null，默认值为 [HitTestBehavior.translucent]。

### excludeFromSemantics

```dart
bool excludeFromSemantics
```

是否将这些手势从语义树中排除。例如，用于显示 tooltip 的长按手势会被排除，因为 tooltip 本身已直接包含在语义树中，若再加入用于显示它的手势会导致信息重复。

### semantics

```dart
SemanticsGestureDelegate? semantics
```

描述应添加到底层渲染对象 [RenderSemanticsGestureHandler](https://www.yuque.com/thyname/flutter.rendering/rendersemanticsgesturehandler) 的语义标注。

如果 [excludeFromSemantics] 为 true，则此项不起作用。

当 [semantics](https://www.yuque.com/thyname/flutter.semantics) 为 null 时，[RawGestureDetector](https://www.yuque.com/thyname/flutter.widgets/rawgesturedetector) 将回退到一个默认委托，该委托会检查检测器是否拥有特定的手势识别器，并在存在时调用其回调：

- 在语义点击（semantic tap）期间，它会调用 [TapGestureRecognizer](https://www.yuque.com/thyname/flutter.gestures/tapgesturerecognizer) 的 `onTapDown`、`onTapUp` 和 `onTap`。
- 在语义长按（semantic long press）期间，它会调用 [LongPressGestureRecognizer](https://www.yuque.com/thyname/flutter.gestures/longpressgesturerecognizer) 的 `onLongPressDown`、`onLongPressStart`、`onLongPress`、`onLongPressEnd` 和 `onLongPressUp`。
- 在语义水平拖动（semantic horizontal drag）期间，它会调用 [HorizontalDragGestureRecognizer](https://www.yuque.com/thyname/flutter.gestures/horizontaldraggesturerecognizer) 的 `onDown`、`onStart`、`onUpdate` 和 `onEnd`，然后调用 [PanGestureRecognizer](https://www.yuque.com/thyname/flutter.gestures/pangesturerecognizer) 的 `onDown`、`onStart`、`onUpdate` 和 `onEnd`。
- 在语义垂直拖动（semantic vertical drag）期间，它会调用 [VerticalDragGestureRecognizer](https://www.yuque.com/thyname/flutter.gestures/verticaldraggesturerecognizer) 的 `onDown`、`onStart`、`onUpdate` 和 `onEnd`，然后调用 [PanGestureRecognizer](https://www.yuque.com/thyname/flutter.gestures/pangesturerecognizer) 的 `onDown`、`onStart`、`onUpdate` 和 `onEnd`。

{@tool snippet} 此自定义手势检测器会监听力度按压（force press），同时也允许通过语义长按触发相同的回调。

```dart
class ForcePressGestureDetectorWithSemantics extends StatelessWidget {
  const ForcePressGestureDetectorWithSemantics({
    super.key,
    required this.child,
    required this.onForcePress,
  });

  final Widget child;
  final VoidCallback onForcePress;

  @override
  Widget build(BuildContext context) {
    return RawGestureDetector(
      gestures: <Type, GestureRecognizerFactory>{
        ForcePressGestureRecognizer: GestureRecognizerFactoryWithHandlers<ForcePressGestureRecognizer>(
          () => ForcePressGestureRecognizer(debugOwner: this),
          (ForcePressGestureRecognizer instance) {
            instance.onStart = (_) => onForcePress();
          }
        ),
      },
      behavior: HitTestBehavior.opaque,
      semantics: _LongPressSemanticsDelegate(onForcePress),
      child: child,
    );
  }
}

class _LongPressSemanticsDelegate extends SemanticsGestureDelegate {
  _LongPressSemanticsDelegate(this.onLongPress);

  VoidCallback onLongPress;

  @override
  void assignSemantics(RenderSemanticsGestureHandler renderObject) {
    renderObject.onLongPress = onLongPress;
  }
}
```

{@end-tool}

### createState()

```dart
RawGestureDetectorState createState()
```

# RawGestureDetectorState

```dart
class RawGestureDetectorState extends State<RawGestureDetector> {}
```

[RawGestureDetector](https://www.yuque.com/thyname/flutter.widgets/rawgesturedetector) 的状态。

### initState()

```dart
void initState()
```

### didUpdateWidget()

```dart
void didUpdateWidget(RawGestureDetector oldWidget)
```

### replaceGestureRecognizers()

```dart
void replaceGestureRecognizers(Map<Type, GestureRecognizerFactory> gestures)
```

此方法可以在构建阶段之后，在手势检测器最近的 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 后代进行布局期间调用，以更新当前活动的手势识别器列表。

典型用例是 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable)，它将自身的视口（viewport）放置在其手势检测器中，随后需要知道视口及其子 widget 的尺寸，以确定是否应启用该手势检测器。

此参数应遵循与 [RawGestureDetector.gestures] 相同的约定。它相当于该值的临时替代品，直到下一次构建为止。

### replaceSemanticsActions()

```dart
void replaceSemanticsActions(Set<SemanticsAction> actions)
```

可以调用此方法，在渲染对象创建后，过滤可用语义操作的列表。

实际的过滤操作会在下一帧进行；如果尚无待处理的帧，则会安排一帧。

[Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 使用此方法来配置系统的无障碍工具，以便它们了解某个特定列表可以朝哪些方向滚动。

如果从未调用此方法，则操作不会被过滤。如果要过滤的操作列表发生变化，必须再次调用此方法。

### dispose()

```dart
void dispose()
```

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SemanticsGestureDelegate

```dart
abstract class SemanticsGestureDelegate {}
```

用于描述 [RawGestureDetector](https://www.yuque.com/thyname/flutter.widgets/rawgesturedetector) 应向渲染对象 [RenderSemanticsGestureHandler](https://www.yuque.com/thyname/flutter.rendering/rendersemanticsgesturehandler) 添加哪些语义标注的基类。

用于允许自定义 [GestureDetector](https://www.yuque.com/thyname/flutter.widgets/gesturedetector) 添加语义标注。

### SemanticsGestureDelegate()

```dart
SemanticsGestureDelegate()
```

创建一个手势语义的委托。

### assignSemantics()

```dart
void assignSemantics(RenderSemanticsGestureHandler renderObject)
```

将语义标注分配给手势检测器的 [RenderSemanticsGestureHandler](https://www.yuque.com/thyname/flutter.rendering/rendersemanticsgesturehandler) 渲染对象。

此方法会在 widget 被创建、更新，或在 [RawGestureDetectorState.replaceGestureRecognizers] 期间调用。
