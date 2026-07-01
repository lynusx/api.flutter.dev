# RadioGroup

```dart
class RadioGroup<T> extends StatefulWidget {}
```

A group for radios.

This widget treats all radios, such as [RawRadio], [Radio], [CupertinoRadio] in the sub tree with the same type T as a group. Radios with different types are not included in the group.

This widget handles the group value for the radios in the subtree with the same value type.

Using this widget also provides keyboard navigation and semantics for the radio buttons that matches [APG](https://www.w3.org/WAI/ARIA/apg/patterns/radio/).

The keyboard behaviors are:

- Tab and Shift+Tab: moves focus into and out of radio group. When focus moves into a radio group and a radio button is select, focus is set on selected button. Otherwise, it focus the first radio button in reading order.
- Space: toggle the selection on the focused radio button.
- Right and down arrow key: move selection to next radio button in the group in reading order.
- Left and up arrow key: move selection to previous radio button in the group in reading order.

Arrow keys will wrap around if it reach the first or last radio in the group.

{@tool dartpad} Here is an example of RadioGroup widget.

Try using tab, arrow keys, and space to see how the widget responds.

** See code in examples/api/lib/widgets/radio_group/radio_group.0.dart ** {@end-tool}

### RadioGroup()

```dart
RadioGroup({dynamic key, T? groupValue, required ValueChanged<T?> onChanged, required Widget child})
```

Creates a radio group.

The `groupValue` set the selection on a subtree radio with the same [RawRadio.value].

The `onChanged` is called when the selection has changed in the subtree radios.

### groupValue

```dart
T? groupValue
```

The selected value under this radio group.

[RawRadio] under this radio group where its [RawRadio.value] equals to this value will be selected.

### onChanged

```dart
ValueChanged<T?> onChanged
```

Called when selection has changed.

The value can be null when unselect the [RawRadio] with [RawRadio.toggleable] set to true.

### child

```dart
Widget child
```

{@macro flutter.widgets.ProxyWidget.child}

### maybeOf()

```dart
RadioGroupRegistry<T>? maybeOf<T>(BuildContext context)
```

Gets the [RadioGroupRegistry] from the above the context.

This registers a dependencies on the context that it causes rebuild if [RadioGroupRegistry] has changed or its [RadioGroupRegistry.groupValue] has changed.

### createState()

```dart
State<StatefulWidget> createState()
```

# RadioGroupRegistry

```dart
abstract class RadioGroupRegistry<T> {}
```

An abstract interface for registering a group of radios.

Use [registerClient] or [unregisterClient] to handle registrations of radios.

The registry manages the group value for the radios. The radio needs to call [onChanged] to notify the group value needs to be changed.

### groupValue

```dart
T? get groupValue
```

The group value for the group.

### registerClient()

```dart
void registerClient(RadioClient<T> radio)
```

Registers a radio client.

The subclass provides additional features, such as keyboard navigation for the registered clients.

### unregisterClient()

```dart
void unregisterClient(RadioClient<T> radio)
```

Unregisters a radio client.

### onChanged

```dart
ValueChanged<T?> get onChanged
```

Notifies the registry that the a radio is selected or unselected.

# RadioClient

```dart
mixin RadioClient<T> {}
```

A client for a [RadioGroupRegistry].

This is typically mixed with a [State].

To register to a [RadioGroupRegistry], assign the registry to [registry].

To unregister from previous [RadioGroupRegistry], either assign a different value to [registry] or set it to null.

### tristate

```dart
bool get tristate
```

Whether this radio support toggles.

Used by registry to provide additional feature such as keyboard support.

### radioValue

```dart
T get radioValue
```

This value this radio represents.

Used by registry to provide additional feature such as keyboard support.

### enabled

```dart
bool get enabled
```

Whether this radio is enabled.

If false, the registry skips this client when handling keyboard navigation.

### focusNode

```dart
FocusNode get focusNode
```

Focus node for this radio.

Used by registry to provide additional feature such as keyboard support.

### registry

```dart
RadioGroupRegistry<T>? get registry
```

The [RadioGroupRegistry] this client register to.

Setting this property automatically register to the new value and unregister the old value.

This should set to null when dispose.

### registry

```dart
set registry(RadioGroupRegistry<T>? newRegistry)
```
