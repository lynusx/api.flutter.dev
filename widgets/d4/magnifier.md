@docImport 'package:flutter/material.dart';

@docImport 'text_selection.dart';

# MagnifierBuilder

```dart
typedef MagnifierBuilder = Widget? Function(BuildContext context, MagnifierController controller, ValueNotifier<MagnifierInfo> magnifierInfo)
```

用于构建带有 [MagnifierController](https://www.yuque.com/thyname/flutter.widgets/magnifiercontroller) 的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 的构建器（builder）签名。

每个放大镜（magnifier）只会调用一次该构建器。

如果 `controller` 参数的 [MagnifierController.animationController] 字段被（由构建器）设置为一个 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)，[MagnifierController](https://www.yuque.com/thyname/flutter.widgets/magnifiercontroller) 将在放大镜进入和退出时驱动该动画。

`magnifierInfo` 参数会在所构建的放大镜的生命周期内不断更新为新的 [MagnifierInfo](https://www.yuque.com/thyname/flutter.widgets/magnifierinfo) 实例，例如当用户在文本字段中移动手指时。

# MagnifierInfo

```dart
class MagnifierInfo {}
```

一个数据类，包含用于定位放大镜的文本布局与选择手势的几何信息。

### MagnifierInfo()

```dart
MagnifierInfo({required Offset globalGesturePosition, required Rect caretRect, required Rect fieldBounds, required Rect currentLineBoundaries})
```

根据提供的几何值构造一个 [MagnifierInfo](https://www.yuque.com/thyname/flutter.widgets/magnifierinfo)。

### empty

```dart
MagnifierInfo empty
```

所有值均为 0 的常量 [MagnifierInfo](https://www.yuque.com/thyname/flutter.widgets/magnifierinfo)。

### globalGesturePosition

```dart
Offset globalGesturePosition
```

放大镜应显示位置的手势偏移量。

### currentLineBoundaries

```dart
Rect currentLineBoundaries
```

放大镜应显示位置所在当前行的矩形区域，不考虑字段的任何内边距，仅考虑首尾字符的位置。

### caretRect

```dart
Rect caretRect
```

放大镜应跟随的控制柄（handle）的矩形区域。

### fieldBounds

```dart
Rect fieldBounds
```

放大镜所绑定的整个文本字段的边界。

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# TextMagnifierConfiguration

```dart
class TextMagnifierConfiguration {}
```

放大镜（例如文本字段中的放大镜）的配置对象。

一般来说，放大镜的大多数功能特性都可以通过控制 [magnifierBuilder] 构建的组件来配置。

### TextMagnifierConfiguration()

```dart
TextMagnifierConfiguration({MagnifierBuilder? magnifierBuilder, bool shouldDisplayHandlesInMagnifier = true})
```

通过各组成部分构造一个 [TextMagnifierConfiguration](https://www.yuque.com/thyname/flutter.widgets/textmagnifierconfiguration)。

如果 [magnifierBuilder] 为 null，将使用一个不构建任何放大镜的默认 [MagnifierBuilder](https://www.yuque.com/thyname/flutter.widgets/magnifierbuilder)。

### magnifierBuilder

```dart
MagnifierBuilder get magnifierBuilder
```

创建渲染放大镜的组件的构建器回调函数。

### shouldDisplayHandlesInMagnifier

```dart
bool shouldDisplayHandlesInMagnifier
```

放大镜是否应显示文本编辑控制柄（handle）。

此标志由 [SelectionOverlay.showMagnifier] 用于控制渲染中图层的顺序；具体而言，即是否将包含控制柄的图层置于包含放大镜的图层之上或之下，二者均位于 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中。

### disabled

```dart
TextMagnifierConfiguration disabled
```

一个已禁用的 [TextMagnifierConfiguration](https://www.yuque.com/thyname/flutter.widgets/textmagnifierconfiguration) 常量，表示无论平台如何，都不会构建任何内容。

# MagnifierController

```dart
class MagnifierController {}
```

放大镜的控制器。

相较于直接持有一个原始的 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry)，[MagnifierController](https://www.yuque.com/thyname/flutter.widgets/magnifiercontroller) 的主要优势在于它能够处理等待放大镜完成进入或退出动画的相关逻辑。

如果放大镜选择使用进入/退出动画，则应将该动画控制器提供给 [MagnifierController.animationController]。[MagnifierController](https://www.yuque.com/thyname/flutter.widgets/magnifiercontroller) 随后会驱动该 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)，并在将其从 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中移除之前等待动画完成。

要检查放大镜的状态，请参见 [MagnifierController.shown]。

### MagnifierController()

```dart
MagnifierController({AnimationController? animationController})
```

如果放大镜没有进入/退出动画，[animationController] 应保持为 null。

### animationController

```dart
AnimationController? animationController
```

在触发显示/隐藏时，分别驱动进入/退出动画的控制器。

### overlayEntry

```dart
OverlayEntry? get overlayEntry
```

放大镜当前所在 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中的 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry)（如果存在）。

公开此属性是为了让其他的覆盖层条目（overlay entry）可以定位在该 [overlayEntry] 之上或之下。在此 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 中，位于 [RawMagnifier](https://www.yuque.com/thyname/flutter.widgets/rawmagnifier) 绘制顺序之后的任何内容都不会显示在放大镜中；如果希望某个覆盖层条目显示在放大镜中，则*必须*将其定位在放大镜下方。

{@tool snippet}

```dart
void magnifierShowExample(BuildContext context) {
  final MagnifierController myMagnifierController = MagnifierController();

  // Placed below the magnifier, so it will show.
  Overlay.of(context).insert(OverlayEntry(
      builder: (BuildContext context) => const Text('I WILL display in the magnifier')));

  // Will display in the magnifier, since this entry was passed to show.
  final OverlayEntry displayInMagnifier = OverlayEntry(
      builder: (BuildContext context) =>
          const Text('I WILL display in the magnifier'));

  Overlay.of(context)
      .insert(displayInMagnifier);
  myMagnifierController.show(
      context: context,
      below: displayInMagnifier,
      builder: (BuildContext context) => const RawMagnifier(
            size: Size(100, 100),
          ));

  // By default, new entries will be placed over the top entry.
  Overlay.of(context).insert(OverlayEntry(
      builder: (BuildContext context) => const Text('I WILL NOT display in the magnifier')));

  Overlay.of(context).insert(
      below:
          myMagnifierController.overlayEntry, // Explicitly placed below the magnifier.
      OverlayEntry(
          builder: (BuildContext context) => const Text('I WILL display in the magnifier')));
}
```

{@end-tool}

要检查放大镜是否位于覆盖层（overlay）中，请使用 [shown]。即使放大镜不可见，[overlayEntry] 字段也可能非空。

### shown

```dart
bool get shown
```

放大镜当前是否正在显示。

当覆盖层中没有任何内容、[animationController] 处于 [AnimationStatus.dismissed] 状态，或 [animationController] 正在执行退出动画（即处于 [AnimationStatus.reverse] 状态）时，此值为 false。

在相反的情况下则为 true，即当覆盖层不为空，并且 [animationController] 为 null，或处于 [AnimationStatus.completed] 状态，或处于 [AnimationStatus.forward] 状态时。

### show()

```dart
Future<void> show({required BuildContext context, required WidgetBuilder builder, Widget? debugRequiredFor, OverlayEntry? below})
```

显示放大镜。

返回一个 Future，当放大镜完全显示（即完成其进入动画）时该 Future 完成。

要控制放大镜中显示哪些覆盖层，请使用 `below`。有关如何使用 `below` 的更多详情，请参见 [overlayEntry]。

如果放大镜已存在（即 [overlayEntry] != null），则 [show] 会在不播放退出动画的情况下替换旧的覆盖层。可以考虑先等待 [hide] 完成，以便从旧放大镜过渡到新放大镜。

### hide()

```dart
Future<void> hide({bool removeFromOverlay = true})
```

安排隐藏放大镜。

如果此 [MagnifierController](https://www.yuque.com/thyname/flutter.widgets/magnifiercontroller) 具有 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)，则 [hide] 会反向执行该动画控制器，并等待动画完成。然后，如果 [removeFromOverlay] 为 true，则将放大镜从覆盖层中移除。

通常情况下，`removeFromOverlay` 应为 true，除非放大镜需要在显示/隐藏之间保留状态。

另请参见：

- [removeFromOverlay]，它会同步将 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 从 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中移除。

### removeFromOverlay()

```dart
void removeFromOverlay()
```

将 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 从 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中移除。

无论是否存在退出动画，此方法都会同步移除 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry)：这会导致带有动画的 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 被生硬地移除。

要让 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 播放其退出动画，可考虑改为调用 [hide]，并将 `removeFromOverlay` 设置为 true，同时可选择等待其返回的 Future。

### shiftWithinBounds()

```dart
Rect shiftWithinBounds({required Rect rect, required Rect bounds})
```

一个用于根据 [rect] 计算新 [Rect](https://www.yuque.com/thyname/dart.ui/rect) 的工具方法，使得计算得到的 [rect] 完全被约束在 [bounds] 之内。

输出矩形中的任意一点都保证同时也是 [bounds] 中包含的点。

如果 [rect] 的宽度大于 [bounds] 的宽度，则会在运行时产生错误；同样，如果 [rect] 的高度大于 [bounds] 的高度，也会产生错误。

此算法会将 [rect] 平移最短的距离，使其完全位于 [bounds] 之内。

如果 [rect] 已经位于 [bounds] 之内，则不会对 [rect] 应用任何平移，[rect] 将按原样返回。

输出矩形的某个点位于 [bounds] 的边缘上是完全合法的。如果所需的输出矩形要求没有任何边与 [bounds] 的边平行，请参见对 [bounds] 使用 [Rect.deflate] 缩小 1 来实现这一效果。

# MagnifierDecoration

```dart
class MagnifierDecoration {}
```

[RawMagnifier](https://www.yuque.com/thyname/flutter.widgets/rawmagnifier) 中放大镜周围的装饰。

另请参见：

- [Decoration](https://www.yuque.com/thyname/flutter.painting/decoration)，一种更通用的 [DecoratedBox](https://www.yuque.com/thyname/flutter.widgets/decoratedbox) 解决方案。

### MagnifierDecoration()

```dart
MagnifierDecoration({double opacity = 1.0, List<BoxShadow>? shadows, ShapeBorder shape = const RoundedRectangleBorder()})
```

构造一个 [MagnifierDecoration](https://www.yuque.com/thyname/flutter.widgets/magnifierdecoration)。

默认情况下，[MagnifierDecoration](https://www.yuque.com/thyname/flutter.widgets/magnifierdecoration) 是一个矩形放大镜，没有阴影，且完全不透明。

### opacity

```dart
double opacity
```

放大镜及其周围装饰的不透明度。

当此值为 1.0 时，放大后的图像以放大镜的 [shape] 形状显示。当此值小于 1.0 时，放大后的图像呈透明状态，可以透过它看到未放大的背景。

通常，此属性仅在为放大镜的进入和退出制作动画时才有用，因为透明的放大镜看起来会相当令人困惑。

### shadows

```dart
List<BoxShadow>? shadows
```

[shape] 投射的阴影列表。

如果阴影带有偏移，请考虑将 [RawMagnifier.clipBehavior] 设置为 [Clip.hardEdge]（或类似值），以确保阴影不会遮挡放大镜（阴影绘制在放大镜之上）。

如果阴影*没有*偏移，请考虑改为在阴影中使用 [BlurStyle.outer]，以避免需要引入裁剪。

如果 [shape] 由一组边框堆叠而成，阴影将根据最后一个边框的边界绘制。

另请参见：

- [kElevationToShadow](https://www.yuque.com/thyname/flutter.material/kelevationtoshadow)，其中定义了一些用于 Material 设计的阴影。这些阴影使用 [BlurStyle.normal]，在与 [MagnifierDecoration](https://www.yuque.com/thyname/flutter.widgets/magnifierdecoration) 一起使用时可能需要转换为 [BlurStyle.outer]。

### shape

```dart
ShapeBorder shape
```

放大镜的形状及其周围轮廓（边框）的形状。

形状可以堆叠（使用 `+` 运算符）。在这种情况下，放大镜和阴影将根据最后一个形状的外边缘绘制，边框则绘制在最上层。

# RawMagnifier

```dart
class RawMagnifier extends StatelessWidget {}
```

放大镜的通用基类。

{@tool dartpad} 此示例演示了放大镜是什么，以及如何使用它。

** 参见 examples/api/lib/widgets/magnifier/magnifier.0.dart 中的代码 ** {@end-tool}

{@template flutter.widgets.magnifier.intro} 这个放大镜适用于移动设备上的一些场景：当用户的手指可能遮住屏幕中正在执行精细操作（如通过拖动手势在图片或文本上导航一个微小的光标）的部分区域时非常有用。{@endtemplate}

可以使用 [MagnifierController](https://www.yuque.com/thyname/flutter.widgets/magnifiercontroller) 来方便地管理放大镜，它可以处理放大镜的显示与隐藏，并支持可选的进入/退出动画。

另请参见：

- [MagnifierController](https://www.yuque.com/thyname/flutter.widgets/magnifiercontroller)，用于处理覆盖层（overlay）中放大镜的控制器。

### RawMagnifier()

```dart
RawMagnifier({dynamic key, Widget? child, MagnifierDecoration decoration = const MagnifierDecoration(), Clip clipBehavior = Clip.none, Offset focalPointOffset = Offset.zero, double magnificationScale = 1, required Size size})
```

构造一个 [RawMagnifier](https://www.yuque.com/thyname/flutter.widgets/rawmagnifier)。

默认情况下，此放大镜使用默认的 [MagnifierDecoration](https://www.yuque.com/thyname/flutter.widgets/magnifierdecoration)（不绘制任何内容），焦点直接位于放大镜正下方，且不进行任何放大；这意味着默认的放大镜对肉眼来说是完全不可见的，它会精确地绘制其下方的内容，且位置与原始绘制位置完全相同。

### child

```dart
Widget? child
```

一个可选组件，用于定位在 [RawMagnifier](https://www.yuque.com/thyname/flutter.widgets/rawmagnifier) 的镜头（len）内部。

它被定位在 [RawMagnifier](https://www.yuque.com/thyname/flutter.widgets/rawmagnifier) 之上——可用于为 [RawMagnifier](https://www.yuque.com/thyname/flutter.widgets/rawmagnifier) 着色，或绘制类似十字准线的 UI。

### decoration

```dart
MagnifierDecoration decoration
```

此放大镜的装饰。

它用于设置放大镜的形状，以及所投射的任何边框和阴影。默认情况下没有边框，也没有阴影；结合默认的 [magnificationScale]（1.0），这会使放大镜没有任何可见效果。

如果 [decoration] 的 [MagnifierDecoration.shadows] 使用了带偏移的阴影，或使用了会遮挡放大图像的 [BlurStyle](https://www.yuque.com/thyname/dart.ui/blurstyle)，请考虑将 [clipBehavior] 设置为 [Clip.hardEdge]（或类似值），以确保放大后的图像可见。

### clipBehavior

```dart
Clip clipBehavior
```

是否以及如何裁剪在镜头内部渲染的 [decoration] 部分。

默认为 [Clip.none]。

参见 [decoration] 中的讨论。

### focalPointOffset

```dart
Offset focalPointOffset
```

放大镜焦点相对于 [RawMagnifier](https://www.yuque.com/thyname/flutter.widgets/rawmagnifier) 中心的偏移量。

{@template flutter.widgets.magnifier.offset} 例如，如果 [RawMagnifier](https://www.yuque.com/thyname/flutter.widgets/rawmagnifier) 的全局定位在 Offset(100, 100)，且 [focalPointOffset] 为 Offset(-20, -20)，那么 [RawMagnifier](https://www.yuque.com/thyname/flutter.widgets/rawmagnifier) 将显示全局偏移 (80, 80) 处的内容。

如果保持为 [Offset.zero]，[RawMagnifier](https://www.yuque.com/thyname/flutter.widgets/rawmagnifier) 将显示其正下方的内容。{@endtemplate}

### magnificationScale

```dart
double magnificationScale
```

放大对象在镜头中被"放大"的程度。

默认值为 1.0，即不进行放大。

### size

```dart
Size size
```

放大镜的大小。

此大小不包括 [decoration] 产生的边框，仅包括放大镜本身的大小。
