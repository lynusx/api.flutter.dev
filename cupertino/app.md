@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/services.dart';

@docImport 'page_scaffold.dart'; @docImport 'tab_view.dart';

# CupertinoApp

```dart
class CupertinoApp extends StatefulWidget {}
```

An application that uses Cupertino design.

A convenience widget that wraps a number of widgets that are commonly required for an iOS-design targeting application. It builds upon a [WidgetsApp] by iOS specific defaulting such as fonts and scrolling physics.

The [CupertinoApp] configures the top-level [Navigator] to search for routes in the following order:

1.  For the `/` route, the [home] property, if non-null, is used.

2.  Otherwise, the [routes] table is used, if it has an entry for the route.

3.  Otherwise, [onGenerateRoute] is called, if provided. It should return a non-null value for any _valid_ route not handled by [home] and [routes].

4.  Finally if all else fails [onUnknownRoute] is called.

If [home], [routes], [onGenerateRoute], and [onUnknownRoute] are all null, and [builder] is not null, then no [Navigator] is created.

This widget also configures the observer of the top-level [Navigator] (if any) to perform [Hero] animations.

The [CupertinoApp] widget isn't a required ancestor for other Cupertino widgets, but many Cupertino widgets could depend on the [CupertinoTheme] widget, which the [CupertinoApp] composes. If you use Material widgets, a [MaterialApp] also creates the needed dependencies for Cupertino widgets.

{@template flutter.cupertino.CupertinoApp.defaultSelectionStyle} The [CupertinoApp] automatically creates a [DefaultSelectionStyle] with selectionColor sets to [CupertinoThemeData.primaryColor] with 0.2 opacity and cursorColor sets to [CupertinoThemeData.primaryColor]. {@endtemplate}

Use this widget with caution on Android since it may produce behaviors Android users are not expecting such as:

- Pages will be dismissible via a back swipe.
- Scrolling past extremities will trigger iOS-style spring overscrolls.
- The San Francisco font family is unavailable on Android and can result in undefined font behavior.

{@tool snippet} This example shows how to create a [CupertinoApp] that disables the "debug" banner with a [home] route that will be displayed when the app is launched.

