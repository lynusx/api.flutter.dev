@docImport 'no_splash.dart';

# TabBarIndicatorSize

```dart
enum TabBarIndicatorSize {}
```

Defines how the bounds of the selected tab indicator are computed.

See also:

- [TabBar], which displays a row of tabs.
- [TabBarView], which displays a widget for the currently selected tab.
- [TabBar.indicator], which defines the appearance of the selected tab indicator relative to the tab's bounds.

The tab indicator's bounds are as wide as the space occupied by the tab in the tab bar: from the right edge of the previous tab to the left edge of the next tab.

The tab's bounds are only as wide as the (centered) tab widget itself.

This value is used to align the tab's label, typically a [Tab] widget's text or icon, with the selected tab indicator.

# TabAlignment

```dart
enum TabAlignment {}
```

Defines how tabs are aligned horizontally in a [TabBar].

See also:

- [TabBar], which displays a row of tabs.
- [TabBarView], which displays a widget for the currently selected tab.
- [TabBar.tabAlignment], which defines the horizontal alignment of the tabs within the [TabBar].

If [TabBar.isScrollable] is true, tabs are aligned to the start of the [TabBar]. Otherwise throws an exception.

It is not recommended to set [TabAlignment.start] when [ThemeData.useMaterial3] is false.

If [TabBar.isScrollable] is true, tabs are aligned to the start of the [TabBar] with an offset of 52.0 pixels. Otherwise throws an exception.

It is not recommended to set [TabAlignment.startOffset] when [ThemeData.useMaterial3] is false.

If [TabBar.isScrollable] is false, tabs are stretched to fill the [TabBar]. Otherwise throws an exception.

Tabs are aligned to the center of the [TabBar].

# TabIndicatorAnimation

```dart
enum TabIndicatorAnimation {}
```

Defines how the tab indicator animates when the selected tab changes.

See also:

- [TabBar], which displays a row of tabs.
- [TabBarThemeData], which can be used to configure the appearance of the tab indicator.

The tab indicator animates linearly.

The tab indicator animates with an elastic effect.

# Tab

```dart
class Tab extends StatelessWidget implements PreferredSizeWidget {}
```

A Material Design [TabBar] tab.

If both [icon] and [text] are provided, the text is displayed below the icon.

See also:

- [TabBar], which displays a row of tabs.
- [TabBarView], which displays a widget for the currently selected tab.
- [TabController], which coordinates tab selection between a [TabBar] and a [TabBarView].
- <https://material.io/design/components/tabs.html>

### Tab()

```dart
Tab({dynamic key, String? text, Widget? icon, EdgeInsetsGeometry? iconMargin, double? height, Widget? child})
```

Creates a Material Design [TabBar] tab.

At least one of [text], [icon], and [child] must be non-null. The [text] and [child] arguments must not be used at the same time. The [iconMargin] is only useful when [icon] and either one of [text] or [child] is non-null.

### text

```dart
String? text
```

The text to display as the tab's label.

Must not be used in combination with [child].

### child

```dart
Widget? child
```

The widget to be used as the tab's label.

Usually a [Text] widget, possibly wrapped in a [Semantics] widget.

Must not be used in combination with [text].

### icon

```dart
Widget? icon
```

An icon to display as the tab's label.

### iconMargin

```dart
EdgeInsetsGeometry? iconMargin
```

The margin added around the tab's icon.

Only useful when used in combination with [icon], and either one of [text] or [child] is non-null.

Defaults to 2 pixels of bottom margin. If [ThemeData.useMaterial3] is false, then defaults to 10 pixels of bottom margin.

### height

```dart
double? height
```

The height of the [Tab].

If null, the height will be calculated based on the content of the [Tab]. When `icon` is not null along with `child` or `text`, the default height is 72.0 pixels. Without an `icon`, the height is 46.0 pixels.

{@tool snippet}

The provided tab height cannot be lower than the default height. Use [PreferredSize] widget to adjust the overall [TabBar] height and match the provided tab [height]:

