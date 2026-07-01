@docImport 'route.dart'; @docImport 'text_theme.dart';

# CupertinoPicker

```dart
class CupertinoPicker extends StatefulWidget {}
```

An iOS-styled picker.

Displays its children widgets on a wheel for selection and calls back when the currently selected item changes.

By default, the first child in `children` will be the initially selected child. The index of a different child can be specified in [scrollController], to make that child the initially selected child.

Can be used with [showCupertinoModalPopup] to display the picker modally at the bottom of the screen. When calling [showCupertinoModalPopup], be sure to set `semanticsDismissible` to true to enable dismissing the modal via semantics.

Sizes itself to its parent. All children are sized to the same size based on [itemExtent].

By default, descendent texts are shown with [CupertinoTextThemeData.pickerTextStyle].

{@tool dartpad} This example shows a [CupertinoPicker] that displays a list of fruits on a wheel for selection.

** See code in examples/api/lib/cupertino/picker/cupertino_picker.0.dart ** {@end-tool}

See also:

- [ListWheelScrollView], the generic widget backing this picker without the iOS design specific chrome.
- <https://developer.apple.com/design/human-interface-guidelines/pickers/>

### CupertinoPicker()

```dart
CupertinoPicker({dynamic key, double diameterRatio = _kDefaultDiameterRatio, Color? backgroundColor, double offAxisFraction = 0.0, bool useMagnifier = false, double magnification = 1.0, FixedExtentScrollController? scrollController, double squeeze = _kSqueeze, ChangeReportingBehavior changeReportingBehavior = ChangeReportingBehavior.onScrollUpdate, required double itemExtent, required ValueChanged<int>? onSelectedItemChanged, required List<Widget> children, Widget? selectionOverlay = const CupertinoPickerDefaultSelectionOverlay(), bool looping = false})
```

Creates a picker from a concrete list of children.

The [itemExtent] must be greater than zero.

The [backgroundColor] defaults to null, which disables background painting entirely. (i.e. the picker is going to have a completely transparent background), to match the native UIPicker and UIDatePicker. Also, if it has transparency, no gradient effect will be rendered.

The [scrollController] argument can be used to specify a custom [FixedExtentScrollController] for programmatically reading or changing the current picker index or for selecting an initial index value.

The [looping] argument decides whether the child list loops and can be scrolled infinitely. If set to true, scrolling past the end of the list will loop the list back to the beginning. If set to false, the list will stop scrolling when you reach the end or the beginning.

### CupertinoPicker.builder()

```dart
CupertinoPicker.builder({dynamic key, double diameterRatio = _kDefaultDiameterRatio, Color? backgroundColor, double offAxisFraction = 0.0, bool useMagnifier = false, double magnification = 1.0, FixedExtentScrollController? scrollController, double squeeze = _kSqueeze, ChangeReportingBehavior changeReportingBehavior = ChangeReportingBehavior.onScrollUpdate, required double itemExtent, required ValueChanged<int>? onSelectedItemChanged, required NullableIndexedWidgetBuilder itemBuilder, int? childCount, Widget? selectionOverlay = const CupertinoPickerDefaultSelectionOverlay()})
```

Creates a picker from an [IndexedWidgetBuilder] callback where the builder is dynamically invoked during layout.

A child is lazily created when it starts becoming visible in the viewport. All of the children provided by the builder are cached and reused, so normally the builder is only called once for each index (except when rebuilding - the cache is cleared).

The [childCount] argument reflects the number of children that will be provided by the [itemBuilder]. {@macro flutter.widgets.ListWheelChildBuilderDelegate.childCount}

The [itemExtent] argument must be positive.

The [backgroundColor] defaults to null, which disables background painting entirely. (i.e. the picker is going to have a completely transparent background), to match the native UIPicker and UIDatePicker.

### diameterRatio

```dart
double diameterRatio
```

Relative ratio between this picker's height and the simulated cylinder's diameter.

Smaller values creates more pronounced curvatures in the scrollable wheel.

For more details, see [ListWheelScrollView.diameterRatio].

Defaults to 1.1 to visually mimic iOS.

### backgroundColor

```dart
Color? backgroundColor
```

Background color behind the children.

Defaults to null, which disables background painting entirely. (i.e. the picker is going to have a completely transparent background), to match the native UIPicker and UIDatePicker.

Any alpha value less 255 (fully opaque) will cause the removal of the wheel list edge fade gradient from rendering of the widget.

