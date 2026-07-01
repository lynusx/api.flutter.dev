@docImport 'color_scheme.dart'; @docImport 'scaffold.dart'; @docImport 'selection_area.dart'; @docImport 'text_field.dart';

# iOSHorizontalOffset

```dart
int iOSHorizontalOffset
```

An eyeballed value that moves the cursor slightly left of where it is rendered for text on Android so its positioning more accurately matches the native iOS text cursor positioning.

This value is in device pixels, not logical pixels as is typically used throughout the codebase.

# SelectableText

```dart
class SelectableText extends StatefulWidget {}
```

A run of selectable text with a single style.

Consider using [SelectionArea] or [SelectableRegion] instead, which enable selection on a widget subtree, including but not limited to [Text] widgets.

The [SelectableText] widget displays a string of text with a single style. The string might break across multiple lines or might all be displayed on the same line depending on the layout constraints.

{@youtube 560 315 https://www.youtube.com/watch?v=ZSU3ZXOs6hc}

The [style] argument is optional. When omitted, the text will use the style from the closest enclosing [DefaultTextStyle]. If the given style's [TextStyle.inherit] property is true (the default), the given style will be merged with the closest enclosing [DefaultTextStyle]. This merging behavior is useful, for example, to make the text bold while using the default font family and size.

{@macro flutter.material.textfield.wantKeepAlive}

{@tool snippet}

```dart
const SelectableText(
  'Hello! How are you?',
  textAlign: TextAlign.center,
  style: TextStyle(fontWeight: FontWeight.bold),
)
```

{@end-tool}

Using the [SelectableText.rich] constructor, the [SelectableText] widget can display a paragraph with differently styled [TextSpan]s. The sample that follows displays "Hello beautiful world" with different styles for each word.

{@tool snippet}

```dart
const SelectableText.rich(
  TextSpan(
    text: 'Hello', // default text style
    children: <TextSpan>[
      TextSpan(text: ' beautiful ', style: TextStyle(fontStyle: FontStyle.italic)),
      TextSpan(text: 'world', style: TextStyle(fontWeight: FontWeight.bold)),
    ],
  ),
)
```

{@end-tool}

## Interactivity

To make [SelectableText] react to touch events, use callback [onTap] to achieve the desired behavior.

## Scrolling Considerations

If this [SelectableText] is not a descendant of [Scaffold] and is being used within a [Scrollable] or nested [Scrollable]s, consider placing a [ScrollNotificationObserver] above the root [Scrollable] that contains this [SelectableText] to ensure proper scroll coordination for [SelectableText] and its components like [TextSelectionOverlay].

See also:

- [Text], which is the non selectable version of this widget.
- [TextField], which is the editable version of this widget.
- [SelectionArea], which enables the selection of multiple [Text] widgets and of other widgets.

### SelectableText()

```dart
SelectableText(String? data, {dynamic key, FocusNode? focusNode, TextStyle? style, StrutStyle? strutStyle, TextAlign? textAlign, TextDirection? textDirection, double? textScaleFactor, TextScaler? textScaler, bool showCursor = false, bool autofocus = false, ToolbarOptions? toolbarOptions, int? minLines, int? maxLines, double cursorWidth = 2.0, double? cursorHeight, Radius? cursorRadius, Color? cursorColor, Color? selectionColor, ui.BoxHeightStyle? selectionHeightStyle, ui.BoxWidthStyle? selectionWidthStyle, DragStartBehavior dragStartBehavior = DragStartBehavior.start, bool enableInteractiveSelection = true, TextSelectionControls? selectionControls, GestureTapCallback? onTap, ScrollPhysics? scrollPhysics, ScrollBehavior? scrollBehavior, String? semanticsLabel, TextHeightBehavior? textHeightBehavior, TextWidthBasis? textWidthBasis, SelectionChangedCallback? onSelectionChanged, EditableTextContextMenuBuilder? contextMenuBuilder = _defaultContextMenuBuilder, TextMagnifierConfiguration? magnifierConfiguration})
```

Creates a selectable text widget.

If the [style] argument is null, the text will use the style from the closest enclosing [DefaultTextStyle].

If the [showCursor], [autofocus], [dragStartBehavior], [selectionHeightStyle], [selectionWidthStyle] and [data] arguments are specified, the [maxLines] argument must be greater than zero.

### SelectableText.rich()

```dart
SelectableText.rich(TextSpan? textSpan, {dynamic key, FocusNode? focusNode, TextStyle? style, StrutStyle? strutStyle, TextAlign? textAlign, TextDirection? textDirection, double? textScaleFactor, TextScaler? textScaler, bool showCursor = false, bool autofocus = false, ToolbarOptions? toolbarOptions, int? minLines, int? maxLines, double cursorWidth = 2.0, double? cursorHeight, Radius? cursorRadius, Color? cursorColor, Color? selectionColor, ui.BoxHeightStyle? selectionHeightStyle, ui.BoxWidthStyle? selectionWidthStyle, DragStartBehavior dragStartBehavior = DragStartBehavior.start, bool enableInteractiveSelection = true, TextSelectionControls? selectionControls, GestureTapCallback? onTap, ScrollPhysics? scrollPhysics, ScrollBehavior? scrollBehavior, String? semanticsLabel, TextHeightBehavior? textHeightBehavior, TextWidthBasis? textWidthBasis, SelectionChangedCallback? onSelectionChanged, EditableTextContextMenuBuilder? contextMenuBuilder = _defaultContextMenuBuilder, TextMagnifierConfiguration? magnifierConfiguration})
```

Creates a selectable text widget with a [TextSpan].

The [TextSpan.children] attribute of the [textSpan] parameter must only contain [TextSpan]s. Other types of [InlineSpan] are not allowed.

### data

```dart
String? data
```

The text to display.

This will be null if a [textSpan] is provided instead.

### textSpan

```dart
TextSpan? textSpan
```

The text to display as a [TextSpan].

This will be null if [data] is provided instead.

### focusNode

```dart
FocusNode? focusNode
```

Defines the focus for this widget.

Text is only selectable when widget is focused.

The [focusNode] is a long-lived object that's typically managed by a [StatefulWidget] parent. See [FocusNode] for more information.

To give the focus to this widget, provide a [focusNode] and then use the current [FocusScope] to request the focus:

```dart
FocusScope.of(context).requestFocus(myFocusNode);
```

This happens automatically when the widget is tapped.

To be notified when the widget gains or loses the focus, add a listener to the [focusNode]:

```dart
myFocusNode.addListener(() { print(myFocusNode.hasFocus); });
```

If null, this widget will create its own [FocusNode] with [FocusNode.skipTraversal] parameter set to `true`, which causes the widget to be skipped over during focus traversal.

### style

```dart
TextStyle? style
```

The style to use for the text.

If null, defaults [DefaultTextStyle] of context.

### strutStyle

```dart
StrutStyle? strutStyle
```

{@macro flutter.widgets.editableText.strutStyle}

### textAlign

```dart
TextAlign? textAlign
```

{@macro flutter.widgets.editableText.textAlign}

### textDirection

```dart
TextDirection? textDirection
```

{@macro flutter.widgets.editableText.textDirection}

### textScaleFactor

```dart
double? textScaleFactor
```

{@macro flutter.widgets.editableText.textScaleFactor}

### textScaler

```dart
TextScaler? textScaler
```

{@macro flutter.painting.textPainter.textScaler}

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.editableText.autofocus}

