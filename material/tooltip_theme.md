@docImport 'app.dart'; @docImport 'tooltip.dart';

# TooltipThemeData

```dart
class TooltipThemeData with Diagnosticable {}
```

Defines default property values for descendant [Tooltip] widgets.

Descendant widgets obtain the current [TooltipThemeData] object using [TooltipTheme.of]. Instances of [TooltipThemeData] can be customized with [TooltipThemeData.copyWith].

Typically a [TooltipThemeData] is specified as part of the overall [Theme] with [ThemeData.tooltipTheme].

See also:

- [TooltipTheme], a widget which overrides the tooltip theme for a subtree.
- [ThemeData.tooltipTheme], which specifies a tooltip theme as part of an overall theme.
- [MaterialApp.theme], which specifies a theme for the whole application.

### TooltipThemeData()

```dart
TooltipThemeData({double? height, BoxConstraints? constraints, EdgeInsetsGeometry? padding, EdgeInsetsGeometry? margin, double? verticalOffset, bool? preferBelow, bool? excludeFromSemantics, Decoration? decoration, TextStyle? textStyle, TextAlign? textAlign, Duration? waitDuration, Duration? showDuration, Duration? exitDuration, TooltipTriggerMode? triggerMode, bool? enableFeedback})
```

Creates the set of properties used to configure [Tooltip]s.

### height

```dart
double? height
```

The minimum height of the [Tooltip]'s message.

### constraints

```dart
BoxConstraints? constraints
```

Constrains the size of the [Tooltip]'s message.

### padding

```dart
EdgeInsetsGeometry? padding
```

If provided, the amount of space by which to inset the [Tooltip]'s message.

### margin

```dart
EdgeInsetsGeometry? margin
```

If provided, the amount of empty space to surround the [Tooltip].

### verticalOffset

```dart
double? verticalOffset
```

The vertical gap between the widget and the displayed tooltip.

When [preferBelow] is set to true and tooltips have sufficient space to display themselves, this property defines how much vertical space tooltips will position themselves under their corresponding widgets. Otherwise, tooltips will position themselves above their corresponding widgets with the given offset.

### preferBelow

```dart
bool? preferBelow
```

Whether the tooltip is displayed below its widget by default.

If there is insufficient space to display the tooltip in the preferred direction, the tooltip will be displayed in the opposite direction.

Applying `false` for the entire app is recommended to avoid having a finger or cursor hide a tooltip.

### excludeFromSemantics

```dart
bool? excludeFromSemantics
```

Whether the [Tooltip.message] should be excluded from the semantics tree.

By default, [Tooltip]s will add a [Semantics] label that is set to [Tooltip.message]. Set this property to true if the app is going to provide its own custom semantics label.

### decoration

```dart
Decoration? decoration
```

The [Tooltip]'s shape and background color.

### textStyle

```dart
TextStyle? textStyle
```

The style to use for the message of [Tooltip]s.

### textAlign

```dart
TextAlign? textAlign
```

The [TextAlign] to use for the message of [Tooltip]s.

### waitDuration

```dart
Duration? waitDuration
```

The length of time that a pointer must hover over a tooltip's widget before the tooltip will be shown.

### showDuration

```dart
Duration? showDuration
```

The length of time that the tooltip will be shown once it has appeared.

### exitDuration

```dart
Duration? exitDuration
```

The length of time that a pointer must have stopped hovering over a tooltip's widget before the tooltip will be hidden.

### triggerMode

```dart
TooltipTriggerMode? triggerMode
```

The [TooltipTriggerMode] that will show the tooltip.

### enableFeedback

```dart
bool? enableFeedback
```

Whether the tooltip should provide acoustic and/or haptic feedback.

For example, on Android a tap will produce a clicking sound and a long-press will produce a short vibration, when feedback is enabled.

This value is used if [Tooltip.enableFeedback] is null. If this value is null, the default is true.

See also:

- [Feedback], for providing platform-specific feedback to certain actions.

### copyWith()

```dart
TooltipThemeData copyWith({double? height, BoxConstraints? constraints, EdgeInsetsGeometry? padding, EdgeInsetsGeometry? margin, double? verticalOffset, bool? preferBelow, bool? excludeFromSemantics, Decoration? decoration, TextStyle? textStyle, TextAlign? textAlign, Duration? waitDuration, Duration? showDuration, Duration? exitDuration, TooltipTriggerMode? triggerMode, bool? enableFeedback})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
TooltipThemeData? lerp(TooltipThemeData? a, TooltipThemeData? b, double t)
```

Linearly interpolate between two tooltip themes.

If both arguments are null, then null is returned.

{@macro dart.ui.shadow.lerp}

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# TooltipTheme

```dart
class TooltipTheme extends InheritedTheme {}
```

Applies a tooltip theme to descendant [Tooltip] widgets.

A tooltip theme describes the values to use for [Tooltip] properties that are not given an explicit non-null value.

Descendant widgets obtain the ambient tooltip theme, a [TooltipThemeData], using [TooltipTheme.of].

{@tool snippet}

Here is an example of a tooltip theme that applies a blue foreground with non-rounded corners.

```dart
TooltipTheme(
  data: TooltipThemeData(
    decoration: BoxDecoration(
      color: Colors.blue.withValues(alpha: 0.9),
      borderRadius: BorderRadius.zero,
    ),
  ),
  child: Tooltip(
    message: 'Example tooltip',
    child: IconButton(
      iconSize: 36.0,
      icon: const Icon(Icons.touch_app),
      onPressed: () {},
    ),
  ),
)
```

{@end-tool}

See also:

- [TooltipThemeData], which describes the actual configuration of a tooltip theme.
- [TooltipVisibility], which can be used to visually disable descendant [Tooltip]s.

### TooltipTheme()

```dart
TooltipTheme({dynamic key, required TooltipThemeData data, required dynamic child})
```

Creates a tooltip theme that controls the configurations for [Tooltip].

### data

```dart
TooltipThemeData data
```

The properties for descendant [Tooltip] widgets.

### of()

```dart
TooltipThemeData of(BuildContext context)
```

Retrieves the [TooltipThemeData] from the closest ancestor [TooltipTheme].

The result comes from the closest [TooltipTheme] ancestor if any, and otherwise from [Theme.of] and [ThemeData.tooltipTheme].

When a widget uses this method, it is automatically rebuilt if the tooltip theme later changes, so that the changes can be applied.

Typical usage is as follows:

```dart
TooltipThemeData theme = TooltipTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(TooltipTheme oldWidget)
```