![The CupertinoApp displays a CupertinoPageScaffold](https://flutter.github.io/assets-for-api-docs/assets/cupertino/basic_cupertino_app.png)

```dart
const CupertinoApp(
  home: CupertinoPageScaffold(
    navigationBar: CupertinoNavigationBar(
      middle: Text('Home'),
    ),
    child: Center(child: Icon(CupertinoIcons.share)),
  ),
  debugShowCheckedModeBanner: false,
)
```

{@end-tool}

{@tool snippet} This example shows how to create a [CupertinoApp] that uses the [routes] `Map` to define the "home" route and an "about" route.

```dart
CupertinoApp(
  routes: <String, WidgetBuilder>{
    '/': (BuildContext context) {
      return const CupertinoPageScaffold(
        navigationBar: CupertinoNavigationBar(
          middle: Text('Home Route'),
        ),
        child: Center(child: Icon(CupertinoIcons.share)),
      );
    },
    '/about': (BuildContext context) {
      return const CupertinoPageScaffold(
        navigationBar: CupertinoNavigationBar(
          middle: Text('About Route'),
        ),
        child: Center(child: Icon(CupertinoIcons.share)),
      );
    }
  },
)
```

{@end-tool}

{@tool snippet} This example shows how to create a [CupertinoApp] that defines a [theme] that will be used for Cupertino widgets in the app.

![The CupertinoApp displays a CupertinoPageScaffold with orange-colored icons](https://flutter.github.io/assets-for-api-docs/assets/cupertino/theme_cupertino_app.png)

```dart
const CupertinoApp(
  theme: CupertinoThemeData(
    brightness: Brightness.dark,
    primaryColor: CupertinoColors.systemOrange,
  ),
  home: CupertinoPageScaffold(
    navigationBar: CupertinoNavigationBar(
      middle: Text('CupertinoApp Theme'),
    ),
    child: Center(child: Icon(CupertinoIcons.share)),
  ),
)
```

{@end-tool}

See also:

- [CupertinoPageScaffold], which provides a standard page layout default with nav bars.
- [Navigator], which is used to manage the app's stack of pages.
- [CupertinoPageRoute], which defines an app page that transitions in an iOS-specific way.
- [WidgetsApp], which defines the basic app elements but does not depend on the Cupertino library.

### CupertinoApp()

```dart
CupertinoApp({dynamic key, GlobalKey<NavigatorState>? navigatorKey, Widget? home, CupertinoThemeData? theme, Map<String, WidgetBuilder>? routes = const <String, WidgetBuilder>{}, String? initialRoute, RouteFactory? onGenerateRoute, InitialRouteListFactory? onGenerateInitialRoutes, RouteFactory? onUnknownRoute, NotificationListenerCallback<NavigationNotification>? onNavigationNotification, List<NavigatorObserver>? navigatorObservers = const <NavigatorObserver>[], TransitionBuilder? builder, String? title, GenerateAppTitle? onGenerateTitle, Color? color, Locale? locale, Iterable<LocalizationsDelegate<dynamic>>? localizationsDelegates, LocaleListResolutionCallback? localeListResolutionCallback, LocaleResolutionCallback? localeResolutionCallback, Iterable<Locale> supportedLocales = const <Locale>[Locale('en', 'US')], bool showPerformanceOverlay = false, bool checkerboardRasterCacheImages = false, bool checkerboardOffscreenLayers = false, bool showSemanticsDebugger = false, bool debugShowCheckedModeBanner = true, Map<ShortcutActivator, Intent>? shortcuts, Map<Type, Action<Intent>>? actions, String? restorationScopeId, ScrollBehavior? scrollBehavior, bool useInheritedMediaQuery = false})
```

Creates a CupertinoApp.

At least one of [home], [routes], [onGenerateRoute], or [builder] must be non-null. If only [routes] is given, it must include an entry for the [Navigator.defaultRouteName] (`/`), since that is the route used when the application is launched with an intent that specifies an otherwise unsupported route.

This class creates an instance of [WidgetsApp].

### CupertinoApp.router()

```dart
CupertinoApp.router({dynamic key, RouteInformationProvider? routeInformationProvider, RouteInformationParser<Object>? routeInformationParser, RouterDelegate<Object>? routerDelegate, BackButtonDispatcher? backButtonDispatcher, RouterConfig<Object>? routerConfig, CupertinoThemeData? theme, TransitionBuilder? builder, String? title, GenerateAppTitle? onGenerateTitle, NotificationListenerCallback<NavigationNotification>? onNavigationNotification, Color? color, Locale? locale, Iterable<LocalizationsDelegate<dynamic>>? localizationsDelegates, LocaleListResolutionCallback? localeListResolutionCallback, LocaleResolutionCallback? localeResolutionCallback, Iterable<Locale> supportedLocales = const <Locale>[Locale('en', 'US')], bool showPerformanceOverlay = false, bool checkerboardRasterCacheImages = false, bool checkerboardOffscreenLayers = false, bool showSemanticsDebugger = false, bool debugShowCheckedModeBanner = true, Map<ShortcutActivator, Intent>? shortcuts, Map<Type, Action<Intent>>? actions, String? restorationScopeId, ScrollBehavior? scrollBehavior, bool useInheritedMediaQuery = false})
```

Creates a [CupertinoApp] that uses the [Router] instead of a [Navigator].

{@macro flutter.widgets.WidgetsApp.router}

### navigatorKey

```dart
GlobalKey<NavigatorState>? navigatorKey
```

{@macro flutter.widgets.widgetsApp.navigatorKey}

### home

```dart
Widget? home
```

{@macro flutter.widgets.widgetsApp.home}

### theme

```dart
CupertinoThemeData? theme
```

The top-level [CupertinoTheme] styling.

A null [theme] or unspecified [theme] attributes will default to iOS system values.

### routes

```dart
Map<String, WidgetBuilder>? routes
```

The application's top-level routing table.

When a named route is pushed with [Navigator.pushNamed], the route name is looked up in this map. If the name is present, the associated [WidgetBuilder] is used to construct a [CupertinoPageRoute] that performs an appropriate transition, including [Hero] animations, to the new route.

{@macro flutter.widgets.widgetsApp.routes}

### initialRoute

```dart
String? initialRoute
```

{@macro flutter.widgets.widgetsApp.initialRoute}

### onGenerateRoute

```dart
RouteFactory? onGenerateRoute
```

{@macro flutter.widgets.widgetsApp.onGenerateRoute}

### onGenerateInitialRoutes

```dart
InitialRouteListFactory? onGenerateInitialRoutes
```

{@macro flutter.widgets.widgetsApp.onGenerateInitialRoutes}

### onUnknownRoute

```dart
RouteFactory? onUnknownRoute
```

{@macro flutter.widgets.widgetsApp.onUnknownRoute}

### onNavigationNotification

```dart
NotificationListenerCallback<NavigationNotification>? onNavigationNotification
```

{@macro flutter.widgets.widgetsApp.onNavigationNotification}

### navigatorObservers

```dart
List<NavigatorObserver>? navigatorObservers
```

{@macro flutter.widgets.widgetsApp.navigatorObservers}

### routeInformationProvider

```dart
RouteInformationProvider? routeInformationProvider
```

{@macro flutter.widgets.widgetsApp.routeInformationProvider}

### routeInformationParser

```dart
RouteInformationParser<Object>? routeInformationParser
```

{@macro flutter.widgets.widgetsApp.routeInformationParser}

### routerDelegate

```dart
RouterDelegate<Object>? routerDelegate
```

{@macro flutter.widgets.widgetsApp.routerDelegate}

### backButtonDispatcher

```dart
BackButtonDispatcher? backButtonDispatcher
```

{@macro flutter.widgets.widgetsApp.backButtonDispatcher}

### routerConfig

```dart
RouterConfig<Object>? routerConfig
```

{@macro flutter.widgets.widgetsApp.routerConfig}

### builder

```dart
TransitionBuilder? builder
```

{@macro flutter.widgets.widgetsApp.builder}

### title

```dart
String? title
```

{@macro flutter.widgets.widgetsApp.title}

This value is passed unmodified to [WidgetsApp.title].

### onGenerateTitle

```dart
GenerateAppTitle? onGenerateTitle
```

{@macro flutter.widgets.widgetsApp.onGenerateTitle}

This value is passed unmodified to [WidgetsApp.onGenerateTitle].

### color

```dart
Color? color
```

{@macro flutter.widgets.widgetsApp.color}

### locale

```dart
Locale? locale
```

{@macro flutter.widgets.widgetsApp.locale}

### localizationsDelegates

```dart
Iterable<LocalizationsDelegate<dynamic>>? localizationsDelegates
```

{@macro flutter.widgets.widgetsApp.localizationsDelegates}

### localeListResolutionCallback

```dart
LocaleListResolutionCallback? localeListResolutionCallback
```

{@macro flutter.widgets.widgetsApp.localeListResolutionCallback}

This callback is passed along to the [WidgetsApp] built by this widget.

### localeResolutionCallback

```dart
LocaleResolutionCallback? localeResolutionCallback
```

{@macro flutter.widgets.LocaleResolutionCallback}

This callback is passed along to the [WidgetsApp] built by this widget.

### supportedLocales

```dart
Iterable<Locale> supportedLocales
```

{@macro flutter.widgets.widgetsApp.supportedLocales}

It is passed along unmodified to the [WidgetsApp] built by this widget.

### showPerformanceOverlay

```dart
bool showPerformanceOverlay
```

Turns on a performance overlay.

See also:

- <https://flutter.dev/to/performance-overlay>

### checkerboardRasterCacheImages

```dart
bool checkerboardRasterCacheImages
```

Turns on checkerboarding of raster cache images.

### checkerboardOffscreenLayers

```dart
bool checkerboardOffscreenLayers
```

Turns on checkerboarding of layers rendered to offscreen bitmaps.

### showSemanticsDebugger

```dart
bool showSemanticsDebugger
```

Turns on an overlay that shows the accessibility information reported by the framework.

### debugShowCheckedModeBanner

```dart
bool debugShowCheckedModeBanner
```

{@macro flutter.widgets.widgetsApp.debugShowCheckedModeBanner}

### shortcuts

```dart
Map<ShortcutActivator, Intent>? shortcuts
```

{@macro flutter.widgets.widgetsApp.shortcuts} {@tool snippet} This example shows how to add a single shortcut for [LogicalKeyboardKey.select] to the default shortcuts without needing to add your own [Shortcuts] widget.

Alternatively, you could insert a [Shortcuts] widget with just the mapping you want to add between the [WidgetsApp] and its child and get the same effect.

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

{@end-tool} {@macro flutter.widgets.widgetsApp.shortcuts.seeAlso}

### actions

```dart
Map<Type, Action<Intent>>? actions
```

{@macro flutter.widgets.widgetsApp.actions} {@tool snippet} This example shows how to add a single action handling an [ActivateAction] to the default actions without needing to add your own [Actions] widget.

Alternatively, you could insert a [Actions] widget with just the mapping you want to add between the [WidgetsApp] and its child and get the same effect.

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

{@end-tool} {@macro flutter.widgets.widgetsApp.actions.seeAlso}

### restorationScopeId

```dart
String? restorationScopeId
```

{@macro flutter.widgets.widgetsApp.restorationScopeId}

### scrollBehavior

```dart
ScrollBehavior? scrollBehavior
```

{@macro flutter.material.materialApp.scrollBehavior}

When null, defaults to [CupertinoScrollBehavior].

See also:

- [ScrollConfiguration], which controls how [Scrollable] widgets behave in a subtree.

### useInheritedMediaQuery

```dart
bool useInheritedMediaQuery
```

{@macro flutter.widgets.widgetsApp.useInheritedMediaQuery}

### createState()

```dart
State<CupertinoApp> createState()
```

### createCupertinoHeroController()

```dart
HeroController createCupertinoHeroController()
```

The [HeroController] used for Cupertino page transitions.

Used by [CupertinoTabView] and [CupertinoApp].

# CupertinoScrollBehavior

```dart
class CupertinoScrollBehavior extends ScrollBehavior {}
```

Describes how [Scrollable] widgets behave for [CupertinoApp]s.

{@macro flutter.widgets.scrollBehavior}

Setting a [CupertinoScrollBehavior] will result in descendant [Scrollable] widgets using [BouncingScrollPhysics] by default. No [GlowingOverscrollIndicator] is applied when using a [CupertinoScrollBehavior] either, regardless of platform. When executing on desktop platforms, a [CupertinoScrollbar] is applied to the child.

See also:

- [ScrollBehavior], the default scrolling behavior extended by this class.

### CupertinoScrollBehavior()

```dart
CupertinoScrollBehavior()
```

Creates a CupertinoScrollBehavior that uses [BouncingScrollPhysics] and adds [CupertinoScrollbar]s on desktop platforms.

### buildScrollbar()

```dart
Widget buildScrollbar(BuildContext context, Widget child, ScrollableDetails details)
```

### buildOverscrollIndicator()

```dart
Widget buildOverscrollIndicator(BuildContext context, Widget child, ScrollableDetails details)
```

### getScrollPhysics()

```dart
ScrollPhysics getScrollPhysics(BuildContext context)
```

### getMultitouchDragStrategy()

```dart
MultitouchDragStrategy getMultitouchDragStrategy(BuildContext context)
```
