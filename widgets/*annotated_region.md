# AnnotatedRegion

```dart
class AnnotatedRegion<T extends Object> extends SingleChildRenderObjectWidget {}
```

为图层树的某个区域标注一个值。

另请参阅：

- [Layer.find]，展示了如何获取该值的示例。
- [AnnotatedRegionLayer](https://www.yuque.com/thyname/flutter.rendering/annotatedregionlayer)，被推入图层树的图层。

### AnnotatedRegion()

```dart
AnnotatedRegion({dynamic key, required Widget child, required T value, bool sized = true})
```

创建一个新的标注区域，将 [value] 插入图层树中。

[child] 和 [value] 均不能为 null。

[sized] 默认为 true，用于控制标注区域是否裁剪其子组件。

### value

```dart
T value
```

一个可以通过 [Layer.find] 获取的值。

### sized

```dart
bool sized
```

如果为 false，则推入树中的图层将不会提供尺寸信息。

带有尺寸的 [AnnotatedRegionLayer](https://www.yuque.com/thyname/flutter.rendering/annotatedregionlayer) 会检查 [Layer.find] 中提供的偏移量是否在边界内，如果不在边界内则返回 null。

另请参阅：

- [AnnotatedRegionLayer](https://www.yuque.com/thyname/flutter.rendering/annotatedregionlayer)，了解此行为的说明。

### createRenderObject()

```dart
RenderObject createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderAnnotatedRegion<T> renderObject)
```
