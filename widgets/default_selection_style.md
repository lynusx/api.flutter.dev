@docImport 'package:flutter/material.dart';

@docImport 'editable_text.dart'; @docImport 'text.dart';

# DefaultSelectionStyle

```dart
class DefaultSelectionStyle extends InheritedTheme {}
```

The selection style to apply to descendant [EditableText] widgets which don't have an explicit style.

{@macro flutter.cupertino.CupertinoApp.defaultSelectionStyle}

{@macro flutter.material.MaterialApp.defaultSelectionStyle}

See also:

- [TextSelectionTheme]: which also creates a [DefaultSelectionStyle] for the subtree.

### DefaultSelectionStyle()

```dart
DefaultSelectionStyle({dynamic key, Color? cursorColor, Color? selectionColor, MouseCursor? mouseCursor, required Widget child})
```

Creates a default selection style widget that specifies the selection properties for all widgets below it in the widget tree.

### DefaultSelectionStyle.fallback()

```dart
DefaultSelectionStyle.fallback({dynamic key})
```

A const-constructable default selection style that provides fallback values (null).

Returned from [of] when the given [BuildContext] doesn't have an enclosing default selection style.

This constructor creates a [DefaultTextStyle] with an invalid [child], which means the constructed value cannot be incorporated into the tree.

### merge()

```dart
Widget merge({Key? key, Color? cursorColor, Color? selectionColor, MouseCursor? mouseCursor, required Widget child})
```

Creates a default selection style that overrides the selection styles in scope at this point in the widget tree.

Any Arguments that are not null replace the corresponding properties on the default selection style for the [BuildContext] where the widget is inserted.

### defaultColor

```dart
Color defaultColor
```

The default cursor and selection color (semi-transparent grey).

This is the color that the [Text] widget uses when the specified selection color is null.

### cursorColor

```dart
Color? cursorColor
```

The color of the text field's cursor.

The cursor indicates the current location of the text insertion point in the field.

### selectionColor

```dart
Color? selectionColor
```

The background color of selected text.

### mouseCursor

```dart
MouseCursor? mouseCursor
```

The [MouseCursor] for mouse pointers hovering over selectable Text widgets.

If this property is null, [SystemMouseCursors.text] will be used.

### of()

```dart
DefaultSelectionStyle of(BuildContext context)
```

The closest instance of this class that encloses the given context.

If no such instance exists, returns an instance created by [DefaultSelectionStyle.fallback], which contains fallback values.

Typical usage is as follows:

```dart
DefaultSelectionStyle style = DefaultSelectionStyle.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(DefaultSelectionStyle oldWidget)
```