```dart
bottom: const PreferredSize(
  preferredSize: Size.fromHeight(20.0),
  child: TabBar(
    tabs: <Widget>[
      Tab(
        text: 'Tab 1',
        height: 20.0,
      ),
      Tab(
        text: 'Tab 2',
        height: 20.0,
      ),
    ],
  ),
),
```

{@end-tool}

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### preferredSize

```dart
Size get preferredSize
```

# TabBarScrollController

```dart
final class TabBarScrollController extends ScrollController {}
```

The [ScrollController] for a [TabBar] widget.

### debugCheckHasTabBarState()

```dart
bool debugCheckHasTabBarState()
```

Asserts that this controller is currently attached to a [TabBar]'s [State].

To invoke this function, wrap it in an assert: `assert(debugCheckHasTabBarState());`

Does nothing if asserts are disabled. Always returns true.

### createScrollPosition()

```dart
ScrollPosition createScrollPosition(ScrollPhysics physics, ScrollContext context, ScrollPosition? oldPosition)
```

### dispose()

```dart
void dispose()
```

# TabValueChanged

```dart
typedef TabValueChanged<T> = void Function(T value, int index)
```

Signature for [TabBar] callbacks that report that an underlying value has changed for a given [Tab] at `index`.

Used for [TabBar.onHover] and [TabBar.onFocusChange] callbacks The provided `value` being true indicates focus has been gained, or a pointer has hovered over the tab, with false indicated focus has been lost or the pointer has exited hovering.

# TabBar

```dart
class TabBar extends StatefulWidget implements PreferredSizeWidget {}
```

A Material Design primary tab bar.

Primary tabs are placed at the top of the content pane under a top app bar. They display the main content destinations.

Typically created as the [AppBar.bottom] part of an [AppBar] and in conjunction with a [TabBarView].

