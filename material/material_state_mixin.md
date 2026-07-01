@docImport 'ink_well.dart';

# MaterialStateMixin

```dart
mixin MaterialStateMixin<T extends StatefulWidget> on State<T> {}
```

Mixin for [State] classes that require knowledge of changing [WidgetState] values for their child widgets.

This mixin does nothing by mere application to a [State] class, but is helpful when writing `build` methods that include child [InkWell], [GestureDetector], [MouseRegion], or [Focus] widgets. Instead of manually creating handlers for each type of user interaction, such [State] classes can instead provide a `ValueChanged<bool>` function and allow [MaterialStateMixin] to manage the set of active [WidgetState]s, and the calling of [setState] as necessary.

{@tool snippet} This example shows how to write a [StatefulWidget] that uses the [MaterialStateMixin] class to watch [WidgetState] values.

```dart
class MyWidget extends StatefulWidget {
  const MyWidget({super.key, required this.color, required this.child});

  final WidgetStateColor color;
  final Widget child;

  @override
  State<MyWidget> createState() => MyWidgetState();
}

class MyWidgetState extends State<MyWidget> with MaterialStateMixin<MyWidget> {
  @override
  Widget build(BuildContext context) {
    return InkWell(
      onFocusChange: updateMaterialState(WidgetState.focused),
      child: ColoredBox(
        color: widget.color.resolve(materialStates),
        child: widget.child,
      ),
    );
  }
}
```

{@end-tool}

### materialStates

```dart
Set<WidgetState> materialStates
```

Managed set of active [WidgetState] values; designed to be passed to [WidgetStateProperty.resolve] methods.

To mutate and have [setState] called automatically for you, use [setMaterialState], [addMaterialState], or [removeMaterialState]. Directly mutating the set is possible, and may be necessary if you need to alter its list without calling [setState] (and thus triggering a re-render).

To check for a single condition, convenience getters [isPressed], [isHovered], [isFocused], etc, are available for each [WidgetState] value.

### updateMaterialState()

```dart
ValueChanged<bool> updateMaterialState(WidgetState key, {ValueChanged<bool>? onChanged})
```

Callback factory which accepts a [WidgetState] value and returns a closure to mutate [materialStates] and call [setState].

Accepts an optional second named parameter, `onChanged`, which allows arbitrary functionality to be wired through the [MaterialStateMixin]. If supplied, the [onChanged] function is only called when child widgets report events that make changes to the current set of [WidgetState]s.

{@tool snippet} This example shows how to use the [updateMaterialState] callback factory in other widgets, including the optional [onChanged] callback.

```dart
class MyWidget extends StatefulWidget {
  const MyWidget({super.key, this.onPressed});

  /// Something important this widget must do when pressed.
  final VoidCallback? onPressed;

  @override
  State<MyWidget> createState() => MyWidgetState();
}

class MyWidgetState extends State<MyWidget> with MaterialStateMixin<MyWidget> {
  @override
  Widget build(BuildContext context) {
    return ColoredBox(
      color: isPressed ? Colors.black : Colors.white,
      child: InkWell(
        onHighlightChanged: updateMaterialState(
          WidgetState.pressed,
          onChanged: (bool val) {
            if (val) {
              widget.onPressed?.call();
            }
          },
        ),
      ),
    );
  }
}
```

{@end-tool}

### setMaterialState()

```dart
void setMaterialState(WidgetState state, bool isSet)
```

Mutator to mark a [WidgetState] value as either active or inactive.

### addMaterialState()

```dart
void addMaterialState(WidgetState state)
```

Mutator to mark a [WidgetState] value as active.

### removeMaterialState()

```dart
void removeMaterialState(WidgetState state)
```

Mutator to mark a [WidgetState] value as inactive.

### isDisabled

```dart
bool get isDisabled
```

Getter for whether this class considers [WidgetState.disabled] to be active.

### isDragged

```dart
bool get isDragged
```

Getter for whether this class considers [WidgetState.dragged] to be active.

### isErrored

```dart
bool get isErrored
```

Getter for whether this class considers [WidgetState.error] to be active.

### isFocused

```dart
bool get isFocused
```

Getter for whether this class considers [WidgetState.focused] to be active.

### isHovered

```dart
bool get isHovered
```

Getter for whether this class considers [WidgetState.hovered] to be active.

### isPressed

```dart
bool get isPressed
```

Getter for whether this class considers [WidgetState.pressed] to be active.

### isScrolledUnder

```dart
bool get isScrolledUnder
```

Getter for whether this class considers [WidgetState.scrolledUnder] to be active.

### isSelected

```dart
bool get isSelected
```

Getter for whether this class considers [WidgetState.selected] to be active.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
