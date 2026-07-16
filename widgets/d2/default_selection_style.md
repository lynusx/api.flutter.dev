@docImport 'package:flutter/material.dart';

@docImport 'editable_text.dart'; @docImport 'text.dart';

# DefaultSelectionStyle

```dart
class DefaultSelectionStyle extends InheritedTheme {}
```

应用于没有显式样式的后代 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) Widget 的选区样式。

{@macro flutter.cupertino.CupertinoApp.defaultSelectionStyle}

{@macro flutter.material.MaterialApp.defaultSelectionStyle}

另请参阅：

- [TextSelectionTheme](https://www.yuque.com/thyname/flutter.material/textselectiontheme)：它也会为子树创建一个 [DefaultSelectionStyle](https://www.yuque.com/thyname/flutter.widgets/defaultselectionstyle)。

### DefaultSelectionStyle()

```dart
DefaultSelectionStyle({dynamic key, Color? cursorColor, Color? selectionColor, MouseCursor? mouseCursor, required Widget child})
```

创建一个默认选区样式 Widget，用于为其下方 Widget 树中的所有 Widget 指定选区属性。

### DefaultSelectionStyle.fallback()

```dart
DefaultSelectionStyle.fallback({dynamic key})
```

一个可通过 const 构造的默认选区样式，提供后备（fallback）值（null）。

当给定的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 没有外层的默认选区样式时，由 [of] 返回。

此构造函数创建了一个带有无效 [child] 的 [DefaultTextStyle](https://www.yuque.com/thyname/flutter.widgets/defaulttextstyle)，这意味着构造出的值无法被并入 Widget 树中。

### merge()

```dart
Widget merge({Key? key, Color? cursorColor, Color? selectionColor, MouseCursor? mouseCursor, required Widget child})
```

创建一个默认选区样式，覆盖当前作用域下 Widget 树中此处的选区样式。

任何非 null 的参数都会替换该 Widget 被插入处的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 上对应的默认选区样式属性。

### defaultColor

```dart
Color defaultColor
```

默认的光标和选区颜色（半透明灰色）。

当指定的选区颜色为 null 时，[Text](https://www.yuque.com/thyname/flutter.widgets/text) Widget 会使用此颜色。

### cursorColor

```dart
Color? cursorColor
```

文本字段光标的颜色。

光标指示当前文本插入点在字段中的位置。

### selectionColor

```dart
Color? selectionColor
```

选中文本的背景颜色。

### mouseCursor

```dart
MouseCursor? mouseCursor
```

鼠标指针悬停在可选中的 Text Widget 上时使用的 [MouseCursor](https://www.yuque.com/thyname/flutter.services/mousecursor)。

如果此属性为 null，则会使用 [SystemMouseCursors.text]。

### of()

```dart
DefaultSelectionStyle of(BuildContext context)
```

最近的一个封闭给定上下文的此类实例。

如果不存在这样的实例，则返回由 [DefaultSelectionStyle.fallback] 创建的实例，其中包含后备值。

典型用法如下：

```dart
DefaultSelectionStyle style = DefaultSelectionStyle.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(DefaultSelectionStyle oldWidget)
```
