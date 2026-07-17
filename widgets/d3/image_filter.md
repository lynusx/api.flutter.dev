@docImport 'basic.dart'; @docImport 'color_filter.dart';

# ImageFiltered

```dart
class ImageFiltered extends SingleChildRenderObjectWidget {}
```

将 [ImageFilter](https://www.yuque.com/thyname/dart.ui/imagefilter) 应用于其子组件。

图片滤镜总会对子组件应用滤镜操作，即使该滤镜在概念上是"空操作"，例如半径为 0 的 ImageFilter.blur，或矩阵为单位矩阵的 ImageFilter.matrix。将 [ImageFiltered.enabled] 设置为 `false` 是禁用图片滤镜更为高效的方式。

框架不会尝试优化掉"空操作"滤镜，因为它无法区分有意为之的空操作与仅仅是碰巧变成空操作的滤镜。以一个会被动画驱动的 ImageFilter.matrix 为例，它在动画过程中恰好经过单位矩阵这一状态。如果框架将其识别为空操作，就会在动画期间丢弃并重新创建该图层，这样做的开销反而比保留图层更大。

{@youtube 560 315 https://www.youtube.com/watch?v=7Lftorq4i2o}

另请参阅：

- [BackdropFilter](https://www.yuque.com/thyname/flutter.widgets/backdropfilter)，将 [ImageFilter](https://www.yuque.com/thyname/dart.ui/imagefilter) 应用于其子组件下方的所有内容。
- [ColorFiltered](https://www.yuque.com/thyname/flutter.widgets/colorfiltered)，将 [ColorFilter](https://www.yuque.com/thyname/dart.ui/colorfilter) 应用于其子组件。

### ImageFiltered()

```dart
ImageFiltered({dynamic key, required ImageFilter imageFilter, Widget? child, bool enabled = true})
```

创建一个将 [ImageFilter](https://www.yuque.com/thyname/dart.ui/imagefilter) 应用于其子组件的组件。

### imageFilter

```dart
ImageFilter imageFilter
```

要应用于此组件子组件的图片滤镜。

### enabled

```dart
bool enabled
```

是否对此组件的子组件应用图片滤镜操作。

出于性能考虑，建议将 enabled 设置为 `false`，而不是创建"空操作"类型的滤镜。
