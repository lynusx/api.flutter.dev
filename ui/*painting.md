# Color

```dart
class Color {}
```

不可变的 ARGB 格式颜色值。

以 [Flutter logo](https://flutter.dev/brand) 的浅青色为例。该颜色完全不透明，红色 [r] 通道值为 `0.2588`（即 8 位值 `0x42` 或 `66`），绿色 [g] 通道值为 `0.6471`（即 8 位值 `0xA5` 或 `165`），蓝色 [b] 通道值为 `0.9608`（即 8 位值 `0xF5` 或 `245`）。按照常见的 [CSS 十六进制颜色语法](https://developer.mozilla.org/en-US/docs/Web/CSS/hex-color) 表示 RGB 颜色值，该颜色可以描述为 `#42A5F5`。

以下是构造该颜色的几种方式：

```dart
const Color c1 = Color.from(alpha: 1.0, red: 0.2588, green: 0.6471, blue: 0.9608);
const Color c2 = Color(0xFF42A5F5);
const Color c3 = Color.fromARGB(0xFF, 0x42, 0xA5, 0xF5);
const Color c4 = Color.fromARGB(255, 66, 165, 245);
const Color c5 = Color.fromRGBO(66, 165, 245, 1.0);
```

如果你在使用 [Color.new] 时遇到问题，发现颜色似乎没有被绘制出来，请检查是否指定了完整的 8 位十六进制数字。如果只指定了 6 位，那么前两位会被视为零，这意味着颜色是完全透明的：

```dart
const Color c1 = Color(0xFFFFFF); // 完全透明的白色（不可见）
const Color c2 = Color(0xFFFFFFFF); // 完全不透明的白色（可见）

// 或使用基于 double 的通道值：
const Color c3 = Color.from(alpha: 1.0, red: 1.0, green: 1.0, blue: 1.0);
```

[Color](https://www.yuque.com/thyname/dart.ui/color) 的颜色分量以浮点值形式存储。如果不希望使用 `operator==` 提供的字面值相等性比较，则需要注意这一点。要在 Flutter 测试中检验相等性，可以考虑使用 [`isSameColorAs`][]。

另请参阅：

- [Colors](https://www.yuque.com/thyname/flutter.material/colors)：定义了 Material Design 规范中的颜色。
- [`isSameColorAs`][]：一个 Matcher，用于在检查 [Color](https://www.yuque.com/thyname/dart.ui/color) 相等性时处理浮点数误差。

[`isSameColorAs`]: https://api.flutter.dev/flutter/flutter_test/isSameColorAs.html

### Color()

```dart
Color(int value)
```

从 [int](https://www.yuque.com/thyname/dart.core/int) 的低 32 位构造一个 [ColorSpace.sRGB] 颜色。

各位的含义如下：

- 第 24-31 位为 alpha 值。
- 第 16-23 位为红色值。
- 第 8-15 位为绿色值。
- 第 0-7 位为蓝色值。

换句话说，如果 AA 是十六进制的 alpha 值，RR 是十六进制的红色值，GG 是十六进制的绿色值，BB 是十六进制的蓝色值，则颜色可以表示为 `Color(0xAARRGGBB)`。

例如，要获得完全不透明的橙色，可以使用 `const Color(0xFFFF9000)`（`FF` 表示 alpha，`FF` 表示红色，`90` 表示绿色，`00` 表示蓝色）。

{@template dart.ui.Color.componentsStoredAsFloatingPoint}

> [!NOTE]
> 每个颜色都以浮点颜色分量存储，其中每个分量的最终值通过存储 `c / 255` 来近似表示，其中 `c` 是四个分量（alpha、红、绿、蓝）之一。 {@endtemplate}

### Color.from()

```dart
Color.from({required double alpha, required double red, required double green, required double blue, ColorSpace colorSpace = ColorSpace.sRGB})
```

使用浮点颜色分量构造颜色。

颜色分量允许支持任意位深度的颜色分量。这些值根据 [ColorSpace](https://www.yuque.com/thyname/dart.ui/colorspace) 参数进行解释。

## Example

```dart
// 完全不透明的最大红色
const Color c1 = Color.from(alpha: 1.0, red: 1.0, green: 0.0, blue: 0.0);

// 部分透明的中等蓝绿色
const Color c2 = Color.from(alpha: 0.5, red: 0.0, green: 0.5, blue: 0.5);

// 完全透明的颜色
const Color c3 = Color.from(alpha: 0.0, red: 0.0, green: 0.0, blue: 0.0);
```

### Color.fromARGB()

```dart
Color.fromARGB(int a, int r, int g, int b)
```

从四个整数的低 8 位构造一个 sRGB 颜色。

- `a` 为 alpha 值，0 表示透明，255 表示完全不透明。
- `r` 为 [red]（红色），范围 0 到 255。
- `g` 为 [green]（绿色），范围 0 到 255。
- `b` 为 [blue]（蓝色），范围 0 到 255。

超出范围的值会通过对 255 取模的方式限定到范围内。

另请参阅 [fromRGBO]，它以浮点值形式接收 alpha 值。

{@macro dart.ui.Color.componentsStoredAsFloatingPoint}

### Color.fromRGBO()

```dart
Color.fromRGBO(int r, int g, int b, double opacity)
```

根据红、绿、蓝和不透明度创建一个 sRGB 颜色，类似于 CSS 中的 `rgba()`。

- `r` 为 [red]（红色），范围 0 到 255。
- `g` 为 [green]（绿色），范围 0 到 255。
- `b` 为 [blue]（蓝色），范围 0 到 255。
- `opacity` 为该颜色的 alpha 通道，以 double 表示，0.0 表示透明，1.0 表示完全不透明。

超出范围的值会通过对 255 取模的方式限定到范围内。

另请参阅 [fromARGB]，它以整数值形式接收不透明度。

{@macro dart.ui.Color.componentsStoredAsFloatingPoint}

### a

```dart
double a
```

该颜色的 alpha 通道。

### r

```dart
double r
```

该颜色的红色通道。

### g

```dart
double g
```

该颜色的绿色通道。

### b

```dart
double b
```

该颜色的蓝色通道。

### colorSpace

```dart
ColorSpace colorSpace
```

该颜色的色彩空间。

### value

```dart
int get value
```

表示此颜色的 32 位值。

此获取器是一个 _stub_（存根）。建议改用显式的 [toARGB32] 方法。

### toARGB32()

```dart
int toARGB32()
```

返回表示此颜色的 32 位值。

返回值与默认构造函数（[Color.new]）兼容，但由于[数值转换中的精度损失](https://en.wikipedia.org/wiki/Floating-point_error_mitigation)，并不能保证得到相同的颜色。

与单独访问浮点等效通道（[a]、[r]、[g]、[b]）不同，此方法是有意设计为*有损*的，它使用 `(channel * 255.0).round().clamp(0, 255)` 对每个通道进行缩放。

虽然此方法可用于存储 32 位整数值，但在需要更高精度的情况下，建议直接访问各个通道（并存储其 double 等效值）。

各位的分配如下：

- 第 24-31 位表示 [a] 通道，为 8 位无符号整数。
- 第 16-23 位表示 [r] 通道，为 8 位无符号整数。
- 第 8-15 位表示 [g] 通道，为 8 位无符号整数。
- 第 0-7 位表示 [b] 通道，为 8 位无符号整数。

> [!WARNING]
> 此获取器返回的值通过 [toARGB32] 方法将浮点分量值（例如 `0.5`）隐式转换为其对应的 8 位等效值；由于浮点数运算的复杂性，返回值不保证在不同平台或不同执行过程中保持稳定。

### alpha

```dart
int get alpha
```

该颜色的 alpha 通道，以 8 位值表示。

值为 0 表示此颜色完全透明。值为 255 表示此颜色完全不透明。

### opacity

```dart
double get opacity
```

该颜色的 alpha 通道，以 double 表示。

值为 0.0 表示此颜色完全透明。值为 1.0 表示此颜色完全不透明。

### red

```dart
int get red
```

该颜色的红色通道，以 8 位值表示。

### green

```dart
int get green
```

该颜色的绿色通道，以 8 位值表示。

### blue

```dart
int get blue
```

该颜色的蓝色通道，以 8 位值表示。

### withValues()

```dart
Color withValues({double? alpha, double? red, double? green, double? blue, ColorSpace? colorSpace})
```

返回一个更新了指定分量的新颜色。

每个分量（[alpha]、[red]、[green]、[blue]）表示一个浮点值；详情和示例请参阅 [Color.from]。

如果提供了 [colorSpace] 且与当前色彩空间不同，则会先更新分量值，再将其转换到指定的 [colorSpace]。

示例：

```dart
import 'dart:ui';
/// 创建一个不透明度为 50% 的颜色。
Color makeTransparent(Color color) => color.withValues(alpha: 0.5);
```

### withAlpha()

```dart
Color withAlpha(int a)
```

返回一个新颜色，该颜色与此颜色相同，但 alpha 通道被替换为 `a`（范围为 0 到 255）。

超出范围的值会产生意外效果。

### withOpacity()

```dart
Color withOpacity(double opacity)
```

返回一个新颜色，该颜色与此颜色相同，但 alpha 通道被替换为给定的 `opacity`（范围为 0.0 到 1.0）。

超出范围的值会产生意外效果。

### withRed()

```dart
Color withRed(int r)
```

返回一个新颜色，该颜色与此颜色相同，但红色通道被替换为 `r`（范围为 0 到 255）。

超出范围的值会产生意外效果。

### withGreen()

```dart
Color withGreen(int g)
```

返回一个新颜色，该颜色与此颜色相同，但绿色通道被替换为 `g`（范围为 0 到 255）。

超出范围的值会产生意外效果。

### withBlue()

```dart
Color withBlue(int b)
```

返回一个新颜色，该颜色与此颜色相同，但蓝色通道被替换为 `b`（范围为 0 到 255）。

超出范围的值会产生意外效果。

### computeLuminance()

```dart
double computeLuminance()
```

返回一个介于 0（最暗）和 1（最亮）之间的亮度值。

表示该颜色的相对亮度。此值的计算开销较大。

参见 <https://en.wikipedia.org/wiki/Relative_luminance>。

### lerp()

```dart
Color? lerp(Color? x, Color? y, double t)
```

在两个颜色之间进行线性插值。

此方法旨在实现快速插值，但结果可能不够美观。可以考虑使用 [HSVColor](https://www.yuque.com/thyname/flutter.painting/hsvcolor) 或编写自定义的颜色插值逻辑。

如果其中一个颜色为 null，则此函数从另一个颜色的透明实例开始进行线性插值。这通常比从 [material.Colors.transparent]（即 `const Color(0x00000000)`，特指透明的*黑色*）进行插值更为可取。

`t` 参数表示在时间线上的位置，0.0 表示插值尚未开始，返回 `a`（或与 `a` 等效的值）；1.0 表示插值已完成，返回 `b`（或与 `b` 等效的值）；介于两者之间的值表示插值处于 `a` 与 `b` 之间时间线上的相应位置。插值可以外推到 0.0 和 1.0 之外，因此负值和大于 1.0 的值都是合法的（并且很容易由诸如 [Curves.elasticInOut] 之类的曲线生成）。每个通道都会被限定在 0 到 255 的范围内。

`t` 的值通常从 [Animation<double>]（例如 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)）获取。

如果两种颜色处于不同的色彩空间，则会先将两者都转换到色域更宽的色彩空间，再进行插值。结果将处于该更宽色域的色彩空间中。例如，在 sRGB 颜色和 Display P3 颜色之间进行插值将产生一个 Display P3 结果。

### alphaBlend()

```dart
Color alphaBlend(Color foreground, Color background)
```

将前景色作为透明颜色叠加在背景色之上，并返回合成后的结果颜色。

此方法使用标准的 alpha 混合（"SRC over DST"）规则，从两种颜色生成一种混合颜色。当需要绘制两个形状相同但相互叠加的纯色对象时，可以使用此方法作为性能优化手段，避免不必要的 alpha 混合合成操作：只需用合成后的颜色绘制一次即可。

### getAlphaFromOpacity()

```dart
int getAlphaFromOpacity(double opacity)
```

返回与给定 [opacity] 值相对应的 alpha 值。

[opacity] 值不能为 null。

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

# BlendMode

```dart
enum BlendMode {}
```

在画布上绘制时使用的算法。

在画布上绘制形状或图像时，可以使用不同的算法来混合像素。[BlendMode](https://www.yuque.com/thyname/dart.ui/blendmode) 的不同取值指定了不同的此类算法。

每种算法都有两个输入：_源（source）_，即正在绘制的图像；以及*目标（destination）*，即源图像被合成到其上的图像。目标通常被视为*背景*。源和目标都有四个颜色通道：红、绿、蓝和 alpha 通道，通常表示为 0.0 到 1.0 范围内的数值。该算法的输出同样具有这四个通道，其值由源和目标计算得出。

下面各取值的文档描述了该算法的工作原理。在每种情况下，图片展示了将源图像与目标图像混合后的输出结果。在下方的图片中，目标由带水平线条的图像和一张不透明的风景照片表示，源由带垂直线条的图像（与目标的线条相同但经过旋转）和一张鸟的剪贴画表示。[src] 模式仅显示源图像，[dst] 模式仅显示目标图像。在下方的文档中，透明度用棋盘格图案表示。[clear] 模式会丢弃源图像和目标图像，得到完全透明的输出（用纯棋盘格图案表示）。

这些图片中的水平和垂直条带展示了红、绿、蓝三个通道在不同不透明度级别下的效果，随后是三个颜色通道在相同不透明度级别下同时叠加的效果，接着是三个颜色通道均设为零、不透明度不同的效果，然后是两条展示红/绿/蓝重复渐变的色带（第一条完全不透明，第二条部分透明），最后是一条三个颜色通道均设为零、但不透明度呈重复渐变的色带。

## 在 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) API 中的应用

当使用 [Canvas.saveLayer] 和 [Canvas.restore] 时，传递给 [Canvas.saveLayer] 的 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 的混合模式会在调用 [Canvas.restore] 时被应用。每次调用 [Canvas.saveLayer] 都会在其上引入一个新的图层，用于绘制形状和图像；当调用 [Canvas.restore] 时，该图层会合成到父图层上，其中源是最近绘制的形状和图像，目标是父图层。（对于第一次调用 [Canvas.saveLayer]，父图层即画布本身。）

另请参阅：

- [Paint.blendMode]：使用 [BlendMode](https://www.yuque.com/thyname/dart.ui/blendmode) 定义合成策略。

丢弃源图像和目标图像，不留下任何内容。

这对应于 "clear" Porter-Duff 运算符。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_clear.png)

丢弃目标图像，仅绘制源图像。

从概念上讲，目标首先被清除，然后绘制源图像。

这对应于 "Copy" Porter-Duff 运算符。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_src.png)

丢弃源图像，仅绘制目标图像。

从概念上讲，源图像被丢弃，目标图像保持不变。

这对应于 "Destination" Porter-Duff 运算符。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_dst.png)

将源图像合成到目标图像之上。

这是默认值。它代表了最直观的情形，即形状被绘制在其下方内容之上，透明区域显示出目标图层。

这对应于 "Source over Destination" Porter-Duff 运算符，也称为画家算法（Painter's Algorithm）。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_srcOver.png)

将源图像合成到目标图像之下。

这与 [srcOver] 相反。

这对应于 "Destination over Source" Porter-Duff 运算符。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_dstOver.png)

当源图像本应在目标图像之前绘制、但由于某种原因无法做到时，此模式非常有用。

仅在两幅图像重叠的区域显示源图像。目标图像不会被渲染，仅被视为一个遮罩。目标的颜色通道会被忽略，只有不透明度会产生影响。

若要改为显示目标图像，可以考虑使用 [dstIn]。

若要反转遮罩的语义（仅在目标不存在的区域显示源，而非目标存在的区域），可以考虑使用 [srcOut]。

这对应于 "Source in Destination" Porter-Duff 运算符。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_srcIn.png)

仅在两幅图像重叠的区域显示目标图像。源图像不会被渲染，仅被视为一个遮罩。源的颜色通道会被忽略，只有不透明度会产生影响。

若要改为显示源图像，可以考虑使用 [srcIn]。

若要反转遮罩的语义（仅在源存在的区域显示源，而非源不存在的区域），可以考虑使用 [dstOut]。

这对应于 "Destination in Source" Porter-Duff 运算符。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_dstIn.png)

仅在两幅图像不重叠的区域显示源图像。目标图像不会被渲染，仅被视为一个遮罩。目标的颜色通道会被忽略，只有不透明度会产生影响。

若要改为显示目标图像，可以考虑使用 [dstOut]。

若要反转遮罩的语义（仅在目标存在的区域显示源，而非目标不存在的区域），可以考虑使用 [srcIn]。

这对应于 "Source out Destination" Porter-Duff 运算符。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_srcOut.png)

仅在两幅图像不重叠的区域显示目标图像。源图像不会被渲染，仅被视为一个遮罩。源的颜色通道会被忽略，只有不透明度会产生影响。

若要改为显示源图像，可以考虑使用 [srcOut]。

若要反转遮罩的语义（仅在源存在的区域显示目标，而非源不存在的区域），可以考虑使用 [dstIn]。

这对应于 "Destination out Source" Porter-Duff 运算符。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_dstOut.png)

将源图像合成到目标图像之上，但仅在与目标重叠的区域进行。

这对应于 "Source atop Destination" Porter-Duff 运算符。

这本质上是 [srcOver] 运算符，但输出的不透明度通道被设置为目标图像的不透明度，而不是两幅图像不透明度的组合。

如需目标在上、源在下的变体，请参阅 [dstATop]。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_srcATop.png)

将目标图像合成到源图像之上，但仅在与源重叠的区域进行。

这对应于 "Destination atop Source" Porter-Duff 运算符。

这本质上是 [dstOver] 运算符，但输出的不透明度通道被设置为源图像的不透明度，而不是两幅图像不透明度的组合。

如需源在上、目标在下的变体，请参阅 [srcATop]。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_dstATop.png)

对源图像和目标图像应用按位 `xor` 运算符。这会在两者重叠的位置留下透明区域。

这对应于 "Source xor Destination" Porter-Duff 运算符。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_xor.png)

将源图像和目标图像的分量相加。

一幅图像中某个像素的透明度会降低该图像对相应输出像素的贡献，就如同该图像中该像素的颜色变暗了一样。

这对应于 "Source plus Destination" Porter-Duff 运算符。

这是两幅图像之间交叉淡入淡出的正确混合模式。设有两幅图像 A 和 B，以及一个插值时间变量 _t_（从 0.0 到 1.0）。要在它们之间进行交叉淡入淡出，应先使用 [BlendMode.srcOver] 以不透明度 1.0 - _t_ 将 A 绘制到一个新图层中，再使用 [BlendMode.plus] 以不透明度 _t_ 将 B 绘制在其上，绘制到同一图层中。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_plus.png)

将源图像和目标图像的颜色分量相乘。

这只能得到相同或更深的颜色（乘以白色 1.0 不会产生变化；乘以黑色 0.0 会得到黑色）。

在合成两幅不透明图像时，此效果类似于在投影仪上叠加两张透明胶片。

如需了解在此基础上同时也对 alpha 通道进行相乘的变体，请参阅 [multiply]。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_modulate.png)

另请参阅：

- [screen]：执行类似但相反的计算。
- [overlay]：结合 [modulate] 和 [screen]，偏向目标图像。
- [hardLight]：结合 [modulate] 和 [screen]，偏向源图像。

将源图像和目标图像分量的反色相乘，再对结果取反。

分量取反意味着完全饱和的通道（不透明白色）被视为值 0.0，而通常被视为 0.0 的值（黑色、透明）被视为 1.0。

这本质上与 [modulate] 混合模式相同，但在相乘之前先对颜色值取反，并在渲染前将结果再次取反。

这只能得到相同或更浅的颜色（乘以黑色 1.0 不会产生变化；乘以白色 0.0 会得到白色）。类似地，在 alpha 通道中，只能得到不透明度更高的颜色。

此效果类似于两台投影仪同时在同一屏幕上显示各自的图像。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_screen.png)

另请参阅：

- [modulate]：执行类似的计算，但不对数值取反。
- [overlay]：结合 [modulate] 和 [screen]，偏向目标图像。
- [hardLight]：结合 [modulate] 和 [screen]，偏向源图像。

在调整源图像和目标图像的分量以偏向目标之后，将两者相乘。

具体而言，如果目标值较小，则将其与源值相乘；如果源值较小，则将源值的反色与目标值的反色相乘，然后对结果取反。

分量取反意味着完全饱和的通道（不透明白色）被视为值 0.0，而通常被视为 0.0 的值（黑色、透明）被视为 1.0。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_overlay.png)

另请参阅：

- [modulate]：始终相乘数值。
- [screen]：始终相乘数值的反色。
- [hardLight]：与 [overlay] 类似，但偏向源图像而非目标图像。

通过从每个颜色通道中选取较小的值来合成源图像和目标图像。

输出图像的不透明度计算方式与 [srcOver] 相同。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_darken.png)

通过从每个颜色通道中选取较大的值来合成源图像和目标图像。

输出图像的不透明度计算方式与 [srcOver] 相同。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_lighten.png)

用目标除以源的反色。

分量取反意味着完全饱和的通道（不透明白色）被视为值 0.0，而通常被视为 0.0 的值（黑色、透明）被视为 1.0。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_colorDodge.png)

用目标的反色除以源，再对结果取反。

分量取反意味着完全饱和的通道（不透明白色）被视为值 0.0，而通常被视为 0.0 的值（黑色、透明）被视为 1.0。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_colorBurn.png)

在调整源图像和目标图像的分量以偏向源之后，将两者相乘。

具体而言，如果源值较小，则将其与目标值相乘；如果目标值较小，则将目标值的反色与源值的反色相乘，然后对结果取反。

分量取反意味着完全饱和的通道（不透明白色）被视为值 0.0，而通常被视为 0.0 的值（黑色、透明）被视为 1.0。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_hardLight.png)

另请参阅：

- [modulate]：始终相乘数值。
- [screen]：始终相乘数值的反色。
- [overlay]：与 [hardLight] 类似，但偏向目标图像而非源图像。

对于低于 0.5 的源值使用 [colorDodge]，对于高于 0.5 的源值使用 [colorBurn]。

其效果与 [overlay] 类似但更柔和。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_softLight.png)

另请参阅：

- [color]：一种更细腻的着色效果。

对每个通道，用较大值减去较小值。

叠加黑色不会产生任何效果；叠加白色会反转另一幅图像的颜色。

输出图像的不透明度计算方式与 [srcOver] 相同。

此效果与 [exclusion] 类似，但更强烈。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_difference.png)

用两幅图像之和减去两幅图像乘积的两倍。

叠加黑色不会产生任何效果；叠加白色会反转另一幅图像的颜色。

输出图像的不透明度计算方式与 [srcOver] 相同。

此效果与 [difference] 类似，但更柔和。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_exclusion.png)

将源图像和目标图像的分量相乘，包括 alpha 通道。

这只能得到相同或更深的颜色（乘以白色 1.0 不会产生变化；乘以黑色 0.0 会得到黑色）。

由于 alpha 通道也会被相乘，其中一幅图像中完全透明的像素（不透明度 0.0）会使输出中的对应像素也完全透明。这与 [dstIn] 类似，但会同时混合颜色。

如需仅相乘颜色而不相乘 alpha 通道的变体，请参阅 [modulate]。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_multiply.png)

采用源图像的色相，以及目标图像的饱和度和明度。

效果是用源图像为目标图像着色。

输出图像的不透明度计算方式与 [srcOver] 相同。在源图像中完全透明的区域，其色相取自目标图像。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_hue.png)

另请参阅：

- [color]：一种类似但更强烈的效果，因为它同时应用了源图像的饱和度。
- [HSVColor](https://www.yuque.com/thyname/flutter.painting/hsvcolor)：允许使用色相（而非 [Color](https://www.yuque.com/thyname/dart.ui/color) 的红/绿/蓝通道）来表示颜色。

采用源图像的饱和度，以及目标图像的色相和明度。

输出图像的不透明度计算方式与 [srcOver] 相同。在源图像中完全透明的区域，其饱和度取自目标图像。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_saturation.png)

另请参阅：

- [color]：同时应用源图像的色相。
- [luminosity]：将源图像的明度应用于目标图像。

采用源图像的色相和饱和度，以及目标图像的明度。

效果是用源图像为目标图像着色。

输出图像的不透明度计算方式与 [srcOver] 相同。在源图像中完全透明的区域，其色相和饱和度取自目标图像。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_color.png)

另请参阅：

- [hue]：一种类似但较弱的效果。
- [softLight]：一种类似的着色效果，但也会为白色着色。
- [saturation]：仅应用源图像的饱和度。

采用源图像的明度，以及目标图像的色相和饱和度。

输出图像的不透明度计算方式与 [srcOver] 相同。在源图像中完全透明的区域，其明度取自目标图像。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/blend_mode_luminosity.png)

另请参阅：

- [saturation]：将源图像的饱和度应用于目标图像。
- [ImageFilter.blur]：可与 [BackdropFilter](https://www.yuque.com/thyname/flutter.widgets/backdropfilter) 结合使用以实现相关效果。

# FilterQuality

```dart
enum FilterQuality {}
```

用于 [ImageFilter](https://www.yuque.com/thyname/dart.ui/imagefilter) 和 [Shader](https://www.yuque.com/thyname/dart.ui/shader) 对图像进行采样的对象，以及用于渲染图像的 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 操作的图像采样质量级别。

放大时，质量通常在 [none] 时最低，在 [low] 和 [medium] 时较高，而对于非常大的缩放系数（超过 10 倍），在 [high] 时最高。

缩小时，[medium] 提供最佳质量，尤其是在将图像缩小到其原始尺寸的一半以下，或在这类缩小之间对缩放系数进行动画处理时。否则，对于 50% 到 100% 之间的缩小，[low] 和 [high] 提供相似的效果，但图像在低于 50% 时可能会丢失细节并出现丢帧现象。

为了在放大和缩小图像时，或在缩放系数未知时获得高质量效果，[medium] 通常是一个较为均衡的选择。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/filter_quality.png)

另请参阅：

- [Paint.filterQuality]：在 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 上使用 drawImage 调用时，用于将 [FilterQuality](https://www.yuque.com/thyname/dart.ui/filterquality) 传递给引擎。
- [ImageShader](https://www.yuque.com/thyname/dart.ui/imageshader)。
- [FragmentShader.setImageSampler]。
- [ImageFilter.matrix]。
- [Canvas.drawImage]。
- [Canvas.drawImageRect]。
- [Canvas.drawImageNine]。
- [Canvas.drawAtlas]。

最快的过滤方法，但质量也最低。

此值会产生一种"最近邻"（Nearest Neighbor）算法，在图像放大或缩小时，仅通过重复或剔除像素来实现。

质量优于 [none]，速度快于 [medium]。

此值会产生一种"双线性"（Bilinear）算法，在图像中的像素之间进行平滑插值。

在各种过滤方法中综合表现最佳，仅在极大的缩放系数下逊色于 [high]。

此值在 [low] 指定的"双线性"算法基础上进行了改进，利用 Mipmap 预先计算图像在一半（以及四分之一、八分之一等）尺寸下的高质量低分辨率版本，然后在这些版本之间进行混合，以防止在缩小尺寸时丢失细节。

{@template dart.ui.filterQuality.seeAlso} 另请参阅：

- [FilterQuality](https://www.yuque.com/thyname/dart.ui/filterquality) 类级别文档，详细讨论了各常量值的相对质量。 {@endtemplate}

当以大于 5-10 倍的缩放系数放大图像时，可获得最佳质量。

当图像缩小时，对于小于 0.5 倍的缩放，或在对缩放系数进行动画处理时，此选项的效果可能比 [medium] 更差。

此选项也是最慢的。

此值会产生一种标准的"双三次"（Bicubic）算法，该算法使用三阶方程来平滑像素之间的突变过渡，同时保留一定的边缘感并避免结果中出现尖锐的峰值。

{@macro dart.ui.filterQuality.seeAlso}

# StrokeCap

```dart
enum StrokeCap {}
```

用于线条端点的样式。

另请参阅：

- [Paint.strokeCap]：了解此值的使用方式。
- [StrokeJoin](https://www.yuque.com/thyname/dart.ui/strokejoin)：不同种类的线段连接方式。

以平直边缘开始和结束轮廓，不做任何延伸。

![平头端点（butt cap）以方形端点结束线段，该端点在线段末端处终止。](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/butt_cap.png)

与 [square]（方形）端点相比，两者形状相同，但方形端点会超出线段末端延伸半个描边宽度。

以半圆形延伸开始和结束轮廓。

![圆头端点（round cap）会在线段末端添加一个圆形端点，其突出长度为线条粗细的一半（即端点的半径）。](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/round_cap.png)

上图中该端点被着色以突出显示：在正常使用中，它与线条颜色相同。

以半个方形延伸开始和结束轮廓。这类似于将每条轮廓延伸半个描边宽度（由 [Paint.strokeWidth] 给出）。

![方头端点（square cap）具有方形端点，可有效地将线条长度延伸半个描边宽度。](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/square_cap.png)

上图中该端点被着色以突出显示：在正常使用中，它与线条颜色相同。

与 [butt]（平头）端点相比，两者形状相同，但平头端点不会超出线段末端延伸。

# StrokeJoin

```dart
enum StrokeJoin {}
```

用于线段连接处的样式。

这仅影响由 [Canvas.drawPath] 绘制的多边形和矩形的线条连接方式，不影响使用 [Canvas.drawPoints] 绘制为线条的点。

另请参阅：

- [Paint.strokeJoin] 和 [Paint.strokeMiterLimit]：了解此值的使用方式。
- [StrokeCap](https://www.yuque.com/thyname/dart.ui/strokecap)：不同种类的线条端点。

线段之间的连接形成尖角。

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/miter_4_join.mp4}

上图中线段的中心部分被着色以突出显示连接处，但在正常使用中，连接处与线条颜色相同。

另请参阅：

- [Paint.strokeJoin]：用于将线段连接样式设置为此值。
- [Paint.strokeMiterLimit]：用于定义当连接设置为此值时，何时应绘制斜接（miter）而非斜切（bevel）。

线段之间的连接呈半圆形。

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/round_join.mp4}

上图中线段的中心部分被着色以突出显示连接处，但在正常使用中，连接处与线条颜色相同。

另请参阅：

- [Paint.strokeJoin]：用于将线段连接样式设置为此值。

线段之间的连接会将线段平头端点的角连接起来，形成斜切（beveled）外观。

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/bevel_join.mp4}

上图中线段的中心部分被着色以突出显示连接处，但在正常使用中，连接处与线条颜色相同。

另请参阅：

- [Paint.strokeJoin]：用于将线段连接样式设置为此值。

# PaintingStyle

```dart
enum PaintingStyle {}
```

在画布上绘制形状和路径的策略。

参见 [Paint.style]。

将 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 应用于形状的内部。例如，应用于 [Canvas.drawCircle] 调用时，会绘制出给定大小的实心圆盘。

将 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 应用于形状的边缘。例如，应用于 [Canvas.drawCircle] 调用时，会绘制出给定大小的圆环。边缘绘制的线条宽度由 [Paint.strokeWidth] 属性给出。

# Clip

```dart
enum Clip {}
```

不同的内容裁剪方式。

另请参阅：

- [Paint.isAntiAlias]：常规绘制操作的抗锯齿开关。

完全不裁剪。

这是大多数组件的默认选项：如果内容没有超出组件边界，则不会为裁剪付出任何性能代价。

如果内容确实超出边界，可以考虑以下 [Clip](https://www.yuque.com/thyname/dart.ui/clip) 选项：

- [hardEdge]：裁剪速度最快，但保真度较低。
- [antiAlias]：比 [hardEdge] 略慢，但边缘经过平滑处理。
- [antiAliasWithSaveLayer]：比 [antiAlias] 慢得多，应尽量少用。

进行裁剪，但不应用抗锯齿。

此模式启用裁剪，但曲线和非轴对齐的直线会出现锯齿，因为不会做任何抗锯齿处理。

比其他裁剪模式更快，但比 [none] 慢。

如果容器是轴对齐的矩形，或是圆角半径非常小的轴对齐圆角矩形，这是一个合理的选择。

另请参阅：

- [antiAlias]：当需要裁剪且形状不是轴对齐矩形时推荐使用。

带抗锯齿的裁剪。

此模式具有抗锯齿的裁剪边缘，当裁剪形状本身具有对角线、曲线或其他非轴对齐的边缘时，可以减少锯齿。

这比 [antiAliasWithSaveLayer] 快得多，但比 [hardEdge] 慢。

与 [hardEdge] 和 [antiAliasWithSaveLayer] 不同，此裁剪可能会出现边缘渗色伪影（[Skia Fiddle 示例](https://fiddle.skia.org/c/21cb4c2b2515996b537f36e7819288ae)）。

另请参阅：

- [hardEdge]：速度更快，但保真度较低。
- [antiAliasWithSaveLayer]：速度慢得多，但可避免边缘渗色伪影。
- [Paint.isAntiAlias]：常规绘制操作的抗锯齿开关。

带抗锯齿的裁剪，并在裁剪之后立即执行 `saveLayer`。

此模式不仅使用抗锯齿进行裁剪，还会分配一个离屏缓冲区。所有后续的绘制都会先在该缓冲区上进行，最终再进行裁剪并合成回原图。

此方式非常慢。与 [antiAlias] 不同，它不会产生边缘渗色伪影，但它会引入一个离屏缓冲区，从而改变语义。例如，参见这个[不使用 `saveLayer` 的 Skia Fiddle 示例](https://fiddle.skia.org/c/83ed46ceadaf90f36a4df3b98cbe1c35)和这个[使用 `saveLayer` 的 Skia Fiddle 示例](https://fiddle.skia.org/c/704acfa049a7e99fbe685232c45d1582)。

仅在必要时使用此模式。例如，如果需要在差异很大的背景颜色上叠加一张图片。在这种情况下，请考虑是否可以避免在同一位置叠加多种颜色（例如，让背景颜色仅出现在图片缺失的地方）。如果可能，请优先使用 [antiAlias]，因为它要快得多。

另请参阅：

- [antiAlias]：速度快得多，且裁剪效果相似。
- [Canvas.saveLayer]。

# Paint

```dart
final class Paint {}
```

描述在 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 上绘制时所用样式的类。

[Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 上的大多数 API 都接受一个 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 对象，用于描述该操作所使用的样式。

### Paint()

```dart
Paint()
```

构造一个所有字段均初始化为默认值的空 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 对象。

### Paint.from()

```dart
Paint.from(Paint other)
```

构造一个与 [other] 具有相同字段的新 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 对象。

对返回对象所做的任何更改都不会影响 [other]，对 [other] 的更改也不会影响返回的对象。

不同后端（例如 web 与原生）可能具有不同的性能特征。如果代码对性能敏感，请考虑进行性能分析，并在必要时改为复用单个 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 对象。

### isAntiAlias

```dart
bool get isAntiAlias
```

是否对画布上绘制的线条和图像应用抗锯齿。

默认为 true。

### isAntiAlias

```dart
set isAntiAlias(bool value)
```

### color

```dart
Color get color
```

对形状进行描边或填充时使用的颜色。

默认为不透明黑色。

另请参阅：

- [style]：控制是描边、填充还是两者兼有。
- [colorFilter]：会覆盖 [color]。
- [shader]：以更精细的效果覆盖 [color]。

此颜色不用于合成。要为图层着色，请使用 [colorFilter]。

### color

```dart
set color(Color value)
```

### blendMode

```dart
BlendMode get blendMode
```

绘制形状或合成图层时应用的混合模式。

源颜色来自正在绘制的形状（例如来自 [Canvas.drawPath]）或正在合成的图层（在 [Canvas.saveLayer] 和 [Canvas.restore] 调用之间绘制的图形），并在此之前应用了（如果有的话）[colorFilter]。

目标颜色来自形状或图层被合成到的背景。

默认为 [BlendMode.srcOver]。

另请参阅：

- [Canvas.saveLayer]：在调用 [Canvas.restore] 时，使用其 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 的 [blendMode] 来合成图层。
- [BlendMode](https://www.yuque.com/thyname/dart.ui/blendmode)：讨论了 [Canvas.saveLayer] 与 [blendMode] 的配合使用。

### blendMode

```dart
set blendMode(BlendMode value)
```

### style

```dart
PaintingStyle get style
```

是绘制形状内部、形状边缘，还是两者都绘制。

默认为 [PaintingStyle.fill]。

### style

```dart
set style(PaintingStyle value)
```

### strokeWidth

```dart
double get strokeWidth
```

当 [style] 设置为 [PaintingStyle.stroke] 时，绘制边缘的宽度。该宽度以逻辑像素为单位，沿垂直于路径方向的方向度量。

默认为 0.0，对应于发丝宽度（hairline width）。

### strokeWidth

```dart
set strokeWidth(double value)
```

### strokeCap

```dart
StrokeCap get strokeCap
```

当 [style] 设置为 [PaintingStyle.stroke] 时，绘制线条末端所使用的收尾样式。

默认为 [StrokeCap.butt]，即无端点。

### strokeCap

```dart
set strokeCap(StrokeCap value)
```

### strokeJoin

```dart
StrokeJoin get strokeJoin
```

线段之间连接处所使用的收尾样式。

这适用于当 [style] 设置为 [PaintingStyle.stroke] 时绘制的路径，不适用于使用 [Canvas.drawPoints] 绘制为线条的点。

默认为 [StrokeJoin.miter]，即尖角。

一些连接方式的示例：

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/miter_4_join.mp4}

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/round_join.mp4}

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/bevel_join.mp4}

上图中线段的中心部分被着色以突出显示连接处，但在正常使用中，连接处与线条颜色相同。

另请参阅：

- [strokeMiterLimit]：控制当此值设置为 [StrokeJoin.miter] 时，斜接何时会被斜切替代。
- [strokeCap]：控制描边末端的绘制方式。
- [StrokeJoin](https://www.yuque.com/thyname/dart.ui/strokejoin)：查看完整的线条连接方式列表。

### strokeJoin

```dart
set strokeJoin(StrokeJoin value)
```

### strokeMiterLimit

```dart
double get strokeMiterLimit
```

当连接方式设置为 [StrokeJoin.miter] 且 [style] 设置为 [PaintingStyle.stroke] 时，线段上斜接（miter）绘制的限制值。如果超过此限制，则会改为绘制 [StrokeJoin.bevel] 连接。当线段之间的夹角被动画化时，这可能会导致路径拐角处出现"跳变"现象，如下图所示。

此限制以斜接长度的限制形式表示。

默认为 4.0。使用零作为限制会导致始终使用 [StrokeJoin.bevel] 连接。

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/miter_0_join.mp4}

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/miter_4_join.mp4}

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/dart-ui/miter_6_join.mp4}

上图中线段的中心部分被着色以突出显示连接处，但在正常使用中，连接处与线条颜色相同。

另请参阅：

- [strokeJoin]：控制线段之间连接处所使用的收尾样式。
- [strokeCap]：控制描边末端的绘制方式。

### strokeMiterLimit

```dart
set strokeMiterLimit(double value)
```

### maskFilter

```dart
MaskFilter? get maskFilter
```

在形状绘制完成后、合成到图像之前应用于该形状的遮罩过滤器（例如模糊效果）。

详情请参阅 [MaskFilter](https://www.yuque.com/thyname/dart.ui/maskfilter)。

### maskFilter

```dart
set maskFilter(MaskFilter? value)
```

### filterQuality

```dart
FilterQuality get filterQuality
```

在对位图进行采样时（例如使用 [ImageShader](https://www.yuque.com/thyname/dart.ui/imageshader)），或在绘制图像时（例如使用 [Canvas.drawImage]、[Canvas.drawImageRect]、[Canvas.drawImageNine] 或 [Canvas.drawAtlas]），控制性能与质量之间权衡的参数。

默认为 [FilterQuality.none]。

### filterQuality

```dart
set filterQuality(FilterQuality value)
```

### shader

```dart
Shader? get shader
```

对形状进行描边或填充时使用的着色器（shader）。

当此值为 null 时，将改为使用 [color]。

另请参阅：

- [Gradient](https://www.yuque.com/thyname/dart.ui/gradient)：一种绘制颜色渐变的着色器。
- [ImageShader](https://www.yuque.com/thyname/dart.ui/imageshader)：一种平铺 [Image](https://www.yuque.com/thyname/dart.ui/image) 的着色器。
- [colorFilter]：会覆盖 [shader]。
- [color]：当 [shader] 和 [colorFilter] 均为 null 时使用。

### shader

```dart
set shader(Shader? value)
```

### colorFilter

```dart
ColorFilter? get colorFilter
```

在绘制形状或合成图层时应用的颜色过滤器。

详情请参阅 [ColorFilter](https://www.yuque.com/thyname/dart.ui/colorfilter)。

在绘制形状时，[colorFilter] 会覆盖 [color] 和 [shader]。

### colorFilter

```dart
set colorFilter(ColorFilter? value)
```

### imageFilter

```dart
ImageFilter? get imageFilter
```

绘制光栅图像时使用的 [ImageFilter](https://www.yuque.com/thyname/dart.ui/imagefilter)。

例如，要在使用 [Canvas.drawImage] 时对图像进行模糊处理，可以应用 [ImageFilter.blur]：

```dart
void paint(Canvas canvas, Size size) {
  canvas.drawImage(
    _image,
    ui.Offset.zero,
    Paint()..imageFilter = ui.ImageFilter.blur(sigmaX: 0.5, sigmaY: 0.5),
  );
}
```

另请参阅：

- [MaskFilter](https://www.yuque.com/thyname/dart.ui/maskfilter)：用于绘制几何图形。

### imageFilter

```dart
set imageFilter(ImageFilter? value)
```

### invertColors

```dart
bool get invertColors
```

绘制图像时是否反转其颜色。

反转图像的颜色会应用一个新的颜色过滤器，该过滤器会与用户提供的任何颜色过滤器组合。这主要用于在 iOS 上实现智能反转（smart invert）。

### invertColors

```dart
set invertColors(bool value)
```

### toString()

```dart
String toString()
```

# ColorSpace

```dart
enum ColorSpace {}
```

色彩空间描述了 [Image](https://www.yuque.com/thyname/dart.ui/image) 可用的颜色范围。

此值有助于确定在 [Image.toByteData] 中使用哪种 [ImageByteFormat](https://www.yuque.com/thyname/dart.ui/imagebyteformat)。处于 [extendedSRGB] 色彩空间的图像应使用类似 [ImageByteFormat.rawExtendedRgba128] 的格式，以避免丢失超出 sRGB 色域的颜色。

这也是 [Image.colorSpace] 的返回结果。

另请参阅：https://en.wikipedia.org/wiki/Color_space

sRGB 色彩空间。

你可能了解它是 web 的标准色彩空间，也是非广色域 Flutter 应用的色彩空间。

另请参阅：https://en.wikipedia.org/wiki/SRGB

一种与 sRGB 向后兼容、但可以用 [0..1] 之外的值表示该色域之外颜色的色彩空间。要查看扩展值，必须使用类似 [ImageByteFormat.rawExtendedRgba128] 的 [ImageByteFormat](https://www.yuque.com/thyname/dart.ui/imagebyteformat)。

Display P3 色彩空间。

这是一种具有广泛硬件支持的广色域色彩空间。例如在 iOS 上使用 Impeller 时即支持此空间。在不支持 Display P3 的平台上使用时，颜色会被限定（clamp）到 sRGB。

另请参阅：https://en.wikipedia.org/wiki/DCI-P3

# ImageByteFormat

```dart
enum ImageByteFormat {}
```

使用 [Image.toByteData] 时返回图像字节所采用的格式。

原始 RGBA 格式。

未编码字节，按行优先的 RGBA 形式排列，使用预乘 alpha，每个通道 8 位。

原始直接 RGBA 格式。

未编码字节，按行优先的 RGBA 形式排列，使用直接（straight）alpha，每个通道 8 位。

原始未修改格式。

未编码字节，采用图像现有的格式。例如，灰度图像的每个像素可能使用单个 8 位通道。

原始扩展范围 RGBA 格式。

未编码字节，按行优先的 RGBA 形式排列，使用直接（straight）alpha，每个通道为 32 位浮点数（IEEE 754 binary32）。

示例用法：

```dart
import 'dart:ui' as ui;
import 'dart:typed_data';

Future<Map<String, double>> getFirstPixel(ui.Image image) async {
  final ByteData data =
      (await image.toByteData(format: ui.ImageByteFormat.rawExtendedRgba128))!;
  final Float32List floats = Float32List.view(data.buffer);
  return <String, double>{
    'r': floats[0],
    'g': floats[1],
    'b': floats[2],
    'a': floats[3],
  };
}
```

PNG 格式。

一种无损压缩的图像格式。此格式非常适合具有硬边缘的图像，例如截图或精灵图，以及带有文本的图像。支持透明度。PNG 格式支持每个维度最多 2,147,483,647 像素的图像，不过在实践中，可用内存对最大图像尺寸构成了更直接的限制。

PNG 图像通常使用 `.png` 文件扩展名和 `image/png` MIME 类型。

另请参阅：

- <https://en.wikipedia.org/wiki/Portable_Network_Graphics>：关于 PNG 的维基百科页面。
- <https://tools.ietf.org/rfc/rfc2083.txt>：PNG 标准。

# PixelFormat

```dart
enum PixelFormat {}
```

传递给 [decodeImageFromPixels](https://www.yuque.com/thyname/dart.ui/decodeimagefrompixels) 的像素数据格式。

每个像素为 32 位，最高 8 位表示红色，接下来的 8 位表示绿色，再接下来的 8 位表示蓝色，最低 8 位表示 alpha。使用预乘 alpha。

每个像素为 32 位，最高 8 位表示蓝色，接下来的 8 位表示绿色，再接下来的 8 位表示红色，最低 8 位表示 alpha。使用预乘 alpha。

每个像素为 128 位，其中每个颜色分量为一个在 sRGB 色域内归一化的 32 位浮点数。第一个浮点数为红色分量，随后依次为：绿色、蓝色和 alpha。不使用预乘 alpha，与 [ImageByteFormat.rawExtendedRgba128] 一致。

每个像素为 32 位，红色通道仅为一个 32 位浮点数。

# TargetPixelFormat

```dart
enum TargetPixelFormat {}
```

由 [decodeImageFromPixels](https://www.yuque.com/thyname/dart.ui/decodeimagefrompixels) 生成的纹理所使用的像素数据格式。

未指定像素格式，由引擎决定最佳像素格式。

每个像素为 128 位，其中每个颜色分量为一个 32 位浮点数。

每个像素为 32 位，红色通道仅为一个 32 位浮点数。

# ImageEventCallback

```dart
typedef ImageEventCallback = void Function(Image image)
```

[Image](https://www.yuque.com/thyname/dart.ui/image) 生命周期事件的签名。

# Image

```dart
class Image {}
```

指向原始已解码图像数据（像素）的不透明句柄。

要获取 [Image](https://www.yuque.com/thyname/dart.ui/image) 对象，请使用 [ImageDescriptor](https://www.yuque.com/thyname/dart.ui/imagedescriptor) API。

要绘制 [Image](https://www.yuque.com/thyname/dart.ui/image)，请使用 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 类上的某个方法，例如 [Canvas.drawImage]。

接收 image 对象的类或方法必须在不再需要该句柄时对其调用 [dispose]。要创建对底层图像的可共享引用，请调用 [clone]。接收新实例的方法或对象将负责释放该实例，而底层图像本身将在所有未释放的句柄都被释放后才会被释放。

如果 `dart:ui` 传递了一个 `Image` 对象，而接收方希望将该句柄与其他调用方共享，则必须在调用 [dispose] _之前_ 调用 [clone]。已释放的句柄无法再创建新的句柄。

另请参阅：

- [Image](https://www.yuque.com/thyname/dart.ui/image)：[widgets](https://www.yuque.com/thyname/flutter.widgets) 库中的对应类。
- [ImageDescriptor](https://www.yuque.com/thyname/dart.ui/imagedescriptor)：允许读取图像信息并创建用于解码的 codec。
- [instantiateImageCodec](https://www.yuque.com/thyname/dart.ui/instantiateimagecodec)：一个封装了 [ImageDescriptor](https://www.yuque.com/thyname/dart.ui/imagedescriptor) 的实用方法。

### onCreate

```dart
ImageEventCallback? onCreate
```

用于报告图像创建的回调。

相比直接使用 [onCreate]，更推荐使用 flutter/foundation.dart 中的 [MemoryAllocations](https://www.yuque.com/thyname/flutter.foundation/memoryallocations)，因为 [MemoryAllocations](https://www.yuque.com/thyname/flutter.foundation/memoryallocations) 支持多个回调。

### onDispose

```dart
ImageEventCallback? onDispose
```

用于报告图像释放的回调。

相比直接使用 [onDispose]，更推荐使用 flutter/foundation.dart 中的 [MemoryAllocations](https://www.yuque.com/thyname/flutter.foundation/memoryallocations)，因为 [MemoryAllocations](https://www.yuque.com/thyname/flutter.foundation/memoryallocations) 支持多个回调。

### width

```dart
int width
```

沿图像水平轴的图像像素数。

### height

```dart
int height
```

沿图像垂直轴的图像像素数。

### dispose()

```dart
void dispose()
```

释放此句柄对底层 Image 的占用。调用此方法后，此句柄将不再可用。

一旦所有未释放的句柄都被释放，底层图像也将随之释放。

在调试模式下，[debugGetOpenHandleStackTraces] 将返回所有未关闭句柄创建位置的 [StackTrace](https://www.yuque.com/thyname/dart.core/stacktrace) 对象列表。这在尝试确定程序的哪些部分使某个图像一直驻留在内存中时非常有用。

### debugDisposed

```dart
bool get debugDisposed
```

此底层图像的引用是否已被 [dispose]。

仅当启用了断言时，此方法才会返回有效值，且不得在其他情况下使用。

### toByteData()

```dart
Future<ByteData?> toByteData({ImageByteFormat format = ImageByteFormat.rawRgba})
```

将 [Image](https://www.yuque.com/thyname/dart.ui/image) 对象转换为字节数组。

[format] 参数指定返回字节所采用的格式。

对处于 [ColorSpace.extendedSRGB] 色彩空间的图像使用 [ImageByteFormat.rawRgba] 会导致色域被压缩以适配 sRGB 色域，从而丢失广色域颜色。

返回一个 Future，其在完成时携带二进制图像数据，或在编码失败时携带错误。

### colorSpace

```dart
ColorSpace get colorSpace
```

[Image](https://www.yuque.com/thyname/dart.ui/image) 的颜色所使用的色彩空间。

此值是 [Image](https://www.yuque.com/thyname/dart.ui/image) 创建方式的结果。例如，加载一个处于 Display P3 色彩空间的 PNG 会得到一个 [ColorSpace.extendedSRGB] 图像。

在不支持广色域颜色的渲染后端上（除 iOS Impeller 之外的所有后端），如果不支持渲染广色域颜色，广色域图像仍会报告为 [ColorSpace.sRGB]。

### debugGetOpenHandleStackTraces()

```dart
List<StackTrace>? debugGetOpenHandleStackTraces()
```

如果启用了断言，返回来自 [clone] 的每个未关闭句柄的 [StackTrace](https://www.yuque.com/thyname/dart.core/stacktrace)，按创建顺序排列。

如果禁用了断言，此方法始终返回 null。

### clone()

```dart
Image clone()
```

为此图像创建一个可释放的句柄。

[Image](https://www.yuque.com/thyname/dart.ui/image) 的持有者必须在不再需要访问或绘制该图像时释放该图像。但是，一旦底层图像被释放，就不能再使用它。如果图像的某个持有者需要与另一个对象或方法共享对该图像的访问权，[clone] 会创建一个重复的句柄。只有当所有未释放的句柄都被释放后，底层图像才会被释放。这样就可以在安全共享图像引用的同时，在所有使用方都完成使用后释放底层资源。

如果当前持有者不再需要某个 [Image](https://www.yuque.com/thyname/dart.ui/image) 句柄，则可以安全地将其传递给另一个对象或方法。

要检查两个 [Image](https://www.yuque.com/thyname/dart.ui/image) 引用是否指向同一个底层图像内存，应使用 [isCloneOf]，而不是相等运算符或 [identical](https://www.yuque.com/thyname/dart.core/identical)。

以下示例演示了正确的用法。

```dart
import 'dart:async';
import 'dart:typed_data';
import 'dart:ui';

Future<Image> _loadImage(int width, int height) {
  final Completer<Image> completer = Completer<Image>();
  decodeImageFromPixels(
    Uint8List.fromList(List<int>.filled(width * height * 4, 0xFF)),
    width,
    height,
    PixelFormat.rgba8888,
    // 不必担心释放或克隆此图像——责任已转移给调用方，
    // 这样做是安全的，因为此方法之后不会再接触该图像。
    (Image image) => completer.complete(image),
  );
  return completer.future;
}

Future<void> main() async {
  final Image image = await _loadImage(5, 5);
  // 请务必克隆该图像，因为 MyHolder 可能会释放它，
  // 而我们需要再次访问它。
  final MyImageHolder holder = MyImageHolder(image.clone());
  final MyImageHolder holder2 = MyImageHolder(image.clone());
  // 现在释放它，因为我们不会再需要它了。
  image.dispose();

  final PictureRecorder recorder = PictureRecorder();
  final Canvas canvas = Canvas(recorder);

  holder.draw(canvas);
  holder.dispose();

  canvas.translate(50, 50);
  holder2.draw(canvas);
  holder2.dispose();
}

class MyImageHolder {
  MyImageHolder(this.image);

  final Image image;

  void draw(Canvas canvas) {
    canvas.drawImage(image, Offset.zero, Paint());
  }

  void dispose() => image.dispose();
}
```

返回对象的行为与此图像完全相同。对其调用 [dispose] 只有在它是最后一个剩余句柄时才会释放底层原生资源。

### isCloneOf()

```dart
bool isCloneOf(Image other)
```

如果 `other` 是此对象的 [clone]（即使 this 或 `other` 已被 [dispose]），因而共享同一底层图像内存，则返回 true。

对于从同一底层资源解码出的两个图像，如果它们没有共享同一内存，此方法可能会返回 false。例如，如果同一文件使用 [instantiateImageCodec](https://www.yuque.com/thyname/dart.ui/instantiateimagecodec) 解码两次，或同一字节数据使用 [decodeImageFromPixels](https://www.yuque.com/thyname/dart.ui/decodeimagefrompixels) 解码两次，将会得到两个渲染效果相同、但不共享底层内存的不同 [Image](https://www.yuque.com/thyname/dart.ui/image)，因此不会被视为彼此的克隆。

### toString()

```dart
String toString()
```

# ImageDecoderCallback

```dart
typedef ImageDecoderCallback = void Function(Image result)
```

[decodeImageFromList](https://www.yuque.com/thyname/dart.ui/decodeimagefromlist) 的回调签名。

# FrameInfo

```dart
class FrameInfo {}
```

动画中单帧的信息。

要获取 [FrameInfo](https://www.yuque.com/thyname/dart.ui/frameinfo) 接口的实例，请参阅 [Codec.getNextFrame]。

此类实例的接收方负责对 [image] 调用 [Image.dispose]。要与其他相关方共享该图像，请使用 [Image.clone]。如果 [FrameInfo](https://www.yuque.com/thyname/dart.ui/frameinfo) 对象本身被传递给另一个方法或对象，则该方法或对象必须自行负责在使用完毕后释放该图像，且传递方在此之后不得再访问该 [image]。

例如，以下代码示例是不正确的：

```dart
/// 错误示例
Future<void> nextFrameRoutine(ui.Codec codec) async {
  final ui.FrameInfo frameInfo = await codec.getNextFrame();
  _cacheImage(frameInfo);
  // 错误——_cacheImage 现在负责释放该图像，
  // 该图像可能不再可用于此绘制流程。
  _drawImage(frameInfo);
  // 再次错误——之前的方法可能已经创建了指向该图像的句柄，也可能没有。
  frameInfo.image.dispose();
}
```

正确的用法是：

```dart
/// 正确示例
Future<void> nextFrameRoutine(ui.Codec codec) async {
  final ui.FrameInfo frameInfo = await codec.getNextFrame();
  _cacheImage(frameInfo.image.clone(), frameInfo.duration);
  _drawImage(frameInfo.image.clone(), frameInfo.duration);
  // 此方法已用完自己的句柄，并已将句柄传递给它的调用方。
  // 该图像将一直存在，直到这些调用方释放各自的句柄，
  // 而此处的句柄不需要释放，因为它不会再被使用。
  frameInfo.image.dispose();
}
```

### duration

```dart
Duration duration
```

此帧应显示的持续时间。

持续时间为零表示该帧应无限期显示。

### image

```dart
Image image
```

此帧对应的 [Image](https://www.yuque.com/thyname/dart.ui/image) 对象。

此对象必须由此帧信息的接收方负责释放。

要与其他相关方共享此图像，请使用 [Image.clone]。

# Codec

```dart
abstract class Codec {}
```

指向图像 codec 的句柄。

此类由引擎创建，不应直接实例化或扩展。

要获取 [Codec](https://www.yuque.com/thyname/dart.ui/codec) 接口的实例，请参阅 [instantiateImageCodec](https://www.yuque.com/thyname/dart.ui/instantiateimagecodec)。

### frameCount

```dart
int get frameCount
```

此图像中的帧数。

### repetitionCount

```dart
int get repetitionCount
```

动画重复播放的次数。

- 0 表示动画只播放一次。
- -1 表示无限次重复。

### getNextFrame()

```dart
Future<FrameInfo> getNextFrame()
```

获取下一个动画帧。

返回最后一帧后会回绕到第一帧。

如果解码失败，返回的 Future 可能以错误完成。

调用此方法的一方负责释放返回对象中的 [FrameInfo.image]。

### dispose()

```dart
void dispose()
```

释放此对象使用的资源。调用此方法后，该对象将不再可用。

此方法不能是叶子调用（leaf call），因为该原生函数会调用 Dart API（Dart_SetNativeInstanceField）。

# instantiateImageCodec()

```dart
Future<Codec> instantiateImageCodec(Uint8List list, {int? targetWidth, int? targetHeight, bool allowUpscaling = true})
```

实例化一个图像 [Codec](https://www.yuque.com/thyname/dart.ui/codec)。

此方法是对 [ImageDescriptor](https://www.yuque.com/thyname/dart.ui/imagedescriptor) API 的一个便捷封装，建议直接使用 [ImageDescriptor](https://www.yuque.com/thyname/dart.ui/imagedescriptor)，因为它允许调用方更好地决定如何以及是否使用 `targetWidth` 和 `targetHeight` 参数。

`list` 参数为二进制图像数据（例如 PNG 或 GIF 的二进制数据）。数据可以是静态图像或动画图像。支持以下图像格式：

{@template dart.ui.imageFormats} JPEG、PNG、GIF、动图 GIF、WebP、动图 WebP、BMP 和 WBMP。底层平台可能支持其他附加格式。Flutter 会尝试调用平台 API 来解码无法识别的格式，如果平台 API 支持解码该图像，Flutter 将能够渲染它。 {@endtemplate}

`targetWidth` 和 `targetHeight` 参数以图像像素为单位指定输出图像的大小。如果它们与图像的固有尺寸不相等，则图像会在解码后进行缩放。如果 `allowUpscaling` 参数未设置为 true，则即使只有一个维度会超出图像的固有尺寸，两个维度也都会被限定在图像的固有尺寸以内。如果这两个参数中恰好只指定了一个，则会在强制图像匹配另一个给定维度的同时保持宽高比。如果两者均未指定，则图像会保持其固有大小。

通常应避免将图像缩放到大于其固有大小，因为这会导致图像占用比必要更多的内存。建议改为缩放 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 变换。如果必须放大图像，则必须将 `allowUpscaling` 参数设置为 true。

如果图像解码失败，返回的 Future 可能以错误完成。

# instantiateImageCodecFromBuffer()

```dart
Future<Codec> instantiateImageCodecFromBuffer(ImmutableBuffer buffer, {int? targetWidth, int? targetHeight, bool allowUpscaling = true})
```

实例化一个图像 [Codec](https://www.yuque.com/thyname/dart.ui/codec)。

此方法是对 [ImageDescriptor](https://www.yuque.com/thyname/dart.ui/imagedescriptor) API 的一个便捷封装，建议直接使用 [ImageDescriptor](https://www.yuque.com/thyname/dart.ui/imagedescriptor)，因为它允许调用方更好地决定如何以及是否使用 `targetWidth` 和 `targetHeight` 参数。

[buffer] 参数为二进制图像数据（例如 PNG 或 GIF 的二进制数据）。数据可以是静态图像或动画图像。支持以下图像格式：{@macro dart.ui.imageFormats}

一旦创建了 codec，此方法将释放 [buffer]，因此调用方在调用此方法时必须放弃对 [buffer] 的所有权。

[targetWidth] 和 [targetHeight] 参数以图像像素为单位指定输出图像的大小。如果它们与图像的固有尺寸不相等，则图像会在解码后进行缩放。如果 `allowUpscaling` 参数未设置为 true，则即使只有一个维度会超出图像的固有尺寸，两个维度也都会被限定在图像的固有尺寸以内。如果这两个参数中恰好只指定了一个，则会在强制图像匹配另一个给定维度的同时保持宽高比。如果两者均未指定，则图像会保持其固有大小。

通常应避免将图像缩放到大于其固有大小，因为这会导致图像占用比必要更多的内存。建议改为缩放 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 变换。如果必须放大图像，则必须将 `allowUpscaling` 参数设置为 true。

如果图像解码失败，返回的 Future 可能以错误完成。

# instantiateImageCodecWithSize()

```dart
Future<Codec> instantiateImageCodecWithSize(ImmutableBuffer buffer, {TargetImageSizeCallback? getTargetSize})
```

实例化一个图像 [Codec](https://www.yuque.com/thyname/dart.ui/codec)。

此方法是对 [ImageDescriptor](https://www.yuque.com/thyname/dart.ui/imagedescriptor) API 的一个便捷封装。

[buffer] 参数为二进制图像数据（例如 PNG 或 GIF 的二进制数据）。数据可以是静态图像或动画图像。支持以下图像格式：{@macro dart.ui.imageFormats}

一旦创建了 codec，此方法将释放 [buffer]，因此调用方在调用此方法时必须放弃对 [buffer] 的所有权。

如果指定了 [getTargetSize] 参数，将会调用它并传入图像的固有大小，以确定解码图像所使用的大小。它返回的大小的宽度和高度必须为大于等于 1 的正值，或为 null。可以只返回指定了 `width` 和 `height` 之一、另一个保留为 null 的 [TargetImageSize](https://www.yuque.com/thyname/dart.ui/targetimagesize)，此时被省略的维度将按原始尺寸的宽高比进行缩放。当两者均为 null 或省略时，图像将以其原始分辨率解码（如果省略 [getTargetSize] 参数，情况也是如此）。

通常应避免将图像缩放到大于其固有大小，因为这会导致图像占用比必要更多的内存。建议改为缩放 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 变换。

如果图像解码失败，返回的 Future 可能以错误完成。

# TargetImageSizeCallback

```dart
typedef TargetImageSizeCallback = TargetImageSize Function(int intrinsicWidth, int intrinsicHeight)
```

用于根据图像的固有大小确定应将其解码为何种大小的回调签名。

另请参阅：

- [instantiateImageCodecWithSize](https://www.yuque.com/thyname/dart.ui/instantiateimagecodecwithsize)：其 `getTargetSize` 参数使用了此签名。

# TargetImageSize

```dart
class TargetImageSize {}
```

图像应被解码成的目标大小的规格说明。

另请参阅：

- [TargetImageSizeCallback](https://www.yuque.com/thyname/dart.ui/targetimagesizecallback)：当被 [instantiateImageCodecWithSize](https://www.yuque.com/thyname/dart.ui/instantiateimagecodecwithsize) 等图像解码方法调用时，返回此类实例的回调。

### TargetImageSize()

```dart
TargetImageSize({int? width, int? height})
```

创建此类的一个新实例。

`width` 和 `height` 可以同时为 null，但如果它们非 null，则必须为正值。

### width

```dart
int? width
```

图像应加载到的宽度。

如果此值非 null，图像将被解码为指定的宽度。如果此值为 null 且 [height] 也为 null，图像将被解码为其固有大小。如果此值为 null 而 [height] 非 null，图像将被解码为一个在保持其固有宽高比的同时符合 [height] 值的宽度。

如果此值非 null，则必须为正值。

### height

```dart
int? height
```

图像应加载到的高度。

如果此值非 null，图像将被解码为指定的高度。如果此值为 null 且 [width] 也为 null，图像将被解码为其固有大小。如果此值为 null 而 [width] 非 null，图像将被解码为一个在保持其固有宽高比的同时符合 [width] 值的高度。

如果此值非 null，则必须为正值。

### toString()

```dart
String toString()
```

# decodeImageFromList()

```dart
void decodeImageFromList(Uint8List list, ImageDecoderCallback callback)
```

从字节数组中加载单个图像帧到 [Image](https://www.yuque.com/thyname/dart.ui/image) 对象中。

这是对 [instantiateImageCodec](https://www.yuque.com/thyname/dart.ui/instantiateimagecodec) 的便捷封装。建议优先使用 [instantiateImageCodec](https://www.yuque.com/thyname/dart.ui/instantiateimagecodec)，它还支持多帧图像并提供更好的错误处理。此函数会吞掉异步错误。

# decodeImageFromPixels()

```dart
void decodeImageFromPixels(Uint8List pixels, int width, int height, PixelFormat format, ImageDecoderCallback callback, {int? rowBytes, int? targetWidth, int? targetHeight, bool allowUpscaling = true, TargetPixelFormat targetFormat = TargetPixelFormat.dontCare})
```

将像素值数组转换为 [Image](https://www.yuque.com/thyname/dart.ui/image) 对象。

`pixels` 参数为像素数据。它们按照 `format` 描述的顺序打包为字节，然后按行分组，从左到右、从上到下排列。

`rowBytes` 参数为数据缓冲区中每行像素所占用的字节数。如果未指定，默认为 `width` 乘以 `format` 中每像素的字节数。

`targetWidth` 和 `targetHeight` 参数以图像像素为单位指定输出图像的大小。如果它们与图像的固有尺寸不相等，则图像会在解码后进行缩放。如果 `allowUpscaling` 参数未设置为 true，则即使只有一个维度会超出图像的固有尺寸，两个维度也都会被限定在图像的固有尺寸以内。如果这两个参数中恰好只指定了一个，则会在强制图像匹配另一个给定维度的同时保持宽高比。如果两者均未指定，则图像会保持其固有大小。

通常应避免将图像缩放到大于其固有大小，因为这会导致图像占用比必要更多的内存。建议改为缩放 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 变换。如果必须放大图像，则必须将 `allowUpscaling` 参数设置为 true。

# decodeImageFromPixelsSync()

```dart
Image decodeImageFromPixelsSync(Uint8List pixels, int width, int height, PixelFormat format)
```

将给定的 [pixels] 同步解码为 [Image](https://www.yuque.com/thyname/dart.ui/image)。

[pixels] 应为 [format] 指定的格式。

[width] 和 [height] 参数指定图像的尺寸。

此函数会立即返回一个 [Image](https://www.yuque.com/thyname/dart.ui/image)。该图像此时可能尚未完全解码，但已经可以绘制到 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 上。

# PathFillType

```dart
enum PathFillType {}
```

决定如何计算 [Path](https://www.yuque.com/thyname/dart.ui/path) 内部区域的环绕规则。

此枚举由 [Path.fillType] 属性使用。

内部区域由带符号边缘穿越次数的非零总和定义。

对于给定的点，如果从该点向无穷远处画一条直线，其穿越顺时针方向环绕该点的线的次数与穿越逆时针方向环绕该点的线的次数不同，则认为该点位于路径内部。

参见：<https://en.wikipedia.org/wiki/Nonzero-rule>

内部区域由奇数次边缘穿越定义。

对于给定的点，如果从该点向无穷远处画一条直线，穿越了奇数条线，则认为该点位于路径内部。

参见：<https://en.wikipedia.org/wiki/Even-odd_rule>

# PathOperation

```dart
enum PathOperation {}
```

组合路径的策略。

另请参阅：

- [Path.combine]：使用此枚举决定如何组合两条路径。

从第一条路径中减去第二条路径。

例如，如果两条路径是直径相同但中心不同的两个重叠圆，结果将是第一个圆中未被第二个圆重叠的新月形部分。

另请参阅：

- [reverseDifference]：操作相同，但是从第二条路径中减去第一条路径。

创建一条新路径，为两条路径的交集，保留路径重叠的部分。

例如，如果两条路径是直径相同但中心不同的两个重叠圆，结果将只是两个圆重叠的部分。

另请参阅：

- [xor]：此操作的逆操作。

创建一条新路径，为两条路径的并集（取或）。

例如，如果两条路径是直径相同但中心不同的两个重叠圆，结果将是一个类似 8 字形的形状，匹配两个圆的外边界。

创建一条新路径，为两条路径的异或（exclusive-or），保留除重叠部分之外的所有内容。

例如，如果两条路径是直径相同但中心不同的两个重叠圆，结果将是类似 8 字形的形状，但不含重叠部分。

另请参阅：

- [intersect]：此操作的逆操作。

从第二条路径中减去第一条路径。

例如，如果两条路径是直径相同但中心不同的两个重叠圆，结果将是第二个圆中未被第一个圆重叠的新月形部分。

另请参阅：

- [difference]：操作相同，但是从第一条路径中减去第二条路径。

# EngineLayer

```dart
abstract class EngineLayer {}
```

供框架跨帧持有和保留引擎图层的句柄。

### dispose()

```dart
void dispose()
```

释放此对象使用的资源。调用此方法后，该对象将不再可用。

EngineLayer 会间接保留特定于平台的图形资源。其中一些资源（例如图像）可能占用大量内存。对于不再使用的 EngineLayer 对象，应尽快释放，以避免在下一次垃圾回收之前一直保留这些资源。

一旦此 EngineLayer 被释放，它将不再适合用作保留图层，并且不得作为 `oldLayer` 传递给任何接受该参数的 [SceneBuilder](https://www.yuque.com/thyname/dart.ui/scenebuilder) 方法。

此方法不能是叶子调用（leaf call），因为该原生函数会调用 Dart API（Dart_SetNativeInstanceField）。

# Path

```dart
abstract class Path {}
```

一个平面上的复杂一维子集。

路径由若干子路径和一个*当前点*组成。

子路径由不同类型的线段组成，如直线、圆弧或贝塞尔曲线。子路径可以是开放的或闭合的，并且可以自相交。

闭合的子路径根据当前的 [fillType] 围合平面上的一个（可能不连续的）区域。

*当前点*的初始位置在原点。每次向子路径添加一个线段的操作之后，当前点都会更新为该线段的终点。

路径可以使用 [Canvas.drawPath] 绘制在画布上，也可以用于通过 [Canvas.clipPath] 创建裁剪区域。

### Path()

```dart
Path()
```

### Path.from()

```dart
Path.from(Path source)
```

创建另一个 [Path](https://www.yuque.com/thyname/dart.ui/path) 的副本。

此复制操作速度很快，除非 `source` 路径或此构造函数返回的路径被修改，否则不会占用额外内存。

### fillType

```dart
PathFillType get fillType
```

决定如何计算此路径内部区域的填充方式。

默认为非零环绕规则 [PathFillType.nonZero]。

### fillType

```dart
set fillType(PathFillType value)
```

### moveTo()

```dart
void moveTo(double x, double y)
```

在给定坐标处开始一个新的子路径。

### relativeMoveTo()

```dart
void relativeMoveTo(double dx, double dy)
```

在相对于当前点的给定偏移处开始一个新的子路径。

### lineTo()

```dart
void lineTo(double x, double y)
```

添加一条从当前点到给定点的直线段。

### relativeLineTo()

```dart
void relativeLineTo(double dx, double dy)
```

添加一条从当前点到相对于当前点的给定偏移点的直线段。

### quadraticBezierTo()

```dart
void quadraticBezierTo(double x1, double y1, double x2, double y2)
```

添加一条从当前点弯曲到给定点 (x2,y2) 的二次贝塞尔曲线段，使用控制点 (x1,y1)。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_quadratic_to.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_quadratic_to_dark.png#gh-dark-mode-only)

### relativeQuadraticBezierTo()

```dart
void relativeQuadraticBezierTo(double x1, double y1, double x2, double y2)
```

添加一条从当前点弯曲到相对于当前点的偏移点 (x2,y2) 的二次贝塞尔曲线段，使用相对于当前点的偏移控制点 (x1,y1)。

### cubicTo()

```dart
void cubicTo(double x1, double y1, double x2, double y2, double x3, double y3)
```

添加一条从当前点弯曲到给定点 (x3,y3) 的三次贝塞尔曲线段，使用控制点 (x1,y1) 和 (x2,y2)。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_cubic_to.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_cubic_to_dark.png#gh-dark-mode-only)

### relativeCubicTo()

```dart
void relativeCubicTo(double x1, double y1, double x2, double y2, double x3, double y3)
```

添加一条从当前点弯曲到相对于当前点的偏移点 (x3,y3) 的三次贝塞尔曲线段，使用相对于当前点的偏移控制点 (x1,y1) 和 (x2,y2)。

### conicTo()

```dart
void conicTo(double x1, double y1, double x2, double y2, double w)
```

添加一条从当前点弯曲到给定点 (x2,y2) 的贝塞尔曲线段，使用控制点 (x1,y1) 和权重 w。如果权重大于 1，则曲线为双曲线；如果权重等于 1，则为抛物线；如果权重小于 1，则为椭圆。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_conic_to.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_conic_to_dark.png#gh-dark-mode-only)

### relativeConicTo()

```dart
void relativeConicTo(double x1, double y1, double x2, double y2, double w)
```

添加一条从当前点弯曲到相对于当前点的偏移点 (x2,y2) 的贝塞尔曲线段，使用相对于当前点的偏移控制点 (x1,y1) 和权重 w。如果权重大于 1，则曲线为双曲线；如果权重等于 1，则为抛物线；如果权重小于 1，则为椭圆。

### arcTo()

```dart
void arcTo(Rect rect, double startAngle, double sweepAngle, bool forceMoveTo)
```

如果 `forceMoveTo` 参数为 false，则添加一条直线段和一段圆弧。

如果 `forceMoveTo` 参数为 true，则开始一个由圆弧组成的新子路径。

无论哪种情况，该圆弧线段都沿着由给定矩形所限定的椭圆边缘，从椭圆上 startAngle 弧度处延伸到 startAngle + sweepAngle 弧度处，其中零弧度是椭圆右侧与经过矩形中心的水平线相交的点，正角度沿椭圆顺时针方向增加。

如果 `forceMoveTo` 为 false，添加的直线段从当前点开始，到圆弧的起点结束。请注意，如果 [sweepAngle] 是 $2\pi$ 的倍数（例如 $2\pi$、$4\pi$），此方法不会绘制任何内容。如果需要绘制一个完整的圆或重叠的圆弧，可使用 [addArc] 作为替代方案。

### arcToPoint()

```dart
void arcToPoint(Offset arcEnd, {Radius radius = Radius.zero, double rotation = 0.0, bool largeArc = false, bool clockwise = true})
```

最多附加四条经过加权的圆锥曲线，以描绘一个具有 `radius` 半径并旋转 `rotation`（以度为单位，顺时针方向）的椭圆。

第一条曲线从路径中的最后一个点开始，最后一条曲线在 `arcEnd` 处结束。这些曲线沿着由 `clockwise` 和 `largeArc` 决定的方向延伸，且扫描角始终小于 360 度。

如果两个半径均为零，或者路径中的最后一个点即为 `arcEnd`，则会添加一条简单的直线。如果两个半径都大于零但太小而无法描述圆弧，则会缩放半径以适应路径中的最后一个点。

### relativeArcToPoint()

```dart
void relativeArcToPoint(Offset arcEndDelta, {Radius radius = Radius.zero, double rotation = 0.0, bool largeArc = false, bool clockwise = true})
```

最多附加四条经过加权的圆锥曲线，以描绘一个具有 `radius` 半径并旋转 `rotation`（以度为单位，顺时针方向）的椭圆。

路径中的最后一个点用 (px, py) 表示。

第一条曲线从路径中的最后一个点开始，最后一条曲线在 `arcEndDelta.dx + px` 和 `arcEndDelta.dy + py` 处结束。这些曲线沿着由 `clockwise` 和 `largeArc` 决定的方向延伸，且扫描角始终小于 360 度。

如果任一半径为零，或者 `arcEndDelta.dx` 和 `arcEndDelta.dy` 都为零，则会添加一条简单的直线。如果两个半径都大于零但太小而无法描述圆弧，则会缩放半径以适应路径中的最后一个点。

### addRect()

```dart
void addRect(Rect rect)
```

添加一个由四条线组成的新子路径，勾勒出给定矩形的轮廓。

### addOval()

```dart
void addOval(Rect oval)
```

添加一个新子路径，该子路径由一条填满给定矩形的椭圆曲线组成。

要添加一个圆形，可传入合适的矩形作为 `oval`。可以使用 [Rect.fromCircle] 方便地根据圆心 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 和半径来描述圆形。

### addArc()

```dart
void addArc(Rect oval, double startAngle, double sweepAngle)
```

添加一个仅含一段圆弧的新子路径，该圆弧沿着由给定矩形所限定的椭圆边缘，从椭圆上 startAngle 弧度处延伸到 startAngle + sweepAngle 弧度处，其中零弧度是椭圆右侧与经过矩形中心的水平线相交的点，正角度沿椭圆顺时针方向增加。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_add_arc.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_add_arc_dark.png#gh-dark-mode-only)

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_add_arc_ccw.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/path_add_arc_ccw_dark.png#gh-dark-mode-only)

### addPolygon()

```dart
void addPolygon(List<Offset> points, bool close)
```

添加一个由一系列连接给定点的线段组成的新子路径。

如果 `close` 为 true，会额外添加一条连接最后一个点和第一个点的线段。

`points` 参数被解释为相对于原点的偏移量。

### addRRect()

```dart
void addRRect(RRect rrect)
```

添加一个由描述该参数所指定的圆角矩形所需的直线和曲线组成的新子路径。

### addRSuperellipse()

```dart
void addRSuperellipse(RSuperellipse rsuperellipse)
```

添加一个由描述该参数所指定的圆角超椭圆所需的曲线组成的新子路径。

### addPath()

```dart
void addPath(Path path, Offset offset, {Float64List? matrix4})
```

将 `path` 的各个子路径按 `offset` 偏移后添加到此路径中。

如果指定了 `matrix4`，路径会先按给定偏移量平移，再应用此矩阵进行变换。该矩阵是以列主序存储的 4x4 矩阵。

### extendWithPath()

```dart
void extendWithPath(Path path, Offset offset, {Float64List? matrix4})
```

将 `path` 的各个子路径按 `offset` 偏移后添加到此路径中。当前子路径会被扩展，并与 `path` 的第一个子路径相连，必要时通过 lineTo 进行连接。

如果指定了 `matrix4`，路径会先按给定的 `offset` 偏移量平移，再应用此矩阵进行变换。该矩阵是以列主序存储的 4x4 矩阵。

### close()

```dart
void close()
```

关闭最后一个子路径，效果相当于从当前点向该子路径的第一个点绘制一条直线。

### reset()

```dart
void reset()
```

清除 [Path](https://www.yuque.com/thyname/dart.ui/path) 对象中的所有子路径，使其恢复到创建时的初始状态。*当前点*会被重置为原点。

### contains()

```dart
bool contains(Offset point)
```

测试给定的点是否在路径内（即，如果该路径被用于 [Canvas.clipPath]，该点是否会位于可见部分内）。

`point` 参数被解释为相对于原点的偏移量。

如果该点在路径内，则返回 true，否则返回 false。

### shift()

```dart
Path shift(Offset offset)
```

返回此路径的一个副本，其中每个子路径的所有线段均按给定偏移量平移。

### transform()

```dart
Path transform(Float64List matrix4)
```

返回此路径的一个副本，其中每个子路径的所有线段均按给定矩阵进行变换。

### getBounds()

```dart
Rect getBounds()
```

计算此路径的边界矩形。

仅包含位于同一直线上的轴对齐点的路径将没有面积，因此 `Rect.isEmpty` 对于这样的路径将返回 true。可以考虑改用 `rect.width + rect.height > 0.0` 进行检查，或使用 [computeMetrics] API 来检查路径长度。

对于许多更复杂的路径，边界可能并不精确。例如，当路径包含一个圆形时，用于计算边界的点是该圆形隐含的控制点，这些点构成了围绕圆形的一个正方形；如果对该圆形应用了 [transform] 变换，那么这个正方形会被旋转，因此（轴对齐、未旋转的）边界框最终会严重高估圆形实际覆盖的面积。

### combine()

```dart
Path combine(PathOperation operation, Path path1, Path path2)
```

根据给定的 `operation` 所指定的方式合并两条路径。

生成的路径将由互不重叠的轮廓构成。曲线阶数会尽可能降低，以便三次曲线可以转换为二次曲线，二次曲线可以转换为直线。

### computeMetrics()

```dart
PathMetrics computeMetrics({bool forceClosed = false})
```

为此路径创建一个 [PathMetrics](https://www.yuque.com/thyname/dart.ui/pathmetrics) 对象，用于描述路径各轮廓的各种属性。

一个 [Path](https://www.yuque.com/thyname/dart.ui/path) 由零个或多个轮廓组成。轮廓由相连的曲线和线段组成，可通过 [lineTo]、[cubicTo]、[arcTo]、[quadraticBezierTo] 等方法及其相对版本创建，也可以通过 addRect 等 add\* 方法创建。创建新的 [Path](https://www.yuque.com/thyname/dart.ui/path) 时，一旦有任何绘制指令便会开始一个新的轮廓，并且每个 [moveTo] 指令都会开始另一个新的轮廓。

[PathMetric](https://www.yuque.com/thyname/dart.ui/pathmetric) 对象描述单个轮廓的属性，例如其长度、是否闭合、沿路径某一偏移处的切线向量等。它还提供了一个用于创建子路径的方法：[PathMetric.extractPath]。

计算 [PathMetric](https://www.yuque.com/thyname/dart.ui/pathmetric) 对象并非易事。此方法返回的 [PathMetrics](https://www.yuque.com/thyname/dart.ui/pathmetrics) 对象是一个惰性 [Iterable](https://www.yuque.com/thyname/dart.core/iterable)，这意味着只有在迭代器移动到下一个 [PathMetric](https://www.yuque.com/thyname/dart.ui/pathmetric) 时才会执行计算。需要多次遍历该可迭代对象的调用者可以简单地对此方法的结果使用 [Iterable.toList] 来实现记忆化。特别是，希望了解路径中包含多少轮廓的调用者应存储 `path.computeMetrics().length` 的结果，或者使用 `path.computeMetrics().toList()`，这样便可以反复检查长度，因为调用 `Iterable.length` 会导致遍历整个可迭代对象。

需要特别说明的是，调用者应知悉 [PathMetrics.length] 是轮廓的数量，**而非路径的长度**。要获取路径中某个轮廓的长度，请使用 [PathMetric.length]。

零长度的轮廓（即起点和终点相同，例如 `Path()..lineTo(0, 0)`）不会包含在返回的 [PathMetrics](https://www.yuque.com/thyname/dart.ui/pathmetrics) 中。只有长度为正的轮廓才会有对应的 [PathMetric](https://www.yuque.com/thyname/dart.ui/pathmetric)。

如果 `forceClosed` 设置为 true，即使路径的各轮廓未被显式闭合，也会被当作已闭合状态进行度量计算。

# Tangent

```dart
class Tangent {}
```

切线的几何描述：某一点处的角度。

另请参阅：

- [PathMetric.getTangentForOffset]，返回路径上某一偏移处的切线。

### Tangent()

```dart
Tangent(Offset position, Offset vector)
```

使用给定的值创建一个 [Tangent](https://www.yuque.com/thyname/dart.ui/tangent)。

参数不得为 null。

### Tangent.fromAngle()

```dart
Tangent.fromAngle(Offset position, double angle)
```

根据角度（而非向量）创建一个 [Tangent](https://www.yuque.com/thyname/dart.ui/tangent)。

[vector] 的计算方式为给定角度处的单位向量，该角度被解释为从 x 轴起沿顺时针方向计量的弧度。

### position

```dart
Offset position
```

切线的位置。

当与 [PathMetric.getTangentForOffset] 一起使用时，此值表示沿路径给定偏移所对应的精确位置。

### vector

```dart
Offset vector
```

[position] 处曲线的向量。

当与 [PathMetric.getTangentForOffset] 一起使用时，这是位于路径上给定偏移处的曲线向量（即 [position] 处曲线的方向）。

### angle

```dart
double get angle
```

[position] 处曲线的方向。

当与 [PathMetric.getTangentForOffset] 一起使用时，这是位于路径上给定偏移处的曲线角度（即 [position] 处曲线的方向）。

此值以弧度为单位，0.0 表示沿 x 轴正方向，正数表示朝向 y 轴负方向（即顺时针方向），负数表示朝向 y 轴正方向（即逆时针方向）。

# PathMetrics

```dart
class PathMetrics extends collection.IterableBase<PathMetric> {}
```

描述 [Path](https://www.yuque.com/thyname/dart.ui/path) 的 [PathMetric](https://www.yuque.com/thyname/dart.ui/pathmetric) 对象的可迭代集合。

[PathMetrics](https://www.yuque.com/thyname/dart.ui/pathmetrics) 对象通过 [Path.computeMetrics] 方法创建，表示调用时刻的路径状态。路径的后续修改不会影响该 [PathMetrics](https://www.yuque.com/thyname/dart.ui/pathmetrics) 对象。

每个路径度量对应路径的一个片段或轮廓。

例如，一条由 [Path.lineTo]、[Path.moveTo] 以及另一个 [Path.lineTo] 组成的路径将包含两个轮廓，因此由两个 [PathMetric](https://www.yuque.com/thyname/dart.ui/pathmetric) 对象表示。

此可迭代对象不进行记忆化。需要多次遍历列表或需要随机访问列表元素的调用者应对该对象使用 [toList]。

### iterator

```dart
Iterator<PathMetric> get iterator
```

# PathMetricIterator

```dart
class PathMetricIterator implements Iterator<PathMetric> {}
```

由 [PathMetrics](https://www.yuque.com/thyname/dart.ui/pathmetrics) 用于跟踪从路径的一个片段迭代到下一个片段以进行度量。

### current

```dart
PathMetric get current
```

### moveNext()

```dart
bool moveNext()
```

# PathMetric

```dart
class PathMetric {}
```

用于度量 [Path](https://www.yuque.com/thyname/dart.ui/path) 并提取子路径的实用工具。

对 [Path.computeMetrics] 返回的对象进行迭代以获取 [PathMetric](https://www.yuque.com/thyname/dart.ui/pathmetric) 对象。希望随机访问元素或多次迭代的调用者应使用 `path.computeMetrics().toList()`，因为 [PathMetrics](https://www.yuque.com/thyname/dart.ui/pathmetrics) 不进行记忆化。

一旦创建，度量结果仅对调用 [Path.computeMetrics] 时指定的路径状态有效。如果添加了额外的轮廓或任何轮廓被更新，则需要重新计算度量结果。先前创建的度量结果仍将指向计算时路径的快照，而不会反映路径新变化后的实际度量结果。

### length

```dart
double length
```

返回当前轮廓的总长度。

该长度可能是根据原始添加的几何图形的近似值计算得出的。因此，不建议依赖此属性来获取常见形状在数学上精确的长度。

### isClosed

```dart
bool isClosed
```

该轮廓是否闭合。

如果轮廓以对 [Path.close] 的调用结束（使用 [Path.addRect] 等方法时可能隐含此调用），或者在调用 [Path.computeMetrics] 时将 `forceClosed` 指定为 true，则返回 true。否则返回 false。

### contourIndex

```dart
int contourIndex
```

轮廓从零开始的索引。

[Path](https://www.yuque.com/thyname/dart.ui/path) 对象由零个或多个轮廓组成。一旦发出绘制指令（例如 [Path.lineTo]），便会创建第一个轮廓。绘制指令之后的 [Path.moveTo] 指令可能会创建一个新轮廓，但如果应用了某些优化，判定该移动指令实际上并未导致画笔移动，则可能不会创建新轮廓。

此属性仅在参照其原始迭代器以及计算路径度量时路径的轮廓时才有效。如果之后添加了额外的轮廓或更新了现有轮廓，则此度量对于路径的当前状态将无效。

### getTangentForOffset()

```dart
Tangent? getTangentForOffset(double distance)
```

计算当前轮廓在给定偏移处的位置，以及路径在该点处的角度。

例如，对于一条从 0.0,0.0 到 2.0,2.0 的直线，以偏移量 1.41 调用此方法将得到点 1.0,1.0 以及 45 度的角度（但以弧度表示）。

如果轮廓的 [length] 为零，则返回 null。

偏移量会被限制在当前轮廓的 [length] 范围内。

### extractPath()

```dart
Path extractPath(double start, double end, {bool startWithMoveTo = true})
```

给定起始和结束的偏移量，返回其间的线段。

`start` 和 `end` 会被限制在合法值范围内（0..[length]）。如果 `startWithMoveTo` 为 true，则该线段以 moveTo 开始。

### toString()

```dart
String toString()
```

# BlurStyle

```dart
enum BlurStyle {}
```

用于 [MaskFilter](https://www.yuque.com/thyname/dart.ui/maskfilter) 对象中模糊效果的样式。

内外皆模糊。这对于绘制相对于其表面上正在投射阴影的形状发生了偏移的阴影非常有用。

内部实心，外部模糊。这相当于绘制该形状，并额外绘制模糊效果。这可以使物体看起来更明亮，甚至类似于发出荧光。

内部无效果，外部模糊。这对于绘制部分透明形状的阴影非常有用，此时阴影是单独绘制且没有偏移的，因此阴影不会绘制在形状下方。

内部模糊，外部无效果。这可以使形状看起来像是由内而外被照亮。

# MaskFilter

```dart
class MaskFilter {}
```

在绘制形状时应用的蒙版滤镜。蒙版滤镜是一个函数，它接收一个彩色像素位图，并返回另一个彩色像素位图。

此类的实例与 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 对象上的 [Paint.maskFilter] 一起使用。

### MaskFilter.blur()

```dart
MaskFilter.blur(BlurStyle _style, double _sigma)
```

创建一个蒙版滤镜，对正在绘制的形状进行模糊处理。

这通常用于近似模拟阴影。

`style` 参数控制要绘制的效果类型；请参阅 [BlurStyle](https://www.yuque.com/thyname/dart.ui/blurstyle)。

`sigma` 参数控制效果的大小。它是所应用高斯模糊的标准差。该值必须大于零。sigma 大致对应于效果半径（以像素为单位）的一半。

模糊是一项昂贵的操作，因此应谨慎使用。

参数不得为 null。

另请参阅：

- [Canvas.drawShadow]，这是一种更高效的绘制阴影的方法。

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

# ColorFilter

```dart
class ColorFilter implements ImageFilter {}
```

在使用特定 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 绘制形状或合成图层时应用的颜色滤镜的描述。颜色滤镜是一个函数，它接收两种颜色，并输出一种颜色。在合成期间应用时，会在将整个图层与目标合并之前，独立地应用于正在绘制图层的每个像素。

此类的实例与 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 对象上的 [Paint.colorFilter] 一起使用。

### ColorFilter.mode()

```dart
ColorFilter.mode(Color color, BlendMode blendMode)
```

创建一个应用第二个参数所给出的混合模式的颜色滤镜。源颜色为第一个参数所给出的颜色，目标颜色为正在合成的图层的颜色。

然后，此滤镜的输出会根据 [Paint.blendMode]，以此滤镜的输出作为源、以背景作为目标合成到背景中。

### ColorFilter.matrix()

```dart
ColorFilter.matrix(List<double> matrix)
```

根据一个 4x5 的行主序矩阵构造颜色滤镜。该矩阵被解释为一个 5x5 矩阵，其中第五行为单位矩阵配置。

每个像素的颜色值（表示为 `[R, G, B, A]`）会通过矩阵乘法生成一个新的颜色：

| R' | | a00 a01 a02 a03 a04 | | R | | G' | | a10 a11 a12 a13 a14 | | G | | B' | = | a20 a21 a22 a23 a24 | \* | B | | A' | | a30 a31 a32 a33 a34 | | A | | 1 | | 0 0 0 0 1 | | 1 |

该矩阵为行主序，且平移列以未归一化的 0...255 空间表示。例如，单位矩阵为：

```dart
const ColorFilter identity = ColorFilter.matrix(<double>[
  1, 0, 0, 0, 0,
  0, 1, 0, 0, 0,
  0, 0, 1, 0, 0,
  0, 0, 0, 1, 0,
]);
```

## 示例

一个反色的颜色矩阵：

```dart
const ColorFilter invert = ColorFilter.matrix(<double>[
  -1,  0,  0, 0, 255,
   0, -1,  0, 0, 255,
   0,  0, -1, 0, 255,
   0,  0,  0, 1,   0,
]);
```

一个棕褐色调的颜色矩阵（数值基于 [Filter Effects 规范](https://www.w3.org/TR/filter-effects-1/#sepiaEquivalent)）：

```dart
const ColorFilter sepia = ColorFilter.matrix(<double>[
  0.393, 0.769, 0.189, 0, 0,
  0.349, 0.686, 0.168, 0, 0,
  0.272, 0.534, 0.131, 0, 0,
  0,     0,     0,     1, 0,
]);
```

一个灰度颜色滤镜（数值基于 [Filter Effects 规范](https://www.w3.org/TR/filter-effects-1/#grayscaleEquivalent)）：

```dart
const ColorFilter greyscale = ColorFilter.matrix(<double>[
  0.2126, 0.7152, 0.0722, 0, 0,
  0.2126, 0.7152, 0.0722, 0, 0,
  0.2126, 0.7152, 0.0722, 0, 0,
  0,      0,      0,      1, 0,
]);
```

### ColorFilter.linearToSrgbGamma()

```dart
ColorFilter.linearToSrgbGamma()
```

构造一个对 RGB 通道应用 sRGB 伽马曲线的颜色滤镜。

### ColorFilter.srgbToLinearGamma()

```dart
ColorFilter.srgbToLinearGamma()
```

创建一个对 RGB 通道应用 sRGB 伽马曲线之逆运算的颜色滤镜。

### ColorFilter.saturation()

```dart
ColorFilter.saturation(double saturation)
```

创建一个对 RGB 通道应用给定饱和度的颜色滤镜。

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### debugShortDescription

```dart
String get debugShortDescription
```

### toString()

```dart
String toString()
```

# ImageFilter

```dart
abstract class ImageFilter {}
```

应用于光栅图像的滤镜操作。

另请参阅：

- [BackdropFilter](https://www.yuque.com/thyname/flutter.widgets/backdropfilter)，一个将 [ImageFilter](https://www.yuque.com/thyname/dart.ui/imagefilter) 应用于其渲染内容的 Widget。
- [ClipRect](https://www.yuque.com/thyname/flutter.widgets/cliprect)，一个在与 [BackdropFilter](https://www.yuque.com/thyname/flutter.widgets/backdropfilter) 一起使用时限制 [ImageFilter](https://www.yuque.com/thyname/dart.ui/imagefilter) 影响区域的 Widget。
- [ImageFiltered](https://www.yuque.com/thyname/flutter.widgets/imagefiltered)，一个将 [ImageFilter](https://www.yuque.com/thyname/dart.ui/imagefilter) 应用于其子组件的 Widget。
- [SceneBuilder.pushBackdropFilter]，将此类用作背景滤镜的底层 API。
- [SceneBuilder.pushImageFilter]，将此类用作子图层滤镜的底层 API。

### ImageFilter.blur()

```dart
ImageFilter.blur({double sigmaX = 0.0, double sigmaY = 0.0, TileMode? tileMode, Rect? bounds})
```

创建一个应用高斯模糊的图像滤镜。

`sigma_x` 和 `sigma_y` 分别是 X 方向和 Y 方向上高斯核的标准差。

`tile_mode` 定义了在执行标准的无边界模糊时，对边缘像素进行采样的行为。

`bounds` 参数是可选的，用于启用"有边界模糊"模式。当 `bounds` 非空时，图像滤镜会将其在指定边界矩形之外读取的任何采样替换为透明黑色。然后，最终的加权和会除以非透明采样的总权重（有效 alpha 值），从而得到不透明的输出。

有边界模式可以防止相邻内容的颜色渗入模糊区域，通常用于模糊效果必须被严格限制在裁剪区域内的场景，例如 iOS 风格的毛玻璃效果。

`bounds` 矩形以画布当前坐标空间指定，并受当前变换的影响；因此，在最终的画布坐标中，该边界可能不是轴对齐的。

### ImageFilter.dilate()

```dart
ImageFilter.dilate({double radiusX = 0.0, double radiusY = 0.0})
```

创建一个图像滤镜，将每个输入像素的通道值膨胀为沿 x 轴和 y 轴给定半径范围内的最大值。

### ImageFilter.erode()

```dart
ImageFilter.erode({double radiusX = 0.0, double radiusY = 0.0})
```

创建一个滤镜，将每个输入像素的通道值腐蚀为沿 x 轴和 y 轴给定半径范围内的最小通道值。

### ImageFilter.matrix()

```dart
ImageFilter.matrix(Float64List matrix4, {FilterQuality filterQuality = FilterQuality.medium})
```

创建一个应用矩阵变换的图像滤镜。

例如，在与 [BackdropFilter](https://www.yuque.com/thyname/flutter.widgets/backdropfilter) 一起使用时应用一个正的缩放矩阵（参见 [Matrix4.diagonal3]）将放大背景图像。

### ImageFilter.compose()

```dart
ImageFilter.compose({required ImageFilter outer, required ImageFilter inner})
```

将 `inner` 滤镜与 `outer` 组合，以结合它们的效果。

创建一个单一的 [ImageFilter](https://www.yuque.com/thyname/dart.ui/imagefilter)，应用该滤镜时，其效果等同于依次应用 `inner` 和 `outer`，即 result = outer(inner(source))。

### ImageFilter.shader()

```dart
ImageFilter.shader(FragmentShader shader)
```

根据 [FragmentShader](https://www.yuque.com/thyname/dart.ui/fragmentshader) 创建一个图像滤镜。

> [!WARNING]
> 此 API 仅在使用 Impeller 渲染引擎时受支持。
> 在其他后端上，将抛出 [UnsupportedError](https://www.yuque.com/thyname/dart.core/unsupportederror)。

> 若要在运行时检查是否支持此 API，请使用 [isShaderFilterSupported]。

用法示例：

```dart
if (ui.ImageFilter.isShaderFilterSupported) {
  // 使用该滤镜……
}
```

此处提供的片段着色器要想被引擎用于滤镜处理，需满足额外要求。第一个 uniform 值必须是 vec2 类型，该值将由引擎设置为所绑定纹理的尺寸。还必须至少有一个 sampler2D 类型的 uniform，其中第一个将由引擎设置为包含滤镜的输入内容。

当 Impeller 使用 OpenGL(ES) 后端时，y 轴方向是反转的。自定义片段着色器必须在 GLES 上反转 y 轴，否则渲染结果将是上下颠倒的。

例如，以下是可与此 API 一起使用的有效片段着色器。请注意，uniform 的名称不要求具有任何特定值。

```glsl
#include <flutter/runtime_effect.glsl>

uniform vec2 u_size;
uniform float u_time;

uniform sampler2D u_texture_input;

out vec4 frag_color;

void main() {
  vec2 uv = FlutterFragCoord().xy / u_size;
// 在 OpenGL 后端反转 y 轴。
#ifdef IMPELLER_TARGET_OPENGLES
  uv.y = 1.0 - uv.y
#endif
  frag_color = texture(u_texture_input, uv) * u_time;

}

```

### isShaderFilterSupported

```dart
bool get isShaderFilterSupported
```

当前后端是否支持 [ImageFilter.shader]。

> [!WARNING]
> 此属性仅在启用 Impeller 渲染引擎时才会返回 true。
> 当此属性为 `false` 时尝试创建 [ImageFilter.shader] 将抛出 [UnsupportedError](https://www.yuque.com/thyname/dart.core/unsupportederror)。

### debugShortDescription

```dart
String get debugShortDescription
```

当滤镜作为使用 [ImageFilter.compose] 创建的复合 [ImageFilter](https://www.yuque.com/thyname/dart.ui/imagefilter) 的一部分时，要显示的描述文本。

# Shader

```dart
base class Shader extends NativeFieldWrapperClass1 {}
```

诸如 [Gradient](https://www.yuque.com/thyname/dart.ui/gradient) 和 [ImageShader](https://www.yuque.com/thyname/dart.ui/imageshader) 之类、与 [Paint.shader] 所使用的着色器相对应的对象的基类。

### debugDisposed

```dart
bool get debugDisposed
```

是否已调用 [dispose]。

这仅应在启用断言时使用。否则将抛出异常。

### dispose()

```dart
void dispose()
```

释放此对象所使用的资源。调用此方法后，该对象将不再可用。

如果此对象所分配的底层内存仍被另一个尚未释放的对象所需要，则该内存将在此调用之后继续保留。例如，一个尚未释放、引用了 [ImageShader](https://www.yuque.com/thyname/dart.ui/imageshader) 的 [Picture](https://www.yuque.com/thyname/dart.ui/picture) 可能会使其底层资源保持存活。

重写此方法的类必须调用 `super.dispose()`。

# TileMode

```dart
enum TileMode {}
```

定义如何处理渐变或图像滤镜的已定义边界之外的区域。

## 对于渐变

渐变通过一些特定的边界来定义，从而创建一个内部区域和一个外部区域，`TileMode` 控制如何确定这些边界之外区域的颜色：

- **线性渐变**：内部区域是两点（在渐变 API 中通常称为 `start` 和 `end`）之间的区域，或更准确地说，是与连接这两点的直线正交的平行线之间的区域。此区域之外的颜色由 `TileMode` 决定。

- **径向渐变**：内部区域是由中心点和半径所定义的圆盘。此圆盘之外的颜色由 `TileMode` 决定。

- **扫描渐变**：内部区域是 `startAngle` 和 `endAngle` 之间的角度扇形。此扇形之外的颜色由 `TileMode` 决定。

## 对于图像滤镜

在应用需要从图像边界之外采样颜色的滤镜（如模糊）时，`TileMode` 定义了如何确定这些边界外采样的方式：

- 它控制当滤镜需要从原始图像边界之外的区域采样时使用的颜色值。
- 这对于图像边缘附近的模糊等效果尤为重要。

另请参阅：

- [painting.Gradient]，[LinearGradient](https://www.yuque.com/thyname/flutter.painting/lineargradient) 和 [RadialGradient](https://www.yuque.com/thyname/flutter.painting/radialgradient) 的父类，被 [BoxDecoration](https://www.yuque.com/thyname/flutter.painting/boxdecoration) 等使用，它以相对坐标工作，并可以按需为特定 [Rect](https://www.yuque.com/thyname/dart.ui/rect) 创建表示渐变的 [Shader](https://www.yuque.com/thyname/dart.ui/shader)。
- [dart:ui.Gradient]，在直接处理 [Paint.shader] 属性时所使用的底层类，具有 [Gradient.linear] 和 [Gradient.radial] 构造函数。
- [dart:ui.ImageFilter.blur]，一种有时需要从图像外部读取采样以与图像边缘附近的像素相结合的图像滤镜。

超出边缘的采样会被限制为内部区域中最接近的颜色。

对于渐变而言，这意味着内部区域之外的区域将被涂上颜色停止点列表中最接近该区域一端的颜色。

特别对于扫描渐变，[startAngle] 和 [endAngle] 所定义的角度扇形之外的整个区域都将被涂上颜色停止点列表中最接近该区域一端的颜色。

图像滤镜会将最近的边缘像素替代为从源图像外部读取的任何采样。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_clamp_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_clamp_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_clamp_sweep.png)

超出边缘的采样会从已定义区域的另一端开始重复。

对于渐变而言，这种方式相当于将 0.0 到 1.0 的停止点重复从 1.0 到 2.0、2.0 到 3.0，依此类推（对于线性渐变，同理从 -1.0 到 0.0、-2.0 到 -1.0 等）。

对于扫描渐变，超出 [endAngle] 或早于 [startAngle] 的角度将沿相同方向（顺时针）重复渐变模式。

图像滤镜会将其源图像视为在其读取所在的放大采样空间内平铺，每个平铺块的方向都与基础图像相同。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_repeated_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_repeated_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_repeated_sweep.png)

超出边缘的采样会在已定义区域内来回镜像。

对于渐变而言，这种方式相当于将 0.0 到 1.0 的停止点先向后重复从 2.0 到 1.0，再向前从 2.0 到 3.0，然后再次向后从 4.0 到 3.0，依此类推（对于线性渐变，在负方向上同理）。

对于扫描渐变，当角度增加超出 [endAngle] 或减小低于 [startAngle] 时，渐变模式会来回镜像。

图像滤镜会将其源图像视为在其读取所在的采样空间内，以交替的前进和后退或向上和向下的方向平铺。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_mirror_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_mirror_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_mirror_sweep.png)

超出边缘的采样会被视为透明黑色。

渐变会在径向渐变圆之外、线性渐变内部区域所定义的平行线之外，或扫描渐变的角度扇形之外的任何区域渲染透明效果。

对于扫描渐变，仅 [startAngle] 和 [endAngle] 之间的扇形会被绘制；所有其他区域均为透明。

图像滤镜会将从源图像外部读取的任何采样替换为透明黑色。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_decal_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_decal_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_decal_sweep.png)

# Gradient

```dart
base class Gradient extends Shader {}
```

渲染颜色渐变的着色器（供 [Paint.shader] 使用）。

有多种类型的渐变，由此类的各个构造函数表示。

另请参阅：

- [Gradient](https://www.yuque.com/thyname/dart.ui/gradient)，[painting](https://www.yuque.com/thyname/flutter.painting) 库中的对应类。

### Gradient.linear()

```dart
Gradient.linear(Offset from, Offset to, List<Color> colors, [List<double>? colorStops, TileMode tileMode = TileMode.clamp, Float64List? matrix4])
```

创建一个从 `from` 到 `to` 的线性渐变。

如果提供了 `colorStops`，则 `colorStops[i]` 是一个 0.0 到 1.0 之间的数字，用于指定 `color[i]` 在渐变中开始的位置。如果未提供 `colorStops`，则默认仅隐含两个停止点，分别位于 0.0 和 1.0 处（因此 `color` 必须只包含两个条目）。小于 0.0 的停止点值将向上舍入为 0.0，大于 1.0 的停止点值将向下舍入为 1.0。每个停止点值都必须大于或等于前一个停止点值。不满足此条件的停止点值将向上舍入为前一个停止点值。

`from` 之前和 `to` 之后的行为由 `tileMode` 参数描述。详情请参阅 [TileMode](https://www.yuque.com/thyname/dart.ui/tilemode) 枚举。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_clamp_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_decal_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_mirror_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_repeated_linear.png)

如果 `from`、`to`、`colors` 或 `tileMode` 为 null，或者 `colors` 或 `colorStops` 包含 null 值，此构造函数将抛出 [NoSuchMethodError](https://www.yuque.com/thyname/dart.core/nosuchmethoderror)。

如果提供了 `matrix4`，渐变填充将相对于本地坐标系按指定的 4x4 矩阵进行变换。`matrix4` 必须是打包成包含 16 个值的列表的列主序矩阵。

### Gradient.radial()

```dart
Gradient.radial(Offset center, double radius, List<Color> colors, [List<double>? colorStops, TileMode tileMode = TileMode.clamp, Float64List? matrix4, Offset? focal, double focalRadius = 0.0])
```

创建一个以 `center` 为中心、在距中心 `radius` 距离处结束的径向渐变。

如果提供了 `colorStops`，则 `colorStops[i]` 是一个 0.0 到 1.0 之间的数字，用于指定 `color[i]` 在渐变中开始的位置。如果未提供 `colorStops`，则默认仅隐含两个停止点，分别位于 0.0 和 1.0 处（因此 `color` 必须只包含两个条目）。小于 0.0 的停止点值将向上舍入为 0.0，大于 1.0 的停止点值将向下舍入为 1.0。每个停止点值都必须大于或等于前一个停止点值。不满足此条件的停止点值将向上舍入为前一个停止点值。

半径之前和之后的行为由 `tileMode` 参数描述。详情请参阅 [TileMode](https://www.yuque.com/thyname/dart.ui/tilemode) 枚举。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_clamp_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_decal_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_mirror_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_repeated_radial.png)

如果 `center`、`radius`、`colors` 或 `tileMode` 为 null，或者 `colors` 或 `colorStops` 包含 null 值，此构造函数将抛出 [NoSuchMethodError](https://www.yuque.com/thyname/dart.core/nosuchmethoderror)。

如果提供了 `matrix4`，渐变填充将相对于本地坐标系按指定的 4x4 矩阵进行变换。`matrix4` 必须是打包成包含 16 个值的列表的列主序矩阵。

如果提供了 `focal` 且不等于 `center`，并且提供了 `focalRadius` 且不等于 0.0，则生成的着色器将是双焦点圆锥径向渐变，其中 `focal` 是焦点圆的中心，`focalRadius` 是该圆的半径。如果提供了 `focal` 且不等于 `center`，则两个偏移量中至少有一个不得等于 [Offset.zero]。

### Gradient.sweep()

```dart
Gradient.sweep(Offset center, List<Color> colors, [List<double>? colorStops, TileMode tileMode = TileMode.clamp, double startAngle = 0.0, double endAngle = math.pi * 2, Float64List? matrix4])
```

创建一个以 `center` 为中心、从 `startAngle` 开始到 `endAngle` 结束的扫描渐变。

`startAngle` 和 `endAngle` 应以弧度提供，零弧度为经过 `center` 的水平线右侧方向，正角度沿 `center` 顺时针方向增加。

如果提供了 `colorStops`，则 `colorStops[i]` 是一个 0.0 到 1.0 之间的数字，用于指定 `colors[i]` 在渐变中开始的位置。如果未提供 `colorStops`，则默认仅隐含两个停止点，分别位于 0.0 和 1.0 处（因此 `colors` 必须只包含两个条目）。小于 0.0 的停止点值将向上舍入为 0.0，大于 1.0 的停止点值将向下舍入为 1.0。每个停止点值都必须大于或等于前一个停止点值。不满足此条件的停止点值将向上舍入为前一个停止点值。

`startAngle` 和 `endAngle` 参数定义了要绘制的角度扇形。角度以弧度计量，从 x 轴正方向顺时针方向计算。超出 `[0, 2π]` 范围的值会通过取模运算归一化到此范围内。渐变仅在 `startAngle` 和 `endAngle` 之间的扇形内绘制。`tileMode` 决定了渐变在此扇形之外的行为方式。

`startAngle` 之前和 `endAngle` 之后的行为由 `tileMode` 参数描述。详情请参阅 [TileMode](https://www.yuque.com/thyname/dart.ui/tilemode) 枚举。

- [TileMode.clamp]：边缘颜色向无限远处延伸。
- [TileMode.mirror]：渐变重复，每次交替方向。
- [TileMode.repeated]：渐变沿相同方向重复。
- [TileMode.decal]：仅绘制渐变角度扇形内的颜色，其他区域为透明黑色。

如果指定了 [colorStops] 参数，其取值个数必须与 [colors] 相同。它指定了每个颜色停止点在 0.0 到 1.0 之间的位置。如果为 null，则假定颜色均匀分布。停止点值必须按升序排列。停止点值 0.0 对应于 [startAngle]，停止点值 1.0 对应于 [endAngle]。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_clamp_sweep.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_decal_sweep.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_mirror_sweep.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_repeated_sweep.png)

如果 `center`、`colors`、`tileMode`、`startAngle` 或 `endAngle` 为 null，或者 `colors` 或 `colorStops` 包含 null 值，此构造函数将抛出 [NoSuchMethodError](https://www.yuque.com/thyname/dart.core/nosuchmethoderror)。

如果提供了 `matrix4`，渐变填充将相对于本地坐标系按指定的 4x4 矩阵进行变换。`matrix4` 必须是打包成包含 16 个值的列表的列主序矩阵。

# ImageShader

```dart
base class ImageShader extends Shader {}
```

平铺图像的着色器（供 [Paint.shader] 使用）。

### ImageShader()

```dart
ImageShader(Image image, TileMode tmx, TileMode tmy, Float64List matrix4, {FilterQuality? filterQuality})
```

创建一个图像平铺着色器。

第一个参数指定要渲染的图像。[decodeImageFromList](https://www.yuque.com/thyname/dart.ui/decodeimagefromlist) 函数可用于将字节解码为此处所需的图像格式。（在生产代码中，从 [instantiateImageCodec](https://www.yuque.com/thyname/dart.ui/instantiateimagecodec) 开始可能更为可取。）

第二个和第三个参数分别指定 x 方向和 y 方向的 [TileMode](https://www.yuque.com/thyname/dart.ui/tilemode)。可使用 [TileMode.repeated] 来平铺图像。

第四个参数给出应用于该效果的矩阵。表达式 `Matrix4.identity().storage` 会创建一个预先填充了单位矩阵的 [Float64List](https://www.yuque.com/thyname/dart.typed_data/float64list)。

除 [filterQuality] 外，所有参数均为必需参数且不得为 null。如果构造时未指定 [filterQuality]，将根据其使用环境（例如 [Paint.filterQuality]）进行推断。

### dispose()

```dart
void dispose()
```

# FragmentProgram

```dart
base class FragmentProgram extends NativeFieldWrapperClass1 {}
```

[FragmentProgram](https://www.yuque.com/thyname/dart.ui/fragmentprogram) 的实例用于创建 [Shader](https://www.yuque.com/thyname/dart.ui/shader) 对象（供 [Paint.shader] 使用）。

更多信息请参阅网站[文档](https://docs.flutter.dev/development/ui/advanced/shaders)。

### fromAsset()

```dart
Future<FragmentProgram> fromAsset(String assetKey)
```

根据键为 [assetKey] 的资源创建一个片段程序。

该资源必须是 `impellerc` 编译器输出的文件。随后应通过 [fragmentShader] 方法复用所构造的对象，以创建可供 [Paint.shader] 使用的 [Shader](https://www.yuque.com/thyname/dart.ui/shader) 对象。

### fragmentShader()

```dart
FragmentShader fragmentShader()
```

返回一个全新的 [FragmentShader](https://www.yuque.com/thyname/dart.ui/fragmentshader) 实例。

# UniformType

```dart
sealed class UniformType {}
```

着色器中定义的 uniform 的绑定。目前用于限制可创建的 UniformArray 的类型。

# UniformFloatSlot

```dart
base class UniformFloatSlot extends UniformType {}
```

对 float 类型 uniform 的绑定。对此对象调用 [set] 会更新一个 float uniform 的值。

示例：

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformFloat('uColor', 0).set(1.0);
  shader.getUniformFloat('uColor', 1).set(0.0);
  shader.getUniformFloat('uColor', 2).set(0.0);
}
```

另请参阅：[FragmentShader.getUniformFloat] —— 如何获取 [UniformFloatSlot](https://www.yuque.com/thyname/dart.ui/uniformfloatslot) 实例。

### set()

```dart
void set(double val)
```

设置所绑定 uniform 的 float 值。

### shaderIndex

```dart
int get shaderIndex
```

VisibleForTesting：这是用于此 uniform 的 [FragmentShader.setFloat] 所使用的索引。

### name

```dart
String name
```

所绑定 uniform 的名称。

### index

```dart
int index
```

所绑定 uniform 中的偏移量。例如，对于 `.y` 为 1，对于 `.b` 为 2。

# UniformVec2Slot

```dart
base class UniformVec2Slot extends UniformType {}
```

对 vec2 类型 uniform 的绑定。对此对象调用 [set] 会更新该 uniform 的值。

示例：

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformVec2('uSize').set(100, 100);
}
```

另请参阅：[FragmentShader.getUniformVec2] —— 如何获取 [UniformVec2Slot](https://www.yuque.com/thyname/dart.ui/uniformvec2slot) 实例。

### set()

```dart
void set(double x, double y)
```

设置所绑定 uniform 的 float 值。

# UniformVec3Slot

```dart
base class UniformVec3Slot extends UniformType {}
```

对 vec3 类型 uniform 的绑定。对此对象调用 [set] 会更新该 uniform 的值。

示例：

```dart
void updateShader(ui.FragmentShader shader, double time) {
  shader.getUniformVec3('uScaledTime').set(time, time*0.1, time*0.01);
}
```

另请参阅：[FragmentShader.getUniformVec3] —— 如何获取 [UniformVec3Slot](https://www.yuque.com/thyname/dart.ui/uniformvec3slot) 实例。

### set()

```dart
void set(double x, double y, double z)
```

设置所绑定 uniform 的 float 值。

# UniformVec4Slot

```dart
base class UniformVec4Slot extends UniformType {}
```

对 vec4 类型 uniform 的绑定。对此对象调用 [set] 会更新该 uniform 的值。

示例：

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformVec4('uColor').set(1.0, 0.0, 1.0, 1.0);
}
```

另请参阅：[FragmentShader.getUniformVec4] —— 如何获取 [UniformVec4Slot](https://www.yuque.com/thyname/dart.ui/uniformvec4slot) 实例。

### set()

```dart
void set(double x, double y, double z, double w)
```

设置所绑定 uniform 的 float 值。

# UniformMat2Slot

```dart
base class UniformMat2Slot extends UniformType {}
```

对 mat2 类型 uniform 的绑定。对此对象调用 [set] 会更新该 uniform 的值。

示例：

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformMat2('uIdentity').set(
    1.0, 0.0,
    0.0, 1.0
  );
}
```

另请参阅：[FragmentShader.getUniformMat2] —— 如何获取 [UniformMat2Slot](https://www.yuque.com/thyname/dart.ui/uniformmat2slot) 实例。

### set()

```dart
void set(double m00, double m01, double m10, double m11)
```

以行主序设置矩阵的 float 值。

# UniformMat3Slot

```dart
base class UniformMat3Slot extends UniformType {}
```

对 mat3 类型 uniform 的绑定。对此对象调用 [set] 会更新该 uniform 的值。

示例：

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformMat3('uIdentity').set(
    1.0, 0.0, 0.0,
    0.0, 1.0, 0.0,
    0.0, 0.0, 1.0
  );
}
```

另请参阅：[FragmentShader.getUniformMat3] —— 如何获取 [UniformMat3Slot](https://www.yuque.com/thyname/dart.ui/uniformmat3slot) 实例。

### set()

```dart
void set(double m00, double m01, double m02, double m10, double m11, double m12, double m20, double m21, double m22)
```

以行主序设置矩阵的 float 值。

# UniformMat4Slot

```dart
base class UniformMat4Slot extends UniformType {}
```

对 mat4 类型 uniform 的绑定。对此对象调用 [set] 会更新该 uniform 的值。

示例：

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformMat4('uIdentity').set(
    1.0, 0.0, 0.0, 0.0,
    0.0, 1.0, 0.0, 0.0,
    0.0, 0.0, 1.0, 0.0,
    0.0, 0.0, 0.0, 1.0
  );
}
```

另请参阅：[FragmentShader.getUniformMat4] —— 如何获取 [UniformMat4Slot](https://www.yuque.com/thyname/dart.ui/uniformmat4slot) 实例。

### set()

```dart
void set(double m00, double m01, double m02, double m03, double m10, double m11, double m12, double m13, double m20, double m21, double m22, double m23, double m30, double m31, double m32, double m33)
```

以行主序设置矩阵的 float 值。

# UniformArray

```dart
class UniformArray<T extends UniformType> {}
```

对同一类型 T 的 uniform 的绑定数组。通过 [] 访问元素并单独设置它们。示例：

```dart
void updateShader(ui.FragmentShader shader) {
  final ui.UniformArray<ui.UniformVec4Slot> colors = shader.getUniformVec4Array('uColorArray');
  colors[0].set(1.0, 0.0, 1.0, 0.3);
}
```

另请参阅：[FragmentShader.getUniformFloatArray] —— 如何获取 [UniformArray<Float>] 实例。

### operator []()

```dart
T operator [](int index)
```

访问 UniformArray 中的一个元素。

### length

```dart
int get length
```

UniformArray 中 Uniform 的数量。

# ImageSamplerSlot

```dart
base class ImageSamplerSlot {}
```

对着色器图像采样器的绑定。对此对象调用 [set] 会更新采样器所绑定的图像。

### set()

```dart
void set(Image val)
```

为与此绑定关联的采样器设置 [Image](https://www.yuque.com/thyname/dart.ui/image) 值。

### shaderIndex

```dart
int get shaderIndex
```

VisibleForTesting：这是用于此采样器的 [FragmentShader.setImageSampler] 所使用的索引。

### name

```dart
String name
```

所绑定 uniform 的名称。

# FragmentShader

```dart
base class FragmentShader extends Shader {}
```

从 [FragmentProgram](https://www.yuque.com/thyname/dart.ui/fragmentprogram) 生成的 [Shader](https://www.yuque.com/thyname/dart.ui/shader)。

此类的实例可从 [FragmentProgram.fragmentShader] 方法获得。float uniform 列表会被初始化为着色器所期望的大小，并以零填充。随后可通过调用 [setFloat] 设置 float 类型的 uniform。采样器 uniform 通过调用 [setImageSampler] 设置。

[FragmentShader](https://www.yuque.com/thyname/dart.ui/fragmentshader) 可以被重复使用，这是一种避免重新分配和重新初始化 uniform 缓冲区及采样器的高效方式。但是，如果需要同时存在两个具有不同 float uniform 或采样器的 [FragmentShader](https://www.yuque.com/thyname/dart.ui/fragmentshader) 对象，则必须通过对 [FragmentProgram.fragmentShader] 的两次不同调用来获取它们。

### setFloat()

```dart
void setFloat(int index, double value)
```

将 [index] 处的 float uniform 设置为 [value]。

片段着色器中定义的所有非采样器类型的 uniform 都必须通过此方法设置。这包括 float 以及 vec2、vec3 和 vec4。每个 uniform 的正确索引由 uniform 在片段程序中定义的顺序决定，忽略所有采样器。对于由多个 float 组成的数据类型（例如 vec4），需要多次调用 [setFloat]。

例如，给定片段程序中的以下 uniform：

```glsl
uniform float uScale;
uniform sampler2D uTexture;
uniform vec2 uMagnitude;
uniform vec4 uColor;
```

那么用于正确初始化这些 uniform 的相应 Dart 代码为：

```dart
void updateShader(ui.FragmentShader shader, Color color, ui.Image image) {
  shader.setFloat(0, 23);  // uScale
  shader.setFloat(1, 114); // uMagnitude x
  shader.setFloat(2, 83);  // uMagnitude y

  // 将颜色转换为预乘不透明度。
  shader.setFloat(3, color.r * color.a); // uColor r
  shader.setFloat(4, color.g * color.a); // uColor g
  shader.setFloat(5, color.b * color.a); // uColor b
  shader.setFloat(6, color.a);           // uColor a

  // 初始化采样器 uniform。
  shader.setImageSampler(0, image);
}
```

请注意，所使用的索引不计入 `sampler2D` uniform。此 uniform 将通过 [setImageSampler] 单独设置，其索引从 0 重新开始。

任何未初始化的 float uniform 将默认为 `0`。

### getUniformFloat()

```dart
UniformFloatSlot getUniformFloat(String name, [int? index])
```

访问名为 [name] 的 uniform 的 float 绑定，可选带有偏移量 [index]。[index] 的示例值：'foo.y' 为 1，'foo.b' 为 2。

示例：

```glsl
uniform float uScale;
uniform sampler2D uTexture;
uniform vec2 uMagnitude;
uniform vec4 uColor;
```

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformFloat('uScale');
  shader.getUniformFloat('uMagnitude', 0);
  shader.getUniformFloat('uMagnitude', 1);
  shader.getUniformFloat('uColor', 0);
  shader.getUniformFloat('uColor', 1);
  shader.getUniformFloat('uColor', 2);
  shader.getUniformFloat('uColor', 3);
}
```

### getUniformVec2()

```dart
UniformVec2Slot getUniformVec2(String name)
```

访问名为 [name] 的 vec2 类型 uniform 的 float 绑定。

示例：

```glsl
uniform float uScale;
uniform vec2 uMagnitude;
```

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformFloat('uScale');
  shader.getUniformVec2('uMagnitude');
}
```

### getUniformVec3()

```dart
UniformVec3Slot getUniformVec3(String name)
```

访问名为 [name] 的 vec3 类型 uniform 的 float 绑定。

示例：

```glsl
uniform float uScale;
uniform vec3 uScaledTime;
```

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformFloat('uScale');
  shader.getUniformVec3('uScaledTime');
}
```

### getUniformVec4()

```dart
UniformVec4Slot getUniformVec4(String name)
```

访问名为 [name] 的 vec4 类型 uniform 的 float 绑定。

示例：

```glsl
uniform float uScale;
uniform vec4 uColor;
```

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformFloat('uScale');
  shader.getUniformVec4('uColor');
}
```

### getUniformMat2()

```dart
UniformMat2Slot getUniformMat2(String name)
```

访问名为 [name] 的 mat2 类型 uniform 的 float 绑定。

示例：

```glsl
uniform mat2 uIdentity;
```

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformMat2('uIdentity');
}
```

### getUniformMat3()

```dart
UniformMat3Slot getUniformMat3(String name)
```

访问名为 [name] 的 mat3 类型 uniform 的 float 绑定。

示例：

```glsl
uniform mat3 uIdentity;
```

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformMat3('uIdentity');
}
```

### getUniformMat4()

```dart
UniformMat4Slot getUniformMat4(String name)
```

访问名为 [name] 的 mat4 类型 uniform 的 float 绑定。

示例：

```glsl
uniform mat4 uIdentity;
```

```dart
void updateShader(ui.FragmentShader shader) {
  shader.getUniformMat4('uIdentity');
}
```

### getUniformFloatArray()

```dart
UniformArray<UniformFloatSlot> getUniformFloatArray(String name)
```

访问名为 [name] 的 float[] 类型 uniform 的绑定。

示例：

```glsl
uniform float[10] uValues;
```

```dart
void updateShader(ui.FragmentShader shader) {
  final ui.UniformArray<ui.UniformFloatSlot> values = shader.getUniformFloatArray('uValues');
  values[2].set(1.0);
}
```

### getUniformVec2Array()

```dart
UniformArray<UniformVec2Slot> getUniformVec2Array(String name)
```

访问名为 [name] 的 vec2[] 类型 uniform 的绑定。

示例：

```glsl
uniform vec2[10] uPositions;
```

```dart
void updateShader(ui.FragmentShader shader) {
  final ui.UniformArray<ui.UniformVec2Slot> positions = shader.getUniformVec2Array('uPositions');
  positions[2].set(6.0, 7.0);
}
```

### getUniformVec3Array()

```dart
UniformArray<UniformVec3Slot> getUniformVec3Array(String name)
```

访问名为 [name] 的 vec3[] 类型 uniform 的绑定。

示例：

```glsl
uniform vec3[10] uColors;
```

```dart
void updateShader(ui.FragmentShader shader) {
  final ui.UniformArray<ui.UniformVec3Slot> colors = shader.getUniformVec3Array('uColors');
  colors[0].set(1.0, 0.0, 1.0);
}
```

### getUniformVec4Array()

```dart
UniformArray<UniformVec4Slot> getUniformVec4Array(String name)
```

访问名为 [name] 的 vec4[] 类型 uniform 的绑定。

示例：

```glsl
uniform vec4[10] uColors;
```

```dart
void updateShader(ui.FragmentShader shader) {
  final ui.UniformArray<ui.UniformVec4Slot> colors = shader.getUniformVec4Array('uColors');
  colors[0].set(1.0, 0.0, 1.0, 0.5);
}
```

### getUniformMat2Array()

```dart
UniformArray<UniformMat2Slot> getUniformMat2Array(String name)
```

访问名为 [name] 的 mat2[] 类型 uniform 的绑定。

示例：

```glsl
uniform mat2[10] uMatricies;
```

```dart
void updateShader(ui.FragmentShader shader) {
  final ui.UniformArray<ui.UniformMat2Slot> mats = shader.getUniformMat2Array('uMatricies');
  mats[0].set(
    1.0, 0.0,
    1.0, 0.5
  );
}
```

### getUniformMat3Array()

```dart
UniformArray<UniformMat3Slot> getUniformMat3Array(String name)
```

访问名为 [name] 的 mat3[] 类型 uniform 的绑定。

示例：

```glsl
uniform mat3[10] uMatricies;
```

```dart
void updateShader(ui.FragmentShader shader) {
  final ui.UniformArray<ui.UniformMat3Slot> mats = shader.getUniformMat3Array('uMatricies');
  mats[0].set(
    1.0, 0.0, 0.0,
    1.0, 0.5, 0.0,
    1.0, 0.3, 1.2
  );
}
```

### getUniformMat4Array()

```dart
UniformArray<UniformMat4Slot> getUniformMat4Array(String name)
```

访问名为 [name] 的 mat4[] 类型 uniform 的绑定。

示例：

```glsl
uniform mat4[10] uMatricies;
```

```dart
void updateShader(ui.FragmentShader shader) {
  final ui.UniformArray<ui.UniformMat4Slot> mats = shader.getUniformMat4Array('uMatricies');
  mats[0].set(
    1.0, 0.0, 0.0, 1.0,
    1.0, 0.5, 0.0, 0.4,
    1.0, 0.3, 1.2, 0.2,
    0.0, 0.0, 1.0, 0.3,
  );
}
```

### getImageSampler()

```dart
ImageSamplerSlot getImageSampler(String name)
```

访问与名为 [name] 的采样器关联的 [ImageSamplerSlot](https://www.yuque.com/thyname/dart.ui/imagesamplerslot) 绑定。

传递给 setImageSampler 的索引是片段程序中定义的采样器 uniform 的索引，不包括所有非采样器 uniform。

### setImageSampler()

```dart
void setImageSampler(int index, Image image, {FilterQuality filterQuality = FilterQuality.none})
```

将 [index] 处的采样器 uniform 设置为 [image]。

传递给 setImageSampler 的索引是片段程序中定义的采样器 uniform 的索引，不包括所有非采样器 uniform。

可选的 [filterQuality] 参数可用于设置对图像进行采样时使用的质量级别。默认设置为 [FilterQuality.none]。

必须提供着色器所期望的所有采样器 uniform，否则结果将是未定义的。

### dispose()

```dart
void dispose()
```

释放 [FragmentShader](https://www.yuque.com/thyname/dart.ui/fragmentshader) 所持有的原生资源。

调用此方法后，再调用着色器的方法，或将其附加到 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 对象都将失败并抛出异常。两次调用 [dispose] 也会导致抛出异常。

# VertexMode

```dart
enum VertexMode {}
```

定义在绘制一组三角形时如何解释一系列点。

由 [Canvas.drawVertices] 使用。

将每三个连续的点绘制为一个三角形的顶点。

将每个滑动窗口内的三个点绘制为一个三角形的顶点。

将第一个点和每个滑动窗口内的两个点绘制为一个三角形的顶点。

大多数后端并不原生支持此模式，而是通过将这些点展开为等效的 [VertexMode.triangles] 来实现，这种方式通常效率更高。

# Vertices

```dart
base class Vertices extends NativeFieldWrapperClass1 {}
```

用于 [Canvas.drawVertices] 的一组顶点数据。

顶点数据由画布坐标空间中的一系列点组成。根据 [VertexMode](https://www.yuque.com/thyname/dart.ui/vertexmode) 的不同,这些点可被解释为独立的三角形([VertexMode.triangles]),一系列点构成的滑动窗口所形成的三角形链,其中每个三角形与下一个共享一条边([VertexMode.triangleStrip]),或者以单个共享点为中心呈扇形排列的三角形([VertexMode.triangleFan])。

每个点都可以关联一种颜色。每个三角形都以渐变方式绘制,在该三角形三个点的三种颜色之间进行混合。如果未指定颜色,则所有点均视为透明黑色。

这些颜色随后会与调用 [Canvas.drawVertices] 时指定的 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 混合。此画笔可以是纯色([Paint.color]),也可以是使用着色器([Paint.shader])指定的位图,通常是渐变([Gradient](https://www.yuque.com/thyname/dart.ui/gradient))或图像([ImageFilter](https://www.yuque.com/thyname/dart.ui/imagefilter))。该位图使用与画布相同的坐标空间(对于 [ImageFilter](https://www.yuque.com/thyname/dart.ui/imagefilter) 而言,这与源图像的坐标空间明显不同;源图像会根据滤镜的配置进行平铺,绘制三角形时采样的图像是应用所有重复平铺后的无限图像。)

[Vertices](https://www.yuque.com/thyname/dart.ui/vertices) 中的每个点都与该图像上的特定点相关联。绘制每个三角形时,会在与三角形三个点对应的图像三个点之间进行插值,从而从该图像中采样点。

[Vertices.new] 构造函数使用 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 和 [Color](https://www.yuque.com/thyname/dart.ui/color) 对象列表配置上述所有内容。而 [Vertices.raw] 构造函数则使用 [Float32List](https://www.yuque.com/thyname/dart.typed_data/float32list)、[Int32List](https://www.yuque.com/thyname/dart.typed_data/int32list) 和 [Uint16List](https://www.yuque.com/thyname/dart.typed_data/uint16list) 对象,这与内部使用的数据格式更为接近,因此可以减少部分转换开销。如果数据来自其他来源(例如文件),可以直接解析为底层表示形式,此时使用 raw 构造函数会更为方便。

### Vertices()

```dart
Vertices(VertexMode mode, List<Offset> positions, {List<Color>? colors, List<Offset>? textureCoordinates, List<int>? indices})
```

创建一组用于 [Canvas.drawVertices] 的顶点数据。

`mode` 参数描述了这些点应如何被解释:作为独立的三角形([VertexMode.triangles]),作为一系列点构成的滑动窗口所形成的三角形链,其中每个三角形与下一个共享一条边([VertexMode.triangleStrip]),或者作为以单个共享点为中心的扇形三角形([VertexMode.triangleFan])。

`positions` 参数提供画布空间中用于绘制三角形的点。

如果指定了 `colors` 参数,则为 `positions` 中的每个点提供颜色。每个三角形都以渐变方式绘制,在该三角形三个点的三种颜色之间进行混合。(这些颜色随后会与调用 [Canvas.drawVertices] 时指定的 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 混合。)

如果指定了 `textureCoordinates` 参数,则为 `positions` 中的对应点提供在 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 图像中需要采样的点。

如果指定了 `colors` 或 `textureCoordinates` 参数,它们的长度必须与 `positions` 相同。

`indices` 参数指定了各点被绘制的顺序。如果省略该参数(或该参数存在但为空),这些点将按照它们在 `positions` 中给出的顺序处理,如同 `indices` 是一个从 0 到 n-1 的列表,其中 _n_ 是 `positions` 中的条目数。如果 `indices` 参数存在且非空,它必须至少包含三个条目,但可以超过此长度的任意长度。索引可以多次引用 positions 数组中的偏移量,也可以完全跳过某些位置。

如果指定了 `indices` 参数,该列表中的所有值都必须是 `positions` 的有效索引值。

`mode` 和 `positions` 参数不能为 null。

此构造函数会先将其参数转换为 [dart:typed_data](https://www.yuque.com/thyname/dart.typed_data) 列表(例如使用 [Float32List](https://www.yuque.com/thyname/dart.typed_data/float32list) 存储坐标),然后再将其发送给 Flutter 引擎。如果提供给此构造函数的数据尚未采用 [List](https://www.yuque.com/thyname/dart.core/list) 形式,可考虑改用 [Vertices.raw] 构造函数,以避免对数据进行两次转换。

### Vertices.raw()

```dart
Vertices.raw(VertexMode mode, Float32List positions, {Int32List? colors, Float32List? textureCoordinates, Uint16List? indices})
```

使用 Flutter 引擎所需的编码方式,创建一组用于 [Canvas.drawVertices] 的顶点数据。

`mode` 参数描述了这些点应如何被解释:作为独立的三角形([VertexMode.triangles]),作为一系列点构成的滑动窗口所形成的三角形链,其中每个三角形与下一个共享一条边([VertexMode.triangleStrip]),或者作为以单个共享点为中心的扇形三角形([VertexMode.triangleFan])。

`positions` 参数提供画布空间中用于绘制三角形的点。列表中的每个点用两个数字表示,第一个为 x 坐标,第二个为 y 坐标。(因此,该列表必须包含偶数个条目。)

如果指定了 `colors` 参数,则为 `positions` 中的每个点提供颜色。每种颜色以 8 位色彩通道的 ARGB 形式表示(类似于 [Color.value] 的内部表示形式),因此如果指定该列表,其长度必须为 `positions` 长度的一半。每个三角形都以渐变方式绘制,在该三角形三个点的三种颜色之间进行混合。(这些颜色随后会与调用 [Canvas.drawVertices] 时指定的 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 混合。)

如果指定了 `textureCoordinates` 参数,则为 `positions` 中的对应点提供在 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 图像中需要采样的点。列表中的每个点用两个数字表示,第一个为 x 坐标,第二个为 y 坐标。如果指定该列表,其长度必须与 `positions` 相同。

`indices` 参数指定了各点被绘制的顺序。如果省略该参数(或该参数存在但为空),这些点将按照它们在 `positions` 中给出的顺序处理,如同 `indices` 是一个从 0 到 n-2 的列表,其中 _n_ 是 `positions` 中点对的数量(即 `positions` 长度的一半)。如果 `indices` 参数存在且非空,它必须至少包含三个条目,但可以超过此长度的任意长度。索引可以多次引用 positions 数组中的偏移量,也可以完全跳过某些位置。

如果指定了 `indices` 参数,该列表中的所有值都必须是 `positions` 中点对的有效索引值。例如,如果 `positions` 中有 12 个数字(表示 6 个坐标),`indices` 中的数字必须在 0 到 5(含)的范围内。

`mode` 和 `positions` 参数不能为 null。

### dispose()

```dart
void dispose()
```

释放此对象所使用的资源。调用此方法后,该对象将不可再使用。

### debugDisposed

```dart
bool get debugDisposed
```

此底层顶点数据的引用是否已被 [dispose]。

仅当启用断言时,此属性才会返回有效值,否则不得使用。

# PointMode

```dart
enum PointMode {}
```

定义在绘制一组点时,点列表应如何被解释。

由 [Canvas.drawPoints] 和 [Canvas.drawRawPoints] 使用。

分别绘制每个点。

如果 [Paint.strokeCap] 为 [StrokeCap.round],则每个点都绘制为直径等于 [Paint.strokeWidth] 的圆形,并按照 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 所描述的方式填充(忽略 [Paint.style])。

否则,每个点都绘制为边长等于 [Paint.strokeWidth] 的轴对齐正方形,并按照 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 所描述的方式填充(忽略 [Paint.style])。

将每两个连续点绘制为一条线段。

如果点的数量为奇数,则忽略最后一个点。

这些线条按照 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 所描述的方式描边(忽略 [Paint.style])。

将整个点序列绘制为一条线。

这些线条按照 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 所描述的方式描边(忽略 [Paint.style])。

# ClipOp

```dart
enum ClipOp {}
```

定义新裁剪区域应如何与现有裁剪区域合并。

由 [Canvas.clipRect] 使用。

从现有区域中减去新区域。

将新区域与现有区域求交集。

# Canvas

```dart
abstract class Canvas {}
```

用于记录图形操作的接口。

[Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 对象用于创建 [Picture](https://www.yuque.com/thyname/dart.ui/picture) 对象,而 [Picture](https://www.yuque.com/thyname/dart.ui/picture) 对象本身可与 [SceneBuilder](https://www.yuque.com/thyname/dart.ui/scenebuilder) 一起用于构建 [Scene](https://www.yuque.com/thyname/dart.ui/scene)。不过,在正常使用中,这一切都由框架自动处理。

画布具有一个当前变换矩阵,该矩阵会应用于所有操作。初始情况下,变换矩阵为单位变换。可以使用 [translate]、[scale]、[rotate]、[skew] 和 [transform] 方法修改该矩阵。

画布还具有一个当前裁剪区域,该区域会应用于所有操作。初始情况下,裁剪区域是无限的。可以使用 [clipRect]、[clipRRect] 和 [clipPath] 方法修改该区域。

可以使用由 [save]、[saveLayer] 和 [restore] 方法管理的栈来保存和恢复当前的变换与裁剪状态。

## 与 Flutter 框架配合使用

Flutter 框架的 [RendererBinding](https://www.yuque.com/thyname/flutter.rendering/rendererbinding) 提供了一个用于创建 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 对象的钩子([RendererBinding.createCanvas]),使测试能够接入场景创建逻辑。在 Flutter 框架的上下文中,如果要创建一个将与 [PictureLayer](https://www.yuque.com/thyname/flutter.rendering/picturelayer) 一起作为 [Scene](https://www.yuque.com/thyname/dart.ui/scene) 一部分使用的 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas),应考虑调用 [RendererBinding.createCanvas],而不是直接调用 [Canvas.new] 构造函数。

当使用画布生成用于其他目的的位图时(例如使用 [Picture.toImage] 生成 PNG 图像),此规则不适用。

### Canvas()

```dart
Canvas(PictureRecorder recorder, [Rect? cullRect])
```

创建一个画布,用于将图形操作记录到给定的图片记录器中。

完全影响给定 `cullRect` 之外像素的图形操作可能会被实现丢弃。但是,如果某个命令绘制的内容部分位于 `cullRect` 内部、部分位于外部,实现仍可能在这些边界之外进行绘制。若要确保给定区域之外的像素被丢弃,应考虑使用 [clipRect]。`cullRect` 是可选的;默认情况下,所有操作都会被保留。

要结束记录,请对给定的记录器调用 [PictureRecorder.endRecording]。

### save()

```dart
void save()
```

将当前变换和裁剪的副本保存到保存栈中。

调用 [restore] 以弹出保存栈。

另请参阅:

- [saveLayer],功能相同,但还会将执行的命令分组,直到对应的 [restore] 为止。

### saveLayer()

```dart
void saveLayer(Rect? bounds, Paint paint)
```

将当前变换和裁剪的副本保存到保存栈中,然后创建一个新的分组,后续调用都将成为该分组的一部分。当保存栈稍后被弹出时,该分组将被展平为一个图层,并应用给定 `paint` 的 [Paint.colorFilter] 和 [Paint.blendMode]。

这使你能够创建合成效果,例如使一组绘制命令呈现半透明效果。如果不使用 [saveLayer],该分组中的每个部分都会被单独绘制,因此它们重叠的地方会比不重叠的地方颜色更深。通过使用 [saveLayer] 将它们分组,可以先以不透明颜色绘制它们,然后使用 [saveLayer] 的画笔使整个分组变为透明。

调用 [restore] 以弹出保存栈,并将画笔应用于该分组。

## 将 saveLayer 与裁剪配合使用

当矩形裁剪操作(来自 [clipRect])与光栅缓冲区不轴对齐,或者当裁剪操作不是直线型的(例如,由 [clipRRect] 创建的圆角矩形裁剪,或由 [clipPath] 创建的任意复杂路径裁剪)时,裁剪的边缘需要进行抗锯齿处理。

如果两次绘制调用在此类裁剪区域的边缘发生重叠,在不使用 [saveLayer] 的情况下,第一次绘制会先与背景进行抗锯齿处理,然后第二次绘制会与第一次绘制和背景混合后的结果进行抗锯齿处理。另一方面,如果在建立裁剪后立即使用 [saveLayer],第二次绘制会在图层中覆盖第一次绘制,因此当图层被裁剪并合成时(调用 [restore] 时),只有第二次绘制会单独与背景进行抗锯齿处理。

例如,以下 [CustomPainter.paint] 方法绘制了一个干净的白色圆角矩形:

```dart
void paint(Canvas canvas, Size size) {
  Rect rect = Offset.zero & size;
  canvas.save();
  canvas.clipRRect(RRect.fromRectXY(rect, 100.0, 100.0));
  canvas.saveLayer(rect, Paint());
  canvas.drawPaint(Paint()..color = Colors.red);
  canvas.drawPaint(Paint()..color = Colors.white);
  canvas.restore();
  canvas.restore();
}
```

而下面这个例子则会渲染出红色轮廓,这是因为红色画笔在裁剪边缘与背景进行了抗锯齿处理,然后白色画笔也以相同方式与背景(_包括已裁剪的红色部分_)进行了抗锯齿处理:

```dart
void paint(Canvas canvas, Size size) {
  // (this example renders poorly, prefer the example above)
  Rect rect = Offset.zero & size;
  canvas.save();
  canvas.clipRRect(RRect.fromRectXY(rect, 100.0, 100.0));
  canvas.drawPaint(Paint()..color = Colors.red);
  canvas.drawPaint(Paint()..color = Colors.white);
  canvas.restore();
}
```

如果裁剪只影响一次绘制操作,则上述问题并不存在。例如,以下 paint 方法绘制了一对干净的白色圆角矩形,即使这些裁剪并未在单独的图层上完成:

```dart
void paint(Canvas canvas, Size size) {
  canvas.save();
  canvas.clipRRect(RRect.fromRectXY(Offset.zero & (size / 2.0), 50.0, 50.0));
  canvas.drawPaint(Paint()..color = Colors.white);
  canvas.restore();
  canvas.save();
  canvas.clipRRect(RRect.fromRectXY(size.center(Offset.zero) & (size / 2.0), 50.0, 50.0));
  canvas.drawPaint(Paint()..color = Colors.white);
  canvas.restore();
}
```

(顺便一提,与其像这样使用 [clipRRect] 和 [drawPaint] 来绘制圆角矩形,不如优先使用 [drawRRect] 方法。这些示例使用 [drawPaint] 作为"将被裁剪的复杂绘制操作"的代表,以说明这一点。)

## 性能考量

一般来说,[saveLayer] 的开销相对较大。

GPU(图形处理单元,即处理图形运算的硬件)存在多种不同的硬件架构,但其中大多数都会为了性能而对命令进行批处理和重新排序。当使用图层时,会导致渲染管线不得不切换渲染目标(从一个图层切换到另一个图层)。渲染目标切换会刷新 GPU 的命令缓冲区,这通常意味着更大批处理所能获得的优化会因此丧失。渲染目标切换还会产生大量内存抖动,因为 GPU 需要将当前帧缓冲区的内容从针对写入优化的那部分内存中复制出来,待之前的渲染目标(图层)恢复后,再将其复制回去。

另请参阅:

- [save],保存当前状态,但不会为后续命令创建新图层。
- [BlendMode](https://www.yuque.com/thyname/dart.ui/blendmode),讨论了 [Paint.blendMode] 与 [saveLayer] 配合使用的方式。

### restore()

```dart
void restore()
```

如果保存栈中有内容,则弹出当前保存栈。否则不执行任何操作。

使用 [save] 和 [saveLayer] 将状态压入栈中。

如果该状态是通过 [saveLayer] 压入的,则此调用还会将新图层合成到之前的图层中。

### restoreToCount()

```dart
void restoreToCount(int count)
```

将保存栈恢复到之前的某个层级,该层级值可通过 [getSaveCount] 获得。如果 [count] 小于 1,则栈会恢复到其初始状态。如果 [count] 大于当前的 [getSaveCount],则不执行任何操作。

使用 [save] 和 [saveLayer] 将状态压入栈中。

如果此调用恢复的状态栈层级中有任何一层是通过 [saveLayer] 压入的,则此调用还会将这些图层合成到它们各自之前的图层中。

### getSaveCount()

```dart
int getSaveCount()
```

返回保存栈中的条目数,包括初始状态。这意味着对于一个干净的画布,该方法返回 1;每次调用 [save] 和 [saveLayer] 都会使其递增,而每次与之对应的 [restore] 调用都会使其递减。

该数值不会低于 1。

### translate()

```dart
void translate(double dx, double dy)
```

为当前变换添加一个平移,水平方向按第一个参数偏移坐标空间,垂直方向按第二个参数偏移坐标空间。

### scale()

```dart
void scale(double sx, [double? sy])
```

为当前变换添加一个轴对齐的缩放,水平方向按第一个参数缩放,垂直方向按第二个参数缩放。

如果未指定 [sy],则两个方向的缩放都将使用 [sx]。

### rotate()

```dart
void rotate(double radians)
```

为当前变换添加一个旋转。参数单位为顺时针方向的弧度。

### skew()

```dart
void skew(double sx, double sy)
```

为当前变换添加一个轴对齐的倾斜,第一个参数是围绕原点顺时针方向的水平倾斜量(以"高度/宽度"为单位),第二个参数是围绕原点顺时针方向的垂直倾斜量(以"高度/宽度"为单位)。

### transform()

```dart
void transform(Float64List matrix4)
```

将当前变换与指定的 4⨉4 变换矩阵相乘,该矩阵以列主序的数值列表形式指定。

### getTransform()

```dart
Float64List getTransform()
```

返回当前变换,包括自创建此 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 对象以来执行的所有变换方法的组合结果,并遵循 save/restore 历史记录。

可以改变当前变换的方法包括 [translate]、[scale]、[rotate]、[skew] 和 [transform]。[restore] 方法也可以修改当前变换,将其恢复为与之关联的 [save] 或 [saveLayer] 调用之前的值。

### clipRect()

```dart
void clipRect(Rect rect, {ClipOp clipOp = ClipOp.intersect, bool doAntiAlias = true})
```

将裁剪区域缩小为当前裁剪与给定矩形的交集。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/clip_rect.png)

如果 [doAntiAlias] 为 true,则裁剪将进行抗锯齿处理。

如果多个绘制命令与裁剪边界相交,可能会导致裁剪边界处的混合结果不正确。有关如何解决此问题的讨论,请参阅 [saveLayer]。

使用 [ClipOp.difference] 可从当前裁剪中减去所提供的矩形。

### clipRRect()

```dart
void clipRRect(RRect rrect, {bool doAntiAlias = true})
```

将裁剪区域缩小为当前裁剪与给定圆角矩形的交集。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/clip_rrect.png)

如果 [doAntiAlias] 为 true,则裁剪将进行抗锯齿处理。

如果多个绘制命令与裁剪边界相交,可能会导致裁剪边界处的混合结果不正确。有关如何解决此问题的讨论以及 [clipRRect] 的一些使用示例,请参阅 [saveLayer]。

### clipRSuperellipse()

```dart
void clipRSuperellipse(RSuperellipse rsuperellipse, {bool doAntiAlias = true})
```

将裁剪区域缩小为当前裁剪与给定圆角超椭圆的交集。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/clip_rsuperellipse.png)

如果 [doAntiAlias] 为 true,则裁剪将进行抗锯齿处理。

如果多个绘制命令与裁剪边界相交,可能会导致裁剪边界处的混合结果不正确。有关如何解决此问题的讨论以及 [clipRSuperellipse] 的一些使用示例,请参阅 [saveLayer]。

### clipPath()

```dart
void clipPath(Path path, {bool doAntiAlias = true})
```

将裁剪区域缩小为当前裁剪与给定 [Path](https://www.yuque.com/thyname/dart.ui/path) 的交集。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/clip_path.png)

如果 [doAntiAlias] 为 true,则裁剪将进行抗锯齿处理。

如果多个绘制命令与裁剪边界相交,可能会导致裁剪边界处的混合结果不正确。有关如何解决此问题的讨论,请参阅 [saveLayer]。

### getLocalClipBounds()

```dart
Rect getLocalClipBounds()
```

返回此 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 对象当前保存栈内执行的所有裁剪方法组合结果的保守边界,该边界以当前执行渲染操作时所处的本地坐标空间为准进行度量。

组合后的裁剪结果会先向外舍入到整数像素边界,然后再转换回本地坐标空间,这一处理考虑了渲染操作(尤其是抗锯齿处理)中的像素舍入。由于 [Picture](https://www.yuque.com/thyname/dart.ui/picture) 最终可能会在变换组件或图层的上下文中被渲染到场景中,因此该结果可能会因过早舍入而过于保守。结合外部变换以及在真实设备坐标系中的舍入,使用 [getDestinationClipBounds] 方法将产生更精确的结果,但该值可提供一种更便捷的近似方式,用于将渲染操作与已建立的裁剪进行比较。

{@template dart.ui.canvas.conservativeClipBounds} 边界的保守估计基于对每个以 [ClipOp.intersect] 方式执行的裁剪方法的边界求交集,并可能忽略任何以 [ClipOp.difference] 方式执行的裁剪方法。[ClipOp](https://www.yuque.com/thyname/dart.ui/clipop) 参数仅存在于 [clipRect] 方法中。

要理解边界估计为何会是保守的,请考虑以下两次裁剪方法调用:

```dart
void draw(Canvas canvas) {
  canvas.clipPath(Path()
    ..addRect(const Rect.fromLTRB(10, 10, 20, 20))
    ..addRect(const Rect.fromLTRB(80, 80, 100, 100)));
  canvas.clipPath(Path()
    ..addRect(const Rect.fromLTRB(80, 10, 100, 20))
    ..addRect(const Rect.fromLTRB(10, 80, 20, 100)));
  // ...
}
```

在执行这两次调用之后,由于这两条路径没有重叠区域,因此已没有可供绘制的区域。但在这种情况下,[getLocalClipBounds] 仍会返回一个从 `10, 10` 到 `100, 100` 的矩形,因为它仅通过对两个路径对象的边界求交集来获得其保守估计。

裁剪边界不受任何外层 [saveLayer] 调用边界的影响,因为引擎目前并不保证在渲染期间严格执行这些边界。

可以改变当前裁剪的方法包括 [clipRect]、[clipRRect] 和 [clipPath]。[restore] 方法也可以修改当前裁剪,将其恢复为与之关联的 [save] 或 [saveLayer] 调用之前的值。{@endtemplate}

### getDestinationClipBounds()

```dart
Rect getDestinationClipBounds()
```

返回此 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 对象当前保存栈内执行的所有裁剪方法组合结果的保守边界,该边界以 [Picture](https://www.yuque.com/thyname/dart.ui/picture) 将被渲染到的目标坐标空间为准进行度量。

与 [getLocalClipBounds] 不同,此处的边界不会向外舍入到整数像素边界,因为如果正在构建的 [Picture](https://www.yuque.com/thyname/dart.ui/picture) 在渲染或添加到场景时会经过进一步变换,目标坐标空间可能并不代表像素。为了确定受影响的真实像素,应先应用这些外部变换,然后再将结果向外舍入到整数像素边界。最典型的情况是,[Picture](https://www.yuque.com/thyname/dart.ui/picture) 对象会在场景中以代表设备像素比的缩放变换进行渲染。

{@macro dart.ui.canvas.conservativeClipBounds}

### drawColor()

```dart
void drawColor(Color color, BlendMode blendMode)
```

将给定的 [Color](https://www.yuque.com/thyname/dart.ui/color) 绘制到画布上,并应用给定的 [BlendMode](https://www.yuque.com/thyname/dart.ui/blendmode),其中给定的颜色作为源,背景作为目标。

### drawLine()

```dart
void drawLine(Offset p1, Offset p2, Paint paint)
```

使用给定的画笔在给定的两点之间绘制一条线。该线条以描边方式绘制,此调用会忽略 [Paint.style] 的值。

`p1` 和 `p2` 参数被解释为相对于原点的偏移量。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_line.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_line_dark.png#gh-dark-mode-only)

### drawPaint()

```dart
void drawPaint(Paint paint)
```

使用给定的 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 填充整个画布。

若要使用纯色和混合模式填充画布,可考虑改用 [drawColor]。

### drawRect()

```dart
void drawRect(Rect rect, Paint paint)
```

使用给定的 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 绘制一个矩形。该矩形是填充还是描边(或两者兼有)由 [Paint.style] 控制。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_rect.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_rect_dark.png#gh-dark-mode-only)

### drawRRect()

```dart
void drawRRect(RRect rrect, Paint paint)
```

使用给定的 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 绘制一个圆角矩形。该矩形是填充还是描边(或两者兼有)由 [Paint.style] 控制。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_rrect.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_rrect_dark.png#gh-dark-mode-only)

### drawDRRect()

```dart
void drawDRRect(RRect outer, RRect inner, Paint paint)
```

使用给定的 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 绘制一个由两个圆角矩形之差构成的形状。该形状是填充还是描边(或两者兼有)由 [Paint.style] 控制。

该形状与圆环几乎相似,但并非完全相同。

### drawRSuperellipse()

```dart
void drawRSuperellipse(RSuperellipse rsuperellipse, Paint paint)
```

使用给定的 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 绘制一个圆角超椭圆。该形状以填充方式绘制,此调用会忽略 [Paint.style] 的值。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_rsuperellipse.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_rsuperellipse.png#gh-dark-mode-only)

### drawOval()

```dart
void drawOval(Rect rect, Paint paint)
```

使用给定的 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 绘制一个轴对齐的椭圆,该椭圆填满给定的轴对齐矩形。该椭圆是填充还是描边(或两者兼有)由 [Paint.style] 控制。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_oval.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_oval_dark.png#gh-dark-mode-only)

### drawCircle()

```dart
void drawCircle(Offset c, double radius, Paint paint)
```

绘制一个圆,其圆心为第一个参数给定的点,半径为第二个参数给定的值,使用第三个参数给定的 [Paint](https://www.yuque.com/thyname/dart.ui/paint)。该圆是填充还是描边(或两者兼有)由 [Paint.style] 控制。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_circle.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_circle_dark.png#gh-dark-mode-only)

### drawArc()

```dart
void drawArc(Rect rect, double startAngle, double sweepAngle, bool useCenter, Paint paint)
```

绘制一段弧,并将其缩放以适应给定的矩形。

该弧从围绕椭圆的 `startAngle` 弧度处开始,到 `startAngle` + `sweepAngle` 弧度处结束,其中 0 弧度是椭圆右侧与经过矩形中心的水平线相交的那个点,正角度沿椭圆顺时针方向增加。如果 `useCenter` 为 true,则该弧会闭合回圆心,形成一个扇形。否则,该弧不闭合,形成一个弓形。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_draw_arc.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/canvas_draw_arc_dark.png#gh-dark-mode-only)

此方法针对绘制弧进行了优化,应比 [Path.arcTo] 更快。

### drawPath()

```dart
void drawPath(Path path, Paint paint)
```

使用给定的 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 绘制给定的 [Path](https://www.yuque.com/thyname/dart.ui/path)。

该形状是填充还是描边(或两者兼有)由 [Paint.style] 控制。如果该路径以填充方式绘制,则其中的子路径会被隐式闭合(参见 [Path.close])。

绘制简单形状(如矩形、椭圆或圆角矩形)时,应优先使用 [drawRect]、[drawOval] 或 [drawRRect] 等方法,而非 [drawPath]。绘制简单形状的方法通常比绘制 [Path](https://www.yuque.com/thyname/dart.ui/path) 更高效。

### drawImage()

```dart
void drawImage(Image image, Offset offset, Paint paint)
```

将给定的 [Image](https://www.yuque.com/thyname/dart.ui/image) 绘制到画布中,其左上角位于给定的 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 处。该图像会使用给定的 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 合成到画布中。

### drawImageRect()

```dart
void drawImageRect(Image image, Rect src, Rect dst, Paint paint)
```

将由 `src` 参数描述的给定图像子集绘制到画布中由 `dst` 参数给定的轴对齐矩形内。

此操作可能会从 `src` 矩形之外采样,最多可超出所应用滤镜宽度的一半。

对同一图像使用不同参数多次调用此方法时,可以将这些调用批量合并为对 [drawAtlas] 的一次调用,以提升性能。

### drawImageNine()

```dart
void drawImageNine(Image image, Rect center, Rect dst, Paint paint)
```

使用给定的 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 将给定的 [Image](https://www.yuque.com/thyname/dart.ui/image) 绘制到画布中。

该图像会被分成九个部分绘制,其分割方式是绘制两条水平线和两条垂直线,其中 `center` 参数描述了这四条线相互交叉所形成的四个点构成的矩形。(这样会形成一个 3×3 的区域网格,中心区域由 `center` 参数描述。)

四个角落区域会不经缩放地绘制在由 `dst` 描述的目标矩形的四个角上。其余五个区域则通过拉伸绘制,使其在保持相对位置的同时恰好覆盖整个目标矩形。

### drawPicture()

```dart
void drawPicture(Picture picture)
```

将给定的图片绘制到画布上。要创建图片,请参阅 [PictureRecorder](https://www.yuque.com/thyname/dart.ui/picturerecorder)。

### drawParagraph()

```dart
void drawParagraph(Paragraph paragraph, Offset offset)
```

将给定 [Paragraph](https://www.yuque.com/thyname/dart.ui/paragraph) 中的文本绘制到此画布中给定的 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 处。

必须先对 [Paragraph](https://www.yuque.com/thyname/dart.ui/paragraph) 对象调用过 [Paragraph.layout]。

要对齐文本,请在传递给 [ParagraphBuilder.new] 构造函数的 [ParagraphStyle](https://www.yuque.com/thyname/dart.ui/paragraphstyle) 对象上设置 `textAlign`。更多详情请参阅 [TextAlign](https://www.yuque.com/thyname/dart.ui/textalign) 以及 [ParagraphStyle.new] 处的讨论。

如果文本为左对齐或两端对齐,左边距将位于 `offset` 参数的 [Offset.dx] 坐标所指定的位置。

如果文本为右对齐或两端对齐,右边距将位于通过把传递给 [Paragraph.layout] 的 [ParagraphConstraints.width] 加到 `offset` 参数的 [Offset.dx] 坐标上所得到的位置。

如果文本为居中对齐,居中轴将位于通过把传递给 [Paragraph.layout] 的 [ParagraphConstraints.width] 的一半加到 `offset` 参数的 [Offset.dx] 坐标上所得到的位置。

### drawPoints()

```dart
void drawPoints(PointMode pointMode, List<Offset> points, Paint paint)
```

根据给定的 [PointMode](https://www.yuque.com/thyname/dart.ui/pointmode) 绘制一系列点。

`points` 参数被解释为相对于原点的偏移量。

`paint` 用于每个点([PointMode.points])或线条([PointMode.lines] 或 [PointMode.polygon]),并忽略 [Paint.style]。

另请参阅:

- [drawRawPoints],该方法将 `points` 作为 [Float32List](https://www.yuque.com/thyname/dart.typed_data/float32list) 而非 [List<Offset>] 接收。

### drawRawPoints()

```dart
void drawRawPoints(PointMode pointMode, Float32List points, Paint paint)
```

根据给定的 [PointMode](https://www.yuque.com/thyname/dart.ui/pointmode) 绘制一系列点。

`points` 参数被解释为一系列浮点数对的列表,其中每一对分别表示相对于原点的 x 和 y 偏移量。

`paint` 用于每个点([PointMode.points])或线条([PointMode.lines] 或 [PointMode.polygon]),并忽略 [Paint.style]。

另请参阅:

- [drawPoints],该方法将 `points` 作为 [List<Offset>] 而非 [List<Float32List>] 接收。

### drawVertices()

```dart
void drawVertices(Vertices vertices, BlendMode blendMode, Paint paint)
```

将一组 [Vertices](https://www.yuque.com/thyname/dart.ui/vertices) 作为一个或多个三角形绘制到画布上。

[Paint.color] 属性指定用于这些三角形的默认颜色。

如果设置了 [Paint.shader] 属性,则会完全覆盖该颜色,并将其替换为指定的 [ImageShader](https://www.yuque.com/thyname/dart.ui/imageshader)、[Gradient](https://www.yuque.com/thyname/dart.ui/gradient) 或其他着色器所提供的颜色。

`blendMode` 参数用于控制 `vertices` 中的颜色应如何与 `paint` 中的颜色相结合。如果 `vertices` 中未指定颜色,则 `blendMode` 不起作用。如果 `vertices` 中包含颜色,则从 `paint` 的 [Paint.shader] 或 [Paint.color] 中取出的颜色会使用 `blendMode` 参数与 `vertices` 中指定的颜色进行混合。就此混合而言,`paint` 参数提供的颜色被视为源,`vertices` 提供的颜色被视为目标。[BlendMode.dst] 会忽略 `paint`,仅使用 `vertices` 的颜色;[BlendMode.src] 会忽略 `vertices` 的颜色,仅使用 `paint` 中的颜色。

所有参数都不能为 null。

另请参阅:

- [Vertices.new],用于创建一组要在画布上绘制的顶点。
- [Vertices.raw],使用类型化数据列表而非未编码列表来创建顶点。
- [paint],图像着色器可用于在三角形网格上绘制图像。

### drawAtlas()

```dart
void drawAtlas(Image atlas, List<RSTransform> transforms, List<Rect> rects, List<Color>? colors, BlendMode? blendMode, Rect? cullRect, Paint paint)
```

将一张图像(即 [atlas])的多个部分绘制到画布上。

当你需要将一张图像的多个部分绘制到画布上时(例如使用精灵图或进行缩放),此方法可以带来性能优化。它比多次调用 [drawImageRect] 更高效,并提供了更多功能,可以通过单独的旋转或缩放对每个图像部分进行独立变换,以及使用纯色对这些部分进行混合或调制。

该方法接受一个 [Rect](https://www.yuque.com/thyname/dart.ui/rect) 对象列表,每个 [Rect](https://www.yuque.com/thyname/dart.ui/rect) 都定义了 [atlas] 图像中要独立绘制的一部分。每个 [Rect](https://www.yuque.com/thyname/dart.ui/rect) 都与 [transforms] 列表中的一个 [RSTransform](https://www.yuque.com/thyname/dart.ui/rstransform) 条目相关联,该条目定义了绘制该图像部分时所使用的位置、旋转和(统一)缩放。每个 [Rect](https://www.yuque.com/thyname/dart.ui/rect) 还可以关联一个可选的 [Color](https://www.yuque.com/thyname/dart.ui/color),该颜色会在使用 [blendMode] 将结果混合到画布之前,先与关联的图像部分进行合成。整个操作可分解为:

- 使用 [blendMode] 参数,将 [rects] 参数中某一条目所指定的图像矩形部分,与 [colors] 列表中与之关联的条目进行混合(如果指定了颜色)。在此步骤中,图像部分被视为该操作的源,关联的颜色被视为目标。
- 使用 [transforms] 列表中关联条目所表示的平移、旋转和缩放属性,并结合 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 对象的属性,将第一步的结果混合到画布上。

如果需要将每个图像部分与颜色混合的第一阶段操作,则 [colors] 和 [blendMode] 参数都不能为 null,并且 [colors] 列表中必须为每个图像部分提供一个条目。如果不需要该阶段,则 [colors] 参数可以为 null 或空列表,[blendMode] 参数也可以为 null。

可选的 [cullRect] 参数可以提供 atlas 所有组件所渲染坐标的边界估计值,用于与裁剪进行比较,以便在不相交时快速拒绝该操作。

以下是一个使用示例,展示如何在没有旋转或缩放的情况下,从单个精灵图集中渲染多个精灵:

```dart
class Sprite {
  Sprite(this.index, this.center);
  int index;
  Offset center;
}

class MyPainter extends CustomPainter {
  MyPainter(this.spriteAtlas, this.allSprites);

  // assume spriteAtlas contains N 10x10 sprites side by side in a (N*10)x10 image
  ui.Image spriteAtlas;
  List<Sprite> allSprites;

  @override
  void paint(Canvas canvas, Size size) {
    Paint paint = Paint();
    canvas.drawAtlas(spriteAtlas, <RSTransform>[
      for (final Sprite sprite in allSprites)
        RSTransform.fromComponents(
          rotation: 0.0,
          scale: 1.0,
          // Center of the sprite relative to its rect
          anchorX: 5.0,
          anchorY: 5.0,
          // Location at which to draw the center of the sprite
          translateX: sprite.center.dx,
          translateY: sprite.center.dy,
        ),
    ], <Rect>[
      for (final Sprite sprite in allSprites)
        Rect.fromLTWH(sprite.index * 10.0, 0.0, 10.0, 10.0),
    ], null, null, null, paint);
  }

  // ...
}
```

以下是另一个使用示例,展示如何渲染带有可选透明度和旋转的精灵:

```dart
class Sprite {
  Sprite(this.index, this.center, this.alpha, this.rotation);
  int index;
  Offset center;
  int alpha;
  double rotation;
}

class MyPainter extends CustomPainter {
  MyPainter(this.spriteAtlas, this.allSprites);

  // assume spriteAtlas contains N 10x10 sprites side by side in a (N*10)x10 image
  ui.Image spriteAtlas;
  List<Sprite> allSprites;

  @override
  void paint(Canvas canvas, Size size) {
    Paint paint = Paint();
    canvas.drawAtlas(spriteAtlas, <RSTransform>[
      for (final Sprite sprite in allSprites)
        RSTransform.fromComponents(
          rotation: sprite.rotation,
          scale: 1.0,
          // Center of the sprite relative to its rect
          anchorX: 5.0,
          anchorY: 5.0,
          // Location at which to draw the center of the sprite
          translateX: sprite.center.dx,
          translateY: sprite.center.dy,
        ),
    ], <Rect>[
      for (final Sprite sprite in allSprites)
        Rect.fromLTWH(sprite.index * 10.0, 0.0, 10.0, 10.0),
    ], <Color>[
      for (final Sprite sprite in allSprites)
        Colors.white.withAlpha(sprite.alpha),
    ], BlendMode.srcIn, null, paint);
  }

  // ...
}
```

[transforms] 和 [rects] 列表的长度必须相等;如果 [colors] 参数不为 null,则它必须为空或与另外两个列表的长度相同。

另请参阅:

- [drawRawAtlas],该方法以类型化数据列表而非对象的形式接收参数。

### drawRawAtlas()

```dart
void drawRawAtlas(Image atlas, Float32List rstTransforms, Float32List rects, Int32List? colors, BlendMode? blendMode, Rect? cullRect, Paint paint)
```

将一张图像(即 [atlas])的多个部分绘制到画布上。

当你需要将一张图像的多个部分绘制到画布上时(例如使用精灵图或进行缩放),此方法可以带来性能优化。它比多次调用 [drawImageRect] 更高效,并提供了更多功能,可以通过单独的旋转或缩放对每个图像部分进行独立变换,以及使用纯色对这些部分进行混合或调制。由于参数中的数据已按可被渲染代码直接使用的格式打包,因此该方法也比 [drawAtlas] 更高效。

有关此方法如何使用其参数绘制到画布上的完整说明,请参阅 [drawAtlas] 方法的描述。

[rstTransforms] 参数被解释为一系列四元组的列表,每个四元组为([RSTransform.scos]、[RSTransform.ssin]、[RSTransform.tx]、[RSTransform.ty])。

[rects] 参数被解释为一系列四元组的列表,每个四元组为([Rect.left]、[Rect.top]、[Rect.right]、[Rect.bottom])。

[colors] 参数可以为 null,它被解释为一系列 32 位颜色的列表,其打包方式与 [Color.value] 相同。如果 [colors] 参数不为 null,则 [blendMode] 参数也不能为 null。

以下是一个使用示例,展示如何在没有旋转或缩放的情况下,从单个精灵图集中渲染多个精灵:

```dart
class Sprite {
  Sprite(this.index, this.center);
  int index;
  Offset center;
}

class MyPainter extends CustomPainter {
  MyPainter(this.spriteAtlas, this.allSprites);

  // assume spriteAtlas contains N 10x10 sprites side by side in a (N*10)x10 image
  ui.Image spriteAtlas;
  List<Sprite> allSprites;

  @override
  void paint(Canvas canvas, Size size) {
    // For best advantage, these lists should be cached and only specific
    // entries updated when the sprite information changes. This code is
    // illustrative of how to set up the data and not a recommendation for
    // optimal usage.
    Float32List rectList = Float32List(allSprites.length * 4);
    Float32List transformList = Float32List(allSprites.length * 4);
    for (int i = 0; i < allSprites.length; i++) {
      Sprite sprite = allSprites[i];
      final double rectX = sprite.index * 10.0;
      rectList[i * 4 + 0] = rectX;
      rectList[i * 4 + 1] = 0.0;
      rectList[i * 4 + 2] = rectX + 10.0;
      rectList[i * 4 + 3] = 10.0;

      // This example sets the RSTransform values directly for a common case of no
      // rotations or scales and just a translation to position the atlas entry. For
      // more complicated transforms one could use the RSTransform class to compute
      // the necessary values or do the same math directly.
      transformList[i * 4 + 0] = 1.0;
      transformList[i * 4 + 1] = 0.0;
      transformList[i * 4 + 2] = sprite.center.dx - 5.0;
      transformList[i * 4 + 3] = sprite.center.dy - 5.0;
    }
    Paint paint = Paint();
    canvas.drawRawAtlas(spriteAtlas, transformList, rectList, null, null, null, paint);
  }

  // ...
}
```

以下是另一个使用示例,展示如何渲染带有可选透明度和旋转的精灵:

```dart
class Sprite {
  Sprite(this.index, this.center, this.alpha, this.rotation);
  int index;
  Offset center;
  int alpha;
  double rotation;
}

class MyPainter extends CustomPainter {
  MyPainter(this.spriteAtlas, this.allSprites);

  // assume spriteAtlas contains N 10x10 sprites side by side in a (N*10)x10 image
  ui.Image spriteAtlas;
  List<Sprite> allSprites;

  @override
  void paint(Canvas canvas, Size size) {
    // For best advantage, these lists should be cached and only specific
    // entries updated when the sprite information changes. This code is
    // illustrative of how to set up the data and not a recommendation for
    // optimal usage.
    Float32List rectList = Float32List(allSprites.length * 4);
    Float32List transformList = Float32List(allSprites.length * 4);
    Int32List colorList = Int32List(allSprites.length);
    for (int i = 0; i < allSprites.length; i++) {
      Sprite sprite = allSprites[i];
      final double rectX = sprite.index * 10.0;
      rectList[i * 4 + 0] = rectX;
      rectList[i * 4 + 1] = 0.0;
      rectList[i * 4 + 2] = rectX + 10.0;
      rectList[i * 4 + 3] = 10.0;

      // This example uses an RSTransform object to compute the necessary values for
      // the transform using a factory helper method because the sprites contain
      // rotation values which are not trivial to work with. But if the math for the
      // values falls out from other calculations on the sprites then the values could
      // possibly be generated directly from the sprite update code.
      final RSTransform transform = RSTransform.fromComponents(
        rotation: sprite.rotation,
        scale: 1.0,
        // Center of the sprite relative to its rect
        anchorX: 5.0,
        anchorY: 5.0,
        // Location at which to draw the center of the sprite
        translateX: sprite.center.dx,
        translateY: sprite.center.dy,
      );
      transformList[i * 4 + 0] = transform.scos;
      transformList[i * 4 + 1] = transform.ssin;
      transformList[i * 4 + 2] = transform.tx;
      transformList[i * 4 + 3] = transform.ty;

      // This example computes the color value directly, but one could also compute
      // an actual Color object and use its Color.value getter for the same result.
      // Since we are using BlendMode.srcIn, only the alpha component matters for
      // these colors which makes this a simple shift operation.
      colorList[i] = sprite.alpha << 24;
    }
    Paint paint = Paint();
    canvas.drawRawAtlas(spriteAtlas, transformList, rectList, colorList, BlendMode.srcIn, null, paint);
  }

  // ...
}
```

另请参阅:

- [drawAtlas],该方法以对象而非类型化数据列表的形式接收参数。

### drawShadow()

```dart
void drawShadow(Path path, Color color, double elevation, bool transparentOccluder)
```

为表示给定 Material 高度的 [Path](https://www.yuque.com/thyname/dart.ui/path) 绘制阴影。

如果遮挡对象不是不透明的,则 `transparentOccluder` 参数应为 true。

参数不能为 null。

# PictureEventCallback

```dart
typedef PictureEventCallback = void Function(Picture picture)
```

[Picture](https://www.yuque.com/thyname/dart.ui/picture) 生命周期事件的签名。

# Picture

```dart
abstract class Picture {}
```

表示一系列已记录图形操作的对象。

要创建 [Picture](https://www.yuque.com/thyname/dart.ui/picture),请使用 [PictureRecorder](https://www.yuque.com/thyname/dart.ui/picturerecorder)。

可以通过 [SceneBuilder.addPicture] 方法,使用 [SceneBuilder](https://www.yuque.com/thyname/dart.ui/scenebuilder) 将 [Picture](https://www.yuque.com/thyname/dart.ui/picture) 放入 [Scene](https://www.yuque.com/thyname/dart.ui/scene) 中。也可以使用 [Canvas.drawPicture] 方法将 [Picture](https://www.yuque.com/thyname/dart.ui/picture) 绘制到 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 中。

### onCreate

```dart
PictureEventCallback? onCreate
```

用于报告图片创建情况的回调。

相比直接使用 [onCreate],更推荐使用 flutter/foundation.dart 中的 [MemoryAllocations](https://www.yuque.com/thyname/flutter.foundation/memoryallocations),因为 [MemoryAllocations](https://www.yuque.com/thyname/flutter.foundation/memoryallocations) 支持多个回调。

### onDispose

```dart
PictureEventCallback? onDispose
```

用于报告图片释放情况的回调。

相比直接使用 [onDispose],更推荐使用 flutter/foundation.dart 中的 [MemoryAllocations](https://www.yuque.com/thyname/flutter.foundation/memoryallocations),因为 [MemoryAllocations](https://www.yuque.com/thyname/flutter.foundation/memoryallocations) 支持多个回调。

### toImage()

```dart
Future<Image> toImage(int width, int height)
```

根据此图片创建一个图像。

返回的图像宽度为 `width` 像素,高度为 `height` 像素。该图片会在 0(左)、0(上)、`width`(右)、`height`(下)所构成的边界内进行光栅化。这些边界之外的内容将被裁剪。

### toImageSync()

```dart
Image toImageSync(int width, int height, {TargetPixelFormat targetFormat = TargetPixelFormat.dontCare})
```

同步创建此图片对应图像的句柄。

{@template dart.ui.painting.Picture.toImageSync} 返回的图像宽度为 [width] 像素,高度为 [height] 像素。该图片会在 0(左)、0(上)、[width](右)、[height](下)所构成的边界内进行光栅化。这些边界之外的内容将被裁剪。

该图像对象是同步创建并返回的,但会异步进行光栅化。如果光栅化失败,当该图像被绘制到 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 时将抛出异常。

如果存在可用的 GPU 上下文,该图像将被创建为驻留于 GPU 中,而不会被复制回主机。这意味着绘制该图像时会更加高效。

如果没有可用的 GPU 上下文,该图像将在 CPU 上进行光栅化。

[targetFormat] 参数指定返回的 [Image](https://www.yuque.com/thyname/dart.ui/image) 的像素格式。如果指定 [TargetPixelFormat.dontCare],则会根据 GPU 的能力自动选择像素格式。{@endtemplate}

### dispose()

```dart
void dispose()
```

释放此对象所使用的资源。调用此方法后,该对象将不可再使用。

### debugDisposed

```dart
bool get debugDisposed
```

此底层图片的引用是否已被 [dispose]。

仅当启用断言时,此属性才会返回有效值,否则不得使用。

### approximateBytesUsed

```dart
int get approximateBytesUsed
```

返回为此对象分配的大致字节数。

该图片的实际大小可能更大,特别是当它包含对图像或其他大型对象的引用时。

# PictureRecorder

```dart
abstract class PictureRecorder {}
```

记录一个包含一系列图形操作的 [Picture](https://www.yuque.com/thyname/dart.ui/picture)。

要开始记录,请构造一个 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 来记录命令。要结束记录,请使用 [PictureRecorder.endRecording] 方法。

## 与 Flutter 框架配合使用

Flutter 框架的 [RendererBinding](https://www.yuque.com/thyname/flutter.rendering/rendererbinding) 提供了一个用于创建 [PictureRecorder](https://www.yuque.com/thyname/dart.ui/picturerecorder) 对象的钩子([RendererBinding.createPictureRecorder]),使测试能够接入场景创建逻辑。在 Flutter 框架的上下文中,如果要创建一个将与 [PictureLayer](https://www.yuque.com/thyname/flutter.rendering/picturelayer) 一起作为 [Scene](https://www.yuque.com/thyname/dart.ui/scene) 一部分使用的 [PictureRecorder](https://www.yuque.com/thyname/dart.ui/picturerecorder) 和 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas),应考虑调用 [RendererBinding.createPictureRecorder],而不是直接调用 [PictureRecorder.new] 构造函数。

当使用画布生成用于其他目的的位图时(例如使用 [Picture.toImage] 生成 PNG 图像),此规则不适用。

### PictureRecorder()

```dart
PictureRecorder()
```

创建一个新的空闲 PictureRecorder。要将其与 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 关联并开始记录,请将此 [PictureRecorder](https://www.yuque.com/thyname/dart.ui/picturerecorder) 传递给 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 构造函数。

### isRecording

```dart
bool get isRecording
```

此对象当前是否正在记录命令。

具体而言,如果已创建用于记录命令的 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 对象,且尚未通过调用 [endRecording] 结束记录,则此属性返回 true;如果此 [PictureRecorder](https://www.yuque.com/thyname/dart.ui/picturerecorder) 尚未与任何 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 关联,或者已经调用过 [endRecording] 方法,则返回 false。

### endRecording()

```dart
Picture endRecording()
```

结束图形操作的记录。

返回一个包含迄今为止已记录的图形操作的图片。调用此函数后,图片记录器和画布对象都将失效,无法继续使用。

# Shadow

```dart
class Shadow {}
```

单个阴影。

多个阴影会在 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 中叠加在一起。

### Shadow()

```dart
Shadow({Color color = const Color(_kColorDefault), Offset offset = Offset.zero, double blurRadius = 0.0})
```

构造一个阴影。

默认阴影是一个偏移量为零、模糊半径为零的黑色阴影。默认阴影应完全被投射阴影的元素覆盖,因而不可见。

透明度应通过 [color] 的 alpha 值进行调整。

由于合成多个半透明对象不满足交换律,因此阴影的顺序会影响最终效果。

### color

```dart
Color color
```

阴影将使用的绘制颜色。

阴影是直接合成在基础画布之上的形状,并不代表光学遮挡。

### offset

```dart
Offset offset
```

阴影相对于投射该阴影的元素的位移。

正的 x/y 偏移量会使阴影向右下方移动,而负的偏移量会使阴影向左上方移动。这些偏移量是相对于投射该阴影的元素的位置而言的。

### blurRadius

```dart
double blurRadius
```

与阴影形状进行卷积的高斯函数的标准差。

### convertRadiusToSigma()

```dart
double convertRadiusToSigma(double radius)
```

将以像素为单位的模糊半径转换为 sigma 值。

参见 [MaskFilter.blur] 的 sigma 参数。

### blurSigma

```dart
double get blurSigma
```

以 sigma(而非逻辑像素)表示的 [blurRadius]。

参见 [MaskFilter.blur] 的 sigma 参数。

### toPaint()

```dart
Paint toPaint()
```

创建与此阴影描述相对应的 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 对象。

[offset] 不会体现在 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 对象中。为了同时兼顾此偏移量,应在使用此 [Paint](https://www.yuque.com/thyname/dart.ui/paint) 填充形状之前,先将该形状按 [offset] 进行平移。

此类不提供禁用阴影的方式,以避免阴影模糊渲染出现不一致的情况,这主要是为了降低测试的不稳定性。若需要该功能,应在子类中重写 [toPaint]。

### scale()

```dart
Shadow scale(double factor)
```

返回一个新的阴影,其 [offset] 和 [blurRadius] 均按给定的系数进行缩放。

### lerp()

```dart
Shadow? lerp(Shadow? a, Shadow? b, double t)
```

在两个阴影之间进行线性插值。

如果其中一个阴影为 null,则此函数会从一个阴影进行线性插值,该阴影的颜色与另一个阴影相同,但偏移量和 blurRadius 均为零。

{@template dart.ui.shadow.lerp} `t` 参数表示时间线上的位置,0.0 表示插值尚未开始,返回 `a`(或与 `a` 等效的值);1.0 表示插值已经完成,返回 `b`(或与 `b` 等效的值);介于两者之间的值则表示插值处于 `a` 与 `b` 之间时间线上的相应位置。该插值可以外推到 0.0 和 1.0 的范围之外,因此小于 0 或大于 1.0 的值也是有效的(例如 [Curves.elasticInOut] 等曲线就很容易生成此类值)。

`t` 的值通常来自 [Animation<double>],例如 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)。{@endtemplate}

### lerpList()

```dart
List<Shadow>? lerpList(List<Shadow>? a, List<Shadow>? b, double t)
```

在两个阴影列表之间进行线性插值。

如果两个列表长度不同,多出的项会与 null 进行插值。

{@macro dart.ui.shadow.lerp}

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

# ImmutableBuffer

```dart
base class ImmutableBuffer extends NativeFieldWrapperClass1 {}
```

由引擎管理的只读字节缓冲区句柄。

该对象的创建者负责在不再需要时调用 [dispose]。

### fromUint8List()

```dart
Future<ImmutableBuffer> fromUint8List(Uint8List list)
```

从 [Uint8List](https://www.yuque.com/thyname/dart.typed_data/uint8list) 创建一份适合引擎内部使用的数据副本。

### fromAsset()

```dart
Future<ImmutableBuffer> fromAsset(String assetKey)
```

使用键为 [assetKey] 的资源创建一个缓冲区。

如果该资源不存在,则抛出 [Exception](https://www.yuque.com/thyname/dart.core/exception)。

### fromFilePath()

```dart
Future<ImmutableBuffer> fromFilePath(String path)
```

使用路径为 [path] 的文件创建一个缓冲区。

如果该资源不存在,则抛出 [Exception](https://www.yuque.com/thyname/dart.core/exception)。

### length

```dart
int get length
```

底层数据的长度,以字节为单位。

### debugDisposed

```dart
bool get debugDisposed
```

是否已调用过 [dispose]。

此属性只能在启用断言时使用,否则将会抛出异常。

### dispose()

```dart
void dispose()
```

释放此对象所使用的资源。调用此方法后,该对象将不可再使用。

如果此对象所分配的底层内存仍被其他尚未释放的对象所需要,则该内存会在此调用之后继续保留。例如,一个尚未被释放的 [ImageDescriptor](https://www.yuque.com/thyname/dart.ui/imagedescriptor) 即使在此缓冲区已被释放后,仍可能保留对该缓冲区内存的引用。要释放该内存,需要释放所有可能仍持有该内存的资源。

# ImageDescriptor

```dart
abstract class ImageDescriptor {}
```

可通过 [Codec](https://www.yuque.com/thyname/dart.ui/codec) 转换为 [Image](https://www.yuque.com/thyname/dart.ui/image) 的数据描述符。

使用此类可以在解码图像数据之前确定其高度、宽度和字节大小。

### ImageDescriptor.raw()

```dart
ImageDescriptor.raw(ImmutableBuffer buffer, {required int width, required int height, int? rowBytes, required PixelFormat pixelFormat})
```

根据原始图像像素创建一个图像描述符。

`pixels` 参数是像素数据。这些数据按照 `pixelFormat` 所描述的顺序以字节形式打包,然后按行分组,先从左到右,再从上到下。

`rowBytes` 参数是数据缓冲区中每行像素所占用的字节数。如果未指定,则默认为 `width` 乘以所提供 `format` 中每个像素的字节数。

### encoded()

```dart
Future<ImageDescriptor> encoded(ImmutableBuffer buffer)
```

根据受支持格式的编码数据创建一个图像描述符。

### width

```dart
int get width
```

图像的宽度,以像素为单位。

在 Web 平台上,此属性仅对 [raw] 图像提供支持。

### height

```dart
int get height
```

图像的高度,以像素为单位。

在 Web 平台上,此属性仅对 [raw] 图像提供支持。

### bytesPerPixel

```dart
int get bytesPerPixel
```

图像中每个像素所占的字节数。

在 Web 平台上,此属性仅对 [raw] 图像提供支持。

### dispose()

```dart
void dispose()
```

释放此对象所使用的资源。调用此方法后,该对象将不可再使用。

此调用不能作为叶子调用,因为该原生函数会调用 Dart API(Dart_SetNativeInstanceField)。

### instantiateCodec()

```dart
Future<Codec> instantiateCodec({int? targetWidth, int? targetHeight, TargetPixelFormat targetFormat = TargetPixelFormat.dontCare})
```

创建一个适合将缓冲区中的数据解码为 [Image](https://www.yuque.com/thyname/dart.ui/image) 的 [Codec](https://www.yuque.com/thyname/dart.ui/codec) 对象。

如果只指定了 targetWidth 或 targetHeight 中的一个,另一个维度将根据所提供维度的宽高比进行缩放。

如果 targetWidth 或 targetHeight 中任意一个小于或等于零,则会被视为 null 处理。

# PictureRasterizationException

```dart
class PictureRasterizationException implements Exception {}
```

当绘制通过 [Picture.toImageSync] 创建、且处于无效状态的 [Image](https://www.yuque.com/thyname/dart.ui/image) 时,由 [Canvas.drawImage] 及相关方法抛出的异常。

如果请求的图像尺寸超过了 GPU 所允许的最大 2D 纹理尺寸,或者在请求光栅化时没有可用的 GPU surface 或上下文,则可能会抛出此异常。

### message

```dart
String message
```

包含失败详情的字符串。

### stack

```dart
StackTrace? stack
```

如果可用,则为调用 [Picture.toImageSync] 时的堆栈跟踪。
