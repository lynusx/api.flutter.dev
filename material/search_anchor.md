@docImport 'package:flutter/services.dart';

# SearchAnchorChildBuilder

```dart
typedef SearchAnchorChildBuilder = Widget Function(BuildContext context, SearchController controller)
```

Signature for a function that creates a [Widget] which is used to open a search view.

The `controller` callback provided to [SearchAnchor.builder] can be used to open the search view and control the editable field on the view.

# SuggestionsBuilder

```dart
typedef SuggestionsBuilder = FutureOr<Iterable<Widget>> Function(BuildContext context, SearchController controller)
```

Signature for a function that creates a [Widget] to build the suggestion list based on the input in the search bar.

The `controller` callback provided to [SearchAnchor.suggestionsBuilder] can be used to close the search view and control the editable field on the view.

# ViewBuilder

```dart
typedef ViewBuilder = Widget Function(Iterable<Widget> suggestions)
```

Signature for a function that creates a [Widget] to layout the suggestion list.

Parameter `suggestions` is the content list that this function wants to lay out.

# SearchAnchor

```dart
class SearchAnchor extends StatefulWidget {}
```

Manages a "search view" route that allows the user to select one of the suggested completions for a search query.

The search view's route can either be shown by creating a [SearchController] and then calling [SearchController.openView] or by tapping on an anchor. When the anchor is tapped or [SearchController.openView] is called, the search view either grows to a specific size, or grows to fill the entire screen. By default, the search view only shows full screen on mobile platforms. Use [SearchAnchor.isFullScreen] to override the default setting.

The search view is usually opened by a [SearchBar], an [IconButton] or an [Icon]. If [builder] returns an Icon, or any un-tappable widgets, we don't have to explicitly call [SearchController.openView].

The search view route will be popped if the window size is changed and the search view route is not in full-screen mode. However, if the search view route is in full-screen mode, changing the window size, such as rotating a mobile device from portrait mode to landscape mode, will not close the search view.

{@tool dartpad} This example shows how to use an IconButton to open a search view in a [SearchAnchor]. It also shows how to use [SearchController] to open or close the search view route.

** See code in examples/api/lib/material/search_anchor/search_anchor.2.dart ** {@end-tool}

{@tool dartpad} This example shows how to set up a floating (or pinned) AppBar with a [SearchAnchor] for a title.

** See code in examples/api/lib/material/search_anchor/search_anchor.1.dart ** {@end-tool}

{@tool dartpad} This example shows how to fetch the search suggestions from a remote API.

** See code in examples/api/lib/material/search_anchor/search_anchor.3.dart ** {@end-tool}

{@tool dartpad} This example demonstrates fetching the search suggestions asynchronously and debouncing network calls.

** See code in examples/api/lib/material/search_anchor/search_anchor.4.dart ** {@end-tool}

See also:

- [SearchBar], a widget that defines a search bar.
- [SearchBarTheme], a widget that overrides the default configuration of a search bar.
- [SearchViewTheme], a widget that overrides the default configuration of a search view.

### SearchAnchor()

```dart
SearchAnchor({dynamic key, bool? isFullScreen, SearchController? searchController, ViewBuilder? viewBuilder, Widget? viewLeading, Iterable<Widget>? viewTrailing, String? viewHintText, Color? viewBackgroundColor, double? viewElevation, Color? viewSurfaceTintColor, BorderSide? viewSide, OutlinedBorder? viewShape, EdgeInsetsGeometry? viewBarPadding, double? headerHeight, TextStyle? headerTextStyle, TextStyle? headerHintStyle, Color? dividerColor, BoxConstraints? viewConstraints, EdgeInsetsGeometry? viewPadding, bool? shrinkWrap, TextCapitalization? textCapitalization, ValueChanged<String>? viewOnChanged, ValueChanged<String>? viewOnSubmitted, VoidCallback? viewOnClose, VoidCallback? viewOnOpen, required SearchAnchorChildBuilder builder, required SuggestionsBuilder suggestionsBuilder, TextInputAction? textInputAction, TextInputType? keyboardType, bool enabled = true, SmartDashesType? smartDashesType, SmartQuotesType? smartQuotesType})
```