{@youtube 560 315 https://www.youtube.com/watch?v=POtoEH-5l40}

If a [TabController] is not provided, then a [DefaultTabController] ancestor must be provided instead. The tab controller's [TabController.length] must equal the length of the [tabs] list and the length of the [TabBarView.children] list.

Requires one of its ancestors to be a [Material] widget.

Uses values from [TabBarThemeData] if it is set in the current context.

{@tool dartpad} This sample shows the implementation of [TabBar] and [TabBarView] using a [DefaultTabController]. Each [Tab] corresponds to a child of the [TabBarView] in the order they are written.

** See code in examples/api/lib/material/tabs/tab_bar.0.dart ** {@end-tool}

{@tool dartpad} [TabBar] can also be implemented by using a [TabController] which provides more options to control the behavior of the [TabBar] and [TabBarView]. This can be used instead of a [DefaultTabController], demonstrated below.

** See code in examples/api/lib/material/tabs/tab_bar.1.dart ** {@end-tool}

{@tool dartpad} This sample showcases nested Material 3 [TabBar]s. It consists of a primary [TabBar] with nested a secondary [TabBar]. The primary [TabBar] uses a [DefaultTabController] while the secondary [TabBar] uses a [TabController].

** See code in examples/api/lib/material/tabs/tab_bar.2.dart ** {@end-tool}

{@tool dartpad} This sample showcases how to apply custom behavior based on the scroll in [TabBar]. It utilizes scroll notifications ([ScrollMetricsNotification] and [ScrollNotification]) within [NotificationListener] callback to monitor the scroll offset, allowing for interface customization based on the obtained offset.

** See code in examples/api/lib/material/tabs/tab_bar.3.dart ** {@end-tool}

See also:

- [TabBar.secondary], for a secondary tab bar.
- [TabBarView], which displays page views that correspond to each tab.
- [TabController], which coordinates tab selection between a [TabBar] and a [TabBarView].
- https://m3.material.io/components/tabs/overview, the Material 3 tab bar specification.

### TabBar()

```dart
TabBar({dynamic key, required List<Widget> tabs, TabController? controller, TabBarScrollController? scrollController, bool isScrollable = false, EdgeInsetsGeometry? padding, Color? indicatorColor, bool automaticIndicatorColorAdjustment = true, double indicatorWeight = 2.0, EdgeInsetsGeometry indicatorPadding = EdgeInsets.zero, Decoration? indicator, TabBarIndicatorSize? indicatorSize, Color? dividerColor, double? dividerHeight, Color? labelColor, TextStyle? labelStyle, EdgeInsetsGeometry? labelPadding, Color? unselectedLabelColor, TextStyle? unselectedLabelStyle, DragStartBehavior dragStartBehavior = DragStartBehavior.start, WidgetStateProperty<Color?>? overlayColor, MouseCursor? mouseCursor, bool? enableFeedback, ValueChanged<int>? onTap, TabValueChanged<bool>? onHover, TabValueChanged<bool>? onFocusChange, ScrollPhysics? physics, InteractiveInkFeatureFactory? splashFactory, BorderRadius? splashBorderRadius, TabAlignment? tabAlignment, TextScaler? textScaler, TabIndicatorAnimation? indicatorAnimation})
```

Creates a Material Design primary tab bar.

The length of the [tabs] argument must match the [controller]'s [TabController.length].

If a [TabController] is not provided, then there must be a [DefaultTabController] ancestor.

The [indicatorWeight] parameter defaults to 2.

The [indicatorPadding] parameter defaults to [EdgeInsets.zero].

If [indicator] is not null or provided from [TabBarTheme], then [indicatorColor] is ignored.

The [indicatorWeight] does not affect the visual appearance of the indicator when a custom [indicator] is provided. However, it may still be used to compute the TabBar's preferred size.

### TabBar.secondary()

```dart
TabBar.secondary({dynamic key, required List<Widget> tabs, TabController? controller, TabBarScrollController? scrollController, bool isScrollable = false, EdgeInsetsGeometry? padding, Color? indicatorColor, bool automaticIndicatorColorAdjustment = true, double indicatorWeight = 2.0, EdgeInsetsGeometry indicatorPadding = EdgeInsets.zero, Decoration? indicator, TabBarIndicatorSize? indicatorSize, Color? dividerColor, double? dividerHeight, Color? labelColor, TextStyle? labelStyle, EdgeInsetsGeometry? labelPadding, Color? unselectedLabelColor, TextStyle? unselectedLabelStyle, DragStartBehavior dragStartBehavior = DragStartBehavior.start, WidgetStateProperty<Color?>? overlayColor, MouseCursor? mouseCursor, bool? enableFeedback, ValueChanged<int>? onTap, TabValueChanged<bool>? onHover, TabValueChanged<bool>? onFocusChange, ScrollPhysics? physics, InteractiveInkFeatureFactory? splashFactory, BorderRadius? splashBorderRadius, TabAlignment? tabAlignment, TextScaler? textScaler, TabIndicatorAnimation? indicatorAnimation})
```

Creates a Material Design secondary tab bar.

Secondary tabs are used within a content area to further separate related content and establish hierarchy.

{@tool dartpad} This sample showcases nested Material 3 [TabBar]s. It consists of a primary [TabBar] with nested a secondary [TabBar]. The primary [TabBar] uses a [DefaultTabController] while the secondary [TabBar] uses a [TabController].

** See code in examples/api/lib/material/tabs/tab_bar.2.dart ** {@end-tool}

See also:

- [TabBar], for a primary tab bar.
- [TabBarView], which displays page views that correspond to each tab.
- [TabController], which coordinates tab selection between a [TabBar] and a [TabBarView].
- https://m3.material.io/components/tabs/overview, the Material 3 tab bar specification.

### tabs

```dart
List<Widget> tabs
```

Typically a list of two or more [Tab] widgets.

The length of this list must match the [controller]'s [TabController.length] and the length of the [TabBarView.children] list.

### controller

```dart
TabController? controller
```

This widget's selection and animation state.

If [TabController] is not provided, then the value of [DefaultTabController.of] will be used.

### scrollController

```dart
TabBarScrollController? scrollController
```

The [TabBarScrollController] for this [TabBar].

This controller can be used to manipulate the scroll position of the [TabBar].

### isScrollable

```dart
bool isScrollable
```

Whether this tab bar can be scrolled horizontally.

If [isScrollable] is true, then each tab is as wide as needed for its label and the entire [TabBar] is scrollable. Otherwise each tab gets an equal share of the available space.

### padding

```dart
EdgeInsetsGeometry? padding
```

The amount of space by which to inset the tab bar.

When [isScrollable] is false, this will yield the same result as if [TabBar] was wrapped in a [Padding] widget. When [isScrollable] is true, the scrollable itself is inset, allowing the padding to scroll with the tab bar, rather than enclosing it.

### indicatorColor

```dart
Color? indicatorColor
```

The color of the line that appears below the selected tab.

If this parameter is null, then the value of the Theme's indicatorColor property is used.

If [indicator] is specified or provided from [TabBarThemeData], this property is ignored.

### indicatorWeight

```dart
double indicatorWeight
```

The thickness of the line that appears below the selected tab.

The value of this parameter must be greater than zero.

If [ThemeData.useMaterial3] is true and [TabBar] is used to create a primary tab bar, the default value is 3.0. If the provided value is less than 3.0, the default value is used.

If [ThemeData.useMaterial3] is true and [TabBar.secondary] is used to create a secondary tab bar, the default value is 2.0.

If [ThemeData.useMaterial3] is false, the default value is 2.0.

If [indicator] is specified or provided from [TabBarThemeData], this property is ignored.

### indicatorPadding

```dart
EdgeInsetsGeometry indicatorPadding
```

The padding for the indicator.

The default value of this property is [EdgeInsets.zero].

For [isScrollable] tab bars, specifying [kTabLabelPadding] will align the indicator with the tab's text for [Tab] widgets and all but the shortest [Tab.text] values.

### indicator

```dart
Decoration? indicator
```

Defines the appearance of the selected tab indicator.

If [indicator] is specified or provided from [TabBarThemeData], the [indicatorColor] and [indicatorWeight] properties are ignored.

The default, underline-style, selected tab indicator can be defined with [UnderlineTabIndicator].

The indicator's size is based on the tab's bounds. If [indicatorSize] is [TabBarIndicatorSize.tab] the tab's bounds are as wide as the space occupied by the tab in the tab bar. If [indicatorSize] is [TabBarIndicatorSize.label], then the tab's bounds are only as wide as the tab widget itself.

See also:

- [splashBorderRadius], which defines the clipping radius of the splash and is generally used with [BoxDecoration.borderRadius].

### automaticIndicatorColorAdjustment

```dart
bool automaticIndicatorColorAdjustment
```

Whether this tab bar should automatically adjust the [indicatorColor].

The default value of this property is true.

If [automaticIndicatorColorAdjustment] is true, then the [indicatorColor] will be automatically adjusted to [Colors.white] when the [indicatorColor] is same as [Material.color] of the [Material] parent widget.

### indicatorSize

```dart
TabBarIndicatorSize? indicatorSize
```

Defines how the selected tab indicator's size is computed.

The size of the selected tab indicator is defined relative to the tab's overall bounds if [indicatorSize] is [TabBarIndicatorSize.tab] (the default) or relative to the bounds of the tab's widget if [indicatorSize] is [TabBarIndicatorSize.label].

The selected tab's location appearance can be refined further with the [indicatorColor], [indicatorWeight], [indicatorPadding], and [indicator] properties.

### dividerColor

```dart
Color? dividerColor
```

The color of the divider.

If the [dividerColor] is [Colors.transparent], then the divider will not be drawn.

If null and [ThemeData.useMaterial3] is false, [TabBarThemeData.dividerColor] color is used. If that is null and [ThemeData.useMaterial3] is true, [ColorScheme.outlineVariant] will be used, otherwise divider will not be drawn.

### dividerHeight

```dart
double? dividerHeight
```

The height of the divider.

If the [dividerHeight] is zero or negative, then the divider will not be drawn.

If null and [ThemeData.useMaterial3] is true, [TabBarThemeData.dividerHeight] is used. If that is also null and [ThemeData.useMaterial3] is true, 1.0 will be used. Otherwise divider will not be drawn.

### labelColor

```dart
Color? labelColor
```

The color of selected tab labels.

If null, then [TabBarThemeData.labelColor] is used. If that is also null and [ThemeData.useMaterial3] is true, [ColorScheme.primary] will be used, otherwise the color of the [ThemeData.primaryTextTheme]'s [TextTheme.bodyLarge] text color is used.

If [labelColor] (or, if null, [TabBarThemeData.labelColor]) is a [WidgetStateColor], then the effective tab color will depend on the [WidgetState.selected] state, i.e. if the [Tab] is selected or not, ignoring [unselectedLabelColor] even if it's non-null.

When this color or the [TabBarThemeData.labelColor] is specified, it overrides the [TextStyle.color] specified for the [labelStyle] or the [TabBarThemeData.labelStyle].

See also:

- [unselectedLabelColor], for color of unselected tab labels.

### unselectedLabelColor

```dart
Color? unselectedLabelColor
```

The color of unselected tab labels.

If [labelColor] (or, if null, [TabBarThemeData.labelColor]) is a [WidgetStateColor], then the unselected tabs are rendered with that [WidgetStateColor]'s resolved color for unselected state, even if [unselectedLabelColor] is non-null.

If null, then [TabBarThemeData.unselectedLabelColor] is used. If that is also null and [ThemeData.useMaterial3] is true, [ColorScheme.onSurfaceVariant] will be used, otherwise unselected tab labels are rendered with [labelColor] at 70% opacity.

When this color or the [TabBarThemeData.unselectedLabelColor] is specified, it overrides the [TextStyle.color] specified for the [unselectedLabelStyle] or the [TabBarThemeData.unselectedLabelStyle].

See also:

- [labelColor], for color of selected tab labels.

### labelStyle

```dart
TextStyle? labelStyle
```

The text style of the selected tab labels.

The color specified in [labelStyle] and [TabBarThemeData.labelStyle] is used to style the label when [labelColor] or [TabBarThemeData.labelColor] are not specified.

If [unselectedLabelStyle] is null, then this text style will be used for both selected and unselected label styles.

If this property is null, then [TabBarThemeData.labelStyle] will be used.

If that is also null and [ThemeData.useMaterial3] is true, [TextTheme.titleSmall] will be used, otherwise the text style of the [ThemeData.primaryTextTheme]'s [TextTheme.bodyLarge] definition is used.

### unselectedLabelStyle

```dart
TextStyle? unselectedLabelStyle
```

The text style of the unselected tab labels.

The color specified in [unselectedLabelStyle] and [TabBarThemeData.unselectedLabelStyle] is used to style the label when [unselectedLabelColor] or [TabBarThemeData.unselectedLabelColor] are not specified.

If this property is null, then [TabBarThemeData.unselectedLabelStyle] will be used.

If that is also null and [ThemeData.useMaterial3] is true, [TextTheme.titleSmall] will be used, otherwise then the [labelStyle] value is used. If [labelStyle] is null, the text style of the [ThemeData.primaryTextTheme]'s [TextTheme.bodyLarge] definition is used.

### labelPadding

```dart
EdgeInsetsGeometry? labelPadding
```

The padding added to each of the tab labels.

If there are few tabs with both icon and text and few tabs with only icon or text, this padding is vertically adjusted to provide uniform padding to all tabs.

If this property is null, then [kTabLabelPadding] is used.

### overlayColor

```dart
WidgetStateProperty<Color?>? overlayColor
```

Defines the ink response focus, hover, and splash colors.

If non-null, it is resolved against one of [WidgetState.focused], [WidgetState.hovered], and [WidgetState.pressed].

[WidgetState.pressed] triggers a ripple (an ink splash), per the current Material Design spec.

If the overlay color is null or resolves to null, then if [ThemeData.useMaterial3] is false, the default values for [InkResponse.focusColor], [InkResponse.hoverColor], [InkResponse.splashColor], and [InkResponse.highlightColor] will be used instead. If [ThemeData.useMaterial3] if true, the default values are:

- selected:
- pressed - ThemeData.colorScheme.primary(0.1)
- hovered - ThemeData.colorScheme.primary(0.08)
- focused - ThemeData.colorScheme.primary(0.1)
- pressed - ThemeData.colorScheme.primary(0.1)
- hovered - ThemeData.colorScheme.onSurface(0.08)
- focused - ThemeData.colorScheme.onSurface(0.1)

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.widgets.scrollable.dragStartBehavior}

