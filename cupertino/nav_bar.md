@docImport 'refresh.dart';

# NavigationBarBottomMode

```dart
enum NavigationBarBottomMode {}
```

Modes that determine how to display the navigation bar's bottom in relation to scroll events.

Enable hiding the bottom in response to scrolling.

As scrolling starts, the large title stays pinned while the bottom resizes until it is completely consumed. Then, the large title scrolls under the persistent navigation bar.

Always display the bottom regardless of the scroll activity.

When scrolled, the bottom stays pinned while the large title scrolls under the persistent navigation bar.

# CupertinoNavigationBar

```dart
class CupertinoNavigationBar extends StatefulWidget implements ObstructingPreferredSizeWidget {}
```

An iOS-styled navigation bar.

The navigation bar is a toolbar that minimally consists of a widget, normally a page title.

It also supports [leading] and [trailing] widgets on either end of the toolbar, typically for actions and navigation.

The [leading] widget will automatically be a back chevron icon button (or a cancel button in case of a fullscreen dialog) to pop the current route if none is provided and [automaticallyImplyLeading] is true (true by default).

This toolbar should be placed at top of the screen where it will automatically account for the OS's status bar.

If the given [backgroundColor]'s opacity is not 1.0 (which is the case by default), it will produce a blurring effect to the content behind it.

### Layout options

While the [CupertinoSliverNavigationBar] can dynamically change size and layout in response to scrolling, this static version can reflect the same large (expanded) layout, or the small (collapsed) layout.

The default constructor will display the collapsed version of the [CupertinoSliverNavigationBar]. The [middle] widget will automatically be a title text from the current [CupertinoPageRoute] if none is provided and [automaticallyImplyMiddle] is true (true by default).

Using the [CupertinoNavigationBar.large] constructor will display the expanded version of [CupertinoSliverNavigationBar]. The [largeTitle] widget will automatically be a title text from the current [CupertinoPageRoute] if none is provided and `automaticallyImplyTitle` is true (true by default).

### Transitions

When [transitionBetweenRoutes] is true, this navigation bar will transition on top of the routes instead of inside them if the route being transitioned to also has a [CupertinoNavigationBar] or a [CupertinoSliverNavigationBar] with [transitionBetweenRoutes] set to true. If [transitionBetweenRoutes] is true, none of the [Widget] parameters can contain a key in its subtree since that widget will exist in multiple places in the tree simultaneously.

By default, only one [CupertinoNavigationBar] or [CupertinoSliverNavigationBar] should be present in each [PageRoute] to support the default transitions. Use [transitionBetweenRoutes] or [heroTag] to customize the transition behavior for multiple navigation bars per route.

When used in a [CupertinoPageScaffold], [CupertinoPageScaffold.navigationBar] disables text scaling to match the native iOS behavior. To override this behavior, wrap each of the `navigationBar`'s components inside a [MediaQuery] with the desired [TextScaler].

{@tool dartpad} This example shows a [CupertinoNavigationBar] placed in a [CupertinoPageScaffold]. Since [backgroundColor]'s opacity is not 1.0, there is a blur effect and content slides underneath.

** See code in examples/api/lib/cupertino/nav_bar/cupertino_navigation_bar.0.dart ** {@end-tool}

{@tool dartpad} This example shows the resulting layout from [CupertinoNavigationBar.large] constructor, showing a large title similar to the expanded state of [CupertinoSliverNavigationBar].

** See code in examples/api/lib/cupertino/nav_bar/cupertino_navigation_bar.2.dart ** {@end-tool}

See also:

- [CupertinoPageScaffold], a page layout helper typically hosting the [CupertinoNavigationBar].
- [CupertinoSliverNavigationBar] for a navigation bar to be placed in a scrolling list and that supports iOS-11-style large titles.
- <https://developer.apple.com/design/human-interface-guidelines/ios/bars/navigation-bars/>

### CupertinoNavigationBar()

```dart
CupertinoNavigationBar({dynamic key, Widget? leading, bool automaticallyImplyLeading = true, bool automaticallyImplyMiddle = true, String? previousPageTitle, Widget? middle, Widget? trailing, Border? border = _kDefaultNavBarBorder, Color? backgroundColor, bool automaticBackgroundVisibility = true, bool enableBackgroundFilterBlur = true, Brightness? brightness, EdgeInsetsDirectional? padding, bool transitionBetweenRoutes = true, Object heroTag = _defaultHeroTag, PreferredSizeWidget? bottom})
```

