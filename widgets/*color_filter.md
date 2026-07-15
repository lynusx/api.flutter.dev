@docImport 'basic.dart';

# ColorFiltered

```dart
class ColorFiltered extends SingleChildRenderObjectWidget {}
```

对其子组件应用 [ColorFilter](https://www.yuque.com/thyname/dart.ui/colorfilter)。

此组件根据指定的 [ColorFilter](https://www.yuque.com/thyname/dart.ui/colorfilter)，独立地对 [child] 内容的每个像素应用一个函数。使用 [ColorFilter.mode] 构造函数可以通过 [BlendMode](https://www.yuque.com/thyname/dart.ui/blendmode) 应用一个 [Color](https://www.yuque.com/thyname/dart.ui/color)。如果需要将 [ColorFilter](https://www.yuque.com/thyname/dart.ui/colorfilter) 应用到 [child] 下方的内容上，请改用 [BackdropFilter](https://www.yuque.com/thyname/flutter.widgets/backdropfilter) 组件。

{@youtube 560 315 https://www.youtube.com/watch?v=F7Cll22Dno8}

{@tool dartpad} 这两张图片分别应用了两种不同 [BlendMode](https://www.yuque.com/thyname/dart.ui/blendmode) 的 [ColorFilter](https://www.yuque.com/thyname/dart.ui/colorfilter)：一种使用红色和 [BlendMode.modulate]，另一种使用灰色和 [BlendMode.saturation]。

** See code in examples/api/lib/widgets/color_filter/color_filtered.0.dart ** {@end-tool}

另请参阅：

- [BlendMode](https://www.yuque.com/thyname/dart.ui/blendmode)，描述如何将源图像与目标图像混合。
- [ColorFilter](https://www.yuque.com/thyname/dart.ui/colorfilter)，描述将一种颜色转换为另一种颜色的函数。

### ColorFiltered()

```dart
ColorFiltered({required ColorFilter colorFilter, Widget? child, dynamic key})
```

创建一个对其子组件应用 [ColorFilter](https://www.yuque.com/thyname/dart.ui/colorfilter) 的组件。

### colorFilter

```dart
ColorFilter colorFilter
```

应用于此组件子组件的颜色过滤器。

### createRenderObject()

```dart
RenderObject createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderObject renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
