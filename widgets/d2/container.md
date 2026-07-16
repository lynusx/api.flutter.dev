# DecoratedBox

```dart
class DecoratedBox extends SingleChildRenderObjectWidget {}
```

一个在其子组件绘制之前或之后绘制 [Decoration](https://www.yuque.com/thyname/flutter.painting/decoration) 的 Widget。

[Container](https://www.yuque.com/thyname/flutter.widgets/container) 会根据边框宽度为其子组件设置内边距；而此 Widget 不会。

常与 [BoxDecoration](https://www.yuque.com/thyname/flutter.painting/boxdecoration) 一起使用。

[child] 不会被裁剪。如需将子组件裁剪为特定 [ShapeDecoration](https://www.yuque.com/thyname/flutter.painting/shapedecoration) 的形状，可考虑使用 [ClipPath](https://www.yuque.com/thyname/flutter.widgets/clippath) Widget。

{@tool snippet}

此示例展示了一个径向渐变，在夜空中绘制出一轮明月：

```dart
const DecoratedBox(
  decoration: BoxDecoration(
    gradient: RadialGradient(
      center: Alignment(-0.5, -0.6),
      radius: 0.15,
      colors: <Color>[
        Color(0xFFEEEEEE),
        Color(0xFF111133),
      ],
      stops: <double>[0.9, 1.0],
    ),
  ),
)
```

{@end-tool}

另请参阅：

- [Ink](https://www.yuque.com/thyname/flutter.material/ink)，在 [Material](https://www.yuque.com/thyname/flutter.material/material) 上绘制 [Decoration](https://www.yuque.com/thyname/flutter.painting/decoration)，使 [InkResponse](https://www.yuque.com/thyname/flutter.material/inkresponse) 和 [InkWell](https://www.yuque.com/thyname/flutter.material/inkwell) 的水波纹效果可以覆盖在其上绘制。
- [DecoratedBoxTransition](https://www.yuque.com/thyname/flutter.widgets/decoratedboxtransition)，此类的动画版本，可对 [decoration] 属性进行动画处理。
- [Decoration](https://www.yuque.com/thyname/flutter.painting/decoration)，可通过继承它为 [DecoratedBox](https://www.yuque.com/thyname/flutter.widgets/decoratedbox) 提供其他效果。
- [CustomPaint](https://www.yuque.com/thyname/flutter.widgets/custompaint)，另一种从 Widget 层绘制自定义效果的方式。
- [DecoratedSliver](https://www.yuque.com/thyname/flutter.widgets/decoratedsliver)，将 [Decoration](https://www.yuque.com/thyname/flutter.painting/decoration) 应用于 sliver。

### DecoratedBox()

```dart
DecoratedBox({dynamic key, required Decoration decoration, DecorationPosition position = DecorationPosition.background, Widget? child})
```

创建一个绘制 [Decoration](https://www.yuque.com/thyname/flutter.painting/decoration) 的 Widget。

默认情况下，装饰绘制在子组件后面。

### decoration

```dart
Decoration decoration
```

要绘制的装饰。

通常为 [BoxDecoration](https://www.yuque.com/thyname/flutter.painting/boxdecoration)。

### position

```dart
DecorationPosition position
```

决定盒装饰绘制在子组件的后面还是前面。

### createRenderObject()

```dart
RenderDecoratedBox createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderDecoratedBox renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# Container

```dart
class Container extends StatelessWidget {}
```

一个组合了常见绘制、定位和尺寸调整 Widget 的便捷 Widget。

{@youtube 560 315 https://www.youtube.com/watch?v=c1xLMaTUWCY}

Container 首先用 [padding]（会因 [decoration] 中存在的任何边框而增大）包围子组件，然后对填充后的范围应用额外的 [constraints]（若 `width` 和 `height` 中任一非空，则将其纳入约束）。之后 Container 会被 [margin] 所描述的额外空白空间包围。

在绘制过程中，Container 首先应用给定的 [transform]，然后绘制 [decoration] 以填充带内边距的范围，接着绘制子组件，最后绘制 [foregroundDecoration]，同样填充带内边距的范围。

没有子组件的 Container 会尽可能变大，除非传入的约束是无边界的，在这种情况下它会尽可能变小。有子组件的 Container 会根据其子组件来调整自身尺寸。构造函数中的 `width`、`height` 和 [constraints] 参数会覆盖此行为。

默认情况下，Container 对所有命中测试均返回 false。如果指定了 [color] 属性，命中测试将由 [ColoredBox](https://www.yuque.com/thyname/flutter.widgets/coloredbox) 处理，其始终返回 true。如果指定了 [decoration] 或 [foregroundDecoration] 属性，命中测试将由 [Decoration.hitTest] 处理。

## 布局行为

_有关盒布局模型的介绍，请参阅 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints)。_

由于 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 组合了多个各自具有不同布局行为的 Widget，因此 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 的布局行为相对复杂。

概括来说，[Container](https://www.yuque.com/thyname/flutter.widgets/container) 会按以下顺序尝试：遵循 [alignment]、根据 [child] 调整自身尺寸、遵循 `width`、`height` 和 [constraints]、扩展以适应父组件、尽可能变小。

更具体地说：

如果该 Widget 没有 child、没有 `height`、没有 `width`、没有 [constraints]，且父组件提供的是无边界约束，则 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 会尝试尽可能变小。

如果该 Widget 没有 child、没有 [alignment]，但提供了 `height`、`width` 或 [constraints]，则 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 会根据这些约束与父组件约束的组合，尝试尽可能变小。

如果该 Widget 没有 child、没有 `height`、没有 `width`、没有 [constraints]，也没有 [alignment]，但父组件提供的是有边界约束，则 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 会扩展以适应父组件提供的约束。

如果该 Widget 具有 [alignment]，且父组件提供的是无边界约束，则 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 会尝试根据子组件调整自身尺寸。

如果该 Widget 具有 [alignment]，且父组件提供的是有边界约束，则 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 会尝试扩展以适应父组件，然后根据 [alignment] 在自身内部定位子组件。

否则，该 Widget 具有 [child]，但没有 `height`、没有 `width`、没有 [constraints]，也没有 [alignment]，此时 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 会将父组件的约束传递给子组件，并将自身尺寸调整为与子组件相匹配。

[margin] 和 [padding] 属性也会影响布局，具体如这两个属性的文档所述（它们的效果只是对上述规则的补充）。[decoration] 可以隐式地增加 [padding]（例如 [BoxDecoration](https://www.yuque.com/thyname/flutter.painting/boxdecoration) 中的边框会计入 [padding]）；参见 [Decoration.padding]。

## 示例

{@tool snippet} 此示例展示了一个 48x48 的琥珀色正方形（放置在 [Center](https://www.yuque.com/thyname/flutter.widgets/center) Widget 内，以防父 Widget 对 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 应采用的尺寸有自己的主张），并设置了 margin 使其与相邻 Widget 保持距离：

![An amber colored container with the dimensions of 48 square pixels.](https://flutter.github.io/assets-for-api-docs/assets/widgets/container_a.png)

```dart
Center(
  child: Container(
    margin: const EdgeInsets.all(10.0),
    color: Colors.amber[600],
    width: 48.0,
    height: 48.0,
  ),
)
```

{@end-tool}

{@tool snippet}

此示例展示了如何同时使用 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 的多个特性。[constraints] 被设置为在垂直方向上适应字体大小并留出充足的空间，同时在水平方向上扩展以适应父组件。[padding] 用于确保内容与文本之间留有间距。[color] 使该盒子呈现蓝色。[alignment] 使 [child] 在盒子中居中显示。最后，[transform] 对整个装置施加了轻微的旋转，以完成这一效果。

![A blue rectangular container with 'Hello World' in the center, rotated slightly in the z axis.](https://flutter.github.io/assets-for-api-docs/assets/widgets/container_b.png)

```dart
Container(
  constraints: BoxConstraints.expand(
    height: Theme.of(context).textTheme.headlineMedium!.fontSize! * 1.1 + 200.0,
  ),
  padding: const EdgeInsets.all(8.0),
  color: Colors.blue[600],
  alignment: Alignment.center,
  transform: Matrix4.rotationZ(0.1),
  child: Text('Hello World',
    style: Theme.of(context)
        .textTheme
        .headlineMedium!
        .copyWith(color: Colors.white)),
)
```

{@end-tool}

另请参阅：

- [AnimatedContainer](https://www.yuque.com/thyname/flutter.widgets/animatedcontainer)，一种在属性发生变化时能够平滑地进行动画过渡的变体。
- [Border](https://www.yuque.com/thyname/flutter.painting/border)，其中有一个大量使用 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 的示例。
- [Ink](https://www.yuque.com/thyname/flutter.material/ink)，在 [Material](https://www.yuque.com/thyname/flutter.material/material) 上绘制 [Decoration](https://www.yuque.com/thyname/flutter.painting/decoration)，使 [InkResponse](https://www.yuque.com/thyname/flutter.material/inkresponse) 和 [InkWell](https://www.yuque.com/thyname/flutter.material/inkwell) 的水波纹效果可以覆盖在其上绘制。
- Cookbook：[为容器的属性添加动画](https://docs.flutter.dev/cookbook/animation/animated-container)
- [布局 Widget 目录](https://docs.flutter.dev/ui/widgets/layout)。

### Container()

```dart
Container({dynamic key, AlignmentGeometry? alignment, EdgeInsetsGeometry? padding, Color? color, bool isAntiAlias = true, Decoration? decoration, Decoration? foregroundDecoration, double? width, double? height, BoxConstraints? constraints, EdgeInsetsGeometry? margin, Matrix4? transform, AlignmentGeometry? transformAlignment, Widget? child, Clip clipBehavior = Clip.none})
```

创建一个组合了常见绘制、定位和尺寸调整 Widget 的 Widget。

`height` 和 `width` 的值包含 padding。

`color` 和 `decoration` 参数不能同时提供，因为这可能导致装饰绘制在背景色之上。若要为装饰指定颜色，请使用 `decoration: BoxDecoration(color: color)`。

### child

```dart
Widget? child
```

Container 所包含的 [child]。

若为 null，且 [constraints] 为无边界或同样为 null，则 Container 会扩展以填满其父组件中所有可用空间，除非父组件提供的是无边界约束，在这种情况下 Container 会尝试尽可能变小。

{@macro flutter.widgets.ProxyWidget.child}

### alignment

```dart
AlignmentGeometry? alignment
```

在 Container 内对齐 [child]。

若非 null，Container 会扩展以填满其父组件，并根据给定的值在自身内部定位其子组件。若传入的约束是无边界的，则子组件将改为按需收缩包裹（shrink-wrapped）。

若 [child] 为 null，则此属性会被忽略。

另请参阅：

- [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，一个包含便捷常量的类，通常用于指定 [AlignmentGeometry](https://www.yuque.com/thyname/flutter.painting/alignmentgeometry)。
- [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)，类似于 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，用于指定相对于文本方向的对齐方式。

### padding

```dart
EdgeInsetsGeometry? padding
```

在 [decoration] 内部预留的空白空间。若存在 [child]，则会被放置在此内边距内部。

此内边距是在 [decoration] 自身固有内边距的基础上额外附加的；参见 [Decoration.padding]。

### color

```dart
Color? color
```

绘制在 [child] 后面的颜色。

当背景是纯色时，应优先使用此属性。对于渐变或图片等其他情况，请使用 [decoration] 属性。

如果使用了 [decoration]，则此属性必须为 null。即使此属性为 null，[decoration] 仍可能绘制出背景色。

### isAntiAlias

```dart
bool isAntiAlias
```

{@macro flutter.widgets.ColoredBox.isAntiAlias}

### decoration

```dart
Decoration? decoration
```

绘制在 [child] 后面的装饰。

使用 [color] 属性来指定简单的纯色。

[child] 不会被裁剪为装饰的形状。如需将子组件裁剪为特定 [ShapeDecoration](https://www.yuque.com/thyname/flutter.painting/shapedecoration) 的形状，可考虑使用 [ClipPath](https://www.yuque.com/thyname/flutter.widgets/clippath) Widget。

### foregroundDecoration

```dart
Decoration? foregroundDecoration
```

绘制在 [child] 前面的装饰。

### constraints

```dart
BoxConstraints? constraints
```

应用于子组件的额外约束。

构造函数的 `width` 和 `height` 参数会与 `constraints` 参数组合，共同设置此属性。

[padding] 位于约束内部。

### margin

```dart
EdgeInsetsGeometry? margin
```

环绕在 [decoration] 和 [child] 周围的空白空间。

### transform

```dart
Matrix4? transform
```

在绘制 Container 之前应用的变换矩阵。

### transformAlignment

```dart
AlignmentGeometry? transformAlignment
```

若指定了 [transform]，此属性表示相对于 Container 尺寸的原点对齐方式。

当 [transform] 为 null 时，此属性的值会被忽略。

另请参阅：

- [Transform.alignment]，由此属性设置。

### clipBehavior

```dart
Clip clipBehavior
```

当 [Container.decoration] 不为 null 时的裁剪行为。

默认为 [Clip.none]。若 [decoration] 为 null，则此属性必须为 [Clip.none]。

若要应用裁剪，所提供装饰的 [Decoration.getClipPath] 方法必须返回一个裁剪路径（并非所有装饰都支持此功能；该方法的默认实现会抛出 [UnsupportedError](https://www.yuque.com/thyname/dart.core/unsupportederror)）。
