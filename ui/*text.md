# kTextHeightNone

```dart
double kTextHeightNone
```

一个 [TextStyle.height] 值，表示文本范围应采用字体所定义的高度，该高度可能与 [TextStyle.fontSize] 的高度不完全一致。

# FontStyle

```dart
enum FontStyle {}
```

是否使用字体的斜体字形变体。

一些现代字体允许以更精细的方式选择此项。详情参见 [FontVariation.italic]。

斜体（Italic）与倾斜字形不同。若要控制字形的倾斜角度，请考虑使用 [FontVariation.slant] 字体特性。

使用正体（"Roman"）字形。

使用具有更明显角度的字形，通常呈现草书风格（"斜体"）。

# FontWeight

```dart
class FontWeight {}
```

用于绘制文本的字形粗细。

取值范围必须在 1 到 1000 之间。

字体通常采用 9 级刻度进行分级，出于历史原因，使用名称 100 到 900。在 Flutter 中，这些级别被命名为 `w100` 到 `w900`，其常规含义如下：

- [w100]：极细（Thin），最细的字重。

- [w200]：特细（Extra light）。

- [w300]：细体（Light）。

- [w400]：常规（Normal）。常量 [FontWeight.normal] 是该值的别名。

- [w500]：中等（Medium）。

- [w600]：半粗体（Semi-bold）。

- [w700]：粗体（Bold）。常量 [FontWeight.bold] 是该值的别名。

- [w800]：特粗体（Extra-bold）。

- [w900]：黑体（Black），最粗的字重。

例如，名为 "Roboto Medium" 的字体通常以名称为 "Roboto"、字重为 [FontWeight.w500] 的字体形式对外提供。

一些现代字体允许以任意增量调整字重。使用这些字体时，应用程序可以指定使用非预定义值构造的 [FontWeight](https://www.yuque.com/thyname/dart.ui/fontweight) 实例。对于这些字体，[FontWeight](https://www.yuque.com/thyname/dart.ui/fontweight) 将设置 `wght` 轴的值（其效果与使用 [FontVariation.weight] 显式设置该属性相同）。

### FontWeight()

```dart
FontWeight(int value)
```

创建一个 [FontWeight](https://www.yuque.com/thyname/dart.ui/fontweight) 对象，可将其添加到 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 中以选择字体字形的粗细。

### index

```dart
int get index
```

此字重的编码整数值。

### value

```dart
int value
```

此字重的粗细数值。

### w100

```dart
FontWeight w100
```

极细，最不粗。

### w200

```dart
FontWeight w200
```

特细。

### w300

```dart
FontWeight w300
```

细体。

### w400

```dart
FontWeight w400
```

常规 / 正常 / 朴素。

### w500

```dart
FontWeight w500
```

中等。

### w600

```dart
FontWeight w600
```

半粗体。

### w700

```dart
FontWeight w700
```

粗体。

### w800

```dart
FontWeight w800
```

特粗体。

### w900

```dart
FontWeight w900
```

黑体，最粗。

### normal

```dart
FontWeight normal
```

默认字重。

### bold

```dart
FontWeight bold
```

一种比常规字重更粗的常用字重。

### values

```dart
List<FontWeight> values
```

所有字重的列表。

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### lerp()

```dart
FontWeight? lerp(FontWeight? a, FontWeight? b, double t)
```

在两个字重之间进行线性插值。

如果 `a` 和 `b` 都为 null，则此方法返回 null。否则，`a` 或 `b` 的任何 null 值都会被解释为等同于 [normal]（即 [w400]）。

参数 `t` 表示时间轴上的位置，0.0 表示插值尚未开始，返回 `a`（或等同于 `a` 的值）；1.0 表示插值已完成，返回 `b`（或等同于 `b` 的值）；介于两者之间的值表示插值处于 `a` 与 `b` 之间时间轴上的相应位置。插值可以外推超出 0.0 和 1.0 的范围，因此负值和大于 1.0 的值都是有效的（例如通过 [Curves.elasticInOut] 等曲线可以轻易生成这类值）。结果会被限制在 [w100]–[w900] 范围内。

`t` 的取值通常来自 [Animation<double>]，例如 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)。

### toString()

```dart
String toString()
```

# FontFeature

```dart
class FontFeature {}
```

影响字体中字形选择的特性标签和数值。

不同字体支持不同的特性。可以考虑使用诸如 <https://wakamaifondue.com/> 之类的工具来检查你的字体，以确定有哪些可用特性。

{@tool sample} 此示例展示了多种 OpenType 字体特性的用法，包括小型大写字母（Small Caps，通过 "smcp" 代码手动选择）、旧式数字、分数连字以及风格集。

** 代码参见 examples/api/lib/ui/text/font_feature.0.dart ** {@end-tool}

一些字体还支持连续的字体变体；参见 [FontVariation](https://www.yuque.com/thyname/dart.ui/fontvariation) 类。

另请参见：

- <https://en.wikipedia.org/wiki/List_of_typographic_features>，维基百科对这些排版特性的说明。

- <https://docs.microsoft.com/en-us/typography/opentype/spec/featuretags>，微软维护的这些特性的注册表。

### FontFeature()

```dart
FontFeature(String feature, [int value = 1])
```

创建一个 [FontFeature](https://www.yuque.com/thyname/dart.ui/fontfeature) 对象，可将其添加到 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 中以改变引擎在渲染文本时选择字形的方式。

`feature` 是标识该特性的四字符标签。这些标签由 OpenType 等字体格式所规定。

`value` 是该特性将被设置成的值。其行为取决于具体特性。许多特性都是布尔标志，取值可以是 1（启用时）或 0（禁用时）。

参见 <https://docs.microsoft.com/en-us/typography/opentype/spec/featuretags>

### FontFeature.enable()

```dart
FontFeature.enable(String feature)
```

创建一个用于启用具有给定标签的特性的 [FontFeature](https://www.yuque.com/thyname/dart.ui/fontfeature) 对象。

### FontFeature.disable()

```dart
FontFeature.disable(String feature)
```

创建一个用于禁用具有给定标签的特性的 [FontFeature](https://www.yuque.com/thyname/dart.ui/fontfeature) 对象。

### FontFeature.alternative()

```dart
FontFeature.alternative(int value)
```

访问替代字形。（`aalt`）

此特性为范围内的字形选择给定的字形变体。

{@tool sample} Raleway 字体支持多种替代字形。下面的代码展示了如何选择特定的字形。当 `aalt` 设置为默认值 0 时，使用正常字形。当值为非零时，Raleway 会将小写字母替换为小型大写字母。当值为 2 时，小写字母 "a" 会变为无衬线的 "a"，而小写字母 "t" 则变为竖线而非带曲线的形态。通过（使用 [widgets.Text.rich]）针对文本中的特定字母进行处理，可以实现对每个字形所需的渲染效果。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_aalt.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_alternative.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_ae#aalt>

### FontFeature.alternativeFractions()

```dart
FontFeature.alternativeFractions()
```

使用替代连字表示分数。（`afrc`）

启用此特性后（且字体支持该特性时），由 U+002F 斜线字符（/）或 U+2044 分数斜线（⁄）分隔的数字序列会被替换为表示相应分数的连字。这些连字可能与 [FontFeature.fractions] 特性所使用的连字不同。

此特性会覆盖所有其他特性。

{@tool sample} Ubuntu Mono 字体支持 `afrc` 特性。它使斜线前的数字变为上标，斜线后的数字变为下标。这与 [FontFeature.fractions] 所产生的效果形成对比。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_afrc.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_alternative_fractions.0.dart ** {@end-tool}

另请参见：

- [FontFeature.fractions]，具有类似（但不同）效果的特性。
- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_ae#afrc>

### FontFeature.contextualAlternates()

```dart
FontFeature.contextualAlternates()
```

启用上下文替代字形。（`calt`）

启用此特性后，特定字形可能会根据附近文本被替换为替代字形。

{@tool sample} Barriecito 字体支持 `calt` 特性。它使某些字母在与自身其他实例靠近时使用不同的字形，从而让字形看起来更具变化性，而不是每个字母总是使用某个固定字形。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_calt.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_contextual_alternates.0.dart ** {@end-tool}

另请参见：

- [FontFeature.randomize]，一种较少被支持但效果更强大的类似方式。
- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_ae#calt>

### FontFeature.caseSensitiveForms()

```dart
FontFeature.caseSensitiveForms()
```

启用大小写敏感形式。（`case`）

某些字形，例如括号或运算符，通常设计为适配混合大小写乃至以小写字母为主的文本。当这些字形靠近大写字母串时，会显得有点偏离中心。

此特性在字体支持的情况下，会使这些字形略微偏移或做其他调整，以便与大写字母组合出更美观的效果。

{@tool sample} Piazzolla 字体支持 `case` 特性。它会使圆括号、方括号、花括号、书名号、斜线、项目符号以及其他一些字形（下方未展示）略微上移，使大写字母看起来居中对齐。禁用该特性时，这些字形针对小写字母进行了优化，因此大写字母相对标点符号会显得偏高。

这种差异非常细微，在比较方括号与大写字母 A 时可能最为明显。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_case.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_case_sensitive_forms.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_ae#case>

### FontFeature.characterVariant()

```dart
FontFeature.characterVariant(int value)
```

选择字符变体。（`cv01` 至 `cv99`）

字体最多可以有 99 组字符变体，编号从 1 到 99，每组都可以独立启用或禁用。

相关的字符变体通常会被归入由 [FontFeature.stylisticSet] 特性（`ssXX`）控制的风格集中。

{@tool sample} Source Code Pro 字体针对多个字符支持 `cvXX` 特性。在下面的示例中，选择了变体 1（`cv01`）、2（`cv02`）和 4（`cv04`）。变体 1 改变字符 "a" 的渲染方式，变体 2 改变小写字母 "g" 的渲染方式，变体 4 改变小写字母 "i" 和 "l" 的渲染方式。此外还有一些变体（此处未展示）用于控制诸如希腊字母 beta 和 theta 等字符的渲染。

值得注意的是，这可以与风格集进行对比：影响字符 "a" 的风格集同时也会影响 beta，而影响字符 "g" 的风格集同时也会影响 theta 和 delta。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_cvXX.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_character_variant.0.dart ** {@end-tool}

另请参见：

- [FontFeature.stylisticSet]，可一次性选择整组字符变体，而非单个字符变体。
- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_ae#cv01-cv99>

### FontFeature.denominator()

```dart
FontFeature.denominator()
```

将数字显示为分母。（`dnom`）

这通常由字体渲染系统在实现分数（参见 [FontFeature.fractions]）中分母部分的 `frac` 时自动使用。

{@tool sample} Piazzolla 字体支持 `dnom` 特性。它使数字以更小的尺寸渲染，并靠近 EM 框的底部。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_dnom.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_denominator.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_ae#dnom>

### FontFeature.fractions()

```dart
FontFeature.fractions()
```

使用连字表示分数。（`afrc`）

启用此特性后（且字体支持该特性时），由 U+002F 斜线字符（/）或 U+2044 分数斜线（⁄）分隔的数字序列会被替换为表示相应分数的连字。

此特性可能隐含启用 [FontFeature.numerators] 和 [FontFeature.denominator] 特性。

{@tool sample} Ubuntu Mono 字体支持 `frac` 特性。它使斜线周围的数字变为专用的分数字形。这与 [FontFeature.alternativeFractions] 所产生的效果形成对比。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_frac.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_fractions.0.dart ** {@end-tool}

另请参见：

- [FontFeature.alternativeFractions]，具有类似（但不同）效果的特性。
- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_fj#frac>

### FontFeature.historicalForms()

```dart
FontFeature.historicalForms()
```

使用历史形式。（`hist`）

一些字体为随时代演变的字母提供了替代形式。在拉丁字母中，这种情况常见于长形 "s" 或哥特体（Fraktur）的 "k"。此特性会启用这些替代字形。

这不会启用旧式连字，仅启用单字符替代。要启用历史连字，请使用 [FontFeature.historicalLigatures]。

此特性可能会覆盖其他字形替换特性。

{@tool sample} Cardo 字体专门针对字母 "s" 支持 `hist` 特性：它将该字母的出现替换为 U+017F LATIN SMALL LETTER LONG S 所使用的字形。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_historical.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_historical_forms.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_fj#hist>

### FontFeature.historicalLigatures()

```dart
FontFeature.historicalLigatures()
```

使用历史连字。（`hlig`）

一些字体支持如今已不常用、但在历史上曾被普遍使用的连字。此特性会启用这些连字。

例如，"long s" 字形在历史上曾与 "t"、"h" 等字符以单个连字的形式排版。

这不会启用旧式形式，仅启用连字。参见 [FontFeature.historicalForms]，可启用将单个字符替换为其历史替代形式。通常建议同时启用这两项特性，因为连字通常特定地应用于同时具有历史形式的字符。例如，历史形式特性可能会将字符 "s" 替换为 "long s"（ſ）字符，而历史连字特性则可能专门应用于 "long s" 后跟其他字符（如 "t"）的情形。在这类情况下，如果不启用历史形式，连字将只会在显式使用 "long s" 时才生效。

此特性可能会覆盖其他字形替换特性。

{@tool sample} Cardo 字体支持 `hlig` 特性。它为 "VI" 和 "NT" 提供旧式连字，并为涉及 "long s" 的各种组合提供连字。在下面的示例中，历史形式（`hist 1`）和历史连字（`hlig 1`）都被启用，因此，例如 "fish" 会变为 "fiſh"，随后最后两个字符会以连字形式渲染。

类似地，"business" 会被 `hist` 转换为 "buſineſſ"，而 `ſi` 和 `ſſ` 这两组字符对则会被 `hlig` 连接为连字。特别请留意 "business" 中各种组合下字母 "i" 上方点号的位置变化。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_historical.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_historical_ligatures.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_fj#hlig>

### FontFeature.liningFigures()

```dart
FontFeature.liningFigures()
```

使用等高数字（Lining figures）。（`lnum`）

一些字体的数字如同小写拉丁字母一样，同时具有下伸部和上伸部。在某些情况下，尤其是与大写字母搭配时，这会导致美观上的不协调。而等高数字则具有统一的高度，与基线及大写字母的高度对齐。从概念上讲，可以将其视为"大写数字"。

此特性可能与 [FontFeature.oldstyleFigures] 冲突。

{@tool sample} Sorts Mill Goudy 字体支持 `lnum` 特性。它使数字与大写字母更协调地融合。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_lnum.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_lining_figures.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_ko#lnum>

### FontFeature.localeAware()

```dart
FontFeature.localeAware({bool enable = true})
```

使用特定语言区域的字形。（`locl`）

某些字符，尤其是 Unicode 汉字统一表意文字区块中的字符，其呈现方式会因语言区域而异。例如，表示"草"的表意文字（U+8349，草）在繁体中文中顶部线条是断开的，而在简体中文、日语、韩语和越南语中则是连续的。这种变化也存在于其他文字体系中，例如保加利亚语和塞尔维亚语所使用的西里尔字符与俄语的对应字符也有所不同。

某种字体可能默认使用其构建所依据的语言区域的字形形式，但仍支持其他语言区域的替代形式。启用此特性后，将使用语言区域（例如通过 [painting.TextStyle.locale] 指定）来确定在存在特定语言区域替代形式时应使用哪些字形。禁用此特性会使字体渲染忽略语言区域信息，仅使用默认字形。

此特性默认启用。使用 `FontFeature.localeAware(enable: false)` 可禁用语言区域感知功能。（当然，不指定语言区域也会产生同样的效果。）

{@tool sample} Noto Sans CJK 字体针对 CJK 字符支持 `locl` 特性。在此示例中，并未显式使用 `localeAware` 特性，因为它默认已启用。此示例转而展示了如何设置语言区域，从而演示 Noto Sans 如何根据语言区域调整字形形状。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_locl.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_locale_aware.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_ko#locl>
- <https://en.wikipedia.org/wiki/Han_unification>
- <https://en.wikipedia.org/wiki/Cyrillic_script>

### FontFeature.notationalForms()

```dart
FontFeature.notationalForms([int value = 1])
```

为数字显示替代字形（备用标注形式）。（`nalt`）

将用于编号列表（例如 1、2、3……或 a、b、c……）的字形替换为可能更具排版趣味性的标注变体。

字体有时支持多种替代方案，参数用于选择使用哪一组（正整数，或 0 表示禁用该特性）。若未指定，默认使用第 1 组。

{@tool sample} Gothic A1 字体通过 `nalt` 特性支持多组标注变体。

第 1 组改变字形间距。第 2 组为拉丁字母加上括号并将数字缩小为下标。第 3 组为字形加圆圈。第 4 组为数字加括号。第 5 组对数字使用反色圆圈。第 7 组将数字上标化。

下面的代码展示了如何选择第 3 组。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_nalt.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_notational_forms.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_ko#nalt>

### FontFeature.numerators()

```dart
FontFeature.numerators()
```

将数字显示为分子。（`numr`）

这通常由字体渲染系统在实现分数（参见 [FontFeature.fractions]）中分子部分的 `frac` 时自动使用。

{@tool sample} Piazzolla 字体支持 `numr` 特性。它使数字以更小的尺寸渲染，并靠近 EM 框的顶部。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_numr.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_numerators.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_ko#numr>

### FontFeature.oldstyleFigures()

```dart
FontFeature.oldstyleFigures()
```

使用旧式数字。（`onum`）

某些字体拥有数字（例如数字 9）的变体，启用此特性后，这些数字会以下伸至基线以下的形式渲染，而不是完全位于基线之上。如果默认数字为等高数字，则此特性可选择与大小写混排文本更协调的数字。

此特性会覆盖 [FontFeature.slashedZero]，且可能与 [FontFeature.liningFigures] 冲突。

{@tool sample} Piazzolla 字体支持 `onum` 特性。它使数字延伸至基线以下。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_onum.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_oldstyle_figures.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_ko#onum>
- <https://en.wikipedia.org/wiki/Text_figures>

### FontFeature.ordinalForms()

```dart
FontFeature.ordinalForms()
```

为字母字形使用序数形式。（`ordn`）

一些字体拥有专用于数字后表示序数（如 "1st"、"2nd"、"3rd"）的字母字形变体。此特性会启用这些替代字形。

这可能会覆盖其他执行字形替换的特性。

{@tool sample} Piazzolla 字体支持 `ordn` 特性。它使字母字形变小并上标化。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_ordn.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_ordinal_forms.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_ko#ordn>

### FontFeature.proportionalFigures()

```dart
FontFeature.proportionalFigures()
```

使用比例（宽度可变）数字。（`pnum`）

对于同时具有比例数字和表格（等宽）数字的字体，此特性启用比例数字。

此特性与 [FontFeature.tabularFigures] 互斥。

默认行为因字体而异。

{@tool sample} Kufam 字体支持 `pnum` 特性。它使数字变为按比例调整大小，而不是全部宽度相同。在该字体中，这一点在数字 "1" 上尤为明显：通常情况下，在这款无衬线字体中 "1" 带有非常明显的衬线，但启用比例数字后，该数字会变得窄得多。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_pnum.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_proportional_figures.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_pt#pnum>

### FontFeature.randomize()

```dart
FontFeature.randomize()
```

随机化文本中使用的替代形式。（`rand`）

例如，这可以与经过适当准备的手写字体配合使用，为每个字符变化所使用的形式，从而使诸如 "cross-section" 这样的单词在渲染时会使用两种不同的 "c"、两种不同的 "o" 以及三种不同的 "s"。

上下文替代特性（[FontFeature.contextualAlternates]）在一些字体中可产生类似效果，但不依赖随机性。

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_pt#rand>

### FontFeature.stylisticAlternates()

```dart
FontFeature.stylisticAlternates()
```

启用风格化替代形式。（`salt`）

一些字体拥有不与特定用途（例如历史形式、上下文相关的替代形式或连字等）绑定的替代形式。此字体特性会启用这些纯粹的风格化替代形式。

这可能会覆盖其他执行字形替换的特性。

{@tool sample} Source Code Pro 字体支持 `salt` 特性。它会使某些字形呈现不同效果，例如 "a" 和 "g" 字形从常见的双层形式变为更简单的单层形式，美元符号的竖线从不连续变为连续（并倾斜），"0" 的渲染从中间带点变为带斜线。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_salt.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_stylistic_alternates.0.dart ** {@end-tool}

另请参见：

- [FontFeature.contextualAlternates]，用于启用特定上下文中的替代形式。
- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_pt#salt>

### FontFeature.scientificInferiors()

```dart
FontFeature.scientificInferiors()
```

使用科学下标（Scientific inferiors）。（`sinf`）

某些字体拥有数字（例如数字 2）的变体，启用此特性后，会以更适合科学场景（例如化学式）中下标数字（"inferiors"）使用的方式渲染。

这可能会覆盖其他执行字形替换的特性。

{@tool sample} Piazzolla 字体支持 `sinf` 特性。它使数字变小并下标化。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_sinf.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_scientific_inferiors.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_pt#sinf>

### FontFeature.stylisticSet()

```dart
FontFeature.stylisticSet(int value)
```

选择风格集。（`ss01` 至 `ss20`）

字体最多可以有 20 组风格集，编号从 1 到 20，每组都可以独立启用或禁用。

若需要更精细的控制，在一些字体中，单个字符变体也可以通过 [FontFeature.characterVariant] 特性（`cvXX`）来控制。

{@tool sample} Source Code Pro 字体针对多组风格集支持 `ssXX` 特性。在下面的示例中，选择了风格集 2（`ss02`）、3（`ss03`）和 4（`ss04`）。风格集 2 改变字符 "a" 和 beta 字符的渲染方式，风格集 3 改变小写字母 "g"、theta 和 delta 字符，风格集 4 改变小写字母 "i" 和 "l" 字符。

此字体同时支持字符变体（参见 [FontFeature.characterVariant]）。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_ssXX_1.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_stylistic_set.0.dart ** {@end-tool}

{@tool sample} Piazzolla 字体通过 `ssXX` 特性支持更为精致的风格效果。第 1 组将部分拉丁字符转换为罗马数字，第 2 组使部分 ASCII 字符能够组成漂亮的箭头，以此类推。

_这些_ 风格集与字符变体 _并不_ 对应。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_ssXX_2.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_stylistic_set.1.dart ** {@end-tool}

另请参见：

- [FontFeature.characterVariant]，用于选择单个字符变体，而非整组风格集。
- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_pt#ssxx>

### FontFeature.subscripts()

```dart
FontFeature.subscripts()
```

启用下标。（`subs`）

此特性使一些字体将某些字形改为其下标形式。

它通常不会影响所有字形，因此不适合用于将全部文本统一设为下标。

这可能会覆盖其他执行字形替换的特性。

{@tool sample} Piazzolla 字体支持 `subs` 特性。它使数字变小并下标化。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_subs.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_subscripts.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_pt#subs>
- [FontFeature.scientificInferiors]，与此类似但专用于科学场景中的下标。
- [FontFeature.superscripts]，与此类似但用于上标。

### FontFeature.superscripts()

```dart
FontFeature.superscripts()
```

启用上标。（`sups`）

此特性使一些字体将某些字形改为其上标形式。这可能不仅仅是改变位置。例如，数字可能会变为等高数字（参见 [FontFeature.liningFigures]），同时被提升并缩小。

它通常不会影响所有字形，因此不适合用于将全部文本统一设为上标。

这可能会覆盖其他执行字形替换的特性。

{@tool sample} Sorts Mill Goudy 字体支持 `sups` 特性。它使数字变小、上标化，并转换为等高数字（因此高度一致）。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_sups.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_superscripts.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_pt#sups>
- [FontFeature.subscripts]，与此类似但用于下标。

### FontFeature.swash()

```dart
FontFeature.swash([int value = 1])
```

启用花饰字形（Swash glyphs）。（`swsh`）

一些字体在部分字符上拥有精美的装饰笔画。这些装饰以多种形式出现，例如夸张的衬线、长尾、长起笔或其他形式的字符装饰性延伸。

此特性用于启用这些装饰笔画的渲染。一些字体每个字符拥有多种花饰形式；若指定了参数，则用于选择使用哪一种花饰（0 表示完全禁用）。

一些字体拥有数量惊人的替代花饰形式。例如，Adobe 的 Poetica 字体因通过此特性提供多达 63 种不同的 & 符号形式而闻名！

{@tool sample} BioRhyme Expanded 字体专门针对大写字母 "Q"、"R" 字形以及 & 符号支持 `swsh` 特性。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_swsh.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_swash.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_pt#swsh>
- <https://en.wikipedia.org/wiki/Swash_(typography)>

### FontFeature.tabularFigures()

```dart
FontFeature.tabularFigures()
```

使用表格（等宽）数字。（`tnum`）

对于同时具有比例（宽度可变）数字和表格数字的字体，此特性启用表格数字。表格数字是等宽的（宽度全部相同），因此可以在数字表格中对齐。

此特性与 [FontFeature.proportionalFigures] 互斥。

默认行为因字体而异。

{@tool sample} Piazzolla 字体支持 `tnum` 特性。它使数字统一大小，而不是具有不同宽度。在该字体中，这一点在数字 "1" 上尤为明显；启用表格数字后，数字 "1" 的间距会更宽。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_tnum.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_tabular_figures.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_pt#tnum>

### FontFeature.slashedZero()

```dart
FontFeature.slashedZero()
```

使用带斜线的零。（`zero`）

一些字体同时包含圆形的零和带斜线的零。此特性用于启用后一种形式。

此特性会被 [FontFeature.oldstyleFigures] 覆盖。

{@tool sample} Source Code Pro 字体支持 `zero` 特性。它使数字零以带斜线的方式绘制，而不是默认的带点渲染方式。

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/font_feature_zero.png)

** 代码参见 examples/api/lib/ui/text/font_feature.font_feature_slashed_zero.0.dart ** {@end-tool}

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/features_uz#zero>

### feature

```dart
String feature
```

标识此特性效果的标签。必须由 4 个 ASCII 字符（通常为小写字母）组成。

这些特性定义在微软维护的注册表中：<https://docs.microsoft.com/en-us/typography/opentype/spec/featuretags>

### value

```dart
int value
```

分配给此特性的值。

必须为正整数。许多特性是布尔值，接受 0（禁用该特性）或 1（启用该特性）。其他特性具有一个有界的取值范围（对于具有专用构造函数的特性，可能会在此 API 文档中说明，通常也会在官方注册表中记录）。在某些情况下，具体支持的取值范围取决于字体。

另请参见：

- <https://docs.microsoft.com/en-us/typography/opentype/spec/featurelist>

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

# FontVariation

```dart
class FontVariation {}
```

用于自定义可变字体的轴标签和数值。

一些字体是可变字体，可以通过更改字体设计轴的值来生成一系列不同的字体面貌。

例如：

```dart
const TextStyle(fontVariations: <ui.FontVariation>[ui.FontVariation('slnt', -5.0)])
```

字体变体（Font variations）与 [FontFeature](https://www.yuque.com/thyname/dart.ui/fontfeature) 类所暴露的字体特性（Font features）不同。特性可以离散地启用或禁用，而变体则提供连续的控制轴。

另请参见：

- <https://learn.microsoft.com/en-us/typography/opentype/spec/dvaraxisreg#registered-axis-tags>，列出了已注册的轴标签。

- <https://docs.microsoft.com/en-us/typography/opentype/spec/otvaroverview>，字体变体技术概述。

### FontVariation()

```dart
FontVariation(String axis, double value)
```

创建一个 [FontVariation](https://www.yuque.com/thyname/dart.ui/fontvariation) 对象，可将其添加到 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 中以改变字体的可变属性。

`axis` 是标识设计轴的四字符标签。OpenType 列出了[当前已注册的轴标签](https://docs.microsoft.com/en-us/typography/opentype/spec/dvaraxisreg)。

`value` 是该轴将被设置成的值。其行为取决于字体如何实现该轴。

### FontVariation.italic()

```dart
FontVariation.italic(double value)
```

可变字体样式。（`ital`）

在正常与斜体之间调整字体中字形的样式。

取值必须在 0.0（表示正常，或称正体，如同 [FontStyle.normal]）到 1.0（表示完全斜体，如同 [FontStyle.italic]）之间。

这与 [FontVariation.slant] 不同，后者是在不改变字体样式的情况下使字符倾斜。

另请参见：

- <https://learn.microsoft.com/en-us/typography/opentype/spec/dvaraxistag_ital>

### FontVariation.opticalSize()

```dart
FontVariation.opticalSize(double value)
```

视觉尺寸优化。（`opzs`）

改变字体的渲染，使其针对给定文本尺寸进行优化。通常，字体的视觉尺寸会根据字体大小推导得出。

此特性可用于文本代表特定物理字体大小的场合，例如表示印刷版杂志文本的场景，此时其并不对应用于渲染文本的实际字体大小。通过显式设置视觉尺寸，可以固定在文本缩放时可能应用的字体变体。

此特性还可用于平滑动画。如果字体在字体大小调整时会改变其渲染方式，那么在字体大小进行动画变化时可能会出现"抖动"（或者也可以说是 "flutter"）的现象。通过设置固定的视觉尺寸，可以在文本大小进行动画变化时将渲染固定为某种特定样式。

取值必须大于零，以磅（points）为单位解读。一磅为 1/72 英寸，或 1.333 逻辑像素（96/72）。

另请参见：

- <https://learn.microsoft.com/en-us/typography/opentype/spec/dvaraxistag_opsz>

### FontVariation.slant()

```dart
FontVariation.slant(double value)
```

可变字体宽度。（`slnt`）

改变字体中字形的倾斜角度。

取值必须大于 -90.0 且小于 +90.0，表示相对于 "正常"（0.0）的*逆时针*角度。

例如，要使字形向前倾斜 45 度，可使用 `FontVariation.slant(-45.0)`。

这与 [FontVariation.italic] 不同，倾斜（slant）是在不改变字体样式的情况下使字符倾斜。

另请参见：

- <https://learn.microsoft.com/en-us/typography/opentype/spec/dvaraxistag_slnt>

### FontVariation.width()

```dart
FontVariation.width(double value)
```

可变字体宽度。（`wdth`）

改变字体中字形的宽度。

取值必须大于零，没有上限。100.0 表示 "正常" 宽度。较小的值表示 "收缩"（condensed），较大的值表示 "扩展"（extended）。

另请参见：

- <https://learn.microsoft.com/en-us/typography/opentype/spec/dvaraxistag_wdth>

### FontVariation.weight()

```dart
FontVariation.weight(double value)
```

可变字体字重。（`wght`）

应用程序应避免直接使用此项，而应通过指定 [FontWeight](https://www.yuque.com/thyname/dart.ui/fontweight) 来声明字体字重，这会隐式设置此属性。但是，如果为此属性提供了值，则该值将覆盖 [FontWeight](https://www.yuque.com/thyname/dart.ui/fontweight)。

改变字体的笔画粗细。

取值必须在 1 到 1000 之间，其解读方式应与 [FontWeight](https://www.yuque.com/thyname/dart.ui/fontweight) 的取值保持一致。例如，`400` 为 "正常" 字重，`700` 为 "粗体"。

另请参见：

- <https://learn.microsoft.com/en-us/typography/opentype/spec/dvaraxistag_wght>

### axis

```dart
String axis
```

标识设计轴的标签。

轴标签必须由 4 个 ASCII 字符组成。

### value

```dart
double value
```

分配给此设计轴的值。

可用取值的范围取决于该轴的规范。

尽管此属性在此 API 中以 [double](https://www.yuque.com/thyname/dart.core/double)（[binary64](https://en.wikipedia.org/wiki/Double-precision_floating-point_format)）表示，但字体使用定点 16.16 格式来表示字体变体的值。这意味着实际范围为 -32768.0 到约 32767.999985，原则上两个值之间的最小增量约为 0.000015（1/65536）。

遗憾的是，出于技术原因，该值首先会被转换为 [binary32 浮点格式](https://en.wikipedia.org/wiki/Single-precision_floating-point_format)，该格式仅有 24 位精度。这意味着对于 -256.0 到 256.0 范围之外的值，最小增量将大于 OpenType 技术上所支持的数值。在取值范围的极端边缘，最小增量仅约为 ±0.002。

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### lerp()

```dart
FontVariation? lerp(FontVariation? a, FontVariation? b, double t)
```

在两个字体变体之间进行线性插值。

如果两个变体具有不同的轴标签，插值会在 t=0.5 时从一个突然切换到另一个。否则，值会进行插值（参见 [lerpDouble](https://www.yuque.com/thyname/dart.ui/lerpdouble)）。

该值不会被限制在该轴标签的有效取值范围内，但会被限制在字体变体值的总体有效范围内（即有符号 16.16 定点数的范围）。

参数 `t` 表示时间轴上的位置，0.0 表示插值尚未开始，返回 `a`（或等同于 `a` 的值）；1.0 表示插值已完成，返回 `b`（或等同于 `b` 的值）；介于两者之间的值表示插值处于 `a` 与 `b` 之间时间轴上的相应位置。插值可以外推超出 0.0 和 1.0 的范围，因此负值和大于 1.0 的值都是有效的（例如通过 [Curves.elasticInOut] 等曲线可以轻易生成这类值）。

`t` 的取值通常来自 [Animation<double>]，例如 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)。

### toString()

```dart
String toString()
```

# GlyphInfo

```dart
final class GlyphInfo {}
```

段落中一个字符（或一组视觉上相连的字符）的度量信息。

另请参见：

- [Paragraph.getGlyphInfoAt]，用于查找与文本中某个代码单元关联的 [GlyphInfo](https://www.yuque.com/thyname/dart.ui/glyphinfo)。
- [Paragraph.getClosestGlyphInfoForOffset]，用于查找屏幕上距给定 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 最近的字形的 [GlyphInfo](https://www.yuque.com/thyname/dart.ui/glyphinfo)。

### GlyphInfo()

```dart
GlyphInfo(Rect graphemeClusterLayoutBounds, TextRange graphemeClusterCodeUnitRange, TextDirection writingDirection)
```

使用指定的值创建一个 [GlyphInfo](https://www.yuque.com/thyname/dart.ui/glyphinfo)。

### graphemeClusterLayoutBounds

```dart
Rect graphemeClusterLayoutBounds
```

相关字符的布局边界矩形，以段落坐标系表示。

这**并非**紧密贴合字符轮廓的精确边界框。所报告的垂直范围来源于字体度量（而非字形度量），水平范围为该字符的水平前进量（advance）。

### graphemeClusterCodeUnitRange

```dart
TextRange graphemeClusterCodeUnitRange
```

文本中相关字符的 UTF-16 范围。

### writingDirection

```dart
TextDirection writingDirection
```

[GlyphInfo](https://www.yuque.com/thyname/dart.ui/glyphinfo) 内的书写方向。

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

# TextAlign

```dart
enum TextAlign {}
```

是否以及如何在水平方向上对齐文本。

将文本对齐到容器的左边缘。

将文本对齐到容器的右边缘。

将文本在容器中居中对齐。

拉伸以软换行结尾的文本行，使其填满容器的宽度。

以硬换行结尾的行会朝 [start] 边缘对齐。

将文本对齐到容器的前导边缘（leading edge）。

对于从左到右的文本（[TextDirection.ltr]），这是左边缘。

对于从右到左的文本（[TextDirection.rtl]），这是右边缘。

将文本对齐到容器的尾随边缘（trailing edge）。

对于从左到右的文本（[TextDirection.ltr]），这是右边缘。

对于从右到左的文本（[TextDirection.rtl]），这是左边缘。

# TextBaseline

```dart
enum TextBaseline {}
```

用于对齐文本的水平线。

用于对齐拉丁字母字符字形底部的水平线。

此基线常用于拉丁语、希腊语、西里尔语等字母文字。

带下伸部的字符（如 'p'、'g' 或 'y'）会延伸到该线以下。

用于对齐表意文字字符的水平线。

此基线常用于具有统一方形高度的文字体系，如中文、日文、韩文等。

# TextDecoration

```dart
final class TextDecoration {}
```

在文本附近绘制的线性装饰。

### TextDecoration.combine()

```dart
TextDecoration.combine(List<TextDecoration> decorations)
```

创建一个绘制所有给定装饰之并集的装饰。

### maskValue

```dart
int get maskValue
```

表示此装饰的位掩码值。

### contains()

```dart
bool contains(TextDecoration other)
```

此装饰所绘制的装饰内容是否至少与给定装饰一样多。

### none

```dart
TextDecoration none
```

不绘制装饰

### underline

```dart
TextDecoration underline
```

在每行文本下方绘制一条线

### overline

```dart
TextDecoration overline
```

在每行文本上方绘制一条线

### lineThrough

```dart
TextDecoration lineThrough
```

在每行文本中间绘制一条贯穿线

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

# TextDecorationStyle

```dart
enum TextDecorationStyle {}
```

绘制文本装饰所使用的样式

绘制实线

绘制双线

绘制点线

绘制虚线

绘制波浪线

# TextLeadingDistribution

```dart
enum TextLeadingDistribution {}
```

{@macro dart.ui.textLeadingDistribution}

按照字体的上升高度/下降高度（ascent/descent）比例，将文本的[行距](https://en.wikipedia.org/wiki/Leading)按比例分布在文本上方和下方。

{@template dart.ui.leading} 一行文本的行距定义为 `TextStyle.height * TextStyle.fontSize - TextStyle.fontSize`。当未设置 [TextStyle.height] 时，该行文本使用字体自身指定的行距。{@endtemplate}

将文本的["行距"](https://en.wikipedia.org/wiki/Leading)平均分布在文本上方和下方（即在字体的上升部上方和下降部下方平均分布）。

{@macro dart.ui.leading}

当 [TextStyle.height] 小于 1.0 时，行距可能变为负值。

这是 CSS 所使用的默认策略，称为["半行距"](https://www.w3.org/TR/css-inline-3/#half-leading)（half-leading）。

# TextHeightBehavior

```dart
class TextHeightBehavior {}
```

{@template dart.ui.textHeightBehavior} 定义如何在文本上方和下方应用 [TextStyle.height]。

[TextHeightBehavior.applyHeightToFirstAscent] 和 [TextHeightBehavior.applyHeightToLastDescent] 表示 [TextStyle.height] 修饰符是否会应用于相应的度量。默认情况下这两个属性均为 true，[TextStyle.height] 会按正常方式应用。设为 false 时，将使用字体的默认上升高度。

[TextHeightBehavior.leadingDistribution] 决定行距如何分布在文本上方和下方。此属性在 [TextHeightBehavior.applyHeightToFirstAscent] 和 [TextHeightBehavior.applyHeightToLastDescent] 之前生效。

{@endtemplate}

### TextHeightBehavior()

```dart
TextHeightBehavior({bool applyHeightToFirstAscent = true, bool applyHeightToLastDescent = true, TextLeadingDistribution leadingDistribution = TextLeadingDistribution.proportional})
```

创建一个新的 TextHeightBehavior 对象。

- applyHeightToFirstAscent：当 true 时，[TextStyle.height] 修饰符会应用于首行的上升高度。当 false 时，将使用字体的默认上升高度。
- applyHeightToLastDescent：当 true 时，[TextStyle.height] 修饰符会应用于末行的下降高度。当 false 时，将使用字体的默认下降高度。
- leadingDistribution：行距如何分布在文本上方和下方。

所有属性默认均为 true（按正常方式应用高度修饰）。

### applyHeightToFirstAscent

```dart
bool applyHeightToFirstAscent
```

是否将 [TextStyle.height] 修饰符应用于段落中首行的上升高度。

为 true 时，[TextStyle.height] 修饰符会应用于首行的上升高度。为 false 时，将使用字体的默认上升高度，[TextStyle.height] 将不会影响首行的上升高度。

此属性仅在指定了非 null 的 [TextStyle.height] 时生效。

默认为 true（按正常方式应用高度修饰）。

### applyHeightToLastDescent

```dart
bool applyHeightToLastDescent
```

是否将 [TextStyle.height] 修饰符应用于段落中末行的下降高度。

为 true 时，[TextStyle.height] 修饰符会应用于末行的下降高度。为 false 时，将使用字体的默认下降高度，[TextStyle.height] 将不会影响末行的下降高度。

此属性仅在指定了非 null 的 [TextStyle.height] 时生效。

默认为 true（按正常方式应用高度修饰）。

### leadingDistribution

```dart
TextLeadingDistribution leadingDistribution
```

{@template dart.ui.textLeadingDistribution} [行距](https://en.wikipedia.org/wiki/Leading)如何分布在文本上方和下方。

当未指定 [TextStyle.height] 时不影响布局。例如，当 [TextLeadingDistribution.even] 与远小于 1.0 的 [TextStyle.height] 一起使用时，行距可能变为负值。{@endtemplate}

默认为 [TextLeadingDistribution.proportional]。

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

# TextStyle

```dart
class TextStyle {}
```

一个不透明对象，用于确定文本的大小、位置和渲染方式。

另请参见：

- [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle)，[painting](https://www.yuque.com/thyname/flutter.painting) 库中的对应类。

### TextStyle()

```dart
TextStyle({Color? color, TextDecoration? decoration, Color? decorationColor, TextDecorationStyle? decorationStyle, double? decorationThickness, FontWeight? fontWeight, FontStyle? fontStyle, TextBaseline? textBaseline, String? fontFamily, List<String>? fontFamilyFallback, double? fontSize, double? letterSpacing, double? wordSpacing, double? height, TextLeadingDistribution? leadingDistribution, Locale? locale, Paint? background, Paint? foreground, List<Shadow>? shadows, List<FontFeature>? fontFeatures, List<FontVariation>? fontVariations})
```

创建一个新的 TextStyle 对象。

- `color`：绘制文本时使用的颜色。若指定此项，则 `foreground` 必须为 null。
- `decoration`：在文本附近绘制的装饰（例如下划线）。
- `decorationColor`：绘制文本装饰所使用的颜色。
- `decorationStyle`：绘制文本装饰所使用的样式（例如虚线）。
- `decorationThickness`：装饰的粗细，作为字体所指定粗细的倍数。
- `fontWeight`：绘制文本时使用的字体粗细（例如粗体）。
- `fontStyle`：绘制字母时使用的字体变体（例如斜体）。
- `fontFamily`：绘制文本时使用的字体名称（例如 Roboto）。若提供了 `fontFamilyFallback` 而未提供 `fontFamily`，则 `fontFamilyFallback` 中的第一个字体族将取代首选字体族的位置。当无法找到优先级更高的字体或该字体不包含所需字形时，将使用优先级较低的字体。
- `fontFamilyFallback`：当高优先级字体中找不到某字形时用于回退的字体名称的有序列表。当 `fontFamily` 为 null 时，此列表中的第一个字体族将被用作首选字体。在内部，`fontFamily` 会被拼接到此列表的开头。当既未通过 `fontFamilyFallback`（null 或空）也未通过 `fontFamily` 提供字体族时，将使用平台默认字体。
- `fontSize`：绘制文本时使用的字形大小（以逻辑像素为单位）。
- `letterSpacing`：在每个字母之间添加的空间量（以逻辑像素为单位）。
- `wordSpacing`：在每个空白序列（即每个单词之间）添加的空间量（以逻辑像素为单位）。
- `textBaseline`：应在此文本范围与其父文本范围之间对齐的公共基线，对于根文本范围，则是与行框对齐的基线。
- `height`：此文本范围的高度，作为字体大小的倍数。将 `height` 设置为 `kTextHeightNone` 将允许行高采用字体所定义的高度，该高度可能与 fontSize 的高度不完全一致。
- `leadingDistribution`：当 `height` 被设置为非 null 且不为 `kTextHeightNone` 的值时，额外的垂直空间应如何分布在文本上方和下方。若未指定，默认使用段落的 [TextHeightBehavior](https://www.yuque.com/thyname/dart.ui/textheightbehavior)。
- `locale`：用于选择特定语言区域字形的语言区域。
- `background`：作为文本背景绘制的画笔（paint）。
- `foreground`：用于绘制文本的画笔（paint）。若指定此项，则 `color` 必须为 null。
- `fontFeatures`：应用于文本的字体特性。
- `fontVariations`：应用于文本的字体变体。

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

# ParagraphStyle

```dart
class ParagraphStyle {}
```

一个不透明对象，用于确定 [ParagraphBuilder](https://www.yuque.com/thyname/dart.ui/paragraphbuilder) 在 [Paragraph](https://www.yuque.com/thyname/dart.ui/paragraph) 文本内定位各行时所使用的配置。

### ParagraphStyle()

```dart
ParagraphStyle({TextAlign? textAlign, TextDirection? textDirection, int? maxLines, String? fontFamily, double? fontSize, double? height, TextHeightBehavior? textHeightBehavior, FontWeight? fontWeight, FontStyle? fontStyle, StrutStyle? strutStyle, String? ellipsis, Locale? locale})
```

创建一个新的 ParagraphStyle 对象。

- `textAlign`：段落各行内文本的对齐方式。若末行被省略号截断（参见下方的 `ellipsis`），对齐方式会在该行被截断之后、添加省略号之前应用。参见：https://github.com/flutter/flutter/issues/9819

- `textDirection`：文本的方向性，从左到右（例如挪威语）或从右到左（例如希伯来语）。这控制着段落的整体方向性，以及 `textAlign` 字段中 [TextAlign.start] 和 [TextAlign.end] 的含义。

- `maxLines`：绘制的最大行数。超出此行数的行会被静默丢弃。例如，若 `maxLines` 为 1，则只渲染一行。若 `maxLines` 为 null，但 `ellipsis` 不为 null，则第一行超出宽度约束之后的所有行都会被丢弃。宽度约束由传递给 [Paragraph.layout] 方法的 [ParagraphConstraints](https://www.yuque.com/thyname/dart.ui/paragraphconstraints) 对象设定。

- `fontFamily`：在没有 `textStyle` 附加到该文本范围时，绘制文本所应用的字体族名称。

- `fontSize`：绘制文本时使用的回退字形大小（以逻辑像素为单位）。此项在没有 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 时使用。

- `height`：作为字体大小倍数的文本范围回退高度。当未通过 [TextStyle.height] 提供高度时，使用该回退高度。此处省略 `height`（或将其设为 [kTextHeightNone](https://www.yuque.com/thyname/dart.ui/ktextheightnone)），并且在 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 中也未设置，将允许行高采用字体所定义的高度，该高度可能与 `fontSize` 的高度不完全一致。

- `textHeightBehavior`：指定 `height` 倍数如何应用于首行的上升高度和末行的下降高度。

- `leadingDistribution`：指定由 `height` 倍数所增加的额外垂直空间应如何分布在文本上方和下方。默认为 [TextLeadingDistribution.proportional]。

- `fontWeight`：绘制文本时使用的字体粗细（例如粗体）。

- `fontStyle`：绘制字母时使用的字体变体（例如斜体）。

- `strutStyle`：支柱（strut）的属性。支柱定义了一组与最小垂直行高相关的度量，可用于获得更高级的行间距行为。

- `ellipsis`：用于省略溢出文本的字符串。若 `maxLines` 不为 null，则在最后渲染的行超出宽度约束时，会对该行应用 `ellipsis`（如果有）。若 `maxLines` 为 null，则 `ellipsis` 会应用于第一行超出宽度约束的行，其后的行会被丢弃。宽度约束由传递给 [Paragraph.layout] 方法的 [ParagraphConstraints](https://www.yuque.com/thyname/dart.ui/paragraphconstraints) 对象设定。空字符串与 null 值被视为等效，均会关闭此行为。

- `locale`：用于选择特定语言区域字形的语言区域。

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

# StrutStyle

```dart
class StrutStyle {}
```

另请参见：

- [StrutStyle](https://www.yuque.com/thyname/dart.ui/strutstyle)，[painting](https://www.yuque.com/thyname/flutter.painting) 库中的对应类。

### StrutStyle()

```dart
StrutStyle({String? fontFamily, List<String>? fontFamilyFallback, double? fontSize, double? height, TextLeadingDistribution? leadingDistribution, double? leading, FontWeight? fontWeight, FontStyle? fontStyle, bool? forceStrutHeight})
```

创建一个新的 StrutStyle 对象。

- `fontFamily`：绘制文本时使用的字体名称（例如 Roboto）。

- `fontFamilyFallback`：当 `fontFamily` 中的字体找不到时用于搜索的字体族名称的有序列表。

- `fontSize`：绘制文本时使用的字形大小（以逻辑像素为单位）。

- `height`：行框的最小高度，作为字体大小的倍数。当 `fontSize` 不为 null 时，段落各行的高度至少为 `(height + leading) * fontSize`。省略 `height`（或将其设为 [kTextHeightNone](https://www.yuque.com/thyname/dart.ui/ktextheightnone)）将允许最小行高采用字体所定义的高度，该高度可能与 `fontSize` 的高度不完全一致。当 `fontSize` 为 null 时，没有最小行高。由于基线对齐或较大的 [TextStyle.fontSize] 而导致的高字形，可能会使布局后的实际行高高于此处指定的值。必须提供 `fontSize` 才能使此属性生效。

- `leading`：作为字体大小倍数的行间最小行距。必须提供 `fontSize` 才能使此属性生效。由此属性添加的行距会均匀分布在文本上方和下方，与 `leadingDistribution` 无关。

- `leadingDistribution`：由 `height` 倍数所增加的额外垂直空间应如何分布在文本上方和下方，独立于（始终均匀分布在文本上方和下方的）`leading`。默认为段落的 [TextHeightBehavior](https://www.yuque.com/thyname/dart.ui/textheightbehavior) 所指定的行距分布方式。

- `fontWeight`：绘制文本时使用的字体粗细（例如粗体）。

- `fontStyle`：绘制字母时使用的字体变体（例如斜体）。

- `forceStrutHeight`：为 true 时，段落将强制所有行的基线到基线高度恰好为 `(height + leading) * fontSize`。此时 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 将不再能够影响行高，任何高字形都可能与上方的行重叠。若指定了 `fontFamily`，首行的总上升高度将取 `fontFamily` 的 `上升高度 + 半行距` 与 `(height + leading) * fontSize` 两者中的较小值。否则，将由首个文本的上升高度 + 半行距确定。

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# TextDirection

```dart
enum TextDirection {}
```

文本流动的方向。

一些语言从左向右书写（例如英语、泰米尔语或中文），而另一些语言则从右向左书写（例如阿拉姆语、希伯来语或乌尔都语）。还有一些语言会混合使用两种方向，例如阿拉伯语大多从右向左书写，但数字则从左向右书写。

在渲染文本或需要水平布局盒子的 API 中必须提供文本方向，以便这些 API 确定应从哪个方向开始：从右向左（[TextDirection.rtl]），或从左向右（[TextDirection.ltr]）。

## 设计讨论

Flutter 旨在满足使用任何一种世界现行语言编写的应用程序的需求，无论其采用从右向左还是从左向右的书写方向。Flutter 不支持其他书写模式，例如竖排文本或牛耕式转行书写（boustrophedon），因为这些在计算机程序中很少使用。

在开发用户界面框架时，通常会选定一个默认文本方向——通常是从左向右，即框架开发工程师最熟悉的方向——因为这样可以简化该平台上应用程序的开发。遗憾的是，这经常导致该平台产生意料之外的从左向右偏见或假设，因为工程师通常会遗漏需要支持从右向左文本的地方。这随之会导致仅在从右向左环境中才会显现的 bug。

为了尽量减少 Flutter 出现此类问题，Flutter 框架的最底层不设默认的文本阅读方向。任何需要阅读方向的场合，例如需要显示文本时，或需要解释与书写方向相关的值时，都必须显式指定阅读方向。在可行之处，例如在 `switch` 语句中，从右向左的情形会被列在最前面，以避免给人一种它只是事后添加的印象。

在更高的层级（具体从 widgets 库开始），会引入一个环境性的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)，用以提供默认值。因此，例如，在 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 组件作用范围内的 [widgets.Text] 组件无需被赋予显式的书写方向。可以使用 [Directionality.of] 静态方法获取特定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的环境文本方向。

### Flutter 中已知的从左向右偏见

尽管有上述设计意图，某些从左向右的偏见仍然渗入了 Flutter 的设计中。包括：

- [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 的原点位于左上角，x 轴沿从左到右的方向递增。

- widgets 库和 material 库中的默认本地化为美式英语，这是一种从左向右的语言。

### 视觉属性与方向性属性

Flutter 框架中的许多类都提供两种版本：一种是面向视觉的变体，另一种是依赖文本方向的变体。例如，[EdgeInsets](https://www.yuque.com/thyname/flutter.painting/edgeinsets) 以上、左、右、下来描述，而 [EdgeInsetsDirectional](https://www.yuque.com/thyname/flutter.painting/edgeinsetsdirectional) 则以上、起始（start）、结束（end）、下来描述，其中起始和结束在从右向左文本中分别对应右和左，在从左向右文本中分别对应左和右。

这两种变体各有其独特的使用场景。

依赖文本方向的变体适用于希望随文本方向"翻转"的用户界面开发场景。例如，一段英文文本段落通常靠左对齐，引用内容从左侧缩进，而在阿拉伯语中则靠右对齐，引用内容从右侧缩进。这两种情形都可以通过依赖方向的 [TextAlign.start] 和 [EdgeInsetsDirectional.start] 来描述。

相对地，当文本方向已知且不受阅读方向影响时，视觉变体则很有用。例如，一个显示驾车导航的应用程序可能会在左侧显示"左转"箭头、在右侧显示"右转"箭头——无论该应用程序是本地化为法语（从左向右）还是希伯来语（从右向左），都应如此显示。

实际上，也可以预见许多开发者只会面向一种语言，在这种情况下，直接以视觉化的方式思考可能更简单。

文本从右向左流动（例如阿拉伯语、希伯来语）。

文本从左向右流动（例如英语、法语）。

# TextBox

```dart
class TextBox {}
```

一个包围一段文本的矩形。

这与 [Rect](https://www.yuque.com/thyname/dart.ui/rect) 类似，但包含固有的 [TextDirection](https://www.yuque.com/thyname/dart.ui/textdirection)。

### TextBox.fromLTRBD()

```dart
TextBox.fromLTRBD(double left, double top, double right, double bottom, TextDirection direction)
```

创建一个描述包含文本的盒子的对象。

### left

```dart
double left
```

文本盒子的左边缘，与方向无关。

若要获取前导边缘（可能取决于 [direction]），请考虑使用 [start]。

### top

```dart
double top
```

文本盒子的上边缘。

### right

```dart
double right
```

文本盒子的右边缘，与方向无关。

若要获取尾随边缘（可能取决于 [direction]），请考虑使用 [end]。

### bottom

```dart
double bottom
```

文本盒子的下边缘。

### direction

```dart
TextDirection direction
```

此盒子内文本流动的方向。

### toRect()

```dart
Rect toRect()
```

返回一个与此盒子大小相同的矩形。

### start

```dart
double get start
```

对于从左到右的文本，为盒子的 [left] 边缘；对于从右到左的文本，为盒子的 [right] 边缘。

另请参见：

- [direction]，用于指定文本方向。

### end

```dart
double get end
```

对于从左到右的文本，为盒子的 [right] 边缘；对于从右到左的文本，为盒子的 [left] 边缘。

另请参见：

- [direction]，用于指定文本方向。

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

# TextAffinity

```dart
enum TextAffinity {}
```

一种用于消除 [TextPosition](https://www.yuque.com/thyname/dart.ui/textposition) 歧义的方式，适用于其偏移量（offset）可能匹配渲染字符串中两个不同位置的情形。

例如，在渲染文本发生换行的偏移处，该偏移可能代表两个视觉位置：一个位于换行前（第一行的末尾），另一个位于换行后（第二行的开头）。文本亲和性（Text affinity）用于消除这两种情形之间的歧义。

这仅影响由自动换行引起的换行，不影响显式的换行符。对于换行符，其位置仅由偏移量本身完全确定，不存在歧义。

[TextAffinity](https://www.yuque.com/thyname/dart.ui/textaffinity) 还会影响从左到右（LTR）与从右到左（RTL）文本交界处的双向文本。考虑以下字符串，其中小写字母将以 LTR 方式显示，大写字母以 RTL 方式显示："helloHELLO"。渲染时，该字符串在视觉上会显示为 "helloOLLEH"。若没有相应的 [TextAffinity](https://www.yuque.com/thyname/dart.ui/textaffinity)，偏移量 5 将具有歧义。从代码角度看这个字符串，该偏移代表紧跟在 "o" 之后、紧邻 "H" 之前的位置。渲染时，此偏移可能位于字符串中间 "o" 的右侧，也可能位于字符串末尾 "H" 的右侧。

该位置的亲和方向为文本位置的上游（upstream）一侧，即朝向字符串开头的方向。

在文本因换行而产生歧义偏移的示例中，upstream 表示第一行的末尾。

在双向文本示例 "helloHELLO" 中，若偏移量为 5 且 [TextAffinity](https://www.yuque.com/thyname/dart.ui/textaffinity) 为 upstream，则会出现在渲染文本的中间，紧邻 "o" 的右侧。完整示例参见 [TextAffinity](https://www.yuque.com/thyname/dart.ui/textaffinity) 的定义。

该位置的亲和方向为文本位置的下游（downstream）一侧，即朝向字符串末尾的方向。

在文本因换行而产生歧义偏移的示例中，downstream 表示第二行的开头。

在双向文本示例 "helloHELLO" 中，若偏移量为 5 且 [TextAffinity](https://www.yuque.com/thyname/dart.ui/textaffinity) 为 downstream，则会出现在渲染文本的末尾，紧邻 "H" 的右侧。完整示例参见 [TextAffinity](https://www.yuque.com/thyname/dart.ui/textaffinity) 的定义。

# TextPosition

```dart
class TextPosition {}
```

字符串文本中的一个位置。

TextPosition 可用于描述字符之间的光标位置。[offset] 指向字符串中第 `offset - 1` 个字符与第 `offset` 个字符之间的位置，[affinity] 用于描述该位置与哪个字符相关联。

一种使用场景是渲染文本被强制换行时。在这种情况下，发生换行处的偏移在视觉上既可能出现在第一行末尾，也可能出现在第二行开头。第二种情形是双向文本：两种不同文本方向交界处的偏移在渲染文本中可能对应两个位置之一。

参见 [TextAffinity](https://www.yuque.com/thyname/dart.ui/textaffinity) 的文档，了解 TextAffinity 如何消除此类情形的歧义的更多信息。

### TextPosition()

```dart
TextPosition({required int offset, TextAffinity affinity = TextAffinity.downstream})
```

创建一个表示字符串中特定位置的对象。

参数不得为 null（因此 [offset] 参数是必需的）。

### offset

```dart
int offset
```

紧跟在字符串文本表示中该位置之后的字符索引。

例如，给定字符串 `'Hello'`，偏移量 0 表示光标位于 `H` 之前，而偏移量 5 表示光标恰好位于 `o` 之后。

### affinity

```dart
TextAffinity affinity
```

用于消除 [offset] 所给定的字符串位置可能代表渲染文本中两个不同视觉位置的歧义。例如，当文本被强制换行，或某段文本以多种文本方向渲染时，可能发生这种情况。

参见 [TextAffinity](https://www.yuque.com/thyname/dart.ui/textaffinity) 的文档，了解 TextAffinity 如何消除此类情形的歧义的更多信息。

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

# TextRange

```dart
class TextRange {}
```

字符串文本中的一段字符范围。

### TextRange()

```dart
TextRange({required int start, required int end})
```

创建一个文本范围。

[start] 和 [end] 参数不得为 null。[start] 和 [end] 必须同时大于或等于零，或者同时恰好为 -1。

该范围所包含的文本包括 [start] 处的字符，但不包括 [end] 处的字符。

与其创建一个空的文本范围，不如考虑使用 [empty] 常量。

### TextRange.collapsed()

```dart
TextRange.collapsed(int offset)
```

一个在 offset 处开始并结束的文本范围。

[offset] 参数不得为 null，且必须大于或等于 -1。

### empty

```dart
TextRange empty
```

一个不包含任何内容、且不在文本中的文本范围。

### start

```dart
int start
```

范围中第一个字符的索引。

若 [start] 和 [end] 都为 -1，则该文本范围为空。

### end

```dart
int end
```

此范围中字符之后的下一个索引。

若 [start] 和 [end] 都为 -1，则该文本范围为空。

### isValid

```dart
bool get isValid
```

此范围是否表示文本中的一个有效位置。

### isCollapsed

```dart
bool get isCollapsed
```

此范围是否为空（但仍有可能被置于文本内部）。

### isNormalized

```dart
bool get isNormalized
```

此范围的起始位置是否位于结束位置之前。

### textBefore()

```dart
String textBefore(String text)
```

此范围之前的文本。

### textAfter()

```dart
String textAfter(String text)
```

此范围之后的文本。

### textInside()

```dart
String textInside(String text)
```

此范围内部的文本。

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

# ParagraphConstraints

```dart
class ParagraphConstraints {}
```

[Paragraph](https://www.yuque.com/thyname/dart.ui/paragraph) 对象的布局约束。

此类的实例通常与 [Paragraph.layout] 一起使用。

唯一可以指定的约束是 [width]。详情参见 [width] 处的讨论。

### ParagraphConstraints()

```dart
ParagraphConstraints({required double width})
```

创建用于段落布局的约束。

[width] 参数不得为 null。

### width

```dart
double width
```

段落在计算字形位置时应使用的宽度。

如果可能，段落会在到达此宽度之前选择一个软换行处。若没有可用的软换行，段落会在到达此宽度之前选择一个硬换行处。若这会导致在尚未放置任何字符的情况下强制换行（即若接下来要布局的字符无法在给定的宽度约束内容纳），则允许该字符溢出宽度约束，并在其后放置一个强制换行（即便紧随其后有显式换行符）。

该宽度会影响省略号的应用方式。详情参见 [ParagraphStyle.new] 处的讨论。

在使用 [ParagraphBuilder](https://www.yuque.com/thyname/dart.ui/paragraphbuilder) 构建 [Paragraph](https://www.yuque.com/thyname/dart.ui/paragraph) 时，此宽度也用于根据 [ParagraphStyle](https://www.yuque.com/thyname/dart.ui/paragraphstyle) 中描述的 [TextAlign](https://www.yuque.com/thyname/dart.ui/textalign) 对齐方式来定位字形。

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

# BoxHeightStyle

```dart
enum BoxHeightStyle {}
```

定义 [Paragraph.getBoxesForRange] 所返回盒子在垂直方向上的多种限定方式。

关于控制宽度的类似属性，参见 [BoxWidthStyle](https://www.yuque.com/thyname/dart.ui/boxwidthstyle)。

提供按每个文本行紧密贴合高度的边界框。此样式可能导致边界框高低不齐，无法与相邻盒子平滑衔接。

盒子的高度将为该行中所有文本行（run）的最大高度。同一行中的所有盒子高度相同。

这不保证在存在额外行间距时盒子会覆盖整行的完整垂直高度。

关于能覆盖整行的样式，参见 [BoxHeightStyle.includeLineSpacingTop]、[BoxHeightStyle.includeLineSpacingMiddle] 和 [BoxHeightStyle.includeLineSpacingBottom]。

扩展边界的上边缘和下边缘，以完全覆盖任何行间距。

每个盒子的顶部和底部将分别覆盖该行上方一半和下方一半的空间。

{@template dart.ui.boxHeightStyle.includeLineSpacing} 每行的顶部边缘应与上一行的底部边缘相同。无论行间距多大，垂直方向的覆盖都不应存在空隙。由于第一行上方和最后一行下方不存在额外空间，因此不会在此处添加行间距。{@endtemplate}

扩展边界的上边缘，以完全覆盖任何行间距。

行间距会被添加到盒子的顶部。

{@macro dart.ui.boxHeightStyle.includeLineSpacing}

扩展边界的下边缘，以完全覆盖任何行间距。

行间距会被添加到盒子的底部。

{@macro dart.ui.boxHeightStyle.includeLineSpacing}

根据此段落 [StrutStyle](https://www.yuque.com/thyname/dart.ui/strutstyle) 的度量来计算盒子高度。

基于支柱（strut）的盒子在整个段落中将具有一致的高度。每行的顶部边缘将与上一行的底部边缘对齐。字形有可能延伸到这些盒子之外。

# BoxWidthStyle

```dart
enum BoxWidthStyle {}
```

定义 [Paragraph.getBoxesForRange] 所返回盒子在水平方向上的多种限定方式。

关于控制高度的类似属性，参见 [BoxHeightStyle](https://www.yuque.com/thyname/dart.ui/boxheightstyle)。

提供按每行分别紧密贴合宽度的边界框。

根据需要在每行的开头和/或结尾处最多添加两个额外的盒子，使该行中盒子的宽度与段落中最宽一行的宽度相同。

仅当某行相关边缘处的相关盒子未跨越该段落的最大宽度时，才会在该行添加这些额外的盒子。

# PlaceholderAlignment

```dart
enum PlaceholderAlignment {}
```

占位符相对于周围文本在垂直方向上的对齐位置。

由 [ParagraphBuilder.addPlaceholder] 使用。

将占位符的基线与指定基线对齐。

使用此对齐模式时，必须指定非 null 的 [TextBaseline](https://www.yuque.com/thyname/dart.ui/textbaseline)。

将占位符的下边缘与基线对齐，使占位符位于基线之上。

使用此对齐模式时，必须指定非 null 的 [TextBaseline](https://www.yuque.com/thyname/dart.ui/textbaseline)。

将占位符的上边缘与指定基线对齐，使占位符悬挂于基线之下。

将占位符的上边缘与文本的上边缘对齐。

当占位符非常高时，额外的空间将从顶部向下延伸，贯穿该行的底部。

将占位符的下边缘与文本的下边缘对齐。

当占位符非常高时，额外的空间将从底部向上延伸，贯穿该行的顶部。

将占位符的中部与文本的中部对齐。

当占位符非常高时，额外的空间将从该行的顶部和底部均等地增长。

# LineMetrics

```dart
class LineMetrics {}
```

[LineMetrics](https://www.yuque.com/thyname/dart.ui/linemetrics) 存储段落中单行的度量和统计信息。

此处的度量针对整行而言，代表该行的最大范围，而非按文本行（run）或按字形的度量。若需要更详细的度量，参见 [TextBox](https://www.yuque.com/thyname/dart.ui/textbox) 和 [Paragraph.getBoxesForRange]。

[LineMetrics](https://www.yuque.com/thyname/dart.ui/linemetrics) 应直接通过 [Paragraph.computeLineMetrics] 方法获取。

### LineMetrics()

```dart
LineMetrics({required bool hardBreak, required double ascent, required double descent, required double unscaledAscent, required double height, required double width, required double left, required double baseline, required int lineNumber})
```

仅使用指定的值创建一个 [LineMetrics](https://www.yuque.com/thyname/dart.ui/linemetrics) 对象。

### hardBreak

```dart
bool hardBreak
```

若此行以显式换行符（例如 '\n'）结尾或为段落末尾，则为 true。否则为 false。

### ascent

```dart
double ascent
```

根据此行的字体和样式所计算出的、相对于 [baseline] 的上升高度。

这是最终计算出的上升高度，可能受支柱、高度、缩放以及其他非常高的文本行（run）的影响。

[ascent] 以正值提供，尽管在字体中通常将其定义为负值。这是为了确保这些度量运算的正负号能直接反映预期值的正负号。例如，该行顶部边缘的 y 坐标为 `baseline - ascent`。

### descent

```dart
double descent
```

根据此行的字体和样式所计算出的、相对于 [baseline] 的下降高度。

这是最终计算出的上升高度，可能受支柱、高度、缩放以及其他非常高的文本行（run）的影响。

该行底部边缘的 y 坐标为 `baseline + descent`。

### unscaledAscent

```dart
double unscaledAscent
```

根据此行的字体和样式、忽略 [TextStyle.height] 所计算出的、相对于 [baseline] 的上升高度。

[unscaledAscent] 以正值提供，尽管在字体中通常将其定义为负值。这是为了确保这些度量运算的正负号能直接反映预期值的正负号。

### height

```dart
double height
```

该行从顶部边缘到底部边缘的总高度。

这等同于 `round(ascent + descent)`。之所以单独提供此值，是因为四舍五入会导致与未四舍五入值之间存在亚像素级差异。

### width

```dart
double width
```

该行从最左侧字形的左边缘到最右侧字形的右边缘的宽度。

这与段落的宽度不同。

另请参见：

- [Paragraph.width]，布局时传入的最大宽度。
- [Paragraph.longestLine]，段落中最长一行的宽度。

### left

```dart
double left
```

该行左边缘的 x 坐标。

右边缘可通过 `left + width` 得到。

### baseline

```dart
double baseline
```

此行基线相对于段落顶部的 y 坐标。

段落中至此行（包含此行）为止底部边缘的位置可通过 `baseline + descent` 获得。

### lineNumber

```dart
int lineNumber
```

此行在整个段落中的编号，首行编号为 0。

例如，第一行为第 0 行，第二行为第 1 行。

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

# Paragraph

```dart
abstract class Paragraph {}
```

一段文本段落。

段落保留每个字形的大小和位置信息，可高效地进行调整大小和绘制。

要创建 [Paragraph](https://www.yuque.com/thyname/dart.ui/paragraph) 对象，请使用 [ParagraphBuilder](https://www.yuque.com/thyname/dart.ui/paragraphbuilder)。

段落可以通过 [Canvas.drawParagraph] 方法显示在 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 上。

### width

```dart
double get width
```

此段落占用的水平空间量。

仅在调用 [layout] 之后有效。

### height

```dart
double get height
```

此段落占用的垂直空间量。

仅在调用 [layout] 之后有效。

### longestLine

```dart
double get longestLine
```

段落中从最左侧字形的左边缘到最右侧字形的右边缘的距离。

仅在调用 [layout] 之后有效。

### minIntrinsicWidth

```dart
double get minIntrinsicWidth
```

此段落在不导致内容绘制失败的前提下所能拥有的最小宽度。

仅在调用 [layout] 之后有效。

### maxIntrinsicWidth

```dart
double get maxIntrinsicWidth
```

返回超过该宽度后，继续增加宽度也不会再减少高度的最小宽度。

仅在调用 [layout] 之后有效。

### alphabeticBaseline

```dart
double get alphabeticBaseline
```

从段落顶部到首行拉丁字母基线的距离，以逻辑像素为单位。

### ideographicBaseline

```dart
double get ideographicBaseline
```

从段落顶部到首行表意文字基线的距离，以逻辑像素为单位。

### didExceedMaxLines

```dart
bool get didExceedMaxLines
```

若还有更多垂直方向的内容，但文本已被截断——无论是因为达到了 `maxLines` 指定的行数，还是因为 `maxLines` 为 null、`ellipsis` 不为 null，且某一行超出了宽度约束——则为 true。

参见 [ParagraphStyle.new] 处关于 `maxLines` 和 `ellipsis` 参数的讨论。

### layout()

```dart
void layout(ParagraphConstraints constraints)
```

计算段落中每个字形的大小和位置。

[ParagraphConstraints](https://www.yuque.com/thyname/dart.ui/paragraphconstraints) 用于控制文本允许的最大宽度。

### getBoxesForRange()

```dart
List<TextBox> getBoxesForRange(int start, int end, {BoxHeightStyle boxHeightStyle = BoxHeightStyle.tight, BoxWidthStyle boxWidthStyle = BoxWidthStyle.tight})
```

返回包围给定文本范围的一组文本盒子（text box）列表。

[boxHeightStyle] 和 [boxWidthStyle] 参数允许自定义盒子在垂直和水平方向上的边界方式。两个样式参数默认均为 tight 选项，该选项提供紧密贴合的盒子，且不考虑任何行间距。

TextBox 的坐标相对于段落的左上角，正的 y 值表示向下。

[boxHeightStyle] 和 [boxWidthStyle] 参数不得为 null。

关于每个选项的完整说明，参见 [BoxHeightStyle](https://www.yuque.com/thyname/dart.ui/boxheightstyle) 和 [BoxWidthStyle](https://www.yuque.com/thyname/dart.ui/boxwidthstyle)。

### getBoxesForPlaceholders()

```dart
List<TextBox> getBoxesForPlaceholders()
```

返回包围段落中所有占位符的一组文本盒子列表。

盒子的顺序与通过 [ParagraphBuilder.addPlaceholder] 传入的顺序相同。

[TextBox](https://www.yuque.com/thyname/dart.ui/textbox) 的坐标相对于段落的左上角，正的 y 值表示向下。

### getPositionForOffset()

```dart
TextPosition getPositionForOffset(Offset offset)
```

返回最接近给定偏移的文本位置。

对于任意给定的 [offset]，此方法总会返回一个 [TextPosition](https://www.yuque.com/thyname/dart.ui/textposition)，即便该 [offset] 并不靠近任何文本，或段落为空时也是如此。这对于确定用户拖动文本选择手柄时应选中的文本很有用。

另请参见：

- [getClosestGlyphInfoForOffset]，返回关于最接近某 [Offset](https://www.yuque.com/thyname/dart.ui/offset) 的字符的更多信息。

### getClosestGlyphInfoForOffset()

```dart
GlyphInfo? getClosestGlyphInfoForOffset(Offset offset)
```

返回段落坐标系中最接近给定 `offset` 的字形的 [GlyphInfo](https://www.yuque.com/thyname/dart.ui/glyphinfo)；若文本为空，或文本被完全裁剪或省略，则返回 null。

此方法首先找到最接近 `offset.dy` 的行，然后返回该行内最接近的字形的 [GlyphInfo](https://www.yuque.com/thyname/dart.ui/glyphinfo)。

### getGlyphInfoAt()

```dart
GlyphInfo? getGlyphInfoAt(int codeUnitOffset)
```

返回位于段落中给定 UTF-16 `codeUnitOffset` 处的 [GlyphInfo](https://www.yuque.com/thyname/dart.ui/glyphinfo)；若给定的 `codeUnitOffset` 超出可见行范围或已被省略，则返回 null。

### getWordBoundary()

```dart
TextRange getWordBoundary(TextPosition position)
```

返回给定 [TextPosition](https://www.yuque.com/thyname/dart.ui/textposition) 处单词的 [TextRange](https://www.yuque.com/thyname/dart.ui/textrange)。

不属于单词一部分的字符，如空格、符号和标点，其两侧均存在单词边界。在这种情况下，此方法会返回 (offset, offset+1)。单词边界在 Unicode 标准附件 #29 http://www.unicode.org/reports/tr29/#Word_Boundaries 中有更精确的定义。

[TextPosition](https://www.yuque.com/thyname/dart.ui/textposition) 被视为光标位置，其 [TextPosition.affinity] 用于确定该位置指向哪个字符。例如，对于 `string = 'Hello word'`，位置 `TextPosition(offset: 5, affinity: TextPosition.upstream)` 处的单词边界将返回范围 (0, 5)，因为该位置指向字符 'o' 而非空格。

### getLineBoundary()

```dart
TextRange getLineBoundary(TextPosition position)
```

返回给定 [TextPosition](https://www.yuque.com/thyname/dart.ui/textposition) 所在行的 [TextRange](https://www.yuque.com/thyname/dart.ui/textrange)。

换行符（若有）会作为该范围的一部分返回。

在调用 layout 之前无效。

由于需要计算行度量信息，此操作可能开销较大，因此应谨慎使用。

### computeLineMetrics()

```dart
List<LineMetrics> computeLineMetrics()
```

返回详细描述每个已布局行各项度量的完整 [LineMetrics](https://www.yuque.com/thyname/dart.ui/linemetrics) 列表。

在调用 layout 之前无效。

此操作可能返回大量数据，因此不建议反复调用。应改为缓存结果。

### getLineMetricsAt()

```dart
LineMetrics? getLineMetricsAt(int lineNumber)
```

返回第 `lineNumber` 行的 [LineMetrics](https://www.yuque.com/thyname/dart.ui/linemetrics)；若给定的 `lineNumber` 大于或等于 [numberOfLines]，则返回 null。

### numberOfLines

```dart
int get numberOfLines
```

段落中可见行的总数。

返回一个非负数。若 `maxLines` 不为 null，[numberOfLines] 的值永远不会超过 `maxLines`。

### getLineNumberAt()

```dart
int? getLineNumberAt(int codeUnitOffset)
```

返回 `codeUnitOffset` 所指向代码单元所在行的行号。

若给定的 `codeUnitOffset` 超出边界，或在逻辑上位于最后一个可见代码点之后，此方法返回 null。这包括目标代码单元所属的代码点属于某个可见行，但文本布局库已将其替换为省略号的情形。

若目标代码单元指向引入强制换行的控制字符（最常见的是换行符 `LF`，通常在字符串中以转义序列 "\n" 表示），为符合[Unicode 规则](https://unicode.org/reports/tr14/#LB4)，该控制字符本身始终被视为位于"当前"行的末尾，而非新行的开头。

### dispose()

```dart
void dispose()
```

释放此对象所使用的资源。调用此方法后，该对象将不再可用。

### debugDisposed

```dart
bool get debugDisposed
```

此对底层图片（picture）的引用是否已被 [dispose]。

此值仅在启用断言（asserts）时有效，不得在其他情况下使用。

# ParagraphBuilder

```dart
abstract class ParagraphBuilder {}
```

使用给定的样式信息构建包含文本的 [Paragraph](https://www.yuque.com/thyname/dart.ui/paragraph)。

要设置段落的对齐方式、截断和省略行为，请将一个配置适当的 [ParagraphStyle](https://www.yuque.com/thyname/dart.ui/paragraphstyle) 对象传递给 [ParagraphBuilder.new] 构造函数。

然后，调用 [pushStyle]、[addText] 和 [pop] 的组合，向该对象添加带样式的文本。

最后，调用 [build] 以获得构建完成的 [Paragraph](https://www.yuque.com/thyname/dart.ui/paragraph) 对象。此后，该构建器将不再可用。

构造出 [Paragraph](https://www.yuque.com/thyname/dart.ui/paragraph) 后，对其调用 [Paragraph.layout]，然后使用 [Canvas.drawParagraph] 进行绘制。

### ParagraphBuilder()

```dart
ParagraphBuilder(ParagraphStyle style)
```

创建一个新的 [ParagraphBuilder](https://www.yuque.com/thyname/dart.ui/paragraphbuilder) 对象，用于创建 [Paragraph](https://www.yuque.com/thyname/dart.ui/paragraph)。

### placeholderCount

```dart
int get placeholderCount
```

段落中当前占位符的数量。

### placeholderScales

```dart
List<double> get placeholderScales
```

段落中各占位符的缩放比例。

### pushStyle()

```dart
void pushStyle(TextStyle style)
```

将给定样式应用于后续添加的文本，直至调用 [pop]。

详情参见 [pop]。

### pop()

```dart
void pop()
```

结束最近一次调用 [pushStyle] 所产生的效果。

在内部，段落构建器维护一个文本样式栈。添加到段落中的文本会受到栈中所有样式的影响。调用 [pop] 会移除栈顶的样式，其余样式继续生效。

### addText()

```dart
void addText(String text)
```

将给定文本添加到段落中。

该文本将根据当前的文本样式栈进行样式化。

### addPlaceholder()

```dart
void addPlaceholder(double width, double height, PlaceholderAlignment alignment, {double scale = 1.0, double? baselineOffset, TextBaseline? baseline})
```

向段落添加一个内联占位符空间。

该段落将包含一个指定尺寸、不含文本的矩形空间。

`width` 和 `height` 参数指定占位符矩形的大小。

`alignment` 参数指定占位符矩形与周围文本在垂直方向上的对齐方式。使用 [PlaceholderAlignment.baseline]、[PlaceholderAlignment.aboveBaseline] 和 [PlaceholderAlignment.belowBaseline] 对齐模式时，需要通过 `baseline` 设置基线。使用 [PlaceholderAlignment.baseline] 时，`baselineOffset` 表示基线相对于矩形顶部向下的距离。默认的 `baselineOffset` 为 `height`。

示例：

- 对于一个 30x50 的占位符，其底部边缘与文本底部对齐，使用：`addPlaceholder(30, 50, PlaceholderAlignment.bottom);`
- 对于一个 30x50 的占位符，使其垂直居中于文本，使用：`addPlaceholder(30, 50, PlaceholderAlignment.middle);`。
- 对于一个 30x50 的占位符，使其完全位于拉丁字母基线之上，使用：`addPlaceholder(30, 50, PlaceholderAlignment.aboveBaseline, baseline: TextBaseline.alphabetic)`。
- 对于一个 30x50 的占位符，在拉丁字母基线上方 40 像素、下方 10 像素，使用：`addPlaceholder(30, 50, PlaceholderAlignment.baseline, baseline: TextBaseline.alphabetic, baselineOffset: 40)`。

允许在每个占位符周围进行换行。

装饰将根据最近推入的 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 中定义的字体绘制。装饰的绘制方式如同占位符空间中存在 Unicode 文本一般，且无论占位符的高度和对齐方式如何，都会以相同方式绘制。若要隐藏或手动调整装饰以适配占位符，应在添加占位符之前推入具有所需装饰行为的文本样式。

通过占位符绘制的任何装饰都会存在于与文本相同的画布/图层上。这意味着绘制在占位符所保留空间之上的任何内容，都会覆盖在装饰之上，可能会遮挡该装饰。

占位符在文本缓冲区中以 Unicode 0xFFFC "对象替换字符" 表示。对于每个占位符，都会在文本缓冲区中添加一个对象替换字符。

`scale` 参数将按指定量缩放 `width` 和 `height`，并记录该缩放比例。已添加占位符的缩放比例可通过 [placeholderScales] 访问。这主要用于无障碍缩放。

### build()

```dart
Paragraph build()
```

应用给定的段落样式，并返回一个包含已添加文本及相关样式的 [Paragraph](https://www.yuque.com/thyname/dart.ui/paragraph)。

调用此函数后，该段落构建器对象将失效，无法进一步使用。

# loadFontFromList()

```dart
Future<void> loadFontFromList(Uint8List list, {String? fontFamily})
```

从缓冲区加载字体，并使其可用于文本渲染。

- `list`：包含字体文件的字节列表。
- `fontFamily`：用于在文本样式中标识该字体的字体族名称。若未提供此项，则字体族名称将从字体文件中提取。