### mouseCursor

```dart
MouseCursor? mouseCursor
```

{@template flutter.material.tabs.mouseCursor} The cursor for a mouse pointer when it enters or is hovering over the individual tab widgets.

If [mouseCursor] is a [WidgetStateMouseCursor], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.selected]. {@endtemplate}

If null, then the value of [TabBarThemeData.mouseCursor] is used. If that is also null, then [WidgetStateMouseCursor.clickable] is used.

### enableFeedback

```dart
bool? enableFeedback
```

Whether detected gestures should provide acoustic and/or haptic feedback.

For example, on Android a tap will produce a clicking sound and a long-press will produce a short vibration, when feedback is enabled.

Defaults to true.

### onTap

```dart
ValueChanged<int>? onTap
```

An optional callback that's called when the [TabBar] is tapped.

The callback is applied to the index of the tab where the tap occurred.

This callback has no effect on the default handling of taps. It's for applications that want to do a little extra work when a tab is tapped, even if the tap doesn't change the TabController's index. TabBar [onTap] callbacks should not make changes to the TabController since that would interfere with the default tap handler.

### onHover

```dart
TabValueChanged<bool>? onHover
```

An optional callback that's called when a [Tab]'s hover state in the [TabBar] changes.

Called when a pointer enters or exits the ink response area of the [Tab].

