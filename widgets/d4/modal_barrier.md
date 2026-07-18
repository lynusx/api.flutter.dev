@docImport 'routes.dart';

# ModalBarrier

```dart
class ModalBarrier extends StatelessWidget {}
```

一个阻止用户与其后方 Widget 进行交互的 Widget。

模态屏障（modal barrier）是渲染在每个路由（route）后方的幕布（scrim），通常用于阻止用户与当前路由下方的路由进行交互，并且通常会部分遮蔽这些路由。

例如，当对话框显示在屏幕上时，对话框下方的页面通常会被模态屏障变暗。

另请参阅：

- [ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute)，间接使用此 Widget。
- [AnimatedModalBarrier](https://www.yuque.com/thyname/flutter.widgets/animatedmodalbarrier)，与此类似，但接受一个动画化的 [color] 而非单一颜色值。

### ModalBarrier()

```dart
ModalBarrier({dynamic key, Color? color, bool dismissible = true, VoidCallback? onDismiss, String? semanticsLabel, bool? barrierSemanticsDismissible = true, ValueNotifier<EdgeInsets>? clipDetailsNotifier, String? semanticsOnTapHint})
```

创建一个阻止用户交互的 Widget。

### color

```dart
Color? color
```

如果非空，则使用此颜色填充屏障。

另请参阅：

- [ModalRoute.barrierColor]，为 [ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute) 构建的 [ModalBarrier](https://www.yuque.com/thyname/flutter.widgets/modalbarrier) 控制此属性。

### dismissible

```dart
bool dismissible
```

指定当用户点按屏障时是否会将其关闭。

如果为 true，且 [onDismiss] 非空，则会调用 [onDismiss]；否则会将当前路由从环境 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 中弹出。

如果为 false，点按屏障将不会有任何效果。

另请参阅：

- [ModalRoute.barrierDismissible]，为 [ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute) 构建的 [ModalBarrier](https://www.yuque.com/thyname/flutter.widgets/modalbarrier) 控制此属性。

### onDismiss

```dart
VoidCallback? onDismiss
```

{@template flutter.widgets.ModalBarrier.onDismiss} 当屏障即将被关闭时调用。

如果 [onDismiss] 非空，将调用它来代替弹出当前路由。由该回调函数负责处理屏障的关闭。

如果为空，将弹出环境 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的当前路由。

当 [dismissible] 为 false 时，此字段将被忽略。{@endtemplate}

### barrierSemanticsDismissible

```dart
bool? barrierSemanticsDismissible
```

模态屏障的语义是否包含在语义树中。

另请参阅：

- [ModalRoute.semanticsDismissible]，为 [ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute) 构建的 [ModalBarrier](https://www.yuque.com/thyname/flutter.widgets/modalbarrier) 控制此属性。

### semanticsLabel

```dart
String? semanticsLabel
```

当屏障为 [dismissible] 时使用的语义标签。

该语义标签会被无障碍工具（例如 Android 上的 TalkBack 和 iOS 上的 VoiceOver）在屏障获得焦点时朗读出来。

另请参阅：

- [ModalRoute.barrierLabel]，为 [ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute) 构建的 [ModalBarrier](https://www.yuque.com/thyname/flutter.widgets/modalbarrier) 控制此属性。

### clipDetailsNotifier

```dart
ValueNotifier<EdgeInsets>? clipDetailsNotifier
```

{@template flutter.widgets.ModalBarrier.clipDetailsNotifier} 包含一个 [EdgeInsets](https://www.yuque.com/thyname/flutter.painting/edgeinsets) 类型的值，用于指定该 Widget 的 [SemanticsNode.rect] 应如何被裁剪。

另请参阅：

- [_SemanticsClipper]，利用其中的值来更新其子级的 [SemanticsNode.rect]。{@endtemplate}

### semanticsOnTapHint

```dart
String? semanticsOnTapHint
```

{@macro flutter.material.ModalBottomSheetRoute.barrierOnTapHint}

### build()

```dart
Widget build(BuildContext context)
```

# AnimatedModalBarrier

```dart
class AnimatedModalBarrier extends AnimatedWidget {}
```

一个阻止用户与其后方 Widget 进行交互的 Widget，并且可以配置一个动画化的颜色值。

模态屏障是渲染在每个路由后方的幕布，通常用于阻止用户与当前路由下方的路由进行交互，并且通常会部分遮蔽这些路由。

例如，当对话框显示在屏幕上时，对话框下方的页面通常会被模态屏障变暗。

此 Widget 与 [ModalBarrier](https://www.yuque.com/thyname/flutter.widgets/modalbarrier) 类似，不同之处在于它接受一个动画化的 [color]，而非单一颜色。

另请参阅：

- [ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute)，使用此 Widget。

### AnimatedModalBarrier()

```dart
AnimatedModalBarrier({dynamic key, required Animation<Color?> color, bool dismissible = true, String? semanticsLabel, bool? barrierSemanticsDismissible, VoidCallback? onDismiss, ValueNotifier<EdgeInsets>? clipDetailsNotifier, String? semanticsOnTapHint})
```

创建一个阻止用户交互的 Widget。

### color

```dart
Animation<Color?> get color
```

如果非空，则使用此颜色填充屏障。

另请参阅：

- [ModalRoute.barrierColor]，为 [ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute) 构建的 [AnimatedModalBarrier](https://www.yuque.com/thyname/flutter.widgets/animatedmodalbarrier) 控制此属性。

### dismissible

```dart
bool dismissible
```

点按屏障是否会将当前路由从 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 中弹出。

另请参阅：

- [ModalRoute.barrierDismissible]，为 [ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute) 构建的 [AnimatedModalBarrier](https://www.yuque.com/thyname/flutter.widgets/animatedmodalbarrier) 控制此属性。

### semanticsLabel

```dart
String? semanticsLabel
```

当屏障为 [dismissible] 时使用的语义标签。

该语义标签会被无障碍工具（例如 Android 上的 TalkBack 和 iOS 上的 VoiceOver）在屏障获得焦点时朗读出来。另请参阅：

- [ModalRoute.barrierLabel]，为 [ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute) 构建的 [ModalBarrier](https://www.yuque.com/thyname/flutter.widgets/modalbarrier) 控制此属性。

### barrierSemanticsDismissible

```dart
bool? barrierSemanticsDismissible
```

模态屏障的语义是否包含在语义树中。

另请参阅：

- [ModalRoute.semanticsDismissible]，为 [ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute) 构建的 [ModalBarrier](https://www.yuque.com/thyname/flutter.widgets/modalbarrier) 控制此属性。

### onDismiss

```dart
VoidCallback? onDismiss
```

{@macro flutter.widgets.ModalBarrier.onDismiss}

### clipDetailsNotifier

```dart
ValueNotifier<EdgeInsets>? clipDetailsNotifier
```

{@macro flutter.widgets.ModalBarrier.clipDetailsNotifier}

### semanticsOnTapHint

```dart
String? semanticsOnTapHint
```

此提示文本用于说明当用户点按 [ModalBarrier](https://www.yuque.com/thyname/flutter.widgets/modalbarrier) 时可以执行的操作。

例如，如果提示文本为 "close bottom sheet"，则会朗读为 "Double tap to close bottom sheet"（双击以关闭底部面板）。

如果此值为空，则会应用默认的 onTapHint，朗读为 "Double tap to activate"（双击以激活）。
