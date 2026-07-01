@docImport 'app.dart'; @docImport 'material_localizations.dart'; @docImport 'selectable_text.dart';

# SelectionArea

```dart
class SelectionArea extends StatefulWidget {}
```

A widget that introduces an area for user selections with adaptive selection controls.

This widget creates a [SelectableRegion] with platform-adaptive selection controls.

Flutter widgets are not selectable by default. To enable selection for a specific screen, consider wrapping the body of the [Route] with a [SelectionArea].

The [SelectionArea] widget must have a [Localizations] ancestor that contains a [MaterialLocalizations] delegate; using the [MaterialApp] widget ensures that such an ancestor is present.

{@tool dartpad} This example shows how to make a screen selectable.

** See code in examples/api/lib/material/selection_area/selection_area.0.dart ** {@end-tool}

See also:

- [SelectableRegion], which provides an overview of the selection system.
- [SelectableText], which enables selection on a single run of text.
- [SelectionListener], which enables accessing the [SelectionDetails] of the selectable subtree it wraps.

### SelectionArea()

```dart
SelectionArea({dynamic key, FocusNode? focusNode, TextSelectionControls? selectionControls, SelectableRegionContextMenuBuilder? contextMenuBuilder = _defaultContextMenuBuilder, TextMagnifierConfiguration? magnifierConfiguration, ValueChanged<SelectedContent?>? onSelectionChanged, required Widget child})
```

Creates a [SelectionArea].

If [selectionControls] is null, a platform specific one is used.

### magnifierConfiguration

```dart
TextMagnifierConfiguration? magnifierConfiguration
```

The configuration for the magnifier in the selection region.

By default, builds a [CupertinoTextMagnifier] on iOS and [TextMagnifier] on Android, and builds nothing on all other platforms. To suppress the magnifier, consider passing [TextMagnifierConfiguration.disabled].

{@macro flutter.widgets.magnifier.intro}

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### selectionControls

```dart
TextSelectionControls? selectionControls
```

The delegate to build the selection handles and toolbar.

If it is null, the platform specific selection control is used.

### contextMenuBuilder

```dart
SelectableRegionContextMenuBuilder? contextMenuBuilder
```

{@macro flutter.widgets.EditableText.contextMenuBuilder}

If not provided, will build a default menu based on the ambient [ThemeData.platform].

{@tool dartpad} This example shows how to build a custom context menu for any selected content in a SelectionArea.

** See code in examples/api/lib/material/context_menu/selectable_region_toolbar_builder.0.dart ** {@end-tool}

See also:

- [AdaptiveTextSelectionToolbar], which is built by default.

### onSelectionChanged

```dart
ValueChanged<SelectedContent?>? onSelectionChanged
```

Called when the selected content changes.

### child

```dart
Widget child
```

The child widget this selection area applies to.

{@macro flutter.widgets.ProxyWidget.child}

### createState()

```dart
State<StatefulWidget> createState()
```

# SelectionAreaState

```dart
class SelectionAreaState extends State<SelectionArea> {}
```

State for a [SelectionArea].

### selectableRegion

```dart
SelectableRegionState get selectableRegion
```

The [State] of the [SelectableRegion] for which this [SelectionArea] wraps.

### build()

```dart
Widget build(BuildContext context)
```