The value passed to the callback is true if a pointer has entered the [Tab] at `index` and false if a pointer has exited.

When hover is moved from one tab directly to another, this will be called twice. First to represent hover exiting the initial tab, and then second for the pointer entering hover over the next tab.

{@tool dartpad} This sample shows how to customize a [Tab] in response to hovering over a [TabBar].

** See code in examples/api/lib/material/tabs/tab_bar.onHover.dart ** {@end-tool}

### onFocusChange

```dart
TabValueChanged<bool>? onFocusChange
```

An optional callback that's called when a [Tab]'s focus state in the [TabBar] changes.

Called when the node for the [Tab] at `index` gains or loses focus.

The value passed to the callback is true if the node has gained focus for the [Tab] at `index` and false if focus has been lost.

When focus is moved from one tab directly to another, this will be called twice. First to represent focus being lost by the initially focused tab, and then second for the next tab gaining focus.

{@tool dartpad} This sample shows how to customize a [Tab] based on focus traversal in enclosing [TabBar].

** See code in examples/api/lib/material/tabs/tab_bar.onFocusChange.dart ** {@end-tool}

### physics

```dart
ScrollPhysics? physics
```

How the [TabBar]'s scroll view should respond to user input.

For example, determines how the scroll view continues to animate after the user stops dragging the scroll view.

