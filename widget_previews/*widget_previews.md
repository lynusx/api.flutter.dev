@docImport 'package:/flutter/cupertino.dart'; @docImport 'package:/flutter/material.dart';

# PreviewTheme

```dart
typedef PreviewTheme = PreviewThemeData Function()
```

用于构建 [Preview](https://www.yuque.com/thyname/flutter.widget_previews/preview) 时创建主题数据的回调函数签名。

# WidgetWrapper

```dart
typedef WidgetWrapper = Widget Function(Widget)
```

用于在创建 [Preview](https://www.yuque.com/thyname/flutter.widget_previews/preview) 时使用另一个 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 包装某个 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 的回调函数签名。

# PreviewLocalizations

```dart
typedef PreviewLocalizations = PreviewLocalizationsData Function()
```

用于构建 [Preview](https://www.yuque.com/thyname/flutter.widget_previews/preview) 时创建本地化数据的回调函数签名。

# Preview

```dart
base class Preview {}
```

用于标记返回 widget 预览的函数的注解。

注意：此接口尚不稳定，**将会发生变化**。

{@tool snippet}

标注了 `@Preview()` 的函数必须返回 `Widget` 或 `WidgetBuilder`，并且必须是公开的。此注解只能应用于顶层函数、类中定义的静态方法，以及不带必需参数的公共 `Widget` 构造函数和工厂函数。

```dart
@Preview(name: 'Top-level preview')
Widget preview() => const Text('Foo');

@Preview(name: 'Builder preview')
WidgetBuilder builderPreview() {
  return (BuildContext context) {
    return const Text('Builder');
  };
}

class MyWidget extends StatelessWidget {
  @Preview(name: 'Constructor preview')
  const MyWidget.preview({super.key});

  @Preview(name: 'Factory constructor preview')
  factory MyWidget.factoryPreview() => const MyWidget.preview();

  @Preview(name: 'Static preview')
  static Widget previewStatic() => const Text('Static');

  @override
  Widget build(BuildContext context) {
    return const Text('MyWidget');
  }
}
```

{@end-tool}

**重要提示：** 提供给 `@Preview()` 注解的所有值都必须是常量，回调参数也必须是静态且非私有的。在运行时创建 [Preview](https://www.yuque.com/thyname/flutter.widget_previews/preview) 实例时（包括在 [Preview.transform()] 中），不受这些限制约束。

另请参阅：

- [MultiPreview](https://www.yuque.com/thyname/flutter.widget_previews/multipreview)，一个允许通过单个注解创建多个 [Preview](https://www.yuque.com/thyname/flutter.widget_previews/preview) 的基类。
- [flutter.dev/to/widget-previews](https://flutter.dev/to/widget-previews)，了解 widget 预览入门的详细信息。

### Preview()

```dart
Preview({String group = 'Default', String? name, Size? size, double? textScaleFactor, WidgetWrapper? wrapper, PreviewTheme? theme, Brightness? brightness, PreviewLocalizations? localizations})
```

用于标记返回 widget 预览的函数的注解。

### group

```dart
String group
```

{@template widget_preview_group} 该预览所属的分组。

具有相同分组名称的预览将在预览工具中一起显示。如果未提供，则使用 'Default'。{@endtemplate}

### name

```dart
String? name
```

{@template widget_preview_name} 与预览一起显示的描述文字。

如果未提供，则不会关联任何名称。{@endtemplate}

### size

```dart
Size? size
```

{@template widget_preview_size} 应用于被预览 widget 的人工约束。

如果未提供，被预览的 widget 将尝试自行设置约束。

如果某个维度的值为 `double.infinity`，被预览的 widget 将尝试在相应维度上自行设置约束。

若要仅设置一个维度并让另一个维度自行设置约束，请使用 [Size.fromHeight] 或 [Size.fromWidth]。{@endtemplate}

### textScaleFactor

```dart
double? textScaleFactor
```

{@template widget_preview_text_scale_factor} 对被预览 widget 内的文本应用字体缩放。

如果未提供，将使用 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 提供的默认文本缩放系数。{@endtemplate}

### wrapper

```dart
WidgetWrapper? wrapper
```

{@template widget_preview_wrapper} 将被预览的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 包装在一个 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 树中。

此函数可用于执行依赖注入，或设置正确渲染预览所需的其他脚手架结构。{@endtemplate}

{@template widget_preview_must_be_static_const} 注意：当作为参数提供给注解时，此值必须是对静态、公共函数的引用，该函数须定义为类中的顶层函数或静态成员。{@endtemplate}

### theme

```dart
PreviewTheme? theme
```

{@template widget_preview_theme} 用于返回要应用于被预览 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 的 Material 和 Cupertino 主题数据的回调函数。{@endtemplate}

{@macro widget_preview_must_be_static_const}

### brightness

```dart
Brightness? brightness
```

{@template widget_preview_brightness} 设置初始主题明暗模式。

如果未提供，将使用当前系统默认的明暗模式。{@endtemplate}

### localizations

```dart
PreviewLocalizations? localizations
```

{@template widget_preview_localizations} 用于返回要应用于被预览 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 的本地化配置的回调函数。{@endtemplate}

{@macro widget_preview_must_be_static_const}

### transform()

```dart
Preview transform()
```

对当前 [Preview](https://www.yuque.com/thyname/flutter.widget_previews/preview) 应用转换。

重写此方法可以让自定义 [Preview](https://www.yuque.com/thyname/flutter.widget_previews/preview) 实现初始化更复杂的预览，而这些预览由于用于注解的常量构造函数的限制而无法以其他方式实现。

另请参阅：

- [PreviewBuilder](https://www.yuque.com/thyname/flutter.widget_previews/previewbuilder)，一个用于构建和修改 [Preview](https://www.yuque.com/thyname/flutter.widget_previews/preview) 的工具类。

### toBuilder()

```dart
PreviewBuilder toBuilder()
```

创建一个使用此预览中设置的值初始化的 [PreviewBuilder](https://www.yuque.com/thyname/flutter.widget_previews/previewbuilder)。

# MultiPreview

```dart
abstract base class MultiPreview {}
```

用于定义自定义"多重预览"注解的基类。

用 [MultiPreview](https://www.yuque.com/thyname/flutter.widget_previews/multipreview) 的实例标记返回 widget 预览的函数，等价于将 `previews` 字段中的每个 [Preview](https://www.yuque.com/thyname/flutter.widget_previews/preview) 实例分别应用于该函数。

{@tool snippet} 此示例展示了为单个预览函数定义多个预览的两种方法。

第一种方法使用 [MultiPreview](https://www.yuque.com/thyname/flutter.widget_previews/multipreview) 实现，通过浅色和深色模式主题创建预览。

第二种方法使用多个 [Preview](https://www.yuque.com/thyname/flutter.widget_previews/preview) 注解来实现相同的效果。

```dart
final class BrightnessPreview extends MultiPreview {
  const BrightnessPreview();

  @override
  // ignore: avoid_field_initializers_in_const_classes
  final List<Preview> previews = const <Preview>[
    Preview(name: 'Light', brightness: Brightness.light),
    Preview(name: 'Dark', brightness: Brightness.dark),
  ];
}

// Using a multi-preview to create 'Light' and 'Dark' previews.
@BrightnessPreview()
WidgetBuilder brightnessPreview() {
  return (BuildContext context) {
    final ThemeData theme = Theme.of(context);
    return Text('Brightness: ${theme.brightness}');
  };
}

// Using multiple Preview annotations to create 'Light' and 'Dark' previews.
@Preview(name: 'Light', brightness: Brightness.light)
@Preview(name: 'Dark', brightness: Brightness.dark)
WidgetBuilder brightnessPreviewManual() {
  return (BuildContext context) {
    final ThemeData theme = Theme.of(context);
    return Text('Brightness: ${theme.brightness}');
  };
}
```

{@end-tool}

**重要提示：** 提供给 [MultiPreview](https://www.yuque.com/thyname/flutter.widget_previews/multipreview) 派生注解的所有值都必须是常量，回调参数也必须是静态且非私有的。在运行时创建 [MultiPreview](https://www.yuque.com/thyname/flutter.widget_previews/multipreview) 实例时（包括在 [Preview.transform()] 中），不受这些限制约束。

另请参阅：

- [Preview](https://www.yuque.com/thyname/flutter.widget_previews/preview)，用于标记返回 widget 预览的函数的注解。
- [flutter.dev/to/widget-previews](https://flutter.dev/to/widget-previews)，了解 widget 预览入门的详细信息。

### MultiPreview()

```dart
MultiPreview()
```

创建一个 [MultiPreview](https://www.yuque.com/thyname/flutter.widget_previews/multipreview) 注解实例。

### previews

```dart
List<Preview> get previews
```

为被注解函数创建的一组 [Preview](https://www.yuque.com/thyname/flutter.widget_previews/preview)。

### transform()

```dart
List<Preview> transform()
```

对 [previews] 中的每个 [Preview](https://www.yuque.com/thyname/flutter.widget_previews/preview) 应用转换。

重写此方法可以让 [MultiPreview](https://www.yuque.com/thyname/flutter.widget_previews/multipreview) 实现初始化更复杂的预览，而这些预览由于用于注解的常量构造函数的限制而无法以其他方式实现。

另请参阅：

- [PreviewBuilder](https://www.yuque.com/thyname/flutter.widget_previews/previewbuilder)，一个用于构建和修改 [Preview](https://www.yuque.com/thyname/flutter.widget_previews/preview) 的工具类。

# PreviewBuilder

```dart
final class PreviewBuilder {}
```

用于构建 [Preview](https://www.yuque.com/thyname/flutter.widget_previews/preview) 实例的工具类。

### PreviewBuilder()

```dart
PreviewBuilder()
```

创建一个不带初始状态的 [PreviewBuilder](https://www.yuque.com/thyname/flutter.widget_previews/previewbuilder)。

### group

```dart
String? group
```

{@macro widget_preview_group}

### name

```dart
String? name
```

{@macro widget_preview_name}

### size

```dart
Size? size
```

{@macro widget_preview_size}

### textScaleFactor

```dart
double? textScaleFactor
```

{@macro widget_preview_text_scale_factor}

### wrapper

```dart
WidgetWrapper? wrapper
```

{@macro widget_preview_wrapper}

### addWrapper()

```dart
void addWrapper(WidgetWrapper newWrapper)
```

将 [newWrapper] 应用到当前 [wrapper] 的返回值上。

### theme

```dart
PreviewTheme? theme
```

{@macro widget_preview_theme}

### brightness

```dart
Brightness? brightness
```

{@macro widget_preview_brightness}

### localizations

```dart
PreviewLocalizations? localizations
```

{@macro widget_preview_localizations}

### build()

```dart
Preview build()
```

返回根据构建器状态创建的 [Preview](https://www.yuque.com/thyname/flutter.widget_previews/preview) 实例。

# PreviewLocalizationsData

```dart
base class PreviewLocalizationsData {}
```

用于 widget 预览的本地化对象和回调函数的集合。

### PreviewLocalizationsData()

```dart
PreviewLocalizationsData({Locale? locale, List<Locale> supportedLocales = const <Locale>[Locale('en', 'US')], Iterable<LocalizationsDelegate<Object?>>? localizationsDelegates, LocaleListResolutionCallback? localeListResolutionCallback, LocaleResolutionCallback? localeResolutionCallback})
```

创建一个用于 widget 预览的本地化对象和回调函数的集合。

### locale

```dart
Locale? locale
```

{@macro flutter.widgets.widgetsApp.locale}

另请参阅：

- [localeResolutionCallback]，可以覆盖默认的 [supportedLocales] 匹配算法。
- [localizationsDelegates]，共同定义此预览使用的所有本地化资源。

### supportedLocales

```dart
List<Locale> supportedLocales
```

{@macro flutter.widgets.widgetsApp.supportedLocales}

另请参阅：

- [localeResolutionCallback]，当设备语言区域发生变化时用于解析应用语言区域的应用回调。
- [localizationsDelegates]，共同定义此应用使用的所有本地化资源。
- [basicLocaleListResolution](https://www.yuque.com/thyname/flutter.widgets/basiclocalelistresolution)，默认的语言区域解析算法。

### localizationsDelegates

```dart
Iterable<LocalizationsDelegate<Object?>>? localizationsDelegates
```

此预览的 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) widget 的委托。

这些委托共同定义了此预览的 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) widget 的所有本地化资源。

### localeListResolutionCallback

```dart
LocaleListResolutionCallback? localeListResolutionCallback
```

{@macro flutter.widgets.widgetsApp.localeListResolutionCallback}

此回调考虑整个首选语言区域列表。

该算法应能够处理 null 或空的首选语言区域列表，这表示 Flutter 尚未从平台接收到语言区域信息。

另请参阅：

- [basicLocaleListResolution](https://www.yuque.com/thyname/flutter.widgets/basiclocalelistresolution)，默认的语言区域解析算法。

### localeResolutionCallback

```dart
LocaleResolutionCallback? localeResolutionCallback
```

{@macro flutter.widgets.widgetsApp.localeListResolutionCallback}

此回调仅考虑默认语言区域，即首选语言区域列表中的第一个语言区域。建议优先设置 [localeListResolutionCallback] 而非 [localeResolutionCallback]，因为它提供了完整的首选语言区域列表。

该算法应能够处理 null 语言区域，这表示 Flutter 尚未从平台接收到语言区域信息。

另请参阅：

- [basicLocaleListResolution](https://www.yuque.com/thyname/flutter.widgets/basiclocalelistresolution)，默认的语言区域解析算法。

# PreviewThemeData

```dart
base class PreviewThemeData {}
```

用于 widget 预览的 [ThemeData](https://www.yuque.com/thyname/flutter.material/themedata) 和 [CupertinoThemeData](https://www.yuque.com/thyname/flutter.cupertino/cupertinothemedata) 实例的集合。

注意：此接口尚不稳定，**将会发生变化**。

### PreviewThemeData()

```dart
PreviewThemeData({ThemeData? materialLight, ThemeData? materialDark, CupertinoThemeData? cupertinoLight, CupertinoThemeData? cupertinoDark})
```

创建一个用于 widget 预览的 [ThemeData](https://www.yuque.com/thyname/flutter.material/themedata) 和 [CupertinoThemeData](https://www.yuque.com/thyname/flutter.cupertino/cupertinothemedata) 实例的集合。

如果未为特定配置提供主题，则不会应用任何主题数据，将使用默认主题。

### materialLight

```dart
ThemeData? materialLight
```

启用浅色模式时应用的 Material [ThemeData](https://www.yuque.com/thyname/flutter.material/themedata)。

### materialDark

```dart
ThemeData? materialDark
```

启用深色模式时应用的 Material [ThemeData](https://www.yuque.com/thyname/flutter.material/themedata)。

### cupertinoLight

```dart
CupertinoThemeData? cupertinoLight
```

启用浅色模式时应用的 Cupertino [CupertinoThemeData](https://www.yuque.com/thyname/flutter.cupertino/cupertinothemedata)。

### cupertinoDark

```dart
CupertinoThemeData? cupertinoDark
```

启用深色模式时应用的 Cupertino [CupertinoThemeData](https://www.yuque.com/thyname/flutter.cupertino/cupertinothemedata)。

### themeForBrightness()

```dart
(ThemeData?, CupertinoThemeData?) themeForBrightness(Brightness brightness)
```

返回与 [brightness] 的值对应的一对 [ThemeData](https://www.yuque.com/thyname/flutter.material/themedata) 和 [CupertinoThemeData](https://www.yuque.com/thyname/flutter.cupertino/cupertinothemedata)。
