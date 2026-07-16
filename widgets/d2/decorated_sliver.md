@docImport 'package:flutter/material.dart';

@docImport 'container.dart'; @docImport 'scroll_view.dart';

# DecoratedSliver

```dart
class DecoratedSliver extends SingleChildRenderObjectWidget {}
```

一个 sliver Widget，会在其子 Widget 绘制之前或之后绘制一个 [Decoration](https://www.yuque.com/thyname/flutter.painting/decoration)。

与 [DecoratedBox](https://www.yuque.com/thyname/flutter.widgets/decoratedbox) 不同，此 Widget 要求其子 Widget 是一个 sliver，并且必须放置在需要 sliver 的 Widget 中。

如果子 sliver 的 [SliverGeometry.scrollExtent] 为无限，则只会将装饰绘制到底部的 [SliverGeometry.cacheExtent] 处，此时必须确保底部边框不会延伸到缓存区域顶部之上。如果边框半径大于缓存区域的范围，就可能出现这种情况。

通常与 [BoxDecoration](https://www.yuque.com/thyname/flutter.painting/boxdecoration) 搭配使用。

{@tool dartpad} 此示例展示了一个径向渐变，用于绘制夜空中的一轮明月：

** 代码见 examples/api/lib/widgets/sliver/decorated_sliver.0.dart ** {@end-tool}

{@tool dartpad} 此示例演示了 [CustomScrollView.clipBehavior] 如何影响一个被装饰的 sliver 的外观。

[Switch](https://www.yuque.com/thyname/flutter.material/switch) 用于确定是否启用裁剪，[Slider](https://www.yuque.com/thyname/flutter.material/slider) 用于调整窗口的高度。

** 代码见 examples/api/lib/widgets/sliver/decorated_sliver.1.dart ** {@end-tool}

此 Widget 不会对其 [child] 应用任何额外的裁剪。若要根据 [Decoration](https://www.yuque.com/thyname/flutter.painting/decoration) 的形状裁剪子 Widget，可以考虑使用 [ClipPath](https://www.yuque.com/thyname/flutter.widgets/clippath) Widget。

另请参阅：

- [DecoratedBox](https://www.yuque.com/thyname/flutter.widgets/decoratedbox)，此类适用于 RenderBox Widget 的对应版本。
- [Decoration](https://www.yuque.com/thyname/flutter.painting/decoration)，你可以扩展它以便为 [DecoratedSliver](https://www.yuque.com/thyname/flutter.widgets/decoratedsliver) 提供其他效果。
- [CustomPaint](https://www.yuque.com/thyname/flutter.widgets/custompaint)，另一种从 Widget 层绘制自定义效果的方式。

### DecoratedSliver()

```dart
DecoratedSliver({dynamic key, required Decoration decoration, DecorationPosition position = DecorationPosition.background, Widget? sliver})
```

创建一个绘制 [Decoration](https://www.yuque.com/thyname/flutter.painting/decoration) 的 Widget。

默认情况下，该装饰会绘制在子 Widget 后面。

### decoration

```dart
Decoration decoration
```

要绘制的装饰。

通常是一个 [BoxDecoration](https://www.yuque.com/thyname/flutter.painting/boxdecoration)。

### position

```dart
DecorationPosition position
```

装饰是绘制在子 Widget 后面还是前面。

### createRenderObject()

```dart
RenderDecoratedSliver createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderDecoratedSliver renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