Defaults to matching platform conventions.

### splashFactory

```dart
InteractiveInkFeatureFactory? splashFactory
```

Creates the tab bar's [InkWell] splash factory, which defines the appearance of "ink" splashes that occur in response to taps.

Use [NoSplash.splashFactory] to defeat ink splash rendering. For example to defeat both the splash and the hover/pressed overlay, but not the keyboard focused overlay:

```dart
TabBar(
  splashFactory: NoSplash.splashFactory,
  overlayColor: WidgetStateProperty.resolveWith<Color?>(
    (Set<WidgetState> states) {
      return states.contains(WidgetState.focused) ? null : Colors.transparent;
    },
  ),
  tabs: const <Widget>[
    // ...
  ],
)
```

### splashBorderRadius

```dart
BorderRadius? splashBorderRadius
```

Defines the clipping radius of splashes that extend outside the bounds of the tab.

This can be useful to match the [BoxDecoration.borderRadius] provided as [indicator].

```dart
TabBar(
  indicator: BoxDecoration(
    borderRadius: BorderRadius.circular(40),
  ),
  splashBorderRadius: BorderRadius.circular(40),
  tabs: const <Widget>[
    // ...
  ],
)
```

If this property is null, it is interpreted as [BorderRadius.zero].

### tabAlignment

