@docImport 'package:flutter/cupertino.dart';

@docImport 'input_decorator.dart'; @docImport 'selectable_text.dart'; @docImport 'text_field.dart';

# TextSelectionThemeData

```dart
class TextSelectionThemeData with Diagnosticable {}
```

Defines the text selection visual properties for descendant [TextField] and [SelectableText] widgets.

Descendant widgets obtain the current [TextSelectionThemeData] object using [TextSelectionTheme.of]. Instances of [TextSelectionThemeData] can be customized with [TextSelectionThemeData.copyWith].

Typically a [TextSelectionThemeData] is specified as part of the overall [Theme] with [ThemeData.textSelectionTheme].

See also:

- [TextSelectionTheme], an [InheritedWidget] that propagates the theme down its subtree.
- [InputDecorationThemeData], which defines most other visual properties of text fields.

### TextSelectionThemeData()

```dart
TextSelectionThemeData({Color? cursorColor, Color? selectionColor, Color? selectionHandleColor})
```

Creates the set of properties used to configure [TextField]s.

### cursorColor

```dart
Color? cursorColor
```

The color of the cursor in the text field.

The cursor indicates the current location of text insertion point in the field.

### selectionColor

```dart
Color? selectionColor
```

The background color of selected text.

### selectionHandleColor

```dart
Color? selectionHandleColor
```

The color of the selection handles on the text field.

Selection handles are used to indicate the bounds of the selected text, or as a handle to drag the cursor to a new location in the text.

On iOS [TextField] and [SelectableText] cannot access [selectionHandleColor]. To set the [selectionHandleColor] on iOS, you can change the [CupertinoThemeData.selectionHandleColor] by wrapping the subtree containing your [TextField] or [SelectableText] with a [CupertinoTheme].

### copyWith()

```dart
TextSelectionThemeData copyWith({Color? cursorColor, Color? selectionColor, Color? selectionHandleColor})
```

Creates a copy of this object with the given fields replaced with the specified values.

### lerp()

```dart
TextSelectionThemeData? lerp(TextSelectionThemeData? a, TextSelectionThemeData? b, double t)
```

Linearly interpolate between two text field themes.

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

# TextSelectionTheme

```dart
class TextSelectionTheme extends InheritedTheme {}
```

An inherited widget that defines the appearance of text selection in this widget's subtree.

Values specified here are used for [TextField] and [SelectableText] properties that are not given an explicit non-null value.

{@tool snippet}

Here is an example of a text selection theme that applies a blue cursor color with light blue selection handles to the child text field.

```dart
const TextSelectionTheme(
  data: TextSelectionThemeData(
    cursorColor: Colors.blue,
    selectionHandleColor: Colors.lightBlue,
  ),
  child: TextField(),
)
```

{@end-tool}

This widget also creates a [DefaultSelectionStyle] for its subtree with [data].

### TextSelectionTheme()

```dart
TextSelectionTheme({dynamic key, required TextSelectionThemeData data, required Widget child})
```

Creates a text selection theme widget that specifies the text selection properties for all widgets below it in the widget tree.

### data

```dart
TextSelectionThemeData data
```

The properties for descendant [TextField] and [SelectableText] widgets.

### child

```dart
Widget get child
```

### of()

```dart
TextSelectionThemeData of(BuildContext context)
```

Returns the [data] from the closest [TextSelectionTheme] ancestor. If there is no ancestor, it returns [ThemeData.textSelectionTheme]. Applications can assume that the returned value will not be null.

Typical usage is as follows:

```dart
TextSelectionThemeData theme = TextSelectionTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(TextSelectionTheme oldWidget)
```
