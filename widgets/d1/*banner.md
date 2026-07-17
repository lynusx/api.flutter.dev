@docImport 'package:flutter/material.dart';

@docImport 'app.dart';

# BannerLocation

```dart
enum BannerLocation {}
```

在何处显示 [Banner](https://www.yuque.com/thyname/flutter.widgets/banner)。

起始和结束位置是相对于环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)（可由 [Banner.layoutDirection] 覆盖）而言的。

当环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)（或 [Banner.layoutDirection]）为 [TextDirection.rtl] 时，在右上角显示横幅；当环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 为 [TextDirection.ltr] 时，在左上角显示横幅。

当环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)（或 [Banner.layoutDirection]）为 [TextDirection.rtl] 时，在左上角显示横幅；当环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 为 [TextDirection.ltr] 时，在右上角显示横幅。

当环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)（或 [Banner.layoutDirection]）为 [TextDirection.rtl] 时，在右下角显示横幅；当环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 为 [TextDirection.ltr] 时，在左下角显示横幅。

当环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)（或 [Banner.layoutDirection]）为 [TextDirection.rtl] 时，在左下角显示横幅；当环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 为 [TextDirection.ltr] 时，在右下角显示横幅。

# BannerPainter

```dart
class BannerPainter extends CustomPainter {}
```

绘制一个 [Banner](https://www.yuque.com/thyname/flutter.widgets/banner)。

### BannerPainter()

```dart
BannerPainter({required String message, required TextDirection textDirection, required BannerLocation location, required TextDirection layoutDirection, Color color = _kColor, TextStyle textStyle = _kTextStyle, BoxShadow shadow = _kShadow})
```

创建一个横幅绘制器。

### message

```dart
String message
```

要在横幅中显示的消息。

### textDirection

```dart
TextDirection textDirection
```

文本的方向性。

此值用于消除双向文本渲染方式的歧义。例如，若消息是一个英语短语后跟一个希伯来语短语，在 [TextDirection.ltr] 上下文中，英语短语会在左侧，希伯来语短语在其右侧；而在 [TextDirection.rtl] 上下文中，英语短语会在右侧，希伯来语短语在其左侧。

另请参阅：

- [layoutDirection]，它控制 [location] 中值的解释方式。

### location

```dart
BannerLocation location
```

在何处显示横幅（例如右上角）。

### layoutDirection

```dart
TextDirection layoutDirection
```

布局的方向性。

此值用于解释横幅的 [location]。

另请参阅：

- [textDirection]，它控制 [message] 的阅读方向。

### color

```dart
Color color
```

在 [message] 背后绘制的颜色。

默认为深红色。

### textStyle

```dart
TextStyle textStyle
```

用于 [message] 的文本样式。

默认为白色粗体文本。

### shadow

```dart
BoxShadow shadow
```

横幅的阴影属性。

使用 [BoxShadow](https://www.yuque.com/thyname/flutter.painting/boxshadow) 对象来定义阴影的颜色、模糊半径和扩散半径。这些属性可用于创建不同的阴影效果。

### dispose()

```dart
void dispose()
```

释放此绘制器持有的资源。

调用此方法后，此对象将不再可用。

### paint()

```dart
void paint(Canvas canvas, Size size)
```

### shouldRepaint()

```dart
bool shouldRepaint(BannerPainter oldDelegate)
```

### hitTest()

```dart
bool hitTest(Offset position)
```

# Banner

```dart
class Banner extends StatefulWidget {}
```

在另一个组件的角上方显示一条对角线消息。

可用于显示应用的执行模式（例如断言已启用）。

另请参阅：

- [CheckedModeBanner](https://www.yuque.com/thyname/flutter.widgets/checkedmodebanner)，[WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 组件在调试模式下默认包含它，用于显示一条写着 "DEBUG" 的横幅。

### Banner()

```dart
Banner({dynamic key, Widget? child, required String message, TextDirection? textDirection, required BannerLocation location, TextDirection? layoutDirection, Color color = _kColor, TextStyle textStyle = _kTextStyle, BoxShadow shadow = _kShadow})
```

创建一个横幅。

### child

```dart
Widget? child
```

要显示在横幅背后的组件。

{@macro flutter.widgets.ProxyWidget.child}

### message

```dart
String message
```

要在横幅中显示的消息。

### textDirection

```dart
TextDirection? textDirection
```

文本的方向性。

此值用于消除双向文本渲染方式的歧义。例如，若消息是一个英语短语后跟一个希伯来语短语，在 [TextDirection.ltr] 上下文中，英语短语会在左侧，希伯来语短语在其右侧；而在 [TextDirection.rtl] 上下文中，英语短语会在右侧，希伯来语短语在其左侧。

若存在环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)，则默认使用它。

另请参阅：

- [layoutDirection]，它控制 [location] 的解释方式。

### location

```dart
BannerLocation location
```

在何处显示横幅（例如右上角）。

### layoutDirection

```dart
TextDirection? layoutDirection
```

布局的方向性。

此值用于解析 [location] 的取值。

若存在环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)，则默认使用它。

另请参阅：

- [textDirection]，它控制 [message] 的阅读方向。

### color

```dart
Color color
```

横幅的颜色。

### textStyle

```dart
TextStyle textStyle
```

横幅上显示文本的样式。

### shadow

```dart
BoxShadow shadow
```

横幅的阴影属性。

使用 [BoxShadow](https://www.yuque.com/thyname/flutter.painting/boxshadow) 对象来定义阴影的颜色、模糊半径和扩散半径。这些属性可用于创建不同的阴影效果。

### createState()

```dart
State<Banner> createState()
```

# CheckedModeBanner

```dart
class CheckedModeBanner extends StatelessWidget {}
```

在调试模式下运行时显示一条写着 "DEBUG" 的 [Banner](https://www.yuque.com/thyname/flutter.widgets/banner)。[MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 默认会构建一个这样的组件。

在发布模式下不执行任何操作。

### CheckedModeBanner()

```dart
CheckedModeBanner({dynamic key, required Widget child})
```

创建一个 const 调试模式横幅。

### child

```dart
Widget child
```

要显示在横幅背后的组件。

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