Creates a static iOS style navigation bar, with a centered [middle] title.

Similar to the collapsed state of [CupertinoSliverNavigationBar], which can dynamically change size in response to scrolling.

See also:

- [CupertinoNavigationBar.large], which creates a static iOS style navigation bar with a [largeTitle], similar to the expanded state of [CupertinoSliverNavigationBar].

### CupertinoNavigationBar.large()

```dart
CupertinoNavigationBar.large({dynamic key, Widget? largeTitle, Widget? leading, bool automaticallyImplyLeading = true, bool automaticallyImplyTitle = true, String? previousPageTitle, Widget? trailing, Border? border = _kDefaultNavBarBorder, Color? backgroundColor, bool automaticBackgroundVisibility = true, bool enableBackgroundFilterBlur = true, Brightness? brightness, EdgeInsetsDirectional? padding, bool transitionBetweenRoutes = true, Object heroTag = _defaultHeroTag, PreferredSizeWidget? bottom})
```

Creates a static iOS style navigation bar, with a left aligned [largeTitle].

Similar to the expanded state of [CupertinoSliverNavigationBar], which can dynamically change size in response to scrolling.

See also:

- [CupertinoNavigationBar]'s base constructor, which creates a static iOS style navigation bar with [middle], similar to the collapsed state of [CupertinoSliverNavigationBar].

### largeTitle

```dart
Widget? largeTitle
```

The navigation bar's title, when using [CupertinoNavigationBar.large].

If null and `automaticallyImplyTitle` is true, an appropriate [Text] title will be created if the current route is a [CupertinoPageRoute] and has a `title`.

This property is null for the base [CupertinoNavigationBar] constructor, which shows a collapsed navigation bar and uses [middle] for the title instead.

See also:

- [CupertinoSliverNavigationBar.largeTitle], a similar property in the expanded state of [CupertinoSliverNavigationBar], which can dynamically change size in response to scrolling.

### leading

```dart
Widget? leading
```

{@template flutter.cupertino.CupertinoNavigationBar.leading} Widget to place at the start of the navigation bar. Normally a back button for a normal page or a cancel button for full page dialogs.

If null and [automaticallyImplyLeading] is true, an appropriate button will be automatically created. {@endtemplate}

### automaticallyImplyLeading

```dart
bool automaticallyImplyLeading
```

{@template flutter.cupertino.CupertinoNavigationBar.automaticallyImplyLeading} Controls whether we should try to imply the leading widget if null.

If true and [leading] is null, automatically try to deduce what the [leading] widget should be. If [leading] widget is not null, this parameter has no effect.

Specifically this navigation bar will:

1.  Show a 'Cancel' button if the current route is a `fullscreenDialog`.
2.  Show a back chevron with [previousPageTitle] if [previousPageTitle] is not null.
3.  Show a back chevron with the previous route's `title` if the current route is a [CupertinoPageRoute] and the previous route is also a [CupertinoPageRoute]. {@endtemplate}

### automaticallyImplyMiddle

```dart
bool automaticallyImplyMiddle
```

Controls whether we should try to imply the middle widget if null.

If true and [middle] is null, automatically fill in a [Text] widget with the current route's `title` if the route is a [CupertinoPageRoute]. If [middle] widget is not null, this parameter has no effect.

### previousPageTitle

```dart
String? previousPageTitle
```

{@template flutter.cupertino.CupertinoNavigationBar.previousPageTitle} Manually specify the previous route's title when automatically implying the leading back button.

Overrides the text shown with the back chevron instead of automatically showing the previous [CupertinoPageRoute]'s `title` when [automaticallyImplyLeading] is true.

Has no effect when [leading] is not null or if [automaticallyImplyLeading] is false. {@endtemplate}

### middle

```dart
Widget? middle
```

The navigation bar's default title.

If null and [automaticallyImplyMiddle] is true, an appropriate [Text] title will be created if the current route is a [CupertinoPageRoute] and has a `title`.

This property is null for the [CupertinoNavigationBar.large] constructor, which shows an expanded navigation bar and uses [largeTitle] instead.

See also:

- [CupertinoSliverNavigationBar.middle], a similar property in the collapsed state of [CupertinoSliverNavigationBar], which can dynamically change size in response to scrolling.

### trailing

```dart
Widget? trailing
```

{@template flutter.cupertino.CupertinoNavigationBar.trailing} Widget to place at the end of the navigation bar. Normally additional actions taken on the page such as a search or edit function. {@endtemplate}