```dart
TabAlignment? tabAlignment
```

Specifies the horizontal alignment of the tabs within a [TabBar].

If [TabBar.isScrollable] is false, only [TabAlignment.fill] and [TabAlignment.center] are supported. Otherwise an exception is thrown.

If [TabBar.isScrollable] is true, only [TabAlignment.start], [TabAlignment.startOffset], and [TabAlignment.center] are supported. Otherwise an exception is thrown.

If this is null, then the value of [TabBarThemeData.tabAlignment] is used.

If [TabBarThemeData.tabAlignment] is null and [ThemeData.useMaterial3] is true, then [TabAlignment.startOffset] is used if [isScrollable] is true, otherwise [TabAlignment.fill] is used.

If [TabBarThemeData.tabAlignment] is null and [ThemeData.useMaterial3] is false, then [TabAlignment.center] is used if [isScrollable] is true, otherwise [TabAlignment.fill] is used.

### textScaler

```dart
TextScaler? textScaler
```

Specifies the text scaling behavior for the [Tab] label.

If this is null, then the value of [TabBarThemeData.textScaler] is used. If that is also null, then the text scaling behavior is determined by the [MediaQueryData.textScaler] from the ambient [MediaQuery], or 1.0 if there is no [MediaQuery] in scope.

See also:

- [TextScaler], which is used to scale text based on the device's text scale factor.

### indicatorAnimation

```dart
TabIndicatorAnimation? indicatorAnimation
```

Specifies the animation behavior of the tab indicator.

If this is null, then the value of [TabBarThemeData.indicatorAnimation] is used. If that is also null, then the tab indicator will animate linearly if the [indicatorSize] is [TabBarIndicatorSize.tab], otherwise it will animate with an elastic effect if the [indicatorSize] is [TabBarIndicatorSize.label].

{@tool dartpad} This sample shows how to customize the animation behavior of the tab indicator by using the [indicatorAnimation] property.

** See code in examples/api/lib/material/tabs/tab_bar.indicator_animation.0.dart ** {@end-tool}

See also:

- [TabIndicatorAnimation], which specifies the animation behavior of the tab indicator.

### preferredSize

```dart
Size get preferredSize
```

A size whose height depends on if the tabs have both icons and text.

[AppBar] uses this size to compute its own preferred size.

### tabHasTextAndIcon

```dart
bool get tabHasTextAndIcon
```

Returns whether the [TabBar] contains a tab with both text and icon.

[TabBar] uses this to give uniform padding to all tabs in cases where there are some tabs with both text and icon and some which contain only text or icon.

### createState()

```dart
State<TabBar> createState()
```

# TabBarView

```dart
class TabBarView extends StatefulWidget {}
```

A page view that displays the widget which corresponds to the currently selected tab.

This widget is typically used in conjunction with a [TabBar].

