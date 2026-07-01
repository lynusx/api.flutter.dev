@docImport 'card.dart'; @docImport 'checkbox.dart'; @docImport 'checkbox_list_tile.dart'; @docImport 'circle_avatar.dart'; @docImport 'drawer.dart'; @docImport 'expansion_tile.dart'; @docImport 'material.dart'; @docImport 'radio.dart'; @docImport 'radio_list_tile.dart'; @docImport 'scaffold.dart'; @docImport 'switch.dart'; @docImport 'switch_list_tile.dart';

# ListTileStyle

```dart
enum ListTileStyle {}
```

Defines the title font used for [ListTile] descendants of a [ListTileTheme].

List tiles that appear in a [Drawer] use the theme's [TextTheme.bodyLarge] text style, which is a little smaller than the theme's [TextTheme.titleMedium] text style, which is used by default.

Use a title font that's appropriate for a [ListTile] in a list.

Use a title font that's appropriate for a [ListTile] that appears in a [Drawer].

# ListTileControlAffinity

```dart
enum ListTileControlAffinity {}
```

Where to place the control in widgets that use [ListTile] to position a control next to a label.

See also:

- [CheckboxListTile], which combines a [ListTile] with a [Checkbox].
- [RadioListTile], which combines a [ListTile] with a [Radio] button.
- [SwitchListTile], which combines a [ListTile] with a [Switch].
- [ExpansionTile], which combines a [ListTile] with a button that expands or collapses the tile to reveal or hide the children.

Position the control on the leading edge, and the secondary widget, if any, on the trailing edge.

Position the control on the trailing edge, and the secondary widget, if any, on the leading edge.

Position the control relative to the text in the fashion that is typical for the current platform, and place the secondary widget on the opposite side.

# ListTileTitleAlignment

```dart
enum ListTileTitleAlignment {}
```

Defines how [ListTile.leading] and [ListTile.trailing] are vertically aligned relative to the [ListTile]'s titles ([ListTile.title] and [ListTile.subtitle]).

See also:

- [ListTile.titleAlignment], to configure the title alignment for an individual [ListTile].
- [ListTileThemeData.titleAlignment], to configure the title alignment for all of the [ListTile]s under a [ListTileTheme].
- [ThemeData.listTileTheme], to configure the [ListTileTheme] for an entire app.

The top of the [ListTile.leading] and [ListTile.trailing] widgets are placed [ListTile.minVerticalPadding] below the top of the [ListTile.title] if [ListTile.isThreeLine] is true, otherwise they're centered relative to the [ListTile.title] and [ListTile.subtitle] widgets.

This is the default when [ThemeData.useMaterial3] is true.

The tops of the [ListTile.leading] and [ListTile.trailing] widgets are placed 16 pixels below the top of the [ListTile.title] widget, if the [ListTile]'s overall height is greater than 72, otherwise the [ListTile.trailing] widget is centered relative to the [ListTile.title] and [ListTile.subtitle] widgets, and the [ListTile.leading] widget is 16 pixels below the top of [ListTile.title], or center-aligned with [ListTile.title], whichever makes the [ListTile.leading] closer to the top edge of [ListTile.title].

This is the default when [ThemeData.useMaterial3] is false.

The tops of the [ListTile.leading] and [ListTile.trailing] widgets are placed [ListTile.minVerticalPadding] below the top of the [ListTile.title].

The [ListTile.leading] and [ListTile.trailing] widgets are centered relative to the [ListTile]'s titles.

The bottoms of the [ListTile.leading] and [ListTile.trailing] widgets are placed [ListTile.minVerticalPadding] above the bottom of the [ListTile]'s titles.

# ListTile

```dart
class ListTile extends StatelessWidget {}
```

A single fixed-height row that typically contains some text as well as a leading or trailing icon.

