# OverflowBarAlignment

```dart
enum OverflowBarAlignment {}
```

定义当 [OverflowBar](https://www.yuque.com/thyname/flutter.widgets/overflowbar) 的子组件以溢出列形式布局时的水平对齐方式。

该值必须相对于当前环境的 [TextDirection](https://www.yuque.com/thyname/dart.ui/textdirection) 来解释。

当 [TextDirection.ltr] 时每个子组件左对齐，当 [TextDirection.rtl] 时右对齐。

当 [TextDirection.ltr] 时每个子组件右对齐，当 [TextDirection.rtl] 时左对齐。

每个子组件水平居中对齐。

# OverflowBar

```dart
class OverflowBar extends MultiChildRenderObjectWidget {}
```

一个将其 [children] 以行的形式布局的组件，除非它们“溢出”可用的水平空间，在这种情况下会改为以列的形式布局。

该组件的宽度会扩展以容纳其子组件以及指定的 [spacing]，直到发生溢出为止。溢出列将占用全部可用宽度。[overflowAlignment] 定义了每个子组件在溢出列中的对齐方式，[overflowSpacing] 定义了子组件之间的间距。

子组件在水平布局中出现的顺序由 [textDirection] 决定，这与 [Row](https://www.yuque.com/thyname/flutter.widgets/row) 组件的行为一致。如果布局发生溢出，则子组件在列中的顺序改为由 [overflowDirection] 指定。

{@tool dartpad} 此示例定义了一个简单的对话框布局示例，其中对话框操作按钮的布局由 [OverflowBar](https://www.yuque.com/thyname/flutter.widgets/overflowbar) 定义。内容被包裹在 [SingleChildScrollView](https://www.yuque.com/thyname/flutter.widgets/singlechildscrollview) 中，这样一来，如果发生溢出，无论垂直空间有多少，操作按钮仍可通过滚动访问。

** See code in examples/api/lib/widgets/overflow_bar/overflow_bar.0.dart ** {@end-tool}

### OverflowBar()

```dart
OverflowBar({dynamic key, double spacing = 0.0, MainAxisAlignment? alignment, double overflowSpacing = 0.0, OverflowBarAlignment overflowAlignment = OverflowBarAlignment.start, VerticalDirection overflowDirection = VerticalDirection.down, TextDirection? textDirection, List<Widget> children})
```

构造一个 OverflowBar。

### spacing

```dart
double spacing
```

默认水平布局中 [children] 之间的间隙宽度。

如果水平布局发生溢出，则改为使用 [overflowSpacing]。

默认值为 0.0。

### alignment

```dart
MainAxisAlignment? alignment
```

按照与 [Row.mainAxisAlignment] 相同的规则定义 [children] 的水平布局。

如果此属性非空，并且 [children]（以 [spacing] 分隔）能够容纳在可用宽度内，则该 overflow bar 会尽可能地扩展至最大宽度。如果子组件无法容纳在可用宽度内，则此属性将被忽略，转而应用 [overflowAlignment]。

如果此属性为 null（默认值），则该 overflow bar 的宽度仅为布局 [children]（以 [spacing] 分隔）所需的宽度，同时受传入约束的限制。

如果 [alignment] 为 [MainAxisAlignment.spaceAround]、[MainAxisAlignment.spaceBetween] 或 [MainAxisAlignment.spaceEvenly] 之一，则 [spacing] 参数仅用于判断水平布局是否会发生溢出。

默认值为 null。

另请参阅：

- [overflowAlignment]，即 [children] 在垂直“溢出”布局中的水平对齐方式。

### overflowSpacing

```dart
double overflowSpacing
```

垂直“溢出”布局中 [children] 之间的间隙高度。

仅当水平布局发生溢出时（即没有足够的水平空间容纳 [children] 和 [spacing] 时）才会使用此参数。

默认值为 0.0。

另请参阅：

- [spacing]，默认水平布局中每对子组件之间的间隙宽度。

### overflowAlignment

```dart
OverflowBarAlignment overflowAlignment
```

[children] 在垂直“溢出”布局中的水平对齐方式。

仅当水平布局发生溢出时（即没有足够的水平空间容纳 [children] 和 [spacing] 时）才会使用此参数。在这种情况下，overflow bar 会扩展以填满可用宽度，并将其 [children] 以列的形式布局。每个子组件在该列中的水平对齐方式由此参数和 [textDirection] 共同决定。如果 [textDirection] 为 [TextDirection.ltr]，则当取值为 [OverflowBarAlignment.start] 时，每个子组件将与可用空间的左边缘对齐；当取值为 [OverflowBarAlignment.end] 时，则与可用空间的右边缘对齐。类似地，如果 [textDirection] 为 [TextDirection.rtl]，则 [OverflowBarAlignment.start] 对应可用空间的右边缘，[OverflowBarAlignment.end] 对应左边缘。对于 [OverflowBarAlignment.center]，每个子组件将在可用空间内水平居中。

默认值为 [OverflowBarAlignment.start]。

另请参阅：

- [alignment]，当子组件（以 [spacing] 分隔）能够容纳在可用空间内时，定义 [children] 水平布局方式（依照与 [Row.mainAxisAlignment] 相同的规则）。
- [overflowDirection]，定义当水平布局发生溢出时 [OverflowBar](https://www.yuque.com/thyname/flutter.widgets/overflowbar) 的子组件出现的顺序。

### overflowDirection

```dart
VerticalDirection overflowDirection
```

定义当水平布局发生溢出时 [children] 出现的顺序。

仅当水平布局发生溢出时（即没有足够的水平空间容纳 [children] 和 [spacing] 时）才会使用此参数。

如果子组件无法排列在同一行中，则会以列的形式排列。如果此属性设置为 [VerticalDirection.down]，则第一个子组件位于列的顶部，因为它从顶部“开始”，在底部“结束”。另一方面，如果此属性设置为 [VerticalDirection.up]，则第一个子组件将位于列的底部，因为它从底部“开始”，在顶部“结束”。

默认值为 [VerticalDirection.down]。

另请参阅：

- [overflowAlignment]，定义子组件在垂直“溢出”布局中的水平对齐方式。

### textDirection

```dart
TextDirection? textDirection
```

决定 [children] 在默认水平布局中出现的顺序，以及在垂直溢出布局中 [OverflowBarAlignment.start] 和 [OverflowBarAlignment.end] 的解释方式。

对于默认水平布局，如果 [textDirection] 为 [TextDirection.rtl]，则最后一个子组件最先被布局。如果 [textDirection] 为 [TextDirection.ltr]，则第一个子组件最先被布局。

如果此参数为 null，则使用 `Directionality.of(context)` 的值。

另请参阅：

- [overflowDirection]，定义当水平布局发生溢出时 [OverflowBar](https://www.yuque.com/thyname/flutter.widgets/overflowbar) 的子组件出现的顺序。
- [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)，定义文本以及对文本方向敏感的渲染对象的环境方向性。

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
