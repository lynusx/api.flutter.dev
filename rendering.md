Flutter 渲染树。

要使用此库，请导入 `package:flutter/rendering.dart`。

[RenderObject] 层次结构被 Flutter Widgets 库用于实现其布局和绘制后端。一般来说，虽然你可以在应用程序中使用自定义 [RenderBox] 类来实现特定效果，但大多数情况下，你与 [RenderObject] 层次结构的唯一交互将是调试布局问题。

如果你正在直接基于渲染库开发自己的库或应用程序，那么你需要有一个绑定（binding，见 [BindingBase]）。你可以使用 [RenderingFlutterBinding]，也可以创建自己的绑定。如果你创建自己的绑定，它至少需要导入 [ServicesBinding]、[GestureBinding]、[SchedulerBinding]、[PaintingBinding] 和 [RendererBinding]。渲染库不会自动创建绑定，而是依赖于使用这些特性初始化的绑定。
