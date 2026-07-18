@docImport 'package:flutter/material.dart'; @docImport 'package:flutter_localizations/flutter_localizations.dart';

@docImport 'app.dart'; @docImport 'reorderable_list.dart';

# LocalizationsDelegate

```dart
abstract class LocalizationsDelegate<T> {}
```

用于加载一组类型为 `T` 的本地化资源的工厂类，这些资源将由 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) Widget 加载。

典型应用中只有一个由 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 创建的 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) Widget，并通过应用的 `localizationsDelegates` 参数（一个委托列表）进行配置。委托的 [type] 用于标识各个委托的 [load] 方法所创建的对象。

此处 `T` 的取值可以是例如 [MaterialLocalizations](https://www.yuque.com/thyname/flutter.material/materiallocalizations) 这样的类。

### LocalizationsDelegate()

```dart
LocalizationsDelegate()
```

抽象 const 构造函数。该构造函数使子类能够提供 const 构造函数，从而可以在 const 表达式中使用。

### isSupported()

```dart
bool isSupported(Locale locale)
```

此委托是否可以加载给定 `locale` 的资源。

如果此委托的 [load] 方法所加载的 `T` 实例支持给定 `locale` 的语言，则返回 true。

### load()

```dart
Future<T> load(Locale locale)
```

开始为 `locale` 加载资源。当资源加载完成时，返回的 future 完成。

假定此方法返回的对象包含一组相关的字符串资源集合（通常每个资源对应一个方法）。该对象将通过 [Localizations.of] 获取。

### shouldReload()

```dart
bool shouldReload(LocalizationsDelegate<T> old)
```

如果应通过调用 [load] 方法重新加载此委托的资源，则返回 true。

每当其 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) Widget 重建时都会调用此方法。如果返回 true，则在 [load] 完成后，依赖的 Widget 将被重建。

### type

```dart
Type get type
```

[load] 方法返回的对象的类型，默认为 T。

此类型用于从 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) 继承组件（InheritedWidget）中获取由此 [LocalizationsDelegate](https://www.yuque.com/thyname/flutter.widgets/localizationsdelegate) "加载" 的对象。例如，由 `LocalizationsDelegate<Foo>` 加载的对象可通过以下方式获取：

```dart
Foo foo = Localizations.of<Foo>(context, Foo)!;
```

通常不需要重写此获取器。

### toString()

```dart
String toString()
```

# WidgetsLocalizations

```dart
abstract class WidgetsLocalizations {}
```

为 Flutter 框架最底层提供本地化资源值的接口。

此类还通过 [textDirection] 属性将 locale 映射到特定的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)。

另请参阅：