### backgroundColor

```dart
Color? backgroundColor
```

{@template flutter.cupertino.CupertinoNavigationBar.backgroundColor} The background color of the navigation bar. If it contains transparency, the tab bar will automatically produce a blurring effect to the content behind it. This behavior can be disabled by setting [enableBackgroundFilterBlur] to false.

By default, the navigation bar's background is visible only when scrolled under. This behavior can be controlled with [automaticBackgroundVisibility].

Defaults to [CupertinoTheme]'s `barBackgroundColor` if null. {@endtemplate}

### automaticBackgroundVisibility

```dart
bool automaticBackgroundVisibility
```

{@template flutter.cupertino.CupertinoNavigationBar.automaticBackgroundVisibility} Whether the navigation bar appears transparent when no content is scrolled under.

If this is true, the navigation bar's background color will be transparent until the content scrolls under it. If false, the navigation bar will always use [backgroundColor] as its background color.

If the navigation bar is not a child of a [CupertinoPageScaffold], this has no effect.

This value defaults to true. {@endtemplate}

### brightness

```dart
Brightness? brightness
```

{@template flutter.cupertino.CupertinoNavigationBar.brightness} The brightness of the specified [backgroundColor].

Setting this value changes the style of the system status bar. Typically used to increase the contrast ratio of the system status bar over [backgroundColor].

If set to null, the value of the property will be inferred from the relative luminance of [backgroundColor]. {@endtemplate}

### padding

```dart
EdgeInsetsDirectional? padding
```

{@template flutter.cupertino.CupertinoNavigationBar.padding} Padding for the contents of the navigation bar.

If null, the navigation bar will adopt the following defaults:

- Vertically, contents will be sized to the same height as the navigation bar itself minus the status bar.
- Horizontally, padding will be 16 pixels according to iOS specifications unless the leading widget is an automatically inserted back button, in which case the padding will be 0.

Vertical padding won't change the height of the nav bar. {@endtemplate}

### border

```dart
Border? border
```

{@template flutter.cupertino.CupertinoNavigationBar.border} The border of the navigation bar. By default renders a single pixel bottom border side.

If a border is null, the navigation bar will not display a border. {@endtemplate}

### transitionBetweenRoutes

```dart
bool transitionBetweenRoutes
```

{@template flutter.cupertino.CupertinoNavigationBar.transitionBetweenRoutes} Whether to transition between navigation bars.

When [transitionBetweenRoutes] is true, this navigation bar will transition on top of the routes instead of inside it if the route being transitioned to also has a [CupertinoNavigationBar] or a [CupertinoSliverNavigationBar] with [transitionBetweenRoutes] set to true.

This transition will also occur on edge back swipe gestures like on iOS but only if the previous page below has `maintainState` set to true on the [PageRoute].

When set to true, only one navigation bar can be present per route unless [heroTag] is also set.

This value defaults to true. {@endtemplate}

### enableBackgroundFilterBlur

```dart
bool enableBackgroundFilterBlur
```

{@template flutter.cupertino.CupertinoNavigationBar.enableBackgroundFilterBlur} Whether to have a blur effect when a non-opaque background color is used.

When [enableBackgroundFilterBlur] is set to false, the blur effect will be disabled. The behaviour of [enableBackgroundFilterBlur] will only be respected when [automaticBackgroundVisibility] is false or until content scrolls under the navbar.

This value defaults to true. {@endtemplate}

### heroTag

```dart
Object heroTag
```

{@template flutter.cupertino.CupertinoNavigationBar.heroTag} Tag for the navigation bar's Hero widget if [transitionBetweenRoutes] is true.

Defaults to a common tag between all [CupertinoNavigationBar] and [CupertinoSliverNavigationBar] instances of the same [Navigator]. With the default tag, all navigation bars of the same navigator can transition between each other as long as there's only one navigation bar per route.

This [heroTag] can be overridden to manually handle having multiple navigation bars per route or to transition between multiple [Navigator]s.

To disable Hero transitions for this navigation bar, set [transitionBetweenRoutes] to false. {@endtemplate}

### bottom

```dart
PreferredSizeWidget? bottom
```

A widget to place at the bottom of the navigation bar.

Only widgets that implement [PreferredSizeWidget] can be used at the bottom of a navigation bar.

{@tool dartpad} This example shows a [CupertinoSearchTextField] at the bottom of a [CupertinoNavigationBar].

