@docImport 'dart:ui'; @docImport 'package:flutter/semantics.dart'; @docImport 'package:flutter/services.dart';

@docImport 'app.dart'; @docImport 'text_button.dart';

# Dialog

```dart
class Dialog extends StatelessWidget {}
```

A Material Design dialog.

This dialog widget does not have any opinion about the contents of the dialog. Rather than using this widget directly, consider using [AlertDialog] or [SimpleDialog], which implement specific kinds of Material Design dialogs.

{@tool dartpad} This sample shows the creation of [Dialog] and [Dialog.fullscreen] widgets.

** See code in examples/api/lib/material/dialog/dialog.0.dart ** {@end-tool}

## Contraints

The Material 3 guideline recommends that a dialog should have a maximal width of 560dp. For historical reasons, Flutter's [Dialog] widget does not come with this constraint by default. For applications targeting large screens such as desktop or Web, it is recommended to set the [constraints] property.

{@tool snippet} This sample shows a [Dialog] using [BoxConstraints] defined by the Material 3 specification.

```dart
const Dialog(constraints: BoxConstraints(maxWidth: 560, minHeight: 280));
```

{@end-tool}

See also:

- [AlertDialog], for dialogs that have a message and some buttons.
- [SimpleDialog], for dialogs that offer a variety of options.
- [showDialog], which actually displays the dialog and returns its result.
- <https://material.io/design/components/dialogs.html>

### Dialog()

```dart
Dialog({dynamic key, Color? backgroundColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, Duration insetAnimationDuration = const Duration(milliseconds: 100), Curve insetAnimationCurve = Curves.decelerate, EdgeInsets? insetPadding, Clip? clipBehavior, ShapeBorder? shape, AlignmentGeometry? alignment, Widget? child, SemanticsRole semanticsRole = SemanticsRole.dialog, BoxConstraints? constraints})
```

Creates a dialog.

Typically used in conjunction with [showDialog].

### Dialog.fullscreen()

```dart
Dialog.fullscreen({dynamic key, Color? backgroundColor, Duration insetAnimationDuration = Duration.zero, Curve insetAnimationCurve = Curves.decelerate, Widget? child, SemanticsRole semanticsRole = SemanticsRole.dialog})
```

Creates a fullscreen dialog.

Typically used in conjunction with [showDialog].

### backgroundColor

```dart
Color? backgroundColor
```

{@template flutter.material.dialog.backgroundColor} The background color of the surface of this [Dialog].

This sets the [Material.color] on this [Dialog]'s [Material].

If null, then the [DialogThemeData.backgroundColor] is used. If that is also null, defaults to [ColorScheme.surfaceContainerHigh]. If [ThemeData.useMaterial3] is false, defaults to [Colors.grey] with a shade of 800 in dark theme and [Colors.white] in light theme.

If [Dialog.fullscreen] is used, defaults to [ColorScheme.surface]. {@endtemplate}

### elevation

```dart
double? elevation
```

{@template flutter.material.dialog.elevation} The z-coordinate of this [Dialog].

Controls how far above the parent the dialog will appear. Elevation is represented by a drop shadow if [shadowColor] is non null, and a surface tint overlay on the background color if [surfaceTintColor] is non null.

If null then [DialogThemeData.elevation] is used, and if that is null then the elevation will match the Material Design specification for Dialogs.

See also:

- [Material.elevation], which describes how [elevation] effects the drop shadow or surface tint overlay.
- [shadowColor], color of the drop shadow used to indicate the elevation.
- [surfaceTintColor], color of an overlay on top of the background color used to indicate the elevation.
- <https://m3.material.io/components/dialogs/overview>, the Material Design specification for dialogs. {@endtemplate}

### shadowColor

```dart
Color? shadowColor
```

{@template flutter.material.dialog.shadowColor} The color used to paint a drop shadow under the dialog's [Material], which reflects the dialog's [elevation].

If null and [ThemeData.useMaterial3] is true then no drop shadow will be rendered.

If null and [ThemeData.useMaterial3] is false then it will default to [ThemeData.shadowColor].

See also:

- [Material.shadowColor], which describes how the drop shadow is painted.
- [elevation], which affects how the drop shadow is painted.
- [surfaceTintColor], which can be used to indicate elevation through tinting the background color. {@endtemplate}

### surfaceTintColor

```dart
Color? surfaceTintColor
```

{@template flutter.material.dialog.surfaceTintColor} The color used as a surface tint overlay on the dialog's background color, which reflects the dialog's [elevation].

If [ThemeData.useMaterial3] is false property has no effect.

