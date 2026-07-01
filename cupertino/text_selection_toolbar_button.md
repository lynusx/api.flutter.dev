# CupertinoTextSelectionToolbarButton

```dart
class CupertinoTextSelectionToolbarButton extends StatefulWidget {}
```

A button in the style of the iOS text selection toolbar buttons.

### CupertinoTextSelectionToolbarButton()

```dart
CupertinoTextSelectionToolbarButton({dynamic key, VoidCallback? onPressed, required Widget? child})
```

Create an instance of [CupertinoTextSelectionToolbarButton].

### CupertinoTextSelectionToolbarButton.text()

```dart
CupertinoTextSelectionToolbarButton.text({dynamic key, VoidCallback? onPressed, required String? text})
```

Create an instance of [CupertinoTextSelectionToolbarButton] whose child is a [Text] widget styled like the default iOS text selection toolbar button.

### CupertinoTextSelectionToolbarButton.buttonItem()

```dart
CupertinoTextSelectionToolbarButton.buttonItem({dynamic key, required ContextMenuButtonItem? buttonItem})
```

Create an instance of [CupertinoTextSelectionToolbarButton] from the given [ContextMenuButtonItem].

### child

```dart
Widget? child
```

{@template flutter.cupertino.CupertinoTextSelectionToolbarButton.child} The child of this button.

Usually a [Text] or an [Icon]. {@endtemplate}

### onPressed

```dart
VoidCallback? onPressed
```

{@template flutter.cupertino.CupertinoTextSelectionToolbarButton.onPressed} Called when this button is pressed. {@endtemplate}

### buttonItem

```dart
ContextMenuButtonItem? buttonItem
```

{@template flutter.cupertino.CupertinoTextSelectionToolbarButton.onPressed} The buttonItem used to generate the button when using [CupertinoTextSelectionToolbarButton.buttonItem]. {@endtemplate}

### text

```dart
String? text
```

{@template flutter.cupertino.CupertinoTextSelectionToolbarButton.text} The text used in the button's label when using [CupertinoTextSelectionToolbarButton.text]. {@endtemplate}

### getButtonLabel()

```dart
String getButtonLabel(BuildContext context, ContextMenuButtonItem buttonItem)
```

Returns the default button label String for the button of the given [ContextMenuButtonItem]'s [ContextMenuButtonType].

### createState()

```dart
State<StatefulWidget> createState()
```