** See code in examples/api/lib/cupertino/nav_bar/cupertino_navigation_bar.1.dart ** {@end-tool}

See also:

- [PreferredSize], which can be used to give an arbitrary widget a preferred size.

### shouldFullyObstruct()

```dart
bool shouldFullyObstruct(BuildContext context)
```

True if the navigation bar's background color has no transparency.

### preferredSize

```dart
Size get preferredSize
```

### createState()

```dart
State<CupertinoNavigationBar> createState()
```

# CupertinoSliverNavigationBar

```dart
class CupertinoSliverNavigationBar extends StatefulWidget {}
```

An iOS-styled navigation bar with iOS-11-style large titles using slivers.

The [CupertinoSliverNavigationBar] must be placed in a sliver group such as the [CustomScrollView].

This navigation bar consists of two sections, a pinned static section on top and a sliding section containing iOS-11-style large title below it.

It should be placed at top of the screen and automatically accounts for the iOS status bar.

This navigation bar is expanded only in portrait orientation. In landscape mode, the navigation bar remains permanently collapsed. The navigation bar also collapses when scrolling in portrait mode.

Minimally, a [largeTitle] widget will appear in the middle of the app bar when the sliver is collapsed and transfer to the area below in larger font when the sliver is expanded. This expanded view will only trigger in portrait orientation, while in landscape mode the bar will stay in its collapsed view.

For advanced uses, an optional [middle] widget can be supplied to show a different widget in the middle of the navigation bar when the sliver is collapsed.

Like [CupertinoNavigationBar], it also supports a [leading] and [trailing] widget on the static section on top that remains while scrolling.

The [leading] widget will automatically be a back chevron icon button (or a cancel button in case of a fullscreen dialog) to pop the current route if none is provided and [automaticallyImplyLeading] is true (true by default).

The [largeTitle] widget will automatically be a title text from the current [CupertinoPageRoute] if none is provided and [automaticallyImplyTitle] is true (true by default).

When [transitionBetweenRoutes] is true, this navigation bar will transition on top of the routes instead of inside them if the route being transitioned to also has a [CupertinoNavigationBar] or a [CupertinoSliverNavigationBar] with [transitionBetweenRoutes] set to true. If [transitionBetweenRoutes] is true, none of the [Widget] parameters can contain any [GlobalKey]s in their subtrees since those widgets will exist in multiple places in the tree simultaneously.

By default, only one [CupertinoNavigationBar] or [CupertinoSliverNavigationBar] should be present in each [PageRoute] to support the default transitions. Use [transitionBetweenRoutes] or [heroTag] to customize the transition behavior for multiple navigation bars per route.

The [stretch] parameter determines whether the nav bar should stretch to fill the over-scroll area. The nav bar can still expand and contract as the user scrolls, but it will also stretch when the user over-scrolls if the [stretch] value is `true`. Defaults to `false`.

{@tool dartpad} This example shows [CupertinoSliverNavigationBar] in action inside a [CustomScrollView].

** See code in examples/api/lib/cupertino/nav_bar/cupertino_sliver_nav_bar.0.dart ** {@end-tool}

{@tool dartpad} To add a widget to the bottom of the nav bar, wrap it with [PreferredSize] and provide its fully extended size.

** See code in examples/api/lib/cupertino/nav_bar/cupertino_sliver_nav_bar.2.dart ** {@end-tool}

See also:

- [CupertinoNavigationBar], an iOS navigation bar for use on non-scrolling pages.
- [CustomScrollView], a ScrollView that creates custom scroll effects using slivers.
- <https://developer.apple.com/design/human-interface-guidelines/ios/bars/navigation-bars/>

### CupertinoSliverNavigationBar()

```dart
CupertinoSliverNavigationBar({dynamic key, Widget? largeTitle, Widget? leading, bool automaticallyImplyLeading = true, bool automaticallyImplyTitle = true, bool alwaysShowMiddle = true, String? previousPageTitle, Widget? middle, Widget? trailing, Border? border = _kDefaultNavBarBorder, Color? backgroundColor, bool automaticBackgroundVisibility = true, bool enableBackgroundFilterBlur = true, Brightness? brightness, EdgeInsetsDirectional? padding, bool transitionBetweenRoutes = true, Object heroTag = _defaultHeroTag, bool stretch = false, PreferredSizeWidget? bottom, NavigationBarBottomMode? bottomMode})
```

Creates a navigation bar for scrolling lists.

If [automaticallyImplyTitle] is false, then the [largeTitle] argument is required.

