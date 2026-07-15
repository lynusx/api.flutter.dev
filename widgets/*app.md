@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

@docImport 'heroes.dart'; @docImport 'overlay.dart'; @docImport 'view.dart';

# LocaleListResolutionCallback

```dart
typedef LocaleListResolutionCallback = Locale? Function(List<Locale>? locales, Iterable<Locale> supportedLocales)
```

[WidgetsApp.localeListResolutionCallback] 的签名。

[LocaleListResolutionCallback](https://www.yuque.com/thyname/flutter.widgets/localelistresolutioncallback) 负责在应用启动时以及用户更改设备的语言区域列表时，计算应用的 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) 对象所使用的语言区域。

[locales] 列表是应用启动时设备的首选语言区域列表，或是应用启动后用户选择的设备首选语言区域列表。该列表按优先级排序。如果此列表为 null 或为空，则表示 Flutter 尚未从平台接收到语言区域信息。[supportedLocales] 参数即为 [WidgetsApp.supportedLocales] 的值。

另请参阅：

- [LocaleResolutionCallback](https://www.yuque.com/thyname/flutter.widgets/localeresolutioncallback)，它只接受一个默认语言区域（而不是列表），并且仅在此回调失败或为 null 时才会被尝试调用。建议优先使用 [LocaleListResolutionCallback](https://www.yuque.com/thyname/flutter.widgets/localelistresolutioncallback) 而非 [LocaleResolutionCallback](https://www.yuque.com/thyname/flutter.widgets/localeresolutioncallback)。

# LocaleResolutionCallback

```dart
typedef LocaleResolutionCallback = Locale? Function(Locale? locale, Iterable<Locale> supportedLocales)
```

{@template flutter.widgets.LocaleResolutionCallback} [WidgetsApp.localeResolutionCallback] 的签名。

建议尽可能提供 [LocaleListResolutionCallback](https://www.yuque.com/thyname/flutter.widgets/localelistresolutioncallback) 而非 [LocaleResolutionCallback](https://www.yuque.com/thyname/flutter.widgets/localeresolutioncallback)，因为 [LocaleResolutionCallback](https://www.yuque.com/thyname/flutter.widgets/localeresolutioncallback) 只能接收 [LocaleListResolutionCallback](https://www.yuque.com/thyname/flutter.widgets/localelistresolutioncallback) 所提供信息的一个子集。

[LocaleResolutionCallback](https://www.yuque.com/thyname/flutter.widgets/localeresolutioncallback) 负责在 [LocaleListResolutionCallback](https://www.yuque.com/thyname/flutter.widgets/localelistresolutioncallback) 失败或未提供的情况下，在应用启动时以及用户更改设备的默认语言区域时，计算应用的 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) 对象所使用的语言区域。

如果应用是通过 [WidgetsApp.new] 的 `locale` 参数创建并指定了特定语言区域，则此回调也会被使用。

[locale] 是 [WidgetsApp.locale] 的值，或是应用启动时设备的默认语言区域，或是应用启动后用户选择的设备语言区域。默认语言区域是首选语言区域列表中的第一个语言区域。如果 [locale] 为 null，则表示 Flutter 尚未从平台接收到语言区域信息。[supportedLocales] 参数即为 [WidgetsApp.supportedLocales] 的值。

另请参阅：

- [LocaleListResolutionCallback](https://www.yuque.com/thyname/flutter.widgets/localelistresolutioncallback)，它接受一个首选语言区域列表（而不是单个语言区域）。[LocaleListResolutionCallback](https://www.yuque.com/thyname/flutter.widgets/localelistresolutioncallback) 的解析结果优先于 [LocaleResolutionCallback](https://www.yuque.com/thyname/flutter.widgets/localeresolutioncallback)。{@endtemplate}

# basicLocaleListResolution()

```dart
Locale basicLocaleListResolution(List<Locale>? preferredLocales, Iterable<Locale> supportedLocales)
```

默认的语言区域解析算法。

可以通过 [WidgetsApp.localeListResolutionCallback] 或 [WidgetsApp.localeResolutionCallback] 提供自定义的解析算法。

如果未提供自定义语言区域解析算法，或者两者都无法解析成功，Flutter 将默认调用此算法。

此算法优先考虑速度，代价是在边缘情况下解析结果可能不够合适。

此算法将解析为匹配字段最多的最早的首选语言区域，按以下顺序优先匹配：完全匹配、languageCode+countryCode、languageCode+scriptCode、仅 languageCode。

如果某个语言区域仅通过 languageCode 匹配，且不是默认（第一个）语言区域，那么如果存在下一个完全匹配的首选语言区域，它可以取代该仅 languageCode 匹配的结果。

当一个首选语言区域匹配多个受支持的语言区域时，将解析为 supportedLocales 中列出的第一个匹配语言区域。

当所有首选语言区域都已尝试且没有匹配时，将返回第一个仅匹配 countryCode 的结果。

当完全没有匹配时，将返回 [supportedLocales] 中的第一个（默认）语言区域。

总结来说，主要的匹配优先级为：

1.  [Locale.languageCode]、[Locale.scriptCode] 和 [Locale.countryCode]
2.  仅 [Locale.languageCode] 和 [Locale.scriptCode]
3.  仅 [Locale.languageCode] 和 [Locale.countryCode]
4.  仅 [Locale.languageCode]（有上述提到的特殊情况）
5.  仅当所有 [preferredLocales] 都无法匹配时才匹配 [Locale.countryCode]
6.  返回 [supportedLocales] 的第一个元素作为兜底方案

该算法未考虑语言距离（即语言之间的相似程度），因此在诸如 `de`（德语）不受支持而 `zh`（中文）排在 `fr`（法语）之前的边缘情况下，不会将 `de` 解析为 `fr`，而会解析为 `zh`（尽管德语与法语更为接近）。

# GenerateAppTitle

```dart
typedef GenerateAppTitle = String Function(BuildContext context)
```

[WidgetsApp.onGenerateTitle] 的签名。

用于生成应用 [Title.title] 的值，设备使用该值向用户标识此应用。`context` 包含 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 的 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) 组件，以便此方法可用于生成本地化的标题。

此函数不得返回 null。

# PageRouteFactory

```dart
typedef PageRouteFactory = PageRoute<T> Function<T>(RouteSettings settings, WidgetBuilder builder)
```

[WidgetsApp.pageRouteBuilder] 的签名。

使用给定的 [RouteSettings](https://www.yuque.com/thyname/flutter.widgets/routesettings) 和 [WidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/widgetbuilder) 创建一个 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute)。

# InitialRouteListFactory

```dart
typedef InitialRouteListFactory = List<Route<dynamic>> Function(String initialRoute)
```

[WidgetsApp.onGenerateInitialRoutes] 的签名。

创建一系列一个或多个初始路由。

# WidgetsApp

```dart
class WidgetsApp extends StatefulWidget {}
```

一个便捷组件，封装了应用程序通常所需的若干组件。

[WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 提供的主要作用之一，是将系统返回按钮绑定到弹出 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 或退出应用程序的操作。

[MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 和 [CupertinoApp](https://www.yuque.com/thyname/flutter.cupertino/cupertinoapp) 都使用它来实现应用的基础功能。

在"另请参阅"部分可以找到 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 所封装的许多组件的引用。

另请参阅：

- [CheckedModeBanner](https://www.yuque.com/thyname/flutter.widgets/checkedmodebanner)，在调试模式下运行时显示写有 "DEBUG" 字样的 [Banner](https://www.yuque.com/thyname/flutter.widgets/banner)。
- [DefaultTextStyle](https://www.yuque.com/thyname/flutter.widgets/defaulttextstyle)，应用于没有明确样式的后代 [Text](https://www.yuque.com/thyname/flutter.widgets/text) 组件的文本样式。
- [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery)，建立一个子树，在该子树中媒体查询会解析为 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata)。
- [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations)，为其 `child` 定义 [Locale](https://www.yuque.com/thyname/dart.ui/locale)。
- [Title](https://www.yuque.com/thyname/flutter.widgets/title)，一个用于向操作系统描述此应用的组件。
- [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，一个使用栈规则管理一组子组件的组件。
- [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay)，一个管理可独立操作的 [Stack](https://www.yuque.com/thyname/flutter.widgets/stack) 条目的组件。
- [SemanticsDebugger](https://www.yuque.com/thyname/flutter.widgets/semanticsdebugger)，一个用于可视化子组件语义信息的组件。

### WidgetsApp()

```dart
WidgetsApp({dynamic key, GlobalKey<NavigatorState>? navigatorKey, RouteFactory? onGenerateRoute, InitialRouteListFactory? onGenerateInitialRoutes, RouteFactory? onUnknownRoute, NotificationListenerCallback<NavigationNotification>? onNavigationNotification, List<NavigatorObserver>? navigatorObservers = const <NavigatorObserver>[], String? initialRoute, PageRouteFactory? pageRouteBuilder, Widget? home, Map<String, WidgetBuilder>? routes = const <String, WidgetBuilder>{}, TransitionBuilder? builder, String? title, GenerateAppTitle? onGenerateTitle, TextStyle? textStyle, required Color color, Locale? locale, Iterable<LocalizationsDelegate<dynamic>>? localizationsDelegates, LocaleListResolutionCallback? localeListResolutionCallback, LocaleResolutionCallback? localeResolutionCallback, Iterable<Locale> supportedLocales = const <Locale>[Locale('en', 'US')], bool showPerformanceOverlay = false, bool showSemanticsDebugger = false, bool debugShowWidgetInspector = false, bool debugShowCheckedModeBanner = true, ExitWidgetSelectionButtonBuilder? exitWidgetSelectionButtonBuilder, MoveExitWidgetSelectionButtonBuilder? moveExitWidgetSelectionButtonBuilder, TapBehaviorButtonBuilder? tapBehaviorButtonBuilder, Map<ShortcutActivator, Intent>? shortcuts, Map<Type, Action<Intent>>? actions, String? restorationScopeId, bool useInheritedMediaQuery = false})
```

创建一个组件，用于封装应用程序通常所需的若干组件。

大多数调用者会希望使用 [home] 或 [routes] 参数，或两者都使用。[home] 参数是以下 [routes] 映射的一种便捷写法：

```dart
<String, WidgetBuilder>{ '/': (BuildContext context) => myWidget }
```

可以同时指定 [home] 和 [routes]，但前提是 [routes] 中*不*包含 `'/'` 的条目。反之，如果省略了 [home]，则 [routes] *必须*包含 `'/'` 的条目。

如果 [home] 或 [routes] 不为 null，路由实现需要知道如何正确构建 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute)。这可以通过提供 [pageRouteBuilder] 参数来实现。[MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 和 [CupertinoApp](https://www.yuque.com/thyname/flutter.cupertino/cupertinoapp) 使用 [pageRouteBuilder] 分别创建 [MaterialPageRoute](https://www.yuque.com/thyname/flutter.material/materialpageroute) 和 [CupertinoPageRoute](https://www.yuque.com/thyname/flutter.cupertino/cupertinopageroute)。

[builder] 参数旨在提供将应用的可见内容包装在其他组件中的能力。如果你打算仅在应用中显示单个路由，建议使用 [home] 而非 [builder]。

[WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 还能够通过 [onGenerateRoute] 和 [onUnknownRoute] 参数提供自定义的路由实现。这些参数分别对应 [Navigator.onGenerateRoute] 和 [Navigator.onUnknownRoute]。如果 [home]、[routes] 和 [builder] 均为 null，或者它们未能创建所请求的路由，则将调用 [onGenerateRoute]。如果失败，则将调用 [onUnknownRoute]。

[pageRouteBuilder] 会被调用以创建一个包装新构建路由的 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute)。如果 [builder] 非 null 且 [onGenerateRoute] 参数为 null，则 [builder] 只会提供 context 和子组件，而 [pageRouteBuilder] 将提供 [RouteSettings](https://www.yuque.com/thyname/flutter.widgets/routesettings)；在这种配置下，[navigatorKey]、[onUnknownRoute]、[navigatorObservers] 和 [initialRoute] 属性必须保持其默认值，因为它们将不起作用。

`supportedLocales` 参数必须是一个包含一个或多个元素的列表。默认情况下，supportedLocales 为 `[const Locale('en', 'US')]`。

{@tool dartpad} 此示例展示了使用 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 的一个基础 Flutter 应用程序。

** 请参阅 examples/api/lib/widgets/app/widgets_app.widgets_app.0.dart 中的代码 ** {@end-tool}

### WidgetsApp.router()

```dart
WidgetsApp.router({dynamic key, RouteInformationProvider? routeInformationProvider, RouteInformationParser<Object>? routeInformationParser, RouterDelegate<Object>? routerDelegate, RouterConfig<Object>? routerConfig, BackButtonDispatcher? backButtonDispatcher, TransitionBuilder? builder, String? title, GenerateAppTitle? onGenerateTitle, NotificationListenerCallback<NavigationNotification>? onNavigationNotification, TextStyle? textStyle, required Color color, Locale? locale, Iterable<LocalizationsDelegate<dynamic>>? localizationsDelegates, LocaleListResolutionCallback? localeListResolutionCallback, LocaleResolutionCallback? localeResolutionCallback, Iterable<Locale> supportedLocales = const <Locale>[Locale('en', 'US')], bool showPerformanceOverlay = false, bool showSemanticsDebugger = false, bool debugShowWidgetInspector = false, bool debugShowCheckedModeBanner = true, ExitWidgetSelectionButtonBuilder? exitWidgetSelectionButtonBuilder, MoveExitWidgetSelectionButtonBuilder? moveExitWidgetSelectionButtonBuilder, TapBehaviorButtonBuilder? tapBehaviorButtonBuilder, Map<ShortcutActivator, Intent>? shortcuts, Map<Type, Action<Intent>>? actions, String? restorationScopeId, bool useInheritedMediaQuery = false})
```

创建一个使用 [Router](https://www.yuque.com/thyname/flutter.widgets/router) 而非 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp)。

{@template flutter.widgets.WidgetsApp.router} 如果提供了 [routerConfig]，则其他与路由相关的委托对象，即 [routeInformationParser]、[routeInformationProvider]、[routerDelegate] 和 [backButtonDispatcher]，必须全部为 null。{@endtemplate}

### navigatorKey

```dart
GlobalKey<NavigatorState>? navigatorKey
```

{@template flutter.widgets.widgetsApp.navigatorKey} 构建 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 时使用的键。

如果指定了 [navigatorKey]，则可以直接操作 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，而无需先通过 [Navigator.of] 从 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 获取它：可以从 [navigatorKey] 使用 [GlobalKey.currentState] 获取器。

如果此值发生更改，将创建一个新的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，从而丢失该过程中的所有应用程序状态；在这种情况下，也必须更改 [navigatorObservers]，因为之前的观察者是附加到之前的 navigator 上的。

只有在 [onGenerateRoute] 非 null 时才会构建 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)；如果它为 null，则 [navigatorKey] 也必须为 null。{@endtemplate}

### onGenerateRoute

```dart
RouteFactory? onGenerateRoute
```

{@template flutter.widgets.widgetsApp.onGenerateRoute} 当应用导航到具名路由时使用的路由生成器回调。

如果在构建处理指定 [initialRoute] 的路由时该回调返回 null，则所有路由都将被丢弃，转而使用 [Navigator.defaultRouteName]（即 `/`）。参见 [initialRoute]。

在应用正常运行期间，[onGenerateRoute] 回调只会应用于应用程序推送的路由名称，因此永远不应返回 null。

如果 [routes] 中不包含所请求的路由，则会使用此项。

只有在提供了路由（通过 [home]、[routes]、[onGenerateRoute] 或 [onUnknownRoute] 之一）时才会构建 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)；如果未提供，则 [builder] 不能为 null。{@endtemplate}

如果未设置此属性，则必须设置 [routes] 或 [home] 属性之一，并且还必须设置 [pageRouteBuilder]，以便默认处理程序知道要构建哪些路由和 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute)。

### onGenerateInitialRoutes

```dart
InitialRouteListFactory? onGenerateInitialRoutes
```

{@template flutter.widgets.widgetsApp.onGenerateInitialRoutes} 当提供了 [initialRoute] 时，用于生成初始路由的路由生成器回调。

如果未设置此属性，底层的 [Navigator.onGenerateInitialRoutes] 将默认使用 [Navigator.defaultGenerateInitialRoutes]。{@endtemplate}

### pageRouteBuilder

```dart
PageRouteFactory? pageRouteBuilder
```

当应用导航到具名路由时使用的 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute) 生成器回调。

[PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute) 代表 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 中的页面，以便能够在页面之间正确地进行动画切换，并表示路由的"返回值"（例如，用户在模态对话框中选择了哪个按钮）。

例如，此回调可用于指定应使用 [MaterialPageRoute](https://www.yuque.com/thyname/flutter.material/materialpageroute) 还是 [CupertinoPageRoute](https://www.yuque.com/thyname/flutter.cupertino/cupertinopageroute) 来构建页面过渡效果。

[PageRouteFactory](https://www.yuque.com/thyname/flutter.widgets/pageroutefactory) 类型是泛型的，这意味着所提供的函数本身也必须是泛型的。例如（特别注意闭包开头的 `<T>`）：

```dart
pageRouteBuilder: <T>(RouteSettings settings, WidgetBuilder builder) => PageRouteBuilder<T>(
  settings: settings,
  pageBuilder: (BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation) => builder(context),
),
```

### routeInformationParser

```dart
RouteInformationParser<Object>? routeInformationParser
```

{@template flutter.widgets.widgetsApp.routeInformationParser} 一个委托对象，用于将来自 [routeInformationProvider] 的路由信息解析为一种通用数据类型，供 [routerDelegate] 在后续阶段处理。

该对象将被底层的 [Router](https://www.yuque.com/thyname/flutter.widgets/router) 使用。

泛型类型 `T` 必须与 [routerDelegate] 的泛型类型匹配。

另请参阅：

- [Router.routeInformationParser]，当此组件构建 [Router](https://www.yuque.com/thyname/flutter.widgets/router) 时会接收此对象。{@endtemplate}

### routerDelegate

```dart
RouterDelegate<Object>? routerDelegate
```

{@template flutter.widgets.widgetsApp.routerDelegate} 一个委托对象，使用从 [routeInformationParser] 解析出的结果来配置一个组件（通常是 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)）。

该对象将被底层的 [Router](https://www.yuque.com/thyname/flutter.widgets/router) 使用。

泛型类型 `T` 必须与 [routeInformationParser] 的泛型类型匹配。

另请参阅：

- [Router.routerDelegate]，当此组件构建 [Router](https://www.yuque.com/thyname/flutter.widgets/router) 时会接收此对象。{@endtemplate}

### backButtonDispatcher

```dart
BackButtonDispatcher? backButtonDispatcher
```

{@template flutter.widgets.widgetsApp.backButtonDispatcher} 一个委托对象，决定是否处理 Android 返回按钮的意图。

该对象将被底层的 [Router](https://www.yuque.com/thyname/flutter.widgets/router) 使用。

如果未提供此项，widgets app 将默认创建一个 [RootBackButtonDispatcher](https://www.yuque.com/thyname/flutter.widgets/rootbackbuttondispatcher)。

另请参阅：

- [Router.backButtonDispatcher]，当此组件构建 [Router](https://www.yuque.com/thyname/flutter.widgets/router) 时会接收此对象。{@endtemplate}

### routeInformationProvider

```dart
RouteInformationProvider? routeInformationProvider
```

{@template flutter.widgets.widgetsApp.routeInformationProvider} 一个通过 [RouteInformationProvider.value] 提供路由信息的对象，并在其值发生变化时通知其监听器。

该对象将被底层的 [Router](https://www.yuque.com/thyname/flutter.widgets/router) 使用。

如果未提供此项，widgets app 将默认创建一个初始路由名称等于 [dart:ui.PlatformDispatcher.defaultRouteName] 的 [PlatformRouteInformationProvider](https://www.yuque.com/thyname/flutter.widgets/platformrouteinformationprovider)。

另请参阅：

- [Router.routeInformationProvider]，当此组件构建 [Router](https://www.yuque.com/thyname/flutter.widgets/router) 时会接收此对象。{@endtemplate}

### routerConfig

```dart
RouterConfig<Object>? routerConfig
```

{@template flutter.widgets.widgetsApp.routerConfig} 用于配置底层 [Router](https://www.yuque.com/thyname/flutter.widgets/router) 的对象。

如果提供了 [routerConfig]，则其他与路由相关的委托对象，即 [routeInformationParser]、[routeInformationProvider]、[routerDelegate] 和 [backButtonDispatcher]，必须全部为 null。

另请参阅：

- [Router.withConfig]，当此组件构建 [Router](https://www.yuque.com/thyname/flutter.widgets/router) 时会接收此对象。{@endtemplate}

### home

```dart
Widget? home
```

{@template flutter.widgets.widgetsApp.home} 应用默认路由（[Navigator.defaultRouteName]，即 `/`）所使用的组件。

这是应用正常启动时首先显示的路由，除非指定了 [initialRoute]。如果无法显示 [initialRoute]，这也是将显示的路由。

为了能够在设置 [home] 参数的代码中直接调用 [Theme.of]、[MediaQuery.of] 等方法，可以使用 [Builder](https://www.yuque.com/thyname/flutter.widgets/builder) 组件来获取 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)。

如果指定了 [home]，则 [routes] 不得包含 `/` 的条目，因为 [home] 会取代它的位置。

只有在提供了路由（通过 [home]、[routes]、[onGenerateRoute] 或 [onUnknownRoute] 之一）时才会构建 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)；如果未提供，则 [builder] 不能为 null。{@endtemplate}

如果设置了此属性，则还必须设置 [pageRouteBuilder] 属性，以便默认路由处理程序知道要构建哪种类型的 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute)。

### routes

```dart
Map<String, WidgetBuilder>? routes
```

应用程序的顶层路由表。

当使用 [Navigator.pushNamed] 推送具名路由时，会在此映射中查找该路由名称。如果该名称存在，则使用关联的 [WidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/widgetbuilder) 来构建由 [pageRouteBuilder] 指定的 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute)，以执行适当的过渡效果，包括跳转到新路由的 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero) 动画。

{@template flutter.widgets.widgetsApp.routes} 如果应用只有一个页面，则可以改用 [home] 来指定它。

如果指定了 [home]，则意味着此表中隐含了 [Navigator.defaultRouteName] 路由（`/`）的一个条目，此时在 [routes] 表中再次提供该路由会导致错误。

如果请求的路由未在此表（或 [home]）中指定，则会调用 [onGenerateRoute] 回调来构建该页面。

只有在提供了路由（通过 [home]、[routes]、[onGenerateRoute] 或 [onUnknownRoute] 之一）时才会构建 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)；如果未提供，则 [builder] 不能为 null。{@endtemplate}

如果路由表不为空，则必须设置 [pageRouteBuilder] 属性，以便默认路由处理程序知道要构建哪种类型的 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute)。

### onUnknownRoute

```dart
RouteFactory? onUnknownRoute
```

{@template flutter.widgets.widgetsApp.onUnknownRoute} 当 [onGenerateRoute] 未能生成路由时调用（[initialRoute] 除外）。

此回调通常用于错误处理。例如，此回调可能始终生成一个描述未找到路由的"未找到"页面。

未知路由既可能源自应用中的错误，也可能源自推送路由的外部请求，例如来自 Android intent 的请求。

只有在提供了路由（通过 [home]、[routes]、[onGenerateRoute] 或 [onUnknownRoute] 之一）时才会构建 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)；如果未提供，则 [builder] 不能为 null。{@endtemplate}

### onNavigationNotification

```dart
NotificationListenerCallback<NavigationNotification>? onNavigationNotification
```

{@template flutter.widgets.widgetsApp.onNavigationNotification} 接收到 [NavigationNotification](https://www.yuque.com/thyname/flutter.widgets/navigationnotification) 时使用的回调。

默认情况下，这会使用导航状态更新引擎，并停止该通知的冒泡。

另请参阅：

- [NotificationListener.onNotification]，使用此回调。{@endtemplate}

### initialRoute

```dart
String? initialRoute
```

{@template flutter.widgets.widgetsApp.initialRoute} 如果构建了 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，则表示要显示的第一个路由的名称。

默认为 [dart:ui.PlatformDispatcher.defaultRouteName]，该值可能会被启动应用程序的代码覆盖。

如果路由名称以斜杠开头，则将其视为"深层链接"，在推送此路由之前，会先推送通向此路由的各级路由。例如，如果路由为 `/a/b/c`，则应用启动时会按顺序加载四个路由：`/`、`/a`、`/a/b` 和 `/a/b/c`。即使路由只是 `/a`，应用也会先加载 `/` 再加载 `/a`。可以使用 [onGenerateInitialRoutes] 属性来覆盖此行为。

中间路由不要求必须存在。在上面的例子中，如果 `/a` 和 `/a/b` 没有匹配的路由，则可以跳过它们。但 `/a/b/c` 必须有对应的路由，否则将忽略 [initialRoute] 而改用 [Navigator.defaultRouteName]（即 `/`）。如果应用是通过指定了不存在的路由的 intent 启动的，就可能发生这种情况。

只有在提供了路由（通过 [home]、[routes]、[onGenerateRoute] 或 [onUnknownRoute] 之一）时才会构建 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)；如果未提供，则 [initialRoute] 必须为 null 且 [builder] 不能为 null。

更改 [initialRoute] 不会产生任何效果，因为它只控制*初始*路由。要在应用程序运行期间更改路由，请使用 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 或 [Router](https://www.yuque.com/thyname/flutter.widgets/router) API。

另请参阅：

- [Navigator.initialRoute]，用于实现此属性。
- [Navigator.push]，用于推送额外的路由。
- [Navigator.pop]，用于从栈中移除一个路由。

{@endtemplate}

### navigatorObservers

```dart
List<NavigatorObserver>? navigatorObservers
```

{@template flutter.widgets.widgetsApp.navigatorObservers} 为此应用创建的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的观察者列表。

如果更改了 [navigatorKey]，则必须用一份新创建的观察者列表替换此列表。

只有在提供了路由（通过 [home]、[routes]、[onGenerateRoute] 或 [onUnknownRoute] 之一）时才会构建 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)；如果未提供，则 [navigatorObservers] 必须为空列表且 [builder] 不能为 null。{@endtemplate}

### builder

```dart
TransitionBuilder? builder
```

{@template flutter.widgets.widgetsApp.builder} 一个构建器，用于在 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 或（当使用 [WidgetsApp.router] 构造函数时）[Router](https://www.yuque.com/thyname/flutter.widgets/router) 之上、但在 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 创建的其他组件之下插入组件，或用于完全替换 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)/[Router](https://www.yuque.com/thyname/flutter.widgets/router)。

通过传入此方法的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)，可以使用 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)、[Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations)、[DefaultTextStyle](https://www.yuque.com/thyname/flutter.widgets/defaulttextstyle)、[MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 等，它们都是可用的。也可以以某种方式覆盖它们，从而影响 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 或 [Router](https://www.yuque.com/thyname/flutter.widgets/router) 中的所有路由。

这种用法很少见，但可用于希望覆盖这些默认值的应用程序，例如：即使应用采用英文也强制其进入从右到左模式，或覆盖 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的度量值（例如，为 OEM 代码中的某个插件显示的广告留出空间）。

如果专门要基于 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) 覆盖 [title]，请考虑改用 [onGenerateTitle]。

[builder] 回调接收两个参数：[BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)（作为 `context`）和一个 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 或 [Router](https://www.yuque.com/thyname/flutter.widgets/router) 组件（作为 `child`）。

如果没有通过 [home]、[routes]、[onGenerateRoute] 或 [onUnknownRoute] 向常规 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 构造函数提供任何路由，则 `child` 将为 null，此时由 [builder] 负责提供应用程序的路由机制。

如果通过上述一个或多个属性向常规 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 构造函数提供了路由，或者使用了 [WidgetsApp.router] 构造函数，则 `child` 不为 null，此时返回值应将 `child` 包含在组件子树中；如果不包含，则应用程序将没有 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 或 [Router](https://www.yuque.com/thyname/flutter.widgets/router)，且与路由相关的属性（即 [navigatorKey]、[home]、[routes]、[onGenerateRoute]、[onUnknownRoute]、[initialRoute]、[navigatorObservers]、[routeInformationProvider]、[backButtonDispatcher]、[routerDelegate] 和 [routeInformationParser]）都将被忽略。

如果 [builder] 为 null，则等同于指定了一个直接返回 `child` 的构建器。如果为 null，则必须使用上面列出的其他属性之一来提供路由。

除非通过以下方式之一提供了 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)：[builder] 为 null 时隐式提供、[builder] 在其返回值中包含了 `child` 参数、[builder] 显式提供了自己的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，或 [routerDelegate] 构建了一个，否则诸如 [Hero](https://www.yuque.com/thyname/flutter.widgets/hero)、[Navigator.push] 和 [Navigator.pop] 之类的组件和 API 将无法正常工作。{@endtemplate}

### title

```dart
String? title
```

{@template flutter.widgets.widgetsApp.title} 设备用于向用户标识此应用的单行描述。

在 Android 上，标题会显示在任务管理器的应用快照上方，当用户按下"最近应用"按钮时会显示这些快照。在 iOS 上无法使用此值，而是会优先参考应用 `Info.plist` 中的 `CFBundleDisplayName`（如果存在），否则使用 `CFBundleName`。在 Web 上，此值用作页面标题，显示在浏览器的打开标签页列表中。

要提供本地化的标题，请改用 [onGenerateTitle]。{@endtemplate}

### onGenerateTitle

```dart
GenerateAppTitle? onGenerateTitle
```

{@template flutter.widgets.widgetsApp.onGenerateTitle} 如果非 null，则调用此回调函数来生成应用的标题字符串，否则使用 [title]。

[onGenerateTitle] 的 `context` 参数包含 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 的 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) 组件，以便此回调可用于生成本地化的标题。

此函数不得返回 null。

每次 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 重建时都会调用 [onGenerateTitle] 回调。{@endtemplate}

### textStyle

```dart
TextStyle? textStyle
```

应用程序中 [Text](https://www.yuque.com/thyname/flutter.widgets/text) 的默认文本样式。

### color

```dart
Color color
```

{@template flutter.widgets.widgetsApp.color} 应用程序在操作系统界面中使用的主色。

例如，在 Android 上，这是应用切换器中用于此应用程序的颜色。{@endtemplate}

### locale

```dart
Locale? locale
```

{@template flutter.widgets.widgetsApp.locale} 此应用的 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) 组件的初始语言区域基于此值。

如果 'locale' 为 null，则使用系统的语言区域值。

如果此语言区域与 [supportedLocales] 中的某一项匹配，则 [Localizations.locale] 的值将等于此语言区域。否则，它将是 [supportedLocales] 中的第一个元素。{@endtemplate}

另请参阅：

- [localeResolutionCallback]，可用于覆盖默认的 [supportedLocales] 匹配算法。
- [localizationsDelegates]，共同定义了此应用使用的所有本地化资源。

### localizationsDelegates

```dart
Iterable<LocalizationsDelegate<dynamic>>? localizationsDelegates
```

{@template flutter.widgets.widgetsApp.localizationsDelegates} 此应用的 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) 组件的委托对象。

这些委托对象共同定义了此应用程序的 [Localizations](https://www.yuque.com/thyname/flutter.widgets/localizations) 组件所需的所有本地化资源。{@endtemplate}

### localeListResolutionCallback

```dart
LocaleListResolutionCallback? localeListResolutionCallback
```

{@template flutter.widgets.widgetsApp.localeListResolutionCallback} 此回调负责在应用启动时以及用户更改设备语言区域时选择应用的语言区域。

当提供了 [localeListResolutionCallback] 时，Flutter 会首先尝试使用提供的 [localeListResolutionCallback] 来解析语言区域。如果该回调或结果为 null，则会回退尝试 [localeResolutionCallback]。如果 [localeResolutionCallback] 和 [localeListResolutionCallback] 都保持为 null 或解析失败（返回 null），则将使用基本的兜底算法。

每种可用兜底方案的优先级为：

1.  首先尝试 [localeListResolutionCallback]。
2.  然后尝试 [localeResolutionCallback]。
3.  最后尝试 Flutter 的基本解析算法，如 [supportedLocales] 中所述。

正规的本地化项目应当提供比 [supportedLocales] 中的基本方法更高级的算法，因为该基本方法未实现完整的算法（例如 [Unicode TR35](https://unicode.org/reports/tr35/#LanguageMatching) 中定义的算法），且针对速度进行了优化，牺牲了一些不常见的边缘情况。{@endtemplate}

此回调考虑整个首选语言区域列表。

此算法应能够处理为 null 或空的首选语言区域列表，这表示 Flutter 尚未从平台接收到语言区域信息。

另请参阅：

- [MaterialApp.localeListResolutionCallback]，设置其创建的 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 的回调。
- [basicLocaleListResolution](https://www.yuque.com/thyname/flutter.widgets/basiclocalelistresolution)，默认的语言区域解析算法。

### localeResolutionCallback

```dart
LocaleResolutionCallback? localeResolutionCallback
```

{@macro flutter.widgets.widgetsApp.localeListResolutionCallback}

此回调仅考虑默认语言区域，即首选语言区域列表中的第一个语言区域。建议优先设置 [localeListResolutionCallback] 而非 [localeResolutionCallback]，因为它提供了完整的首选语言区域列表。

此算法应能够处理为 null 的语言区域，这表示 Flutter 尚未从平台接收到语言区域信息。

另请参阅：

- [MaterialApp.localeResolutionCallback]，设置其创建的 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 的回调。
- [basicLocaleListResolution](https://www.yuque.com/thyname/flutter.widgets/basiclocalelistresolution)，默认的语言区域解析算法。

### supportedLocales

```dart
Iterable<Locale> supportedLocales
```

{@template flutter.widgets.widgetsApp.supportedLocales} 此应用已本地化支持的语言区域列表。

默认情况下仅支持美式英语语言区域。应用应配置此列表以匹配其所支持的语言区域。

此列表不得为 null。其默认值仅为 `[const Locale('en', 'US')]`。

列表的顺序很重要。默认的语言区域解析算法 [basicLocaleListResolution](https://www.yuque.com/thyname/flutter.widgets/basiclocalelistresolution) 会尝试按以下优先级进行匹配：

1.  [Locale.languageCode]、[Locale.scriptCode] 和 [Locale.countryCode]
2.  仅 [Locale.languageCode] 和 [Locale.scriptCode]
3.  仅 [Locale.languageCode] 和 [Locale.countryCode]
4.  仅 [Locale.languageCode]
5.  仅当所有首选语言区域都无法匹配时才匹配 [Locale.countryCode]
6.  返回 [supportedLocales] 的第一个元素作为兜底方案

当多个受支持的语言区域符合这些条件之一时，只返回第一个匹配的语言区域。

可以通过为 [localeListResolutionCallback] 提供一个值来覆盖默认的语言区域解析算法。所提供的 [basicLocaleListResolution](https://www.yuque.com/thyname/flutter.widgets/basiclocalelistresolution) 针对速度进行了优化，未实现考虑语言之间距离的完整算法（例如 [Unicode TR35](https://unicode.org/reports/tr35/#LanguageMatching) 中定义的算法）。

对于支持多种文字的语言，建议显式指定 [Locale.scriptCode]。也可以在定义语言区域时不指定 [Locale.countryCode]，以便为特定文字指定一个通用的兜底方案。

一个完全受支持且具有多种文字的语言应当定义一个仅含语言的通用语言区域（例如 'zh'）、仅含语言+文字的语言区域（例如 'zh_Hans' 和 'zh_Hant'），以及任何语言+文字+国家/地区的语言区域（例如 'zh_Hans_CN'）。完整定义所有这些语言区域为受支持并非严格要求，但可以在最多的情况下实现正确的语言区域解析。可以使用 [Locale.fromSubtags] 构造函数指定这些语言区域：

```dart
// Full Chinese support for CN, TW, and HK
supportedLocales: <Locale>[
  const Locale.fromSubtags(languageCode: 'zh'), // generic Chinese 'zh'
  const Locale.fromSubtags(languageCode: 'zh', scriptCode: 'Hans'), // generic simplified Chinese 'zh_Hans'
  const Locale.fromSubtags(languageCode: 'zh', scriptCode: 'Hant'), // generic traditional Chinese 'zh_Hant'
  const Locale.fromSubtags(languageCode: 'zh', scriptCode: 'Hans', countryCode: 'CN'), // 'zh_Hans_CN'
  const Locale.fromSubtags(languageCode: 'zh', scriptCode: 'Hant', countryCode: 'TW'), // 'zh_Hant_TW'
  const Locale.fromSubtags(languageCode: 'zh', scriptCode: 'Hant', countryCode: 'HK'), // 'zh_Hant_HK'
],
```

省略其中一些兜底方案可能导致边缘情况解析不正确，例如，一个使用简体中文的台湾用户（'zh_Hans_TW'）如果省略了 'zh_Hans' 和 'zh_Hans_CN'，可能会解析为繁体中文。{@endtemplate}

另请参阅：

- [MaterialApp.supportedLocales]，设置其创建的 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 的 `supportedLocales`。
- [localeResolutionCallback]，一个在设备语言区域更改时解析应用语言区域的应用回调。
- [localizationsDelegates]，共同定义了此应用使用的所有本地化资源。
- [basicLocaleListResolution](https://www.yuque.com/thyname/flutter.widgets/basiclocalelistresolution)，默认的语言区域解析算法。

### showPerformanceOverlay

```dart
bool showPerformanceOverlay
```

开启性能叠加层。

另请参阅：

- <https://flutter.dev/to/performance-overlay>

### showSemanticsDebugger

```dart
bool showSemanticsDebugger
```

开启一个叠加层，显示框架报告的无障碍信息。

### debugShowWidgetInspector

```dart
bool debugShowWidgetInspector
```

开启一个可用于检查组件树的叠加层。

该检查器仅在调试模式下可用，因为它依赖于 [RenderObject.debugDescribeChildren]，该方法不应在调试模式之外调用。

### exitWidgetSelectionButtonBuilder

```dart
ExitWidgetSelectionButtonBuilder? exitWidgetSelectionButtonBuilder
```

构建 [WidgetInspector](https://www.yuque.com/thyname/flutter.widgets/widgetinspector) 用于退出选择模式的组件。

这使 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 和 [CupertinoApp](https://www.yuque.com/thyname/flutter.cupertino/cupertinoapp) 能够为其设计体系使用样式恰当的按钮，而无需让 [WidgetInspector](https://www.yuque.com/thyname/flutter.widgets/widgetinspector) 依赖于 Material 或 Cupertino 包。

### moveExitWidgetSelectionButtonBuilder

```dart
MoveExitWidgetSelectionButtonBuilder? moveExitWidgetSelectionButtonBuilder
```

构建 [WidgetInspector](https://www.yuque.com/thyname/flutter.widgets/widgetinspector) 用于移动退出选择模式按钮的组件。

这使 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 和 [CupertinoApp](https://www.yuque.com/thyname/flutter.cupertino/cupertinoapp) 能够为其设计体系使用样式恰当的按钮，而无需让 [WidgetInspector](https://www.yuque.com/thyname/flutter.widgets/widgetinspector) 依赖于 Material 或 Cupertino 包。

### tapBehaviorButtonBuilder

```dart
TapBehaviorButtonBuilder? tapBehaviorButtonBuilder
```

构建 [WidgetInspector](https://www.yuque.com/thyname/flutter.widgets/widgetinspector) 用于更改点击应用中组件时默认行为的组件。

这使 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 和 [CupertinoApp](https://www.yuque.com/thyname/flutter.cupertino/cupertinoapp) 能够为其设计体系使用样式恰当的按钮，而无需让 [WidgetInspector](https://www.yuque.com/thyname/flutter.widgets/widgetinspector) 依赖于 Material 或 Cupertino 包。

### debugShowCheckedModeBanner

```dart
bool debugShowCheckedModeBanner
```

{@template flutter.widgets.widgetsApp.debugShowCheckedModeBanner} 在调试模式下开启一个小的 "DEBUG" 横幅，以表明该应用处于调试模式。此选项默认（在调试模式下）开启，如需关闭，可将构造函数参数设为 false。在发布模式下此选项无效。

如果你的应用没有使用 WidgetsApp，要在应用中获得此横幅，可包含一个 [CheckedModeBanner](https://www.yuque.com/thyname/flutter.widgets/checkedmodebanner) 组件。

此横幅旨在阻止有人抱怨应用处于调试模式时运行缓慢的问题。在调试模式下，Flutter 会启用大量开销较大的诊断功能以辅助开发，因此调试模式下的性能并不能代表发布模式下的实际表现。{@endtemplate}

### shortcuts

```dart
Map<ShortcutActivator, Intent>? shortcuts
```

{@template flutter.widgets.widgetsApp.shortcuts} 应用程序键盘快捷键到意图（intent）的默认映射。

默认情况下，此值设为 [WidgetsApp.defaultShortcuts]。

传入此参数不会替换 [DefaultTextEditingShortcuts](https://www.yuque.com/thyname/flutter.widgets/defaulttexteditingshortcuts)。可以通过在组件树的更下层使用 [Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts) 组件来覆盖这些内容。{@endtemplate}

{@tool snippet} 此示例展示了如何在无需添加自己的 [Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts) 组件的情况下，为默认快捷键添加一个针对 [LogicalKeyboardKey.select] 的快捷键。

或者，你也可以在 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 与其子组件之间插入一个仅包含你想添加的映射的 [Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts) 组件，以获得相同的效果。

```dart
Widget build(BuildContext context) {
  return WidgetsApp(
    shortcuts: <ShortcutActivator, Intent>{
      ... WidgetsApp.defaultShortcuts,
      const SingleActivator(LogicalKeyboardKey.select): const ActivateIntent(),
    },
    color: const Color(0xFFFF0000),
    builder: (BuildContext context, Widget? child) {
      return const Placeholder();
    },
  );
}
```

{@end-tool}

{@template flutter.widgets.widgetsApp.shortcuts.seeAlso} 另请参阅：

- [SingleActivator](https://www.yuque.com/thyname/flutter.widgets/singleactivator)，定义单个按键与修饰键组合的快捷键，例如 "Delete" 或 "Control+C"。
- [Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts) 组件，定义键盘映射。
- [Actions](https://www.yuque.com/thyname/flutter.widgets/actions) 组件，定义从意图（intent）到动作（action）的映射。
- [Intent](https://www.yuque.com/thyname/flutter.widgets/intent) 和 [Action](https://www.yuque.com/thyname/flutter.widgets/action) 类，允许定义新的动作。{@endtemplate}

### actions

```dart
Map<Type, Action<Intent>>? actions
```

{@template flutter.widgets.widgetsApp.actions} 应用程序意图（intent）键到动作（action）的默认映射。

默认情况下，此值为使用 [defaultTargetPlatform](https://www.yuque.com/thyname/flutter.foundation/defaulttargetplatform) 调用 [WidgetsApp.defaultActions] 的结果。为应用指定 [actions] 会覆盖默认值，因此如果你希望修改默认的 [actions]，可以调用 [WidgetsApp.defaultActions] 并修改所得到的映射，然后将其作为此应用的 [actions] 传入。你也可以通过添加自己的 [Actions](https://www.yuque.com/thyname/flutter.widgets/actions) 组件来为组件子树添加绑定或覆盖特定的绑定。{@endtemplate}

{@tool snippet} 此示例展示了如何在无需添加自己的 [Actions](https://www.yuque.com/thyname/flutter.widgets/actions) 组件的情况下，为默认动作添加一个处理 [ActivateAction](https://www.yuque.com/thyname/flutter.widgets/activateaction) 的单个动作。

或者，你也可以在 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 与其子组件之间插入一个仅包含你想添加的映射的 [Actions](https://www.yuque.com/thyname/flutter.widgets/actions) 组件，以获得相同的效果。

```dart
Widget build(BuildContext context) {
  return WidgetsApp(
    actions: <Type, Action<Intent>>{
      ... WidgetsApp.defaultActions,
      ActivateAction: CallbackAction<Intent>(
        onInvoke: (Intent intent) {
          // Do something here...
          return null;
        },
      ),
    },
    color: const Color(0xFFFF0000),
    builder: (BuildContext context, Widget? child) {
      return const Placeholder();
    },
  );
}
```

{@end-tool}

{@template flutter.widgets.widgetsApp.actions.seeAlso} 另请参阅：

- [shortcuts] 参数，定义应用程序的默认快捷键集合。
- [Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts) 组件，定义键盘映射。
- [Actions](https://www.yuque.com/thyname/flutter.widgets/actions) 组件，定义从意图（intent）到动作（action）的映射。
- [Intent](https://www.yuque.com/thyname/flutter.widgets/intent) 和 [Action](https://www.yuque.com/thyname/flutter.widgets/action) 类，允许定义新的动作。{@endtemplate}

### restorationScopeId

```dart
String? restorationScopeId
```

{@template flutter.widgets.widgetsApp.restorationScopeId} 用于此应用状态恢复的标识符。

提供恢复 ID 会在组件层级结构中插入一个 [RootRestorationScope](https://www.yuque.com/thyname/flutter.widgets/rootrestorationscope)，从而为后代组件启用状态恢复功能。

提供恢复 ID 还会使 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 构建的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 或 [Router](https://www.yuque.com/thyname/flutter.widgets/router) 能够恢复其状态（即恢复活动 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 的历史栈）。有关路由状态恢复的更多详情，请参阅 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的文档。

另请参阅：

- [RestorationManager](https://www.yuque.com/thyname/flutter.services/restorationmanager)，说明状态恢复在 Flutter 中的工作原理。{@endtemplate}

### useInheritedMediaQuery

```dart
bool useInheritedMediaQuery
```

{@template flutter.widgets.widgetsApp.useInheritedMediaQuery} 已弃用。此设置现已被忽略。

该组件从不引入自己的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery)；这由 [View](https://www.yuque.com/thyname/flutter.widgets/view) 组件负责处理。{@endtemplate}

### showPerformanceOverlayOverride

```dart
bool showPerformanceOverlayOverride
```

如果为 true，则强制在所有实例中显示性能叠加层。

由 `showPerformanceOverlay` VM 服务扩展使用。

### debugShowWidgetInspectorOverride

```dart
bool get debugShowWidgetInspectorOverride
```

如果为 true，则强制显示组件检查器。

已弃用。请改用 WidgetsBinding.instance.debugShowWidgetInspectorOverrideNotifier.value。

覆盖 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 中设置的 `debugShowWidgetInspector` 值。

由 `debugShowWidgetInspector` 调试扩展使用。

该检查器允许在你的设备或模拟器上选择某个位置，并查看与之相关联的组件和渲染对象。所选组件的轮廓和一些摘要信息会显示在设备上，更详细的信息则显示在 IDE 或 DevTools 中。

### debugShowWidgetInspectorOverride

```dart
set debugShowWidgetInspectorOverride(bool value)
```

### debugAllowBannerOverride

```dart
bool debugAllowBannerOverride
```

如果为 false，则阻止显示调试横幅。

由 `debugAllowBanner` VM 服务扩展使用。

这就是 `flutter run` 在你用 "s" 截图时关闭横幅的方式。

### defaultShortcuts

```dart
Map<ShortcutActivator, Intent> get defaultShortcuts
```

根据 [defaultTargetPlatform](https://www.yuque.com/thyname/flutter.foundation/defaulttargetplatform) 生成默认的快捷键绑定。

由 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 用于为 [WidgetsApp.shortcuts] 赋予默认值。

### defaultActions

```dart
Map<Type, Action<Intent>> defaultActions
```

[WidgetsApp.actions] 的默认值。

### createState()

```dart
State<WidgetsApp> createState()
```