### offAxisFraction

```dart
double offAxisFraction
```

{@macro flutter.rendering.RenderListWheelViewport.offAxisFraction}

### useMagnifier

```dart
bool useMagnifier
```

{@macro flutter.rendering.RenderListWheelViewport.useMagnifier}

### magnification

```dart
double magnification
```

{@macro flutter.rendering.RenderListWheelViewport.magnification}

### scrollController

```dart
FixedExtentScrollController? scrollController
```

A [FixedExtentScrollController] to read and control the current item, and to set the initial item.

If null, an implicit one will be created internally.

### itemExtent

```dart
double itemExtent
```

{@template flutter.cupertino.picker.itemExtent} The uniform height of all children.

All children will be given the [BoxConstraints] to match this exact height. Must be a positive value. {@endtemplate}

### squeeze

```dart
double squeeze
```

{@macro flutter.rendering.RenderListWheelViewport.squeeze}

Defaults to `1.45` to visually mimic iOS.

### changeReportingBehavior

```dart
ChangeReportingBehavior changeReportingBehavior
```

The behavior of reporting the selected item index.

This determines when the [onSelectedItemChanged] callback is called.

Native iOS 18 behavior is [ChangeReportingBehavior.onScrollEnd], which calls the callback only when the scrolling stops.

Defaults to [ChangeReportingBehavior.onScrollUpdate].

### onSelectedItemChanged

```dart
ValueChanged<int>? onSelectedItemChanged
```

Called when the selected item changes.

The timing of this callback is controlled by [changeReportingBehavior].

### childDelegate

```dart
ListWheelChildDelegate childDelegate
```

A delegate that lazily instantiates children.

### selectionOverlay

```dart
Widget? selectionOverlay
```

A widget overlaid on the picker to highlight the currently selected entry.

The [selectionOverlay] widget drawn above the [CupertinoPicker]'s picker wheel. It is vertically centered in the picker and is constrained to have the same height as the center row.

If unspecified, it defaults to a [CupertinoPickerDefaultSelectionOverlay] which is a gray rounded rectangle overlay in iOS 14 style. This property can be set to null to remove the overlay.

### createState()

```dart
State<StatefulWidget> createState()
```

# CupertinoPickerDefaultSelectionOverlay

```dart
class CupertinoPickerDefaultSelectionOverlay extends StatelessWidget {}
```

A default selection overlay for [CupertinoPicker]s.

It draws a gray rounded rectangle to match the picker visuals introduced in iOS 14.

This widget is typically only used in [CupertinoPicker.selectionOverlay]. In an iOS 14 multi-column picker, the selection overlay is a single rounded rectangle that spans the entire multi-column picker. To achieve the same effect using [CupertinoPickerDefaultSelectionOverlay], the additional margin and corner radii on the left or the right side can be disabled by turning off [capStartEdge] and [capEndEdge], so this selection overlay visually connects with selection overlays of adjoining [CupertinoPicker]s (i.e., other "column"s).

See also:

- [CupertinoPicker], which uses this widget as its default [CupertinoPicker.selectionOverlay].

### CupertinoPickerDefaultSelectionOverlay()

```dart
CupertinoPickerDefaultSelectionOverlay({dynamic key, Color background = CupertinoColors.tertiarySystemFill, bool capStartEdge = true, bool capEndEdge = true})
```

Creates an iOS 14 style selection overlay that highlights the magnified area (or the currently selected item, depending on how you described it elsewhere) of a [CupertinoPicker].

The [background] argument default value is [CupertinoColors.tertiarySystemFill].

The [capStartEdge] and [capEndEdge] arguments decide whether to add a default margin and use rounded corners on the left and right side of the rectangular overlay, and they both default to true.

### capStartEdge

```dart
bool capStartEdge
```

Whether to use the default use rounded corners and margin on the start side.

### capEndEdge

```dart
bool capEndEdge
```

Whether to use the default use rounded corners and margin on the end side.

### background

```dart
Color background
```

The color to fill in the background of the [CupertinoPickerDefaultSelectionOverlay]. It Support for use [CupertinoDynamicColor].

Typically this should not be set to a fully opaque color, as the currently selected item of the underlying [CupertinoPicker] should remain visible. Defaults to [CupertinoColors.tertiarySystemFill].

### build()

```dart
Widget build(BuildContext context)
```