Creates a const [SearchAnchor].

The [builder] and [suggestionsBuilder] arguments are required.

### SearchAnchor.bar()

```dart
SearchAnchor.bar({Widget? barLeading, Iterable<Widget>? barTrailing, String? barHintText, GestureTapCallback? onTap, ValueChanged<String>? onSubmitted, ValueChanged<String>? onChanged, VoidCallback? onClose, VoidCallback? onOpen, WidgetStateProperty<double?>? barElevation, WidgetStateProperty<Color?>? barBackgroundColor, WidgetStateProperty<Color?>? barOverlayColor, WidgetStateProperty<BorderSide?>? barSide, WidgetStateProperty<OutlinedBorder?>? barShape, WidgetStateProperty<EdgeInsetsGeometry?>? barPadding, EdgeInsetsGeometry? viewBarPadding, WidgetStateProperty<TextStyle?>? barTextStyle, WidgetStateProperty<TextStyle?>? barHintStyle, ViewBuilder? viewBuilder, Widget? viewLeading, Iterable<Widget>? viewTrailing, String? viewHintText, Color? viewBackgroundColor, double? viewElevation, BorderSide? viewSide, OutlinedBorder? viewShape, double? viewHeaderHeight, TextStyle? viewHeaderTextStyle, TextStyle? viewHeaderHintStyle, Color? dividerColor, BoxConstraints? constraints, BoxConstraints? viewConstraints, EdgeInsetsGeometry? viewPadding, bool? shrinkWrap, bool? isFullScreen, SearchController searchController, TextCapitalization textCapitalization, required SuggestionsBuilder suggestionsBuilder, TextInputAction? textInputAction, TextInputType? keyboardType, EdgeInsets scrollPadding, EditableTextContextMenuBuilder contextMenuBuilder, bool enabled, SmartDashesType? smartDashesType, SmartQuotesType? smartQuotesType})
```

Create a [SearchAnchor] that has a [SearchBar] which opens a search view.

All the barX parameters are used to customize the anchor. Similarly, all the viewX parameters are used to override the view's defaults.

{@tool dartpad} This example shows how to use a [SearchAnchor.bar] which uses a default search bar to open a search view route.

** See code in examples/api/lib/material/search_anchor/search_anchor.0.dart ** {@end-tool}

### isFullScreen

```dart
bool? isFullScreen
```

Whether the search view grows to fill the entire screen when the [SearchAnchor] is tapped.

By default, the search view is full-screen on mobile devices. On other platforms, the search view only grows to a specific size that is determined by the anchor and the default size.

### searchController

```dart
SearchController? searchController
```

An optional controller that allows opening and closing of the search view from other widgets.

If this is null, one internal search controller is created automatically and it is used to open the search view when the user taps on the anchor.

### viewBuilder

```dart
ViewBuilder? viewBuilder
```

Optional callback to obtain a widget to lay out the suggestion list of the search view.

Default view uses a [ListView] with a vertical scroll direction.

### viewLeading

```dart
Widget? viewLeading
```

An optional widget to display before the text input field when the search view is open.

Typically the [viewLeading] widget is an [Icon] or an [IconButton].

Defaults to a back button which pops the view.

### viewTrailing

```dart
Iterable<Widget>? viewTrailing
```

An optional widget list to display after the text input field when the search view is open.

Typically the [viewTrailing] widget list only has one or two widgets.

Defaults to an icon button which clears the text in the input field.

### viewHintText

```dart
String? viewHintText
```

Text that is displayed when the search bar's input field is empty.

### viewBackgroundColor

```dart
Color? viewBackgroundColor
```

The search view's background fill color.

If null, the value of [SearchViewThemeData.backgroundColor] will be used. If this is also null, then the default value is [ColorScheme.surfaceContainerHigh].

### viewElevation

```dart
double? viewElevation
```

The elevation of the search view's [Material].

If null, the value of [SearchViewThemeData.elevation] will be used. If this is also null, then default value is 6.0.

### viewSurfaceTintColor