### minLines

```dart
int? minLines
```

{@macro flutter.widgets.editableText.minLines}

### maxLines

```dart
int? maxLines
```

{@macro flutter.widgets.editableText.maxLines}

### showCursor

```dart
bool showCursor
```

{@macro flutter.widgets.editableText.showCursor}

### cursorWidth

```dart
double cursorWidth
```

{@macro flutter.widgets.editableText.cursorWidth}

### cursorHeight

```dart
double? cursorHeight
```

{@macro flutter.widgets.editableText.cursorHeight}

### cursorRadius

```dart
Radius? cursorRadius
```

{@macro flutter.widgets.editableText.cursorRadius}

### cursorColor

```dart
Color? cursorColor
```

The color of the cursor.

The cursor indicates the current text insertion point.

If null then [DefaultSelectionStyle.cursorColor] is used. If that is also null and [ThemeData.platform] is [TargetPlatform.iOS] or [TargetPlatform.macOS], then [CupertinoThemeData.primaryColor] is used. Otherwise [ColorScheme.primary] of [ThemeData.colorScheme] is used.

### selectionColor

```dart
Color? selectionColor
```

The color to use when painting the selection.

If this property is null, this widget gets the selection color from the inherited [DefaultSelectionStyle] (if any); if none, the selection color is derived from the [CupertinoThemeData.primaryColor] on Apple platforms and [ColorScheme.primary] of [ThemeData.colorScheme] on other platforms.