{@youtube 560 315 https://www.youtube.com/watch?v=POtoEH-5l40}

If a [TabController] is not provided, then there must be a [DefaultTabController] ancestor.

The tab controller's [TabController.length] must equal the length of the [children] list and the length of the [TabBar.tabs] list.

To see a sample implementation, visit the [TabController] documentation.

### TabBarView()

```dart
TabBarView({dynamic key, required List<Widget> children, TabController? controller, ScrollPhysics? physics, DragStartBehavior dragStartBehavior = DragStartBehavior.start, double viewportFraction = 1.0, Clip clipBehavior = Clip.hardEdge})
```

Creates a page view with one child per tab.

The length of [children] must be the same as the [controller]'s length.

### controller

```dart
TabController? controller
```

This widget's selection and animation state.

If [TabController] is not provided, then the value of [DefaultTabController.of] will be used.

### children

```dart
List<Widget> children
```

One widget per tab.

Its length must match the length of the [TabBar.tabs] list, as well as the [controller]'s [TabController.length].

### physics

```dart
ScrollPhysics? physics
```

How the page view should respond to user input.

For example, determines how the page view continues to animate after the user stops dragging the page view.

The physics are modified to snap to page boundaries using [PageScrollPhysics] prior to being used.

Defaults to matching platform conventions.

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.widgets.scrollable.dragStartBehavior}

### viewportFraction

```dart
double viewportFraction
```

{@macro flutter.widgets.pageview.viewportFraction}

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### createState()

```dart
State<TabBarView> createState()
```

# TabPageSelectorIndicator

```dart
class TabPageSelectorIndicator extends StatelessWidget {}
```

Displays a single circle with the specified size, border style, border color and background colors.

Used by [TabPageSelector] to indicate the selected page.

### TabPageSelectorIndicator()

```dart
TabPageSelectorIndicator({dynamic key, required Color backgroundColor, required Color borderColor, required double size, BorderStyle borderStyle = BorderStyle.solid})
```

Creates an indicator used by [TabPageSelector].

### backgroundColor

```dart
Color backgroundColor
```

The indicator circle's background color.

### borderColor

```dart
Color borderColor
```

The indicator circle's border color.

### size

```dart
double size
```

The indicator circle's diameter.

### borderStyle

```dart
BorderStyle borderStyle
```

The indicator circle's border style.

Defaults to [BorderStyle.solid] if value is not specified.

### build()

```dart
Widget build(BuildContext context)
```

# TabPageSelector

```dart
class TabPageSelector extends StatefulWidget {}
```

Uses [TabPageSelectorIndicator] to display a row of small circular indicators, one per tab.

{@youtube 560 315 https://www.youtube.com/watch?v=Q628ue9Cq7U}

The selected tab's indicator is highlighted. Often used in conjunction with a [TabBarView].

If a [TabController] is not provided, then there must be a [DefaultTabController] ancestor.

### TabPageSelector()

```dart
TabPageSelector({dynamic key, TabController? controller, double indicatorSize = 12.0, Color? color, Color? selectedColor, BorderStyle? borderStyle})
```

Creates a compact widget that indicates which tab has been selected.

### controller

```dart
TabController? controller
```

This widget's selection and animation state.

If [TabController] is not provided, then the value of [DefaultTabController.of] will be used.

### indicatorSize

```dart
double indicatorSize
```

The indicator circle's diameter (the default value is 12.0).

### color

```dart
Color? color
```

The indicator circle's fill color for unselected pages.

If this parameter is null, then the indicator is filled with [Colors.transparent].

### selectedColor

```dart
Color? selectedColor
```

The indicator circle's fill color for selected pages and border color for all indicator circles.

If this parameter is null, then the indicator is filled with the theme's [ColorScheme.secondary].

### borderStyle

```dart
BorderStyle? borderStyle
```

The indicator circle's border style.

Defaults to [BorderStyle.solid] if value is not specified.

### createState()

```dart
State<TabPageSelector> createState()
```