This is not recommended for use. [Material 3 spec](https://m3.material.io/styles/color/the-color-system/color-roles) introduced a set of tone-based surfaces and surface containers in its [ColorScheme], which provide more flexibility. The intention is to eventually remove surface tint color from the framework.

defaults to [Colors.transparent].

To disable this feature, set [surfaceTintColor] to [Colors.transparent].

See also:

- [Material.surfaceTintColor], which describes how the surface tint will be applied to the background color of the dialog.
- [elevation], which affects the opacity of the surface tint.
- [shadowColor], which can be used to indicate elevation through a drop shadow. {@endtemplate}

### insetAnimationDuration

```dart
Duration insetAnimationDuration
```

{@template flutter.material.dialog.insetAnimationDuration} The duration of the animation to show when the system keyboard intrudes into the space that the dialog is placed in.

Defaults to 100 milliseconds when [Dialog] is used, and [Duration.zero] when [Dialog.fullscreen] is used. {@endtemplate}

### insetAnimationCurve

```dart
Curve insetAnimationCurve
```

{@template flutter.material.dialog.insetAnimationCurve} The curve to use for the animation shown when the system keyboard intrudes into the space that the dialog is placed in.

Defaults to [Curves.decelerate]. {@endtemplate}

### insetPadding

```dart
EdgeInsets? insetPadding
```

{@template flutter.material.dialog.insetPadding} The amount of padding added to [MediaQueryData.viewInsets] on the outside of the dialog. This defines the minimum space between the screen's edges and the dialog.

Defaults to `EdgeInsets.symmetric(horizontal: 40.0, vertical: 24.0)`. {@endtemplate}

### clipBehavior

```dart
Clip? clipBehavior
```

{@template flutter.material.dialog.clipBehavior} Controls how the contents of the dialog are clipped (or not) to the given [shape].

See the enum [Clip] for details of all possible options and their common use cases.

If null, then [DialogThemeData.clipBehavior] is used. If that is also null, defaults to [Clip.none]. {@endtemplate}

### shape

```dart
ShapeBorder? shape
```

{@template flutter.material.dialog.shape} The shape of this dialog's border.

Defines the dialog's [Material.shape].

The default shape is a [RoundedRectangleBorder] with a radius of 4.0 {@endtemplate}

### alignment

```dart
AlignmentGeometry? alignment
```

{@template flutter.material.dialog.alignment} How to align the [Dialog].

If null, then [DialogThemeData.alignment] is used. If that is also null, the default is [Alignment.center]. {@endtemplate}

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### semanticsRole

```dart
SemanticsRole semanticsRole
```

The role this dialog represent in assist technologies.

Defaults to [SemanticsRole.dialog].

### constraints

```dart
BoxConstraints? constraints
```

{@template flutter.material.dialog.constraints} Constrains the size of the dialog.

If null, then [DialogThemeData.constraints] is used. If that is also null, the default is `const BoxConstraints(minWidth: 280.0)`. {@endtemplate}

### build()

```dart
Widget build(BuildContext context)
```

# AlertDialog

```dart
class AlertDialog extends StatelessWidget {}
```

A Material Design alert dialog.

An alert dialog (also known as a basic dialog) informs the user about situations that require acknowledgment. An alert dialog has an optional title and an optional list of actions. The title is displayed above the content and the actions are displayed below the content.

{@youtube 560 315 https://www.youtube.com/watch?v=75CsnyRXf5I}

For dialogs that offer the user a choice between several options, consider using a [SimpleDialog].

Typically passed as the child widget to [showDialog], which displays the dialog.

{@animation 350 622 https://flutter.github.io/assets-for-api-docs/assets/material/alert_dialog.mp4}

{@tool snippet}

This snippet shows a method in a [State] which, when called, displays a dialog box and returns a [Future] that completes when the dialog is dismissed.

```dart
Future<void> _showMyDialog() async {
  return showDialog<void>(
    context: context,
    barrierDismissible: false, // user must tap button!
    builder: (BuildContext context) {
      return AlertDialog(
        title: const Text('AlertDialog Title'),
        content: const SingleChildScrollView(
          child: ListBody(
            children: <Widget>[
              Text('This is a demo alert dialog.'),
              Text('Would you like to approve of this message?'),
            ],
          ),
        ),
        actions: <Widget>[
          TextButton(
            child: const Text('Approve'),
            onPressed: () {
              Navigator.of(context).pop();
            },
          ),
        ],
      );
    },
  );
}
```

{@end-tool}

{@tool dartpad} This demo shows a [TextButton] which when pressed, calls [showDialog]. When called, this method displays a Material dialog above the current contents of the app and returns a [Future] that completes when the dialog is dismissed.

** See code in examples/api/lib/material/dialog/alert_dialog.0.dart ** {@end-tool}

{@tool dartpad} This sample shows the creation of [AlertDialog], as described in: https://m3.material.io/components/dialogs/overview

** See code in examples/api/lib/material/dialog/alert_dialog.1.dart ** {@end-tool}

## Alert dialogs and scrolling

By default, alert dialogs size themselves to contain their children.

If the content is too large to fit on the screen vertically, the dialog will display the title and actions, and let the _[content]_ overflow. This is rarely desired. Consider using a scrolling widget for [content], such as [SingleChildScrollView], to avoid overflow.

Because the dialog attempts to size itself to the contents, the [content] must support reporting its intrinsic dimensions. In particular, this means that lazily-rendered widgets such as [ListView], [GridView], and [CustomScrollView], will not work in an [AlertDialog] unless they are wrapped in a widget that forces a particular size (e.g. a [SizedBox]).

For finer-grained control over the sizing of a dialog, consider using [Dialog] directly.

See also:

- [SimpleDialog], which handles the scrolling of the contents but has no [actions].
- [Dialog], on which [AlertDialog] and [SimpleDialog] are based.
- [CupertinoAlertDialog], an iOS-styled alert dialog.
- [showDialog], which actually displays the dialog and returns its result.
- <https://material.io/design/components/dialogs.html#alert-dialog>
- <https://m3.material.io/components/dialogs>

### AlertDialog()

```dart
AlertDialog({dynamic key, Widget? icon, EdgeInsetsGeometry? iconPadding, Color? iconColor, Widget? title, EdgeInsetsGeometry? titlePadding, TextStyle? titleTextStyle, Widget? content, EdgeInsetsGeometry? contentPadding, TextStyle? contentTextStyle, List<Widget>? actions, EdgeInsetsGeometry? actionsPadding, MainAxisAlignment? actionsAlignment, OverflowBarAlignment? actionsOverflowAlignment, VerticalDirection? actionsOverflowDirection, double? actionsOverflowButtonSpacing, EdgeInsetsGeometry? buttonPadding, Color? backgroundColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, String? semanticLabel, EdgeInsets? insetPadding, Clip? clipBehavior, ShapeBorder? shape, AlignmentGeometry? alignment, BoxConstraints? constraints, bool scrollable = false})
```

Creates an alert dialog.

Typically used in conjunction with [showDialog].

The [titlePadding] and [contentPadding] default to null, which implies a default that depends on the values of the other properties. See the documentation of [titlePadding] and [contentPadding] for details.

### AlertDialog.adaptive()

```dart
AlertDialog.adaptive({Key? key, Widget? icon, EdgeInsetsGeometry? iconPadding, Color? iconColor, Widget? title, EdgeInsetsGeometry? titlePadding, TextStyle? titleTextStyle, Widget? content, EdgeInsetsGeometry? contentPadding, TextStyle? contentTextStyle, List<Widget>? actions, EdgeInsetsGeometry? actionsPadding, MainAxisAlignment? actionsAlignment, OverflowBarAlignment? actionsOverflowAlignment, VerticalDirection? actionsOverflowDirection, double? actionsOverflowButtonSpacing, EdgeInsetsGeometry? buttonPadding, Color? backgroundColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, String? semanticLabel, EdgeInsets insetPadding, Clip? clipBehavior, ShapeBorder? shape, AlignmentGeometry? alignment, BoxConstraints? constraints, bool scrollable, ScrollController? scrollController, ScrollController? actionScrollController, Duration insetAnimationDuration, Curve insetAnimationCurve})
```

Creates an adaptive [AlertDialog] based on whether the target platform is iOS or macOS, following Material design's [Cross-platform guidelines](https://material.io/design/platform-guidance/cross-platform-adaptation.html).

On iOS and macOS, this constructor creates a [CupertinoAlertDialog]. On other platforms, this creates a Material design [AlertDialog].

Typically passed as a child of [showAdaptiveDialog], which will display the alert differently based on platform.

If a [CupertinoAlertDialog] is created only these parameters are used: [title], [content], [actions], [scrollController], [actionScrollController], [insetAnimationDuration], and [insetAnimationCurve]. If a material [AlertDialog] is created, [scrollController], [actionScrollController], [insetAnimationDuration], and [insetAnimationCurve] are ignored.

The target platform is based on the current [Theme]: [ThemeData.platform].

{@tool dartpad} This demo shows a [TextButton] which when pressed, calls [showAdaptiveDialog]. When called, this method displays an adaptive dialog above the current contents of the app, with different behaviors depending on target platform.

[CupertinoDialogAction] is conditionally used as the child to show more platform specific design.

** See code in examples/api/lib/material/dialog/adaptive_alert_dialog.0.dart ** {@end-tool}

### icon

```dart
Widget? icon
```

An optional icon to display at the top of the dialog.

Typically, an [Icon] widget. Providing an icon centers the [title]'s text.

### iconColor

```dart
Color? iconColor
```

Color for the [Icon] in the [icon] of this [AlertDialog].

If null, [DialogThemeData.iconColor] is used. If that is null, defaults to color scheme's [ColorScheme.secondary] if [ThemeData.useMaterial3] is true, black otherwise.

### iconPadding

```dart
EdgeInsetsGeometry? iconPadding
```

Padding around the [icon].

If there is no [icon], no padding will be provided. Otherwise, this padding is used.

This property defaults to providing 24 pixels on the top, left, and right of the [icon]. If [title] is _not_ null, 16 pixels of bottom padding is added to separate the [icon] from the [title]. If the [title] is null and [content] is _not_ null, then no bottom padding is provided (but see [contentPadding]). In any other case 24 pixels of bottom padding is added.

### title

```dart
Widget? title
```

The (optional) title of the dialog is displayed in a large font at the top of the dialog, below the (optional) [icon].

Typically a [Text] widget.

### titlePadding

```dart
EdgeInsetsGeometry? titlePadding
```

Padding around the title.

If there is no title, no padding will be provided. Otherwise, this padding is used.

This property defaults to providing 24 pixels on the top, left, and right of the title. If the [content] is not null, then no bottom padding is provided (but see [contentPadding]). If it _is_ null, then an extra 20 pixels of bottom padding is added to separate the [title] from the [actions].

### titleTextStyle

```dart
TextStyle? titleTextStyle
```

Style for the text in the [title] of this [AlertDialog].

If null, [DialogThemeData.titleTextStyle] is used. If that's null, defaults to [TextTheme.headlineSmall] of [ThemeData.textTheme] if [ThemeData.useMaterial3] is true, [TextTheme.titleLarge] otherwise.

### content

```dart
Widget? content
```

The (optional) content of the dialog is displayed in the center of the dialog in a lighter font.

Typically this is a [SingleChildScrollView] that contains the dialog's message. As noted in the [AlertDialog] documentation, it's important to use a [SingleChildScrollView] if there's any risk that the content will not fit, as the contents will otherwise overflow the dialog.

The [content] must support reporting its intrinsic dimensions. In particular, [ListView], [GridView], and [CustomScrollView] cannot be used here unless they are first wrapped in a widget that itself can report intrinsic dimensions, such as a [SizedBox].

### contentPadding

```dart
EdgeInsetsGeometry? contentPadding
```

Padding around the content.

If there is no [content], no padding will be provided. Otherwise, this padding is used.

This property defaults to providing a padding of 20 pixels above the [content] to separate the [content] from the [title], and 24 pixels on the left, right, and bottom to separate the [content] from the other edges of the dialog.

If [ThemeData.useMaterial3] is true, the top padding separating the content from the title defaults to 16 pixels instead of 20 pixels.

### contentTextStyle

```dart
TextStyle? contentTextStyle
```

Style for the text in the [content] of this [AlertDialog].

If null, [DialogThemeData.contentTextStyle] is used. If that's null, defaults to [TextTheme.bodyMedium] of [ThemeData.textTheme] if [ThemeData.useMaterial3] is true, [TextTheme.titleMedium] otherwise.

### actions

```dart
List<Widget>? actions
```

The (optional) set of actions that are displayed at the bottom of the dialog with an [OverflowBar].

Typically this is a list of [TextButton] widgets. It is recommended to set the [Text.textAlign] to [TextAlign.end] for the [Text] within the [TextButton], so that buttons whose labels wrap to an extra line align with the overall [OverflowBar]'s alignment within the dialog.

If the [title] is not null but the [content] _is_ null, then an extra 20 pixels of padding is added above the [OverflowBar] to separate the [title] from the [actions].

### actionsPadding

```dart
EdgeInsetsGeometry? actionsPadding
```

Padding around the set of [actions] at the bottom of the dialog.

Typically used to provide padding to the button bar between the button bar and the edges of the dialog.

The [buttonPadding] may contribute to the padding on the edges of [actions] as well.

If there are no [actions], then no padding will be included.

{@tool snippet} This is an example of a set of actions aligned with the content widget.

```dart
AlertDialog(
  title: const Text('Title'),
  content: Container(width: 200, height: 200, color: Colors.green),
  actions: <Widget>[
    ElevatedButton(onPressed: () {}, child: const Text('Button 1')),
    ElevatedButton(onPressed: () {}, child: const Text('Button 2')),
  ],
  actionsPadding: const EdgeInsets.symmetric(horizontal: 8.0),
)
```

{@end-tool}

See also:

- [OverflowBar], which [actions] configures to lay itself out.

### actionsAlignment

```dart
MainAxisAlignment? actionsAlignment
```

Defines the horizontal layout of the [actions] according to the same rules as for [Row.mainAxisAlignment].

This parameter is passed along to the dialog's [OverflowBar].

If this parameter is null (the default) then [MainAxisAlignment.end] is used.

### actionsOverflowAlignment

```dart
OverflowBarAlignment? actionsOverflowAlignment
```

The horizontal alignment of [actions] within the vertical "overflow" layout.

If the dialog's [actions] do not fit into a single row, then they are arranged in a column. This parameter controls the horizontal alignment of widgets in the case of an overflow.

If this parameter is null (the default) then [OverflowBarAlignment.end] is used.

See also:

- [OverflowBar], which [actions] configures to lay itself out.

### actionsOverflowDirection

```dart
VerticalDirection? actionsOverflowDirection
```

The vertical direction of [actions] if the children overflow horizontally.

If the dialog's [actions] do not fit into a single row, then they are arranged in a column. The first action is at the top of the column if this property is set to [VerticalDirection.down], since it "starts" at the top and "ends" at the bottom. On the other hand, the first action will be at the bottom of the column if this property is set to [VerticalDirection.up], since it "starts" at the bottom and "ends" at the top.

See also:

- [OverflowBar], which [actions] configures to lay itself out.

### actionsOverflowButtonSpacing

```dart
double? actionsOverflowButtonSpacing
```

The spacing between [actions] when the [OverflowBar] switches to a column layout because the actions don't fit horizontally.

If the widgets in [actions] do not fit into a single row, they are arranged into a column. This parameter provides additional vertical space between buttons when it does overflow.

The button spacing may appear to be more than the value provided. This is because most buttons adhere to the [MaterialTapTargetSize] of 48px. So, even though a button might visually be 36px in height, it might still take up to 48px vertically.

If null then no spacing will be added in between buttons in an overflow state.

### buttonPadding

```dart
EdgeInsetsGeometry? buttonPadding
```

The padding that surrounds each button in [actions].

This is different from [actionsPadding], which defines the padding between the entire button bar and the edges of the dialog.

If this property is null, then it will default to 8.0 logical pixels on the left and right.

### backgroundColor

```dart
Color? backgroundColor
```

{@macro flutter.material.dialog.backgroundColor}

### elevation

```dart
double? elevation
```

{@macro flutter.material.dialog.elevation}

### shadowColor

```dart
Color? shadowColor
```

{@macro flutter.material.dialog.shadowColor}

### surfaceTintColor

```dart
Color? surfaceTintColor
```

{@macro flutter.material.dialog.surfaceTintColor}

### semanticLabel

```dart
String? semanticLabel
```

The semantic label of the dialog used by accessibility frameworks to announce screen transitions when the dialog is opened and closed.

In iOS, if this label is not provided, a semantic label will be inferred from the [title] if it is not null.

In Android, if this label is not provided, the dialog will use the [MaterialLocalizations.alertDialogLabel] as its label.

See also:

- [SemanticsConfiguration.namesRoute], for a description of how this value is used.

### insetPadding

```dart
EdgeInsets? insetPadding
```

{@macro flutter.material.dialog.insetPadding}

### clipBehavior

```dart
Clip? clipBehavior
```

{@macro flutter.material.dialog.clipBehavior}

### shape

```dart
ShapeBorder? shape
```

{@macro flutter.material.dialog.shape}

### alignment

```dart
AlignmentGeometry? alignment
```

{@macro flutter.material.dialog.alignment}

### constraints

```dart
BoxConstraints? constraints
```

{@macro flutter.material.dialog.constraints}

### scrollable

```dart
bool scrollable
```

Determines whether the [title] and [content] widgets are wrapped in a scrollable.

This configuration is used when the [title] and [content] are expected to overflow. Both [title] and [content] are wrapped in a scroll view, allowing all overflowed content to be visible while still showing the button bar.

### build()

```dart
Widget build(BuildContext context)
```

# SimpleDialogOption

```dart
class SimpleDialogOption extends StatelessWidget {}
```

An option used in a [SimpleDialog].

A simple dialog offers the user a choice between several options. This widget is commonly used to represent each of the options. If the user selects this option, the widget will call the [onPressed] callback, which typically uses [Navigator.pop] to close the dialog.

The padding on a [SimpleDialogOption] is configured to combine with the default [SimpleDialog.contentPadding] so that each option ends up 8 pixels from the other vertically, with 20 pixels of spacing between the dialog's title and the first option, and 24 pixels of spacing between the last option and the bottom of the dialog.

{@tool snippet}

```dart
SimpleDialogOption(
  onPressed: () { Navigator.pop(context, Department.treasury); },
  child: const Text('Treasury department'),
)
```

{@end-tool}

See also:

- [SimpleDialog], for a dialog in which to use this widget.
- [showDialog], which actually displays the dialog and returns its result.
- [TextButton], which are commonly used as actions in other kinds of dialogs, such as [AlertDialog]s.
- <https://material.io/design/components/dialogs.html#simple-dialog>

### SimpleDialogOption()

```dart
SimpleDialogOption({dynamic key, VoidCallback? onPressed, EdgeInsets? padding, Widget? child})
```

Creates an option for a [SimpleDialog].

### onPressed

```dart
VoidCallback? onPressed
```

The callback that is called when this option is selected.

If this is set to null, the option cannot be selected.

When used in a [SimpleDialog], this will typically call [Navigator.pop] with a value for [showDialog] to complete its future with.

### child

```dart
Widget? child
```

The widget below this widget in the tree.

Typically a [Text] widget.

### padding

```dart
EdgeInsets? padding
```

The amount of space to surround the [child] with.

Defaults to EdgeInsets.symmetric(vertical: 8.0, horizontal: 24.0).

### build()

```dart
Widget build(BuildContext context)
```

# SimpleDialog

```dart
class SimpleDialog extends StatelessWidget {}
```

A simple Material Design dialog.

A simple dialog offers the user a choice between several options. A simple dialog has an optional title that is displayed above the choices.

Choices are normally represented using [SimpleDialogOption] widgets. If other widgets are used, see [contentPadding] for notes regarding the conventions for obtaining the spacing expected by Material Design.

For dialogs that inform the user about a situation, consider using an [AlertDialog].

Typically passed as the child widget to [showDialog], which displays the dialog.

{@animation 350 622 https://flutter.github.io/assets-for-api-docs/assets/material/simple_dialog.mp4}

{@tool snippet}

In this example, the user is asked to select between two options. These options are represented as an enum. The [showDialog] method here returns a [Future] that completes to a value of that enum. If the user cancels the dialog (e.g. by hitting the back button on Android, or tapping on the mask behind the dialog) then the future completes with the null value.

The return value in this example is used as the index for a switch statement. One advantage of using an enum as the return value and then using that to drive a switch statement is that the analyzer will flag any switch statement that doesn't mention every value in the enum.

```dart
Future<void> _askedToLead() async {
  switch (await showDialog<Department>(
    context: context,
    builder: (BuildContext context) {
      return SimpleDialog(
        title: const Text('Select assignment'),
        children: <Widget>[
          SimpleDialogOption(
            onPressed: () { Navigator.pop(context, Department.treasury); },
            child: const Text('Treasury department'),
          ),
          SimpleDialogOption(
            onPressed: () { Navigator.pop(context, Department.state); },
            child: const Text('State department'),
          ),
        ],
      );
    }
  )) {
    case Department.treasury:
      // Let's go.
      // ...
    break;
    case Department.state:
      // ...
    break;
    case null:
      // dialog dismissed
    break;
  }
}
```

{@end-tool}

See also:

- [SimpleDialogOption], which are options used in this type of dialog.
- [AlertDialog], for dialogs that have a row of buttons below the body.
- [Dialog], on which [SimpleDialog] and [AlertDialog] are based.
- [showDialog], which actually displays the dialog and returns its result.
- <https://material.io/design/components/dialogs.html#simple-dialog>

### SimpleDialog()

```dart
SimpleDialog({dynamic key, Widget? title, EdgeInsetsGeometry titlePadding = const EdgeInsets.fromLTRB(24.0, 24.0, 24.0, 0.0), TextStyle? titleTextStyle, List<Widget>? children, EdgeInsetsGeometry contentPadding = const EdgeInsets.fromLTRB(0.0, 12.0, 0.0, 16.0), TextStyle? contentTextStyle, Color? backgroundColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, String? semanticLabel, EdgeInsets? insetPadding, Clip? clipBehavior, ShapeBorder? shape, AlignmentGeometry? alignment, BoxConstraints? constraints})
```

Creates a simple dialog.

Typically used in conjunction with [showDialog].

### title

```dart
Widget? title
```

The (optional) title of the dialog is displayed in a large font at the top of the dialog.

Typically a [Text] widget.

### titlePadding

```dart
EdgeInsetsGeometry titlePadding
```

Padding around the title.

If there is no title, no padding will be provided.

By default, this provides the recommend Material Design padding of 24 pixels around the left, top, and right edges of the title.

See [contentPadding] for the conventions regarding padding between the [title] and the [children].

### titleTextStyle

```dart
TextStyle? titleTextStyle
```

Style for the text in the [title] of this [SimpleDialog].

If null, [DialogThemeData.titleTextStyle] is used. If that's null, defaults to [TextTheme.titleLarge] of [ThemeData.textTheme].

### children

```dart
List<Widget>? children
```

The (optional) content of the dialog is displayed in a [SingleChildScrollView] underneath the title.

Typically a list of [SimpleDialogOption]s.

### contentPadding

```dart
EdgeInsetsGeometry contentPadding
```

Padding around the content.

By default, this is 12 pixels on the top and 16 pixels on the bottom. This is intended to be combined with children that have 24 pixels of padding on the left and right, and 8 pixels of padding on the top and bottom, so that the content ends up being indented 20 pixels from the title, 24 pixels from the bottom, and 24 pixels from the sides.

The [SimpleDialogOption] widget uses such padding.

If there is no [title], the [contentPadding] should be adjusted so that the top padding ends up being 24 pixels.

### backgroundColor

```dart
Color? backgroundColor
```

{@macro flutter.material.dialog.backgroundColor}

### elevation

```dart
double? elevation
```

{@macro flutter.material.dialog.elevation}

### shadowColor

```dart
Color? shadowColor
```

{@macro flutter.material.dialog.shadowColor}

### surfaceTintColor

```dart
Color? surfaceTintColor
```

{@macro flutter.material.dialog.surfaceTintColor}

### contentTextStyle

```dart
TextStyle? contentTextStyle
```

Style for the text in the [children] of this [SimpleDialog].

If null, [DialogThemeData.contentTextStyle] is used. If that is also null, defaults to [TextTheme.titleMedium] for Material 2, or [TextTheme.bodyMedium] for Material 3.

### semanticLabel

```dart
String? semanticLabel
```

The semantic label of the dialog used by accessibility frameworks to announce screen transitions when the dialog is opened and closed.

If this label is not provided, a semantic label will be inferred from the [title] if it is not null. If there is no title, the label will be taken from [MaterialLocalizations.dialogLabel].

See also:

- [SemanticsConfiguration.namesRoute], for a description of how this value is used.

### insetPadding

```dart
EdgeInsets? insetPadding
```

{@macro flutter.material.dialog.insetPadding}

### clipBehavior

```dart
Clip? clipBehavior
```

{@macro flutter.material.dialog.clipBehavior}

### shape

```dart
ShapeBorder? shape
```

{@macro flutter.material.dialog.shape}

### alignment

```dart
AlignmentGeometry? alignment
```

{@macro flutter.material.dialog.shape}

### constraints

```dart
BoxConstraints? constraints
```

{@macro flutter.material.dialog.constraints}

### build()

```dart
Widget build(BuildContext context)
```

# showDialog()

```dart
Future<T?> showDialog<T>({required BuildContext context, required WidgetBuilder builder, bool barrierDismissible = true, Color? barrierColor, String? barrierLabel, bool useSafeArea = true, bool useRootNavigator = true, RouteSettings? routeSettings, Offset? anchorPoint, TraversalEdgeBehavior? traversalEdgeBehavior, bool fullscreenDialog = false, bool? requestFocus, AnimationStyle? animationStyle})
```

Displays a Material dialog above the current contents of the app, with Material entrance and exit animations, modal barrier color, and modal barrier behavior (dialog is dismissible with a tap on the barrier).

{@macro flutter.widgets.showRawDialog.windowing}

This function takes a `builder` which typically builds a [Dialog] widget. Content below the dialog is dimmed with a [ModalBarrier]. The widget returned by the `builder` does not share a context with the location that [showDialog] is originally called from. Use a [StatefulBuilder] or a custom [StatefulWidget] if the dialog needs to update dynamically.

{@macro flutter.widgets.showRawDialog.context}

The `barrierDismissible` argument is used to indicate whether tapping on the barrier will dismiss the dialog. It is `true` by default and can not be `null`. If windowing is enabled via `flutter config --enable-windowing`,then this argument is ignored as dialogs are displayed in their own windows which do not have a modal barrier.

The `barrierColor` argument is used to specify the color of the modal barrier that darkens everything below the dialog. If `null` the `barrierColor` field from `DialogThemeData` is used. If that is `null` the default color `Colors.black54` is used. If windowing is enabled via `flutter config --enable-windowing`, then this argument is ignored as dialogs are displayed in their own windows which do not have a modal barrier.

The `useSafeArea` argument is used to indicate if the dialog should only display in 'safe' areas of the screen not used by the operating system (see [SafeArea] for more details). It is `true` by default, which means the dialog will not overlap operating system areas. If it is set to `false` the dialog will only be constrained by the screen size. It can not be `null`.

{@macro flutter.widgets.showRawDialog.navigator}

{@macro flutter.widgets.showRawDialog.routeSettings}

If not null, the `traversalEdgeBehavior` argument specifies the transfer of focus beyond the first and the last items of the dialog route. By default, [TraversalEdgeBehavior.closedLoop] is used, because it's typical for dialogs to allow users to cycle through dialog widgets without leaving the dialog. If windowing is enabled via `flutter config --enable-windowing`, then this argument is ignored as dialogs are displayed in their own windows which manage focus traversal independently.

{@template flutter.material.dialog.requestFocus} The `requestFocus` argument is used to specify whether the dialog should request focus when shown. {@endtemplate} {@macro flutter.widgets.navigator.Route.requestFocus} If windowing is enabled via `flutter config --enable-windowing`, then this argument is ignored as dialogs are displayed in their own windows which are focused by the windowing system.

{@macro flutter.widgets.RawDialogRoute}

If the application has multiple [Navigator] objects, it may be necessary to call `Navigator.of(context, rootNavigator: true).pop(result)` to close the dialog rather than just `Navigator.pop(context, result)`.

Returns a [Future] that resolves to the value (if any) that was passed to [Navigator.pop] when the dialog was closed.

{@tool dartpad} This sample demonstrates how to use [showDialog] to display a dialog box.

** See code in examples/api/lib/material/dialog/show_dialog.0.dart ** {@end-tool}

{@tool dartpad} This sample shows the creation of [showDialog], as described in: https://m3.material.io/components/dialogs/overview

** See code in examples/api/lib/material/dialog/show_dialog.1.dart ** {@end-tool}

### State Restoration in Dialogs

Using this method will not enable state restoration for the dialog. In order to enable state restoration for a dialog, use [Navigator.restorablePush] or [Navigator.restorablePushNamed] with [DialogRoute].

For more information about state restoration, see [RestorationManager].

{@tool dartpad} This sample demonstrates how to create a restorable Material dialog. This is accomplished by enabling state restoration by specifying [MaterialApp.restorationScopeId] and using [Navigator.restorablePush] to push [DialogRoute] when the button is tapped.

{@macro flutter.widgets.RestorationManager}

** See code in examples/api/lib/material/dialog/show_dialog.2.dart ** {@end-tool}

See also:

- [AlertDialog], for dialogs that have a row of buttons below a body.
- [SimpleDialog], which handles the scrolling of the contents and does not show buttons below its body.
- [Dialog], on which [SimpleDialog] and [AlertDialog] are based.
- [showCupertinoDialog], which displays an iOS-style dialog.
- [showGeneralDialog], which allows for customization of the dialog popup.
- [DisplayFeatureSubScreen], which documents the specifics of how [DisplayFeature]s can split the screen into sub-screens.
- <https://material.io/design/components/dialogs.html>
- <https://m3.material.io/components/dialogs>

# showAdaptiveDialog()

```dart
Future<T?> showAdaptiveDialog<T>({required BuildContext context, required WidgetBuilder builder, bool? barrierDismissible, Color? barrierColor, String? barrierLabel, bool useSafeArea = true, bool useRootNavigator = true, RouteSettings? routeSettings, Offset? anchorPoint, TraversalEdgeBehavior? traversalEdgeBehavior, bool? requestFocus, AnimationStyle? animationStyle})
```

Displays either a Material or Cupertino dialog depending on platform.

On most platforms this function will act the same as [showDialog], except for iOS and macOS, in which case it will act the same as [showCupertinoDialog].

On Cupertino platforms, [barrierColor], [useSafeArea], and [traversalEdgeBehavior] are ignored.

# DialogRoute

```dart
class DialogRoute<T> extends RawDialogRoute<T> {}
```

A dialog route with Material entrance and exit animations, modal barrier color, and modal barrier behavior (dialog is dismissible with a tap on the barrier).

It is used internally by [showDialog] or can be directly pushed onto the [Navigator] stack to enable state restoration. See [showDialog] for a state restoration app example.

This function takes a `builder` which typically builds a [Dialog] widget. Content below the dialog is dimmed with a [ModalBarrier]. The widget returned by the `builder` does not share a context with the location that `showDialog` is originally called from. Use a [StatefulBuilder] or a custom [StatefulWidget] if the dialog needs to update dynamically.

The `context` argument is used to look up [MaterialLocalizations.modalBarrierDismissLabel], which provides the modal with a localized accessibility label that will be used for the modal's barrier. However, a custom `barrierLabel` can be passed in as well.

The `barrierDismissible` argument is used to indicate whether tapping on the barrier will dismiss the dialog. It is `true` by default and cannot be `null`.

The `barrierColor` argument is used to specify the color of the modal barrier that darkens everything below the dialog. If `null`, the default color `Colors.black54` is used.

The `useSafeArea` argument is used to indicate if the dialog should only display in 'safe' areas of the screen not used by the operating system (see [SafeArea] for more details). It is `true` by default, which means the dialog will not overlap operating system areas. If it is set to `false` the dialog will only be constrained by the screen size. It can not be `null`.

The `settings` argument define the settings for this route. See [RouteSettings] for details.

{@macro flutter.widgets.RawDialogRoute}

See also:

- [showDialog], which is a way to display a DialogRoute.
- [showGeneralDialog], which allows for customization of the dialog popup.
- [showCupertinoDialog], which displays an iOS-style dialog.
- [DisplayFeatureSubScreen], which documents the specifics of how [DisplayFeature]s can split the screen into sub-screens.

### DialogRoute()

```dart
DialogRoute({required BuildContext context, required WidgetBuilder builder, CapturedThemes? themes, dynamic barrierColor = Colors.black54, dynamic barrierDismissible, String? barrierLabel, bool useSafeArea = true, dynamic settings, dynamic requestFocus, dynamic anchorPoint, dynamic traversalEdgeBehavior, dynamic fullscreenDialog, AnimationStyle? animationStyle})
```

A dialog route with Material entrance and exit animations, modal barrier color, and modal barrier behavior (dialog is dismissible with a tap on the barrier).

### buildTransitions()

```dart
Widget buildTransitions(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, Widget child)
```

### dispose()

```dart
void dispose()
```
