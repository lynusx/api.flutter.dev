@docImport 'button_style.dart'; @docImport 'text_selection_toolbar.dart';

# TextSelectionToolbarTextButton

```dart
class TextSelectionToolbarTextButton extends StatelessWidget {}
```

A button styled like a Material native Android text selection menu button.

### TextSelectionToolbarTextButton()

```dart
TextSelectionToolbarTextButton({dynamic key, required Widget child, required EdgeInsetsGeometry padding, VoidCallback? onPressed, AlignmentGeometry? alignment})
```

Creates an instance of TextSelectionToolbarTextButton.

### child

```dart
Widget child
```

{@template flutter.material.TextSelectionToolbarTextButton.child} The child of this button.

Usually a [Text]. {@endtemplate}

### onPressed

```dart
VoidCallback? onPressed
```

{@template flutter.material.TextSelectionToolbarTextButton.onPressed} Called when this button is pressed. {@endtemplate}

### padding

```dart
EdgeInsetsGeometry padding
```

The padding between the button's edge and its child.

In a standard Material [TextSelectionToolbar], the padding depends on the button's position within the toolbar.

See also:

- [getPadding], which calculates the standard padding based on the button's position.
- [ButtonStyle.padding], which is where this padding is applied.

### alignment

```dart
AlignmentGeometry? alignment
```

The alignment of the button's child.

By default, this will be [Alignment.center].

See also:

- [ButtonStyle.alignment], which is where this alignment is applied.

### getPadding()

```dart
EdgeInsetsGeometry getPadding(int index, int total)
```

Returns the standard padding for a button at index out of a total number of buttons.

Standard Material [TextSelectionToolbar]s have buttons with different padding depending on their position in the toolbar.

### copyWith()

```dart
TextSelectionToolbarTextButton copyWith({Widget? child, VoidCallback? onPressed, EdgeInsetsGeometry? padding, AlignmentGeometry? alignment})
```

Returns a copy of the current [TextSelectionToolbarTextButton] instance with specific overrides.

### build()

```dart
Widget build(BuildContext context)
```