- [DefaultWidgetsLocalizations](https://www.yuque.com/thyname/flutter.widgets/defaultwidgetslocalizations)，它实现了此接口并支持多种 locale。

### textDirection

```dart
TextDirection get textDirection
```

此 locale 中文本的阅读方向。

### reorderItemToStart

```dart
String get reorderItemToStart
```

[SliverReorderableList](https://www.yuque.com/thyname/flutter.widgets/sliverreorderablelist) 用于将列表中的某一项重新排序到列表起始位置时使用的语义标签。

### reorderItemToEnd

```dart
String get reorderItemToEnd
```

[SliverReorderableList](https://www.yuque.com/thyname/flutter.widgets/sliverreorderablelist) 用于将列表中的某一项重新排序到列表末尾位置时使用的语义标签。

### reorderItemUp

```dart
String get reorderItemUp
```

[SliverReorderableList](https://www.yuque.com/thyname/flutter.widgets/sliverreorderablelist) 用于将列表中的某一项向上移动一个位置时使用的语义标签。

### reorderItemDown

```dart
String get reorderItemDown
```

[SliverReorderableList](https://www.yuque.com/thyname/flutter.widgets/sliverreorderablelist) 用于将列表中的某一项向下移动一个位置时使用的语义标签。

### reorderItemLeft

```dart
String get reorderItemLeft
```

[SliverReorderableList](https://www.yuque.com/thyname/flutter.widgets/sliverreorderablelist) 用于将列表中的某一项向左移动一个位置时使用的语义标签。

### reorderItemRight

```dart
String get reorderItemRight
```

[SliverReorderableList](https://www.yuque.com/thyname/flutter.widgets/sliverreorderablelist) 用于将列表中的某一项向右移动一个位置时使用的语义标签。

### searchResultsFound

```dart
String get searchResultsFound
```

当选项列表从空变为非空时，[RawAutocomplete](https://www.yuque.com/thyname/flutter.widgets/rawautocomplete) 使用的语义标签。

### noResultsFound

```dart
String get noResultsFound
```

当选项列表从非空变为空时，[RawAutocomplete](https://www.yuque.com/thyname/flutter.widgets/rawautocomplete) 使用的语义标签。

### copyButtonLabel

```dart
String get copyButtonLabel
```

"复制"编辑按钮和菜单项的标签。

### cutButtonLabel

```dart
String get cutButtonLabel
```

"剪切"编辑按钮和菜单项的标签。

### pasteButtonLabel

```dart
String get pasteButtonLabel
```

"粘贴"编辑按钮和菜单项的标签。

### selectAllButtonLabel

```dart
String get selectAllButtonLabel
```

"全选"编辑按钮和菜单项的标签。

### lookUpButtonLabel

```dart
String get lookUpButtonLabel
```

"查询"编辑按钮和菜单项的标签。

### searchWebButtonLabel

```dart
String get searchWebButtonLabel
```

"网页搜索"编辑按钮和菜单项的标签。

### shareButtonLabel

```dart
String get shareButtonLabel
```

"分享"编辑按钮和菜单项的标签。

### radioButtonUnselectedLabel

```dart
String get radioButtonUnselectedLabel
```

未选中单选按钮的无障碍提示。

### of()

```dart
WidgetsLocalizations of(BuildContext context)
```

从最近的、包含给定 context 的 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) 实例中获取的 `WidgetsLocalizations`。

此方法只是以下写法的便捷简写：`Localizations.of<WidgetsLocalizations>(context, WidgetsLocalizations)!`。

对此类所定义的本地化资源的引用通常都通过此方法编写。例如：

```dart
textDirection: WidgetsLocalizations.of(context).textDirection,
```

# DefaultWidgetsLocalizations

```dart
class DefaultWidgetsLocalizations implements WidgetsLocalizations {}
```

widgets 库的美式英语本地化实现。

另请参阅：

- [GlobalWidgetsLocalizations]，它为多种语言提供 widgets 本地化。
- [WidgetsApp.localizationsDelegates]，默认情况下会自动包含 [DefaultWidgetsLocalizations.delegate]。

### DefaultWidgetsLocalizations()

```dart
DefaultWidgetsLocalizations()
```

构造一个对象，为 widgets 库定义（仅限）美式英语的本地化值。

[LocalizationsDelegate](https://www.yuque.com/thyname/flutter.widgets/localizationsdelegate) 的实现通常会调用静态方法 [load]

### reorderItemUp

```dart
String get reorderItemUp
```

### reorderItemDown

```dart
String get reorderItemDown
```

### reorderItemLeft

```dart
String get reorderItemLeft
```

### reorderItemRight

```dart
String get reorderItemRight
```

### reorderItemToEnd

```dart
String get reorderItemToEnd
```

### reorderItemToStart

```dart
String get reorderItemToStart
```

### searchResultsFound

```dart
String get searchResultsFound
```

### noResultsFound

```dart
String get noResultsFound
```

### copyButtonLabel

```dart
String get copyButtonLabel
```

### cutButtonLabel

```dart
String get cutButtonLabel
```

### pasteButtonLabel

```dart
String get pasteButtonLabel
```

### selectAllButtonLabel

```dart
String get selectAllButtonLabel
```

### lookUpButtonLabel

```dart
String get lookUpButtonLabel
```

### searchWebButtonLabel

```dart
String get searchWebButtonLabel
```

### shareButtonLabel

```dart
String get shareButtonLabel
```

### radioButtonUnselectedLabel

```dart
String get radioButtonUnselectedLabel
```

### textDirection

```dart
TextDirection get textDirection
```

### load()

```dart
Future<WidgetsLocalizations> load(Locale locale)
```

创建一个对象，为 widgets 库最底层提供美式英语资源值。

[locale] 参数将被忽略。

此方法通常用于创建 [LocalizationsDelegate](https://www.yuque.com/thyname/flutter.widgets/localizationsdelegate)。[WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 默认就是这样做的。

### delegate

```dart
LocalizationsDelegate<WidgetsLocalizations> delegate
```

使用 [DefaultWidgetsLocalizations.load] 创建此类实例的 [LocalizationsDelegate](https://www.yuque.com/thyname/flutter.widgets/localizationsdelegate)。

[WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 会自动将此值添加到 [WidgetsApp.localizationsDelegates] 中。

# Localizations

```dart
class Localizations extends StatefulWidget {}
```

为其 `child` 定义 [Locale](https://www.yuque.com/thyname/dart.ui/locale)，以及该子级所依赖的本地化资源。

## Defining localized resources

{@tool snippet}

以下类基于 [Dart `intl` 包](https://github.com/dart-lang/i18n/tree/main/pkgs/intl) 定义。使用 `intl` 包并非必需。

```dart
class MyLocalizations {
  MyLocalizations(this.locale);

  final Locale locale;

  static Future<MyLocalizations> load(Locale locale) {
    return initializeMessages(locale.toString())
      .then((void _) {
        return MyLocalizations(locale);
      });
  }

  static MyLocalizations of(BuildContext context) {
    return Localizations.of<MyLocalizations>(context, MyLocalizations)!;
  }

  String title() => Intl.message('<title>', name: 'title', locale: locale.toString());
  // ... more Intl.message() methods like title()
}
```

{@end-tool} 基于 `intl` 包的类会导入一个生成的消息目录（message catalog），该目录提供 `initializeMessages()` 函数以及 `Intl.message()` 所需的按 locale 划分的后备存储。该消息目录由 `intl` 工具生成，该工具会分析包含 `Intl.message()` 调用的类的源代码。在本例中，这仅指 `MyLocalizations` 类。

在遵循此示例结构的前提下，也可以选择其他方式来加载和查找本地化资源。

## Loading localized resources

本地化资源由 [LocalizationsDelegate](https://www.yuque.com/thyname/flutter.widgets/localizationsdelegate) 列表 `delegates` 加载。每个委托本质上都是一组本地化资源的工厂。之所以存在多个委托，是因为应用内的本地化资源来源可能有多个。

委托通常是 [LocalizationsDelegate](https://www.yuque.com/thyname/flutter.widgets/localizationsdelegate) 的简单子类，并重写 [LocalizationsDelegate.load]。例如，上面定义的 `MyLocalizations` 类对应的委托如下：

```dart
// continuing from previous example...
class _MyDelegate extends LocalizationsDelegate<MyLocalizations> {
  @override
  Future<MyLocalizations> load(Locale locale) => MyLocalizations.load(locale);

  @override
  bool isSupported(Locale locale) {
    // in a real implementation this would only return true for
    // locales that are definitely supported.
    return true;
  }

  @override
  bool shouldReload(_MyDelegate old) => false;
}
```

每个委托都可以视为一个工厂，用于生成封装了一组本地化资源的对象。这些对象通过运行时类型并借助 [Localizations.of] 获取。

[WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 类会创建一个 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) Widget，因此大多数应用无需自行创建。widget app 的 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) 委托可以通过 [WidgetsApp.localizationsDelegates] 进行初始化。[MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 类也提供了 `localizationsDelegates` 参数，该参数只是被直接传递给 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp)。

## Obtaining localized resources for use in user interfaces

应用应通过 `Localizations.of<MyLocalizations>(context, MyLocalizations)` 获取本地化资源集合，其中 MyLocalizations 是特定于应用的类，为每个资源定义一个函数。按照惯例，这通常通过自定义本地化资源类（即上面示例中的 `MyLocalizations`）上的静态 `.of` 方法完成。

例如，使用上面定义的 `MyLocalizations` 类，可以按如下方式查找本地化的标题字符串：

```dart
// continuing from previous example...
MyLocalizations.of(context).title()
```

如果 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) 使用新的 `locale` 重建，那么在相应资源加载完成后，与 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) `context` 对应的 Widget 子树也会被重建。

此类本质上是一个 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)。如果它使用新的 `locale` 或不同的委托列表进行重建，或者其任一委托的 [LocalizationsDelegate.shouldReload()] 方法返回 true，那么在新 locale 的资源加载完成后，所有通过调用 `Localizations.of(context)` 建立了依赖关系的 Widget 都会被重建。

[Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) Widget 还会实例化 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)，以便为本地化资源提供恰当的 [Directionality.textDirection] 支持。

### Localizations()

```dart
Localizations({dynamic key, required Locale locale, required List<LocalizationsDelegate<dynamic>> delegates, Widget? child, bool isApplicationLevel = false})
```

创建一个可从中获取本地化资源（如翻译后的字符串）的 Widget。

### Localizations.override()

```dart
Localizations.override({Key? key, required BuildContext context, Locale? locale, List<LocalizationsDelegate<dynamic>>? delegates, Widget? child})
```

为 `child` 重写继承而来的 [Locale](https://www.yuque.com/thyname/dart.ui/locale) 或 [LocalizationsDelegate](https://www.yuque.com/thyname/flutter.widgets/localizationsdelegate) 列表。

此工厂构造函数用于（通常较少见的）情况：应用的某一部分需要使用与设备所定义的 locale 不同的 locale 进行本地化，或者其本地化资源需要来自与 [WidgetsApp.localizationsDelegates] 所定义的列表不同的 [LocalizationsDelegate](https://www.yuque.com/thyname/flutter.widgets/localizationsdelegate) 列表。

例如，你可以指定 `myWidget` 只使用美式英语 locale 进行本地化：

```dart
Widget build(BuildContext context) {
  return Localizations.override(
    context: context,
    locale: const Locale('en', 'US'),
    child: myWidget,
  );
}
```

`locale` 和 `delegates` 参数默认为最近的 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) 祖先节点的 [Localizations.locale] 和 [Localizations.delegates] 值。

要为整个应用重写 [Localizations.locale] 或 [Localizations.delegates]，请指定 [WidgetsApp.locale] 或 [WidgetsApp.localizationsDelegates]（或者为 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 指定相同的参数）。

### locale

```dart
Locale locale
```

[Localizations.of] 返回的资源将特定于此 locale。

### delegates

```dart
List<LocalizationsDelegate<dynamic>> delegates
```

此列表共同定义了可通过 [Localizations.of] 获取的本地化资源对象。

### child

```dart
Widget? child
```

此 Widget 在树中的下级 Widget。

{@macro flutter.widgets.ProxyWidget.child}

### isApplicationLevel

```dart
bool isApplicationLevel
```

此项是否为代表应用 locale 的主本地化 Widget。

### localeOf()

```dart
Locale localeOf(BuildContext context)
```

与 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) `context` 对应的 Widget 树中，Localizations Widget 的 locale。

如果作用域内没有 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) Widget，则 [Localizations.localeOf] 方法将抛出异常。

### maybeLocaleOf()

```dart
Locale? maybeLocaleOf(BuildContext context)
```

与 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) `context` 对应的 Widget 树中，Localizations Widget 的 locale。

如果作用域内没有 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) Widget，则此函数将返回 null。

### of()

```dart
T? of<T>(BuildContext context, Type type)
```

为与给定 `context` 对应的 Widget 树，返回给定 `type` 的本地化资源对象。

如果在给定 `context` 内不存在给定 `type` 的资源对象，则返回 null。

此方法通常由 `type` 类上的静态工厂方法使用。例如，Flutter 的 MaterialLocalizations 类会通过如下方式定义的方法查找 Material 资源：

```dart
static MaterialLocalizations of(BuildContext context) {
  return Localizations.of<MaterialLocalizations>(context, MaterialLocalizations)!;
}
```

### createState()

```dart
State<Localizations> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# LocalizationsResolver

```dart
class LocalizationsResolver extends ChangeNotifier with WidgetsBindingObserver {}
```

用于管理本地化解析的辅助类。

另请参阅：

- [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp)，它使用 [LocalizationsResolver](https://www.yuque.com/thyname/flutter.widgets/localizationsresolver) 来处理 locale。

### LocalizationsResolver()

```dart
LocalizationsResolver({required Iterable<Locale> supportedLocales, Locale? locale, LocaleListResolutionCallback? localeListResolutionCallback, LocaleResolutionCallback? localeResolutionCallback, Iterable<LocalizationsDelegate<Object?>>? localizationsDelegates})
```

创建一个 [LocalizationsResolver](https://www.yuque.com/thyname/flutter.widgets/localizationsresolver)，用于从 [supportedLocales] 集合中确定最匹配的 locale。

如果提供了该参数，locale 解析将尝试使用 [locale] 作为当前 locale，而不是系统 locale。

可以通过提供 [localeListResolutionCallback] 或 [localeResolutionCallback] 来重写 locale 解析行为。

通过 [localizationsDelegates] 设置的委托共同定义了某个 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) Widget 的所有本地化资源。

另请参阅：

- [LocalizationsResolver.localeListResolutionCallback] 和 [LocalizationsResolver.localeResolutionCallback]，了解有关 locale 解析行为的更多细节。
- [LocalizationsDelegate](https://www.yuque.com/thyname/flutter.widgets/localizationsdelegate)，了解有关为 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) Widget 提供本地化资源的更多细节。

### dispose()

```dart
void dispose()
```

### update()

```dart
void update({required Locale? locale, required LocaleListResolutionCallback? localeListResolutionCallback, required LocaleResolutionCallback? localeResolutionCallback, required Iterable<LocalizationsDelegate<Object?>>? localizationsDelegates, required Iterable<Locale> supportedLocales})
```

替换一个或多个用于本地化解析的属性，并重新解析 locale。

### locale

```dart
Locale get locale
```

根据当前平台 locale 和提供的 [supportedLocales] 集合所解析出的当前 [Locale](https://www.yuque.com/thyname/dart.ui/locale)。

### localizationsDelegates

```dart
Iterable<LocalizationsDelegate<Object?>> get localizationsDelegates
```

{@macro flutter.widgets.widgetsApp.localizationsDelegates}

### localeListResolutionCallback

```dart
LocaleListResolutionCallback? get localeListResolutionCallback
```

{@macro flutter.widgets.widgetsApp.localeListResolutionCallback}

另请参阅：

- [basicLocaleListResolution](https://www.yuque.com/thyname/flutter.widgets/basiclocalelistresolution)，默认的 locale 解析算法。

### localeResolutionCallback

```dart
LocaleResolutionCallback? get localeResolutionCallback
```

{@macro flutter.widgets.LocaleResolutionCallback}

### supportedLocales

```dart
Iterable<Locale> get supportedLocales
```

{@macro flutter.widgets.widgetsApp.supportedLocales}

另请参阅：

- [localeResolutionCallback]，一个应用回调，在设备 locale 发生变化时用于解析应用的 locale。
- [localizationsDelegates]，共同定义此应用所使用的所有本地化资源。
- [basicLocaleListResolution](https://www.yuque.com/thyname/flutter.widgets/basiclocalelistresolution)，默认的 locale 解析算法。