### CupertinoSliverNavigationBar.search()

```dart
CupertinoSliverNavigationBar.search({dynamic key, required Widget? searchField, Widget? largeTitle, Widget? leading, bool automaticallyImplyLeading = true, bool automaticallyImplyTitle = true, bool alwaysShowMiddle = true, String? previousPageTitle, Widget? middle, Widget? trailing, Border? border = _kDefaultNavBarBorder, Color? backgroundColor, bool automaticBackgroundVisibility = true, bool enableBackgroundFilterBlur = true, Brightness? brightness, EdgeInsetsDirectional? padding, bool transitionBetweenRoutes = true, Object heroTag = _defaultHeroTag, bool stretch = false, NavigationBarBottomMode? bottomMode = NavigationBarBottomMode.automatic, ValueChanged<bool>? onSearchableBottomTap})
```

A navigation bar for scrolling lists that integrates a provided search field directly into the navigation bar.

This search-enabled navigation bar is functionally equivalent to the standard [CupertinoSliverNavigationBar] constructor, but with the addition of [searchField], which sits at the bottom of the navigation bar.

When the search field is tapped, [leading], [trailing], [middle], and [largeTitle] all collapse, causing the search field to animate to the 'top' of the navigation bar. A 'Cancel' button is presented next to the active [searchField], which when tapped, closes the search view, bringing the navigation bar back to its initial state.

If [automaticallyImplyTitle] is false, then the [largeTitle] argument is required.

{@tool dartpad} This example demonstrates how to use a [CupertinoSliverNavigationBar.search] to manage a search view.

** See code in examples/api/lib/cupertino/nav_bar/cupertino_sliver_nav_bar.1.dart ** {@end-tool}

### largeTitle

```dart
Widget? largeTitle
```

The navigation bar's title.

This text will appear in the top static navigation bar when collapsed and below the navigation bar, in a larger font, when expanded.

A suitable [DefaultTextStyle] is provided around this widget as it is moved around, to change its font size.

If [middle] is null, then the [largeTitle] widget will be inserted into the tree in two places when transitioning from the collapsed state to the expanded state. It is therefore imperative that this subtree not contain any [GlobalKey]s, and that it not rely on maintaining state (for example, animations will not survive the transition from one location to the other, and may in fact be visible in two places at once during the transition).

If null and [automaticallyImplyTitle] is true, an appropriate [Text] title will be created if the current route is a [CupertinoPageRoute] and has a `title`.

This parameter must either be non-null or the route must have a title ([CupertinoPageRoute.title]) and [automaticallyImplyTitle] must be true.

### leading

```dart
Widget? leading
```

{@macro flutter.cupertino.CupertinoNavigationBar.leading}

This widget is visible in both collapsed and expanded states.

### automaticallyImplyLeading

```dart
bool automaticallyImplyLeading
```

{@macro flutter.cupertino.CupertinoNavigationBar.automaticallyImplyLeading}

### automaticallyImplyTitle

```dart
bool automaticallyImplyTitle
```

Controls whether we should try to imply the [largeTitle] widget if null.

If true and [largeTitle] is null, automatically fill in a [Text] widget with the current route's `title` if the route is a [CupertinoPageRoute]. If [largeTitle] widget is not null, this parameter has no effect.

### alwaysShowMiddle

```dart
bool alwaysShowMiddle
```

Controls whether [middle] widget should always be visible (even in expanded state).

If true (default) and [middle] is not null, [middle] widget is always visible. If false, [middle] widget is visible only in collapsed state if it is provided.

This should be set to false if you only want to show [largeTitle] in expanded state and [middle] in collapsed state.

### previousPageTitle

```dart
String? previousPageTitle
```

{@macro flutter.cupertino.CupertinoNavigationBar.previousPageTitle}

### middle

```dart
Widget? middle
```

A widget to place in the middle of the static navigation bar instead of the [largeTitle].

If [alwaysShowMiddle] is true, this widget is visible in both the collapsed and expanded states of the navigation bar. Else, it is visible only in the collapsed state.

If null, [largeTitle] will be displayed in the navigation bar's collapsed state.

### trailing

```dart
Widget? trailing
```

{@macro flutter.cupertino.CupertinoNavigationBar.trailing}

This widget is visible in both collapsed and expanded states.

### backgroundColor

```dart
Color? backgroundColor
```

{@macro flutter.cupertino.CupertinoNavigationBar.backgroundColor}

### automaticBackgroundVisibility