```dart
Color? viewSurfaceTintColor
```

The surface tint color of the search view's [Material].

This is not recommended for use. [Material 3 spec](https://m3.material.io/styles/color/the-color-system/color-roles) introduced a set of tone-based surfaces and surface containers in its [ColorScheme], which provide more flexibility. The intention is to eventually remove surface tint color from the framework.

If null, the value of [SearchViewThemeData.surfaceTintColor] will be used. If this is also null, then the default value is [ColorScheme.surfaceTint].

### viewSide

```dart
BorderSide? viewSide
```

The color and weight of the search view's outline.

This value is combined with [viewShape] to create a shape decorated with an outline. This will be ignored if the view is full-screen.

If null, the value of [SearchViewThemeData.side] will be used. If this is also null, the search view doesn't have a side by default.

### viewShape

```dart
OutlinedBorder? viewShape
```

The shape of the search view's underlying [Material].

This shape is combined with [viewSide] to create a shape decorated with an outline.

If null, the value of [SearchViewThemeData.shape] will be used. If this is also null, then the default value is a rectangle shape for full-screen mode and a [RoundedRectangleBorder] shape with a 28.0 radius otherwise.

### viewBarPadding

```dart
EdgeInsetsGeometry? viewBarPadding
```

The padding to use for the search view's search bar.

If null, then the default value is 8.0 horizontally.

### headerHeight

```dart
double? headerHeight
```

The height of the search field on the search view.

If null, the value of [SearchViewThemeData.headerHeight] will be used. If this is also null, the default value is 56.0.

### headerTextStyle

```dart
TextStyle? headerTextStyle
```

The style to use for the text being edited on the search view.

If null, defaults to the `bodyLarge` text style from the current [Theme]. The default text color is [ColorScheme.onSurface].

### headerHintStyle

```dart
TextStyle? headerHintStyle
```

The style to use for the [viewHintText] on the search view.

If null, the value of [SearchViewThemeData.headerHintStyle] will be used. If this is also null, the value of [headerTextStyle] will be used. If this is also null, defaults to the `bodyLarge` text style from the current [Theme]. The default text color is [ColorScheme.onSurfaceVariant].

### dividerColor

```dart
Color? dividerColor
```

The color of the divider on the search view.

If this property is null, then [SearchViewThemeData.dividerColor] is used. If that is also null, the default value is [ColorScheme.outline].

### viewConstraints

```dart
BoxConstraints? viewConstraints
```

Optional size constraints for the search view.

By default, the search view has the same width as the anchor and is 2/3 the height of the screen. If the width and height of the view are within the [viewConstraints], the view will show its default size. Otherwise, the size of the view will be constrained by this property.

If null, the value of [SearchViewThemeData.constraints] will be used. If this is also null, then the constraints defaults to:

```dart
const BoxConstraints(minWidth: 360.0, minHeight: 240.0)
```

### viewPadding

```dart
EdgeInsetsGeometry? viewPadding
```

The padding to use for the search view.

Has no effect if the search view is full-screen.

If null, the value of [SearchViewThemeData.padding] will be used.

### shrinkWrap

```dart
bool? shrinkWrap
```

Whether the search view should shrink-wrap its contents.

Has no effect if the search view is full-screen.

If null, the value of [SearchViewThemeData.shrinkWrap] will be used. If this is also null, then the default value is `false`.

### textCapitalization

```dart
TextCapitalization? textCapitalization
```

{@macro flutter.widgets.editableText.textCapitalization}

### viewOnChanged

```dart
ValueChanged<String>? viewOnChanged
```

Called each time the user modifies the search view's text field.

See also:

- [viewOnSubmitted], which is called when the user indicates that they are done editing the search view's text field.

### viewOnSubmitted

```dart
ValueChanged<String>? viewOnSubmitted
```

Called when the user indicates that they are done editing the text in the text field of a search view. Typically this is called when the user presses the enter key.

See also:

- [viewOnChanged], which is called when the user modifies the text field of the search view.

### viewOnClose

```dart
VoidCallback? viewOnClose
```

Called when the search view is closed.

### viewOnOpen

```dart
VoidCallback? viewOnOpen
```

Called when the search view is opened.

### builder

```dart
SearchAnchorChildBuilder builder
```

Called to create a widget which can open a search view route when it is tapped.

The widget returned by this builder is faded out when it is tapped. At the same time a search view route is faded in.

### suggestionsBuilder

```dart
SuggestionsBuilder suggestionsBuilder
```

Called to get the suggestion list for the search view.

This builder is called once when the search view is first displayed, and subsequently every time the search text changes.

By default, the list returned by this builder is laid out in a [ListView]. To get a different layout, use [viewBuilder] to override.

### textInputAction

```dart
TextInputAction? textInputAction
```

{@macro flutter.widgets.TextField.textInputAction}

### keyboardType

```dart
TextInputType? keyboardType
```

The type of action button to use for the keyboard.

Defaults to the default value specified in [TextField].

### enabled

```dart
bool enabled
```

Whether or not this widget is currently interactive.

When false, the widget will ignore taps and appear dimmed.

Defaults to true.

### smartDashesType

```dart
SmartDashesType? smartDashesType
```

Configures how smart dashes are handled in the text field used by this [SearchAnchor].

For example, when enabled, double hyphens (`--`) may be automatically replaced with an em dash (`—`) on iOS.

Defaults to [SmartDashesType.enabled].

See also:

- [TextField.smartDashesType], which provides the same configuration option on a standalone [TextField].

### smartQuotesType

```dart
SmartQuotesType? smartQuotesType
```

Configures how smart quotes are handled in the text field used by this [SearchAnchor].

For example, when enabled, straight quotes (`"`) may be automatically replaced with curly quotes (`“ ”`) on iOS.

Defaults to [SmartQuotesType.enabled].

See also:

- [TextField.smartQuotesType], which provides the same configuration option on a standalone [TextField].

### createState()

```dart
State<SearchAnchor> createState()
```

# SearchController

```dart
class SearchController extends TextEditingController {}
```

A controller to manage a search view created by [SearchAnchor].

A [SearchController] is used to control a menu after it has been created, with methods such as [openView] and [closeView]. It can also control the text in the input field.

To observe open/close state changes of search view, provide [SearchAnchor.viewOnOpen] and/or [SearchAnchor.viewOnClose] callbacks.

See also:

- [SearchAnchor], a widget that defines a region that opens a search view.
- [TextEditingController], A controller for an editable text field.

### isAttached

```dart
bool get isAttached
```

Whether this controller has associated search anchor.

### isOpen

```dart
bool get isOpen
```

Whether or not the associated search view is currently open.

### openView()

```dart
void openView()
```

Opens the search view that this controller is associated with.

### closeView()

```dart
void closeView(String? selectedText)
```

Close the search view that this search controller is associated with.

If `selectedText` is given, then the text value of the controller is set to `selectedText`.

# SearchBar

```dart
class SearchBar extends StatefulWidget {}
```

A Material Design search bar.

A [SearchBar] looks like a [TextField]. Tapping a SearchBar typically shows a "search view" route: a route with the search bar at the top and a list of suggested completions for the search bar's text below. [SearchBar]s are usually created by a [SearchAnchor.builder]. The builder provides a [SearchController] that's used by the search bar's [SearchBar.onTap] or [SearchBar.onChanged] callbacks to show the search view and to hide it when the user selects a suggestion.

For [TextDirection.ltr], the [leading] widget is on the left side of the bar. It should contain either a navigational action (such as a menu or up-arrow) or a non-functional search icon.

The [trailing] is an optional list that appears at the other end of the search bar. Typically only one or two action icons are included. These actions can represent additional modes of searching (like voice search), a separate high-level action (such as current location) or an overflow menu.

{@tool dartpad} This example demonstrates how to use a [SearchBar] as the return value of the [SearchAnchor.builder] property. The [SearchBar] also includes a leading search icon and a trailing action to toggle the brightness.

** See code in examples/api/lib/material/search_anchor/search_bar.0.dart ** {@end-tool}

See also:

- [SearchAnchor], a widget that typically uses an [IconButton] or a [SearchBar] to manage a "search view" route.
- [SearchBarTheme], a widget that overrides the default configuration of a search bar.
- [SearchViewTheme], a widget that overrides the default configuration of a search view.

### SearchBar()

```dart
SearchBar({dynamic key, TextEditingController? controller, FocusNode? focusNode, String? hintText, Widget? leading, Iterable<Widget>? trailing, GestureTapCallback? onTap, TapRegionCallback? onTapOutside, ValueChanged<String>? onChanged, ValueChanged<String>? onSubmitted, BoxConstraints? constraints, WidgetStateProperty<double?>? elevation, WidgetStateProperty<Color?>? backgroundColor, WidgetStateProperty<Color?>? shadowColor, WidgetStateProperty<Color?>? surfaceTintColor, WidgetStateProperty<Color?>? overlayColor, WidgetStateProperty<BorderSide?>? side, WidgetStateProperty<OutlinedBorder?>? shape, WidgetStateProperty<EdgeInsetsGeometry?>? padding, WidgetStateProperty<TextStyle?>? textStyle, WidgetStateProperty<TextStyle?>? hintStyle, TextCapitalization? textCapitalization, bool enabled = true, bool autoFocus = false, TextInputAction? textInputAction, TextInputType? keyboardType, EdgeInsets scrollPadding = const EdgeInsets.all(20.0), EditableTextContextMenuBuilder? contextMenuBuilder = _defaultContextMenuBuilder, bool readOnly = false, SmartDashesType? smartDashesType, SmartQuotesType? smartQuotesType})
```

Creates a Material Design search bar.

### controller

```dart
TextEditingController? controller
```

Controls the text being edited in the search bar's text field.

If null, this widget will create its own [TextEditingController].

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### hintText

```dart
String? hintText
```

Text that suggests what sort of input the field accepts.

Displayed at the same location on the screen where text may be entered when the input is empty.

Defaults to null.

### leading

```dart
Widget? leading
```

A widget to display before the text input field.

Typically the [leading] widget is an [Icon] or an [IconButton].

### trailing

```dart
Iterable<Widget>? trailing
```

A list of Widgets to display in a row after the text field.

Typically these actions can represent additional modes of searching (like voice search), an avatar, a separate high-level action (such as current location) or an overflow menu. There should not be more than two trailing actions.

### onTap

```dart
GestureTapCallback? onTap
```

Called when the user taps this search bar.

### onTapOutside

```dart
TapRegionCallback? onTapOutside
```

Called when the user taps outside the search bar.

### onChanged

```dart
ValueChanged<String>? onChanged
```

Invoked upon user input.

### onSubmitted

```dart
ValueChanged<String>? onSubmitted
```

Called when the user indicates that they are done editing the text in the field.

### constraints

```dart
BoxConstraints? constraints
```

Optional size constraints for the search bar.

If null, the value of [SearchBarThemeData.constraints] will be used. If this is also null, then the constraints defaults to:

```dart
const BoxConstraints(minWidth: 360.0, maxWidth: 800.0, minHeight: 56.0)
```

### elevation

```dart
WidgetStateProperty<double?>? elevation
```

The elevation of the search bar's [Material].

If null, the value of [SearchBarThemeData.elevation] will be used. If this is also null, then default value is 6.0.

### backgroundColor

```dart
WidgetStateProperty<Color?>? backgroundColor
```

The search bar's background fill color.

If null, the value of [SearchBarThemeData.backgroundColor] will be used. If this is also null, then the default value is [ColorScheme.surfaceContainerHigh].

### shadowColor

```dart
WidgetStateProperty<Color?>? shadowColor
```

The shadow color of the search bar's [Material].

If null, the value of [SearchBarThemeData.shadowColor] will be used. If this is also null, then the default value is [ColorScheme.shadow].

### surfaceTintColor

```dart
WidgetStateProperty<Color?>? surfaceTintColor
```

The surface tint color of the search bar's [Material].

This is not recommended for use. [Material 3 spec](https://m3.material.io/styles/color/the-color-system/color-roles) introduced a set of tone-based surfaces and surface containers in its [ColorScheme], which provide more flexibility. The intention is to eventually remove surface tint color from the framework.

If null, the value of [SearchBarThemeData.surfaceTintColor] will be used. If this is also null, then the default value is [Colors.transparent].

### overlayColor

```dart
WidgetStateProperty<Color?>? overlayColor
```

The highlight color that's typically used to indicate that the search bar is focused, hovered, or pressed.

### side

```dart
WidgetStateProperty<BorderSide?>? side
```

The color and weight of the search bar's outline.

This value is combined with [shape] to create a shape decorated with an outline.

If null, the value of [SearchBarThemeData.side] will be used. If this is also null, the search bar doesn't have a side by default.

### shape

```dart
WidgetStateProperty<OutlinedBorder?>? shape
```

The shape of the search bar's underlying [Material].

This shape is combined with [side] to create a shape decorated with an outline.

If null, the value of [SearchBarThemeData.shape] will be used. If this is also null, defaults to [StadiumBorder].

### padding

```dart
WidgetStateProperty<EdgeInsetsGeometry?>? padding
```

The padding between the search bar's boundary and its contents.

If null, the value of [SearchBarThemeData.padding] will be used. If this is also null, then the default value is 16.0 horizontally.

### textStyle

```dart
WidgetStateProperty<TextStyle?>? textStyle
```

The style to use for the text being edited.

If null, defaults to the `bodyLarge` text style from the current [Theme]. The default text color is [ColorScheme.onSurface].

### hintStyle

```dart
WidgetStateProperty<TextStyle?>? hintStyle
```

The style to use for the [hintText].

If null, the value of [SearchBarThemeData.hintStyle] will be used. If this is also null, the value of [textStyle] will be used. If this is also null, defaults to the `bodyLarge` text style from the current [Theme]. The default text color is [ColorScheme.onSurfaceVariant].

### textCapitalization

```dart
TextCapitalization? textCapitalization
```

{@macro flutter.widgets.editableText.textCapitalization}

### enabled

```dart
bool enabled
```

Whether or not this widget is currently interactive.

When false, the widget will ignore taps and appear dimmed.

Defaults to true.

### autoFocus

```dart
bool autoFocus
```

{@macro flutter.widgets.editableText.autofocus}

### textInputAction

```dart
TextInputAction? textInputAction
```

{@macro flutter.widgets.TextField.textInputAction}

### keyboardType

```dart
TextInputType? keyboardType
```

The type of action button to use for the keyboard.

Defaults to the default value specified in [TextField].

### scrollPadding

```dart
EdgeInsets scrollPadding
```

{@macro flutter.widgets.editableText.scrollPadding}

### contextMenuBuilder

```dart
EditableTextContextMenuBuilder? contextMenuBuilder
```

{@macro flutter.widgets.EditableText.contextMenuBuilder}

If not provided, will build a default menu based on the platform.

See also:

- [AdaptiveTextSelectionToolbar], which is built by default.
- [BrowserContextMenu], which allows the browser's context menu on web to be disabled and Flutter-rendered context menus to appear.

### readOnly

```dart
bool readOnly
```

{@macro flutter.widgets.editableText.readOnly}

### smartDashesType

```dart
SmartDashesType? smartDashesType
```

Configures how smart dashes are handled in the text field used by this [SearchBar].

For example, when enabled, double hyphens (`--`) may be automatically replaced with an em dash (`—`) on iOS.

Defaults to [SmartDashesType.enabled].

See also:

- [TextField.smartDashesType], which provides the same configuration option on a standalone [TextField].

### smartQuotesType

```dart
SmartQuotesType? smartQuotesType
```

Configures how smart quotes are handled in the text field used by this [SearchBar].

For example, when enabled, straight quotes (`"`) may be automatically replaced with curly quotes (`“ ”`) on iOS.

Defaults to [SmartQuotesType.enabled].

See also:

- [TextField.smartQuotesType], which provides the same configuration option on a standalone [TextField].

### createState()

```dart
State<SearchBar> createState()
```
