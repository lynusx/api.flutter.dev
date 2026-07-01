@docImport 'divider_theme.dart';

# ExpansionPanelCallback

```dart
typedef ExpansionPanelCallback = void Function(int panelIndex, bool isExpanded)
```

Signature for the callback that's called when an [ExpansionPanel] is expanded or collapsed.

The position of the panel within an [ExpansionPanelList] is given by [panelIndex].

# ExpansionPanelHeaderBuilder

```dart
typedef ExpansionPanelHeaderBuilder = Widget Function(BuildContext context, bool isExpanded)
```

Signature for the callback that's called when the header of the [ExpansionPanel] needs to rebuild.

# ExpansionPanel

```dart
class ExpansionPanel {}
```

A material expansion panel. It has a header and a body and can be either expanded or collapsed. The body of the panel is only visible when it is expanded.

{@youtube 560 315 https://www.youtube.com/watch?v=2aJZzRMziJc}

Expansion panels are only intended to be used as children for [ExpansionPanelList].

See [ExpansionPanelList] for a sample implementation.

See also:

- [ExpansionPanelList]
- <https://material.io/design/components/lists.html#types>

### ExpansionPanel()

```dart
ExpansionPanel({required ExpansionPanelHeaderBuilder headerBuilder, required Widget body, bool isExpanded = false, bool canTapOnHeader = false, Color? backgroundColor, Color? splashColor, Color? highlightColor})
```

Creates an expansion panel to be used as a child for [ExpansionPanelList]. See [ExpansionPanelList] for an example on how to use this widget.

### headerBuilder

```dart
ExpansionPanelHeaderBuilder headerBuilder
```

The widget builder that builds the expansion panels' header.

### body

```dart
Widget body
```

The body of the expansion panel that's displayed below the header.

This widget is visible only when the panel is expanded.

### isExpanded

```dart
bool isExpanded
```

Whether the panel is expanded.

Defaults to false.

### splashColor

```dart
Color? splashColor
```

Defines the splash color of the panel if [canTapOnHeader] is true, or the splash color of the expand/collapse IconButton if [canTapOnHeader] is false.

If [canTapOnHeader] is false, and [ThemeData.useMaterial3] is true, this field will be ignored, as [IconButton.splashColor] will be ignored, and you should use [highlightColor] instead.

If this is null, then the icon button will use its default splash color [ThemeData.splashColor], and the panel will use its default splash color [ThemeData.splashColor] (if [canTapOnHeader] is true).

### highlightColor

```dart
Color? highlightColor
```

Defines the highlight color of the panel if [canTapOnHeader] is true, or the highlight color of the expand/collapse IconButton if [canTapOnHeader] is false.

If this is null, then the icon button will use its default highlight color [ThemeData.highlightColor], and the panel will use its default highlight color [ThemeData.highlightColor] (if [canTapOnHeader] is true).

### canTapOnHeader

```dart
bool canTapOnHeader
```

Whether tapping on the panel's header will expand/collapse it.

Defaults to false.

### backgroundColor

```dart
Color? backgroundColor
```

Defines the background color of the panel.

Defaults to [ThemeData.cardColor].

# ExpansionPanelRadio

```dart
class ExpansionPanelRadio extends ExpansionPanel {}
```

An expansion panel that allows for radio-like functionality. This means that at any given time, at most, one [ExpansionPanelRadio] can remain expanded.

A unique identifier [value] must be assigned to each panel. This identifier allows the [ExpansionPanelList] to determine which [ExpansionPanelRadio] instance should be expanded.

See [ExpansionPanelList.radio] for a sample implementation.

### ExpansionPanelRadio()

```dart
ExpansionPanelRadio({required Object value, required InvalidType Function(InvalidType, bool) headerBuilder, required dynamic body, bool canTapOnHeader, dynamic backgroundColor, dynamic splashColor, dynamic highlightColor})
```

An expansion panel that allows for radio functionality.

A unique [value] must be passed into the constructor.

### value

```dart
Object value
```

The value that uniquely identifies a radio panel so that the currently selected radio panel can be identified.

# ExpansionPanelList

```dart
class ExpansionPanelList extends StatefulWidget {}
```

A material expansion panel list that lays out its children and animates expansions.

The [expansionCallback] is called when the expansion state changes. For normal [ExpansionPanelList] widgets, it is the responsibility of the parent widget to rebuild the [ExpansionPanelList] with updated values for [ExpansionPanel.isExpanded]. For [ExpansionPanelList.radio] widgets, the open state is tracked internally and the callback is invoked both for the previously open panel, which is closing, and the previously closed panel, which is opening.

{@tool dartpad} Here is a simple example of how to use [ExpansionPanelList].

** See code in examples/api/lib/material/expansion_panel/expansion_panel_list.0.dart ** {@end-tool}

See also:

- [ExpansionPanel], which is used in the [children] property.
- [ExpansionPanelList.radio], a variant of this widget where only one panel is open at a time.
- <https://material.io/design/components/lists.html#types>

### ExpansionPanelList()

```dart
ExpansionPanelList({dynamic key, List<ExpansionPanel> children = const <ExpansionPanel>[], ExpansionPanelCallback? expansionCallback, Duration animationDuration = kThemeAnimationDuration, EdgeInsets expandedHeaderPadding = _kPanelHeaderExpandedDefaultPadding, Color? dividerColor, double elevation = 2, Color? expandIconColor, double materialGapSize = 16.0})
```

Creates an expansion panel list widget. The [expansionCallback] is triggered when an expansion panel expand/collapse button is pushed.

### ExpansionPanelList.radio()

```dart
ExpansionPanelList.radio({dynamic key, List<ExpansionPanel> children = const <ExpansionPanelRadio>[], ExpansionPanelCallback? expansionCallback, Duration animationDuration = kThemeAnimationDuration, Object? initialOpenPanelValue, EdgeInsets expandedHeaderPadding = _kPanelHeaderExpandedDefaultPadding, Color? dividerColor, double elevation = 2, Color? expandIconColor, double materialGapSize = 16.0})
```

Creates a radio expansion panel list widget.

This widget allows for at most one panel in the list to be open. The expansion panel callback is triggered when an expansion panel expand/collapse button is pushed. The [children] objects must be instances of [ExpansionPanelRadio].

{@tool dartpad} Here is a simple example of how to implement ExpansionPanelList.radio.

** See code in examples/api/lib/material/expansion_panel/expansion_panel_list.expansion_panel_list_radio.0.dart ** {@end-tool}

### children

```dart
List<ExpansionPanel> children
```

The children of the expansion panel list. They are laid out in a similar fashion to [ListBody].

### expansionCallback

```dart
ExpansionPanelCallback? expansionCallback
```

The callback that gets called whenever one of the expand/collapse buttons is pressed. The arguments passed to the callback are the index of the pressed panel and whether the panel is currently expanded or not.

If [ExpansionPanelList.radio] is used, the callback may be called a second time if a different panel was previously open. The arguments passed to the second callback are the index of the panel that will close and false, marking that it will be closed.

For [ExpansionPanelList], the callback should call [State.setState] when it is notified about the closing/opening panel. On the other hand, the callback for [ExpansionPanelList.radio] is intended to inform the parent widget of changes, as the radio panels' open/close states are managed internally.

This callback is useful in order to keep track of the expanded/collapsed panels in a parent widget that may need to react to these changes.

### animationDuration

```dart
Duration animationDuration
```

The duration of the expansion animation.

### initialOpenPanelValue

```dart
Object? initialOpenPanelValue
```

The value of the panel that initially begins open. (This value is only used when initializing with the [ExpansionPanelList.radio] constructor.)

### expandedHeaderPadding

```dart
EdgeInsets expandedHeaderPadding
```

The padding that surrounds the panel header when expanded.

By default, 16px of space is added to the header vertically (above and below) during expansion.

### dividerColor

```dart
Color? dividerColor
```

Defines color for the divider when [ExpansionPanel.isExpanded] is false.

If [dividerColor] is null, then [DividerThemeData.color] is used. If that is null, then [ThemeData.dividerColor] is used.

### elevation

```dart
double elevation
```

Defines elevation for the [ExpansionPanel] while it's expanded.

By default, the value of elevation is 2.

### expandIconColor

```dart
Color? expandIconColor
```

{@macro flutter.material.ExpandIcon.color}

### materialGapSize

```dart
double materialGapSize
```

Defines the [MaterialGap.size] of the [MaterialGap] which is placed between the [ExpansionPanelList.children] when they're expanded.

Defaults to `16.0`.

### createState()

```dart
State<StatefulWidget> createState()
```
