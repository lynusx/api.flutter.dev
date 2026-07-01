@docImport 'app.dart'; @docImport 'drawer.dart'; @docImport 'popup_menu.dart'; @docImport 'snack_bar.dart'; @docImport 'text_button.dart'; @docImport 'text_field.dart';

# AppBar

```dart
class AppBar extends StatefulWidget implements PreferredSizeWidget {}
```

A Material Design app bar.

An app bar consists of a toolbar and potentially other widgets, such as a [TabBar] and a [FlexibleSpaceBar]. App bars typically expose one or more common [actions] with [IconButton]s which are optionally followed by a [PopupMenuButton] for less common operations (sometimes called the "overflow menu").

App bars are typically used in the [Scaffold.appBar] property, which places the app bar as a fixed-height widget at the top of the screen. For a scrollable app bar, see [SliverAppBar], which embeds an [AppBar] in a sliver for use in a [CustomScrollView].

The AppBar displays the toolbar widgets, [leading], [title], and [actions], above the [bottom] (if any). The [bottom] is usually used for a [TabBar]. If a [flexibleSpace] widget is specified then it is stacked behind the toolbar and the bottom widget. The following diagram shows where each of these slots appears in the toolbar when the writing language is left-to-right (e.g. English):

![The leading widget is in the top left, the actions are in the top right, the title is between them. The bottom is, naturally, at the bottom, and the flexibleSpace is behind all of them.](https://flutter.github.io/assets-for-api-docs/assets/material/app_bar.png)

If the [leading] widget is omitted, but the [AppBar] is in a [Scaffold] with a [Drawer], then a button will be inserted to open the drawer. Otherwise, if the nearest [Navigator] has any previous routes, a [BackButton] is inserted instead. This behavior can be turned off by setting the [automaticallyImplyLeading] to false. In that case a null leading widget will result in the middle/title widget stretching to start.

If the [actions] widget list is omitted or empty, but the [AppBar] is in a [Scaffold] with an end [Drawer], then a button will be inserted to open the end drawer. This behavior can be turned off by setting the [automaticallyImplyActions] to false.

The [AppBar] insets its content based on the ambient [MediaQuery]'s padding, to avoid system UI intrusions. It's taken care of by [Scaffold] when used in the [Scaffold.appBar] property. When animating an [AppBar], unexpected [MediaQuery] changes (as is common in [Hero] animations) may cause the content to suddenly jump. Wrap the [AppBar] in a [MediaQuery] widget, and adjust its padding such that the animation is smooth.

{@tool dartpad} This sample shows an [AppBar] with two simple actions. The first action opens a [SnackBar], while the second action navigates to a new page.

** See code in examples/api/lib/material/app_bar/app_bar.0.dart ** {@end-tool}

Material Design 3 introduced new types of app bar. {@tool dartpad} This sample shows the creation of an [AppBar] widget with the [shadowColor] and [scrolledUnderElevation] properties set, as described in: https://m3.material.io/components/top-app-bar/overview

** See code in examples/api/lib/material/app_bar/app_bar.1.dart ** {@end-tool}

## Troubleshooting

### Why don't my TextButton actions appear?

If the app bar's [actions] contains [TextButton]s, they will not be visible if their foreground (text) color is the same as the app bar's background color.

In Material v2 (i.e., when [ThemeData.useMaterial3] is false), the default app bar [backgroundColor] is the overall theme's [ColorScheme.primary] if the overall theme's brightness is [Brightness.light]. Unfortunately this is the same as the default [ButtonStyle.foregroundColor] for [TextButton] for light themes. In this case a preferable text button foreground color is [ColorScheme.onPrimary], a color that contrasts nicely with [ColorScheme.primary]. To remedy the problem, override [TextButton.style]:

{@tool dartpad} This sample shows an [AppBar] with two action buttons with their primary color set to [ColorScheme.onPrimary].

** See code in examples/api/lib/material/app_bar/app_bar.2.dart ** {@end-tool}

{@tool dartpad} This example shows how to listen to a nested Scrollable's scroll notification in a nested scroll view using the [notificationPredicate] property and use it to make [scrolledUnderElevation] take effect.

** See code in examples/api/lib/material/app_bar/app_bar.3.dart ** {@end-tool}

See also:

- [Scaffold], which displays the [AppBar] in its [Scaffold.appBar] slot.
- [SliverAppBar], which uses [AppBar] to provide a flexible app bar that can be used in a [CustomScrollView].
- [TabBar], which is typically placed in the [bottom] slot of the [AppBar] if the screen has multiple pages arranged in tabs.
- [IconButton], which is used with [actions] to show buttons on the app bar.
- [PopupMenuButton], to show a popup menu on the app bar, via [actions].
- [FlexibleSpaceBar], which is used with [flexibleSpace] when the app bar can expand and collapse.
- <https://material.io/design/components/app-bars-top.html>
- <https://m3.material.io/components/top-app-bar>
- Cookbook: [Place a floating app bar above a list](https://docs.flutter.dev/cookbook/lists/floating-app-bar)

### AppBar()

```dart
AppBar({dynamic key, Widget? leading, bool automaticallyImplyLeading = true, Widget? title, List<Widget>? actions, bool automaticallyImplyActions = true, Widget? flexibleSpace, PreferredSizeWidget? bottom, double? elevation, double? scrolledUnderElevation, ScrollNotificationPredicate notificationPredicate = defaultScrollNotificationPredicate, Color? shadowColor, Color? surfaceTintColor, ShapeBorder? shape, Color? backgroundColor, Color? foregroundColor, IconThemeData? iconTheme, IconThemeData? actionsIconTheme, bool primary = true, bool? centerTitle, bool excludeHeaderSemantics = false, double? titleSpacing, double toolbarOpacity = 1.0, double bottomOpacity = 1.0, double? toolbarHeight, double? leadingWidth, TextStyle? toolbarTextStyle, TextStyle? titleTextStyle, SystemUiOverlayStyle? systemOverlayStyle, bool forceMaterialTransparency = false, bool useDefaultSemanticsOrder = true, Clip? clipBehavior, EdgeInsetsGeometry? actionsPadding, bool animateColor = false})
```

Creates a Material Design app bar.

If [elevation] is specified, it must be non-negative.

Typically used in the [Scaffold.appBar] property.

### preferredHeightFor()

```dart
double preferredHeightFor(BuildContext context, Size preferredSize)
```

Used by [Scaffold] to compute its [AppBar]'s overall height. The returned value is the same `preferredSize.height` unless [AppBar.toolbarHeight] was null and `AppBarTheme.of(context).toolbarHeight` is non-null. In that case the return value is the sum of the theme's toolbar height and the height of the app bar's [AppBar.bottom] widget.

### leading

```dart
Widget? leading
```

{@template flutter.material.appbar.leading} A widget to display before the toolbar's [title].

Typically the [leading] widget is an [Icon] or an [IconButton].

Becomes the leading component of the [NavigationToolbar] built by this widget. The [leading] widget's width and height are constrained to be no bigger than [leadingWidth] and [toolbarHeight] respectively.

If this is null and [automaticallyImplyLeading] is set to true, the [AppBar] will imply an appropriate widget. For example, if the [AppBar] is in a [Scaffold] that also has a [Drawer], the [Scaffold] will fill this widget with an [IconButton] that opens the drawer (using [Icons.menu]). If there's no [Drawer] and the parent [Navigator] can go back, the [AppBar] will use a [BackButton] that calls [Navigator.maybePop]. {@endtemplate}

{@tool snippet}

The following code shows how the drawer button could be manually specified instead of relying on [automaticallyImplyLeading]:

```dart
AppBar(
  leading: Builder(
    builder: (BuildContext context) {
      return IconButton(
        icon: const Icon(Icons.menu),
        onPressed: () { Scaffold.of(context).openDrawer(); },
        tooltip: MaterialLocalizations.of(context).openAppDrawerTooltip,
      );
    },
  ),
)
```

{@end-tool}

The [Builder] is used in this example to ensure that the `context` refers to that part of the subtree. That way this code snippet can be used even inside the very code that is creating the [Scaffold] (in which case, without the [Builder], the `context` wouldn't be able to see the [Scaffold], since it would refer to an ancestor of that widget).

See also:

- [Scaffold.appBar], in which an [AppBar] is usually placed.
- [Scaffold.drawer], in which the [Drawer] is usually placed.

### automaticallyImplyLeading

```dart
bool automaticallyImplyLeading
```

{@template flutter.material.appbar.automaticallyImplyLeading} Controls whether we should try to imply the leading widget if null.

If true and [AppBar.leading] is null, automatically try to deduce what the leading widget should be. If false and [AppBar.leading] is null, leading space is given to [AppBar.title]. If leading widget is not null, this parameter has no effect. {@endtemplate}

### title

```dart
Widget? title
```

{@template flutter.material.appbar.title} The primary widget displayed in the app bar.

Becomes the middle component of the [NavigationToolbar] built by this widget.

Typically a [Text] widget that contains a description of the current contents of the app. {@endtemplate}

The [title]'s width is constrained to fit within the remaining space between the toolbar's [leading] and [actions] widgets. Its height is _not_ constrained. The [title] is vertically centered and clipped to fit within the toolbar, whose height is [toolbarHeight]. Typically this isn't noticeable because a simple [Text] [title] will fit within the toolbar by default. On the other hand, it is noticeable when a widget with an intrinsic height that is greater than [toolbarHeight] is used as the [title]. For example, when the height of an Image used as the [title] exceeds [toolbarHeight], it will be centered and clipped (top and bottom), which may be undesirable. In cases like this the height of the [title] widget can be constrained. For example:

```dart
MaterialApp(
  home: Scaffold(
    appBar: AppBar(
      title: SizedBox(
        height: _myToolbarHeight,
        child: Image.asset(_logoAsset),
      ),
      toolbarHeight: _myToolbarHeight,
    ),
  ),
)
```

### actions

```dart
List<Widget>? actions
```

{@template flutter.material.appbar.actions} A list of Widgets to display in a row after the [title] widget.

Typically these widgets are [IconButton]s representing common operations. For less common operations, consider using a [PopupMenuButton] as the last action.

The [actions] become the trailing component of the [NavigationToolbar] built by this widget. The height of each action is constrained to be no bigger than the [toolbarHeight].

To avoid having the last action covered by the debug banner, you may want to set the [MaterialApp.debugShowCheckedModeBanner] to false.

If this is null or empty and [automaticallyImplyActions] is set to true, the [AppBar] will imply an appropriate widget. For example, if the [AppBar] is in a [Scaffold] that also has an end [Drawer], the [Scaffold] will fill this widget with an [IconButton] that opens the end drawer (using [Icons.menu]). {@endtemplate}

{@tool snippet}

```dart
Scaffold(
  body: CustomScrollView(
    primary: true,
    slivers: <Widget>[
      SliverAppBar(
        title: const Text('Hello World'),
        actions: <Widget>[
          IconButton(
            icon: const Icon(Icons.shopping_cart),
            tooltip: 'Open shopping cart',
            onPressed: () {
              // handle the press
            },
          ),
        ],
      ),
      // ...rest of body...
    ],
  ),
)
```

{@end-tool}

### automaticallyImplyActions

```dart
bool automaticallyImplyActions
```

{@template flutter.material.appbar.automaticallyImplyActions} Controls whether we should try to imply the actions widget if null.

If true and [AppBar.actions] is null or empty, automatically try to deduce what the actions widget should be. If false and [AppBar.actions] is null or empty, the actions widget list is kept empty. If [AppBar.actions] is not null, this parameter has no effect. {@endtemplate}

### flexibleSpace

```dart
Widget? flexibleSpace
```

{@template flutter.material.appbar.flexibleSpace} This widget is stacked behind the toolbar and the tab bar. Its height will be the same as the app bar's overall height.

A flexible space isn't actually flexible unless the [AppBar]'s container changes the [AppBar]'s size. A [SliverAppBar] in a [CustomScrollView] changes the [AppBar]'s height when scrolled.

Typically a [FlexibleSpaceBar]. See [FlexibleSpaceBar] for details. {@endtemplate}

### bottom

```dart
PreferredSizeWidget? bottom
```

{@template flutter.material.appbar.bottom} This widget appears across the bottom of the app bar.

Typically a [TabBar]. Only widgets that implement [PreferredSizeWidget] can be used at the bottom of an app bar. {@endtemplate}

See also:

- [PreferredSize], which can be used to give an arbitrary widget a preferred size.

### elevation

```dart
double? elevation
```

{@template flutter.material.appbar.elevation} The z-coordinate at which to place this app bar relative to its parent.

This property controls the size of the shadow below the app bar if [shadowColor] is not null.

If [surfaceTintColor] is not null then it will apply a surface tint overlay to the background color (see [Material.surfaceTintColor] for more detail).

The value must be non-negative.

If this property is null, then the ambient [AppBarThemeData.elevation] is used. If that is also null, the default value is 4. {@endtemplate}

See also:

- [scrolledUnderElevation], which will be used when the app bar has something scrolled underneath it.
- [shadowColor], which is the color of the shadow below the app bar.
- [surfaceTintColor], which determines the elevation overlay that will be applied to the background of the app bar.
- [shape], which defines the shape of the app bar's [Material] and its shadow.

### scrolledUnderElevation

```dart
double? scrolledUnderElevation
```

{@template flutter.material.appbar.scrolledUnderElevation} The elevation that will be used if this app bar has something scrolled underneath it.

If this property is null, then the ambient [AppBarThemeData.scrolledUnderElevation] is used. If that is also null then [elevation] is used.

The value must be non-negative.

{@endtemplate}

See also:

- [elevation], which will be used if there is no content scrolled under the app bar.
- [shadowColor], which is the color of the shadow below the app bar.
- [surfaceTintColor], which determines the elevation overlay that will be applied to the background of the app bar.
- [shape], which defines the shape of the app bar's [Material] and its shadow.

### notificationPredicate

```dart
ScrollNotificationPredicate notificationPredicate
```

A check that specifies which child's [ScrollNotification]s should be listened to.

By default, checks whether `notification.depth == 0`. Set it to something else for more complicated layouts.

### shadowColor

```dart
Color? shadowColor
```

{@template flutter.material.appbar.shadowColor} The color of the shadow below the app bar.

If this property is null, then the ambient [AppBarThemeData.shadowColor] is used. If that is also null, the default value is fully opaque black. {@endtemplate}

See also:

- [elevation], which defines the size of the shadow below the app bar.
- [shape], which defines the shape of the app bar and its shadow.

### surfaceTintColor

```dart
Color? surfaceTintColor
```

{@template flutter.material.appbar.surfaceTintColor} The color of the surface tint overlay applied to the app bar's background color to indicate elevation.

If null no overlay will be applied. {@endtemplate}

See also:

- [Material.surfaceTintColor], which described this feature in more detail.

### shape

```dart
ShapeBorder? shape
```

{@template flutter.material.appbar.shape} The shape of the app bar's [Material] as well as its shadow.

If this property is null, then the ambient [AppBarThemeData.shape] is used. Both properties default to null. If both properties are null then the shape of the app bar's [Material] is just a simple rectangle.

A shadow is only displayed if the [elevation] is greater than zero. {@endtemplate}

{@tool dartpad} This sample demonstrates how to implement a custom app bar shape for the [shape] property.

** See code in examples/api/lib/material/app_bar/app_bar.4.dart ** {@end-tool} See also:

- [elevation], which defines the size of the shadow below the app bar.
- [shadowColor], which is the color of the shadow below the app bar.

### backgroundColor

```dart
Color? backgroundColor
```

{@template flutter.material.appbar.backgroundColor} The fill color to use for an app bar's [Material].

If null, then the [AppBarTheme.backgroundColor] is used. If that value is also null: In Material v2 (i.e., when [ThemeData.useMaterial3] is false), then [AppBar] uses the overall theme's [ColorScheme.primary] if the overall theme's brightness is [Brightness.light], and [ColorScheme.surface] if the overall theme's brightness is [Brightness.dark]. In Material v3 (i.e., when [ThemeData.useMaterial3] is true), then [AppBar] uses the overall theme's [ColorScheme.surface]

If this color is a [WidgetStateColor] it will be resolved against [WidgetState.scrolledUnder] when the content of the app's primary scrollable overlaps the app bar. {@endtemplate}

See also:

- [foregroundColor], which specifies the color for icons and text within the app bar.
- [Theme.of], which returns the current overall Material theme as a [ThemeData].
- [ThemeData.colorScheme], the thirteen colors that most Material widget default colors are based on.
- [ColorScheme.brightness], which indicates if the overall [Theme] is light or dark.

### foregroundColor

```dart
Color? foregroundColor
```

{@template flutter.material.appbar.foregroundColor} The default color for [Text] and [Icon]s within the app bar.

If null, then [AppBarTheme.foregroundColor] is used. If that value is also null: In Material v2 (i.e., when [ThemeData.useMaterial3] is false), then [AppBar] uses the overall theme's [ColorScheme.onPrimary] if the overall theme's brightness is [Brightness.light], and [ColorScheme.onSurface] if the overall theme's brightness is [Brightness.dark]. In Material v3 (i.e., when [ThemeData.useMaterial3] is true), then [AppBar] uses the overall theme's [ColorScheme.onSurface].

This color is used to configure [DefaultTextStyle] that contains the toolbar's children, and the default [IconTheme] widgets that are created if [iconTheme] and [actionsIconTheme] are null. {@endtemplate}

See also:

- [backgroundColor], which specifies the app bar's background color.
- [Theme.of], which returns the current overall Material theme as a [ThemeData].
- [ThemeData.colorScheme], the thirteen colors that most Material widget default colors are based on.
- [ColorScheme.brightness], which indicates if the overall [Theme] is light or dark.

### iconTheme

```dart
IconThemeData? iconTheme
```

{@template flutter.material.appbar.iconTheme} The color, opacity, and size to use for toolbar icons.

If this property is null, then a copy of [ThemeData.iconTheme] is used, with the [IconThemeData.color] set to the app bar's [foregroundColor]. {@endtemplate}

See also:

- [actionsIconTheme], which defines the appearance of icons in the [actions] list.

### actionsIconTheme

```dart
IconThemeData? actionsIconTheme
```

{@template flutter.material.appbar.actionsIconTheme} The color, opacity, and size to use for the icons that appear in the app bar's [actions].

This property should only be used when the [actions] should be themed differently than the icon that appears in the app bar's [leading] widget.

If this property is null, then the ambient [AppBarThemeData.actionsIconTheme] is used. If that is also null, then the value of [iconTheme] is used. {@endtemplate}

See also:

- [iconTheme], which defines the appearance of all of the toolbar icons.

### primary

```dart
bool primary
```

{@template flutter.material.appbar.primary} Whether this app bar is being displayed at the top of the screen.

If true, the app bar's toolbar elements and [bottom] widget will be padded on top by the height of the system status bar. The layout of the [flexibleSpace] is not affected by the [primary] property. {@endtemplate}

### centerTitle

```dart
bool? centerTitle
```

{@template flutter.material.appbar.centerTitle} Whether the title should be centered.

If this property is null, then [AppBarTheme.centerTitle] of [ThemeData.appBarTheme] is used. If that is also null, then value is adapted to the current [TargetPlatform]. {@endtemplate}

### excludeHeaderSemantics

```dart
bool excludeHeaderSemantics
```

{@template flutter.material.appbar.excludeHeaderSemantics} Whether the title should be wrapped with header [Semantics].

If false, the title will be used as [SemanticsProperties.namesRoute] for Android, Fuchsia, Linux, and Windows platform. This means the title is announced by screen reader when transition to this route.

The accessibility behavior is platform adaptive, based on the device's actual platform rather than the theme's platform setting. This ensures that assistive technologies like VoiceOver on iOS and macOS receive the correct `namesRoute` semantic information, even when the app's theme is configured to mimic a different platform's appearance.

Defaults to false. {@endtemplate}

### titleSpacing

```dart
double? titleSpacing
```

{@template flutter.material.appbar.titleSpacing} The spacing around [title] content on the horizontal axis. This spacing is applied even if there is no [leading] content or [actions]. If you want [title] to take all the space available, set this value to 0.0.

If this property is null, then [AppBarTheme.titleSpacing] of [ThemeData.appBarTheme] is used. If that is also null, then the default value is [NavigationToolbar.kMiddleSpacing]. {@endtemplate}

### toolbarOpacity

```dart
double toolbarOpacity
```

{@template flutter.material.appbar.toolbarOpacity} How opaque the toolbar part of the app bar is.

A value of 1.0 is fully opaque, and a value of 0.0 is fully transparent.

Typically, this value is not changed from its default value (1.0). It is used by [SliverAppBar] to animate the opacity of the toolbar when the app bar is scrolled. {@endtemplate}

### bottomOpacity

```dart
double bottomOpacity
```

{@template flutter.material.appbar.bottomOpacity} How opaque the bottom part of the app bar is.

A value of 1.0 is fully opaque, and a value of 0.0 is fully transparent.

Typically, this value is not changed from its default value (1.0). It is used by [SliverAppBar] to animate the opacity of the toolbar when the app bar is scrolled. {@endtemplate}

### preferredSize

```dart
Size preferredSize
```

{@template flutter.material.appbar.preferredSize} A size whose height is the sum of [toolbarHeight] and the [bottom] widget's preferred height.

[Scaffold] uses this size to set its app bar's height. {@endtemplate}

### toolbarHeight

```dart
double? toolbarHeight
```

{@template flutter.material.appbar.toolbarHeight} Defines the height of the toolbar component of an [AppBar].

By default, the value of [toolbarHeight] is [kToolbarHeight]. {@endtemplate}

### leadingWidth

```dart
double? leadingWidth
```

{@template flutter.material.appbar.leadingWidth} Defines the width of [AppBar.leading] widget.

By default, the value of [AppBar.leadingWidth] is 56.0. {@endtemplate}

### toolbarTextStyle

```dart
TextStyle? toolbarTextStyle
```

{@template flutter.material.appbar.toolbarTextStyle} The default text style for the AppBar's [leading], and [actions] widgets, but not its [title].

If this property is null, then [AppBarTheme.toolbarTextStyle] of [ThemeData.appBarTheme] is used. If that is also null, the default value is a copy of the overall theme's [TextTheme.bodyMedium] [TextStyle], with color set to the app bar's [foregroundColor]. {@endtemplate}

See also:

- [titleTextStyle], which overrides the default text style for the [title].
- [DefaultTextStyle], which overrides the default text style for all of the widgets in a subtree.

### titleTextStyle

```dart
TextStyle? titleTextStyle
```

{@template flutter.material.appbar.titleTextStyle} The default text style for the AppBar's [title] widget.

If this property is null, then [AppBarTheme.titleTextStyle] of [ThemeData.appBarTheme] is used. If that is also null, the default value is a copy of the overall theme's [TextTheme.titleLarge] [TextStyle], with color set to the app bar's [foregroundColor]. {@endtemplate}

See also:

- [toolbarTextStyle], which is the default text style for the AppBar's [title], [leading], and [actions] widgets, also known as the AppBar's "toolbar".
- [DefaultTextStyle], which overrides the default text style for all of the widgets in a subtree.

### systemOverlayStyle

```dart
SystemUiOverlayStyle? systemOverlayStyle
```

{@template flutter.material.appbar.systemOverlayStyle} Specifies the style to use for the system overlays (e.g. the status bar on Android or iOS, the system navigation bar on Android).

If this property is null, then [AppBarTheme.systemOverlayStyle] of [ThemeData.appBarTheme] is used. If that is also null, an appropriate [SystemUiOverlayStyle] is calculated based on the [backgroundColor].

The AppBar's descendants are built within a `AnnotatedRegion<SystemUiOverlayStyle>` widget, which causes [SystemChrome.setSystemUIOverlayStyle] to be called automatically. Apps should not enclose an AppBar with their own [AnnotatedRegion]. {@endtemplate}

See also:

- [AnnotatedRegion], for placing [SystemUiOverlayStyle] in the layer tree.
- [SystemChrome.setSystemUIOverlayStyle], the imperative API for setting system overlays style.

### forceMaterialTransparency

```dart
bool forceMaterialTransparency
```

{@template flutter.material.appbar.forceMaterialTransparency} Forces the AppBar's Material widget type to be [MaterialType.transparency] (instead of Material's default type).

This will remove the visual display of [backgroundColor] and [elevation], and affect other characteristics of the AppBar's Material widget.

Provided for cases where the app bar is to be transparent, and gestures must pass through the app bar to widgets beneath the app bar (i.e. with [Scaffold.extendBodyBehindAppBar] set to true).

Defaults to false. {@endtemplate}

### useDefaultSemanticsOrder

```dart
bool useDefaultSemanticsOrder
```

{@template flutter.material.appbar.useDefaultSemanticsOrder} Whether to use the default semantic ordering for the app bar's children for accessibility traversal order.

If this is set to true, the app bar will use the default semantic ordering, which places the flexible space after the main content in the semantics tree. This affects how screen readers and other assistive technologies navigate the app bar's content.

Set this to false if you want to customize semantics traversal order in the app bar. You can then assign [SemanticsSortKey]s to app bar's children to control the order.

Defaults to true.

See also:

- [SemanticsSortKey], which are keys used to define the accessibility traversal order. {@endtemplate}

### clipBehavior

```dart
Clip? clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

### actionsPadding

```dart
EdgeInsetsGeometry? actionsPadding
```

{@template flutter.material.appbar.actionsPadding} The padding between the [actions] and the end of the AppBar.

Defaults to zero. {@endtemplate}

### animateColor

```dart
bool animateColor
```

Whether the color should be animated.

### createState()

```dart
State<AppBar> createState()
```

# SliverAppBar

```dart
class SliverAppBar extends StatefulWidget {}
```

A Material Design app bar that integrates with a [CustomScrollView].

An app bar consists of a toolbar and potentially other widgets, such as a [TabBar] and a [FlexibleSpaceBar]. App bars typically expose one or more common actions with [IconButton]s which are optionally followed by a [PopupMenuButton] for less common operations.

{@youtube 560 315 https://www.youtube.com/watch?v=R9C5KMJKluE}

Sliver app bars are typically used as the first child of a [CustomScrollView], which lets the app bar integrate with the scroll view so that it can vary in height according to the scroll offset or float above the other content in the scroll view. For a fixed-height app bar at the top of the screen see [AppBar], which is used in the [Scaffold.appBar] slot.

The AppBar displays the toolbar widgets, [leading], [title], and [actions], above the [bottom] (if any). If a [flexibleSpace] widget is specified then it is stacked behind the toolbar and the bottom widget.

{@tool snippet}

This is an example that could be included in a [CustomScrollView]'s [CustomScrollView.slivers] list:

```dart
SliverAppBar(
  expandedHeight: 150.0,
  flexibleSpace: const FlexibleSpaceBar(
    title: Text('Available seats'),
  ),
  actions: <Widget>[
    IconButton(
      icon: const Icon(Icons.add_circle),
      tooltip: 'Add new entry',
      onPressed: () { /* ... */ },
    ),
  ]
)
```

{@end-tool}

{@tool dartpad} Here is an example of [SliverAppBar] when using [stretch] and [onStretchTrigger].

** See code in examples/api/lib/material/app_bar/sliver_app_bar.4.dart ** {@end-tool}

{@tool dartpad} This sample shows a [SliverAppBar] and its behavior when using the [pinned], [snap] and [floating] parameters.

** See code in examples/api/lib/material/app_bar/sliver_app_bar.1.dart ** {@end-tool}

## Animated Examples

The following animations show how app bars with different configurations behave when a user scrolls up and then down again.

- App bar with [floating]: false, [pinned]: false, [snap]: false: {@animation 476 400 https://flutter.github.io/assets-for-api-docs/assets/material/app_bar.mp4}

- App bar with [floating]: true, [pinned]: false, [snap]: false: {@animation 476 400 https://flutter.github.io/assets-for-api-docs/assets/material/app_bar_floating.mp4}

- App bar with [floating]: true, [pinned]: false, [snap]: true: {@animation 476 400 https://flutter.github.io/assets-for-api-docs/assets/material/app_bar_floating_snap.mp4}

- App bar with [floating]: true, [pinned]: true, [snap]: false: {@animation 476 400 https://flutter.github.io/assets-for-api-docs/assets/material/app_bar_pinned_floating.mp4}

- App bar with [floating]: true, [pinned]: true, [snap]: true: {@animation 476 400 https://flutter.github.io/assets-for-api-docs/assets/material/app_bar_pinned_floating_snap.mp4}

- App bar with [floating]: false, [pinned]: true, [snap]: false: {@animation 476 400 https://flutter.github.io/assets-for-api-docs/assets/material/app_bar_pinned.mp4}

The property [snap] can only be set to true if [floating] is also true.

See also:

- [CustomScrollView], which integrates the [SliverAppBar] into its scrolling.
- [AppBar], which is a fixed-height app bar for use in [Scaffold.appBar].
- [TabBar], which is typically placed in the [bottom] slot of the [AppBar] if the screen has multiple pages arranged in tabs.
- [IconButton], which is used with [actions] to show buttons on the app bar.
- [PopupMenuButton], to show a popup menu on the app bar, via [actions].
- [FlexibleSpaceBar], which is used with [flexibleSpace] when the app bar can expand and collapse.
- <https://material.io/design/components/app-bars-top.html>

### SliverAppBar()

```dart
SliverAppBar({dynamic key, Widget? leading, bool automaticallyImplyLeading = true, Widget? title, List<Widget>? actions, bool automaticallyImplyActions = true, Widget? flexibleSpace, PreferredSizeWidget? bottom, double? elevation, double? scrolledUnderElevation, Color? shadowColor, Color? surfaceTintColor, bool forceElevated = false, Color? backgroundColor, Color? foregroundColor, IconThemeData? iconTheme, IconThemeData? actionsIconTheme, bool primary = true, bool? centerTitle, bool excludeHeaderSemantics = false, double? titleSpacing, double? collapsedHeight, double? expandedHeight, bool floating = false, bool pinned = false, bool snap = false, bool stretch = false, double stretchTriggerOffset = 100.0, AsyncCallback? onStretchTrigger, ShapeBorder? shape, double toolbarHeight = kToolbarHeight, double? leadingWidth, TextStyle? toolbarTextStyle, TextStyle? titleTextStyle, SystemUiOverlayStyle? systemOverlayStyle, bool forceMaterialTransparency = false, bool useDefaultSemanticsOrder = true, Clip? clipBehavior, EdgeInsetsGeometry? actionsPadding})
```

Creates a Material Design app bar that can be placed in a [CustomScrollView].

### SliverAppBar.medium()

```dart
SliverAppBar.medium({dynamic key, Widget? leading, bool automaticallyImplyLeading = true, Widget? title, List<Widget>? actions, bool automaticallyImplyActions = true, Widget? flexibleSpace, PreferredSizeWidget? bottom, double? elevation, double? scrolledUnderElevation, Color? shadowColor, Color? surfaceTintColor, bool forceElevated = false, Color? backgroundColor, Color? foregroundColor, IconThemeData? iconTheme, IconThemeData? actionsIconTheme, bool primary = true, bool? centerTitle, bool excludeHeaderSemantics = false, double? titleSpacing, double? collapsedHeight, double? expandedHeight, bool floating = false, bool pinned = true, bool snap = false, bool stretch = false, double stretchTriggerOffset = 100.0, AsyncCallback? onStretchTrigger, ShapeBorder? shape, double toolbarHeight = _MediumScrollUnderFlexibleConfig.collapsedHeight, double? leadingWidth, TextStyle? toolbarTextStyle, TextStyle? titleTextStyle, SystemUiOverlayStyle? systemOverlayStyle, bool forceMaterialTransparency = false, bool useDefaultSemanticsOrder = true, Clip? clipBehavior, EdgeInsetsGeometry? actionsPadding})
```

Creates a Material Design medium top app bar that can be placed in a [CustomScrollView].

Returns a [SliverAppBar] configured with appropriate defaults for a medium top app bar as defined in Material 3. It starts fully expanded with the title in an area underneath the main row of icons. When the [CustomScrollView] is scrolled, the title will be scrolled under the main row. When it is fully collapsed, a smaller version of the title will fade in on the main row. The reverse will happen if it is expanded again.

{@tool dartpad} This sample shows how to use [SliverAppBar.medium] in a [CustomScrollView].

** See code in examples/api/lib/material/app_bar/sliver_app_bar.2.dart ** {@end-tool}

See also:

- [AppBar], for a small or center-aligned top app bar.
- [SliverAppBar.large], for a large top app bar.
- https://m3.material.io/components/top-app-bar/overview, the Material 3 app bar specification.

### SliverAppBar.large()

```dart
SliverAppBar.large({dynamic key, Widget? leading, bool automaticallyImplyLeading = true, Widget? title, List<Widget>? actions, bool automaticallyImplyActions = true, Widget? flexibleSpace, PreferredSizeWidget? bottom, double? elevation, double? scrolledUnderElevation, Color? shadowColor, Color? surfaceTintColor, bool forceElevated = false, Color? backgroundColor, Color? foregroundColor, IconThemeData? iconTheme, IconThemeData? actionsIconTheme, bool primary = true, bool? centerTitle, bool excludeHeaderSemantics = false, double? titleSpacing, double? collapsedHeight, double? expandedHeight, bool floating = false, bool pinned = true, bool snap = false, bool stretch = false, double stretchTriggerOffset = 100.0, AsyncCallback? onStretchTrigger, ShapeBorder? shape, double toolbarHeight = _LargeScrollUnderFlexibleConfig.collapsedHeight, double? leadingWidth, TextStyle? toolbarTextStyle, TextStyle? titleTextStyle, SystemUiOverlayStyle? systemOverlayStyle, bool forceMaterialTransparency = false, bool useDefaultSemanticsOrder = true, Clip? clipBehavior, EdgeInsetsGeometry? actionsPadding})
```

Creates a Material Design large top app bar that can be placed in a [CustomScrollView].

Returns a [SliverAppBar] configured with appropriate defaults for a large top app bar as defined in Material 3. It starts fully expanded with the title in an area underneath the main row of icons. When the [CustomScrollView] is scrolled, the title will be scrolled under the main row. When it is fully collapsed, a smaller version of the title will fade in on the main row. The reverse will happen if it is expanded again.

{@tool dartpad} This sample shows how to use [SliverAppBar.large] in a [CustomScrollView].

** See code in examples/api/lib/material/app_bar/sliver_app_bar.3.dart ** {@end-tool}

See also:

- [AppBar], for a small or center-aligned top app bar.
- [SliverAppBar.medium], for a medium top app bar.
- https://m3.material.io/components/top-app-bar/overview, the Material 3 app bar specification.

### leading

```dart
Widget? leading
```

{@macro flutter.material.appbar.leading}

This property is used to configure an [AppBar].

### automaticallyImplyLeading

```dart
bool automaticallyImplyLeading
```

{@macro flutter.material.appbar.automaticallyImplyLeading}

This property is used to configure an [AppBar].

### title

```dart
Widget? title
```

{@macro flutter.material.appbar.title}

This property is used to configure an [AppBar].

### actions

```dart
List<Widget>? actions
```

{@macro flutter.material.appbar.actions}

This property is used to configure an [AppBar].

### automaticallyImplyActions

```dart
bool automaticallyImplyActions
```

{@macro flutter.material.appbar.automaticallyImplyActions}

This property is used to configure an [AppBar].

### flexibleSpace

```dart
Widget? flexibleSpace
```

{@macro flutter.material.appbar.flexibleSpace}

This property is used to configure an [AppBar].

### bottom

```dart
PreferredSizeWidget? bottom
```

{@macro flutter.material.appbar.bottom}

This property is used to configure an [AppBar].

### elevation

```dart
double? elevation
```

{@macro flutter.material.appbar.elevation}

This property is used to configure an [AppBar].

### scrolledUnderElevation

```dart
double? scrolledUnderElevation
```

{@macro flutter.material.appbar.scrolledUnderElevation}

This property is used to configure an [AppBar].

### shadowColor

```dart
Color? shadowColor
```

{@macro flutter.material.appbar.shadowColor}

This property is used to configure an [AppBar].

### surfaceTintColor

```dart
Color? surfaceTintColor
```

{@macro flutter.material.appbar.surfaceTintColor}

This property is used to configure an [AppBar].

### forceElevated

```dart
bool forceElevated
```

Whether to show the shadow appropriate for the [elevation] even if the content is not scrolled under the [AppBar].

Defaults to false, meaning that the [elevation] is only applied when the [AppBar] is being displayed over content that is scrolled under it.

When set to true, the [elevation] is applied regardless.

Ignored when [elevation] is zero.

### backgroundColor

```dart
Color? backgroundColor
```

{@macro flutter.material.appbar.backgroundColor}

This property is used to configure an [AppBar].

### foregroundColor

```dart
Color? foregroundColor
```

{@macro flutter.material.appbar.foregroundColor}

This property is used to configure an [AppBar].

### iconTheme

```dart
IconThemeData? iconTheme
```

{@macro flutter.material.appbar.iconTheme}

This property is used to configure an [AppBar].

### actionsIconTheme

```dart
IconThemeData? actionsIconTheme
```

{@macro flutter.material.appbar.actionsIconTheme}

This property is used to configure an [AppBar].

### primary

```dart
bool primary
```

{@macro flutter.material.appbar.primary}

This property is used to configure an [AppBar].

### centerTitle

```dart
bool? centerTitle
```

{@macro flutter.material.appbar.centerTitle}

This property is used to configure an [AppBar].

### excludeHeaderSemantics

```dart
bool excludeHeaderSemantics
```

{@macro flutter.material.appbar.excludeHeaderSemantics}

This property is used to configure an [AppBar].

### titleSpacing

```dart
double? titleSpacing
```

{@macro flutter.material.appbar.titleSpacing}

This property is used to configure an [AppBar].

### collapsedHeight

```dart
double? collapsedHeight
```

Defines the height of the app bar when it is collapsed.

By default, the collapsed height is [toolbarHeight]. If [bottom] widget is specified, then its height from [PreferredSizeWidget.preferredSize] is added to the height. If [primary] is true, then the [MediaQuery] top padding, [EdgeInsets.top] of [MediaQueryData.padding], is added as well.

If [pinned] and [floating] are true, with [bottom] set, the default collapsed height is only the height of [PreferredSizeWidget.preferredSize] with the [MediaQuery] top padding.

### expandedHeight

```dart
double? expandedHeight
```

The size of the app bar when it is fully expanded.

By default, the total height of the toolbar and the bottom widget (if any). If a [flexibleSpace] widget is specified this height should be big enough to accommodate whatever that widget contains.

This does not include the status bar height (which will be automatically included if [primary] is true).

### floating

```dart
bool floating
```

Whether the app bar should become visible as soon as the user scrolls towards the app bar.

Otherwise, the user will need to scroll near the top of the scroll view to reveal the app bar.

If [snap] is true then a scroll that exposes the app bar will trigger an animation that slides the entire app bar into view. Similarly if a scroll dismisses the app bar, the animation will slide it completely out of view.

## Animated Examples

The following animations show how the app bar changes its scrolling behavior based on the value of this property.

- App bar with [floating] set to false: {@animation 476 400 https://flutter.github.io/assets-for-api-docs/assets/material/app_bar.mp4}
- App bar with [floating] set to true: {@animation 476 400 https://flutter.github.io/assets-for-api-docs/assets/material/app_bar_floating.mp4}

See also:

- [SliverAppBar] for more animated examples of how this property changes the behavior of the app bar in combination with [pinned] and [snap].

### pinned

```dart
bool pinned
```

Whether the app bar should remain visible at the start of the scroll view.

The app bar can still expand and contract as the user scrolls, but it will remain visible rather than being scrolled out of view.

## Animated Examples

The following animations show how the app bar changes its scrolling behavior based on the value of this property.

- App bar with [pinned] set to false: {@animation 476 400 https://flutter.github.io/assets-for-api-docs/assets/material/app_bar.mp4}
- App bar with [pinned] set to true: {@animation 476 400 https://flutter.github.io/assets-for-api-docs/assets/material/app_bar_pinned.mp4}

See also:

- [SliverAppBar] for more animated examples of how this property changes the behavior of the app bar in combination with [floating].

### shape

```dart
ShapeBorder? shape
```

{@macro flutter.material.appbar.shape}

This property is used to configure an [AppBar].

### snap

```dart
bool snap
```

If [snap] and [floating] are true then the floating app bar will "snap" into view.

If [snap] is true then a scroll that exposes the floating app bar will trigger an animation that slides the entire app bar into view. Similarly if a scroll dismisses the app bar, the animation will slide the app bar completely out of view. Additionally, setting [snap] to true will fully expand the floating app bar when the framework tries to reveal the contents of the app bar by calling [RenderObject.showOnScreen]. For example, when a [TextField] in the floating app bar gains focus, if [snap] is true, the framework will always fully expand the floating app bar, in order to reveal the focused [TextField].

Snapping only applies when the app bar is floating, not when the app bar appears at the top of its scroll view.

## Animated Examples

The following animations show how the app bar changes its scrolling behavior based on the value of this property.

- App bar with [snap] set to false: {@animation 476 400 https://flutter.github.io/assets-for-api-docs/assets/material/app_bar_floating.mp4}
- App bar with [snap] set to true: {@animation 476 400 https://flutter.github.io/assets-for-api-docs/assets/material/app_bar_floating_snap.mp4}

See also:

- [SliverAppBar] for more animated examples of how this property changes the behavior of the app bar in combination with [pinned] and [floating].

### stretch

```dart
bool stretch
```

Whether the app bar should stretch to fill the over-scroll area.

The app bar can still expand and contract as the user scrolls, but it will also stretch when the user over-scrolls.

### stretchTriggerOffset

```dart
double stretchTriggerOffset
```

The offset of overscroll required to activate [onStretchTrigger].

This defaults to 100.0.

### onStretchTrigger

```dart
AsyncCallback? onStretchTrigger
```

The callback function to be executed when a user over-scrolls to the offset specified by [stretchTriggerOffset].

### toolbarHeight

```dart
double toolbarHeight
```

{@macro flutter.material.appbar.toolbarHeight}

This property is used to configure an [AppBar].

### leadingWidth

```dart
double? leadingWidth
```

{@macro flutter.material.appbar.leadingWidth}

This property is used to configure an [AppBar].

### toolbarTextStyle

```dart
TextStyle? toolbarTextStyle
```

{@macro flutter.material.appbar.toolbarTextStyle}

This property is used to configure an [AppBar].

### titleTextStyle

```dart
TextStyle? titleTextStyle
```

{@macro flutter.material.appbar.titleTextStyle}

This property is used to configure an [AppBar].

### systemOverlayStyle

```dart
SystemUiOverlayStyle? systemOverlayStyle
```

{@macro flutter.material.appbar.systemOverlayStyle}

This property is used to configure an [AppBar].

### forceMaterialTransparency

```dart
bool forceMaterialTransparency
```

{@macro flutter.material.appbar.forceMaterialTransparency}

This property is used to configure an [AppBar].

### useDefaultSemanticsOrder

```dart
bool useDefaultSemanticsOrder
```

{@macro flutter.material.appbar.useDefaultSemanticsOrder}

This property is used to configure an [AppBar].

### clipBehavior

```dart
Clip? clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

### actionsPadding

```dart
EdgeInsetsGeometry? actionsPadding
```

{@macro flutter.material.appbar.actionsPadding}

This property is used to configure an [AppBar].

### createState()

```dart
State<SliverAppBar> createState()
```
