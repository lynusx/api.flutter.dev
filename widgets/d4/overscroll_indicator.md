@docImport 'package:flutter/material.dart';

@docImport 'nested_scroll_view.dart'; @docImport 'scroll_configuration.dart'; @docImport 'scroll_view.dart'; @docImport 'scrollable.dart';

# GlowingOverscrollIndicator

```dart
class GlowingOverscrollIndicator extends StatefulWidget {}
```

滚动视图发生越界滚动（overscroll）时的视觉提示。

[GlowingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/glowingoverscrollindicator) 通过监听 [ScrollNotification](https://www.yuque.com/thyname/flutter.widgets/scrollnotification) 来控制越界滚动提示的显示。这些通知通常由 [ScrollView](https://www.yuque.com/thyname/flutter.widgets/scrollview)（如 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview) 或 [GridView](https://www.yuque.com/thyname/flutter.widgets/gridview)）生成。

[GlowingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/glowingoverscrollindicator) 在显示越界滚动提示之前会生成 [OverscrollIndicatorNotification](https://www.yuque.com/thyname/flutter.widgets/overscrollindicatornotification)。若要阻止该指示器显示提示，可在该通知上调用 [OverscrollIndicatorNotification.disallowIndicator]。

在通常使用此类越界滚动提示的平台（例如 Android）上，该组件由 [ScrollBehavior.buildOverscrollIndicator] 自动创建。

在 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 中，边缘发光的颜色为整体主题的 [ColorScheme.secondary] 颜色。

## 为高级滚动视图自定义发光位置

在使用 [GlowingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/glowingoverscrollindicator) 构建 [CustomScrollView](https://www.yuque.com/thyname/flutter.widgets/customscrollview) 时，该指示器将应用于整个可滚动区域，无论 CustomScrollView 包含哪些 sliver。

例如，如果你的 CustomScrollView 在第一个位置包含一个 SliverAppBar，GlowingOverscrollIndicator 将覆盖在该 SliverAppBar 上方。要调整这种情况下 GlowingOverscrollIndicator 的位置，你可以使用 [NotificationListener](https://www.yuque.com/thyname/flutter.widgets/notificationlistener) 并为通知提供 [OverscrollIndicatorNotification.paintOffset]，或者使用 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview)。

{@tool dartpad} 此示例演示了如何在构建 [CustomScrollView](https://www.yuque.com/thyname/flutter.widgets/customscrollview) 时使用 [NotificationListener](https://www.yuque.com/thyname/flutter.widgets/notificationlistener) 来调整 [GlowingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/glowingoverscrollindicator) 的位置。拖动可滚动区域即可查看越界滚动指示器的边界。

** See code in examples/api/lib/widgets/overscroll_indicator/glowing_overscroll_indicator.0.dart ** {@end-tool}

{@tool dartpad} 此示例演示了如何在构建 [CustomScrollView](https://www.yuque.com/thyname/flutter.widgets/customscrollview) 时使用 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 来调整 [GlowingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/glowingoverscrollindicator) 的位置。拖动可滚动区域即可查看越界滚动指示器的边界。

** See code in examples/api/lib/widgets/overscroll_indicator/glowing_overscroll_indicator.1.dart ** {@end-tool}

另请参阅：

- [OverscrollIndicatorNotification](https://www.yuque.com/thyname/flutter.widgets/overscrollindicatornotification)，可用于调整发光位置，或完全阻止发光效果的绘制。
- [NotificationListener](https://www.yuque.com/thyname/flutter.widgets/notificationlistener)，用于监听 [OverscrollIndicatorNotification](https://www.yuque.com/thyname/flutter.widgets/overscrollindicatornotification)。
- [StretchingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/stretchingoverscrollindicator)，一种 Material Design 风格的越界滚动指示器。

### GlowingOverscrollIndicator()

```dart
GlowingOverscrollIndicator({dynamic key, bool showLeading = true, bool showTrailing = true, required AxisDirection axisDirection, required Color color, ScrollNotificationPredicate notificationPredicate = defaultScrollNotificationPredicate, Widget? child})
```

创建一个用于显示滚动视图越界滚动提示的视觉指示器。

要使该组件显示越界滚动提示，[child] 组件必须包含一个能够生成 [ScrollNotification](https://www.yuque.com/thyname/flutter.widgets/scrollnotification) 的组件，例如 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview) 或 [GridView](https://www.yuque.com/thyname/flutter.widgets/gridview)。

### showLeading

```dart
bool showLeading
```

是否在负滚动偏移一侧显示越界滚动发光效果。

对于纵向向下的视口，这一侧是顶部。

默认为 true。

另一侧的对应控制项请参阅 [showTrailing]。

### showTrailing

```dart
bool showTrailing
```

是否在正滚动偏移一侧显示越界滚动发光效果。

对于纵向向下的视口，这一侧是底部。

默认为 true。

另一侧的对应控制项请参阅 [showLeading]。

### axisDirection

```dart
AxisDirection axisDirection
```

{@template flutter.overscroll.axisDirection} 需要可视化越界滚动的 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 中正滚动偏移的方向。 {@endtemplate}

### axis

```dart
Axis get axis
```

{@template flutter.overscroll.axis} 需要可视化越界滚动的 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 发生滚动所沿的轴。 {@endtemplate}

### color

```dart
Color color
```

发光效果的颜色。Alpha 通道会被忽略。

### notificationPredicate

```dart
ScrollNotificationPredicate notificationPredicate
```

{@template flutter.overscroll.notificationPredicate} 用于指定该组件是否应处理某个 [ScrollNotification](https://www.yuque.com/thyname/flutter.widgets/scrollnotification) 的检查函数。

默认情况下，会检查 `notification.depth == 0`。对于更复杂的布局（例如嵌套的 [ScrollView](https://www.yuque.com/thyname/flutter.widgets/scrollview)），可将其设置为其他值。 {@endtemplate}

### child

```dart
Widget? child
```

此组件在组件树中的下一级子组件。

越界滚动指示器将绘制在此子组件之上。该子组件（及其子树）应包含 [ScrollNotification](https://www.yuque.com/thyname/flutter.widgets/scrollnotification) 通知的来源。

通常，[GlowingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/glowingoverscrollindicator) 由 [ScrollBehavior.buildOverscrollIndicator] 方法创建，此时 child 通常就是传给该方法的参数。

### createState()

```dart
State<GlowingOverscrollIndicator> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# StretchingOverscrollIndicator

```dart
class StretchingOverscrollIndicator extends StatefulWidget {}
```

一种 Material Design 风格的视觉提示，用于表示滚动视图已发生越界滚动。

[StretchingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/stretchingoverscrollindicator) 通过监听 [ScrollNotification](https://www.yuque.com/thyname/flutter.widgets/scrollnotification) 来拉伸 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 的内容。这些通知通常由 [ScrollView](https://www.yuque.com/thyname/flutter.widgets/scrollview)（如 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview) 或 [GridView](https://www.yuque.com/thyname/flutter.widgets/gridview)）生成。

触发时，[StretchingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/stretchingoverscrollindicator) 会在显示越界滚动提示之前生成一个 [OverscrollIndicatorNotification](https://www.yuque.com/thyname/flutter.widgets/overscrollindicatornotification)。若要阻止该指示器显示提示，可在该通知上调用 [OverscrollIndicatorNotification.disallowIndicator]。

当 [ThemeData.useMaterial3] 为 true 时，在通常使用此类越界滚动提示的平台（例如 Android）上，该组件由 [MaterialScrollBehavior.buildOverscrollIndicator] 创建。否则，当 [ThemeData.useMaterial3] 为 false 时，将使用 [GlowingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/glowingoverscrollindicator)。

另请参阅：

- [OverscrollIndicatorNotification](https://www.yuque.com/thyname/flutter.widgets/overscrollindicatornotification)，可用于完全阻止拉伸效果的应用。
- [NotificationListener](https://www.yuque.com/thyname/flutter.widgets/notificationlistener)，用于监听 [OverscrollIndicatorNotification](https://www.yuque.com/thyname/flutter.widgets/overscrollindicatornotification)。
- [GlowingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/glowingoverscrollindicator)，[TargetPlatform.android] 和 [TargetPlatform.fuchsia] 平台默认使用的越界滚动指示器。

### StretchingOverscrollIndicator()

```dart
StretchingOverscrollIndicator({dynamic key, required AxisDirection axisDirection, ScrollNotificationPredicate notificationPredicate = defaultScrollNotificationPredicate, Clip clipBehavior = Clip.hardEdge, Widget? child})
```

创建一个视觉指示器，通过对内容应用拉伸变换来提示滚动视图已发生越界滚动。

要使该组件显示越界滚动提示，[child] 组件必须包含一个能够生成 [ScrollNotification](https://www.yuque.com/thyname/flutter.widgets/scrollnotification) 的组件，例如 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview) 或 [GridView](https://www.yuque.com/thyname/flutter.widgets/gridview)。

### axisDirection

```dart
AxisDirection axisDirection
```

{@macro flutter.overscroll.axisDirection}

### axis

```dart
Axis get axis
```

{@macro flutter.overscroll.axis}

### notificationPredicate

```dart
ScrollNotificationPredicate notificationPredicate
```

{@macro flutter.overscroll.notificationPredicate}

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

默认为 [Clip.hardEdge]。

### child

```dart
Widget? child
```

此组件在组件树中的下一级子组件。

越界滚动指示器将对该子组件应用拉伸效果。该子组件（及其子树）应包含 [ScrollNotification](https://www.yuque.com/thyname/flutter.widgets/scrollnotification) 通知的来源。

### createState()

```dart
State<StretchingOverscrollIndicator> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# OverscrollIndicatorNotification

```dart
class OverscrollIndicatorNotification extends Notification with ViewportNotificationMixin {}
```

一种通知，表示 [GlowingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/glowingoverscrollindicator) 或 [StretchingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/stretchingoverscrollindicator) 即将开始显示越界滚动提示。

若要阻止该指示器显示提示，可在该通知上调用 [disallowIndicator]。

另请参阅：

- [GlowingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/glowingoverscrollindicator)，通过在子内容上方绘制指示器来生成此类通知。
- [StretchingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/stretchingoverscrollindicator)，通过对子内容应用拉伸变换来生成此类通知。

### OverscrollIndicatorNotification()

```dart
OverscrollIndicatorNotification({required bool leading})
```

创建一个通知，表示 [GlowingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/glowingoverscrollindicator) 或 [StretchingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/stretchingoverscrollindicator) 即将开始显示越界滚动提示。

### leading

```dart
bool leading
```

提示是否将显示在滚动视图的前缘（leading edge）。

### paintOffset

```dart
double paintOffset
```

控制 [GlowingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/glowingoverscrollindicator) 绘制时的偏移量。

正的偏移量会使发光效果远离其所在的边缘，例如对于纵向、[leading] 为 true 的指示器，[paintOffset] 为 100.0 会使指示器在距顶部边缘 100.0 像素处绘制。对于 [leading] 设为 `false` 的纵向指示器，[paintOffset] 为 100.0 则会使其在距底部 100.0 像素处绘制。

负的 [paintOffset] 通常没有意义，因为发光效果会被裁剪掉。

此属性对 [StretchingOverscrollIndicator](https://www.yuque.com/thyname/flutter.widgets/stretchingoverscrollindicator) 没有影响。

### accepted

```dart
bool accepted
```

当前的越界滚动事件是否允许显示指示器。

调用 [disallowIndicator] 会将此值设为 false，从而阻止越界滚动指示器显示。

默认为 true。

### disallowIndicator()

```dart
void disallowIndicator()
```

如果应阻止越界滚动指示器显示，则调用此方法。