### selectionHeightStyle

```dart
ui.BoxHeightStyle? selectionHeightStyle
```

Controls how tall the selection highlight boxes are computed to be.

See [ui.BoxHeightStyle] for details on available styles.

### selectionWidthStyle

```dart
ui.BoxWidthStyle? selectionWidthStyle
```

Controls how wide the selection highlight boxes are computed to be.

See [ui.BoxWidthStyle] for details on available styles.

### enableInteractiveSelection

```dart
bool enableInteractiveSelection
```

{@macro flutter.widgets.editableText.enableInteractiveSelection}

### selectionControls

```dart
TextSelectionControls? selectionControls
```

{@macro flutter.widgets.editableText.selectionControls}

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.widgets.scrollable.dragStartBehavior}

### toolbarOptions

```dart
ToolbarOptions? toolbarOptions
```

Configuration of toolbar options.

Paste and cut will be disabled regardless.

If not set, select all and copy will be enabled by default.

### selectionEnabled

```dart
bool get selectionEnabled
```

{@macro flutter.widgets.editableText.selectionEnabled}

### onTap

```dart
GestureTapCallback? onTap
```

Called when the user taps on this selectable text.

The selectable text builds a [GestureDetector] to handle input events like tap, to trigger focus requests, to move the caret, adjust the selection, etc. Handling some of those events by wrapping the selectable text with a competing GestureDetector is problematic.

To unconditionally handle taps, without interfering with the selectable text's internal gesture detector, provide this callback.

To be notified when the text field gains or loses the focus, provide a [focusNode] and add a listener to that.

To listen to arbitrary pointer events without competing with the selectable text's internal gesture detector, use a [Listener].

### scrollPhysics

```dart
ScrollPhysics? scrollPhysics
```

{@macro flutter.widgets.editableText.scrollPhysics}

### scrollBehavior

```dart
ScrollBehavior? scrollBehavior
```

{@macro flutter.widgets.editableText.scrollBehavior}

### semanticsLabel

```dart
String? semanticsLabel
```

{@macro flutter.widgets.Text.semanticsLabel}

### textHeightBehavior

```dart
TextHeightBehavior? textHeightBehavior
```

{@macro dart.ui.textHeightBehavior}

### textWidthBasis

```dart
TextWidthBasis? textWidthBasis
```

{@macro flutter.painting.textPainter.textWidthBasis}

### onSelectionChanged

```dart
SelectionChangedCallback? onSelectionChanged
```

{@macro flutter.widgets.editableText.onSelectionChanged}

### contextMenuBuilder

```dart
EditableTextContextMenuBuilder? contextMenuBuilder
```

{@macro flutter.widgets.EditableText.contextMenuBuilder}

### magnifierConfiguration

```dart
TextMagnifierConfiguration? magnifierConfiguration
```

The configuration for the magnifier used when the text is selected.

By default, builds a [CupertinoTextMagnifier] on iOS and [TextMagnifier] on Android, and builds nothing on all other platforms. To suppress the magnifier, consider passing [TextMagnifierConfiguration.disabled].

{@macro flutter.widgets.magnifier.intro}

### createState()

```dart
State<SelectableText> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