```dart
bool automaticBackgroundVisibility
```

{@macro flutter.cupertino.CupertinoNavigationBar.automaticBackgroundVisibility}

### enableBackgroundFilterBlur

```dart
bool enableBackgroundFilterBlur
```

{@macro flutter.cupertino.CupertinoNavigationBar.enableBackgroundFilterBlur}

### brightness

```dart
Brightness? brightness
```

{@macro flutter.cupertino.CupertinoNavigationBar.brightness}

### padding

```dart
EdgeInsetsDirectional? padding
```

{@macro flutter.cupertino.CupertinoNavigationBar.padding}

### border

```dart
Border? border
```

{@macro flutter.cupertino.CupertinoNavigationBar.border}

### transitionBetweenRoutes

```dart
bool transitionBetweenRoutes
```

{@macro flutter.cupertino.CupertinoNavigationBar.transitionBetweenRoutes}

### heroTag

```dart
Object heroTag
```

{@macro flutter.cupertino.CupertinoNavigationBar.heroTag}

### bottom

```dart
PreferredSizeWidget? bottom
```

A widget to place at the bottom of the large title or static navigation bar if there is no large title.

Only widgets that implement [PreferredSizeWidget] can be used at the bottom of a navigation bar.

See also:

- [PreferredSize], which can be used to give an arbitrary widget a preferred size.

### bottomMode

```dart
NavigationBarBottomMode? bottomMode
```

Modes that determine how to display the navigation bar's [bottom], or the search field in a [CupertinoSliverNavigationBar.search].

If null, defaults to [NavigationBarBottomMode.automatic] if either a [bottom] is provided or this is a [CupertinoSliverNavigationBar.search].

### onSearchableBottomTap

```dart
ValueChanged<bool>? onSearchableBottomTap
```

Called when the search field in [CupertinoSliverNavigationBar.search] is tapped, toggling between an active and an inactive search state.

### opaque

```dart
bool get opaque
```

True if the navigation bar's background color has no transparency.

### stretch

```dart
bool stretch
```

Whether the nav bar should stretch to fill the over-scroll area.

The nav bar can still expand and contract as the user scrolls, but it will also stretch when the user over-scrolls if the [stretch] value is `true`.

When set to `true`, the nav bar will prevent subsequent slivers from accessing overscrolls. This may be undesirable for using overscroll-based widgets like the [CupertinoSliverRefreshControl].

Defaults to `false`.

### searchField

```dart
Widget? searchField
```

The search field used in [CupertinoSliverNavigationBar.search].

The provided search field is constrained to a fixed height of 35 pixels in its inactive state, and [kMinInteractiveDimensionCupertino] pixels in its active state.

Typically a [CupertinoSearchTextField].

### createState()

```dart
State<CupertinoSliverNavigationBar> createState()
```

# CupertinoNavigationBarBackButton

```dart
class CupertinoNavigationBarBackButton extends StatelessWidget {}
```

A nav bar back button typically used in [CupertinoNavigationBar].

This is automatically inserted into [CupertinoNavigationBar] and [CupertinoSliverNavigationBar]'s `leading` slot when `automaticallyImplyLeading` is true.

When manually inserted, the [CupertinoNavigationBarBackButton] should only be used in routes that can be popped unless a custom [onPressed] is provided.

Shows a back chevron and the previous route's title when available from the previous [CupertinoPageRoute.title]. If [previousPageTitle] is specified, it will be shown instead.

### CupertinoNavigationBarBackButton()

```dart
CupertinoNavigationBarBackButton({dynamic key, Color? color, String? previousPageTitle, VoidCallback? onPressed})
```

Construct a [CupertinoNavigationBarBackButton] that can be used to pop the current route.

### color

```dart
Color? color
```

The [Color] of the back button.

Can be used to override the color of the back button chevron and label.

Defaults to [CupertinoTheme]'s `primaryColor` if null.

### previousPageTitle

```dart
String? previousPageTitle
```

An override for showing the previous route's title. If null, it will be automatically derived from [CupertinoPageRoute.title] if the current and previous routes are both [CupertinoPageRoute]s.

### onPressed

```dart
VoidCallback? onPressed
```

An override callback to perform instead of the default behavior which is to pop the [Navigator].

It can, for instance, be used to pop the platform's navigation stack via [SystemNavigator] instead of Flutter's [Navigator] in add-to-app situations.

Defaults to null.

### build()

```dart
Widget build(BuildContext context)
```
