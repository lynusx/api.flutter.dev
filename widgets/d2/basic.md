@docImport 'dart:ui'; @docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart'; @docImport 'package:flutter/widgets.dart';

# Directionality

```dart
class Directionality extends _UbiquitousInheritedWidget {}
```

一个用于确定文本以及依赖文本方向的渲染对象所处环境方向的 Widget。

例如，[Padding](https://www.yuque.com/thyname/flutter.widgets/padding) 依赖 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 将 [EdgeInsetsDirectional](https://www.yuque.com/thyname/flutter.painting/edgeinsetsdirectional) 对象解析为绝对的 [EdgeInsets](https://www.yuque.com/thyname/flutter.painting/edgeinsets) 对象。

{@tool snippet}

此示例使用从右到左的 [TextDirection](https://www.yuque.com/thyname/dart.ui/textdirection)，并绘制一个右边距为 8 像素的蓝色盒子。

```dart
Directionality(
  textDirection: TextDirection.rtl,
  child: Container(
    margin: const EdgeInsetsDirectional.only(start: 8),
    color: Colors.blue,
  ),
)
```

{@end-tool}

### Directionality()

```dart
Directionality({dynamic key, required TextDirection textDirection, required Widget child})
```

创建一个用于确定文本以及依赖文本方向的渲染对象方向的 Widget。

### textDirection

```dart
TextDirection textDirection
```

此子树的文本方向。

### of()

```dart
TextDirection of(BuildContext context)
```

从包含给定上下文的最近的此类实例中获取文本方向。

如果在给定上下文的树中没有 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 祖先 Widget，则在调试模式下会抛出具有描述性信息的 [FlutterError](https://www.yuque.com/thyname/flutter.foundation/fluttererror)，在发布模式下会抛出异常。

典型用法如下：

```dart
TextDirection textDirection = Directionality.of(context);
```

另请参阅：

- [maybeOf]：如果树中没有 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 祖先 Widget，则返回 null。

### maybeOf()

```dart
TextDirection? maybeOf(BuildContext context)
```

从包含给定上下文的最近的此类实例中获取文本方向。

如果在给定上下文的树中没有 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 祖先 Widget，则返回 null。

典型用法如下：

```dart
TextDirection? textDirection = Directionality.maybeOf(context);
```

另请参阅：

- [of]：如果树中没有 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 祖先 Widget，则会抛出异常。

### updateShouldNotify()

```dart
bool updateShouldNotify(Directionality oldWidget)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# Opacity

```dart
class Opacity extends SingleChildRenderObjectWidget {}
```

一个使其子 Widget 部分透明的 Widget。

此类会将其子 Widget 绘制到一个中间缓冲区，然后以部分透明的方式将子 Widget 混合回场景中。

对于不是 0.0 和 1.0 的透明度值，此类的开销相对较大，因为它需要将子 Widget 绘制到中间缓冲区。当值为 0.0 时，完全不会绘制子 Widget。当值为 1.0 时，子 Widget 会被立即绘制，而不需要中间缓冲区。

默认具有透明背景的中间缓冲区的存在，可能会导致某些子 Widget 的行为有所不同。例如，[BackdropFilter](https://www.yuque.com/thyname/flutter.widgets/backdropfilter) 子 Widget 只能将其滤镜应用于此 Widget 与背景子 Widget 之间的内容，可能需要调整 [BackdropFilter.blendMode] 属性才能产生所需的效果。

{@youtube 560 315 https://www.youtube.com/watch?v=9hltevOHQBw}

{@tool snippet}

此示例展示了当 `_visible` 成员字段为 true 时显示某些 [Text](https://www.yuque.com/thyname/flutter.widgets/text)，为 false 时隐藏它：

```dart
Opacity(
  opacity: _visible ? 1.0 : 0.0,
  child: const Text("Now you see me, now you don't!"),
)
```

{@end-tool}

这比按需在树中添加和移除子 Widget 更高效。

## 透明度动画的性能考虑

直接对 [Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity) Widget 进行动画处理会导致该 Widget（及其可能的子树）在每一帧都重建，这样效率不高。可以考虑使用以下替代 Widget：

- [AnimatedOpacity](https://www.yuque.com/thyname/flutter.widgets/animatedopacity)：在内部使用动画来高效地对透明度进行动画处理。
- [FadeTransition](https://www.yuque.com/thyname/flutter.widgets/fadetransition)：使用提供的动画来高效地对透明度进行动画处理。

## 透明图片

如果只需要将单个 [Image](https://www.yuque.com/thyname/dart.ui/image) 或 [Color](https://www.yuque.com/thyname/dart.ui/color) 与介于 0.0 和 1.0 之间的透明度进行合成，直接使用它们而不使用 [Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity) Widget 会快得多。

例如，`Container(color: Color.fromRGBO(255, 0, 0, 0.5))` 比 `Opacity(opacity: 0.5, child: Container(color: Colors.red))` 快得多。

{@tool snippet}

以下示例在不使用 [Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity) 的情况下绘制了一张透明度为 0.5 的 [Image](https://www.yuque.com/thyname/dart.ui/image)：

```dart
Image.network(
  'https://raw.githubusercontent.com/flutter/assets-for-api-docs/main/packages/diagrams/assets/blend_mode_destination.jpeg',
  color: const Color.fromRGBO(255, 255, 255, 0.5),
  colorBlendMode: BlendMode.modulate
)
```

{@end-tool}

直接绘制带有透明度的 [Image](https://www.yuque.com/thyname/dart.ui/image) 或 [Color](https://www.yuque.com/thyname/dart.ui/color) 比在其上使用 [Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity) 更快，因为 [Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity) 可能会将透明度应用于一组 Widget，因此会使用代价高昂的离屏缓冲区。将内容绘制到离屏缓冲区中还可能触发渲染目标切换，而这种切换在较旧的 GPU 上速度尤其慢。

## 命中测试

将 [opacity] 设置为零并不会阻止对 [Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity) Widget 的后代 Widget 进行命中测试。这可能会让用户感到困惑，因为用户可能什么都看不到，并可能误以为 [Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity) 隐藏 Widget 的那部分界面是不可交互的。

对于某些仅在绘制时才计算其位置的 Widget（例如 [Flow](https://www.yuque.com/thyname/flutter.widgets/flow)），这实际上可能导致 bug（从意外的几何形状到异常），因为当 [opacity] 为零时，[Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity) Widget 根本不会绘制这些 Widget。

为避免此类问题，将 [opacity] 设置为零时，通常最好使用 [IgnorePointer](https://www.yuque.com/thyname/flutter.widgets/ignorepointer) Widget。这可以阻止与子树中任何子 Widget 的交互。

另请参阅：

- [Visibility](https://www.yuque.com/thyname/flutter.widgets/visibility)：可以更高效地隐藏子 Widget（尽管不够精细，因为它只有可见或隐藏两种状态，而不支持小数透明度值）。具体来说，[Visibility.maintain] 构造函数等效于使用值为 `0.0` 或 `1.0` 的 opacity Widget。
- [ShaderMask](https://www.yuque.com/thyname/flutter.widgets/shadermask)：可以为其子 Widget 应用更复杂的效果。
- [Transform](https://www.yuque.com/thyname/flutter.widgets/transform)：在绘制时对其子 Widget 应用任意变换。
- [SliverOpacity](https://www.yuque.com/thyname/flutter.widgets/sliveropacity)：此 Widget 的 sliver 版本。

### Opacity()

```dart
Opacity({dynamic key, required double opacity, bool alwaysIncludeSemantics = false, Widget? child})
```

创建一个使其子 Widget 部分透明的 Widget。

[opacity] 参数必须介于零和一之间（包含两端）。

### opacity

```dart
double opacity
```

用于缩放子 Widget alpha 值的比例。

透明度为一表示完全不透明。透明度为零表示完全透明（即不可见）。

值为一和零时会使用快速路径进行绘制。其他值则需要将子 Widget 绘制到中间缓冲区中，这样开销较大。

### alwaysIncludeSemantics

```dart
bool alwaysIncludeSemantics
```

是否始终包含子 Widget 的语义信息。

默认为 false。

当为 true 时，无论透明度设置如何，子 Widget 的语义信息都会像该 Widget 完全可见一样被暴露出来。这在动画期间标签可能被隐藏、但原本会提供相关语义信息的情况下非常有用。

### createRenderObject()

```dart
RenderOpacity createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderOpacity renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ShaderMask

```dart
class ShaderMask extends SingleChildRenderObjectWidget {}
```

一个将由 [Shader](https://www.yuque.com/thyname/dart.ui/shader) 生成的遮罩应用于其子 Widget 的 Widget。

例如，[ShaderMask](https://www.yuque.com/thyname/flutter.widgets/shadermask) 可用于通过 [RadialGradient](https://www.yuque.com/thyname/flutter.painting/radialgradient) 遮罩逐渐淡出子 Widget 的边缘。

{@youtube 560 315 https://www.youtube.com/watch?v=7sUL66pTQ7Q}

{@tool snippet}

此示例使文本看起来像着火了一样：

```dart
ShaderMask(
  shaderCallback: (Rect bounds) {
    return RadialGradient(
      center: Alignment.topLeft,
      radius: 1.0,
      colors: <Color>[Colors.yellow, Colors.deepOrange.shade900],
      tileMode: TileMode.mirror,
    ).createShader(bounds);
  },
  child: const Text(
    "I'm burning the memories",
    style: TextStyle(color: Colors.white),
  ),
)
```

{@end-tool}

另请参阅：

- [Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity)：可以为其子 Widget 应用统一的 alpha 效果。
- [CustomPaint](https://www.yuque.com/thyname/flutter.widgets/custompaint)：允许你直接在画布上进行绘制。
- [DecoratedBox](https://www.yuque.com/thyname/flutter.widgets/decoratedbox)：装饰子 Widget 的另一种方式。
- [BackdropFilter](https://www.yuque.com/thyname/flutter.widgets/backdropfilter)：将图像滤镜应用于背景。

### ShaderMask()

```dart
ShaderMask({dynamic key, required ShaderCallback shaderCallback, BlendMode blendMode = BlendMode.modulate, Widget? child})
```

创建一个将由 [Shader](https://www.yuque.com/thyname/dart.ui/shader) 生成的遮罩应用于其子 Widget 的 Widget。

### shaderCallback

```dart
ShaderCallback shaderCallback
```

调用此回调以创建生成遮罩的 [dart:ui.Shader]。

调用该着色器回调时会传入子 Widget 的当前大小，以便根据子 Widget 的大小和位置自定义着色器。

通常会使用 [LinearGradient](https://www.yuque.com/thyname/flutter.painting/lineargradient)、[RadialGradient](https://www.yuque.com/thyname/flutter.painting/radialgradient) 或 [SweepGradient](https://www.yuque.com/thyname/flutter.painting/sweepgradient) 来创建 [dart:ui.Shader]，不过也可以使用 [dart:ui.ImageShader] 类。

### blendMode

```dart
BlendMode blendMode
```

将着色器应用于子 Widget 时使用的 [BlendMode](https://www.yuque.com/thyname/dart.ui/blendmode)。

默认值 [BlendMode.modulate] 适用于对子 Widget 应用 alpha 混合。其他混合模式可用于创建其他效果。

### createRenderObject()

```dart
RenderShaderMask createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderShaderMask renderObject)
```

# BackdropGroup

```dart
class BackdropGroup extends InheritedWidget {}
```

一个为所有选择使用它的子 [BackdropFilter](https://www.yuque.com/thyname/flutter.widgets/backdropfilter) Widget 建立共享背景层的 Widget。

共享背景滤镜层可以提升多个背景滤镜的性能。要选择使用共享的 [BackdropGroup](https://www.yuque.com/thyname/flutter.widgets/backdropgroup)，必须使用特殊的 [BackdropFilter.grouped] 构造函数。

### BackdropGroup()

```dart
BackdropGroup({dynamic key, required Widget child, BackdropKey? backdropKey})
```

创建一个新的 [BackdropGroup](https://www.yuque.com/thyname/flutter.widgets/backdropgroup) Widget。

### backdropKey

```dart
BackdropKey backdropKey
```

此背景组将与共享子层一起使用的背景键。

### updateShouldNotify()

```dart
bool updateShouldNotify(BackdropGroup oldWidget)
```

### of()

```dart
BackdropGroup? of(BuildContext context)
```

查找最近的 [BackdropGroup](https://www.yuque.com/thyname/flutter.widgets/backdropgroup)，如果不存在则返回 `null`。

# BackdropFilter

```dart
class BackdropFilter extends SingleChildRenderObjectWidget {}
```

一个将滤镜应用于现有已绘制内容、然后绘制 [child] 的 Widget。

该滤镜将应用于其父级或祖先 Widget 裁剪范围内的所有区域。如果没有裁剪，则该滤镜将应用于整个屏幕。

滤镜的结果将使用 [blendMode] 参数混合回背景中。{@template flutter.widgets.BackdropFilter.blendMode} 所有平台都支持的 [blendMode] 唯一取值是 [BlendMode.srcOver]，它适用于大多数场景。但当 [BackdropFilter](https://www.yuque.com/thyname/flutter.widgets/backdropfilter) 的父级使用了临时缓冲区（save layer）时（例如 [Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity) Widget），该值可能会产生意外的结果。在这种情况下，使用 [BlendMode.src] 值可以产生更令人满意的效果。{@endtemplate}

如果多个背景滤镜 Widget 共享同一个 [BackdropKey](https://www.yuque.com/thyname/flutter.rendering/backdropkey)，Flutter 引擎可以将这些背景滤镜合并为单次渲染操作。背景键唯一标识了背景滤镜的输入，当该键被共享时，表示滤镜处理只需执行一次。这可以显著降低在同一场景中使用多个背景滤镜的开销。该键既可以通过 `backdropKey` 构造函数参数手动提供，也可以通过 `.grouped` 构造函数从 [BackdropGroup](https://www.yuque.com/thyname/flutter.widgets/backdropgroup) 继承 Widget 中查找获得。

相互重叠的背景滤镜不应使用相同的背景键，否则在重叠区域中的效果可能看起来就像只应用了一个滤镜。

以下代码片段演示了如何使用背景键让每个列表项都能高效地实现模糊效果。引擎只会执行一次背景模糊操作，但效果在视觉上与多次模糊完全相同。

```dart
 Widget build(BuildContext context) {
   return BackdropGroup(
     child: ListView.builder(
       itemCount: 60,
       itemBuilder: (BuildContext context, int index) {
         return ClipRect(
           child: BackdropFilter.grouped(
             filter: ui.ImageFilter.blur(
               sigmaX: 40,
               sigmaY: 40,
             ),
             child: Container(
               color: Colors.black.withValues(alpha: 0.2),
               height: 200,
               child: const Text('Blur item'),
             ),
           ),
         );
      }
    ),
  );
}
```

{@youtube 560 315 https://www.youtube.com/watch?v=dYRs7Q1vfYI}

{@tool snippet}

如果需要将 [BackdropFilter](https://www.yuque.com/thyname/flutter.widgets/backdropfilter) 应用于与其子 Widget 完全匹配的区域，请使用一个精确裁剪到该子 Widget 的裁剪 Widget 来包裹 [BackdropFilter](https://www.yuque.com/thyname/flutter.widgets/backdropfilter)。

```dart
Stack(
  fit: StackFit.expand,
  children: <Widget>[
    Text('0' * 10000),
    Center(
      child: ClipRect(  // <-- clips to the 200x200 [Container] below
        child: BackdropFilter(
          filter: ui.ImageFilter.blur(
            sigmaX: 5.0,
            sigmaY: 5.0,
          ),
          child: Container(
            alignment: Alignment.center,
            width: 200.0,
            height: 200.0,
            child: const Text('Hello World'),
          ),
        ),
      ),
    ),
  ],
)
```

{@end-tool}

此效果的开销相对较大，尤其是当滤镜是非局部性的（例如模糊）时。

如果你只是想将 [ImageFilter](https://www.yuque.com/thyname/dart.ui/imagefilter) 应用于单个 Widget（而不是应用于某个 Widget _下方_ 的所有内容），请改用 [ImageFiltered](https://www.yuque.com/thyname/flutter.widgets/imagefiltered)。对于这种场景，[ImageFiltered](https://www.yuque.com/thyname/flutter.widgets/imagefiltered) 既比 [BackdropFilter](https://www.yuque.com/thyname/flutter.widgets/backdropfilter) 更易用，开销也更低。

{@tool snippet}

此示例展示了如何将对单个同级 Widget 应用 [BackdropFilter](https://www.yuque.com/thyname/flutter.widgets/backdropfilter) 模糊这一常见情况替换为 [ImageFiltered](https://www.yuque.com/thyname/flutter.widgets/imagefiltered) Widget。这段代码通常更简单，并且对于像模糊这样复杂的滤镜，性能会得到显著提升。

以下实现的开销是不必要的。

```dart
 Widget buildBackdrop() {
   return Stack(
     children: <Widget>[
       Positioned.fill(child: Image.asset('image.png')),
       Positioned.fill(
         child: BackdropFilter(
           filter: ui.ImageFilter.blur(sigmaX: 6, sigmaY: 6),
         ),
       ),
     ],
   );
 }
```

{@end-tool} {@tool snippet}

相反，可以考虑采用以下方式，直接对子 Widget 应用模糊效果。

```dart
 Widget buildFilter() {
   return ImageFiltered(
     imageFilter: ui.ImageFilter.blur(sigmaX: 6, sigmaY: 6),
     child: Image.asset('image.png'),
   );
 }
```

{@end-tool}

另请参阅：

- [ImageFiltered](https://www.yuque.com/thyname/flutter.widgets/imagefiltered)：将 [ImageFilter](https://www.yuque.com/thyname/dart.ui/imagefilter) 应用于其子 Widget。
- [DecoratedBox](https://www.yuque.com/thyname/flutter.widgets/decoratedbox)：在 Widget 下方（或上方）绘制背景。
- [Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity)：改变 Widget 自身的透明度。
- 关于需要对 iOS PlatformView 进行模糊处理时的详细信息和限制，请参见 https://flutter.dev/go/ios-platformview-backdrop-filter-blur。

### BackdropFilter()

```dart
BackdropFilter({dynamic key, ui.ImageFilter? filter, ImageFilterConfig? filterConfig, Widget? child, BlendMode blendMode = BlendMode.srcOver, bool enabled = true, BackdropKey? backdropGroupKey})
```

创建一个背景滤镜。

[blendMode] 参数默认值为 [BlendMode.srcOver]，如果提供该参数，则不能为 null。

必须且只能提供 [filter] 或 [filterConfig] 中的一个。同时提供或都不提供都会导致断言错误。

### BackdropFilter.grouped()

```dart
BackdropFilter.grouped({dynamic key, ui.ImageFilter? filter, ImageFilterConfig? filterConfig, Widget? child, BlendMode blendMode = BlendMode.srcOver, bool enabled = true})
```

创建一个与最近的父级 [BackdropGroup](https://www.yuque.com/thyname/flutter.widgets/backdropgroup) 进行分组的背景滤镜。

[blendMode] 参数默认值为 [BlendMode.srcOver]，如果提供该参数，则不能为 null。

此构造函数会自动查找最近的 [BackdropGroup](https://www.yuque.com/thyname/flutter.widgets/backdropgroup)，并与同级和子级 [BackdropFilter](https://www.yuque.com/thyname/flutter.widgets/backdropfilter) Widget 共享背景输入。

必须且只能提供 [filter] 或 [filterConfig] 中的一个。同时提供或都不提供都会导致断言错误。

### filter

```dart
ui.ImageFilter? filter
```

在绘制子 Widget 之前应用于现有已绘制内容的图像滤镜。

例如，可以考虑使用 [ImageFilter.blur] 来创建背景模糊效果。

[filter] 参数（借助 [ImageFilterConfig.new] 构造函数）等效于 [filterConfig]，仅有仅由 [ImageFilterConfig](https://www.yuque.com/thyname/flutter.rendering/imagefilterconfig) 支持的功能除外（例如 [ImageFilterConfig.blur] 中的 `bounds` 参数）。

### filterConfig

```dart
ImageFilterConfig? filterConfig
```

应用于现有已绘制内容的图像滤镜配置。

例如，可以考虑使用 [ImageFilterConfig.blur] 来创建背景模糊效果。

[filterConfig] 参数（借助 [ImageFilterConfig.new] 构造函数）等效于 [filter]，仅有仅由 [ImageFilterConfig](https://www.yuque.com/thyname/flutter.rendering/imagefilterconfig) 支持的功能除外（例如 [ImageFilterConfig.blur] 中的 `bounds` 参数）。

### blendMode

```dart
BlendMode blendMode
```

将经过滤镜处理的背景内容应用到背景表面时所使用的混合模式。

{@macro flutter.widgets.BackdropFilter.blendMode}

### enabled

```dart
bool enabled
```

是否将背景滤镜操作应用于此 Widget 的子 Widget。

出于性能考虑，建议将 enabled 设置为 `false`，而不是创建一个"无操作"的滤镜类型。

### backdropGroupKey

```dart
BackdropKey? backdropGroupKey
```

标识此滤镜将应用于哪个背景的 [BackdropKey](https://www.yuque.com/thyname/flutter.rendering/backdropkey)。

背景键的默认值为 `null`。

### createRenderObject()

```dart
RenderBackdropFilter createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderBackdropFilter renderObject)
```

# CustomPaint

```dart
class CustomPaint extends SingleChildRenderObjectWidget {}
```

一个在绘制阶段提供画布供其绘制的 Widget。

当被要求进行绘制时，[CustomPaint](https://www.yuque.com/thyname/flutter.widgets/custompaint) 首先要求其 [painter] 在当前画布上绘制，然后绘制其子 Widget，在绘制完子 Widget 之后，再要求其 [foregroundPainter] 进行绘制。画布的坐标系与 [CustomPaint](https://www.yuque.com/thyname/flutter.widgets/custompaint) 对象的坐标系相匹配。绘制器应在一个从原点开始、覆盖给定大小区域的矩形内进行绘制。（如果绘制器在这些边界之外进行绘制，可能没有分配足够的内存来光栅化绘制指令，由此产生的行为是未定义的。）为了强制在这些边界内进行绘制，可以考虑用 [ClipRect](https://www.yuque.com/thyname/flutter.widgets/cliprect) Widget 包裹此 [CustomPaint](https://www.yuque.com/thyname/flutter.widgets/custompaint)。

绘制器是通过继承 [CustomPainter](https://www.yuque.com/thyname/flutter.rendering/custompainter) 来实现的。

{@youtube 560 315 https://www.youtube.com/watch?v=kp14Y4uHpHs}

由于自定义绘制会在绘制期间调用其绘制器，因此不能在回调中调用 `setState` 或 `markNeedsLayout`（该帧的布局已经完成）。

自定义绘制器通常会将自身大小设置为与其 [child] 相同。如果没有子 Widget，则会尝试将自身大小设为指定的 [size]，其默认值为 [Size.zero]。父级[可能会对此大小施加约束](https://docs.flutter.dev/ui/layout/constraints)。

[isComplex] 和 [willChange] 属性是给合成器的光栅缓存的提示。

{@tool snippet}

此示例展示了如何在 [CustomPaint](https://www.yuque.com/thyname/flutter.widgets/custompaint) Widget 中使用 [CustomPainter](https://www.yuque.com/thyname/flutter.rendering/custompainter) 处所示的示例自定义绘制器，为一些文本显示背景。

```dart
CustomPaint(
  painter: Sky(),
  child: const Center(
    child: Text(
      'Once upon a time...',
      style: TextStyle(
        fontSize: 40.0,
        fontWeight: FontWeight.w900,
        color: Color(0xFFFFFFFF),
      ),
    ),
  ),
)
```

{@end-tool}

另请参阅：

- [CustomPainter](https://www.yuque.com/thyname/flutter.rendering/custompainter)：创建自定义绘制器时需要继承的类。
- [Canvas](https://www.yuque.com/thyname/dart.ui/canvas)：自定义绘制器用于绘制的类。

### CustomPaint()

```dart
CustomPaint({dynamic key, CustomPainter? painter, CustomPainter? foregroundPainter, Size size = Size.zero, bool isComplex = false, bool willChange = false, Widget? child})
```

创建一个将绘制工作委托出去的 Widget。

### painter

```dart
CustomPainter? painter
```

在子 Widget 之前进行绘制的绘制器。

### foregroundPainter

```dart
CustomPainter? foregroundPainter
```

在子 Widget 之后进行绘制的绘制器。

### size

```dart
Size size
```

在没有子 Widget 的情况下，此 [CustomPaint](https://www.yuque.com/thyname/flutter.widgets/custompaint) 在给定布局约束下应达到的目标大小。

默认为 [Size.zero]。

如果存在子 Widget，则忽略此项，转而使用子 Widget 的大小。

### isComplex

```dart
bool isComplex
```

绘制内容是否足够复杂，从而可以从缓存中受益。

合成器包含一个光栅缓存，用于保存各层的位图，以避免在每一帧重复渲染这些层所带来的开销。如果未设置此标志，合成器将采用自身的启发式方法来判断包含此 Widget 的层是否足够复杂，从而可以从缓存中受益。

如果 [painter] 和 [foregroundPainter] 均为 null，则不能将此标志设置为 true，因为在这种情况下该标志会被忽略。

### willChange

```dart
bool willChange
```

是否应告知光栅缓存该绘制内容在下一帧很可能会发生变化。

此提示会告知合成器不要缓存包含此 Widget 的层，因为该缓存在未来不会被使用。如果未设置此提示，合成器将采用自身的启发式方法来判断该层未来是否可能被重复使用。

如果 [painter] 和 [foregroundPainter] 均为 null，则不能将此标志设置为 true，因为在这种情况下该标志会被忽略。

### createRenderObject()

```dart
RenderCustomPaint createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderCustomPaint renderObject)
```

### didUnmountRenderObject()

```dart
void didUnmountRenderObject(RenderCustomPaint renderObject)
```

# ClipRect

```dart
class ClipRect extends SingleChildRenderObjectWidget {}
```

一个使用矩形裁剪其子 Widget 的 Widget。

默认情况下，[ClipRect](https://www.yuque.com/thyname/flutter.widgets/cliprect) 会阻止其子 Widget 在其边界之外进行绘制，但可以使用自定义的 [clipper] 来自定义裁剪矩形的大小和位置。

[ClipRect](https://www.yuque.com/thyname/flutter.widgets/cliprect) 通常与以下这些经常在其边界之外进行绘制的 Widget 搭配使用：

- [CustomPaint](https://www.yuque.com/thyname/flutter.widgets/custompaint)
- [CustomSingleChildLayout](https://www.yuque.com/thyname/flutter.widgets/customsinglechildlayout)
- [CustomMultiChildLayout](https://www.yuque.com/thyname/flutter.widgets/custommultichildlayout)
- [Align](https://www.yuque.com/thyname/flutter.widgets/align) 和 [Center](https://www.yuque.com/thyname/flutter.widgets/center)（例如，当 [Align.widthFactor] 或 [Align.heightFactor] 小于 1.0 时）。
- [OverflowBox](https://www.yuque.com/thyname/flutter.widgets/overflowbox)
- [SizedOverflowBox](https://www.yuque.com/thyname/flutter.widgets/sizedoverflowbox)

{@tool snippet}

例如，通过将 [ClipRect](https://www.yuque.com/thyname/flutter.widgets/cliprect) 与 [Align](https://www.yuque.com/thyname/flutter.widgets/align) 结合使用，可以只显示 [Image](https://www.yuque.com/thyname/dart.ui/image) 的上半部分：

```dart
ClipRect(
  child: Align(
    alignment: Alignment.topCenter,
    heightFactor: 0.5,
    child: Image.network(userAvatarUrl),
  ),
)
```

{@end-tool}

另请参阅：

- [CustomClipper](https://www.yuque.com/thyname/flutter.rendering/customclipper)：有关创建自定义裁剪的信息。
- [ClipRRect](https://www.yuque.com/thyname/flutter.widgets/cliprrect)：带圆角的裁剪。
- [ClipOval](https://www.yuque.com/thyname/flutter.widgets/clipoval)：椭圆形裁剪。
- [ClipPath](https://www.yuque.com/thyname/flutter.widgets/clippath)：任意形状的裁剪。

### ClipRect()

```dart
ClipRect({dynamic key, CustomClipper<Rect>? clipper, Clip clipBehavior = Clip.hardEdge, Widget? child})
```

创建一个矩形裁剪。

如果 [clipper] 为 null，则裁剪范围将与子 Widget 的布局大小和位置相匹配。

如果 [clipBehavior] 为 [Clip.none]，则不会应用任何裁剪。

### clipper

```dart
CustomClipper<Rect>? clipper
```

如果非空，则决定使用哪种裁剪方式。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.rendering.ClipRectLayer.clipBehavior}

默认为 [Clip.hardEdge]。

### createRenderObject()

```dart
RenderClipRect createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderClipRect renderObject)
```

### didUnmountRenderObject()

```dart
void didUnmountRenderObject(RenderClipRect renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ClipRRect

```dart
class ClipRRect extends SingleChildRenderObjectWidget {}
```

一个使用圆角矩形裁剪其子 Widget 的 Widget。

默认情况下，[ClipRRect](https://www.yuque.com/thyname/flutter.widgets/cliprrect) 使用自身的边界作为裁剪的基础矩形，但可以使用自定义的 [clipper] 来自定义裁剪的大小和位置。

{@youtube 560 315 https://www.youtube.com/watch?v=eI43jkQkrvs}

{@tool dartpad} 此示例展示了应用于容器的各种 [ClipRRect](https://www.yuque.com/thyname/flutter.widgets/cliprrect)。

** See code in examples/api/lib/widgets/basic/clip_rrect.0.dart ** {@end-tool}

## 疑难解答

### 为什么我的 [ClipRRect](https://www.yuque.com/thyname/flutter.widgets/cliprrect) 子 Widget 没有圆角？

当 [ClipRRect](https://www.yuque.com/thyname/flutter.widgets/cliprrect) 比其所包含的子 Widget 大时，其圆角可能会被绘制在意想不到的位置。请确保 [ClipRRect](https://www.yuque.com/thyname/flutter.widgets/cliprrect) 及其子 Widget 具有相同的边界（可以使用 [FittedBox](https://www.yuque.com/thyname/flutter.widgets/fittedbox) 缩小 [ClipRRect](https://www.yuque.com/thyname/flutter.widgets/cliprrect)，或者放大子 Widget）。

{@tool dartpad} 此示例展示了一个为图片添加圆角的 [ClipRRect](https://www.yuque.com/thyname/flutter.widgets/cliprrect)。

** See code in examples/api/lib/widgets/basic/clip_rrect.1.dart ** {@end-tool}

另请参阅：

- [CustomClipper](https://www.yuque.com/thyname/flutter.rendering/customclipper)：有关创建自定义裁剪的信息。
- [ClipRect](https://www.yuque.com/thyname/flutter.widgets/cliprect)：不带圆角的更高效裁剪。
- [ClipRSuperellipse](https://www.yuque.com/thyname/flutter.widgets/cliprsuperellipse)：一种类似的裁剪形状，在直边与圆角之间具有更平滑的过渡。此形状与苹果设计语言中常用的圆角矩形非常接近，类似于 SwiftUI 中带有 `.continuous` 圆角样式的 `RoundedRectangle` 形状。
- [ClipOval](https://www.yuque.com/thyname/flutter.widgets/clipoval)：椭圆形裁剪。
- [ClipPath](https://www.yuque.com/thyname/flutter.widgets/clippath)：任意形状的裁剪。

### ClipRRect()

```dart
ClipRRect({dynamic key, BorderRadiusGeometry borderRadius = BorderRadius.zero, CustomClipper<RRect>? clipper, Clip clipBehavior = Clip.antiAlias, Widget? child})
```

创建一个圆角矩形裁剪。

[borderRadius] 默认为 [BorderRadius.zero]，即一个直角矩形。

如果 [clipper] 非空，则忽略 [borderRadius]。

如果 [clipBehavior] 为 [Clip.none]，则不会应用任何裁剪。

### borderRadius

```dart
BorderRadiusGeometry borderRadius
```

圆角的边框半径。

数值会被限制，以确保水平和垂直方向的半径之和不超过宽度/高度。

如果 [clipper] 非空，则忽略此值。

### clipper

```dart
CustomClipper<RRect>? clipper
```

如果非空，则决定使用哪种裁剪方式。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.rendering.ClipRectLayer.clipBehavior}

默认为 [Clip.antiAlias]。

### createRenderObject()

```dart
RenderClipRRect createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderClipRRect renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ClipRSuperellipse

```dart
class ClipRSuperellipse extends SingleChildRenderObjectWidget {}
```

一个使用圆角超椭圆裁剪其子 Widget 的 Widget。

圆角超椭圆是一种类似于典型圆角矩形（[ClipRRect](https://www.yuque.com/thyname/flutter.widgets/cliprrect)）的形状，但在直边与圆角之间具有更平滑的过渡。它类似于 SwiftUI 中带有 `.continuous` 圆角样式的 `RoundedRectangle` 形状。从技术上讲，它是通过用圆弧替换超椭圆（也称为拉梅曲线）的四个角而创建的。

默认情况下，[ClipRSuperellipse](https://www.yuque.com/thyname/flutter.widgets/cliprsuperellipse) 使用自身的边界作为裁剪的基础矩形，但可以使用自定义的 [clipper] 来自定义裁剪的大小和位置。

另请参阅：

- [CustomClipper](https://www.yuque.com/thyname/flutter.rendering/customclipper)：有关创建自定义裁剪的信息。
- [ClipRect](https://www.yuque.com/thyname/flutter.widgets/cliprect)：不带圆角的更高效裁剪。
- [ClipRRect](https://www.yuque.com/thyname/flutter.widgets/cliprrect)：一种典型的圆角矩形，通过用圆弧替换矩形的四个角而创建。
- [ClipOval](https://www.yuque.com/thyname/flutter.widgets/clipoval)：椭圆形裁剪。
- [ClipPath](https://www.yuque.com/thyname/flutter.widgets/clippath)：任意形状的裁剪。

### ClipRSuperellipse()

```dart
ClipRSuperellipse({dynamic key, BorderRadiusGeometry borderRadius = BorderRadius.zero, CustomClipper<RSuperellipse>? clipper, Clip clipBehavior = Clip.antiAlias, Widget? child})
```

创建一个圆角超椭圆裁剪。

[borderRadius] 默认为 [BorderRadius.zero]，即一个直角矩形。

如果 [clipBehavior] 为 [Clip.none]，则不会应用任何裁剪。

### borderRadius

```dart
BorderRadiusGeometry borderRadius
```

圆角的边框半径。

数值会被限制，以确保水平和垂直方向的半径之和不超过宽度/高度。

如果 [clipper] 非空，则忽略此值。

### clipper

```dart
CustomClipper<RSuperellipse>? clipper
```

如果非空，则决定使用哪种裁剪方式。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.rendering.ClipRectLayer.clipBehavior}

默认为 [Clip.antiAlias]。

### createRenderObject()

```dart
RenderClipRSuperellipse createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderClipRSuperellipse renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ClipOval

```dart
class ClipOval extends SingleChildRenderObjectWidget {}
```

一个使用椭圆裁剪其子 Widget 的 Widget。

{@youtube 560 315 https://www.youtube.com/watch?v=vzWWDO6whIM}

默认情况下，会在其布局尺寸内内接一个与坐标轴对齐的椭圆，并阻止其子 Widget 在该椭圆之外进行绘制，但可以使用自定义的 [clipper] 来自定义裁剪椭圆的大小和位置。

{@tool snippet}

此示例使用椭圆裁剪一张猫的图片。

```dart
ClipOval(
  child: Image.asset('images/cat.png'),
)
```

{@end-tool}

另请参阅：

- [CustomClipper](https://www.yuque.com/thyname/flutter.rendering/customclipper)：有关创建自定义裁剪的信息。
- [ClipRect](https://www.yuque.com/thyname/flutter.widgets/cliprect)：不带圆角的更高效裁剪。
- [ClipRRect](https://www.yuque.com/thyname/flutter.widgets/cliprrect)：带圆角的裁剪。
- [ClipPath](https://www.yuque.com/thyname/flutter.widgets/clippath)：任意形状的裁剪。

### ClipOval()

```dart
ClipOval({dynamic key, CustomClipper<Rect>? clipper, Clip clipBehavior = Clip.antiAlias, Widget? child})
```

创建一个椭圆形裁剪。

如果 [clipper] 为 null，则椭圆将内接于子 Widget 的布局大小和位置。

如果 [clipBehavior] 为 [Clip.none]，则不会应用任何裁剪。

### clipper

```dart
CustomClipper<Rect>? clipper
```

如果非空，则决定使用哪种裁剪方式。

该委托会返回一个描述椭圆的轴对齐边界框的矩形。椭圆自身的轴也将与坐标轴对齐。

如果 [clipper] 委托为 null，则椭圆改为使用该 Widget 的边界框（即渲染对象的布局尺寸）。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.rendering.ClipRectLayer.clipBehavior}

默认为 [Clip.antiAlias]。

### createRenderObject()

```dart
RenderClipOval createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderClipOval renderObject)
```

### didUnmountRenderObject()

```dart
void didUnmountRenderObject(RenderClipOval renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ClipPath

```dart
class ClipPath extends SingleChildRenderObjectWidget {}
```

一个使用路径裁剪其子 Widget 的 Widget。

每当该 Widget 需要绘制时，都会在一个委托上调用回调。该回调返回一个路径，该 Widget 会阻止其子 Widget 在该路径之外进行绘制。

{@youtube 560 315 https://www.youtube.com/watch?v=oAUebVIb-7s}

按路径进行裁剪的开销较大。某些形状有更优化的 Widget：

- 若要裁剪为矩形，可以考虑使用 [ClipRect](https://www.yuque.com/thyname/flutter.widgets/cliprect)。
- 若要裁剪为椭圆或圆形，可以考虑使用 [ClipOval](https://www.yuque.com/thyname/flutter.widgets/clipoval)。
- 若要裁剪为圆角矩形，可以考虑使用 [ClipRRect](https://www.yuque.com/thyname/flutter.widgets/cliprrect)。

若要裁剪为特定的 [ShapeBorder](https://www.yuque.com/thyname/flutter.painting/shapeborder)，可以考虑使用 [ClipPath.shape] 静态方法或 [ShapeBorderClipper](https://www.yuque.com/thyname/flutter.rendering/shapeborderclipper) 自定义裁剪类。

### ClipPath()

```dart
ClipPath({dynamic key, CustomClipper<Path>? clipper, Clip clipBehavior = Clip.antiAlias, Widget? child})
```

创建一个路径裁剪。

如果 [clipper] 为 null，则裁剪范围将是一个与子 Widget 的布局大小和位置相匹配的矩形。不过，与其使用此默认设置，不如考虑使用 [ClipRect](https://www.yuque.com/thyname/flutter.widgets/cliprect)，它可以更高效地实现相同的效果。

如果 [clipBehavior] 为 [Clip.none]，则不会应用任何裁剪。

### shape()

```dart
Widget shape({Key? key, required ShapeBorder shape, Clip clipBehavior = Clip.antiAlias, Widget? child})
```

创建一个形状裁剪。

使用 [ShapeBorderClipper](https://www.yuque.com/thyname/flutter.rendering/shapeborderclipper) 配置 [ClipPath](https://www.yuque.com/thyname/flutter.widgets/clippath)，使其裁剪为给定的 [ShapeBorder](https://www.yuque.com/thyname/flutter.painting/shapeborder)。

### clipper

```dart
CustomClipper<Path>? clipper
```

如果非空，则决定使用哪种裁剪方式。

如果此属性为 null，则使用的默认裁剪是该 Widget 的边界框矩形。[ClipRect](https://www.yuque.com/thyname/flutter.widgets/cliprect) 是获得该效果的更高效方式。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.rendering.ClipRectLayer.clipBehavior}

默认为 [Clip.antiAlias]。

### createRenderObject()

```dart
RenderClipPath createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderClipPath renderObject)
```

### didUnmountRenderObject()

```dart
void didUnmountRenderObject(RenderClipPath renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# PhysicalModel

```dart
class PhysicalModel extends SingleChildRenderObjectWidget {}
```

一个表示物理层的 Widget，会将其子 Widget 裁剪为某种形状。

{@youtube 560 315 https://www.youtube.com/watch?v=XgUOSS30OQk}

物理层会根据 [elevation]（标称单位为逻辑像素，垂直于渲染表面向外）投射阴影。

对于无法表示为圆角矩形的形状，请使用 [PhysicalShape](https://www.yuque.com/thyname/flutter.widgets/physicalshape)。

另请参阅：

- [AnimatedPhysicalModel](https://www.yuque.com/thyname/flutter.widgets/animatedphysicalmodel)：在给定的时长内平滑地对属性变化进行动画处理。
- [DecoratedBox](https://www.yuque.com/thyname/flutter.widgets/decoratedbox)：可以应用更任意的阴影效果。
- [ClipRect](https://www.yuque.com/thyname/flutter.widgets/cliprect)：为其子 Widget 应用裁剪。

### PhysicalModel()

```dart
PhysicalModel({dynamic key, BoxShape shape = BoxShape.rectangle, Clip clipBehavior = Clip.none, BorderRadius? borderRadius, double elevation = 0.0, required Color color, Color shadowColor = const Color(0xFF000000), Widget? child})
```

创建一个带圆角矩形裁剪的物理模型。

[color] 是必需的；物理事物都有颜色。

[shape]、[elevation]、[color]、[clipBehavior] 和 [shadowColor] 不能为 null。此外，[elevation] 必须为非负数。

### shape

```dart
BoxShape shape
```

形状的类型。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

默认为 [Clip.none]。

### borderRadius

```dart
BorderRadius? borderRadius
```

圆角的边框半径。

数值会被限制，以确保水平和垂直方向的半径之和不超过宽度/高度。

如果 [shape] 不是 [BoxShape.rectangle]，则忽略此项。

### elevation

```dart
double elevation
```

相对于父级放置此物理对象的 z 坐标。

该值为非负数。

### color

```dart
Color color
```

背景颜色。

### shadowColor

```dart
Color shadowColor
```

阴影颜色。

### createRenderObject()

```dart
RenderPhysicalModel createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderPhysicalModel renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# PhysicalShape

```dart
class PhysicalShape extends SingleChildRenderObjectWidget {}
```

一个表示物理层的 Widget，会将其子 Widget 裁剪为某个路径。

物理层会根据 [elevation]（标称单位为逻辑像素，垂直于渲染表面向外）投射阴影。

[PhysicalModel](https://www.yuque.com/thyname/flutter.widgets/physicalmodel) 的功能与之相同，但仅支持可以表示为圆角矩形的形状。

{@tool dartpad} 此示例展示了如何在居中的 [SizedBox](https://www.yuque.com/thyname/flutter.widgets/sizedbox) 上使用 [PhysicalShape](https://www.yuque.com/thyname/flutter.widgets/physicalshape)，通过 [ShapeBorderClipper](https://www.yuque.com/thyname/flutter.rendering/shapeborderclipper) 将其裁剪为圆角矩形，并为其赋予橙色和阴影。

** See code in examples/api/lib/widgets/basic/physical_shape.0.dart ** {@end-tool}

另请参阅：

- [ShapeBorderClipper](https://www.yuque.com/thyname/flutter.rendering/shapeborderclipper)：将 [ShapeBorder](https://www.yuque.com/thyname/flutter.painting/shapeborder) 转换为此 Widget 所需的 [CustomClipper](https://www.yuque.com/thyname/flutter.rendering/customclipper)。

### PhysicalShape()

```dart
PhysicalShape({dynamic key, required CustomClipper<Path> clipper, Clip clipBehavior = Clip.none, double elevation = 0.0, required Color color, Color shadowColor = const Color(0xFF000000), Widget? child})
```

创建一个具有任意形状裁剪的物理模型。

[color] 是必需的；物理事物都有颜色。

[elevation] 必须为非负数。

### clipper

```dart
CustomClipper<Path> clipper
```

决定使用哪种裁剪方式。

如果所涉及的路径是以 [ShapeBorder](https://www.yuque.com/thyname/flutter.painting/shapeborder) 子类的形式表示的，可以考虑使用 [ShapeBorderClipper](https://www.yuque.com/thyname/flutter.rendering/shapeborderclipper) 委托类，将该形状适配为可与此 Widget 一起使用。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

默认为 [Clip.none]。

### elevation

```dart
double elevation
```

相对于父级放置此物理对象的 z 坐标。

该值为非负数。

### color

```dart
Color color
```

背景颜色。

### shadowColor

```dart
Color shadowColor
```

当 elevation 不为零时用作阴影颜色的颜色。

### createRenderObject()

```dart
RenderPhysicalShape createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderPhysicalShape renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# Transform

```dart
class Transform extends SingleChildRenderObjectWidget {}
```

一个在绘制其子 Widget 之前应用变换的 Widget。

与在布局之前应用旋转的 [RotatedBox](https://www.yuque.com/thyname/flutter.widgets/rotatedbox) 不同，此对象是在绘制之前才应用其变换，这意味着在计算此 Widget 的子 Widget（以及此 Widget 本身）所占用的空间时，不会考虑该变换。

{@youtube 560 315 https://www.youtube.com/watch?v=9z_YNlRlWfA}

{@tool snippet}

此示例对一个包含文本的橙色盒子进行旋转和倾斜，同时保持其右上角固定在原始位置。

```dart
ColoredBox(
  color: Colors.black,
  child: Transform(
    alignment: Alignment.topRight,
    transform: Matrix4.skewY(0.3)..rotateZ(-math.pi / 12.0),
    child: Container(
      padding: const EdgeInsets.all(8.0),
      color: const Color(0xFFE8581C),
      child: const Text('Apartment for rent!'),
    ),
  ),
)
```

{@end-tool}

另请参阅：

- [RotatedBox](https://www.yuque.com/thyname/flutter.widgets/rotatedbox)：在布局期间（而不仅仅是在绘制期间）旋转子 Widget。
- [FractionalTranslation](https://www.yuque.com/thyname/flutter.widgets/fractionaltranslation)：对子 Widget 应用相对于其自身大小的平移。
- [FittedBox](https://www.yuque.com/thyname/flutter.widgets/fittedbox)：根据给定的 [BoxFit](https://www.yuque.com/thyname/flutter.painting/boxfit) 规则调整其子 Widget 的大小和位置，使其适配父级。
- [布局 Widget 目录](https://flutter.dev/widgets/layout/)。

### Transform()

```dart
Transform({dynamic key, required Matrix4 transform, Offset? origin, AlignmentGeometry? alignment, bool transformHitTests = true, FilterQuality? filterQuality, Widget? child})
```

创建一个对其子 Widget 进行变换的 Widget。

### Transform.rotate()

```dart
Transform.rotate({dynamic key, required double angle, Offset? origin, AlignmentGeometry? alignment = Alignment.center, bool transformHitTests = true, FilterQuality? filterQuality, Widget? child})
```

创建一个围绕中心对其子 Widget 进行旋转变换的 Widget。

`angle` 参数以顺时针弧度给出旋转角度。

{@tool snippet}

此示例将一个包含文本的橙色盒子围绕其中心旋转十五度。

```dart
Transform.rotate(
  angle: -math.pi / 12.0,
  child: Container(
    padding: const EdgeInsets.all(8.0),
    color: const Color(0xFFE8581C),
    child: const Text('Apartment for rent!'),
  ),
)
```

{@end-tool}

另请参阅：

- [RotationTransition](https://www.yuque.com/thyname/flutter.widgets/rotationtransition)：在给定的时长内平滑地对旋转变化进行动画处理。

### Transform.translate()

```dart
Transform.translate({dynamic key, required Offset offset, bool transformHitTests = true, FilterQuality? filterQuality, Widget? child})
```

创建一个对其子 Widget 进行平移变换的 Widget。

`offset` 参数指定了平移量。

{@tool snippet}

此示例将银色的子 Widget 向下平移十五像素。

```dart
Transform.translate(
  offset: const Offset(0.0, 15.0),
  child: Container(
    padding: const EdgeInsets.all(8.0),
    color: const Color(0xFF7F7F7F),
    child: const Text('Quarter'),
  ),
)
```

{@end-tool}

### Transform.scale()

```dart
Transform.scale({dynamic key, double? scale, double? scaleX, double? scaleY, Offset? origin, AlignmentGeometry? alignment = Alignment.center, bool transformHitTests = true, FilterQuality? filterQuality, Widget? child})
```

创建一个沿二维平面缩放其子 Widget 的 Widget。

`scaleX` 参数提供了 `x` 轴要乘以的标量，`scaleY` 参数提供了 `y` 轴要乘以的标量。两者均可省略，此时相应轴的缩放系数默认为 1.0。

为方便起见，若要对子 Widget 进行等比例缩放，可以使用 `scale` 参数，而不必提供 `scaleX` 和 `scaleY`。

`scale`、`scaleX` 和 `scaleY` 中至少有一个必须非空。如果提供了 `scale`，则另外两个必须为 null；同样，如果未提供 `scale`，则另外两个中必须提供一个。

[alignment] 控制缩放的原点；默认情况下为盒子的中心。

{@tool snippet}

此示例将一个包含文本的橙色盒子缩小，使其每个维度都变为原本大小的一半。

```dart
Transform.scale(
  scale: 0.5,
  child: Container(
    padding: const EdgeInsets.all(8.0),
    color: const Color(0xFFE8581C),
    child: const Text('Bad Idea Bears'),
  ),
)
```

{@end-tool}

另请参阅：

- [ScaleTransition](https://www.yuque.com/thyname/flutter.widgets/scaletransition)：在给定的时长内平滑地对缩放变化进行动画处理。

### Transform.flip()

```dart
Transform.flip({dynamic key, bool flipX = false, bool flipY = false, Offset? origin, bool transformHitTests = true, FilterQuality? filterQuality, Widget? child})
```

创建一个使其子 Widget 围绕该 Widget 的中心点进行镜像的 Widget。

如果 `flipX` 为 true，子 Widget 将水平翻转。默认为 false。

如果 `flipY` 为 true，子 Widget 将垂直翻转。默认为 false。

如果两者都为 true，子 Widget 将同时垂直和水平翻转，相当于旋转 180 度。

{@tool snippet}

此示例将文本水平翻转。

```dart
Transform.flip(
  flipX: true,
  child: const Text('Horizontal Flip'),
)
```

{@end-tool}

### transform

```dart
Matrix4 transform
```

在绘制期间用于变换子 Widget 的矩阵。

### origin

```dart
Offset? origin
```

应用该矩阵所基于坐标系的原点，相对于 [alignment] 给出的点进行描述。

设置原点等效于用一个平移对变换矩阵进行共轭运算。提供此属性只是为了方便使用。

此偏移量是在任何 [alignment] 变换之外额外应用的，因此在此示例中，由于 [Transform.rotate] 中的 [alignment] 默认为 [Alignment.center]，子 Widget 会围绕其中心进行旋转：

```dart
Transform.rotate(
  angle: math.pi,
  child: Container(
   width: 150.0,
   height: 150.0,
   color: Colors.blue,
 ),
)
```

然而，在此示例中，[origin] 偏移量是在 `alignment` 之后应用的，因此子 Widget 会围绕其右下角进行旋转：

```dart
Transform.rotate(
  angle: math.pi,
  origin: const Offset(75.0, 75.0),
  child: Container(
   width: 150.0,
   height: 150.0,
   color: Colors.blue,
 ),
)
```

### alignment

```dart
AlignmentGeometry? alignment
```

原点相对于盒子大小的对齐方式。

当此属性和 [origin] 均为 null 时，原点为此渲染对象的左上角。对于某些构造函数，此字段的默认值为 null，而对于其他构造函数，默认值为 [Alignment.center]。

这等效于根据盒子的大小设置一个原点。如果与 [origin] 同时指定，则两者都会生效。

[AlignmentDirectional.centerStart] 值等同于这样一个 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)：当 [Directionality.of] 返回 [TextDirection.ltr] 时，其 [Alignment.x] 值为 `-1.0`；当 [Directionality.of] 返回 [TextDirection.rtl] 时，其值为 `1.0`。类似地，[AlignmentDirectional.centerEnd] 等同于这样一个 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)：当 [Directionality.of] 返回 [TextDirection.ltr] 时，其 [Alignment.x] 值为 `1.0`；当 [Directionality.of] 返回 [TextDirection.rtl] 时，其值为 `-1.0`。

### transformHitTests

```dart
bool transformHitTests
```

是否将已注册的命中转换到子 Widget 结果坐标系中。

当为 `true` 时，父级边界内的命中坐标会被转换，以匹配子 Widget 在经过平移、旋转、缩放或倾斜等任何变换后在视觉上出现的位置。

当为 `false` 时，命中坐标不会被转换，这可能导致点击相对于子 Widget 的视觉位置在不同的位置被注册。

**重要提示：** 即使 [transformHitTests] 为 true，子 Widget 也无法接收父级边界之外的事件。命中测试始终从 [RenderBox.hitTest] 中父级自身的边界检查开始。如果指针位于父级边界之外，则不会调用 [RenderBox.hitTestChildren]，子 Widget 也不会被纳入命中测试的考虑范围。

对于需要在其父级原始边界之外可点击的交互元素，可以考虑：

- 扩大父 Widget 的边界，以涵盖经过变换的子 Widget。
- 使用 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 或 [OverlayPortal](https://www.yuque.com/thyname/flutter.widgets/overlayportal) 将该 Widget 放置在 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中。
- 重新组织 Widget 层次结构。

{@tool snippet} 此示例展示了一个被放大的 `Container`。尽管它看起来更大，但点击只会在父级 `SizedBox` 原始的 100x100 区域内被注册。

```dart
Center(
  child: SizedBox(
    width: 100.0,
    height: 100.0,
    child: Transform.scale(
      scale: 2.0,
      child: GestureDetector(
        onTap: () => debugPrint('Tapped!'),
        child: const ColoredBox(
          color: Colors.purple,
        ),
      ),
    ),
  ),
)
```

{@end-tool}

默认为 true。

### filterQuality

```dart
FilterQuality? filterQuality
```

以位图操作方式应用变换时所使用的滤镜质量。

{@template flutter.widgets.Transform.optional.FilterQuality} 如果 [filterQuality] 为 null，则会通过重新渲染子 Widget 来应用该变换；否则，它将控制应用于子 Widget 位图渲染的 [ImageFilter.matrix] 的质量。{@endtemplate}

### createRenderObject()

```dart
RenderTransform createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderTransform renderObject)
```

# CompositedTransformTarget

```dart
class CompositedTransformTarget extends SingleChildRenderObjectWidget {}
```

一个可以被 [CompositedTransformFollower](https://www.yuque.com/thyname/flutter.widgets/compositedtransformfollower) 作为目标的 Widget。

当此 Widget 在合成阶段（如 [WidgetsBinding.drawFrame] 中所述，位于绘制阶段之后）被合成时，会更新 [link] 对象，以便任何在同一帧中随后被合成、且被赋予相同 [LayerLink](https://www.yuque.com/thyname/flutter.rendering/layerlink) 的 [CompositedTransformFollower](https://www.yuque.com/thyname/flutter.widgets/compositedtransformfollower) Widget 都可以将自身定位到相同的屏幕位置。

单个 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 可以被多个 [CompositedTransformFollower](https://www.yuque.com/thyname/flutter.widgets/compositedtransformfollower) Widget 跟随。

[CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 在绘制顺序中必须早于任何与之关联的 [CompositedTransformFollower](https://www.yuque.com/thyname/flutter.widgets/compositedtransformfollower)。

另请参阅：

- [CompositedTransformFollower](https://www.yuque.com/thyname/flutter.widgets/compositedtransformfollower)：可以将此 Widget 作为目标的 Widget。
- [LeaderLayer](https://www.yuque.com/thyname/flutter.rendering/leaderlayer)：实现此 Widget 逻辑的层。

### CompositedTransformTarget()

```dart
CompositedTransformTarget({dynamic key, required LayerLink link, Widget? child})
```

创建一个复合变换目标 Widget。

[link] 属性当前不能被树中任何其他 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 对象使用。

### link

```dart
LayerLink link
```

将此 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 与一个或多个 [CompositedTransformFollower](https://www.yuque.com/thyname/flutter.widgets/compositedtransformfollower) 连接起来的链接对象。

该链接不能与另一个同样正在被绘制的 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 相关联。

### createRenderObject()

```dart
RenderLeaderLayer createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderLeaderLayer renderObject)
```

# CompositedTransformFollower

```dart
class CompositedTransformFollower extends SingleChildRenderObjectWidget {}
```

一个跟随 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 的 Widget。

当此 Widget 在合成阶段（如 [WidgetsBinding.drawFrame] 中所述，位于绘制阶段之后）被合成时，会应用一个变换，使关联的 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 的 [targetAnchor] 与此 Widget 的 [followerAnchor] 重合。这两个锚点将具有相同的全局坐标，除非 [offset] 不是 [Offset.zero]，在这种情况下，[followerAnchor] 将在关联的 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 的坐标空间中偏移 [offset]。

用作 [link] 的 [LayerLink](https://www.yuque.com/thyname/flutter.rendering/layerlink) 对象必须与提供给匹配的 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 的对象是同一个对象。

[CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 在绘制顺序中必须早于此 [CompositedTransformFollower](https://www.yuque.com/thyname/flutter.widgets/compositedtransformfollower)。

只有当目标位置位于此 Widget 父级认为可命中的盒子内时，对此 Widget 后代的命中测试才会起作用。如果父级覆盖了整个屏幕，这一点很容易实现，因此此 Widget 通常被用作应用级 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay)（例如由 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) Widget 的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 创建的 Overlay）中 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 的根 Widget。

另请参阅：

- [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget)：此 Widget 可以作为目标的 Widget。
- [FollowerLayer](https://www.yuque.com/thyname/flutter.rendering/followerlayer)：实现此 Widget 逻辑的层。
- [Transform](https://www.yuque.com/thyname/flutter.widgets/transform)：对子 Widget 应用任意变换。

### CompositedTransformFollower()

```dart
CompositedTransformFollower({dynamic key, required LayerLink link, bool showWhenUnlinked = true, Offset offset = Offset.zero, Alignment targetAnchor = Alignment.topLeft, Alignment followerAnchor = Alignment.topLeft, Widget? child})
```

创建一个复合变换目标 Widget。

如果 [link] 属性也提供给了某个 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget)，则该 Widget 在绘制顺序中必须更早。

[showWhenUnlinked] 和 [offset] 属性也不能为 null。

### link

```dart
LayerLink link
```

将此 [CompositedTransformFollower](https://www.yuque.com/thyname/flutter.widgets/compositedtransformfollower) 与某个 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 连接起来的链接对象。

### showWhenUnlinked

```dart
bool showWhenUnlinked
```

当不存在具有相同 [link] 的对应 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 时，是否显示该 Widget 的内容。

当该 Widget 处于关联状态时，子 Widget 会被定位到与关联的 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 相同的全局位置。

当该 Widget 未处于关联状态时：如果 [showWhenUnlinked] 为 true，则子 Widget 可见且不会被重新定位；如果为 false，则子 Widget 会被隐藏。

### targetAnchor

```dart
Alignment targetAnchor
```

关联的 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 上将与 [followerAnchor] 对齐的锚点。

{@template flutter.widgets.CompositedTransformFollower.targetAnchor} 例如，当 [targetAnchor] 和 [followerAnchor] 均为 [Alignment.topLeft] 时，此 Widget 将与关联的 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 左上对齐。当 [targetAnchor] 为 [Alignment.bottomLeft]、[followerAnchor] 为 [Alignment.topLeft] 时，此 Widget 将与关联的 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 左对齐，且其上边缘将与该 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 的下边缘对齐。{@endtemplate}

默认为 [Alignment.topLeft]。

### followerAnchor

```dart
Alignment followerAnchor
```

此 Widget 上将与关联的 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 的 [targetAnchor] 对齐的锚点。

{@macro flutter.widgets.CompositedTransformFollower.targetAnchor}

默认为 [Alignment.topLeft]。

### offset

```dart
Offset offset
```

应用于关联的 [CompositedTransformTarget](https://www.yuque.com/thyname/flutter.widgets/compositedtransformtarget) 的 [targetAnchor] 以获得此 Widget [followerAnchor] 位置的附加偏移量。

### createRenderObject()

```dart
RenderFollowerLayer createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderFollowerLayer renderObject)
```

# FittedBox

```dart
class FittedBox extends SingleChildRenderObjectWidget {}
```

根据 [fit] 在自身范围内对其子 Widget 进行缩放和定位。

{@youtube 560 315 https://www.youtube.com/watch?v=T4Uehk3_wlY}

{@tool dartpad} 在此示例中，[Placeholder](https://www.yuque.com/thyname/flutter.widgets/placeholder) 被拉伸以填满整个 [Container](https://www.yuque.com/thyname/flutter.widgets/container)。可以尝试更改 fit 类型，观察其对 [Placeholder](https://www.yuque.com/thyname/flutter.widgets/placeholder) 布局的影响。

** See code in examples/api/lib/widgets/basic/fitted_box.0.dart ** {@end-tool}

另请参阅：

- [Transform](https://www.yuque.com/thyname/flutter.widgets/transform)：在绘制时对其子 Widget 应用任意变换。
- [布局 Widget 目录](https://flutter.dev/widgets/layout/)。

### FittedBox()

```dart
FittedBox({dynamic key, BoxFit fit = BoxFit.contain, AlignmentGeometry alignment = Alignment.center, Clip clipBehavior = Clip.none, Widget? child})
```

创建一个根据 [fit] 在自身范围内对其子 Widget 进行缩放和定位的 Widget。

### fit

```dart
BoxFit fit
```

在布局期间分配的空间内如何内接子 Widget。

### alignment

```dart
AlignmentGeometry alignment
```

如何在父级边界内对齐子 Widget。

(-1.0, -1.0) 的对齐方式会将子 Widget 对齐到其父级边界的左上角。(1.0, 0.0) 的对齐方式会将子 Widget 对齐到其父级边界右边缘的中点。

默认为 [Alignment.center]。

另请参阅：

- [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)：一个包含便捷常量的类，通常用于指定 [AlignmentGeometry](https://www.yuque.com/thyname/flutter.painting/alignmentgeometry)。
- [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)：与 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 类似，用于指定相对于文本方向的对齐方式。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

默认为 [Clip.none]。

### createRenderObject()

```dart
RenderFittedBox createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderFittedBox renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# FractionalTranslation

```dart
class FractionalTranslation extends SingleChildRenderObjectWidget {}
```

在绘制其子 Widget 之前应用平移变换。

该平移以按子 Widget 大小缩放的 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 表示。例如，`dx` 为 0.25 的 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 将产生等于子 Widget 宽度四分之一的水平平移。

即使内容因偏移而溢出，命中测试也只会在 [FractionalTranslation](https://www.yuque.com/thyname/flutter.widgets/fractionaltranslation) 的边界内被检测到。

另请参阅：

- [Transform](https://www.yuque.com/thyname/flutter.widgets/transform)：在绘制时对其子 Widget 应用任意变换。
- [Transform.translate]：应用绝对偏移量的平移变换，而不是按子 Widget 缩放的偏移量。
- [布局 Widget 目录](https://flutter.dev/widgets/layout/)。

### FractionalTranslation()

```dart
FractionalTranslation({dynamic key, required Offset translation, bool transformHitTests = true, Widget? child})
```

创建一个对其子 Widget 的绘制进行平移的 Widget。

### translation

```dart
Offset translation
```

应用于子 Widget 的平移量，按子 Widget 的大小进行缩放。

例如，`dx` 为 0.25 的 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 将产生等于子 Widget 宽度四分之一的水平平移。

### transformHitTests

```dart
bool transformHitTests
```

执行命中测试时是否应用该平移。

### createRenderObject()

```dart
RenderFractionalTranslation createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderFractionalTranslation renderObject)
```

# RotatedBox

```dart
class RotatedBox extends SingleChildRenderObjectWidget {}
```

一个将其子 Widget 旋转整数个四分之一圈的 Widget。

与在绘制之前才应用变换的 [Transform](https://www.yuque.com/thyname/flutter.widgets/transform) 不同，此对象在布局之前就应用其旋转，这意味着整个旋转后的盒子只占用旋转后子 Widget 所需的空间。

{@youtube 560 315 https://www.youtube.com/watch?v=BFE6_UglLfQ}

{@tool snippet}

此代码片段旋转子 Widget（某个 [Text](https://www.yuque.com/thyname/flutter.widgets/text)），使其从下到上进行渲染，就像图表上的坐标轴标签一样：

```dart
const RotatedBox(
  quarterTurns: 3,
  child: Text('Hello World!'),
)
```

{@end-tool}

另请参阅：

- [Transform](https://www.yuque.com/thyname/flutter.widgets/transform)：一种绘制效果，允许你对子 Widget 应用任意变换。
- [Transform.rotate]：应用旋转绘制效果。
- [布局 Widget 目录](https://flutter.dev/widgets/layout/)。

### RotatedBox()

```dart
RotatedBox({dynamic key, required int quarterTurns, Widget? child})
```

一个旋转其子 Widget 的 Widget。

### quarterTurns

```dart
int quarterTurns
```

子 Widget 应顺时针旋转的四分之一圈数。

### createRenderObject()

```dart
RenderRotatedBox createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderRotatedBox renderObject)
```

# Padding

```dart
class Padding extends SingleChildRenderObjectWidget {}
```

一个按给定内边距对其子 Widget 进行内缩的 Widget。

{@youtube 560 315 https://www.youtube.com/watch?v=oD5RtLhhubg}

在向其子 Widget 传递布局约束时，padding 会按给定的内边距缩小约束，从而使子 Widget 以更小的尺寸进行布局。然后，Padding 将自身大小设置为其子 Widget 的大小加上内边距，从而有效地在子 Widget 周围创建出空白空间。

{@tool snippet}

此代码片段在 [Card](https://www.yuque.com/thyname/flutter.material/card) 内创建了"Hello World!" [Text](https://www.yuque.com/thyname/flutter.widgets/text)，并在每个方向上都内缩了十六像素。

![](https://flutter.github.io/assets-for-api-docs/assets/widgets/padding.png)

```dart
const Card(
  child: Padding(
    padding: EdgeInsets.all(16.0),
    child: Text('Hello World!'),
  ),
)
```

{@end-tool}

## 设计讨论

### 为什么使用 [Padding](https://www.yuque.com/thyname/flutter.widgets/padding) Widget，而不是带有 [Container.padding] 属性的 [Container](https://www.yuque.com/thyname/flutter.widgets/container)？

两者之间实际上并没有什么区别。如果你提供了 [Container.padding] 参数，[Container](https://www.yuque.com/thyname/flutter.widgets/container) 会为你构建一个 [Padding](https://www.yuque.com/thyname/flutter.widgets/padding) Widget。

[Container](https://www.yuque.com/thyname/flutter.widgets/container) 并不直接实现其属性，而是将若干更简单的 Widget 组合成一个便捷的整体。例如，[Container.padding] 属性会使容器构建一个 [Padding](https://www.yuque.com/thyname/flutter.widgets/padding) Widget，而 [Container.decoration] 属性会使容器构建一个 [DecoratedBox](https://www.yuque.com/thyname/flutter.widgets/decoratedbox) Widget。如果你觉得 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 使用起来很方便，尽管使用它；如果不然，也可以按照满足你需求的任意组合方式来构建这些更简单的 Widget。

事实上，Flutter 中的大多数 Widget 都是由其他更简单的 Widget 组合而成的。组合而非继承，才是构建 Widget 的主要机制。

另请参阅：

- [EdgeInsets](https://www.yuque.com/thyname/flutter.painting/edgeinsets)：用于描述内边距尺寸的类。
- [AnimatedPadding](https://www.yuque.com/thyname/flutter.widgets/animatedpadding)：在给定的时长内对 [padding] 的变化进行动画处理。
- [SliverPadding](https://www.yuque.com/thyname/flutter.widgets/sliverpadding)：此 Widget 的 sliver 等效版本。
- [布局 Widget 目录](https://flutter.dev/widgets/layout/)。

### Padding()

```dart
Padding({dynamic key, required EdgeInsetsGeometry padding, Widget? child})
```

创建一个对其子 Widget 进行内缩的 Widget。

### padding

```dart
EdgeInsetsGeometry padding
```

用于内缩子 Widget 的空间量。

### createRenderObject()

```dart
RenderPadding createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderPadding renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# Align

```dart
class Align extends SingleChildRenderObjectWidget {}
```

一个在自身范围内对其子 Widget 进行对齐、并可选地根据子 Widget 的大小调整自身大小的 Widget。

例如，若要将一个盒子对齐到右下角，你需要为该盒子传入一个比子 Widget 自然大小更大的紧约束，并将对齐方式设为 [Alignment.bottomRight]。

{@youtube 560 315 https://www.youtube.com/watch?v=g2E7yl3MwMk}

如果此 Widget 的尺寸受到约束，且 [widthFactor] 和 [heightFactor] 均为 null，则此 Widget 将尽可能大。如果某个维度不受约束且相应的尺寸系数为 null，则此 Widget 在该维度上将与其子 Widget 的大小相匹配。如果某个尺寸系数非空，则此 Widget 相应维度的大小将是子 Widget 相应维度大小与该尺寸系数的乘积。例如，如果 widthFactor 为 2.0，则此 Widget 的宽度将始终是其子 Widget 宽度的两倍。

{@tool snippet}

此示例中的 [Align](https://www.yuque.com/thyname/flutter.widgets/align) Widget 使用了 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 中定义的一个常量 [Alignment.topRight]。这会将 [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 放置在父级蓝色 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 的右上角。

![A blue square container with the Flutter logo in the top right corner.](https://flutter.github.io/assets-for-api-docs/assets/widgets/align_constant.png)

```dart
Center(
  child: Container(
    height: 120.0,
    width: 120.0,
    color: Colors.blue[50],
    child: const Align(
      alignment: Alignment.topRight,
      child: FlutterLogo(
        size: 60,
      ),
    ),
  ),
)
```

{@end-tool}

## 工作原理

[alignment] 属性描述了 `child` 坐标系中的一个点，以及此 Widget 坐标系中的另一个点。[Align](https://www.yuque.com/thyname/flutter.widgets/align) Widget 会对 `child` 进行定位，使这两个点彼此重合。

{@tool snippet}

以下示例中使用的 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 定义了两个点：

- 在 [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 的坐标系中：(0.2 _ [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 宽度/2 + [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 宽度/2, 0.6 _ [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 高度/2 + [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 高度/2) = (36.0, 48.0)。
- 在 [Align](https://www.yuque.com/thyname/flutter.widgets/align) Widget（蓝色区域）的坐标系中：(0.2 _ [Align](https://www.yuque.com/thyname/flutter.widgets/align) 宽度/2 + [Align](https://www.yuque.com/thyname/flutter.widgets/align) 宽度/2, 0.6 _ [Align](https://www.yuque.com/thyname/flutter.widgets/align) 高度/2 + [Align](https://www.yuque.com/thyname/flutter.widgets/align) 高度/2) = (72.0, 96.0)。

[Align](https://www.yuque.com/thyname/flutter.widgets/align) Widget 会对 [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 进行定位，使这两个点彼此重合。在此示例中，[FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 的左上角将被放置在距 [Align](https://www.yuque.com/thyname/flutter.widgets/align) Widget 左上角 (72.0, 96.0) - (36.0, 48.0) = (36.0, 48.0) 的位置。

![A blue square container with the Flutter logo positioned according to the Alignment specified above. A point is marked at the center of the container for the origin of the Alignment coordinate system.](https://flutter.github.io/assets-for-api-docs/assets/widgets/align_alignment.png)

```dart
Center(
  child: Container(
    height: 120.0,
    width: 120.0,
    color: Colors.blue[50],
    child: const Align(
      alignment: Alignment(0.2, 0.6),
      child: FlutterLogo(
        size: 60,
      ),
    ),
  ),
)
```

{@end-tool}

{@tool snippet}

以下示例中使用的 [FractionalOffset](https://www.yuque.com/thyname/flutter.painting/fractionaloffset) 定义了两个点：

- 在 [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 的坐标系中：(0.2 _ [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 宽度, 0.6 _ [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 高度) = (12.0, 36.0)。
- 在 [Align](https://www.yuque.com/thyname/flutter.widgets/align) Widget（蓝色区域）的坐标系中：(0.2 _ [Align](https://www.yuque.com/thyname/flutter.widgets/align) 宽度, 0.6 _ [Align](https://www.yuque.com/thyname/flutter.widgets/align) 高度) = (24.0, 72.0)。

[Align](https://www.yuque.com/thyname/flutter.widgets/align) Widget 会对 [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 进行定位，使这两个点彼此重合。在此示例中，[FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 的左上角将被放置在距 [Align](https://www.yuque.com/thyname/flutter.widgets/align) Widget 左上角 (24.0, 72.0) - (12.0, 36.0) = (12.0, 36.0) 的位置。

与上例中 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 所使用的以中心为原点的坐标系不同，[FractionalOffset](https://www.yuque.com/thyname/flutter.painting/fractionaloffset) 类使用的坐标系以 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 的左上角为原点。

![A blue square container with the Flutter logo positioned according to the FractionalOffset specified above. A point is marked at the top left corner of the container for the origin of the FractionalOffset coordinate system.](https://flutter.github.io/assets-for-api-docs/assets/widgets/align_fractional_offset.png)

```dart
Center(
  child: Container(
    height: 120.0,
    width: 120.0,
    color: Colors.blue[50],
    child: const Align(
      alignment: FractionalOffset(0.2, 0.6),
      child: FlutterLogo(
        size: 60,
      ),
    ),
  ),
)
```

{@end-tool}

另请参阅：

- [AnimatedAlign](https://www.yuque.com/thyname/flutter.widgets/animatedalign)：在给定的时长内平滑地对 [alignment] 的变化进行动画处理。
- [CustomSingleChildLayout](https://www.yuque.com/thyname/flutter.widgets/customsinglechildlayout)：使用委托来控制单个子 Widget 的布局。
- [Center](https://www.yuque.com/thyname/flutter.widgets/center)：与 [Align](https://www.yuque.com/thyname/flutter.widgets/align) 相同，但 [alignment] 始终设置为 [Alignment.center]。
- [FractionallySizedBox](https://www.yuque.com/thyname/flutter.widgets/fractionallysizedbox)：根据自身大小的一个比例来调整其子 Widget 的大小，并根据 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 值对子 Widget 进行定位。
- [布局 Widget 目录](https://flutter.dev/widgets/layout/)。

### Align()

```dart
Align({dynamic key, AlignmentGeometry alignment = Alignment.center, double? widthFactor, double? heightFactor, Widget? child})
```

创建一个对齐 Widget。

alignment 默认为 [Alignment.center]。

### alignment

```dart
AlignmentGeometry alignment
```

如何对齐子 Widget。

[Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 的 x 值和 y 值分别控制水平和垂直方向的对齐。x 值为 -1.0 表示子 Widget 的左边缘与父级的左边缘对齐，而 x 值为 1.0 表示子 Widget 的右边缘与父级的右边缘对齐。其他值则进行线性插值（或外推）。例如，值为 0.0 表示子 Widget 的中心与父级的中心对齐。

另请参阅：

- [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)：包含更多详细信息以及一些用于常见位置的便捷常量。
- [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)：其水平坐标方向取决于 [TextDirection](https://www.yuque.com/thyname/dart.ui/textdirection)。

### widthFactor

```dart
double? widthFactor
```

如果非空，则将其宽度设置为子 Widget 宽度乘以该系数的结果。

可以大于或小于 1.0，但必须为非负数。

### heightFactor

```dart
double? heightFactor
```

如果非空，则将其高度设置为子 Widget 高度乘以该系数的结果。

可以大于或小于 1.0，但必须为非负数。

### createRenderObject()

```dart
RenderPositionedBox createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderPositionedBox renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# Center

```dart
class Center extends Align {}
```

一个在自身范围内将其子 Widget 居中的 Widget。

如果此 Widget 的尺寸受到约束，且 [widthFactor] 和 [heightFactor] 均为 null，则此 Widget 将尽可能大。如果某个维度不受约束且相应的尺寸系数为 null，则此 Widget 在该维度上将与其子 Widget 的大小相匹配。如果某个尺寸系数非空，则此 Widget 相应维度的大小将是子 Widget 相应维度大小与该尺寸系数的乘积。例如，如果 widthFactor 为 2.0，则此 Widget 的宽度将始终是其子 Widget 宽度的两倍。

另请参阅：

- [Align](https://www.yuque.com/thyname/flutter.widgets/align)：允许你在自身范围内任意定位子 Widget，而不仅仅是将其居中。
- [Row](https://www.yuque.com/thyname/flutter.widgets/row)：以水平数组形式显示其子 Widget 的 Widget。
- [Column](https://www.yuque.com/thyname/flutter.widgets/column)：以垂直数组形式显示其子 Widget 的 Widget。
- [Container](https://www.yuque.com/thyname/flutter.widgets/container)：一个便捷 Widget，组合了常见的绘制、定位和尺寸调整相关 Widget。
- [布局 Widget 目录](https://flutter.dev/widgets/layout/)。

### Center()

```dart
Center({dynamic key, double? widthFactor, double? heightFactor, Widget? child})
```

创建一个使其子 Widget 居中的 Widget。

# CustomSingleChildLayout

```dart
class CustomSingleChildLayout extends SingleChildRenderObjectWidget {}
```

一个将其单个子 Widget 的布局委托给某个委托对象的 Widget。

该委托可以确定子 Widget 的布局约束，也可以决定子 Widget 的位置。该委托还可以确定父级的大小，但父级的大小不能依赖于子 Widget 的大小。

另请参阅：

- [SingleChildLayoutDelegate](https://www.yuque.com/thyname/flutter.rendering/singlechildlayoutdelegate)：控制子 Widget 布局的委托。
- [Align](https://www.yuque.com/thyname/flutter.widgets/align)：根据其子 Widget 的大小调整自身大小，并根据 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 值对子 Widget 进行定位。
- [FractionallySizedBox](https://www.yuque.com/thyname/flutter.widgets/fractionallysizedbox)：根据自身大小的一个比例来调整其子 Widget 的大小，并根据 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 值对子 Widget 进行定位。
- [CustomMultiChildLayout](https://www.yuque.com/thyname/flutter.widgets/custommultichildlayout)：使用委托来定位多个子 Widget。
- [布局 Widget 目录](https://flutter.dev/widgets/layout/)。

### CustomSingleChildLayout()

```dart
CustomSingleChildLayout({dynamic key, required SingleChildLayoutDelegate delegate, Widget? child})
```

创建一个自定义单子 Widget 布局。

### delegate

```dart
SingleChildLayoutDelegate delegate
```

控制子 Widget 布局的委托。

### createRenderObject()

```dart
RenderCustomSingleChildLayoutBox createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderCustomSingleChildLayoutBox renderObject)
```

# LayoutId

```dart
class LayoutId extends ParentDataWidget<MultiChildLayoutParentData> {}
```

用于在 [CustomMultiChildLayout](https://www.yuque.com/thyname/flutter.widgets/custommultichildlayout) 中标识子 Widget 的元数据。

[MultiChildLayoutDelegate.hasChild]、[MultiChildLayoutDelegate.layoutChild] 和 [MultiChildLayoutDelegate.positionChild] 方法会使用这些标识符。

### LayoutId()

```dart
LayoutId({Key? key, required Object id, required Widget child})
```

为子 Widget 标记一个布局标识符。

### id

```dart
Object id
```

表示此子 Widget 身份的对象。

[id] 在 [CustomMultiChildLayout](https://www.yuque.com/thyname/flutter.widgets/custommultichildlayout) 所管理的子 Widget 中必须是唯一的。

### applyParentData()

```dart
void applyParentData(RenderObject renderObject)
```

### debugTypicalAncestorWidgetClass

```dart
Type get debugTypicalAncestorWidgetClass
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# CustomMultiChildLayout

```dart
class CustomMultiChildLayout extends MultiChildRenderObjectWidget {}
```

一个使用委托来调整多个子 Widget 大小和位置的 Widget。

该委托可以确定每个子 Widget 的布局约束，也可以决定每个子 Widget 的位置。该委托还可以确定父级的大小，但父级的大小不能依赖于子 Widget 的大小。

当多个 Widget 的大小和定位之间存在复杂关系时，适合使用 [CustomMultiChildLayout](https://www.yuque.com/thyname/flutter.widgets/custommultichildlayout)。若要控制单个子 Widget 的布局，使用 [CustomSingleChildLayout](https://www.yuque.com/thyname/flutter.widgets/customsinglechildlayout) 更为合适。对于简单情形（例如将某个 Widget 对齐到某条边），使用 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) Widget 更为合适。

每个子 Widget 都必须用 [LayoutId](https://www.yuque.com/thyname/flutter.widgets/layoutid) Widget 包裹，以便向委托标识该 Widget。

{@tool dartpad} 此示例展示了如何使用 [CustomMultiChildLayout](https://www.yuque.com/thyname/flutter.widgets/custommultichildlayout) Widget，以带有部分重叠的层叠方式，从起始位置到结束位置依次布局多个彩色方块。

它会通过重新布局其子 Widget 来响应 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 的变化。

** See code in examples/api/lib/widgets/basic/custom_multi_child_layout.0.dart ** {@end-tool}

另请参阅：

- [MultiChildLayoutDelegate](https://www.yuque.com/thyname/flutter.rendering/multichildlayoutdelegate)：有关如何控制子 Widget 布局的详细信息。
- [CustomSingleChildLayout](https://www.yuque.com/thyname/flutter.widgets/customsinglechildlayout)：使用委托来控制单个子 Widget 的布局。
- [Stack](https://www.yuque.com/thyname/flutter.widgets/stack)：相对于容器的边缘排列子 Widget。
- [Flow](https://www.yuque.com/thyname/flutter.widgets/flow)：使用变换矩阵在绘制时对其子 Widget 进行控制。
- [布局 Widget 目录](https://flutter.dev/widgets/layout/)。

### CustomMultiChildLayout()

```dart
CustomMultiChildLayout({dynamic key, required MultiChildLayoutDelegate delegate, List<Widget> children})
```

创建一个自定义多子 Widget 布局。

### delegate

```dart
MultiChildLayoutDelegate delegate
```

控制子 Widget 布局的委托。

### createRenderObject()

```dart
RenderCustomMultiChildLayoutBox createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderCustomMultiChildLayoutBox renderObject)
```

# SizedBox

```dart
class SizedBox extends SingleChildRenderObjectWidget {}
```

一个具有指定大小的盒子。

{@youtube 560 315 https://www.youtube.com/watch?v=EHPu_DzRfqA}

如果提供了子 Widget，此 Widget 会在父级约束允许的范围内，尝试将其子 Widget 的大小设置为尽可能接近指定的 [height] 和 [width]。如果 width 或 height 中有一个为 null，此 Widget 会尝试将自身在该维度上的大小设置为与子 Widget 的大小相匹配。如果子 Widget 的大小依赖于其父级的大小，则必须提供 height 和 width。

如果没有提供子 Widget，[SizedBox](https://www.yuque.com/thyname/flutter.widgets/sizedbox) 会在父级约束允许的范围内，尝试将自身大小设置为尽可能接近指定的 height 和 width。如果 [height] 或 [width] 为 null 或未指定，则会被视为零。

可以使用 [SizedBox.expand] 构造函数创建一个自身大小适配父级的 [SizedBox](https://www.yuque.com/thyname/flutter.widgets/sizedbox)。这等效于将 [width] 和 [height] 都设置为 [double.infinity]。

{@tool snippet}

此代码片段使子 Widget（一个带有部分 [Text](https://www.yuque.com/thyname/flutter.widgets/text) 的 [Card](https://www.yuque.com/thyname/flutter.material/card)）在父级约束允许的情况下，具有精确的 200x300 大小：

```dart
const SizedBox(
  width: 200.0,
  height: 300.0,
  child: Card(child: Text('Hello World!')),
)
```

{@end-tool}

## 疑难解答

### 为什么我的 [SizedBox](https://www.yuque.com/thyname/flutter.widgets/sizedbox) 被忽略了？

在 Flutter 的布局协议中，约束向下传递，大小向上传递。Widget 必须遵守其父级传递的约束。这可能导致 [SizedBox](https://www.yuque.com/thyname/flutter.widgets/sizedbox) 的取值被忽略：

{@tool snippet}

此代码片段使 [ColoredBox](https://www.yuque.com/thyname/flutter.widgets/coloredbox) 的大小为 200x200。100x100 的大小被忽略，因为它与其父级恰好 200x200 的约束不兼容：

```dart
const SizedBox(
  width: 200.0,
  height: 200.0,
  child: SizedBox( // Ignored!
    width: 100.0,
    height: 100.0,
    child: ColoredBox(color: Colors.green),
  ),
)
```

{@end-tool}

可以通过用某个允许其大小可达父级大小的 Widget（例如 [Center](https://www.yuque.com/thyname/flutter.widgets/center) 或 [Align](https://www.yuque.com/thyname/flutter.widgets/align)）包裹子 [SizedBox](https://www.yuque.com/thyname/flutter.widgets/sizedbox) 来解决此问题。

另请参阅：

- [ConstrainedBox](https://www.yuque.com/thyname/flutter.widgets/constrainedbox)：此类的更通用版本，接受任意 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints)，而不是明确的宽度和高度。
- [UnconstrainedBox](https://www.yuque.com/thyname/flutter.widgets/unconstrainedbox)：一个尝试让其子 Widget 在不受约束的情况下进行绘制的容器。
- [FractionallySizedBox](https://www.yuque.com/thyname/flutter.widgets/fractionallysizedbox)：一个将其子 Widget 大小调整为可用空间总量的一个比例的 Widget。
- [AspectRatio](https://www.yuque.com/thyname/flutter.widgets/aspectratio)：一个尝试在父级约束范围内进行适配、同时将其子 Widget 大小调整为匹配给定宽高比的 Widget。
- [FittedBox](https://www.yuque.com/thyname/flutter.widgets/fittedbox)：根据给定的 [BoxFit](https://www.yuque.com/thyname/flutter.painting/boxfit) 规则调整其子 Widget 的大小和位置，使其适配父级。
- [布局 Widget 目录](https://flutter.dev/widgets/layout/)。
- [理解约束](https://docs.flutter.dev/ui/layout/constraints)：一篇深入探讨 Flutter 布局的文章。

### SizedBox()

```dart
SizedBox({dynamic key, double? width, double? height, Widget? child})
```

创建一个固定大小的盒子。[width] 和 [height] 参数可以为 null，以表示该盒子在相应维度上的大小不应受到约束。

### SizedBox.expand()

```dart
SizedBox.expand({dynamic key, Widget? child})
```

创建一个将变得尽可能大（在父级允许范围内）的盒子。

### SizedBox.shrink()

```dart
SizedBox.shrink({dynamic key, Widget? child})
```

创建一个将变得尽可能小（在父级允许范围内）的盒子。

### SizedBox.fromSize()

```dart
SizedBox.fromSize({dynamic key, Widget? child, Size? size})
```

创建一个具有指定大小的盒子。

### SizedBox.square()

```dart
SizedBox.square({dynamic key, Widget? child, double? dimension})
```

创建一个 [width] 和 [height] 相等的盒子。

### width

```dart
double? width
```

如果非空，则要求子 Widget 的宽度恰好为此值。

### height

```dart
double? height
```

如果非空，则要求子 Widget 的高度恰好为此值。

# ConstrainedBox

```dart
class ConstrainedBox extends SingleChildRenderObjectWidget {}
```

一个对其子组件施加额外约束的 Widget。

例如，如果你希望 [child] 具有 50.0 逻辑像素的最小高度，可以使用 `const BoxConstraints(minHeight: 50.0)` 作为 [constraints]。

{@youtube 560 315 https://www.youtube.com/watch?v=o2KveVr7adg}

{@tool snippet}

此代码片段通过应用 [BoxConstraints.expand] 约束，使子组件（一个包含 [Text](https://www.yuque.com/thyname/flutter.widgets/text) 的 [Card](https://www.yuque.com/thyname/flutter.material/card)）填充父容器：

```dart
ConstrainedBox(
  constraints: const BoxConstraints.expand(),
  child: const Card(child: Text('Hello World!')),
)
```

{@end-tool}

使用 [SizedBox.expand] 组件也可以获得相同的效果。

另请参阅：

- [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints)，描述约束的类。
- [UnconstrainedBox](https://www.yuque.com/thyname/flutter.widgets/unconstrainedbox)，一个尝试让其子组件不受约束进行绘制的容器。
- [SizedBox](https://www.yuque.com/thyname/flutter.widgets/sizedbox)，通过显式指定高度或宽度来指定紧约束。
- [FractionallySizedBox](https://www.yuque.com/thyname/flutter.widgets/fractionallysizedbox)，根据自身大小的一个比例来确定子组件的大小，并根据 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 值定位子组件。
- [AspectRatio](https://www.yuque.com/thyname/flutter.widgets/aspectratio)，一个尝试在满足父容器约束的同时，将其子组件的大小调整为给定宽高比的 Widget。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### ConstrainedBox()

```dart
ConstrainedBox({dynamic key, required BoxConstraints constraints, Widget? child})
```

创建一个对其子组件施加额外约束的 Widget。

### constraints

```dart
BoxConstraints constraints
```

对子组件施加的额外约束。

### createRenderObject()

```dart
RenderConstrainedBox createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderConstrainedBox renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ConstraintsTransformBox

```dart
class ConstraintsTransformBox extends SingleChildRenderObjectWidget {}
```

一个对其约束应用任意变换的容器 Widget，并使用变换后的 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints) 来调整其子组件的大小，可选择裁剪或将溢出视为错误。

此容器通过对自身约束应用 [constraintsTransform] 创建的 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints) 来调整其子组件的大小。此容器随后会尝试在自身约束的限制范围内采用相同的大小。如果最终大小不同，它将根据 [alignment] 对齐子组件。如果容器无法扩展到足以容纳整个子组件，且 [clipBehavior] 不为 [Clip.none]，则子组件将被裁剪。

在调试模式下，如果 [clipBehavior] 为 [Clip.none] 且子组件溢出容器，控制台会打印警告，并且溢出发生的位置会出现黑黄相间的条纹区域。

当 [child] 为 null 时，此 Widget 会尽可能变小，且永远不会溢出。

此 Widget 可用于确保 [child] 的部分自然尺寸得到遵守，否则会在开发过程中提前发出警告。例如，如果 [child] 需要一个最小高度以完整显示其内容，可以将 [constraintsTransform] 设置为 [maxHeightUnconstrained]，这样如果父级 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 未能提供足够的垂直空间，调试模式下将显示警告，同时仍允许 [child] 垂直增长：

{@tool snippet}

在下面的代码片段中，[Card](https://www.yuque.com/thyname/flutter.material/card) 保证至少与其"自然"高度一样高。与 [UnconstrainedBox](https://www.yuque.com/thyname/flutter.widgets/unconstrainedbox) 不同的是，如果其"自然"高度小于 40 像素，它会变得更高。如果 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 的高度不足以显示 [Card](https://www.yuque.com/thyname/flutter.material/card) 的完整内容，调试模式下会给出警告。

```dart
Container(
  constraints: const BoxConstraints(minHeight: 40, maxHeight: 100),
  alignment: Alignment.center,
  child: const ConstraintsTransformBox(
    constraintsTransform: ConstraintsTransformBox.maxHeightUnconstrained,
    child: Card(child: Text('Hello World!')),
  )
)
```

{@end-tool}

另请参阅：

- [ConstrainedBox](https://www.yuque.com/thyname/flutter.widgets/constrainedbox)，渲染一个对其子组件施加约束的盒子。
- [OverflowBox](https://www.yuque.com/thyname/flutter.widgets/overflowbox)，一个对其子组件施加额外约束、并允许子组件溢出自身的 Widget。
- [UnconstrainedBox](https://www.yuque.com/thyname/flutter.widgets/unconstrainedbox)，允许其子组件不受约束地渲染并扩展以适应它们。

### ConstraintsTransformBox()

```dart
ConstraintsTransformBox({dynamic key, Widget? child, TextDirection? textDirection, AlignmentGeometry alignment = Alignment.center, required BoxConstraintsTransform constraintsTransform, Clip clipBehavior = Clip.none, String debugTransformType = ''})
```

创建一个使用函数来变换传递给其子组件的约束的 Widget。如果子组件溢出父容器的约束，调试模式下会给出警告。

`debugTransformType` 参数为此 Widget 添加调试标签。

`alignment`、`clipBehavior` 和 `constraintsTransform` 参数不能为 null。

### unmodified()

```dart
BoxConstraints unmodified(BoxConstraints constraints)
```

一个始终原样返回其参数的 [BoxConstraintsTransform](https://www.yuque.com/thyname/flutter.rendering/boxconstraintstransform)（即恒等函数）。

如果 [constraintsTransform] 设置为此值，[ConstraintsTransformBox](https://www.yuque.com/thyname/flutter.widgets/constraintstransformbox) 将成为一个对布局没有影响的代理 Widget。

### unconstrained()

```dart
BoxConstraints unconstrained(BoxConstraints constraints)
```

一个始终返回不对任一维度施加约束的 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints)（即 `const BoxConstraints()`）的 [BoxConstraintsTransform](https://www.yuque.com/thyname/flutter.rendering/boxconstraintstransform)。

将 [constraintsTransform] 设置为此值，可让 [child] 以其"自然"大小渲染（相当于将 `constrainedAxis` 设为 null 的 [UnconstrainedBox](https://www.yuque.com/thyname/flutter.widgets/unconstrainedbox)）。

### widthUnconstrained()

```dart
BoxConstraints widthUnconstrained(BoxConstraints constraints)
```

一个从输入中移除宽度约束的 [BoxConstraintsTransform](https://www.yuque.com/thyname/flutter.rendering/boxconstraintstransform)。

将 [constraintsTransform] 设置为此值，可让 [child] 以其"自然"宽度渲染（相当于将 `constrainedAxis` 设为 [Axis.horizontal] 的 [UnconstrainedBox](https://www.yuque.com/thyname/flutter.widgets/unconstrainedbox)）。

### heightUnconstrained()

```dart
BoxConstraints heightUnconstrained(BoxConstraints constraints)
```

一个从输入中移除高度约束的 [BoxConstraintsTransform](https://www.yuque.com/thyname/flutter.rendering/boxconstraintstransform)。

将 [constraintsTransform] 设置为此值，可让 [child] 以其"自然"高度渲染（相当于将 `constrainedAxis` 设为 [Axis.vertical] 的 [UnconstrainedBox](https://www.yuque.com/thyname/flutter.widgets/unconstrainedbox)）。

### maxHeightUnconstrained()

```dart
BoxConstraints maxHeightUnconstrained(BoxConstraints constraints)
```

一个从输入中移除 `maxHeight` 约束的 [BoxConstraintsTransform](https://www.yuque.com/thyname/flutter.rendering/boxconstraintstransform)。

将 [constraintsTransform] 设置为此值，可让 [child] 以其"自然"高度或传入 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints) 的 `minHeight` 中较大者渲染。

### maxWidthUnconstrained()

```dart
BoxConstraints maxWidthUnconstrained(BoxConstraints constraints)
```

一个从输入中移除 `maxWidth` 约束的 [BoxConstraintsTransform](https://www.yuque.com/thyname/flutter.rendering/boxconstraintstransform)。

将 [constraintsTransform] 设置为此值，可让 [child] 以其"自然"宽度或传入 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints) 的 `minWidth` 中较大者渲染。

### maxUnconstrained()

```dart
BoxConstraints maxUnconstrained(BoxConstraints constraints)
```

一个同时移除输入中 `maxWidth` 和 `maxHeight` 约束的 [BoxConstraintsTransform](https://www.yuque.com/thyname/flutter.rendering/boxconstraintstransform)。

将 [constraintsTransform] 设置为此值，可让 [child] 至少以其"自然"大小渲染，并且如果传入 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints) 在某个轴上有更大的最小约束，则沿该轴增长。

### textDirection

```dart
TextDirection? textDirection
```

当 [alignment] 是 [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional) 时，用于解释它的文本方向。

默认为 null，此时将使用 [Directionality.maybeOf] 来确定文本方向。

### alignment

```dart
AlignmentGeometry alignment
```

当子组件的大小与此 Widget 不同时，用于布局子组件的对齐方式。

如果这是一个 [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)，则 [textDirection] 不能为 null。

另请参阅：

- [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，用于非 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 感知对齐方式。
- [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)，用于 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 感知对齐方式。

### constraintsTransform

```dart
BoxConstraintsTransform constraintsTransform
```

{@template flutter.widgets.constraintsTransform} 用于变换传入的 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints) 以调整 [child] 大小的函数。

该函数必须返回一个满足 [BoxConstraints.isNormalized] 的 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints)。

有关预定义的常用 [BoxConstraintsTransform](https://www.yuque.com/thyname/flutter.rendering/boxconstraintstransform)，请参阅 [ConstraintsTransformBox](https://www.yuque.com/thyname/flutter.widgets/constraintstransformbox)。 {@endtemplate}

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

{@template flutter.widgets.ConstraintsTransformBox.clipBehavior} 在调试模式下，如果 [clipBehavior] 为 [Clip.none]，且子组件溢出其约束，控制台会打印警告，并且溢出发生的位置会出现黑黄相间的条纹区域。对于其他 [clipBehavior] 值，内容将被相应裁剪。 {@endtemplate}

默认为 [Clip.none]。

### createRenderObject()

```dart
RenderConstraintsTransformBox createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderConstraintsTransformBox renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# UnconstrainedBox

```dart
class UnconstrainedBox extends StatelessWidget {}
```

一个对其子组件不施加任何约束的 Widget，允许其以"自然"大小渲染。

这使子组件能够以其独自置于无限画布上、不受任何约束时的大小进行渲染。此容器随后会尝试在自身约束的限制范围内采用相同的大小。如果最终大小不同，它将根据 [alignment] 对齐子组件。如果盒子无法扩展到足以容纳整个子组件，子组件将被裁剪。

在调试模式下，如果子组件溢出容器，控制台会打印警告，并且溢出发生的位置会出现黑黄相间的条纹区域。

另请参阅：

- [ConstrainedBox](https://www.yuque.com/thyname/flutter.widgets/constrainedbox)，一个对其子组件施加约束的盒子。
- [Align](https://www.yuque.com/thyname/flutter.widgets/align)，它放松传递给子组件的约束，而不是完全移除约束。
- [Container](https://www.yuque.com/thyname/flutter.widgets/container)，一个结合了常见绘制、定位和调整大小功能的便捷 Widget。
- [OverflowBox](https://www.yuque.com/thyname/flutter.widgets/overflowbox)，一个对其子组件施加与从父容器获得的不同约束的 Widget，可能允许子组件溢出父容器。
- [ConstraintsTransformBox](https://www.yuque.com/thyname/flutter.widgets/constraintstransformbox)，一个使用变换后的 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints) 调整子组件大小的 Widget，并在调试模式下于子组件溢出时显示警告。

### UnconstrainedBox()

```dart
UnconstrainedBox({dynamic key, Widget? child, TextDirection? textDirection, AlignmentGeometry alignment = Alignment.center, Axis? constrainedAxis, Clip clipBehavior = Clip.none})
```

创建一个对其子组件不施加任何约束、允许其以"自然"大小渲染的 Widget。如果子组件溢出父容器的约束，调试模式下会给出警告。

### textDirection

```dart
TextDirection? textDirection
```

当 [alignment] 是 [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional) 时，用于解释它的文本方向。

### alignment

```dart
AlignmentGeometry alignment
```

用于布局子组件的对齐方式。

如果这是一个 [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)，则 [textDirection] 不能为 null。

另请参阅：

- [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，用于非 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 感知对齐方式。
- [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)，用于 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 感知对齐方式。

### constrainedAxis

```dart
Axis? constrainedAxis
```

如果有的话，保留约束的轴。

如果未设置，或设置为 null（默认值），则两个轴都不会保留其约束。如果设置为 [Axis.vertical]，则保留垂直约束；如果设置为 [Axis.horizontal]，则保留水平约束。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

默认为 [Clip.none]。

### child

```dart
Widget? child
```

此 Widget 在树中的下级 Widget。

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# FractionallySizedBox

```dart
class FractionallySizedBox extends SingleChildRenderObjectWidget {}
```

一个将其子组件的大小调整为可用空间总量的一个比例的 Widget。有关布局算法的更多详情，请参阅 [RenderFractionallySizedOverflowBox](https://www.yuque.com/thyname/flutter.rendering/renderfractionallysizedoverflowbox)。

{@youtube 560 315 https://www.youtube.com/watch?v=PEsY654EGZ0}

{@tool dartpad} 此示例展示了一个 [FractionallySizedBox](https://www.yuque.com/thyname/flutter.widgets/fractionallysizedbox)，其唯一子组件根据 widthFactor 和 heightFactor 参数为盒子大小的 50%，并通过 alignment 参数在盒子内居中。

** 参见 examples/api/lib/widgets/basic/fractionally_sized_box.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [Align](https://www.yuque.com/thyname/flutter.widgets/align)，根据其子组件的大小调整自身大小，并根据 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 值定位子组件。
- [OverflowBox](https://www.yuque.com/thyname/flutter.widgets/overflowbox)，一个对其子组件施加与从父容器获得的不同约束的 Widget，可能允许子组件溢出父容器。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### FractionallySizedBox()

```dart
FractionallySizedBox({dynamic key, AlignmentGeometry alignment = Alignment.center, double? widthFactor, double? heightFactor, Widget? child})
```

创建一个将其子组件的大小调整为可用空间总量的一个比例的 Widget。

如果非 null，[widthFactor] 和 [heightFactor] 参数必须为非负数。

### widthFactor

```dart
double? widthFactor
```

{@template flutter.widgets.basic.fractionallySizedBox.widthFactor} 如果非 null，则为分配给子组件的传入宽度的比例。

如果非 null，将为子组件提供一个紧约束宽度，其值为传入的最大宽度约束乘以此比例。

如果为 null，则传入的宽度约束将原样传递给子组件。 {@endtemplate}

### heightFactor

```dart
double? heightFactor
```

{@template flutter.widgets.basic.fractionallySizedBox.heightFactor} 如果非 null，则为分配给子组件的传入高度的比例。

如果非 null，将为子组件提供一个紧约束高度，其值为传入的最大高度约束乘以此比例。

如果为 null，则传入的高度约束将原样传递给子组件。 {@endtemplate}

### alignment

```dart
AlignmentGeometry alignment
```

{@template flutter.widgets.basic.fractionallySizedBox.alignment} 如何对齐子组件。

alignment 的 x 值和 y 值分别控制水平和垂直对齐方式。x 值为 -1.0 表示子组件的左边缘与父容器的左边缘对齐，而 x 值为 1.0 表示子组件的右边缘与父容器的右边缘对齐。其他值进行线性插值（和外推）。例如，值为 0.0 表示子组件的中心与父容器的中心对齐。

默认为 [Alignment.center]。

另请参阅：

- [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，一个包含便捷常量的类，通常用于指定 [AlignmentGeometry](https://www.yuque.com/thyname/flutter.painting/alignmentgeometry)。
- [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)，类似于 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，用于指定相对于文本方向的对齐方式。 {@endtemplate}

### createRenderObject()

```dart
RenderFractionallySizedOverflowBox createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderFractionallySizedOverflowBox renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# LimitedBox

```dart
class LimitedBox extends SingleChildRenderObjectWidget {}
```

一个仅在其自身不受约束时才限制其大小的盒子。

如果此 Widget 的最大宽度不受约束，则其子组件的宽度将被限制为 [maxWidth]。类似地，如果此 Widget 的最大高度不受约束，则其子组件的高度将被限制为 [maxHeight]。

这样的效果是在无边界环境中为子组件提供一个自然的维度。例如，通过为一个通常会尽可能变大的 Widget 提供 [maxHeight]，该 Widget 通常会调整自身大小以适应其父容器，但当置于垂直列表中时，它将采用给定的高度。

这在组合那些通常试图匹配其父容器大小的 Widget 时很有用，以便它们在（无边界的）列表中表现得合理。

{@youtube 560 315 https://www.youtube.com/watch?v=uVki2CIzBTs}

另请参阅：

- [ConstrainedBox](https://www.yuque.com/thyname/flutter.widgets/constrainedbox)，它在所有情况下都应用其约束，而不仅仅是在传入约束无边界时。
- [SizedBox](https://www.yuque.com/thyname/flutter.widgets/sizedbox)，通过显式指定高度或宽度来指定紧约束。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### LimitedBox()

```dart
LimitedBox({dynamic key, double maxWidth = double.infinity, double maxHeight = double.infinity, Widget? child})
```

创建一个仅在其自身不受约束时才限制其大小的盒子。

[maxWidth] 和 [maxHeight] 参数不能为负数。

### maxWidth

```dart
double maxWidth
```

在没有 [BoxConstraints.maxWidth] 约束的情况下应用的最大宽度限制。

### maxHeight

```dart
double maxHeight
```

在没有 [BoxConstraints.maxHeight] 约束的情况下应用的最大高度限制。

### createRenderObject()

```dart
RenderLimitedBox createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderLimitedBox renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# OverflowBox

```dart
class OverflowBox extends SingleChildRenderObjectWidget {}
```

一个对其子组件施加与从父容器获得的不同约束的 Widget，可能允许子组件溢出父容器。

{@tool dartpad} 此示例展示了如何使用 [OverflowBox](https://www.yuque.com/thyname/flutter.widgets/overflowbox)，以及它的效果。

** 参见 examples/api/lib/widgets/basic/overflowbox.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [RenderConstrainedOverflowBox](https://www.yuque.com/thyname/flutter.rendering/renderconstrainedoverflowbox)，了解 [OverflowBox](https://www.yuque.com/thyname/flutter.widgets/overflowbox) 如何渲染的详情。
- [SizedOverflowBox](https://www.yuque.com/thyname/flutter.widgets/sizedoverflowbox)，一个具有特定大小、但将其原始约束传递给子组件（子组件可能因此溢出）的 Widget。
- [ConstrainedBox](https://www.yuque.com/thyname/flutter.widgets/constrainedbox)，一个对其子组件施加额外约束的 Widget。
- [UnconstrainedBox](https://www.yuque.com/thyname/flutter.widgets/unconstrainedbox)，一个尝试让其子组件不受约束进行绘制的容器。
- [SizedBox](https://www.yuque.com/thyname/flutter.widgets/sizedbox)，一个具有指定大小的盒子。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### OverflowBox()

```dart
OverflowBox({dynamic key, AlignmentGeometry alignment = Alignment.center, double? minWidth, double? maxWidth, double? minHeight, double? maxHeight, OverflowBoxFit fit = OverflowBoxFit.max, Widget? child})
```

创建一个允许其子组件溢出自身的 Widget。

### alignment

```dart
AlignmentGeometry alignment
```

如何对齐子组件。

alignment 的 x 值和 y 值分别控制水平和垂直对齐方式。x 值为 -1.0 表示子组件的左边缘与父容器的左边缘对齐，而 x 值为 1.0 表示子组件的右边缘与父容器的右边缘对齐。其他值进行线性插值（和外推）。例如，值为 0.0 表示子组件的中心与父容器的中心对齐。

默认为 [Alignment.center]。

另请参阅：

- [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，一个包含便捷常量的类，通常用于指定 [AlignmentGeometry](https://www.yuque.com/thyname/flutter.painting/alignmentgeometry)。
- [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)，类似于 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，用于指定相对于文本方向的对齐方式。

### minWidth

```dart
double? minWidth
```

给子组件的最小宽度约束。将其设置为 null（默认值）以使用来自父容器的约束。

### maxWidth

```dart
double? maxWidth
```

给子组件的最大宽度约束。将其设置为 null（默认值）以使用来自父容器的约束。

### minHeight

```dart
double? minHeight
```

给子组件的最小高度约束。将其设置为 null（默认值）以使用来自父容器的约束。

### maxHeight

```dart
double? maxHeight
```

给子组件的最大高度约束。将其设置为 null（默认值）以使用来自父容器的约束。

### fit

```dart
OverflowBoxFit fit
```

调整渲染对象大小的方式。

这仅在子组件实际未溢出的场景下才会产生影响。如果设置为 [OverflowBoxFit.deferToChild]，渲染对象将在父容器约束范围内调整自身大小以匹配其子组件的大小，如果未设置子组件，则会尽可能小。如果设置为 [OverflowBoxFit.max]（默认值），渲染对象将尽可能调整自身大小以填满父容器允许的空间。

### createRenderObject()

```dart
RenderConstrainedOverflowBox createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderConstrainedOverflowBox renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SizedOverflowBox

```dart
class SizedOverflowBox extends SingleChildRenderObjectWidget {}
```

一个具有特定大小、但将其原始约束传递给子组件（子组件可能因此溢出）的 Widget。

另请参阅：

- [OverflowBox](https://www.yuque.com/thyname/flutter.widgets/overflowbox)，一个对其子组件施加与从父容器获得的不同约束的 Widget，可能允许子组件溢出父容器。
- [ConstrainedBox](https://www.yuque.com/thyname/flutter.widgets/constrainedbox)，一个对其子组件施加额外约束的 Widget。
- [UnconstrainedBox](https://www.yuque.com/thyname/flutter.widgets/unconstrainedbox)，一个尝试让其子组件不受约束进行绘制的容器。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### SizedOverflowBox()

```dart
SizedOverflowBox({dynamic key, required Size size, AlignmentGeometry alignment = Alignment.center, Widget? child})
```

创建一个具有给定大小、且允许其子组件溢出的 Widget。

### alignment

```dart
AlignmentGeometry alignment
```

如何对齐子组件。

alignment 的 x 值和 y 值分别控制水平和垂直对齐方式。x 值为 -1.0 表示子组件的左边缘与父容器的左边缘对齐，而 x 值为 1.0 表示子组件的右边缘与父容器的右边缘对齐。其他值进行线性插值（和外推）。例如，值为 0.0 表示子组件的中心与父容器的中心对齐。

默认为 [Alignment.center]。

另请参阅：

- [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，一个包含便捷常量的类，通常用于指定 [AlignmentGeometry](https://www.yuque.com/thyname/flutter.painting/alignmentgeometry)。
- [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)，类似于 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，用于指定相对于文本方向的对齐方式。

### size

```dart
Size size
```

此 Widget 应尝试达到的大小。

### createRenderObject()

```dart
RenderSizedOverflowBox createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderSizedOverflowBox renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# Offstage

```dart
class Offstage extends SingleChildRenderObjectWidget {}
```

一个将子组件布局为如同其在树中一样、但不进行任何绘制、不使子组件可用于命中测试、且不在父容器中占用任何空间的 Widget。

Offstage 中的子组件仍然是活动的：它们可以接收焦点，并可以将键盘输入定向到它们。

无论动画最终是否可见，动画都会在 offstage 的子组件中继续运行，因此会消耗电量和 CPU 时间。

[Offstage](https://www.yuque.com/thyname/flutter.widgets/offstage) 可用于在将 Widget 呈现到屏幕上（尚未）之前测量其尺寸。要在不需要时将 Widget 从视图中隐藏，最好将其从组件树中完全移除，而不是将其保留在 [Offstage](https://www.yuque.com/thyname/flutter.widgets/offstage) 子树中。

{@tool dartpad} 此示例展示了当 `_offstage` 成员字段为 false 时的 [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) Widget，以及当其为 true 时如何在父容器中不占用任何空间地隐藏它。当处于 offstage 状态时，此应用会显示一个按钮，用于获取 logo 的大小，该大小将显示在 [SnackBar](https://www.yuque.com/thyname/flutter.material/snackbar) 中。

** 参见 examples/api/lib/widgets/basic/offstage.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [Visibility](https://www.yuque.com/thyname/flutter.widgets/visibility)，可以更高效（虽然不太精细）地隐藏子组件。
- [TickerMode](https://www.yuque.com/thyname/flutter.widgets/tickermode)，可用于禁用子树中的动画。
- [SliverOffstage](https://www.yuque.com/thyname/flutter.widgets/sliveroffstage)，此 Widget 的 sliver 版本。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### Offstage()

```dart
Offstage({dynamic key, bool offstage = true, Widget? child})
```

创建一个在视觉上隐藏其子组件的 Widget。

### offstage

```dart
bool offstage
```

是否对树的其余部分隐藏子组件。

如果为 true，子组件将被布局为如同其在树中一样，但不进行任何绘制、不使其可用于命中测试、且不在父容器中占用任何空间。

Offstage 中的子组件仍然是活动的：它们可以接收焦点，并可以将键盘输入定向到它们。

无论动画最终是否可见，动画都会在 offstage 的子组件中继续运行，因此会消耗电量和 CPU 时间。

如果为 false，子组件将正常包含在树中。

### createRenderObject()

```dart
RenderOffstage createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderOffstage renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### createElement()

```dart
SingleChildRenderObjectElement createElement()
```

# AspectRatio

```dart
class AspectRatio extends SingleChildRenderObjectWidget {}
```

一个尝试将子组件调整为特定宽高比的 Widget。

宽高比表示为宽度与高度的比值。例如，16:9 的宽:高宽高比的值为 16.0/9.0。

{@youtube 560 315 https://www.youtube.com/watch?v=XcnP3_mO_Ms}

[AspectRatio](https://www.yuque.com/thyname/flutter.widgets/aspectratio) Widget 使用有限的迭代过程来计算子组件的适当约束，然后使用这些约束对子组件进行一次布局。这个迭代过程效率很高，不需要多次布局。

该 Widget 首先尝试布局约束允许的最大宽度，并通过将给定的宽高比（表示为宽度与高度的比值）应用于该宽度来确定 Widget 的高度。

如果最大宽度是无限的，则通过将宽高比应用于最大高度来确定初始宽度。

该 Widget 随后会检查计算出的尺寸是否与父容器的约束兼容；如果不兼容，则会考虑这些约束进行第二次重新计算。

如果该 Widget 在检查每个约束后都未能找到可行的大小，该 Widget 最终会为子组件选择一个满足布局约束、但不满足宽高比约束的大小。

{@tool dartpad} 此示例展示了当父容器的宽度约束为无限时，[AspectRatio](https://www.yuque.com/thyname/flutter.widgets/aspectratio) 如何设置宽度。由于父容器允许的高度是一个固定值，实际宽度是通过给定的 [aspectRatio] 确定的。

在此示例中，高度固定为 100.0，宽高比设置为 16 / 9，使宽度为 100.0 / 9 \* 16。

** 参见 examples/api/lib/widgets/basic/aspect_ratio.0.dart 中的代码 ** {@end-tool}

{@tool dartpad} 第二个示例使用宽高比为 2.0，布局约束要求宽度在 0.0 到 100.0 之间，高度在 0.0 到 100.0 之间。该 Widget 选择 100.0 的宽度（允许的最大值）和 50.0 的高度（以匹配宽高比）。

** 参见 examples/api/lib/widgets/basic/aspect_ratio.1.dart 中的代码 ** {@end-tool}

{@tool dartpad} 第三个示例与第二个类似，但宽高比设置为 0.5。该 Widget 仍然选择 100.0 的宽度（允许的最大值），并尝试使用 200.0 的高度。不幸的是，这违反了约束，因为子组件最多只能有 100.0 像素高。该 Widget 随后会采用该值并再次应用宽高比，得到 50.0 的宽度。约束允许这个宽度，因此子组件获得 50.0 的宽度和 100.0 的高度。如果该宽度不被允许，该 Widget 将继续遍历约束。

** 参见 examples/api/lib/widgets/basic/aspect_ratio.2.dart 中的代码 ** {@end-tool}

## 在无约束情况下设置宽高比

当使用诸如 [FittedBox](https://www.yuque.com/thyname/flutter.widgets/fittedbox) 之类的 Widget 时，约束是无边界的。这导致 [AspectRatio](https://www.yuque.com/thyname/flutter.widgets/aspectratio) 无法找到一组合适的约束来应用。在这种情况下，可考虑使用 [SizedBox](https://www.yuque.com/thyname/flutter.widgets/sizedbox) 显式设置一个大小，而不是使用 [AspectRatio](https://www.yuque.com/thyname/flutter.widgets/aspectratio) 设置宽高比。然后该大小会由 [FittedBox](https://www.yuque.com/thyname/flutter.widgets/fittedbox) 适当缩放。

另请参阅：

- [Align](https://www.yuque.com/thyname/flutter.widgets/align)，一个在其自身内对齐子组件、并可选择根据子组件的大小调整自身大小的 Widget。
- [ConstrainedBox](https://www.yuque.com/thyname/flutter.widgets/constrainedbox)，一个对其子组件施加额外约束的 Widget。
- [UnconstrainedBox](https://www.yuque.com/thyname/flutter.widgets/unconstrainedbox)，一个尝试让其子组件不受约束进行绘制的容器。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### AspectRatio()

```dart
AspectRatio({dynamic key, required double aspectRatio, Widget? child})
```

创建一个具有特定宽高比的 Widget。

[aspectRatio] 参数必须是一个大于零的有限数。

### aspectRatio

```dart
double aspectRatio
```

尝试使用的宽高比。

宽高比表示为宽度与高度的比值。例如，16:9 的宽:高宽高比的值为 16.0/9.0。

### createRenderObject()

```dart
RenderAspectRatio createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderAspectRatio renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# IntrinsicWidth

```dart
class IntrinsicWidth extends SingleChildRenderObjectWidget {}
```

一个将其子组件调整为子组件最大固有宽度的 Widget。

此类很有用，例如，当有无限的宽度可用、而你希望原本会尝试无限扩展的子组件转而将自身调整为更合理的宽度时。此外，在 [IntrinsicWidth](https://www.yuque.com/thyname/flutter.widgets/intrinsicwidth) 内放置 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 将使所有 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 的子组件都能与最宽的子组件一样宽。

此 Widget 传递给其子组件的约束将遵循父容器的约束，因此如果约束不足以满足子组件的最大固有宽度，则子组件获得的宽度将小于原本可获得的宽度。同样，如果最小宽度约束大于子组件的最大固有宽度，则子组件获得的宽度将大于原本可获得的宽度。

如果 [stepWidth] 非 null，子组件的宽度将被对齐为 [stepWidth] 的倍数。类似地，如果 [stepHeight] 非 null，子组件的高度将被对齐为 [stepHeight] 的倍数。

此类相对开销较大，因为它在最终布局阶段之前增加了一次推测性布局过程。请尽可能避免使用它。在最坏的情况下，此 Widget 可能导致布局在树的深度上呈 O(N²)。

另请参阅：

- [Align](https://www.yuque.com/thyname/flutter.widgets/align)，一个在其自身内对齐子组件的 Widget。这可用于放松传递给 [RenderIntrinsicWidth](https://www.yuque.com/thyname/flutter.rendering/renderintrinsicwidth) 的约束，从而允许 [RenderIntrinsicWidth](https://www.yuque.com/thyname/flutter.rendering/renderintrinsicwidth) 的子组件比其父容器更小。
- [Row](https://www.yuque.com/thyname/flutter.widgets/row)，当与 [CrossAxisAlignment.stretch] 一起使用时，可用于仅放松传递给 [RenderIntrinsicWidth](https://www.yuque.com/thyname/flutter.rendering/renderintrinsicwidth) 的宽度约束，从而允许 [RenderIntrinsicWidth](https://www.yuque.com/thyname/flutter.rendering/renderintrinsicwidth) 的子组件的宽度比其父容器更小。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### IntrinsicWidth()

```dart
IntrinsicWidth({dynamic key, double? stepWidth, double? stepHeight, Widget? child})
```

创建一个将其子组件调整为子组件固有宽度的 Widget。

此类开销相对较大。请尽可能避免使用它。

### stepWidth

```dart
double? stepWidth
```

如果非 null，强制子组件的宽度为此值的倍数。

如果为 null 或 0.0，子组件的宽度将与其最大固有宽度相同。

此值不能为负数。

另请参阅：

- [RenderBox.getMaxIntrinsicWidth]，通常定义 Widget 的最大固有宽度。

### stepHeight

```dart
double? stepHeight
```

如果非 null，强制子组件的高度为此值的倍数。

如果为 null 或 0.0，子组件的高度将不受约束。

此值不能为负数。

### createRenderObject()

```dart
RenderIntrinsicWidth createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderIntrinsicWidth renderObject)
```

# IntrinsicHeight

```dart
class IntrinsicHeight extends SingleChildRenderObjectWidget {}
```

一个将其子组件调整为子组件固有高度的 Widget。

此类很有用，例如，当有无限的高度可用、而你希望原本会尝试无限扩展的子组件转而将自身调整为更合理的高度时。此外，在 [IntrinsicHeight](https://www.yuque.com/thyname/flutter.widgets/intrinsicheight) 内放置 [Row](https://www.yuque.com/thyname/flutter.widgets/row) 将使所有 [Row](https://www.yuque.com/thyname/flutter.widgets/row) 的子组件都能与最高的子组件一样高。

此 Widget 传递给其子组件的约束将遵循父容器的约束，因此如果约束不足以满足子组件的最大固有高度，则子组件获得的高度将小于原本可获得的高度。同样，如果最小高度约束大于子组件的最大固有高度，则子组件获得的高度将大于原本可获得的高度。

此类相对开销较大，因为它在最终布局阶段之前增加了一次推测性布局过程。请尽可能避免使用它。在最坏的情况下，此 Widget 可能导致布局在树的深度上呈 O(N²)。

另请参阅：

- [Align](https://www.yuque.com/thyname/flutter.widgets/align)，一个在其自身内对齐子组件的 Widget。这可用于放松传递给 [RenderIntrinsicHeight](https://www.yuque.com/thyname/flutter.rendering/renderintrinsicheight) 的约束，从而允许 [RenderIntrinsicHeight](https://www.yuque.com/thyname/flutter.rendering/renderintrinsicheight) 的子组件比其父容器更小。
- [Column](https://www.yuque.com/thyname/flutter.widgets/column)，当与 [CrossAxisAlignment.stretch] 一起使用时，可用于仅放松传递给 [RenderIntrinsicHeight](https://www.yuque.com/thyname/flutter.rendering/renderintrinsicheight) 的高度约束，从而允许 [RenderIntrinsicHeight](https://www.yuque.com/thyname/flutter.rendering/renderintrinsicheight) 的子组件的高度比其父容器更小。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### IntrinsicHeight()

```dart
IntrinsicHeight({dynamic key, Widget? child})
```

创建一个将其子组件调整为子组件固有高度的 Widget。

此类开销相对较大。请尽可能避免使用它。

### createRenderObject()

```dart
RenderIntrinsicHeight createRenderObject(BuildContext context)
```

# Baseline

```dart
class Baseline extends SingleChildRenderObjectWidget {}
```

一个根据子组件的基线定位子组件的 Widget。

此 Widget 会向下移动子组件，使得子组件的基线（如果子组件没有基线，则为其底部）位于此盒子顶部下方 [baseline] 逻辑像素处，然后调整此盒子的大小以容纳子组件。如果 [baseline] 小于从子组件顶部到子组件基线的距离，则子组件改为顶部对齐。

{@youtube 560 315 https://www.youtube.com/watch?v=8ZaFk0yvNlI}

另请参阅：

- [Align](https://www.yuque.com/thyname/flutter.widgets/align)，一个在其自身内对齐子组件、并可选择根据子组件的大小调整自身大小的 Widget。
- [Center](https://www.yuque.com/thyname/flutter.widgets/center)，一个在其自身内使子组件居中的 Widget。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### Baseline()

```dart
Baseline({dynamic key, required double baseline, required TextBaseline baselineType, Widget? child})
```

创建一个根据子组件的基线定位子组件的 Widget。

### baseline

```dart
double baseline
```

从此盒子顶部到定位子组件基线处的逻辑像素数。

### baselineType

```dart
TextBaseline baselineType
```

用于定位子组件的基线类型。

### createRenderObject()

```dart
RenderBaseline createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderBaseline renderObject)
```

# IgnoreBaseline

```dart
class IgnoreBaseline extends SingleChildRenderObjectWidget {}
```

一个使父容器出于基线对齐目的而忽略 [child] 的 Widget。

另请参阅：

- [Baseline](https://www.yuque.com/thyname/flutter.widgets/baseline)，一个相对于基线定位子组件的 Widget。

### IgnoreBaseline()

```dart
IgnoreBaseline({dynamic key, Widget? child})
```

创建一个出于基线对齐目的而忽略子组件的 Widget。

### createRenderObject()

```dart
RenderIgnoreBaseline createRenderObject(BuildContext context)
```

# SliverToBoxAdapter

```dart
class SliverToBoxAdapter extends SingleChildRenderObjectWidget {}
```

一个包含单个盒子 Widget 的 sliver。

Sliver 是可以使用 [CustomScrollView](https://www.yuque.com/thyname/flutter.widgets/customscrollview) 组合以创建自定义滚动效果的专用 Widget。[SliverToBoxAdapter](https://www.yuque.com/thyname/flutter.widgets/slivertoboxadapter) 是一个基本的 sliver，它连接回常见的基于盒子的 Widget。

_要了解有关 sliver 的更多信息，请参阅 [CustomScrollView.slivers]。_

与其在 [CustomScrollView](https://www.yuque.com/thyname/flutter.widgets/customscrollview) 中使用多个 [SliverToBoxAdapter](https://www.yuque.com/thyname/flutter.widgets/slivertoboxadapter) Widget 来显示多个盒子 Widget，不如考虑使用 [SliverList](https://www.yuque.com/thyname/flutter.widgets/sliverlist)、[SliverFixedExtentList](https://www.yuque.com/thyname/flutter.widgets/sliverfixedextentlist)、[SliverPrototypeExtentList](https://www.yuque.com/thyname/flutter.widgets/sliverprototypeextentlist) 或 [SliverGrid](https://www.yuque.com/thyname/flutter.widgets/slivergrid)，它们效率更高，因为它们只实例化那些通过滚动视图视口实际可见的子组件。

另请参阅：

- [CustomScrollView](https://www.yuque.com/thyname/flutter.widgets/customscrollview)，显示可滚动的 sliver 列表。
- [SliverList](https://www.yuque.com/thyname/flutter.widgets/sliverlist)，以线性数组显示多个盒子 Widget。
- [SliverFixedExtentList](https://www.yuque.com/thyname/flutter.widgets/sliverfixedextentlist)，以线性数组显示多个具有相同主轴范围的盒子 Widget。
- [SliverPrototypeExtentList](https://www.yuque.com/thyname/flutter.widgets/sliverprototypeextentlist)，以线性数组显示多个与原型项具有相同主轴范围的盒子 Widget。
- [SliverGrid](https://www.yuque.com/thyname/flutter.widgets/slivergrid)，在任意位置显示多个盒子 Widget。

### SliverToBoxAdapter()

```dart
SliverToBoxAdapter({dynamic key, Widget? child})
```

创建一个包含单个盒子 Widget 的 sliver。

### createRenderObject()

```dart
RenderSliverToBoxAdapter createRenderObject(BuildContext context)
```

# SliverPadding

```dart
class SliverPadding extends SingleChildRenderObjectWidget {}
```

一个在另一个 sliver 每一边应用内边距的 sliver。

Sliver 是可以使用 [CustomScrollView](https://www.yuque.com/thyname/flutter.widgets/customscrollview) 组合以创建自定义滚动效果的专用 Widget。[SliverPadding](https://www.yuque.com/thyname/flutter.widgets/sliverpadding) 是一个基本的 sliver，它通过在每一边应用内边距来内缩另一个 sliver。

{@macro flutter.rendering.RenderSliverEdgeInsetsPadding}

另请参阅：

- [CustomScrollView](https://www.yuque.com/thyname/flutter.widgets/customscrollview)，显示可滚动的 sliver 列表。
- [Padding](https://www.yuque.com/thyname/flutter.widgets/padding)，此 Widget 的盒子版本。

### SliverPadding()

```dart
SliverPadding({dynamic key, required EdgeInsetsGeometry padding, Widget? sliver})
```

创建一个在另一个 sliver 每一边应用内边距的 sliver。

### padding

```dart
EdgeInsetsGeometry padding
```

用于内缩子 sliver 的空间量。

### createRenderObject()

```dart
RenderSliverPadding createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderSliverPadding renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SliverSemantics

```dart
class SliverSemantics extends _SemanticsBase {}
```

一个为其子树标注含义描述的 sliver。

{@macro flutter.widgets.SemanticsBase}

- [Semantics](https://www.yuque.com/thyname/flutter.widgets/semantics)，此 sliver 的 Widget 版本。

### SliverSemantics()

```dart
SliverSemantics({dynamic key, required Widget sliver, bool container = false, bool explicitChildNodes = false, bool excludeSemantics = false, bool blockUserActions = false, bool? enabled, bool? checked, bool? mixed, bool? selected, bool? toggled, bool? button, bool? slider, bool? keyboardKey, bool? link, Uri? linkUrl, bool? header, int? headingLevel, bool? textField, bool? readOnly, bool? focusable, bool? focused, dynamic accessibilityFocusBlockType, bool? inMutuallyExclusiveGroup, bool? obscured, bool? multiline, bool? scopesRoute, bool? namesRoute, bool? hidden, bool? image, bool? liveRegion, bool? expanded, bool? isRequired, int? maxValueLength, int? currentValueLength, String? identifier, Object? traversalParentIdentifier, Object? traversalChildIdentifier, String? label, dynamic attributedLabel, String? value, dynamic attributedValue, String? increasedValue, dynamic attributedIncreasedValue, String? decreasedValue, dynamic attributedDecreasedValue, String? hint, dynamic attributedHint, String? tooltip, String? onTapHint, String? onLongPressHint, dynamic textDirection, dynamic sortKey, dynamic tagForChildren, dynamic onTap, dynamic onLongPress, dynamic onScrollLeft, dynamic onScrollRight, dynamic onScrollUp, dynamic onScrollDown, dynamic onIncrease, dynamic onDecrease, dynamic onCopy, dynamic onCut, dynamic onPaste, dynamic onDismiss, dynamic onMoveCursorForwardByCharacter, dynamic onMoveCursorBackwardByCharacter, dynamic onSetSelection, dynamic onSetText, dynamic onDidGainAccessibilityFocus, dynamic onDidLoseAccessibilityFocus, dynamic onFocus, dynamic onExpand, dynamic onCollapse, Map<InvalidType, InvalidType>? customSemanticsActions, dynamic role, Set<String>? controlsNodes, dynamic validationResult = SemanticsValidationResult.none, dynamic hitTestBehavior, dynamic inputType, dynamic localeForSubtree, String? minValue, String? maxValue})
```

创建一个语义标注。

要创建 [SliverSemantics](https://www.yuque.com/thyname/flutter.widgets/sliversemantics) 的 `const` 实例，请使用 [SliverSemantics.fromProperties] 构造函数。

{@macro flutter.widgets.SemanticsBase.constructor}

### SliverSemantics.fromProperties()

```dart
SliverSemantics.fromProperties({dynamic key, Widget? child, bool container = false, bool explicitChildNodes = false, bool excludeSemantics = false, bool blockUserActions = false, dynamic localeForSubtree, required dynamic properties})
```

{@macro flutter.widgets.SemanticsBase.fromProperties}

### createRenderObject()

```dart
RenderSliverSemanticsAnnotations createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderSliverSemanticsAnnotations renderObject)
```

# getAxisDirectionFromAxisReverseAndDirectionality()

```dart
AxisDirection getAxisDirectionFromAxisReverseAndDirectionality(BuildContext context, Axis axis, bool reverse)
```

返回给定 [Axis](https://www.yuque.com/thyname/flutter.painting/axis) 在当前 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 下的 [AxisDirection](https://www.yuque.com/thyname/flutter.painting/axisdirection)（如果 `reverse` 为 true，则返回相反方向）。

如果 `axis` 是 [Axis.vertical]，此函数返回 [AxisDirection.down]，除非 `reverse` 为 true，此时该函数返回 [AxisDirection.up]。

如果 `axis` 是 [Axis.horizontal]，此函数会检查当前 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)。如果当前 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 为从右到左，则此函数返回 [AxisDirection.left]（除非 `reverse` 为 true，此时返回 [AxisDirection.right]）。类似地，如果当前 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 为从左到右，则此函数返回 [AxisDirection.right]（除非 `reverse` 为 true，此时返回 [AxisDirection.left]）。

许多滚动 Widget（例如 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview)、[GridView](https://www.yuque.com/thyname/flutter.widgets/gridview)、[PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 和 [SingleChildScrollView](https://www.yuque.com/thyname/flutter.widgets/singlechildscrollview)）以及 [ListBody](https://www.yuque.com/thyname/flutter.widgets/listbody) 都使用此函数，将它们的 [Axis](https://www.yuque.com/thyname/flutter.painting/axis) 和 `reverse` 属性转换为具体的 [AxisDirection](https://www.yuque.com/thyname/flutter.painting/axisdirection)。

# ListBody

```dart
class ListBody extends MultiChildRenderObjectWidget {}
```

一个沿给定轴顺序排列其子组件、并强制它们在另一个轴上匹配父容器尺寸的 Widget。

此 Widget 很少直接使用。相反，可考虑使用 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview)，它将类似的布局算法与滚动行为相结合，或者使用 [Column](https://www.yuque.com/thyname/flutter.widgets/column)，它对垂直方向的一组盒子的布局提供更灵活的控制。

另请参阅：

- [RenderListBody](https://www.yuque.com/thyname/flutter.rendering/renderlistbody)，实现此布局算法，其文档描述了其中一些微妙之处。
- [SingleChildScrollView](https://www.yuque.com/thyname/flutter.widgets/singlechildscrollview)，有时与 [ListBody](https://www.yuque.com/thyname/flutter.widgets/listbody) 一起使用以使内容可滚动。
- [Column](https://www.yuque.com/thyname/flutter.widgets/column) 和 [Row](https://www.yuque.com/thyname/flutter.widgets/row)，实现了此布局算法的更复杂版本（代价是效率略低）。
- [ListView](https://www.yuque.com/thyname/flutter.widgets/listview)，实现了此布局算法的高效滚动版本。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### ListBody()

```dart
ListBody({dynamic key, Axis mainAxis = Axis.vertical, bool reverse = false, List<Widget> children})
```

创建一个沿给定轴顺序排列其子组件的布局 Widget。

默认情况下，[mainAxis] 为 [Axis.vertical]。

### mainAxis

```dart
Axis mainAxis
```

用作主轴的方向。

### reverse

```dart
bool reverse
```

list body 是否按阅读方向定位子组件。

例如，如果阅读方向为从左到右，且 [mainAxis] 为 [Axis.horizontal]，那么当 [reverse] 为 false 时，list body 从左到右定位子组件；当 [reverse] 为 true 时，从右到左定位。

类似地，如果 [mainAxis] 为 [Axis.vertical]，那么当 [reverse] 为 false 时，list body 从上到下定位；当 [reverse] 为 true 时，从下到上定位。

默认为 false。

### createRenderObject()

```dart
RenderListBody createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderListBody renderObject)
```

# Stack

```dart
class Stack extends MultiChildRenderObjectWidget {}
```

一个根据其盒子边缘定位其子组件的 Widget。

如果你想以简单的方式重叠多个子组件，此类很有用，例如让一些文本和一张图片重叠，覆盖一个渐变和一个位于底部的按钮。

{@youtube 560 315 https://www.youtube.com/watch?v=liEGSeD3Zt8}

[Stack](https://www.yuque.com/thyname/flutter.widgets/stack) Widget 的每个子组件要么是 _已定位的（positioned）_，要么是 _未定位的（non-positioned）_。已定位的子组件是那些包裹在至少有一个非 null 属性的 [Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned) Widget 中的子组件。堆叠会调整自身大小以容纳所有未定位的子组件，这些子组件根据 [alignment]（默认为从左到右环境中的左上角，从右到左环境中的右上角）进行定位。然后根据它们的 top、right、bottom 和 left 属性，相对于堆叠放置已定位的子组件。

堆叠按顺序绘制其子组件，第一个子组件位于底部。如果你想更改子组件的绘制顺序，可以用新顺序的子组件重建堆叠。如果以这种方式重新排序子组件，请考虑为子组件提供非 null 的键。这些键会使框架将子组件的底层对象移动到其新位置，而不是在新位置重新创建它们。

有关堆叠布局算法的更多详情，请参阅 [RenderStack](https://www.yuque.com/thyname/flutter.rendering/renderstack)。

如果你想按特定模式排列若干子组件，或者你想制作自定义布局管理器，你可能需要改用 [CustomMultiChildLayout](https://www.yuque.com/thyname/flutter.widgets/custommultichildlayout)。特别是，使用 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 时，你无法相对于子组件的大小或堆叠自身的大小来定位子组件。

{@tool snippet}

使用 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack)，你可以将 Widget 相互叠放定位。

![该示例创建了一个蓝色盒子，与一个更大的绿色盒子重叠，绿色盒子本身又与一个更大的红色盒子重叠。](https://flutter.github.io/assets-for-api-docs/assets/widgets/stack.png)

```dart
Stack(
  children: <Widget>[
    Container(
      width: 100,
      height: 100,
      color: Colors.red,
    ),
    Container(
      width: 90,
      height: 90,
      color: Colors.green,
    ),
    Container(
      width: 80,
      height: 80,
      color: Colors.blue,
    ),
  ],
)
```

{@end-tool}

{@tool snippet}

此示例展示了如何使用 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 通过添加渐变背景来增强文本的可见性。

![渐变从透明淡出到底部的深灰色，白色文本位于较暗部分之上。](https://flutter.github.io/assets-for-api-docs/assets/widgets/stack_with_gradient.png)

```dart
SizedBox(
  width: 250,
  height: 250,
  child: Stack(
    children: <Widget>[
      Container(
        width: 250,
        height: 250,
        color: Colors.white,
      ),
      Container(
        padding: const EdgeInsets.all(5.0),
        alignment: Alignment.bottomCenter,
        decoration: BoxDecoration(
          gradient: LinearGradient(
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
            colors: <Color>[
              Colors.black.withAlpha(0),
              Colors.black12,
              Colors.black45
            ],
          ),
        ),
        child: const Text(
          'Foreground Text',
          style: TextStyle(color: Colors.white, fontSize: 20.0),
        ),
      ),
    ],
  ),
)
```

{@end-tool}

另请参阅：

- [Align](https://www.yuque.com/thyname/flutter.widgets/align)，根据其子组件的大小调整自身大小，并根据 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 值定位子组件。
- [CustomSingleChildLayout](https://www.yuque.com/thyname/flutter.widgets/customsinglechildlayout)，使用委托来控制单个子组件的布局。
- [CustomMultiChildLayout](https://www.yuque.com/thyname/flutter.widgets/custommultichildlayout)，使用委托来定位多个子组件。
- [Flow](https://www.yuque.com/thyname/flutter.widgets/flow)，使用变换矩阵提供其子组件的绘制时控制。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### Stack()

```dart
Stack({dynamic key, AlignmentGeometry alignment = AlignmentDirectional.topStart, TextDirection? textDirection, StackFit fit = StackFit.loose, Clip clipBehavior = Clip.hardEdge, List<Widget> children})
```

创建一个堆叠布局 Widget。

默认情况下，堆叠的未定位子组件按其左上角对齐。

### alignment

```dart
AlignmentGeometry alignment
```

如何在堆叠中对齐未定位和部分定位的子组件。

未定位的子组件相对于彼此放置，使得由 [alignment] 确定的点位于同一位置。例如，如果 [alignment] 为 [Alignment.topLeft]，则每个未定位子组件的左上角将位于相同的全局坐标处。

部分定位的子组件，即那些未在某个特定轴上指定对齐方式的子组件（例如，既没有设置 `top` 也没有设置 `bottom`），会使用 alignment 来确定它们在该未指定的轴上应如何定位。

默认为 [AlignmentDirectional.topStart]。

另请参阅：

- [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，一个包含便捷常量的类，通常用于指定 [AlignmentGeometry](https://www.yuque.com/thyname/flutter.painting/alignmentgeometry)。
- [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)，类似于 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，用于指定相对于文本方向的对齐方式。

### textDirection

```dart
TextDirection? textDirection
```

用于解析 [alignment] 的文本方向。

默认为环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)。

### fit

```dart
StackFit fit
```

如何调整堆叠中未定位子组件的大小。

从其父容器传入 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的约束要么被放松（[StackFit.loose]），要么被收紧为其最大大小（[StackFit.expand]）。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

堆叠只裁剪那些 _几何形状_ 溢出堆叠的子组件。在其边界之外绘制的子组件（例如带阴影的盒子）不会被裁剪，无论此属性的值如何。类似地，如果子组件本身有一个溢出堆叠的后代，该子组件也不会被裁剪，因为只考虑堆叠直接子组件的几何形状。[Transform](https://www.yuque.com/thyname/flutter.widgets/transform) 是一个可以使其子组件在其几何形状之外绘制的 Widget 的示例。

要裁剪那些几何形状没有溢出堆叠的子组件，请考虑使用 [ClipRect](https://www.yuque.com/thyname/flutter.widgets/cliprect) Widget。

即使设置为 [Clip.none]，堆叠本身也不会扩展其命中测试区域：落在堆叠自身边界之外的指针事件不会到达子组件，即使该子组件在该区域中被绘制。

默认为 [Clip.hardEdge]。

### createRenderObject()

```dart
RenderStack createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderStack renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# Positioned

```dart
class Positioned extends ParentDataWidget<StackParentData> {}
```

一个控制 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的子组件位置的 Widget。

[Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned) Widget 必须是 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的后代，并且从 [Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned) Widget 到其封闭 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的路径只能包含 [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget) 或 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget)（不能包含其他类型的 Widget，如 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget)）。

{@youtube 560 315 https://www.youtube.com/watch?v=EgtPleVwxBQ}

如果一个 Widget 被包裹在 [Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned) 中，那么它就是其 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 中的一个 _已定位_ Widget。如果 [top] 属性非 null，此子组件的顶部边缘将从堆叠 Widget 的顶部向下定位 [top] 个布局单位。[right]、[bottom] 和 [left] 属性的工作方式类似。

如果 [top] 和 [bottom] 属性都非 null，则子组件将被强制具有恰好满足这两个约束所需的高度。类似地，将 [right] 和 [left] 属性设置为非 null 值将强制子组件具有特定的宽度。或者，可以使用 [width] 和 [height] 属性来给出尺寸，并配合一个相应的位置属性（例如 [top] 和 [height]）。

如果特定轴上的所有三个值都为 null，则使用 [Stack.alignment] 属性来定位子组件。

如果所有六个值都为 null，则该子组件是一个未定位的子组件。[Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 仅使用未定位的子组件来调整自身大小。

另请参阅：

- [AnimatedPositioned](https://www.yuque.com/thyname/flutter.widgets/animatedpositioned)，每当给定的位置发生变化时，会在给定的持续时间内自动过渡子组件的位置。
- [PositionedTransition](https://www.yuque.com/thyname/flutter.widgets/positionedtransition)，接受提供的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)，在给定的持续时间内过渡子组件位置的变化。
- [PositionedDirectional](https://www.yuque.com/thyname/flutter.widgets/positioneddirectional)，适应环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)。

### Positioned()

```dart
Positioned({dynamic key, double? left, double? top, double? right, double? bottom, double? width, double? height, required Widget child})
```

创建一个控制 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的子组件位置的 Widget。

在三个水平值（[left]、[right]、[width]）中只能设置两个，在三个垂直值（[top]、[bottom]、[height]）中也只能设置两个。在每种情况下，三个值中至少有一个必须为 null。

另请参阅：

- [Positioned.directional]，使用 `start` 和 `end` 而不是 `left` 和 `right` 来指定 Widget 的水平位置。
- [PositionedDirectional](https://www.yuque.com/thyname/flutter.widgets/positioneddirectional)，与 [Positioned.directional] 类似，但适应环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)。

### Positioned.fromRect()

```dart
Positioned.fromRect({dynamic key, required Rect rect, required Widget child})
```

使用给定 [Rect](https://www.yuque.com/thyname/dart.ui/rect) 的值创建一个 Positioned 对象。

这会根据给定的 [Rect](https://www.yuque.com/thyname/dart.ui/rect) 设置 [left]、[top]、[width] 和 [height] 属性。[right] 和 [bottom] 属性设置为 null。

### Positioned.fromRelativeRect()

```dart
Positioned.fromRelativeRect({dynamic key, required RelativeRect rect, required Widget child})
```

使用给定 [RelativeRect](https://www.yuque.com/thyname/flutter.rendering/relativerect) 的值创建一个 Positioned 对象。

这会根据给定的 [RelativeRect](https://www.yuque.com/thyname/flutter.rendering/relativerect) 设置 [left]、[top]、[right] 和 [bottom] 属性。[height] 和 [width] 属性设置为 null。

### Positioned.fill()

```dart
Positioned.fill({dynamic key, double? left = 0.0, double? top = 0.0, double? right = 0.0, double? bottom = 0.0, required Widget child})
```

创建一个 Positioned 对象，[left]、[top]、[right] 和 [bottom] 设置为 0.0，除非为它们传入了值。

### Positioned.directional()

```dart
Positioned.directional({Key? key, required TextDirection textDirection, double? start, double? top, double? end, double? bottom, double? width, double? height, required Widget child})
```

创建一个控制 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的子组件位置的 Widget。

在三个水平值（`start`、`end`、[width]）中只能设置两个，在三个垂直值（[top]、[bottom]、[height]）中也只能设置两个。在每种情况下，三个值中至少有一个必须为 null。

如果 `textDirection` 为 [TextDirection.rtl]，则 `start` 参数用于 [right] 属性，`end` 参数用于 [left] 属性。否则，如果 `textDirection` 为 [TextDirection.ltr]，则 `start` 参数用于 [left] 属性，`end` 参数用于 [right] 属性。

另请参阅：

- [PositionedDirectional](https://www.yuque.com/thyname/flutter.widgets/positioneddirectional)，适应环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)。

### left

```dart
double? left
```

子组件的左边缘相对于堆叠左边缘的内缩距离。

在三个水平值（[left]、[right]、[width]）中只能设置两个。第三个必须为 null。

如果三个值都为 null，则使用 [Stack.alignment] 来水平定位子组件。

### top

```dart
double? top
```

子组件的顶部边缘相对于堆叠顶部的内缩距离。

在三个垂直值（[top]、[bottom]、[height]）中只能设置两个。第三个必须为 null。

如果三个值都为 null，则使用 [Stack.alignment] 来垂直定位子组件。

### right

```dart
double? right
```

子组件的右边缘相对于堆叠右边缘的内缩距离。

在三个水平值（[left]、[right]、[width]）中只能设置两个。第三个必须为 null。

如果三个值都为 null，则使用 [Stack.alignment] 来水平定位子组件。

### bottom

```dart
double? bottom
```

子组件的底部边缘相对于堆叠底部的内缩距离。

在三个垂直值（[top]、[bottom]、[height]）中只能设置两个。第三个必须为 null。

如果三个值都为 null，则使用 [Stack.alignment] 来垂直定位子组件。

### width

```dart
double? width
```

子组件的宽度。

在三个水平值（[left]、[right]、[width]）中只能设置两个。第三个必须为 null。

如果三个值都为 null，则使用 [Stack.alignment] 来水平定位子组件。

### height

```dart
double? height
```

子组件的高度。

在三个垂直值（[top]、[bottom]、[height]）中只能设置两个。第三个必须为 null。

如果三个值都为 null，则使用 [Stack.alignment] 来垂直定位子组件。

### applyParentData()

```dart
void applyParentData(RenderObject renderObject)
```

### debugTypicalAncestorWidgetClass

```dart
Type get debugTypicalAncestorWidgetClass
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# PositionedDirectional

```dart
class PositionedDirectional extends StatelessWidget {}
```

一个在不指定具体 [TextDirection](https://www.yuque.com/thyname/dart.ui/textdirection) 的情况下、控制 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的子组件位置的 Widget。

使用环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 来确定 [start] 是位于左边还是右边。

[PositionedDirectional](https://www.yuque.com/thyname/flutter.widgets/positioneddirectional) Widget 必须是 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的后代，并且从 [PositionedDirectional](https://www.yuque.com/thyname/flutter.widgets/positioneddirectional) Widget 到其封闭 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的路径只能包含 [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget) 或 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget)（不能包含其他类型的 Widget，如 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget)）。

如果一个 Widget 被包裹在 [PositionedDirectional](https://www.yuque.com/thyname/flutter.widgets/positioneddirectional) 中，那么它就是其 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 中的一个 _已定位_ Widget。如果 [top] 属性非 null，此子组件的顶部边缘将从堆叠 Widget 的顶部向下定位 [top] 个布局单位。[start]、[bottom] 和 [end] 属性的工作方式类似。

如果 [top] 和 [bottom] 属性都非 null，则子组件将被强制具有恰好满足这两个约束所需的高度。类似地，将 [start] 和 [end] 属性设置为非 null 值将强制子组件具有特定的宽度。或者，可以使用 [width] 和 [height] 属性来给出尺寸，并配合一个相应的位置属性（例如 [top] 和 [height]）。

另请参阅：

- [Positioned](https://www.yuque.com/thyname/flutter.widgets/positioned)，直观地指定 Widget 的位置。
- [Positioned.directional]，也使用 [start] 和 [end] 指定 Widget 的水平位置，但具有显式的 [TextDirection](https://www.yuque.com/thyname/dart.ui/textdirection)。
- [AnimatedPositionedDirectional](https://www.yuque.com/thyname/flutter.widgets/animatedpositioneddirectional)，每当给定的位置发生变化时，会在给定的持续时间内自动过渡子组件的位置。

### PositionedDirectional()

```dart
PositionedDirectional({dynamic key, double? start, double? top, double? end, double? bottom, double? width, double? height, required Widget child})
```

创建一个控制 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 的子组件位置的 Widget。

在三个水平值（`start`、`end`、[width]）中只能设置两个，在三个垂直值（[top]、[bottom]、[height]）中也只能设置两个。在每种情况下，三个值中至少有一个必须为 null。

另请参阅：

- [Positioned.directional]，也使用 [start] 和 [end] 指定 Widget 的水平位置，但具有显式的 [TextDirection](https://www.yuque.com/thyname/dart.ui/textdirection)。

### start

```dart
double? start
```

子组件的前缘相对于堆叠前缘的内缩距离。

在三个水平值（[start]、[end]、[width]）中只能设置两个。第三个必须为 null。

### top

```dart
double? top
```

子组件的顶部边缘相对于堆叠顶部的内缩距离。

在三个垂直值（[top]、[bottom]、[height]）中只能设置两个。第三个必须为 null。

### end

```dart
double? end
```

子组件的后缘相对于堆叠后缘的内缩距离。

在三个水平值（[start]、[end]、[width]）中只能设置两个。第三个必须为 null。

### bottom

```dart
double? bottom
```

子组件的底部边缘相对于堆叠底部的内缩距离。

在三个垂直值（[top]、[bottom]、[height]）中只能设置两个。第三个必须为 null。

### width

```dart
double? width
```

子组件的宽度。

在三个水平值（[start]、[end]、[width]）中只能设置两个。第三个必须为 null。

### height

```dart
double? height
```

子组件的高度。

在三个垂直值（[top]、[bottom]、[height]）中只能设置两个。第三个必须为 null。

### child

```dart
Widget child
```

此 Widget 在树中的下级 Widget。

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

# Flex

```dart
class Flex extends MultiChildRenderObjectWidget {}
```

一个以一维数组显示其子组件的 Widget。

[Flex](https://www.yuque.com/thyname/flutter.widgets/flex) Widget 允许你控制子组件放置的轴（水平或垂直）。这称为 _主轴（main axis）_。如果你预先知道主轴，请考虑改用 [Row](https://www.yuque.com/thyname/flutter.widgets/row)（如果是水平的）或 [Column](https://www.yuque.com/thyname/flutter.widgets/column)（如果是垂直的），因为这样会更简洁。

要使子组件在此 Widget 主轴的 [direction] 方向上扩展以填充可用空间，请将子组件包裹在 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) Widget 中。

[Flex](https://www.yuque.com/thyname/flutter.widgets/flex) Widget 不会滚动（并且通常认为，如果 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 中的子组件数量超过可用空间所能容纳的数量，则属于错误）。如果你有一些 Widget，并且希望在空间不足时它们能够滚动，请考虑使用 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview)。

[Flex](https://www.yuque.com/thyname/flutter.widgets/flex) Widget 不允许其子组件跨越多个水平或垂直行进行换行。对于允许其子组件换行的 Widget，请考虑改用 [Wrap](https://www.yuque.com/thyname/flutter.widgets/wrap) Widget。

如果你只有一个子组件，那么与其使用 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex)、[Row](https://www.yuque.com/thyname/flutter.widgets/row) 或 [Column](https://www.yuque.com/thyname/flutter.widgets/column)，不如考虑使用 [Align](https://www.yuque.com/thyname/flutter.widgets/align) 或 [Center](https://www.yuque.com/thyname/flutter.widgets/center) 来定位该子组件。

## 布局算法

_本节描述框架如何渲染 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex)。_ _有关盒子布局模型的介绍，请参阅 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints)。_

[Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 的布局分六步进行：

1.  以无边界的主轴约束和传入的交叉轴约束，布局每个具有 null 或零 flex 因子的子组件（例如，非 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 的子组件）。如果 [crossAxisAlignment] 为 [CrossAxisAlignment.stretch]，则改用与传入的交叉轴最大范围匹配的紧交叉轴约束。
2.  根据 flex 因子，在具有非零 flex 因子的子组件（例如 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 的子组件）之间分配剩余的主轴空间。例如，flex 因子为 2.0 的子组件将获得 flex 因子为 1.0 的子组件两倍的主轴空间。
3.  以与第 1 步相同的交叉轴约束布局剩余的每个子组件，但不使用无边界的主轴约束，而是根据第 2 步中分配的空间量使用最大轴约束。[Flexible.fit] 属性为 [FlexFit.tight] 的子组件将获得紧约束（即强制填满分配的空间），[Flexible.fit] 属性为 [FlexFit.loose] 的子组件将获得松约束（即不强制填满分配的空间）。
4.  [Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 的交叉轴范围是子组件的最大交叉轴范围（这将始终满足传入的约束）。
5.  [Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 的主轴范围由 [mainAxisSize] 属性确定。如果 [mainAxisSize] 属性为 [MainAxisSize.max]，则 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 的主轴范围是传入主轴约束的最大范围。如果 [mainAxisSize] 属性为 [MainAxisSize.min]，则 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 的主轴范围是子组件主轴范围的总和（受传入约束的限制）。
6.  根据 [mainAxisAlignment] 和 [crossAxisAlignment] 确定每个子组件的位置。例如，如果 [mainAxisAlignment] 为 [MainAxisAlignment.spaceBetween]，则未分配给子组件的任何主轴空间将被均分并放置在子组件之间。

另请参阅：

- [Row](https://www.yuque.com/thyname/flutter.widgets/row)，此 Widget 始终为水平方向的版本。
- [Column](https://www.yuque.com/thyname/flutter.widgets/column)，此 Widget 始终为垂直方向的版本。
- [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded)，指示应占用所有剩余空间的子组件。
- [Flexible](https://www.yuque.com/thyname/flutter.widgets/flexible)，指示应共享剩余空间的子组件。
- [Spacer](https://www.yuque.com/thyname/flutter.widgets/spacer)，一个占用与其 flex 值成比例的空间的 Widget。可能会被调整为更小（留下一些未使用的剩余空间）。
- [Wrap](https://www.yuque.com/thyname/flutter.widgets/wrap)，允许其子组件在多个 _行_ 上换行的 Widget。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### Flex()

```dart
Flex({dynamic key, required Axis direction, MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start, MainAxisSize mainAxisSize = MainAxisSize.max, CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center, TextDirection? textDirection, VerticalDirection verticalDirection = VerticalDirection.down, TextBaseline? textBaseline, Clip clipBehavior = Clip.none, double spacing = 0.0, List<Widget> children})
```

创建一个 flex 布局。

[direction] 是必需的。

如果 [crossAxisAlignment] 为 [CrossAxisAlignment.baseline]，则 [textBaseline] 不能为 null。

[textDirection] 参数默认为环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)（如果有）。如果没有环境中的 directionality，并且在决定子组件的排列方向或消除主轴或交叉轴方向的 `start` 或 `end` 值的歧义时需要文本方向，则 [textDirection] 不能为 null。

### direction

```dart
Axis direction
```

用作主轴的方向。

如果你预先知道轴的方向，请考虑改用 [Row](https://www.yuque.com/thyname/flutter.widgets/row)（如果是水平的）或 [Column](https://www.yuque.com/thyname/flutter.widgets/column)（如果是垂直的），而不是 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex)，因为那样会更简洁。（对于 [Row](https://www.yuque.com/thyname/flutter.widgets/row) 和 [Column](https://www.yuque.com/thyname/flutter.widgets/column)，此属性固定为相应的轴。）

### mainAxisAlignment

```dart
MainAxisAlignment mainAxisAlignment
```

子组件应如何沿主轴放置。

例如，默认值 [MainAxisAlignment.start] 将子组件放置在主轴的起始位置（即 [Row](https://www.yuque.com/thyname/flutter.widgets/row) 的左侧或 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 的顶部）。

### mainAxisSize

```dart
MainAxisSize mainAxisSize
```

主轴上应占用多少空间。

在为子组件分配空间之后，可能会有一些剩余的自由空间。此值控制是否在传入布局约束的限制下，最大化或最小化自由空间的量。

如果某些子组件具有非零的 flex 因子（且没有 [FlexFit.loose] 的 fit），它们将扩展以消耗所有可用空间，并且不会有剩余的自由空间需要最大化或最小化，此时该值对最终布局无关紧要。

### crossAxisAlignment

```dart
CrossAxisAlignment crossAxisAlignment
```

子组件应如何沿交叉轴放置。

例如，默认值 [CrossAxisAlignment.center] 将子组件在交叉轴上居中（例如，[Column](https://www.yuque.com/thyname/flutter.widgets/column) 的水平方向）。

当交叉轴为垂直方向（如 [Row](https://www.yuque.com/thyname/flutter.widgets/row)）且子组件包含文本时，请考虑改用 [CrossAxisAlignment.baseline]。如果不同的子组件包含具有不同字体度量的文本，这通常会产生更好的视觉效果，例如因为它们在 [TextStyle.fontSize] 或其他 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 属性上有所不同，或者因为它们使用了因不同文字系统而不同的字体。

### textDirection

```dart
TextDirection? textDirection
```

确定水平排列子组件的顺序，以及如何在水平方向上解释 `start` 和 `end`。

默认为环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)。

如果 [textDirection] 为 [TextDirection.rtl]，则文本流动方向从右到左开始。否则，如果 [textDirection] 为 [TextDirection.ltr]，则文本流动方向从左到右开始。

如果 [direction] 为 [Axis.horizontal]，这将控制子组件的定位顺序（从左到右或从右到左），以及 [mainAxisAlignment] 属性中 [MainAxisAlignment.start] 和 [MainAxisAlignment.end] 值的含义。

如果 [direction] 为 [Axis.vertical]，这将控制 [crossAxisAlignment] 属性中 [CrossAxisAlignment.start] 和 [CrossAxisAlignment.end] 值的含义。

如果 [direction] 为 [Axis.vertical]，且 [crossAxisAlignment] 为 [CrossAxisAlignment.start] 或 [CrossAxisAlignment.end]，则 [textDirection]（或环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)）不能为 null。

### verticalDirection

```dart
VerticalDirection verticalDirection
```

确定垂直排列子组件的顺序，以及如何在垂直方向上解释 `start` 和 `end`。

默认为 [VerticalDirection.down]。

如果 [direction] 为 [Axis.vertical]，这将控制子组件的绘制顺序（向下或向上），以及 [mainAxisAlignment] 属性中 [MainAxisAlignment.start] 和 [MainAxisAlignment.end] 值的含义。

如果 [direction] 为 [Axis.vertical]，且 [mainAxisAlignment] 为 [MainAxisAlignment.start] 或 [MainAxisAlignment.end]，或者有多个子组件，则 [verticalDirection] 不能为 null。

如果 [direction] 为 [Axis.horizontal]，这将控制 [crossAxisAlignment] 属性中 [CrossAxisAlignment.start] 和 [CrossAxisAlignment.end] 值的含义。

如果 [direction] 为 [Axis.horizontal]，且 [crossAxisAlignment] 为 [CrossAxisAlignment.start] 或 [CrossAxisAlignment.end]，则 [verticalDirection] 不能为 null。

### textBaseline

```dart
TextBaseline? textBaseline
```

如果根据基线对齐项目，使用哪个基线。

使用基线对齐时必须设置此项。没有默认值，因为框架无法先验地知道正确的基线。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

默认为 [Clip.none]。

### spacing

```dart
double spacing
```

{@macro flutter.rendering.RenderFlex.spacing}

### getEffectiveTextDirection()

```dart
TextDirection? getEffectiveTextDirection(BuildContext context)
```

传递给 [RenderFlex.textDirection] 的值。

此值来源于 [textDirection] 属性和环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)。如果不需要指定文本方向，则该值为 null。实际上，除了 [crossAxisAlignment] 不依赖文本方向（不是 `start` 或 `end`）的垂直 flex（例如 [Column](https://www.yuque.com/thyname/flutter.widgets/column)）之外，总是需要指定方向。（对于 [Column](https://www.yuque.com/thyname/flutter.widgets/column)，布局顺序由 [verticalDirection] 控制，它始终被指定，因为它不依赖于继承的 Widget，且默认为 [VerticalDirection.down]。）

此方法之所以存在，是为了让 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 的子类（它们创建源自 [RenderFlex](https://www.yuque.com/thyname/flutter.rendering/renderflex) 的自己的渲染对象）能够这样做，同时仍能使用仅在必要时才提供文本方向的逻辑。

### createRenderObject()

```dart
RenderFlex createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderFlex renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# Row

```dart
class Row extends Flex {}
```

一个以水平数组显示其子组件的 Widget。

要使子组件扩展以填充可用的水平空间，请将子组件包裹在 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) Widget 中。

[Row](https://www.yuque.com/thyname/flutter.widgets/row) Widget 不会滚动（并且通常认为，如果 [Row](https://www.yuque.com/thyname/flutter.widgets/row) 中的子组件数量超过可用空间所能容纳的数量，则属于错误）。如果你有一行 Widget，并且希望在空间不足时它们能够滚动，请考虑使用 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview)。

有关垂直方向的变体，请参阅 [Column](https://www.yuque.com/thyname/flutter.widgets/column)。

如果你只有一个子组件，请考虑使用 [Align](https://www.yuque.com/thyname/flutter.widgets/align) 或 [Center](https://www.yuque.com/thyname/flutter.widgets/center) 来定位该子组件。

默认情况下，[crossAxisAlignment] 为 [CrossAxisAlignment.center]，它将子组件在垂直轴上居中。如果多个子组件包含文本，且它们具有不同的字体度量（例如因为它们在 [TextStyle.fontSize] 或其他 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 属性上有所不同，或者因为它们使用了因不同文字系统而不同的字体），这可能会使它们在视觉上出现错位。请考虑改用 [CrossAxisAlignment.baseline]。

{@tool snippet}

此示例将可用空间水平分为三份，在前两个单元格中居中显示文本，并在第三个单元格中居中显示 Flutter logo：

![](https://flutter.github.io/assets-for-api-docs/assets/widgets/row.png)

```dart
const Row(
  children: <Widget>[
    Expanded(
      child: Text('Deliver features faster', textAlign: TextAlign.center),
    ),
    Expanded(
      child: Text('Craft beautiful UIs', textAlign: TextAlign.center),
    ),
    Expanded(
      child: FittedBox(
        child: FlutterLogo(),
      ),
    ),
  ],
)
```

{@end-tool}

## 疑难解答

### 为什么我的 row 有黄黑相间的警告条纹？

如果 row 的非灵活内容（那些未包裹在 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 或 [Flexible](https://www.yuque.com/thyname/flutter.widgets/flexible) Widget 中的内容）加起来比 row 本身更宽，则称该 row 已溢出。当 row 溢出时，row 没有剩余空间可在其 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 和 [Flexible](https://www.yuque.com/thyname/flutter.widgets/flexible) 子组件之间共享。row 通过在溢出的边缘绘制黄黑相间的警告框来报告此问题。如果 row 外部有空间，溢出的量会以红色字体打印出来。

#### 故事时间

假设，例如，你有以下代码：

```dart
const Row(
  children: <Widget>[
    FlutterLogo(),
    Text("Flutter's hot reload helps you quickly and easily experiment, build UIs, add features, and fix bug faster. Experience sub-second reload times, without losing state, on emulators, simulators, and hardware for iOS and Android."),
    Icon(Icons.sentiment_very_satisfied),
  ],
)
```

row 首先要求它的第一个子组件 [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 以其想要的任何大小进行布局。该 logo 很友好，欣然决定边长为 24 像素。这为下一个子组件留下了充足的空间。row 随后要求下一个子组件——文本——以它认为最合适的任何大小进行布局。

这时，文本不知道多宽算是太宽，说道："好的，我将会有这么这么这么宽。"，然后远远超出了 row 可用的空间，且不换行。row 回应道："这不公平，现在我没有更多空间留给我的其他子组件了！"，于是生气并长出了一条黄黑相间的条纹。

![](https://flutter.github.io/assets-for-api-docs/assets/widgets/row_error.png)

解决方法是将第二个子组件包裹在 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) Widget 中，这会告诉 row 该子组件应获得剩余的空间：

```dart
const Row(
  children: <Widget>[
    FlutterLogo(),
    Expanded(
      child: Text("Flutter's hot reload helps you quickly and easily experiment, build UIs, add features, and fix bug faster. Experience sub-second reload times, without losing state, on emulators, simulators, and hardware for iOS and Android."),
    ),
    Icon(Icons.sentiment_very_satisfied),
  ],
)
```

现在，row 首先要求 logo 布局，然后要求 _icon_ 布局。[Icon](https://www.yuque.com/thyname/flutter.widgets/icon) 和 logo 一样，很乐意采用一个合理的大小（同样也是 24 像素，这并非巧合，因为 [FlutterLogo](https://www.yuque.com/thyname/flutter.widgets/flutterlogo) 和 [Icon](https://www.yuque.com/thyname/flutter.widgets/icon) 都遵循环境中的 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme)）。这留下了一些剩余空间，现在 row 会准确地告诉文本应该有多宽：剩余空间的确切宽度。文本这次乐于遵从这个合理的要求，在该宽度内换行文本，于是你最终得到了一段分成几行的段落。

![](https://flutter.github.io/assets-for-api-docs/assets/widgets/row_fixed.png)

[textDirection] 属性控制子组件渲染的方向。[TextDirection.ltr] 是 [Row](https://www.yuque.com/thyname/flutter.widgets/row) 子组件的默认 [textDirection]，因此第一个子组件渲染在 [Row](https://www.yuque.com/thyname/flutter.widgets/row) 的 `start` 处，即左侧，后续子组件依次向右排列。如果你想以相反的方向（从右到左）排列子组件，则可以将 [textDirection] 设置为 [TextDirection.rtl]。下面的示例展示了这一点

```dart
const Row(
  textDirection: TextDirection.rtl,
  children: <Widget>[
    FlutterLogo(),
    Expanded(
      child: Text("Flutter's hot reload helps you quickly and easily experiment, build UIs, add features, and fix bug faster. Experience sub-second reload times, without losing state, on emulators, simulators, and hardware for iOS and Android."),
    ),
    Icon(Icons.sentiment_very_satisfied),
  ],
)
```

![](https://flutter.github.io/assets-for-api-docs/assets/widgets/row_textDirection.png)

## 布局算法

_本节描述框架如何渲染 [Row](https://www.yuque.com/thyname/flutter.widgets/row)。_ _有关盒子布局模型的介绍，请参阅 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints)。_

[Row](https://www.yuque.com/thyname/flutter.widgets/row) 的布局分六步进行：

1.  以无边界的水平约束和传入的垂直约束，布局每个具有 null 或零 flex 因子的子组件（例如，非 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 的子组件）。如果 [crossAxisAlignment] 为 [CrossAxisAlignment.stretch]，则改用与传入的最大高度匹配的紧垂直约束。
2.  根据 flex 因子，在具有非零 flex 因子的子组件（例如 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 的子组件）之间分配剩余的水平空间。例如，flex 因子为 2.0 的子组件将获得 flex 因子为 1.0 的子组件两倍的水平空间。
3.  以与第 1 步相同的垂直约束布局剩余的每个子组件，但不使用无边界的水平约束，而是根据第 2 步中分配的空间量使用水平约束。[Flexible.fit] 属性为 [FlexFit.tight] 的子组件将获得紧约束（即强制填满分配的空间），[Flexible.fit] 属性为 [FlexFit.loose] 的子组件将获得松约束（即不强制填满分配的空间）。
4.  [Row](https://www.yuque.com/thyname/flutter.widgets/row) 的高度是子组件的最大高度（这将始终满足传入的垂直约束）。
5.  [Row](https://www.yuque.com/thyname/flutter.widgets/row) 的宽度由 [mainAxisSize] 属性确定。如果 [mainAxisSize] 属性为 [MainAxisSize.max]，则 [Row](https://www.yuque.com/thyname/flutter.widgets/row) 的宽度是传入约束的最大宽度。如果 [mainAxisSize] 属性为 [MainAxisSize.min]，则 [Row](https://www.yuque.com/thyname/flutter.widgets/row) 的宽度是子组件宽度的总和（受传入约束的限制）。
6.  根据 [mainAxisAlignment] 和 [crossAxisAlignment] 确定每个子组件的位置。例如，如果 [mainAxisAlignment] 为 [MainAxisAlignment.spaceBetween]，则未分配给子组件的任何水平空间将被均分并放置在子组件之间。

另请参阅：

- [Column](https://www.yuque.com/thyname/flutter.widgets/column)，垂直方向的等价物。
- [Flex](https://www.yuque.com/thyname/flutter.widgets/flex)，如果你事先不知道想要水平还是垂直排列。
- [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded)，指示应占用所有剩余空间的子组件。
- [Flexible](https://www.yuque.com/thyname/flutter.widgets/flexible)，指示应共享剩余空间、但可能被调整为更小（留下一些未使用的剩余空间）的子组件。
- [Spacer](https://www.yuque.com/thyname/flutter.widgets/spacer)，一个占用与其 flex 值成比例的空间的 Widget。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### Row()

```dart
Row({dynamic key, dynamic mainAxisAlignment, dynamic mainAxisSize, dynamic crossAxisAlignment, dynamic textDirection, dynamic verticalDirection, dynamic textBaseline, double spacing, List<Widget> children})
```

创建一个水平数组的子组件。

如果 [crossAxisAlignment] 为 [CrossAxisAlignment.baseline]，则 [textBaseline] 不能为 null。

[textDirection] 参数默认为环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)（如果有）。如果没有环境中的 directionality，并且在确定布局顺序（除非 row 没有子组件或只有一个子组件，否则总是如此）或消除 [mainAxisAlignment] 的 `start` 或 `end` 值的歧义时需要文本方向，则 [textDirection] 不能为 null。

# Column

```dart
class Column extends Flex {}
```

一个以垂直数组显示其子组件的 Widget。

要使子组件扩展以填充可用的垂直空间，请将子组件包裹在 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) Widget 中。

[Column](https://www.yuque.com/thyname/flutter.widgets/column) Widget 不会滚动（并且通常认为，如果 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 中的子组件数量超过可用空间所能容纳的数量，则属于错误）。如果你有一行 Widget，并且希望在空间不足时它们能够滚动，请考虑使用 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview)。

有关水平方向的变体，请参阅 [Row](https://www.yuque.com/thyname/flutter.widgets/row)。

如果你只有一个子组件，请考虑使用 [Align](https://www.yuque.com/thyname/flutter.widgets/align) 或 [Center](https://www.yuque.com/thyname/flutter.widgets/center) 来定位该子组件。

{@tool snippet}

此示例使用 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 垂直排列三个 Widget，最后一个被设置为填充所有剩余空间。

![以这种方式使用 Column 会创建两行简短的文本，下方是一个大的 Flutter logo。](https://flutter.github.io/assets-for-api-docs/assets/widgets/column.png)

```dart
const Column(
  children: <Widget>[
    Text('Deliver features faster'),
    Text('Craft beautiful UIs'),
    Expanded(
      child: FittedBox(
        child: FlutterLogo(),
      ),
    ),
  ],
)
```

{@end-tool} {@tool snippet}

在上面的示例中，文本和 logo 在每一行上居中。在下面的示例中，[crossAxisAlignment] 设置为 [CrossAxisAlignment.start]，因此子组件左对齐。[mainAxisSize] 设置为 [MainAxisSize.min]，因此该 column 会收缩以适应子组件。

![](https://flutter.github.io/assets-for-api-docs/assets/widgets/column_properties.png)

```dart
Column(
  crossAxisAlignment: CrossAxisAlignment.start,
  mainAxisSize: MainAxisSize.min,
  children: <Widget>[
    const Text('We move under cover and we move as one'),
    const Text('Through the night, we have one shot to live another day'),
    const Text('We cannot let a stray gunshot give us away'),
    const Text('We will fight up close, seize the moment and stay in it'),
    const Text("It's either that or meet the business end of a bayonet"),
    const Text("The code word is 'Rochambeau,' dig me?"),
    Text('Rochambeau!', style: DefaultTextStyle.of(context).style.apply(fontSizeFactor: 2.0)),
  ],
)
```

{@end-tool}

## 疑难解答

### 当传入的垂直约束是无边界的时

当一个 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 拥有一个或多个 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 或 [Flexible](https://www.yuque.com/thyname/flutter.widgets/flexible) 子组件，并且被放置在另一个 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 中，或在一个 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview) 中，或在任何其他不为 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 提供最大高度约束的环境中，你在运行时会得到一个异常，提示存在非零 flex 的子组件，但垂直约束是无边界的。

如异常附带的详情所述，问题在于使用 [Flexible](https://www.yuque.com/thyname/flutter.widgets/flexible) 或 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 意味着在布局完所有其他子组件后的剩余空间必须均分，但如果传入的垂直约束是无边界的，剩余空间就是无限的。

解决此问题的关键通常是确定为什么 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 收到了无边界的垂直约束。

导致这种情况发生的一个常见原因是，[Column](https://www.yuque.com/thyname/flutter.widgets/column) 被放置在另一个 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 中（且未在内部嵌套的 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 周围使用 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 或 [Flexible](https://www.yuque.com/thyname/flutter.widgets/flexible)）。当一个 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 布局其非 flex 子组件（那些未被 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 或 [Flexible](https://www.yuque.com/thyname/flutter.widgets/flexible) 包裹的子组件）时，它会给它们无边界的约束，以便它们能够确定自己的尺寸（传入无边界约束通常是向子组件发出信号，表示它应该收缩以适应其内容）。这种情况下的解决方案通常只是将内部的 column 包裹在一个 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 中，以表明它应该占用外部 column 的剩余空间，而不是被允许占用它想要的任意空间量。

导致此消息显示的另一个原因是将一个 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 嵌套在 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview) 或其他垂直可滚动组件中。在该场景中，确实存在无限的垂直空间（这正是垂直滚动列表的全部意义所在——允许垂直方向上的无限空间）。在这种场景中，通常值得检查为什么内部的 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 应该有一个 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 或 [Flexible](https://www.yuque.com/thyname/flutter.widgets/flexible) 子组件：内部的子组件真正应该是什么大小？这种情况下的解决方案通常是从内部子组件周围移除 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 或 [Flexible](https://www.yuque.com/thyname/flutter.widgets/flexible) Widget。

{@youtube 560 315 https://www.youtube.com/watch?v=jckqXR5CrPI}

有关约束的更多讨论，请参阅 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints)。

### 黄黑相间的条纹横幅

当 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 的内容超过可用空间量时，[Column](https://www.yuque.com/thyname/flutter.widgets/column) 会溢出，内容会被裁剪。在调试模式下，会在溢出的边缘渲染一条黄黑相间的条纹，并在 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 下方打印一条消息，说明检测到的溢出量。

通常的解决方案是使用 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview) 而不是 [Column](https://www.yuque.com/thyname/flutter.widgets/column)，以便在垂直空间有限时使内容能够滚动。

## 布局算法

_本节描述框架如何渲染 [Column](https://www.yuque.com/thyname/flutter.widgets/column)。_ _有关盒子布局模型的介绍，请参阅 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints)。_

[Column](https://www.yuque.com/thyname/flutter.widgets/column) 的布局分六步进行：

1.  以无边界的垂直约束和传入的水平约束，布局每个具有 null 或零 flex 因子的子组件（例如，非 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 的子组件）。如果 [crossAxisAlignment] 为 [CrossAxisAlignment.stretch]，则改用与传入的最大宽度匹配的紧水平约束。
2.  根据 flex 因子，在具有非零 flex 因子的子组件（例如 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 的子组件）之间分配剩余的垂直空间。例如，flex 因子为 2.0 的子组件将获得 flex 因子为 1.0 的子组件两倍的垂直空间。
3.  以与第 1 步相同的水平约束布局剩余的每个子组件，但不使用无边界的垂直约束，而是根据第 2 步中分配的空间量使用垂直约束。[Flexible.fit] 属性为 [FlexFit.tight] 的子组件将获得紧约束（即强制填满分配的空间），[Flexible.fit] 属性为 [FlexFit.loose] 的子组件将获得松约束（即不强制填满分配的空间）。
4.  [Column](https://www.yuque.com/thyname/flutter.widgets/column) 的宽度是子组件的最大宽度（这将始终满足传入的水平约束）。
5.  [Column](https://www.yuque.com/thyname/flutter.widgets/column) 的高度由 [mainAxisSize] 属性确定。如果 [mainAxisSize] 属性为 [MainAxisSize.max]，则 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 的高度是传入约束的最大高度。如果 [mainAxisSize] 属性为 [MainAxisSize.min]，则 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 的高度是子组件高度的总和（受传入约束的限制）。
6.  根据 [mainAxisAlignment] 和 [crossAxisAlignment] 确定每个子组件的位置。例如，如果 [mainAxisAlignment] 为 [MainAxisAlignment.spaceBetween]，则未分配给子组件的任何垂直空间将被均分并放置在子组件之间。

另请参阅：

- [Row](https://www.yuque.com/thyname/flutter.widgets/row)，水平方向的等价物。
- [Flex](https://www.yuque.com/thyname/flutter.widgets/flex)，如果你事先不知道想要水平还是垂直排列。
- [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded)，指示应占用所有剩余空间的子组件。
- [Flexible](https://www.yuque.com/thyname/flutter.widgets/flexible)，指示应共享剩余空间、但可能会调整为更小（留下一些未使用的剩余空间）的子组件。
- [SingleChildScrollView](https://www.yuque.com/thyname/flutter.widgets/singlechildscrollview)，其文档讨论了在滚动容器中使用 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 的一些方法。
- [Spacer](https://www.yuque.com/thyname/flutter.widgets/spacer)，一个占用与其 flex 值成比例的空间的 Widget。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### Column()

```dart
Column({dynamic key, dynamic mainAxisAlignment, dynamic mainAxisSize, dynamic crossAxisAlignment, dynamic textDirection, dynamic verticalDirection, dynamic textBaseline, double spacing, List<Widget> children})
```

创建一个垂直数组的子组件。

如果 [crossAxisAlignment] 为 [CrossAxisAlignment.baseline]，则 [textBaseline] 不能为 null。

[textDirection] 参数默认为环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)（如果有）。如果没有环境中的 directionality，并且在消除 [crossAxisAlignment] 的 `start` 或 `end` 值的歧义时需要文本方向，则 [textDirection] 不能为 null。

# Flexible

```dart
class Flexible extends ParentDataWidget<FlexParentData> {}
```

一个控制 [Row](https://www.yuque.com/thyname/flutter.widgets/row)、[Column](https://www.yuque.com/thyname/flutter.widgets/column) 或 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 的子组件如何伸缩的 Widget。

使用 [Flexible](https://www.yuque.com/thyname/flutter.widgets/flexible) Widget 可赋予 [Row](https://www.yuque.com/thyname/flutter.widgets/row)、[Column](https://www.yuque.com/thyname/flutter.widgets/column) 或 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 的子组件在主轴方向（例如，[Row](https://www.yuque.com/thyname/flutter.widgets/row) 的水平方向或 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 的垂直方向）上扩展以填充可用空间的灵活性，但与 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 不同，[Flexible](https://www.yuque.com/thyname/flutter.widgets/flexible) 不要求子组件填满可用空间。

[Flexible](https://www.yuque.com/thyname/flutter.widgets/flexible) Widget 必须是 [Row](https://www.yuque.com/thyname/flutter.widgets/row)、[Column](https://www.yuque.com/thyname/flutter.widgets/column) 或 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 的后代，并且从 [Flexible](https://www.yuque.com/thyname/flutter.widgets/flexible) Widget 到其封闭的 [Row](https://www.yuque.com/thyname/flutter.widgets/row)、[Column](https://www.yuque.com/thyname/flutter.widgets/column) 或 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 的路径只能包含 [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget) 或 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget)（不能包含其他类型的 Widget，如 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget)）。

{@youtube 560 315 https://www.youtube.com/watch?v=CI7x0mAZiY0}

另请参阅：

- [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded)，强制子组件扩展以填充可用空间。
- [Spacer](https://www.yuque.com/thyname/flutter.widgets/spacer)，一个占用与其 flex 值成比例的空间的 Widget。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### Flexible()

```dart
Flexible({dynamic key, int flex = 1, FlexFit fit = FlexFit.loose, required Widget child})
```

创建一个控制 [Row](https://www.yuque.com/thyname/flutter.widgets/row)、[Column](https://www.yuque.com/thyname/flutter.widgets/column) 或 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 的子组件如何伸缩的 Widget。

### flex

```dart
int flex
```

用于此子组件的 flex 因子。

如果为零，子组件是不灵活的，并自行确定其大小。如果非零，子组件在主轴上可占用的空间量由根据灵活子组件的 flex 因子分配剩余空间（在放置不灵活的子组件之后）来确定。

### fit

```dart
FlexFit fit
```

灵活子组件如何嵌入到可用空间中。

如果 [flex] 非零，[fit] 决定子组件是否填满父容器在布局期间提供的空间。如果 fit 为 [FlexFit.tight]，则要求子组件填满可用空间。如果 fit 为 [FlexFit.loose]，子组件最多可以和可用空间一样大（但允许更小）。

### applyParentData()

```dart
void applyParentData(RenderObject renderObject)
```

### debugTypicalAncestorWidgetClass

```dart
Type get debugTypicalAncestorWidgetClass
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# Expanded

```dart
class Expanded extends Flexible {}
```

一个扩展 [Row](https://www.yuque.com/thyname/flutter.widgets/row)、[Column](https://www.yuque.com/thyname/flutter.widgets/column) 或 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 的子组件、使其填充可用空间的 Widget。

使用 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) Widget 可使 [Row](https://www.yuque.com/thyname/flutter.widgets/row)、[Column](https://www.yuque.com/thyname/flutter.widgets/column) 或 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 的子组件在主轴方向（例如，[Row](https://www.yuque.com/thyname/flutter.widgets/row) 的水平方向或 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 的垂直方向）上扩展以填充可用空间。如果多个子组件都被扩展，则可用空间会根据 [flex] 因子在它们之间分配。

[Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) Widget 必须是 [Row](https://www.yuque.com/thyname/flutter.widgets/row)、[Column](https://www.yuque.com/thyname/flutter.widgets/column) 或 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 的后代，并且从 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) Widget 到其封闭的 [Row](https://www.yuque.com/thyname/flutter.widgets/row)、[Column](https://www.yuque.com/thyname/flutter.widgets/column) 或 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 的路径只能包含 [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget) 或 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget)（不能包含其他类型的 Widget，如 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget)）。

{@youtube 560 315 https://www.youtube.com/watch?v=_rnZaagadyo}

{@tool dartpad} 此示例展示了如何在 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 中使用 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) Widget，以便其中间子组件（此处为一个 [Container](https://www.yuque.com/thyname/flutter.widgets/container)）扩展以填充空间。

![这会产生两个薄的蓝色盒子，中间是一个较大的琥珀色盒子。](https://flutter.github.io/assets-for-api-docs/assets/widgets/expanded_column.png)

** 参见 examples/api/lib/widgets/basic/expanded.0.dart 中的代码 ** {@end-tool}

{@tool dartpad} 此示例展示了如何在 [Row](https://www.yuque.com/thyname/flutter.widgets/row) 中使用多个子组件扩展的 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) Widget，利用 [flex] 因子来优先分配可用空间。

![这会产生一个宽的琥珀色盒子，接着是一个薄的蓝色盒子，末尾是一个中等宽度的琥珀色盒子。](https://flutter.github.io/assets-for-api-docs/assets/widgets/expanded_row.png)

** 参见 examples/api/lib/widgets/basic/expanded.1.dart 中的代码 ** {@end-tool}

另请参阅：

- [Flexible](https://www.yuque.com/thyname/flutter.widgets/flexible)，不强制子组件填满可用空间。
- [Spacer](https://www.yuque.com/thyname/flutter.widgets/spacer)，一个占用与其 flex 值成比例的空间的 Widget。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### Expanded()

```dart
Expanded({dynamic key, int flex, required Widget child})
```

创建一个扩展 [Row](https://www.yuque.com/thyname/flutter.widgets/row)、[Column](https://www.yuque.com/thyname/flutter.widgets/column) 或 [Flex](https://www.yuque.com/thyname/flutter.widgets/flex) 的子组件、使其沿 flex Widget 主轴填充可用空间的 Widget。

# Wrap

```dart
class Wrap extends MultiChildRenderObjectWidget {}
```

一个以多个水平或垂直行显示其子组件的 Widget。

[Wrap](https://www.yuque.com/thyname/flutter.widgets/wrap) 布局每个子组件，并尝试将子组件在主轴（由 [direction] 给出）方向上放置在前一个子组件的旁边，两者之间留有 [spacing] 的间距。如果没有足够的空间容纳子组件，[Wrap](https://www.yuque.com/thyname/flutter.widgets/wrap) 会在交叉轴方向上创建一个与现有子组件相邻的新 _行（run）_。

在所有子组件都被分配到行之后，行内的子组件会根据主轴上的 [alignment] 和交叉轴上的 [crossAxisAlignment] 进行定位。

然后，行本身会根据 [runSpacing] 和 [runAlignment] 在交叉轴上进行定位。

{@youtube 560 315 https://www.youtube.com/watch?v=z5iw2SeFx2M}

{@tool snippet}

此示例在一个 [Wrap](https://www.yuque.com/thyname/flutter.widgets/wrap) 中渲染了一些代表四位联系人的 [Chip](https://www.yuque.com/thyname/flutter.material/chip)，以便它们根据需要跨行排列。

```dart
Wrap(
  spacing: 8.0, // gap between adjacent chips
  runSpacing: 4.0, // gap between lines
  children: <Widget>[
    Chip(
      avatar: CircleAvatar(backgroundColor: Colors.blue.shade900, child: const Text('AH')),
      label: const Text('Hamilton'),
    ),
    Chip(
      avatar: CircleAvatar(backgroundColor: Colors.blue.shade900, child: const Text('ML')),
      label: const Text('Lafayette'),
    ),
    Chip(
      avatar: CircleAvatar(backgroundColor: Colors.blue.shade900, child: const Text('HM')),
      label: const Text('Mulligan'),
    ),
    Chip(
      avatar: CircleAvatar(backgroundColor: Colors.blue.shade900, child: const Text('JL')),
      label: const Text('Laurens'),
    ),
  ],
)
```

{@end-tool}

另请参阅：

- [Row](https://www.yuque.com/thyname/flutter.widgets/row)，将子组件放置在一行中，并对其对齐方式和间距提供控制。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### Wrap()

```dart
Wrap({dynamic key, Axis direction = Axis.horizontal, WrapAlignment alignment = WrapAlignment.start, double spacing = 0.0, WrapAlignment runAlignment = WrapAlignment.start, double runSpacing = 0.0, WrapCrossAlignment crossAxisAlignment = WrapCrossAlignment.start, TextDirection? textDirection, VerticalDirection verticalDirection = VerticalDirection.down, Clip clipBehavior = Clip.none, List<Widget> children})
```

创建一个 wrap 布局。

默认情况下，wrap 布局是水平的，子组件和行都对齐到起始位置。

[textDirection] 参数默认为环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)（如果有）。如果没有环境中的 directionality，并且在决定子组件的排列方向或消除主轴或交叉轴方向的 `start` 或 `end` 值的歧义时需要文本方向，则 [textDirection] 不能为 null。

### direction

```dart
Axis direction
```

用作主轴的方向。

例如，如果 [direction] 为默认值 [Axis.horizontal]，子组件会彼此相邻放置在一个水平行中，直到可用的水平空间耗尽，此时后续的子组件会被放置在与前一行垂直相邻的新行中。

### alignment

```dart
WrapAlignment alignment
```

一行内的子组件应如何在主轴上放置。

例如，如果 [alignment] 为 [WrapAlignment.center]，则每一行中的子组件会在其行的主轴上分组居中。

默认为 [WrapAlignment.start]。

另请参阅：

- [runAlignment]，控制各行相对于彼此在交叉轴上的放置方式。
- [crossAxisAlignment]，控制每一行内的子组件相对于彼此在交叉轴上的放置方式。

### spacing

```dart
double spacing
```

一行内子组件在主轴上应间隔多少空间。

例如，如果 [spacing] 为 10.0，子组件在主轴上将至少相隔 10.0 逻辑像素。

如果一行中有额外的自由空间（例如，因为 wrap 有一个未被填满的最小大小，或者因为某些行比其他行更长），额外的自由空间将根据 [alignment] 分配。

默认为 0.0。

### runAlignment

```dart
WrapAlignment runAlignment
```

各行本身应如何在交叉轴上放置。

例如，如果 [runAlignment] 为 [WrapAlignment.center]，各行会在整个 [Wrap](https://www.yuque.com/thyname/flutter.widgets/wrap) 的交叉轴上分组居中。

默认为 [WrapAlignment.start]。

另请参阅：

- [alignment]，控制每一行内的子组件相对于彼此在主轴上的放置方式。
- [crossAxisAlignment]，控制每一行内的子组件相对于彼此在交叉轴上的放置方式。

### runSpacing

```dart
double runSpacing
```

各行本身在交叉轴上应间隔多少空间。

例如，如果 [runSpacing] 为 10.0，各行在交叉轴上将至少相隔 10.0 逻辑像素。

如果整个 [Wrap](https://www.yuque.com/thyname/flutter.widgets/wrap) 中有额外的自由空间（例如，因为 wrap 有一个未被填满的最小大小），额外的自由空间将根据 [runAlignment] 分配。

默认为 0.0。

### crossAxisAlignment

```dart
WrapCrossAlignment crossAxisAlignment
```

一行内的子组件应如何相对于彼此在交叉轴上对齐。

例如，如果此值设置为 [WrapCrossAlignment.end]，且 [direction] 为 [Axis.horizontal]，则每一行内的子组件的底部边缘将与该行的底部边缘对齐。

默认为 [WrapCrossAlignment.start]。

另请参阅：

- [alignment]，控制每一行内的子组件相对于彼此在主轴上的放置方式。
- [runAlignment]，控制各行相对于彼此在交叉轴上的放置方式。

### textDirection

```dart
TextDirection? textDirection
```

确定水平排列子组件的顺序，以及如何在水平方向上解释 `start` 和 `end`。

默认为环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)。

如果 [direction] 为 [Axis.horizontal]，这将控制子组件的定位顺序（从左到右或从右到左），以及 [alignment] 属性中 [WrapAlignment.start] 和 [WrapAlignment.end] 值的含义。

如果 [direction] 为 [Axis.horizontal]，且 [alignment] 为 [WrapAlignment.start] 或 [WrapAlignment.end]，或者有多个子组件，则 [textDirection]（或环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)）不能为 null。

如果 [direction] 为 [Axis.vertical]，这将控制各行的定位顺序，[runAlignment] 属性中 [WrapAlignment.start] 和 [WrapAlignment.end] 值的含义，以及 [crossAxisAlignment] 属性中 [WrapCrossAlignment.start] 和 [WrapCrossAlignment.end] 值的含义。

如果 [direction] 为 [Axis.vertical]，且 [runAlignment] 为 [WrapAlignment.start] 或 [WrapAlignment.end]、[crossAxisAlignment] 为 [WrapCrossAlignment.start] 或 [WrapCrossAlignment.end]，或者有多个子组件，则 [textDirection]（或环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)）不能为 null。

### verticalDirection

```dart
VerticalDirection verticalDirection
```

确定垂直排列子组件的顺序，以及如何在垂直方向上解释 `start` 和 `end`。

如果 [direction] 为 [Axis.vertical]，这将控制子组件的绘制顺序（向下或向上），以及 [alignment] 属性中 [WrapAlignment.start] 和 [WrapAlignment.end] 值的含义。

如果 [direction] 为 [Axis.vertical]，且 [alignment] 为 [WrapAlignment.start] 或 [WrapAlignment.end]，或者有多个子组件，则 [verticalDirection] 不能为 null。

如果 [direction] 为 [Axis.horizontal]，这将控制各行的定位顺序，[runAlignment] 属性中 [WrapAlignment.start] 和 [WrapAlignment.end] 值的含义，以及 [crossAxisAlignment] 属性中 [WrapCrossAlignment.start] 和 [WrapCrossAlignment.end] 值的含义。

如果 [direction] 为 [Axis.horizontal]，且 [runAlignment] 为 [WrapAlignment.start] 或 [WrapAlignment.end]、[crossAxisAlignment] 为 [WrapCrossAlignment.start] 或 [WrapCrossAlignment.end]，或者有多个子组件，则 [verticalDirection] 不能为 null。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

默认为 [Clip.none]。

### createRenderObject()

```dart
RenderWrap createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderWrap renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# Flow

```dart
class Flow extends MultiChildRenderObjectWidget {}
```

一个根据 [FlowDelegate](https://www.yuque.com/thyname/flutter.rendering/flowdelegate) 中的逻辑高效地调整和定位子组件大小及位置的 Widget。

{@youtube 560 315 https://www.youtube.com/watch?v=NG6pvXpnIso}

Flow 布局针对使用变换矩阵重新定位子组件进行了优化。

flow 容器由委托的 [FlowDelegate.getSize] 函数独立于子组件调整大小。然后，子组件根据委托的 [FlowDelegate.getConstraintsForChild] 函数给出的约束独立调整大小。

子组件不是在布局期间定位，而是在绘制阶段使用来自 [FlowDelegate.paintChildren] 函数的矩阵、通过变换矩阵进行定位。通过仅 _重新绘制_ flow，可以高效地重新定位子组件，这一过程无需重新布局子组件（与之相对的是 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack)，它在布局期间同时完成大小调整和定位）。

触发 flow 重绘的最有效方式是为 [FlowDelegate](https://www.yuque.com/thyname/flutter.rendering/flowdelegate) 的构造函数提供一个动画。flow 将监听此动画，并在动画每次 tick 时重新绘制，从而避免流水线的构建和布局阶段。

{@tool dartpad} 此示例使用 [Flow](https://www.yuque.com/thyname/flutter.widgets/flow) Widget 创建一个随交互而打开和关闭的菜单，如上所示。菜单中按钮的颜色会随所选按钮的变化而变化。

** 参见 examples/api/lib/widgets/basic/flow.0.dart 中的代码 ** {@end-tool}

## 命中测试与隐藏的 [Flow](https://www.yuque.com/thyname/flutter.widgets/flow) Widget

[Flow](https://www.yuque.com/thyname/flutter.widgets/flow) Widget 在 _绘制_ 阶段而非 _布局_ 阶段重新计算其子组件的位置（用于命中测试）。

诸如 [Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity) 之类的 Widget 会在其子组件因不透明度为零而不可见时避免绘制它们。

不幸的是，这意味着使用 [Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity) Widget 隐藏 [Flow](https://www.yuque.com/thyname/flutter.widgets/flow) Widget 会在用户尝试与隐藏区域交互时（例如通过点按或单击）导致错误。

此类错误会表现为过时的几何形状（点按操作发送到与当前指定 [FlowDelegate](https://www.yuque.com/thyname/flutter.rendering/flowdelegate) 所预期不同的 Widget）或异常（例如，如果上次绘制 [Flow](https://www.yuque.com/thyname/flutter.widgets/flow) 时指定了一组不同的子组件）。

为避免这种情况，当使用 [Opacity](https://www.yuque.com/thyname/flutter.widgets/opacity) Widget（或 [AnimatedOpacity](https://www.yuque.com/thyname/flutter.widgets/animatedopacity) 或类似组件）隐藏 [Flow](https://www.yuque.com/thyname/flutter.widgets/flow) Widget 时，明智的做法是同时使用 [IgnorePointer](https://www.yuque.com/thyname/flutter.widgets/ignorepointer) 禁用该 Widget 上的命中测试。无论如何，这通常都是很好的建议，因为对不可见的 Widget 进行命中测试通常会让用户感到困惑。

另请参阅：

- [Wrap](https://www.yuque.com/thyname/flutter.widgets/wrap)，提供了一些其他框架称为"flow"的布局模型，与 [Flow](https://www.yuque.com/thyname/flutter.widgets/flow) 并无关联。
- [Stack](https://www.yuque.com/thyname/flutter.widgets/stack)，相对于容器的边缘排列子组件。
- [CustomSingleChildLayout](https://www.yuque.com/thyname/flutter.widgets/customsinglechildlayout)，使用委托来控制单个子组件的布局。
- [CustomMultiChildLayout](https://www.yuque.com/thyname/flutter.widgets/custommultichildlayout)，使用委托来定位多个子组件。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### Flow()

```dart
Flow({dynamic key, required FlowDelegate delegate, List<Widget> children = const <Widget>[], Clip clipBehavior = Clip.hardEdge})
```

创建一个 flow 布局。

将每个给定的子组件包裹在一个 [RepaintBoundary](https://www.yuque.com/thyname/flutter.widgets/repaintboundary) 中，以避免在 flow 重绘时重绘子组件。

### Flow.unwrapped()

```dart
Flow.unwrapped({dynamic key, required FlowDelegate delegate, List<Widget> children, Clip clipBehavior = Clip.hardEdge})
```

创建一个 flow 布局。

与默认构造函数不同，不会将给定的子组件包裹在重绘边界中。当子组件的绘制很简单或已经包含重绘边界时很有用。

### delegate

```dart
FlowDelegate delegate
```

控制子组件变换矩阵的委托。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

默认为 [Clip.hardEdge]。

### createRenderObject()

```dart
RenderFlow createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderFlow renderObject)
```

# RichText

```dart
class RichText extends MultiChildRenderObjectWidget {}
```

一段富文本段落。

{@youtube 560 315 https://www.youtube.com/watch?v=rykDVh-QFfw}

[RichText](https://www.yuque.com/thyname/flutter.widgets/richtext) 组件用于显示使用多种不同样式的文本。要显示的文本通过一棵 [TextSpan](https://www.yuque.com/thyname/flutter.painting/textspan) 对象组成的树来描述，每个 [TextSpan](https://www.yuque.com/thyname/flutter.painting/textspan) 都有一个关联的样式，该样式将应用于对应的子树。根据布局约束的不同，文本可能会跨多行显示，也可能全部显示在同一行上。

[RichText](https://www.yuque.com/thyname/flutter.widgets/richtext) 组件中显示的文本必须显式设置样式。在选择使用哪种样式时，可以考虑使用当前 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的 [DefaultTextStyle.of] 来提供默认值。[MediaQuery.maybeBoldTextOf]、[MediaQuery.maybeLineHeightScaleFactorOverrideOf]、[MediaQuery.maybeLetterSpacingOverrideOf]、[MediaQuery.maybeWordSpacingOverrideOf] 以及 [MediaQuery.maybeParagraphSpacingOverrideOf] 也可用于确保文本样式符合无障碍需求。有关如何在 [RichText](https://www.yuque.com/thyname/flutter.widgets/richtext) 组件中设置文本样式的更多细节，请参阅 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 的文档。

可以考虑使用 [Text](https://www.yuque.com/thyname/flutter.widgets/text) 组件以自动与 [DefaultTextStyle](https://www.yuque.com/thyname/flutter.widgets/defaulttextstyle) 集成。当所有文本都使用相同的样式时，使用默认构造函数会更简洁。[Text.rich] 构造函数允许你在为多个片段设置样式的同时，仍然使用默认文本样式。

{@tool snippet}

此示例演示了如何使用 [RichText](https://www.yuque.com/thyname/flutter.widgets/richtext) 组件混合搭配不同文本样式的文本。它会显示文本 "Hello bold world,"，其中 "bold" 一词以粗体字重突出显示。

![](https://flutter.github.io/assets-for-api-docs/assets/widgets/rich_text.png)

```dart
RichText(
  text: TextSpan(
    text: 'Hello ',
    style: DefaultTextStyle.of(context).style,
    children: const <TextSpan>[
      TextSpan(text: 'bold', style: TextStyle(fontWeight: FontWeight.bold)),
      TextSpan(text: ' world!'),
    ],
  ),
)
```

{@end-tool}

## 选择（Selections）

要使此 [RichText](https://www.yuque.com/thyname/flutter.widgets/richtext) 可选中，需要将 [RichText](https://www.yuque.com/thyname/flutter.widgets/richtext) 置于 [SelectionArea](https://www.yuque.com/thyname/flutter.material/selectionarea) 或 [SelectableRegion](https://www.yuque.com/thyname/flutter.widgets/selectableregion) 的子树中，并为 [RichText.selectionRegistrar] 分配一个 [SelectionRegistrar](https://www.yuque.com/thyname/flutter.rendering/selectionregistrar)。可以使用 [SelectionContainer.maybeOf] 从位于 [SelectionArea](https://www.yuque.com/thyname/flutter.material/selectionarea) 或 [SelectableRegion](https://www.yuque.com/thyname/flutter.widgets/selectableregion) 之下的上下文中获取 [SelectionRegistrar](https://www.yuque.com/thyname/flutter.rendering/selectionregistrar)。这使用户能够通过鼠标或触摸事件选中 [RichText](https://www.yuque.com/thyname/flutter.widgets/richtext) 中的文本。

如果同一个 build 方法同时创建了 [SelectionArea](https://www.yuque.com/thyname/flutter.material/selectionarea) 和 [RichText](https://www.yuque.com/thyname/flutter.widgets/richtext)，请使用 [Builder](https://www.yuque.com/thyname/flutter.widgets/builder)，以便 [SelectionContainer.maybeOf] 能够使用位于 [SelectionArea](https://www.yuque.com/thyname/flutter.material/selectionarea) 之下的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 进行调用。

如果启用了选择功能，还需要设置 [selectionColor]，以便绘制选中高亮效果。

{@tool snippet}

此示例演示了如何为 SelectionArea 子树中的 RichText 分配 [SelectionRegistrar](https://www.yuque.com/thyname/flutter.rendering/selectionregistrar)。

![](https://flutter.github.io/assets-for-api-docs/assets/widgets/rich_text.png)

```dart
SelectionArea(
  child: Builder(
    builder: (BuildContext context) {
      return RichText(
        text: const TextSpan(text: 'Hello'),
        selectionRegistrar: SelectionContainer.maybeOf(context),
        selectionColor: const Color(0xAF6694e8),
      );
    },
  ),
)
```

{@end-tool}

另请参阅：

- [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle)，讨论了如何为文本设置样式。
- [TextSpan](https://www.yuque.com/thyname/flutter.painting/textspan)，用于描述段落中的文本。
- [Text](https://www.yuque.com/thyname/flutter.widgets/text)，会自动将 [DefaultTextStyle](https://www.yuque.com/thyname/flutter.widgets/defaulttextstyle) 所描述的环境样式应用于单个字符串。
- [Text.rich]，一个 const 文本组件，提供与 [RichText](https://www.yuque.com/thyname/flutter.widgets/richtext) 类似的功能。[Text.rich] 将从 [DefaultTextStyle](https://www.yuque.com/thyname/flutter.widgets/defaulttextstyle) 继承 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle)。
- [SelectableRegion](https://www.yuque.com/thyname/flutter.widgets/selectableregion)，提供了选择系统的概述。

### RichText()

```dart
RichText({dynamic key, required InlineSpan text, TextAlign textAlign = TextAlign.start, TextDirection? textDirection, bool softWrap = true, TextOverflow overflow = TextOverflow.clip, double textScaleFactor = 1.0, TextScaler textScaler = TextScaler.noScaling, int? maxLines, Locale? locale, StrutStyle? strutStyle, TextWidthBasis textWidthBasis = TextWidthBasis.parent, ui.TextHeightBehavior? textHeightBehavior, SelectionRegistrar? selectionRegistrar, Color? selectionColor})
```

创建一段富文本段落。

[maxLines] 属性可以为 null（实际上默认就是 null），但如果它不为 null，则必须大于零。

[textDirection] 如果为 null，则默认为环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)，此时该值不得为 null。

### text

```dart
InlineSpan text
```

要在此组件中显示的文本。

### textAlign

```dart
TextAlign textAlign
```

文本应如何水平对齐。

### textDirection

```dart
TextDirection? textDirection
```

文本的方向性。

这决定了如何解释 [textAlign] 的值，例如 [TextAlign.start] 和 [TextAlign.end]。

它还用于消除双向文本渲染方式的歧义。例如，如果 [text] 是一段英文短语后跟一段希伯来语短语，在 [TextDirection.ltr] 环境下，英文短语会显示在左侧、希伯来语短语显示在其右侧；而在 [TextDirection.rtl] 环境下，英文短语会显示在右侧、希伯来语短语显示在其左侧。

默认为环境中的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)（如果存在）。如果不存在环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)，则该值不得为 null。

### softWrap

```dart
bool softWrap
```

文本是否应在软换行处断行。

如果为 false，文本中的字形将按照拥有无限水平空间的方式进行定位。

### overflow

```dart
TextOverflow overflow
```

应如何处理视觉溢出。

### textScaleFactor

```dart
double get textScaleFactor
```

已弃用。将在 Flutter 未来版本中移除。请改用 [textScaler]。

每个逻辑像素对应的字体像素数。

例如，如果文本缩放系数为 1.5，文本将比指定字体大小放大 50%。

### textScaler

```dart
TextScaler textScaler
```

{@macro flutter.painting.textPainter.textScaler}

### maxLines

```dart
int? maxLines
```

文本可跨越的最大行数（可选），超出部分将自动换行。如果文本超出给定的行数，将根据 [overflow] 进行截断。

如果该值为 1，文本将不换行。否则，文本将在方框边缘处换行。

### locale

```dart
Locale? locale
```

用于在同一个 Unicode 字符可能因语言区域不同而以不同方式渲染时选择字体。

通常很少需要设置此属性。默认情况下，其值继承自 `Localizations.localeOf(context)` 所在的外层应用。

更多信息请参阅 [RenderParagraph.locale]。

### strutStyle

```dart
StrutStyle? strutStyle
```

{@macro flutter.painting.textPainter.strutStyle}

### textWidthBasis

```dart
TextWidthBasis textWidthBasis
```

{@macro flutter.painting.textPainter.textWidthBasis}

### textHeightBehavior

```dart
ui.TextHeightBehavior? textHeightBehavior
```

{@macro dart.ui.textHeightBehavior}

### selectionRegistrar

```dart
SelectionRegistrar? selectionRegistrar
```

此富文本所订阅的 [SelectionRegistrar](https://www.yuque.com/thyname/flutter.rendering/selectionregistrar)。

如果设置了此项，则 [selectionColor] 必须非空。

### selectionColor

```dart
Color? selectionColor
```

绘制选中内容时使用的颜色。

如果 [selectionRegistrar] 为 null，则忽略此项。

有关如何在 [RichText](https://www.yuque.com/thyname/flutter.widgets/richtext) 组件中启用选择功能的更多细节，请参阅 [RichText](https://www.yuque.com/thyname/flutter.widgets/richtext) 顶层 API 文档中关于选择的章节。

### createRenderObject()

```dart
RenderParagraph createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderParagraph renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RawImage

```dart
class RawImage extends LeafRenderObjectWidget {}
```

一个直接显示 [dart:ui.Image] 的组件。

该图片使用 [paintImage](https://www.yuque.com/thyname/flutter.painting/paintimage) 进行绘制，[paintImage](https://www.yuque.com/thyname/flutter.painting/paintimage) 详细描述了此类中各字段的含义。

此组件不会释放（dispose）[image]。该组件的创建者需要在 [RawImage](https://www.yuque.com/thyname/flutter.widgets/rawimage) 不再可构建时对 [image] 调用 [dart:ui.Image.dispose]。

`scale` 参数指定以图片预期尺寸绘制时使用的线性缩放系数，同时应用于宽度和高度。{@macro flutter.painting.imageInfo.scale}

此组件很少被直接使用。请考虑改用 [Image](https://www.yuque.com/thyname/dart.ui/image)。

### RawImage()

```dart
RawImage({dynamic key, ui.Image? image, String? debugImageLabel, double? width, double? height, double scale = 1.0, Color? color, Animation<double>? opacity, BlendMode? colorBlendMode, BoxFit? fit, AlignmentGeometry alignment = Alignment.center, ImageRepeat repeat = ImageRepeat.noRepeat, Rect? centerSlice, bool matchTextDirection = false, bool invertColors = false, FilterQuality filterQuality = FilterQuality.medium, bool isAntiAlias = false})
```

创建一个显示图片的组件。

[scale]、[alignment]、[repeat]、[matchTextDirection] 和 [filterQuality] 参数不得为 null。

### image

```dart
ui.Image? image
```

要显示的图片。

由于 [RawImage](https://www.yuque.com/thyname/flutter.widgets/rawimage) 是无状态的，它不会释放此图片。[RawImage](https://www.yuque.com/thyname/flutter.widgets/rawimage) 的创建者需要在不再需要该 [RawImage](https://www.yuque.com/thyname/flutter.widgets/rawimage) 时对此图片句柄调用 [dart:ui.Image.dispose]。

### debugImageLabel

```dart
String? debugImageLabel
```

用于标识图片来源的字符串。

### width

```dart
double? width
```

如果非空，则要求图片具有此宽度。

如果为 null，图片将选择最能保持其固有宽高比的尺寸。

### height

```dart
double? height
```

如果非空，则要求图片具有此高度。

如果为 null，图片将选择最能保持其固有宽高比的尺寸。

### scale

```dart
double scale
```

以预期尺寸绘制此图片时使用的线性缩放系数。

该缩放系数同时应用于宽度和高度。

{@macro flutter.painting.imageInfo.scale}

### color

```dart
Color? color
```

如果非空，此颜色将使用 [colorBlendMode] 与每个图片像素混合。

### opacity

```dart
Animation<double>? opacity
```

如果非空，[Animation](https://www.yuque.com/thyname/flutter.animation/animation) 中的值将在绘制到画布之前与每个图片像素的不透明度相乘。

这比使用 [FadeTransition](https://www.yuque.com/thyname/flutter.widgets/fadetransition) 来改变图片的不透明度更高效。

### filterQuality

```dart
FilterQuality filterQuality
```

用于设置图片的 filterQuality（过滤质量）。

默认为 [FilterQuality.medium]。

### colorBlendMode

```dart
BlendMode? colorBlendMode
```

用于将 [color] 与此图片进行组合。

默认值为 [BlendMode.srcIn]。就混合模式而言，[color] 是源（source），此图片是目标（destination）。

另请参阅：

- [BlendMode](https://www.yuque.com/thyname/dart.ui/blendmode)，其中包含了各混合模式效果的示意图。

### fit

```dart
BoxFit? fit
```

在布局期间如何将图片嵌入所分配的空间中。

默认值因其他字段而异。详见 [paintImage](https://www.yuque.com/thyname/flutter.painting/paintimage) 中的讨论。

### alignment

```dart
AlignmentGeometry alignment
```

如何在其边界内对齐图片。

对齐方式会将图片中给定的位置与布局边界中给定的位置对齐。例如，[Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 值为 (-1.0, -1.0) 会将图片对齐到其布局边界的左上角，而 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 值为 (1.0, 1.0) 会将图片的右下角与其布局边界的右下角对齐。类似地，对齐值 (0.0, 1.0) 会将图片底部中间与其布局边界底边中点对齐。

要显示图片的某一部分，可以考虑使用 [CustomPainter](https://www.yuque.com/thyname/flutter.rendering/custompainter) 和 [Canvas.drawImageRect]。

如果 [alignment] 依赖于 [TextDirection](https://www.yuque.com/thyname/dart.ui/textdirection)（即它是一个 [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)），则环境中必须存在一个 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 组件。

默认为 [Alignment.center]。

另请参阅：

- [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，一个包含常用常量的类，通常用于指定 [AlignmentGeometry](https://www.yuque.com/thyname/flutter.painting/alignmentgeometry)。
- [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)，与 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 类似，但用于指定相对于文本方向的对齐方式。

### repeat

```dart
ImageRepeat repeat
```

如何绘制布局边界内未被图片覆盖的部分。

### centerSlice

```dart
Rect? centerSlice
```

九宫格图片（nine-patch image）的中心切片。

图片中位于中心切片内的区域将同时在水平和垂直方向上被拉伸，以适应其目标位置。中心切片上方和下方的图片区域仅会在水平方向上被拉伸，中心切片左右两侧的图片区域仅会在垂直方向上被拉伸。

### matchTextDirection

```dart
bool matchTextDirection
```

是否按照 [TextDirection](https://www.yuque.com/thyname/dart.ui/textdirection) 的方向绘制图片。

如果此项为 true，则在 [TextDirection.ltr] 环境下，图片将以其原点位于左上角进行绘制（图片的"正常"绘制方向）；而在 [TextDirection.rtl] 环境下，图片将在水平方向上以 -1 的缩放系数绘制，从而使原点位于右上角。

这偶尔用于从右到左的环境中显示原本为从左到右语言区域设计的图片。使用此选项时需谨慎，避免翻转带有完整阴影、文字或其他在翻转后会显得不正确的效果的图片。

如果此项为 true，环境中必须存在一个 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 组件。

### invertColors

```dart
bool invertColors
```

绘制图片时是否反转其颜色。

反转图片颜色会为画笔应用一个新的颜色滤镜。如果已指定了其他颜色滤镜，反转将在其之后应用。这主要用于实现 iOS 上的智能反转（smart invert）功能。

另请参阅：

- [Paint.invertColors]，dart:ui 中对应的实现。

### isAntiAlias

```dart
bool isAntiAlias
```

绘制图片时是否使用抗锯齿。

抗锯齿可以缓解图片旋转时出现的锯齿状伪影。

### createRenderObject()

```dart
RenderImage createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderImage renderObject)
```

### didUnmountRenderObject()

```dart
void didUnmountRenderObject(RenderImage renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# DefaultAssetBundle

```dart
class DefaultAssetBundle extends InheritedWidget {}
```

一个为其后代确定默认资源包（asset bundle）的组件。

例如，[Image](https://www.yuque.com/thyname/dart.ui/image) 会使用它来确定在未显式指定资源包时，[AssetImage](https://www.yuque.com/thyname/flutter.painting/assetimage) 应使用哪个资源包。

{@tool snippet}

这可用于在测试中覆盖当前的资源包，从而将特定资源注入被测组件中。

例如，一个测试可以像这样创建一个测试资源包：

```dart
class TestAssetBundle extends CachingAssetBundle {
  @override
  Future<ByteData> load(String key) async {
    if (key == 'resources/test') {
      return ByteData.sublistView(utf8.encode('Hello World!'));
    }
    return ByteData(0);
  }
}
```

{@end-tool} {@tool snippet}

……然后使用此资源包实现，用 [DefaultAssetBundle](https://www.yuque.com/thyname/flutter.widgets/defaultassetbundle) 包裹被测组件：

```dart
// 承接上例……
await tester.pumpWidget(
  MaterialApp(
    home: DefaultAssetBundle(
      bundle: TestAssetBundle(),
      child: const TestWidget(),
    ),
  ),
);
```

{@end-tool}

假设 `TestWidget` 使用 [DefaultAssetBundle.of] 来获取其 [AssetBundle](https://www.yuque.com/thyname/flutter.services/assetbundle)，那么它在请求 "resources/test" 资源时，现在将看到 `TestAssetBundle` 提供的 "Hello World!" 数据。

另请参阅：

- [AssetBundle](https://www.yuque.com/thyname/flutter.services/assetbundle)，资源包的接口。
- [rootBundle](https://www.yuque.com/thyname/flutter.services/rootbundle)，默认的资源包。

### DefaultAssetBundle()

```dart
DefaultAssetBundle({dynamic key, required AssetBundle bundle, required Widget child})
```

创建一个为其后代确定默认资源包的组件。

### bundle

```dart
AssetBundle bundle
```

作为默认值使用的资源包。

### of()

```dart
AssetBundle of(BuildContext context)
```

在给定上下文中，从最近的此类实例中获取资源包。

如果在给定上下文的组件树中没有 [DefaultAssetBundle](https://www.yuque.com/thyname/flutter.widgets/defaultassetbundle) 祖先组件，则将返回 [rootBundle](https://www.yuque.com/thyname/flutter.services/rootbundle)。

典型用法如下：

```dart
AssetBundle bundle = DefaultAssetBundle.of(context);
```

### updateShouldNotify()

```dart
bool updateShouldNotify(DefaultAssetBundle oldWidget)
```

# WidgetToRenderBoxAdapter

```dart
class WidgetToRenderBoxAdapter extends LeafRenderObjectWidget {}
```

用于将特定 [RenderBox](https://www.yuque.com/thyname/flutter.rendering/renderbox) 放置到组件树中的适配器。

给定的渲染对象在组件树中最多只能放置一次。此组件通过使用针对该渲染对象的 [GlobalObjectKey](https://www.yuque.com/thyname/flutter.widgets/globalobjectkey) 为自身设置键，来强制执行此限制。

当此组件被卸载（unmount）时，将对 [renderBox] 调用 [RenderObject.dispose]。此后，[renderBox] 将不可再用。如果曾向该 [renderBox] 添加过任何子项，则必须在 [onUnmount] 回调中释放它们。

### WidgetToRenderBoxAdapter()

```dart
WidgetToRenderBoxAdapter({required RenderBox renderBox, VoidCallback? onBuild, VoidCallback? onUnmount})
```

创建一个用于将特定 [RenderBox](https://www.yuque.com/thyname/flutter.rendering/renderbox) 放置到组件树中的适配器。

### renderBox

```dart
RenderBox renderBox
```

要放置到组件树中的渲染盒。

此组件拥有该渲染对象的所有权。当其被卸载时，也会调用 [RenderObject.dispose]。

### onBuild

```dart
VoidCallback? onBuild
```

在可以安全更新渲染盒及其后代时调用。如果在此回调的调用之外更新此组件下方的 RenderObject 子树，诸如命中测试（hit-testing）之类的功能将失效，因为此时该树处于脏（dirty）状态。

### onUnmount

```dart
VoidCallback? onUnmount
```

在可以安全释放手动添加到 [renderBox] 的子项时调用。

请勿释放 [renderBox] 本身，因为框架会自动将其释放。但在此过程中，框架会检查 [renderBox] 的所有子项是否也已被释放。通常，子 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 会在其对应的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 被卸载时由其释放。然而，手动添加的子渲染对象没有对应的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 来管理其生命周期，因此需要在此手动释放。

另请参阅：

- [RenderObjectElement.unmount]，会在释放其渲染对象之前调用此回调。
- [RenderObject.dispose]，指示渲染对象释放其可能持有的任何资源。

### createRenderObject()

```dart
RenderBox createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderBox renderObject)
```

### didUnmountRenderObject()

```dart
void didUnmountRenderObject(RenderObject renderObject)
```

# Listener

```dart
class Listener extends SingleChildRenderObjectWidget {}
```

一个用于响应常见指针事件而调用回调的组件。

它会监听可以构成手势的事件，例如指针按下、移动，然后释放或取消时的事件。

它不会监听鼠标独有的事件，例如鼠标在未按下任何按钮的情况下进入、退出或悬停在某个区域时的事件。对于这些事件，请使用 [MouseRegion](https://www.yuque.com/thyname/flutter.widgets/mouseregion)。

与其监听原始指针事件，不如考虑使用 [GestureDetector](https://www.yuque.com/thyname/flutter.widgets/gesturedetector) 来监听更高层级的手势。

## 布局行为

_有关盒布局模型的介绍，请参阅 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints)。_

如果该组件有子组件，则由子组件决定尺寸行为。如果没有子组件，则会扩展以适应父组件。

{@tool dartpad} 此示例使 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 在被触摸时做出反应，显示指针按下和抬起的计数。

** 请参阅 examples/api/lib/widgets/basic/listener.0.dart 中的代码 ** {@end-tool}

### Listener()

```dart
Listener({dynamic key, PointerDownEventListener? onPointerDown, PointerMoveEventListener? onPointerMove, PointerUpEventListener? onPointerUp, PointerHoverEventListener? onPointerHover, PointerCancelEventListener? onPointerCancel, PointerPanZoomStartEventListener? onPointerPanZoomStart, PointerPanZoomUpdateEventListener? onPointerPanZoomUpdate, PointerPanZoomEndEventListener? onPointerPanZoomEnd, PointerSignalEventListener? onPointerSignal, HitTestBehavior behavior = HitTestBehavior.deferToChild, Widget? child})
```

创建一个将指针事件转发给回调的组件。

[behavior] 参数默认为 [HitTestBehavior.deferToChild]。

### onPointerDown

```dart
PointerDownEventListener? onPointerDown
```

当指针在此组件所在位置与屏幕接触（对于触摸指针）、或按下按钮（对于鼠标指针）时调用。

### onPointerMove

```dart
PointerMoveEventListener? onPointerMove
```

当触发了 [onPointerDown] 的指针改变位置时调用。

### onPointerUp

```dart
PointerUpEventListener? onPointerUp
```

当触发了 [onPointerDown] 的指针不再与屏幕接触时调用。

### onPointerHover

```dart
PointerHoverEventListener? onPointerHover
```

当未触发 [onPointerDown] 的指针改变位置时调用。

这只针对在未按下时也会报告其位置的指针触发（例如鼠标指针，但大多数触摸指针不会）。

### onPointerCancel

```dart
PointerCancelEventListener? onPointerCancel
```

当触发了 [onPointerDown] 的指针的输入不再指向此接收者时调用。

### onPointerPanZoomStart

```dart
PointerPanZoomStartEventListener? onPointerPanZoomStart
```

当例如触控板手势引发的平移/缩放开始时调用。

### onPointerPanZoomUpdate

```dart
PointerPanZoomUpdateEventListener? onPointerPanZoomUpdate
```

当平移/缩放更新时调用。

### onPointerPanZoomEnd

```dart
PointerPanZoomEndEventListener? onPointerPanZoomEnd
```

当平移/缩放结束时调用。

### onPointerSignal

```dart
PointerSignalEventListener? onPointerSignal
```

当指针信号在此对象上发生时调用。

另请参阅：

- [PointerSignalEvent](https://www.yuque.com/thyname/flutter.gestures/pointersignalevent)，其中更详细地介绍了指针信号事件。

### behavior

```dart
HitTestBehavior behavior
```

命中测试期间的行为方式。

### createRenderObject()

```dart
RenderPointerListener createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderPointerListener renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# MouseRegion

```dart
class MouseRegion extends SingleChildRenderObjectWidget {}
```

一个跟踪鼠标移动的组件。

{@youtube 560 315 https://www.youtube.com/watch?v=1oF3pI5umck}

当需要比较本帧与上一帧之间鼠标指针悬停对象列表的差异时，会用到 [MouseRegion](https://www.yuque.com/thyname/flutter.widgets/mouseregion)。这意味着进入事件、退出事件以及鼠标光标。

要监听通用的指针事件，请使用 [Listener](https://www.yuque.com/thyname/flutter.widgets/listener)，或者更推荐使用 [GestureDetector](https://www.yuque.com/thyname/flutter.widgets/gesturedetector)。

## 布局行为

_有关盒布局模型的介绍，请参阅 [BoxConstraints](https://www.yuque.com/thyname/flutter.rendering/boxconstraints)。_

如果该组件有子组件，则由子组件决定尺寸行为。如果没有子组件，则会扩展以适应父组件。

{@tool dartpad} 此示例使 [Container](https://www.yuque.com/thyname/flutter.widgets/container) 在被鼠标指针进入时做出反应，显示进入和退出的计数。

** 请参阅 examples/api/lib/widgets/basic/mouse_region.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [Listener](https://www.yuque.com/thyname/flutter.widgets/listener)，一个类似的组件，在指针按下按钮时跟踪指针事件。

### MouseRegion()

```dart
MouseRegion({dynamic key, PointerEnterEventListener? onEnter, PointerExitEventListener? onExit, PointerHoverEventListener? onHover, MouseCursor cursor = MouseCursor.defer, bool opaque = true, HitTestBehavior? hitTestBehavior, Widget? child})
```

创建一个将鼠标事件转发给回调的组件。

默认情况下，所有回调均为空，[cursor] 为 [MouseCursor.defer]，[opaque] 为 true。

### onEnter

```dart
PointerEnterEventListener? onEnter
```

当鼠标指针进入此组件时触发。

当指针（无论是否按下按钮）开始被此组件的区域所包含时，会触发此回调。更具体地说，此回调在以下情况下触发：

- 此组件出现在了某个指针下方。
- 此组件移动到了某个指针下方。
- 在此组件内的某处添加了一个新指针。
- 一个已有指针移动进入了此组件。

此回调不总是会有对应的 [onExit]。如果 [MouseRegion](https://www.yuque.com/thyname/flutter.widgets/mouseregion) 在被指针悬停时被卸载，该组件的 [onExit] 将永远不会被调用。更多细节请参阅 [onExit]。

{@template flutter.widgets.MouseRegion.onEnter.triggerTime} 触发此回调的时机始终在帧与帧之间：要么在后帧回调（post-frame callbacks）期间，要么在指针事件的回调期间。{@endtemplate}

另请参阅：

- [onExit]，当鼠标指针退出该区域时触发。
- [MouseTrackerAnnotation.onEnter]，此回调的内部实现方式。

### onHover

```dart
PointerHoverEventListener? onHover
```

当指针在未按下按钮的情况下移动到此组件内的某个位置时触发。

通常这只针对会在未按下时报告其位置的指针触发（例如鼠标指针）。某些设备在无障碍模式下的单击操作中也会触发此事件。

此组件本身的移动不会触发此回调。

触发此回调的时机是在指针事件的回调期间，该时机始终位于帧与帧之间。

另请参阅：

- [Listener.onPointerHover]，执行相同的工作。由于悬停事件与其他常规事件类似，建议优先使用 [Listener.onPointerHover]。

### onExit

```dart
PointerExitEventListener? onExit
```

当鼠标指针在该组件仍处于挂载状态时退出此组件时触发。

当指针（无论是否按下按钮）不再被此组件的区域所包含时，会触发此回调，但因该组件消失而导致的退出除外。更具体地说，此回调在以下情况下触发：

- 一个正悬停在此组件上的指针已移开。
- 一个正悬停在此组件上的指针已被移除。
- 此正被指针悬停的组件已移开。

并且**不会**在以下情况下触发：

- 此正被指针悬停的组件已消失。

这意味着 [MouseRegion.onExit] 可能不会有对应的 [MouseRegion.onEnter]。

此限制旨在防止一种常见的误用：如果在 [MouseRegion.onExit] 中调用 [State.setState] 时没有检查组件是否仍处于挂载状态，则会发生异常。这是因为该回调是在后帧阶段触发的，此时组件已被卸载。由于 [State.setState] 是组件专有的，因此该限制专门针对 [MouseRegion](https://www.yuque.com/thyname/flutter.widgets/mouseregion)，并不适用于其更底层的对应项 [RenderMouseRegion](https://www.yuque.com/thyname/flutter.rendering/rendermouseregion) 和 [MouseTrackerAnnotation](https://www.yuque.com/thyname/flutter.services/mousetrackerannotation)。

有几种方法可以缓解此限制：

- 如果悬停状态完全包含在一个无条件创建此 [MouseRegion](https://www.yuque.com/thyname/flutter.widgets/mouseregion) 的组件内，则这不是问题，因为在 [MouseRegion](https://www.yuque.com/thyname/flutter.widgets/mouseregion) 被卸载后，该状态也不再被使用。
- 否则，外层组件很可能可以访问控制此 [MouseRegion](https://www.yuque.com/thyname/flutter.widgets/mouseregion) 是否存在的变量。如果可以，请在条件由 true 变为 false 的事件中调用 [onExit]。
- 在上述方案都不适用的情况下，你始终可以重写 [State.dispose] 并调用 [onExit]，或使用 [RenderMouseRegion](https://www.yuque.com/thyname/flutter.rendering/rendermouseregion) 创建自己的组件。

{@tool dartpad} 以下示例展示了一个蓝色矩形，在被悬停时会变为黄色。由于悬停状态完全包含在一个无条件创建 `MouseRegion` 的组件内，因此你可以忽略上述限制。

** 请参阅 examples/api/lib/widgets/basic/mouse_region.on_exit.0.dart 中的代码 ** {@end-tool}

{@tool dartpad} 以下示例展示了一个组件，它在被悬停一秒后隐藏其内容，同时暴露进入和退出回调。由于该组件有条件地创建 `MouseRegion`，并泄露了悬停状态，因此需要考虑上述限制。在这种情况下，由于它可以访问触发 `MouseRegion` 消失的事件，因此也会在该事件中触发退出回调。

** 请参阅 examples/api/lib/widgets/basic/mouse_region.on_exit.1.dart 中的代码 ** {@end-tool}

{@macro flutter.widgets.MouseRegion.onEnter.triggerTime}

另请参阅：

- [onEnter]，当鼠标指针进入该区域时触发。
- [RenderMouseRegion](https://www.yuque.com/thyname/flutter.rendering/rendermouseregion) 和 [MouseTrackerAnnotation.onExit]，此回调的内部实现方式，但不受此限制约束。

### cursor

```dart
MouseCursor cursor
```

悬停在该区域上方的鼠标指针所使用的鼠标光标。

当鼠标进入该区域时，其光标将变为 [cursor]。当鼠标离开该区域时，光标将由命中测试顺序中位于其后方区域决定。

[cursor] 默认为 [MouseCursor.defer]，将光标的选择权推迟给命中测试顺序中位于其后的下一个区域。

### opaque

```dart
bool opaque
```

此组件是否应阻止在视觉上位于其后方的其他 [MouseRegion](https://www.yuque.com/thyname/flutter.widgets/mouseregion) 检测到指针。

这会改变指针所悬停区域的列表，从而影响它们的 [onHover]、[onEnter]、[onExit] 和 [cursor] 的行为。

如果 [opaque] 为 true，此组件将吸收鼠标指针，并阻止此组件的兄弟组件（或任何非此组件祖先或后代的其他组件）检测到鼠标指针，即使指针位于它们的区域内。

如果 [opaque] 为 false，此对象不会影响其后方的 [MouseRegion](https://www.yuque.com/thyname/flutter.widgets/mouseregion) 的行为，只要指针位于它们的区域内，它们仍将检测到该指针。

默认为 true。

### hitTestBehavior

```dart
HitTestBehavior? hitTestBehavior
```

命中测试期间的行为方式。

如果为 null，默认为 [HitTestBehavior.opaque]。

### createRenderObject()

```dart
RenderMouseRegion createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderMouseRegion renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RepaintBoundary

```dart
class RepaintBoundary extends SingleChildRenderObjectWidget {}
```

一个为其子组件创建单独显示列表（display list）的组件。

{@youtube 560 315 https://www.youtube.com/watch?v=cVAGLDuc2xE}

此组件为其子组件创建一个单独的显示列表，如果子树的重绘时机与树的其余部分不同，这可以提升性能。

这很有用，因为即使 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 关联的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 实例没有发生变化或重建，[RenderObject.paint] 仍可能被触发。只要与某个 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 共享同一 [Layer](https://www.yuque.com/thyname/flutter.rendering/layer) 的任意 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 被标记为脏并需要绘制（参见 [RenderObject.markNeedsPaint]），例如祖先滚动或祖先/后代产生动画时，[RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 就会重绘。

因此，通过显式或隐式使用 [RepaintBoundary](https://www.yuque.com/thyname/flutter.widgets/repaintboundary)，将 [RenderObject.paint] 限制在渲染子树中实际发生视觉变化的部分，对于最大限度减少冗余工作、提升应用性能至关重要。

当某个 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 通过 [RenderObject.markNeedsPaint] 被标记为需要绘制时，最近的、其 [RenderObject.isRepaintBoundary] 为 true 的祖先 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)（直至应用的根节点）将被要求重绘。该最近祖先的 [RenderObject.paint] 方法会导致其所有后代 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 在同一图层内重绘。

因此，[RepaintBoundary](https://www.yuque.com/thyname/flutter.widgets/repaintboundary) 在沿渲染树向上传播 `markNeedsPaint` 标记的过程中，以及在通过 [PaintingContext.paintChild] 沿渲染树向下遍历的过程中，都被用于策略性地将重绘限制在发生视觉变化的渲染子树内，以提升性能。之所以能做到这一点，是因为 [RepaintBoundary](https://www.yuque.com/thyname/flutter.widgets/repaintboundary) 组件创建的渲染对象始终拥有一个 [Layer](https://www.yuque.com/thyname/flutter.rendering/layer)，从而将祖先渲染对象与后代渲染对象解耦。

如果 [RepaintBoundary](https://www.yuque.com/thyname/flutter.widgets/repaintboundary) 之后的渲染子树足够复杂，且在周围树频繁变化的同时保持静态，那么 [RepaintBoundary](https://www.yuque.com/thyname/flutter.widgets/repaintboundary) 还会带来一个附加效果，即可能向引擎提示应进一步优化动画性能。在这些情况下，引擎可能会选择为此付出一次性代价，对该子树的像素值进行栅格化并缓存，以加快未来 GPU 重新渲染的速度。

若干框架组件插入了 [RepaintBoundary](https://www.yuque.com/thyname/flutter.widgets/repaintboundary) 组件，以标记应用中自然的分隔点。例如，Material Design 抽屉中的内容通常在抽屉打开和关闭时不会发生变化，因此在使用 [Drawer](https://www.yuque.com/thyname/flutter.material/drawer) 组件进行过渡动画时，重绘会自动被限制在抽屉内部或外部的区域中。

另请参阅：

- [debugRepaintRainbowEnabled](https://www.yuque.com/thyname/flutter.rendering/debugrepaintrainbowenabled)，一个用于可视化监控运行中应用的渲染树重绘情况的调试标志。
- [debugProfilePaintsEnabled](https://www.yuque.com/thyname/flutter.rendering/debugprofilepaintsenabled)，一个用于在 Flutter DevTools 的时间线视图中显示渲染树重绘情况的调试标志。

### RepaintBoundary()

```dart
RepaintBoundary({dynamic key, Widget? child})
```

创建一个隔离重绘的组件。

### RepaintBoundary.wrap()

```dart
RepaintBoundary.wrap(Widget child, int childIndex)
```

将给定的子组件包裹在一个 [RepaintBoundary](https://www.yuque.com/thyname/flutter.widgets/repaintboundary) 中。

[RepaintBoundary](https://www.yuque.com/thyname/flutter.widgets/repaintboundary) 的键（key）派生自子组件的键（如果子组件的键非空），否则派生自给定的 `childIndex`。

### wrapAll()

```dart
List<RepaintBoundary> wrapAll(List<Widget> widgets)
```

将给定的每个子组件分别包裹在各自的 [RepaintBoundary](https://www.yuque.com/thyname/flutter.widgets/repaintboundary) 中。

每个 [RepaintBoundary](https://www.yuque.com/thyname/flutter.widgets/repaintboundary) 的键派生自被包裹子组件的现有键（如果非空），否则派生自该子组件在列表中的索引。

### createRenderObject()

```dart
RenderRepaintBoundary createRenderObject(BuildContext context)
```

# IgnorePointer

```dart
class IgnorePointer extends SingleChildRenderObjectWidget {}
```

一个在命中测试期间不可见的组件。

当 [ignoring] 为 true 时，此组件（及其子树）在命中测试中不可见。它在布局期间仍会占用空间，并照常绘制其子组件。只是它不能成为定位事件（located events）的目标，因为它会从 [RenderBox.hitTest] 返回 false。

{@youtube 560 315 https://www.youtube.com/watch?v=qV9pqHWxYgI}

{@tool dartpad} 以下示例中有一个 [IgnorePointer](https://www.yuque.com/thyname/flutter.widgets/ignorepointer) 组件，它包裹着包含一个按钮的 `Column`。当 [ignoring] 设置为 `true` 时，`Column` 内的任何内容都无法被点击。当 [ignoring] 设置为 `false` 时，`Column` 内的任何内容都可以被点击。

** 请参阅 examples/api/lib/widgets/basic/ignore_pointer.0.dart 中的代码 ** {@end-tool}

## 语义（Semantics）

使用此类还可能影响下方语义子树的收集方式。

{@template flutter.widgets.IgnorePointer.semantics} 如果 [ignoring] 为 true，与指针相关的 [SemanticsAction](https://www.yuque.com/thyname/dart.ui/semanticsaction) 将从语义子树中移除。否则，子树保持不变。{@endtemplate}

{@template flutter.widgets.IgnorePointer.ignoringSemantics} [ignoringSemantics] 的用法已弃用，不建议使用。引入此属性是为了绕过 v3.8.0-12.0.pre 之前 [IgnorePointer](https://www.yuque.com/thyname/flutter.widgets/ignorepointer) 及其相关组件的语义行为。

在该版本之前，如果 [ignoring] 为 true，整个语义子树都会被丢弃。开发者只能使用 [ignoringSemantics] 来保留语义子树。

该版本之后，将 [ignoring] 设置为 true 时，只会阻止语义子树中的用户操作（user action），而其他 [SemanticsProperties](https://www.yuque.com/thyname/flutter.semantics/semanticsproperties) 保持不变。因此，不再需要 [ignoringSemantics]。

如果 [ignoringSemantics] 为 true，语义子树将被丢弃。因此，该子树对辅助技术不可见。

如果 [ignoringSemantics] 为 false，语义子树将照常被收集。{@endtemplate}

另请参阅：

- [AbsorbPointer](https://www.yuque.com/thyname/flutter.widgets/absorbpointer)，同样会阻止其子组件接收指针事件，但其自身在命中测试中可见。
- [SliverIgnorePointer](https://www.yuque.com/thyname/flutter.widgets/sliverignorepointer)，此组件的 sliver 版本。

### IgnorePointer()

```dart
IgnorePointer({dynamic key, bool ignoring = true, bool? ignoringSemantics, Widget? child})
```

创建一个在命中测试中不可见的组件。

### ignoring

```dart
bool ignoring
```

此组件在命中测试期间是否被忽略。

无论此组件在命中测试期间是否被忽略，它在布局期间仍会占用空间，并在绘制期间可见。

{@macro flutter.widgets.IgnorePointer.semantics}

默认为 true。

### ignoringSemantics

```dart
bool? ignoringSemantics
```

在编译语义子树时，是否忽略此组件的语义。

{@macro flutter.widgets.IgnorePointer.ignoringSemantics}

关于语义树的更多信息，请参阅 [SemanticsNode](https://www.yuque.com/thyname/flutter.semantics/semanticsnode)。

### createRenderObject()

```dart
RenderIgnorePointer createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderIgnorePointer renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AbsorbPointer

```dart
class AbsorbPointer extends SingleChildRenderObjectWidget {}
```

一个在命中测试期间吸收指针的组件。

当 [absorbing] 为 true 时，此组件通过在自身处终止命中测试，阻止其子树接收指针事件。它在布局期间仍会占用空间，并照常绘制其子组件。只是它会阻止其子组件成为定位事件的目标，因为它会从 [RenderBox.hitTest] 返回 true。

当 [ignoringSemantics] 为 true 时，该子树对语义层（以及例如无障碍工具）不可见。

{@youtube 560 315 https://www.youtube.com/watch?v=65HoWqBboI8}

{@tool dartpad} 以下示例中，一个 [AbsorbPointer](https://www.yuque.com/thyname/flutter.widgets/absorbpointer) 组件包裹着堆叠（stack）顶部的按钮，该组件会吸收指针事件，从而阻止其子按钮**以及**堆叠中位于其下方的按钮接收指针事件。

** 请参阅 examples/api/lib/widgets/basic/absorb_pointer.0.dart 中的代码 ** {@end-tool}

## 语义（Semantics）

使用此类还可能影响下方语义子树的收集方式。

{@template flutter.widgets.AbsorbPointer.semantics} 如果 [absorbing] 为 true，与指针相关的 [SemanticsAction](https://www.yuque.com/thyname/dart.ui/semanticsaction) 将从语义子树中移除。否则，子树保持不变。{@endtemplate}

{@template flutter.widgets.AbsorbPointer.ignoringSemantics} [ignoringSemantics] 的用法已弃用，不建议使用。引入此属性是为了绕过 v3.8.0-12.0.pre 之前 [IgnorePointer](https://www.yuque.com/thyname/flutter.widgets/ignorepointer) 及其相关组件的语义行为。

在该版本之前，如果 [absorbing] 为 true，整个语义子树都会被丢弃。开发者只能使用 [ignoringSemantics] 来保留语义子树。

该版本之后，将 [absorbing] 设置为 true 时，只会阻止语义子树中的用户操作，而其他 [SemanticsProperties](https://www.yuque.com/thyname/flutter.semantics/semanticsproperties) 保持不变。因此，不再需要 [ignoringSemantics]。

如果 [ignoringSemantics] 为 true，语义子树将被丢弃。因此，该子树对辅助技术不可见。

如果 [ignoringSemantics] 为 false，语义子树将照常被收集。{@endtemplate}

另请参阅：

- [IgnorePointer](https://www.yuque.com/thyname/flutter.widgets/ignorepointer)，同样会阻止其子组件接收指针事件，但其自身在命中测试中不可见。

### AbsorbPointer()

```dart
AbsorbPointer({dynamic key, bool absorbing = true, bool? ignoringSemantics, Widget? child})
```

创建一个在命中测试期间吸收指针的组件。

### absorbing

```dart
bool absorbing
```

此组件在命中测试期间是否吸收指针。

无论此渲染对象在命中测试期间是否吸收指针，它在布局期间仍会占用空间，并在绘制期间可见。

{@macro flutter.widgets.AbsorbPointer.semantics}

默认为 true。

### ignoringSemantics

```dart
bool? ignoringSemantics
```

在编译语义树时，是否忽略此渲染对象的语义。

{@macro flutter.widgets.AbsorbPointer.ignoringSemantics}

关于语义树的更多信息，请参阅 [SemanticsNode](https://www.yuque.com/thyname/flutter.semantics/semanticsnode)。

### createRenderObject()

```dart
RenderAbsorbPointer createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderAbsorbPointer renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# MetaData

```dart
class MetaData extends SingleChildRenderObjectWidget {}
```

在渲染树中保存不透明的元数据。

适用于用信息装饰渲染树，这些信息将在稍后被使用。例如，你可以在渲染树中存储一些信息，这些信息将在用户与渲染树交互时使用，但在交互发生之前没有任何视觉影响。

### MetaData()

```dart
MetaData({dynamic key, dynamic metaData, HitTestBehavior behavior = HitTestBehavior.deferToChild, Widget? child})
```

创建一个保存不透明元数据的组件。

[behavior] 参数默认为 [HitTestBehavior.deferToChild]。

### metaData

```dart
dynamic metaData
```

渲染树所忽略的不透明元数据。

### behavior

```dart
HitTestBehavior behavior
```

命中测试期间的行为方式。

### createRenderObject()

```dart
RenderMetaData createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderMetaData renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# Semantics

```dart
class Semantics extends _SemanticsBase {}
```

一个用组件含义的描述来标注组件树的组件。

{@youtube 560 315 https://www.youtube.com/watch?v=NvtMt_DtFrQ}

{@macro flutter.widgets.SemanticsBase}

- [SliverSemantics](https://www.yuque.com/thyname/flutter.widgets/sliversemantics)，此组件的 sliver 变体。

### Semantics()

```dart
Semantics({dynamic key, Widget? child, bool container = false, bool explicitChildNodes = false, bool excludeSemantics = false, bool blockUserActions = false, bool? enabled, bool? checked, bool? mixed, bool? selected, bool? toggled, bool? button, bool? slider, bool? keyboardKey, bool? link, Uri? linkUrl, bool? header, int? headingLevel, bool? textField, bool? readOnly, bool? focusable, bool? focused, dynamic accessibilityFocusBlockType, bool? inMutuallyExclusiveGroup, bool? obscured, bool? multiline, bool? scopesRoute, bool? namesRoute, bool? hidden, bool? image, bool? liveRegion, bool? expanded, bool? isRequired, int? maxValueLength, int? currentValueLength, String? identifier, Object? traversalParentIdentifier, Object? traversalChildIdentifier, String? label, dynamic attributedLabel, String? value, dynamic attributedValue, String? increasedValue, dynamic attributedIncreasedValue, String? decreasedValue, dynamic attributedDecreasedValue, String? hint, dynamic attributedHint, String? tooltip, String? onTapHint, String? onLongPressHint, dynamic textDirection, dynamic sortKey, dynamic tagForChildren, dynamic onTap, dynamic onLongPress, dynamic onScrollLeft, dynamic onScrollRight, dynamic onScrollUp, dynamic onScrollDown, dynamic onIncrease, dynamic onDecrease, dynamic onCopy, dynamic onCut, dynamic onPaste, dynamic onDismiss, dynamic onMoveCursorForwardByCharacter, dynamic onMoveCursorBackwardByCharacter, dynamic onSetSelection, dynamic onSetText, dynamic onDidGainAccessibilityFocus, dynamic onDidLoseAccessibilityFocus, dynamic onFocus, dynamic onExpand, dynamic onCollapse, Map<InvalidType, InvalidType>? customSemanticsActions, dynamic role, Set<String>? controlsNodes, dynamic validationResult = SemanticsValidationResult.none, dynamic hitTestBehavior, dynamic inputType, dynamic localeForSubtree, String? minValue, String? maxValue})
```

创建一个语义标注。

要创建一个 `const` 的 [Semantics](https://www.yuque.com/thyname/flutter.widgets/semantics) 实例，请使用 [Semantics.fromProperties] 构造函数。

{@macro flutter.widgets.SemanticsBase}

### Semantics.fromProperties()

```dart
Semantics.fromProperties({dynamic key, Widget? child, bool container = false, bool explicitChildNodes = false, bool excludeSemantics = false, bool blockUserActions = false, dynamic localeForSubtree, required dynamic properties})
```

{@macro flutter.widgets.SemanticsBase.fromProperties}

### createRenderObject()

```dart
RenderSemanticsAnnotations createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderSemanticsAnnotations renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# MergeSemantics

```dart
class MergeSemantics extends SingleChildRenderObjectWidget {}
```

一个合并其后代语义的组件。

使以此节点为根的子树中的所有语义合并为语义树中的一个节点。例如，如果你有一个组件，其中一个 Text 节点紧挨着一个复选框组件，就可以使用此组件将 Text 节点的标签与复选框的"选中"语义状态合并为一个同时具有标签和选中状态的单一节点。否则，标签将作为与复选框分离的独立特性呈现，用户将无法确定它们是相关的。

{@tool snippet}

此代码片段展示了如何使用 [MergeSemantics](https://www.yuque.com/thyname/flutter.widgets/mergesemantics) 合并 [Checkbox](https://www.yuque.com/thyname/flutter.material/checkbox) 与 [Text](https://www.yuque.com/thyname/flutter.widgets/text) 组件的语义。

```dart
MergeSemantics(
  child: Row(
    children: <Widget>[
      Checkbox(
        value: true,
        onChanged: (bool? value) {},
      ),
      const Text('Settings'),
    ],
  ),
)
```

{@end-tool}

请注意，如果子树中的两个节点存在冲突的语义，结果可能是不合逻辑的。例如，一个包含一个已选中复选框和一个未选中复选框的子树将呈现为已选中状态。所有标签都会被合并为单个字符串（各标签之间以换行符分隔）。如果合并后的子树中有多个节点能够处理语义手势，则按树的顺序排在第一位的节点将成为接收回调的节点。

### MergeSemantics()

```dart
MergeSemantics({dynamic key, Widget? child})
```

创建一个合并其后代语义的组件。

### createRenderObject()

```dart
RenderMergeSemantics createRenderObject(BuildContext context)
```

# BlockSemantics

```dart
class BlockSemantics extends SingleChildRenderObjectWidget {}
```

一个丢弃在同一语义容器中先于其绘制的所有组件语义的组件。

这有助于向无障碍工具隐藏那些绘制在某个组件"背后"的组件，例如，一个警告框通常应禁止与位于其"背后"的任何组件交互（即使它们仍部分可见）。类似地，一个打开的 [Drawer](https://www.yuque.com/thyname/flutter.material/drawer) 会阻止与抽屉外部任何组件的交互。

另请参阅：

- [ExcludeSemantics](https://www.yuque.com/thyname/flutter.widgets/excludesemantics)，会丢弃其所有后代的语义。

### BlockSemantics()

```dart
BlockSemantics({dynamic key, bool blocking = true, Widget? child})
```

创建一个排除在同一语义容器中先于其绘制的所有组件语义的组件。

### blocking

```dart
bool blocking
```

此组件是否阻止在同一语义容器中先于其绘制的所有组件的语义。

### createRenderObject()

```dart
RenderBlockSemantics createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderBlockSemantics renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ExcludeSemantics

```dart
class ExcludeSemantics extends SingleChildRenderObjectWidget {}
```

一个丢弃其所有后代语义的组件。

当 [excluding] 为 true 时，此组件（及其子树）将从语义树中排除。

这可用于隐藏那些原本会被报告、但只会造成混淆的后代组件。例如，material 库中的 [Chip](https://www.yuque.com/thyname/flutter.material/chip) 组件会隐藏头像（avatar），因为它与 chip 的标签重复。

另请参阅：

- [BlockSemantics](https://www.yuque.com/thyname/flutter.widgets/blocksemantics)，会丢弃树中位置更靠前的组件的语义。

### ExcludeSemantics()

```dart
ExcludeSemantics({dynamic key, bool excluding = true, Widget? child})
```

创建一个丢弃其所有后代语义的组件。

### excluding

```dart
bool excluding
```

此组件在语义树中是否被排除。

### createRenderObject()

```dart
RenderExcludeSemantics createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderExcludeSemantics renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# IndexedSemantics

```dart
class IndexedSemantics extends SingleChildRenderObjectWidget {}
```

一个用索引标注子组件语义的组件。

语义索引由 TalkBack/Voiceover 用于就当前滚动状态发出通知。某些组件，如 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview)，会在构建语义时自动提供子项索引。如果并非可滚动组件的所有子项都对语义有贡献，用户可能希望手动提供语义索引。

{@tool snippet}

以下示例处理了可滚动组件中不产生语义贡献的间隔符（spacer）。自动索引会为这些间隔符赋予语义索引，导致滚动通知错误地声明当前可见四个项目。

```dart
ListView(
  addSemanticIndexes: false,
  semanticChildCount: 2,
  children: const <Widget>[
    IndexedSemantics(index: 0, child: Text('First')),
    Spacer(),
    IndexedSemantics(index: 1, child: Text('Second')),
    Spacer(),
  ],
)
```

{@end-tool}

另请参阅：

- [CustomScrollView](https://www.yuque.com/thyname/flutter.widgets/customscrollview)，其中解释了索引语义。

### IndexedSemantics()

```dart
IndexedSemantics({dynamic key, required int index, Widget? child})
```

创建一个为第一个子语义节点标注索引的组件。

### index

```dart
int index
```

用于标注第一个子语义节点的索引。

### createRenderObject()

```dart
RenderIndexedSemantics createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderIndexedSemantics renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# KeyedSubtree

```dart
class KeyedSubtree extends StatelessWidget {}
```

一个构建其子组件的组件。

适用于为现有组件附加一个键（key）。

### KeyedSubtree()

```dart
KeyedSubtree({dynamic key, required Widget child})
```

创建一个在构建其子组件的同时为其分配键的组件。

当你希望在某个组件在组件树中移动位置时，通过将其与一个一致的键相关联来保留该组件的状态时，此方法很有用。

### KeyedSubtree.wrap()

```dart
KeyedSubtree.wrap(Widget child, int childIndex)
```

为 child 创建一个 KeyedSubtree，其键基于该子组件已有的键或 childIndex。

### child

```dart
Widget child
```

此组件下方的组件。

{@macro flutter.widgets.ProxyWidget.child}

### ensureUniqueKeysForList()

```dart
List<Widget> ensureUniqueKeysForList(List<Widget> items, {int baseIndex = 0})
```

将每个项目包裹在一个 KeyedSubtree 中，其键基于该项目已有的键，或基于其列表索引与 `baseIndex` 之和。

### build()

```dart
Widget build(BuildContext context)
```

# Builder

```dart
class Builder extends StatelessWidget {}
```

一个无状态的工具组件，其 [build] 方法使用其 [builder] 回调来创建该组件的子组件。

{@youtube 560 315 https://www.youtube.com/watch?v=xXNOkIuSYuA}

此组件是定义 [StatelessWidget](https://www.yuque.com/thyname/flutter.widgets/statelesswidget) 子类的一种内联替代方式。例如，与其像下面这样定义一个组件：

```dart
class Foo extends StatelessWidget {
  const Foo({super.key});
  @override
  Widget build(BuildContext context) => const Text('foo');
}
```

……并像通常那样使用它：

```dart
// 承接上例……
const Center(child: Foo())
```

……不如在一步之内定义并使用它，而无需定义新的组件类：

```dart
Center(
  child: Builder(
    builder: (BuildContext context) => const Text('foo'),
  ),
)
```

上述两个示例与直接创建子组件而不插入中间组件之间的区别在于，额外的组件会带来一个额外的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 元素。当树中包含一个被诸如 [Scaffold.of] 之类的方法所引用的继承组件（inherited widget）时，这一点尤为明显，此类方法会访问子组件 BuildContext 的祖先。

在以下示例中，按钮的 `onPressed` 回调无法通过 [Scaffold.of] 找到外层的 [ScaffoldState](https://www.yuque.com/thyname/flutter.material/scaffoldstate)：

```dart
Widget build(BuildContext context) {
  return Scaffold(
    body: Center(
      child: TextButton(
        onPressed: () {
          // 失败，因为 Scaffold.of() 在此组件上下文
          // 之上找不到任何内容。
          print(Scaffold.of(context).hasAppBar);
        },
        child: const Text('hasAppBar'),
      )
    ),
  );
}
```

一个 [Builder](https://www.yuque.com/thyname/flutter.widgets/builder) 组件引入了一个额外的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 元素，因此 [Scaffold.of] 方法可以成功执行。

```dart
Widget build(BuildContext context) {
  return Scaffold(
    body: Builder(
      builder: (BuildContext context) {
        return Center(
          child: TextButton(
            onPressed: () {
              print(Scaffold.of(context).hasAppBar);
            },
            child: const Text('hasAppBar'),
          ),
        );
      },
    ),
  );
}
```

另请参阅：

- [StatefulBuilder](https://www.yuque.com/thyname/flutter.widgets/statefulbuilder)，一个有状态的工具组件，其 [build] 方法使用其 [builder] 回调来创建该组件的子组件。

### Builder()

```dart
Builder({dynamic key, required WidgetBuilder builder})
```

创建一个将其构建过程委托给回调的组件。

### builder

```dart
WidgetBuilder builder
```

用于获取子组件的调用。

每当此组件被包含在其父组件的构建过程中，且其所同步的旧组件（如果有）具有不同的对象标识时，就会调用此函数。通常，父组件的 build 方法会构造一棵新的组件树，因此新的 Builder 子组件不会与对应的旧组件[相同（identical）]。

### build()

```dart
Widget build(BuildContext context)
```

# StatefulWidgetBuilder

```dart
typedef StatefulWidgetBuilder = Widget Function(BuildContext context, StateSetter setState)
```

[StatefulBuilder](https://www.yuque.com/thyname/flutter.widgets/statefulbuilder) 所使用的 builder 回调的函数签名。

调用 `setState` 以安排 [StatefulBuilder](https://www.yuque.com/thyname/flutter.widgets/statefulbuilder) 进行重建。

# StatefulBuilder

```dart
class StatefulBuilder extends StatefulWidget {}
```

一个既拥有状态、又调用闭包以获取其子组件的柏拉图式（platonic）组件。

{@youtube 560 315 https://www.youtube.com/watch?v=syvT63CosNE}

传递给 [builder] 的 [StateSetter](https://www.yuque.com/thyname/flutter.widgets/statesetter) 函数用于触发重建，以替代典型 [State](https://www.yuque.com/thyname/flutter.widgets/state) 的 [State.setState]。

由于每当调用 [StateSetter](https://www.yuque.com/thyname/flutter.widgets/statesetter) 时都会重新调用 [builder]，因此任何表示状态的变量都应保存在 [builder] 函数之外。

{@tool snippet}

此示例展示了使用内联的 StatefulBuilder，它既能重建，又拥有自己的状态。

```dart
await showDialog<void>(
  context: context,
  builder: (BuildContext context) {
    int? selectedRadio = 0;
    return AlertDialog(
      content: StatefulBuilder(
        builder: (BuildContext context, StateSetter setState) {
          return RadioGroup<int>(
            groupValue: selectedRadio,
            onChanged: (int? value) {
              setState(() => selectedRadio = value);
            },
            child: Column(
              mainAxisSize: MainAxisSize.min,
              children: List<Widget>.generate(4, (int index) {
                return Radio<int>(value: index);
              }),
            ),
          );
        },
      ),
    );
  },
);
```

{@end-tool}

另请参阅：

- [Builder](https://www.yuque.com/thyname/flutter.widgets/builder)，柏拉图式的无状态组件。

### StatefulBuilder()

```dart
StatefulBuilder({dynamic key, required StatefulWidgetBuilder builder})
```

创建一个既拥有状态、又将其构建过程委托给回调的组件。

### builder

```dart
StatefulWidgetBuilder builder
```

用于获取子组件的调用。

每当此组件被包含在其父组件的构建过程中，且其所同步的旧组件（如果有）具有不同的对象标识时，就会调用此函数。通常，父组件的 build 方法会构造一棵新的组件树，因此新的 Builder 子组件不会与对应的旧组件相同。

### createState()

```dart
State<StatefulBuilder> createState()
```

# ColoredBox

```dart
class ColoredBox extends SingleChildRenderObjectWidget {}
```

一个用指定的 [Color](https://www.yuque.com/thyname/dart.ui/color) 绘制其区域、然后在该颜色之上绘制其子组件的组件。

### ColoredBox()

```dart
ColoredBox({required Color color, bool isAntiAlias = true, Widget? child, dynamic key})
```

创建一个使用指定 [Color](https://www.yuque.com/thyname/dart.ui/color) 绘制其区域的组件。

### color

```dart
Color color
```

用于绘制背景区域的颜色。

### isAntiAlias

```dart
bool isAntiAlias
```

{@template flutter.widgets.ColoredBox.isAntiAlias} 绘制盒子时是否应用抗锯齿。

默认为 `true`。

当为 `true` 时，绘制出的盒子边缘会更平滑。这对于动画和变换（如旋转或缩放）至关重要，因为在这些情况下组件的边缘可能无法与物理像素网格完美对齐。抗锯齿支持子像素渲染，这可以防止运动过程中出现"锯齿状"外观，并确保视觉上平滑的过渡。

对于多个 `ColoredBox` 组件彼此相邻放置、以构成一片更大的无缝纯色区域的特定场景，请将此项设置为 `false`。启用抗锯齿（`true`）时，由于边缘存在半透明像素，各个盒子之间可能会出现细微的接缝或缝隙。禁用抗锯齿可确保各个盒子完美对齐，而不会出现此类视觉伪影。

另请参阅：

- [Paint.isAntiAlias]，此项所控制的底层属性。{@endtemplate}