{@youtube 560 315 https://www.youtube.com/watch?v=l8dj0yPBvgQ}

A list tile contains one to three lines of text optionally flanked by icons or other widgets, such as check boxes. The icons (or other widgets) for the tile are defined with the [leading] and [trailing] parameters. The first line of text is not optional and is specified with [title]. The value of [subtitle], which _is_ optional, will occupy the space allocated for an additional line of text, or two lines if [isThreeLine] is true. If [dense] is true then the overall height of this tile and the size of the [DefaultTextStyle]s that wrap the [title] and [subtitle] widget are reduced.

It is the responsibility of the caller to ensure that [title] does not wrap, and to ensure that [subtitle] doesn't wrap (if [isThreeLine] is false) or wraps to two lines (if it is true).

The heights of the [leading] and [trailing] widgets are constrained according to the [Material spec](https://material.io/design/components/lists.html). An exception is made for one-line ListTiles for accessibility. Please see the example below to see how to adhere to both Material spec and accessibility requirements.

The [leading] and [trailing] widgets can expand as far as they wish horizontally, so ensure that they are properly constrained.

List tiles are typically used in [ListView]s, or arranged in [Column]s in [Drawer]s and [Card]s.

This widget requires a [Material] widget ancestor in the tree to paint itself on, which is typically provided by the app's [Scaffold]. The [tileColor], [selectedTileColor], [focusColor], and [hoverColor] are not painted by the [ListTile] itself but by the [Material] widget ancestor. In this case, one can wrap a [Material] widget around the [ListTile], e.g.:

{@tool snippet}

```dart
const ColoredBox(
  color: Colors.green,
  child: Material(
    child: ListTile(
      title: Text('ListTile with red background'),
      tileColor: Colors.red,
    ),
  ),
)
```

{@end-tool}

## Performance considerations when wrapping [ListTile] with [Material]

Wrapping a large number of [ListTile]s individually with [Material]s is expensive. Consider only wrapping the [ListTile]s that require it or include a common [Material] ancestor where possible.

[ListTile] must be wrapped in a [Material] widget to animate [tileColor], [selectedTileColor], [focusColor], and [hoverColor] as these colors are not drawn by the list tile itself but by the material widget ancestor.

{@tool dartpad} This example showcases how [ListTile] needs to be wrapped in a [Material] widget to animate colors.

** See code in examples/api/lib/material/list_tile/list_tile.0.dart ** {@end-tool}

{@tool dartpad} This example uses a [ListView] to demonstrate different configurations of [ListTile]s in [Card]s.

![Different variations of ListTile](https://flutter.github.io/assets-for-api-docs/assets/material/list_tile.png)

** See code in examples/api/lib/material/list_tile/list_tile.1.dart ** {@end-tool}

{@tool dartpad} This sample shows the creation of a [ListTile] using [ThemeData.useMaterial3] flag, as described in: https://m3.material.io/components/lists/overview.

** See code in examples/api/lib/material/list_tile/list_tile.2.dart ** {@end-tool}

{@tool dartpad} This sample shows [ListTile]'s [textColor] and [iconColor] can use [WidgetStateColor] color to change the color of the text and icon when the [ListTile] is enabled, selected, or disabled.

** See code in examples/api/lib/material/list_tile/list_tile.3.dart ** {@end-tool}

{@tool dartpad} This sample shows [ListTile.titleAlignment] can be used to configure the [leading] and [trailing] widgets alignment relative to the [title] and [subtitle] widgets.

** See code in examples/api/lib/material/list_tile/list_tile.4.dart ** {@end-tool}

{@tool snippet} To use a [ListTile] within a [Row], it needs to be wrapped in an [Expanded] widget. [ListTile] requires fixed width constraints, whereas a [Row] does not constrain its children.

```dart
const Row(
  children: <Widget>[
    Expanded(
      child: ListTile(
        leading: FlutterLogo(),
        title: Text('These ListTiles are expanded '),
      ),
    ),
    Expanded(
      child: ListTile(
        trailing: FlutterLogo(),
        title: Text('to fill the available space.'),
      ),
    ),
  ],
)
```

{@end-tool} {@tool snippet}

Tiles can be much more elaborate. Here is a tile which can be tapped, but which is disabled when the `_act` variable is not 2. When the tile is tapped, the whole row has an ink splash effect (see [InkWell]).

```dart
ListTile(
  leading: const Icon(Icons.flight_land),
  title: const Text("Trix's airplane"),
  subtitle: _act != 2 ? const Text('The airplane is only in Act II.') : null,
  enabled: _act == 2,
  onTap: () { /* react to the tile being tapped */ }
)
```

{@end-tool}

To be accessible, tappable [leading] and [trailing] widgets have to be at least 48x48 in size. However, to adhere to the Material spec, [trailing] and [leading] widgets in one-line ListTiles should visually be at most 32 ([dense]: true) or 40 ([dense]: false) in height, which may conflict with the accessibility requirement.

For this reason, a one-line ListTile allows the height of [leading] and [trailing] widgets to be constrained by the height of the ListTile. This allows for the creation of tappable [leading] and [trailing] widgets that are large enough, but it is up to the developer to ensure that their widgets follow the Material spec.

{@tool snippet}

Here is an example of a one-line, non-[dense] ListTile with a tappable leading widget that adheres to accessibility requirements and the Material spec. To adjust the use case below for a one-line, [dense] ListTile, adjust the vertical padding to 8.0.

```dart
ListTile(
  leading: GestureDetector(
    behavior: HitTestBehavior.translucent,
    onTap: () {},
    child: Container(
      width: 48,
      height: 48,
      padding: const EdgeInsets.symmetric(vertical: 4.0),
      alignment: Alignment.center,
      child: const CircleAvatar(),
    ),
  ),
  title: const Text('title'),
  dense: false,
)
```

{@end-tool}

## The ListTile layout isn't exactly what I want

If the way ListTile pads and positions its elements isn't quite what you're looking for, it's easy to create custom list items with a combination of other widgets, such as [Row]s and [Column]s.

{@tool dartpad} Here is an example of a custom list item that resembles a YouTube-related video list item created with [Expanded] and [Container] widgets.

** See code in examples/api/lib/material/list_tile/custom_list_item.0.dart ** {@end-tool}

{@tool dartpad} Here is an example of an article list item with multiline titles and subtitles. It utilizes [Row]s and [Column]s, as well as [Expanded] and [AspectRatio] widgets to organize its layout.

** See code in examples/api/lib/material/list_tile/custom_list_item.1.dart ** {@end-tool}

See also:

- [ListTileTheme], which defines visual properties for [ListTile]s.
- [ListView], which can display an arbitrary number of [ListTile]s in a scrolling list.
- [CircleAvatar], which shows an icon representing a person and is often used as the [leading] element of a ListTile.
- [Card], which can be used with [Column] to show a few [ListTile]s.
- [Divider], which can be used to separate [ListTile]s.
- [ListTile.divideTiles], a utility for inserting [Divider]s in between [ListTile]s.
- [CheckboxListTile], [RadioListTile], and [SwitchListTile], widgets that combine [ListTile] with other controls.
- Material 3 [ListTile] specifications are referenced from <https://m3.material.io/components/lists/specs> and Material 2 [ListTile] specifications are referenced from <https://material.io/design/components/lists.html>
- Cookbook: [Use lists](https://docs.flutter.dev/cookbook/lists/basic-list)
- Cookbook: [Implement swipe to dismiss](https://docs.flutter.dev/cookbook/gestures/dismissible)

### ListTile()

```dart
ListTile({dynamic key, Widget? leading, Widget? title, Widget? subtitle, Widget? trailing, bool? isThreeLine, bool? dense, VisualDensity? visualDensity, ShapeBorder? shape, ListTileStyle? style, Color? selectedColor, Color? iconColor, Color? textColor, TextStyle? titleTextStyle, TextStyle? subtitleTextStyle, TextStyle? leadingAndTrailingTextStyle, EdgeInsetsGeometry? contentPadding, bool enabled = true, GestureTapCallback? onTap, GestureLongPressCallback? onLongPress, ValueChanged<bool>? onFocusChange, MouseCursor? mouseCursor, bool selected = false, Color? focusColor, Color? hoverColor, Color? splashColor, FocusNode? focusNode, bool autofocus = false, Color? tileColor, Color? selectedTileColor, bool? enableFeedback, double? horizontalTitleGap, double? minVerticalPadding, double? minLeadingWidth, double? minTileHeight, ListTileTitleAlignment? titleAlignment, bool internalAddSemanticForOnTap = true, MaterialStatesController? statesController})
```

Creates a list tile.

If [isThreeLine] is true, then [subtitle] must not be null.

Requires one of its ancestors to be a [Material] widget.

### leading

```dart
Widget? leading
```

A widget to display before the title.

Typically an [Icon] or a [CircleAvatar] widget.

### title

```dart
Widget? title
```

The primary content of the list tile.

Typically a [Text] widget.

This should not wrap. To enforce the single line limit, use [Text.maxLines].

### subtitle

```dart
Widget? subtitle
```

Additional content displayed below the title.

Typically a [Text] widget.

If [isThreeLine] is false, this should not wrap.

If [isThreeLine] is true, this should be configured to take a maximum of two lines. For example, you can use [Text.maxLines] to enforce the number of lines.

The subtitle's default [TextStyle] depends on [TextTheme.bodyMedium] except [TextStyle.color]. The [TextStyle.color] depends on the value of [enabled] and [selected].

When [enabled] is false, the text color is set to [ThemeData.disabledColor].

When [selected] is false, the text color is set to [ListTileTheme.textColor] if it's not null and to [TextTheme.bodySmall]'s color if [ListTileTheme.textColor] is null.

### trailing

```dart
Widget? trailing
```

A widget to display after the title.

Typically an [Icon] widget.

To show right-aligned metadata (assuming left-to-right reading order; left-aligned for right-to-left reading order), consider using a [Row] with [CrossAxisAlignment.baseline] alignment whose first item is [Expanded] and whose second child is the metadata text, instead of using the [trailing] property.

### isThreeLine

```dart
bool? isThreeLine
```

Whether this list tile is intended to display three lines of text.

If true, then [subtitle] must be non-null (since it is expected to give the second and third lines of text).

If false, the list tile is treated as having one line if the subtitle is null and treated as having two lines if the subtitle is non-null.

When using a [Text] widget for [title] and [subtitle], you can enforce line limits using [Text.maxLines].

See also:

- [ListTileTheme.of], which returns the nearest [ListTileTheme]'s [ListTileThemeData].

### dense

```dart
bool? dense
```

{@template flutter.material.ListTile.dense} Whether this list tile is part of a vertically dense list.

If this property is null then its value is based on [ListTileTheme.dense].

Dense list tiles default to a smaller height.

It is not recommended to set [dense] to true when [ThemeData.useMaterial3] is true. {@endtemplate}

### visualDensity

```dart
VisualDensity? visualDensity
```

Defines how compact the list tile's layout will be.

{@macro flutter.material.themedata.visualDensity}

See also:

- [ThemeData.visualDensity], which specifies the [visualDensity] for all widgets within a [Theme].

### shape

```dart
ShapeBorder? shape
```

{@template flutter.material.ListTile.shape} Defines the tile's [InkWell.customBorder] and [Ink.decoration] shape. {@endtemplate}

If this property is null then [ListTileThemeData.shape] is used. If that is also null then a rectangular [Border] will be used.

See also:

- [ListTileTheme.of], which returns the nearest [ListTileTheme]'s [ListTileThemeData].

### selectedColor

```dart
Color? selectedColor
```

Defines the color used for icons and text when the list tile is selected.

If this property is null then [ListTileThemeData.selectedColor] is used. If that is also null then [ColorScheme.primary] is used.

See also:

- [ListTileTheme.of], which returns the nearest [ListTileTheme]'s [ListTileThemeData].

### iconColor

```dart
Color? iconColor
```

Defines the default color for [leading] and [trailing] icons.

If this property is null and [selected] is false then [ListTileThemeData.iconColor] is used. If that is also null and [ThemeData.useMaterial3] is true, [ColorScheme.onSurfaceVariant] is used, otherwise if [ThemeData.brightness] is [Brightness.light], [Colors.black54] is used, and if [ThemeData.brightness] is [Brightness.dark], the value is null.

If this property is null and [selected] is true then [ListTileThemeData.selectedColor] is used. If that is also null then [ColorScheme.primary] is used.

If this color is a [WidgetStateColor] it will be resolved against [WidgetState.selected] and [WidgetState.disabled] states.

See also:

- [ListTileTheme.of], which returns the nearest [ListTileTheme]'s [ListTileThemeData].

### textColor

```dart
Color? textColor
```

Defines the text color for the [title], [subtitle], [leading], and [trailing].

If this property is null and [selected] is false then [ListTileThemeData.textColor] is used. If that is also null then default text color is used for the [title], [subtitle] [leading], and [trailing]. Except for [subtitle], if [ThemeData.useMaterial3] is false, [TextTheme.bodySmall] is used.

If this property is null and [selected] is true then [ListTileThemeData.selectedColor] is used. If that is also null then [ColorScheme.primary] is used.

If this color is a [WidgetStateColor] it will be resolved against [WidgetState.selected] and [WidgetState.disabled] states.

See also:

- [ListTileTheme.of], which returns the nearest [ListTileTheme]'s [ListTileThemeData].

### titleTextStyle

```dart
TextStyle? titleTextStyle
```

The text style for ListTile's [title].

If this property is null, then [ListTileThemeData.titleTextStyle] is used. If that is also null and [ThemeData.useMaterial3] is true, [TextTheme.bodyLarge] with [ColorScheme.onSurface] will be used. Otherwise, If ListTile style is [ListTileStyle.list], [TextTheme.titleMedium] will be used and if ListTile style is [ListTileStyle.drawer], [TextTheme.bodyLarge] will be used.

### subtitleTextStyle

```dart
TextStyle? subtitleTextStyle
```

The text style for ListTile's [subtitle].

If this property is null, then [ListTileThemeData.subtitleTextStyle] is used. If that is also null and [ThemeData.useMaterial3] is true, [TextTheme.bodyMedium] with [ColorScheme.onSurfaceVariant] will be used, otherwise [TextTheme.bodyMedium] with [TextTheme.bodySmall] color will be used.

### leadingAndTrailingTextStyle

```dart
TextStyle? leadingAndTrailingTextStyle
```

The text style for ListTile's [leading] and [trailing].

If this property is null, then [ListTileThemeData.leadingAndTrailingTextStyle] is used. If that is also null and [ThemeData.useMaterial3] is true, [TextTheme.labelSmall] with [ColorScheme.onSurfaceVariant] will be used, otherwise [TextTheme.bodyMedium] will be used.

### style

```dart
ListTileStyle? style
```

Defines the font used for the [title].

If this property is null then [ListTileThemeData.style] is used. If that is also null then [ListTileStyle.list] is used.

See also:

- [ListTileTheme.of], which returns the nearest [ListTileTheme]'s [ListTileThemeData].

### contentPadding

```dart
EdgeInsetsGeometry? contentPadding
```

The tile's internal padding.

Insets a [ListTile]'s contents: its [leading], [title], [subtitle], and [trailing] widgets.

If this property is null, then [ListTileThemeData.contentPadding] is used. If that is also null and [ThemeData.useMaterial3] is true, then a default value of `EdgeInsetsDirectional.only(start: 16.0, end: 24.0)` will be used. Otherwise, a default value of `EdgeInsets.symmetric(horizontal: 16.0)` will be used.

### enabled

```dart
bool enabled
```

Whether this list tile is interactive.

If false, this list tile is styled with the disabled color from the current [Theme] and the [onTap] and [onLongPress] callbacks are inoperative.

### onTap

```dart
GestureTapCallback? onTap
```

Called when the user taps this list tile.

Inoperative if [enabled] is false.

### onLongPress

```dart
GestureLongPressCallback? onLongPress
```

Called when the user long-presses on this list tile.

Inoperative if [enabled] is false.

### onFocusChange

```dart
ValueChanged<bool>? onFocusChange
```

{@macro flutter.material.inkwell.onFocusChange}

### mouseCursor

```dart
MouseCursor? mouseCursor
```

{@template flutter.material.ListTile.mouseCursor} The cursor for a mouse pointer when it enters or is hovering over the widget.

If [mouseCursor] is a [WidgetStateMouseCursor], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.selected].
- [WidgetState.disabled]. {@endtemplate}

If null, then the value of [ListTileThemeData.mouseCursor] is used. If that is also null, then [WidgetStateMouseCursor.clickable] is used.

### selected

```dart
bool selected
```

If this tile is also [enabled] then icons and text are rendered with the same color.

By default the selected color is the theme's primary color. The selected color can be overridden with a [ListTileTheme].

{@tool dartpad} Here is an example of using a [StatefulWidget] to keep track of the selected index, and using that to set the [selected] property on the corresponding [ListTile].

** See code in examples/api/lib/material/list_tile/list_tile.selected.0.dart ** {@end-tool}

### focusColor

```dart
Color? focusColor
```

The color for the tile's [Material] when it has the input focus.

### hoverColor

```dart
Color? hoverColor
```

The color for the tile's [Material] when a pointer is hovering over it.

### splashColor

```dart
Color? splashColor
```

The color of splash for the tile's [Material].

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.Focus.autofocus}

### tileColor

```dart
Color? tileColor
```

{@template flutter.material.ListTile.tileColor} Defines the background color of `ListTile` when [selected] is false.

If this property is null and [selected] is false then [ListTileThemeData.tileColor] is used. If that is also null and [selected] is true, [selectedTileColor] is used. When that is also null, the [ListTileTheme.selectedTileColor] is used, otherwise [Colors.transparent] is used.

{@endtemplate}

### selectedTileColor

```dart
Color? selectedTileColor
```

Defines the background color of `ListTile` when [selected] is true.

When the value if null, the [selectedTileColor] is set to [ListTileTheme.selectedTileColor] if it's not null and to [Colors.transparent] if it's null.

### enableFeedback

```dart
bool? enableFeedback
```

{@template flutter.material.ListTile.enableFeedback} Whether detected gestures should provide acoustic and/or haptic feedback.

For example, on Android a tap will produce a clicking sound and a long-press will produce a short vibration, when feedback is enabled.

When null, the default value is true. {@endtemplate}

See also:

- [Feedback] for providing platform-specific feedback to certain actions.

### horizontalTitleGap

```dart
double? horizontalTitleGap
```

{@template flutter.material.ListTile.horizontalTitleGap} The horizontal gap between the titles and the leading/trailing widgets.

If null, then the value of [ListTileTheme.horizontalTitleGap] is used. If that is also null, then a default value of 16 is used. {@endtemplate}

### minVerticalPadding

```dart
double? minVerticalPadding
```

{@template flutter.material.ListTile.minVerticalPadding} The minimum padding on the top and bottom of the title and subtitle widgets.

If null, then the value of [ListTileTheme.minVerticalPadding] is used. If that is also null, then a default value of 4 is used. {@endtemplate}

### minLeadingWidth

```dart
double? minLeadingWidth
```

{@template flutter.material.ListTile.minLeadingWidth} The minimum width allocated for the [ListTile.leading] widget.

If null, then the value of [ListTileTheme.minLeadingWidth] is used. If that is also null, then a default value of 40 is used. {@endtemplate}

### minTileHeight

```dart
double? minTileHeight
```

{@template flutter.material.ListTile.minTileHeight} The minimum height allocated for the [ListTile] widget.

If this is null, default tile heights are 56.0, 72.0, and 88.0 for one, two, and three lines of text respectively. If `isDense` is true, these defaults are changed to 48.0, 64.0, and 76.0. A visual density value or a large title will also adjust the default tile heights. {@endtemplate}

### titleAlignment

```dart
ListTileTitleAlignment? titleAlignment
```

Defines how [ListTile.leading] and [ListTile.trailing] are vertically aligned relative to the [ListTile]'s titles ([ListTile.title] and [ListTile.subtitle]).

If this property is null then [ListTileThemeData.titleAlignment] is used. If that is also null then [ListTileTitleAlignment.threeLine] is used.

See also:

- [ListTileTheme.of], which returns the nearest [ListTileTheme]'s [ListTileThemeData].

### internalAddSemanticForOnTap

```dart
bool internalAddSemanticForOnTap
```

Whether to add button:true to the semantics if onTap is provided. This is a temporary flag to help changing the behavior of ListTile onTap semantics.

### statesController

```dart
MaterialStatesController? statesController
```

{@macro flutter.material.inkwell.statesController}

### divideTiles()

```dart
Iterable<Widget> divideTiles({BuildContext? context, required Iterable<Widget> tiles, Color? color})
```

Add a one pixel border in between each tile. If color isn't specified the [ThemeData.dividerColor] of the context's [Theme] is used.

See also:

- [Divider], which you can use to obtain this effect manually.

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
