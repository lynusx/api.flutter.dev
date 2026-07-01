# RadioBuilder

```dart
typedef RadioBuilder = Widget Function(BuildContext context, ToggleableStateMixin state)
```

Signature for [RawRadio.builder].

The builder can use `state` to determine the state of the radio and build the visual.

{@macro flutter.widgets.ToggleableStateMixin.buildToggleableWithChild}

# RawRadio

```dart
class RawRadio<T> extends StatefulWidget {}
```

A Radio button that provides basic radio functionalities.

Provide the `builder` to draw UI for radio.

{@macro flutter.widgets.ToggleableStateMixin.buildToggleableWithChild}

This widget allows selection between a number of mutually exclusive values. When one radio button in a group is selected, the other radio buttons in the group cease to be selected. The values are of type `T`, the type parameter of the radio class. Enums are commonly used for this purpose.

{@macro flutter.widget.RawRadio.groupValue}

If [enabled] is false, the radio will not be interactive.

See also:

- [Radio], which uses this widget to build a Material styled radio button.
- [CupertinoRadio], which uses this widget to build a Cupertino styled radio button.

### RawRadio()

```dart
RawRadio({dynamic key, required T value, required WidgetStateProperty<MouseCursor> mouseCursor, required bool toggleable, required FocusNode focusNode, required bool autofocus, required RadioGroupRegistry<T>? groupRegistry, required bool enabled, required RadioBuilder builder})
```

Creates a radio button.

If [enabled] is true, the [groupRegistry] must not be null.

### value

```dart
T value
```

{@template flutter.widget.RawRadio.value} The value represented by this radio button. {@endtemplate}

### mouseCursor

```dart
WidgetStateProperty<MouseCursor> mouseCursor
```

{@template flutter.widget.RawRadio.mouseCursor} The cursor for a mouse pointer when it enters or is hovering over the widget.

If [mouseCursor] is a [WidgetStateMouseCursor], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.disabled]. {@endtemplate}

### toggleable

```dart
bool toggleable
```

{@template flutter.widget.RawRadio.toggleable} Set to true if this radio button is allowed to be returned to an indeterminate state by selecting it again when selected.

To indicate returning to an indeterminate state, [RadioGroup.onChanged] of the [RadioGroup] above the widget tree will be called with null.

If true, [RadioGroup.onChanged] is called with [value] when selected while [RadioGroup.groupValue] != [value], and with null when selected again while [RadioGroup.groupValue] == [value].

If false, [RadioGroup.onChanged] will be called with [value] when it is selected while [RadioGroup.groupValue] != [value], and only by selecting another radio button in the group (i.e. changing the value of [RadioGroup.groupValue]) can this radio button be unselected.

The default is false. {@endtemplate}

### focusNode

```dart
FocusNode focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.Focus.autofocus}

### builder

```dart
RadioBuilder builder
```

The builder for the radio button visual.

Use the input `state` to determine the current state of the radio.

{@macro flutter.widgets.ToggleableStateMixin.buildToggleableWithChild}

### enabled

```dart
bool enabled
```

Whether this widget is enabled.

### groupRegistry

```dart
RadioGroupRegistry<T>? groupRegistry
```

{@template flutter.widget.RawRadio.groupRegistry} The registry this radio registers to. {@endtemplate}

{@template flutter.widget.RawRadio.groupValue} The radio relies on [groupRegistry] to maintains the state for selection. If use in conjunction with a [RadioGroup] widget, use [RadioGroup.maybeOf] to get the group registry from the context. {@endtemplate}

### createState()

```dart
State<RawRadio<T>> createState()
```
