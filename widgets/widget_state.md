@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/scheduler.dart';

# WidgetStatesConstraint

```dart
mixin WidgetStatesConstraint {}
```

This mixin allows [WidgetState] enum values to be combined using the `&`, `|`, and `~` operators.

A [Map] with [WidgetStatesConstraint] objects as keys can be used in the [WidgetStateProperty.fromMap] constructor to resolve to one of its values, based on the first key that [isSatisfiedBy] the current set of states.

{@macro flutter.widgets.WidgetStateMap}

### isSatisfiedBy()

```dart
bool isSatisfiedBy(Set<WidgetState> states)
```

Whether the provided [states] satisfy this object's criteria.

If the constraint is a single [WidgetState] object, it's satisfied by the set if the set contains the object.

The constraint can also be created using one or more operators, for example:

{@template flutter.widgets.WidgetStatesConstraint.isSatisfiedBy}

```dart
final WidgetStatesConstraint constraint = WidgetState.focused | WidgetState.hovered;
```

In the above case, `constraint.isSatisfiedBy(states)` is equivalent to:

```dart
states.contains(WidgetState.focused) || states.contains(WidgetState.hovered);
```

{@endtemplate}

### operator &()

```dart
WidgetStatesConstraint operator &(WidgetStatesConstraint other)
```

Combines two [WidgetStatesConstraint] values using logical "and".

### operator |()

```dart
WidgetStatesConstraint operator |(WidgetStatesConstraint other)
```

Combines two [WidgetStatesConstraint] values using logical "or".

### operator ~()

```dart
WidgetStatesConstraint operator ~()
```

Takes a [WidgetStatesConstraint] and applies the logical "not".

# WidgetState

```dart
enum WidgetState {}
```

Interactive states that some of the widgets can take on when receiving input from the user.

States are defined by https://m3.material.io/foundations/interaction/states, but are not limited to the Material design system or library.

Some widgets track their current state in a `Set<WidgetState>`.

See also:

- [MaterialState], the Material specific version of `WidgetState`.
- [WidgetStateProperty], an interface for objects that "resolve" to different values depending on a widget's state. {@template flutter.widgets.WidgetStateProperty.implementations}
- [WidgetStateColor], a [Color] that implements `WidgetStateProperty` which is used in APIs that need to accept either a [Color] or a `WidgetStateProperty<Color>`.
- [WidgetStateMouseCursor], a [MouseCursor] that implements `WidgetStateProperty` which is used in APIs that need to accept either a [MouseCursor] or a [WidgetStateProperty<MouseCursor>].
- [WidgetStateOutlinedBorder], an [OutlinedBorder] that implements `WidgetStateProperty` which is used in APIs that need to accept either an [OutlinedBorder] or a [WidgetStateProperty<OutlinedBorder>].
- [WidgetStateBorderSide], a [BorderSide] that implements `WidgetStateProperty` which is used in APIs that need to accept either a [BorderSide] or a [WidgetStateProperty<BorderSide>].
- [WidgetStateTextStyle], a [TextStyle] that implements `WidgetStateProperty` which is used in APIs that need to accept either a [TextStyle] or a [WidgetStateProperty<TextStyle>]. {@endtemplate}

The state when the user drags their mouse cursor over the given widget.

See: https://material.io/design/interaction/states.html#hover.

The state when the user navigates with the keyboard to a given widget.

This can also sometimes be triggered when a widget is tapped. For example, when a [TextField] is tapped, it becomes [focused].

See: https://material.io/design/interaction/states.html#focus.

The state when the user is actively pressing down on the given widget.

See: https://material.io/design/interaction/states.html#pressed.

The state when this widget is being dragged from one place to another by the user.

https://material.io/design/interaction/states.html#dragged.

The state when this item has been selected.

This applies to things that can be toggled (such as chips and checkboxes) and things that are selected from a set of options (such as tabs and radio buttons).

See: https://material.io/design/interaction/states.html#selected.

The state when this widget overlaps the content of a scrollable below.

Used by [AppBar] to indicate that the primary scrollable's content has scrolled up and behind the app bar.

The state when this widget is disabled and cannot be interacted with.

Disabled widgets should not respond to hover, focus, press, or drag interactions.

See: https://material.io/design/interaction/states.html#disabled.

The state when the widget has entered some form of invalid state.

See https://material.io/design/interaction/states.html#usage.

### any

```dart
WidgetStatesConstraint any
```

{@template flutter.widgets.WidgetState.any} To prevent a situation where each [WidgetStatesConstraint] isn't satisfied by the given set of states, consider adding [WidgetState.any] as the final [WidgetStateMap] key. {@endtemplate}

### isSatisfiedBy()

```dart
bool isSatisfiedBy(Set<WidgetState> states)
```

# WidgetPropertyResolver

```dart
typedef WidgetPropertyResolver<T> = T Function(Set<WidgetState> states)
```

Signature for the function that returns a value of type `T` based on a given set of states.

# WidgetStateColor

```dart
abstract class WidgetStateColor extends Color implements WidgetStateProperty<Color> {}
```

Defines a [Color] that is also a [WidgetStateProperty].

This class exists to enable widgets with [Color] valued properties to also accept [WidgetStateProperty<Color>] values. A widget state color property represents a color which depends on a widget's "interactive state". This state is represented as a [Set] of [WidgetState]s, like [WidgetState.pressed], [WidgetState.focused] and [WidgetState.hovered].

[WidgetStateColor] should only be used with widgets that document their support, like [TimePickerThemeData.dayPeriodColor].

A [WidgetStateColor] can be created in one of the following ways:

1.  Create a subclass of [WidgetStateColor] and implement the abstract `resolve` method.
2.  Use [WidgetStateColor.resolveWith] and pass in a callback that will be used to resolve the color in the given states.
3.  Use [WidgetStateColor.fromMap] to assign a value using a [WidgetStateMap].

{@tool snippet}

This example defines a [WidgetStateColor] with a const constructor.

```dart
class MyColor extends WidgetStateColor {
  const MyColor() : super(_defaultColor);

  static const int _defaultColor = 0xcafefeed;
  static const int _pressedColor = 0xdeadbeef;

  @override
  Color resolve(Set<WidgetState> states) {
    if (states.contains(WidgetState.pressed)) {
      return const Color(_pressedColor);
    }
    return const Color(_defaultColor);
  }
}
```

{@end-tool}

### WidgetStateColor()

```dart
WidgetStateColor(dynamic defaultValue)
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### WidgetStateColor.resolveWith()

```dart
WidgetStateColor.resolveWith(WidgetPropertyResolver<Color> callback)
```

Creates a [WidgetStateColor] from a [WidgetPropertyResolver<Color>] callback function.

If used as a regular color, the color resolved in the default state (the empty set of states) will be used.

The given callback parameter must return a non-null color in the default state.

### WidgetStateColor.fromMap()

```dart
WidgetStateColor.fromMap(WidgetStateMap<Color> map)
```

Creates a [WidgetStateColor] from a [WidgetStateMap<Color>].

{@macro flutter.widgets.WidgetStateProperty.fromMap} It should only be used with widgets that document support for [WidgetStateColor] (throws an error if used as a normal [Color]).

{@macro flutter.widgets.WidgetState.any}

### resolve()

```dart
Color resolve(Set<WidgetState> states)
```

Returns a [Color] that's to be used when a component is in the specified state.

### transparent

```dart
WidgetStateColor transparent
```

A constant whose value is transparent for all states.

# WidgetStateMouseCursor

```dart
abstract class WidgetStateMouseCursor extends MouseCursor implements WidgetStateProperty<MouseCursor> {}
```

Defines a [MouseCursor] whose value depends on a set of [WidgetState]s which represent the interactive state of a component.

This kind of [MouseCursor] is useful when the set of interactive actions a widget supports varies with its state. For example, a mouse pointer hovering over a disabled [ListTile] should not display [SystemMouseCursors.click], since a disabled list tile doesn't respond to mouse clicks. [ListTile]'s default mouse cursor is a [WidgetStateMouseCursor.clickable], which resolves to [SystemMouseCursors.basic] when the button is disabled.

This class should only be used for parameters that document their support for [WidgetStateMouseCursor].

A [WidgetStateMouseCursor] can be created in one of the following ways:

1.  Create a subclass of [WidgetStateMouseCursor] and implement the abstract `resolve` method.
2.  Use [WidgetStateMouseCursor.resolveWith] and pass in a callback that will be used to resolve the color in the given states.
3.  Use [WidgetStateMouseCursor.fromMap] to assign a value using a [WidgetStateMap].

{@tool dartpad} This example defines a mouse cursor that resolves to [SystemMouseCursors.forbidden] when its widget is disabled.

** See code in examples/api/lib/widgets/widget_state/widget_state_mouse_cursor.0.dart ** {@end-tool}

See also:

- [MouseCursor] for introduction on the mouse cursor system.
- [SystemMouseCursors], which defines cursors that are supported by native platforms.

### WidgetStateMouseCursor()

```dart
WidgetStateMouseCursor()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### WidgetStateMouseCursor.resolveWith()

```dart
WidgetStateMouseCursor.resolveWith(WidgetPropertyResolver<MouseCursor> callback, {String debugDescription})
```

Creates a [WidgetStateMouseCursor] using a [WidgetPropertyResolver] callback.

A [debugDescription] may optionally be provided.

If used as a regular [MouseCursor], the cursor resolved in the default state (the empty set of states) will be used.

### WidgetStateMouseCursor.fromMap()

```dart
WidgetStateMouseCursor.fromMap(WidgetStateMap<MouseCursor> map)
```

Creates a [WidgetStateMouseCursor] from a [WidgetStateMap].

{@macro flutter.widgets.WidgetStateProperty.fromMap} It should only be used with classes that document support for [WidgetStateMouseCursor] (throws an error if used as a regular [MouseCursor].)

### createSession()

```dart
MouseCursorSession createSession(int device)
```

### resolve()

```dart
MouseCursor resolve(Set<WidgetState> states)
```

Returns a [MouseCursor] that's to be used when a component is in the specified state.

### clickable

```dart
WidgetStateMouseCursor clickable
```

A mouse cursor for clickable widgets, which resolves differently when the widget is disabled.

By default this cursor resolves to [SystemMouseCursors.click]. If the widget is disabled, the cursor resolves to [SystemMouseCursors.basic].

### adaptiveClickable

```dart
WidgetStateMouseCursor adaptiveClickable
```

A platform-adaptive mouse cursor for clickable widgets, which resolves differently based on the widget's state and the platform.

On web platforms, this cursor resolves to [SystemMouseCursors.click] by default. If the widget is disabled, it resolves to [SystemMouseCursors.basic].

On non-web platforms, this cursor always resolves to [SystemMouseCursors.basic].

This cursor is commonly used for interactive widgets like buttons. The difference in behavior across platforms reflects native conventions (e.g., web uses a hand pointer for buttons, while desktop platforms do not).

### textable

```dart
WidgetStateMouseCursor textable
```

A mouse cursor for widgets related to text, which resolves differently when the widget is disabled.

By default this cursor resolves to [SystemMouseCursors.text]. If the widget is disabled, the cursor resolves to [SystemMouseCursors.basic].

This cursor is the default for many widgets.

# WidgetStateBorderSide

```dart
abstract class WidgetStateBorderSide extends BorderSide implements WidgetStateProperty<BorderSide?> {}
```

Defines a [BorderSide] whose value depends on a set of [WidgetState]s which represent the interactive state of a component.

This class enables existing widget implementations with [BorderSide] properties to be extended to also effectively support `WidgetStateProperty<BorderSide>` property values. It should only be used for parameters that document support for [WidgetStateBorderSide] objects.

A [WidgetStateBorderSide] can be created in one of the following ways:

1.  Create a subclass of [WidgetStateBorderSide] and implement the abstract `resolve` method.
2.  Use [WidgetStateBorderSide.resolveWith] and pass in a callback that will be used to resolve the color in the given states.
3.  Use [WidgetStateBorderSide.fromMap] to assign a value using a [WidgetStateMap].

{@tool dartpad} This example defines a [WidgetStateBorderSide] which resolves to different border colors depending on how the user interacts with it.

** See code in examples/api/lib/widgets/widget_state/widget_state_border_side.0.dart ** {@end-tool}

### WidgetStateBorderSide()

```dart
WidgetStateBorderSide()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### WidgetStateBorderSide.resolveWith()

```dart
WidgetStateBorderSide.resolveWith(WidgetPropertyResolver<BorderSide?> callback)
```

Creates a [WidgetStateBorderSide] from a [WidgetPropertyResolver<BorderSide?>] callback function.

If used as a regular [BorderSide], its behavior matches an empty `BorderSide()` constructor.

Usage:

```dart
ChipTheme(
  data: Theme.of(context).chipTheme.copyWith(
    side: WidgetStateBorderSide.resolveWith((Set<WidgetState> states) {
      if (states.contains(WidgetState.selected)) {
        return const BorderSide(color: Colors.red);
      }
      return null;  // Defer to default value on the theme or widget.
    }),
  ),
  child: const Chip(
    label: Text('Transceiver'),
  ),
),
```

Alternatively:

```dart
Chip(
  label: const Text('Transceiver'),
  side: WidgetStateBorderSide.resolveWith((Set<WidgetState> states) {
    if (states.contains(WidgetState.selected)) {
      return const BorderSide(color: Colors.red);
    }
    return null;  // Defer to default value on the theme or widget.
  }),
),
```

### WidgetStateBorderSide.fromMap()

```dart
WidgetStateBorderSide.fromMap(WidgetStateMap<BorderSide?> map)
```

Creates a [WidgetStateBorderSide] from a [WidgetStateMap].

{@macro flutter.widgets.WidgetStateProperty.fromMap} It should only be used with widgets that document support for [WidgetStateBorderSide] objects (throws an error if used as a regular [BorderSide].)

Example:

```dart
const Chip(
  label: Text('Transceiver'),
  side: WidgetStateBorderSide.fromMap(<WidgetStatesConstraint, BorderSide?>{
    WidgetState.selected: BorderSide(color: Colors.red),
    // returns null if not selected, deferring to default theme/widget value.
  }),
),
```

{@macro flutter.widgets.WidgetState.any}

### resolve()

```dart
BorderSide? resolve(Set<WidgetState> states)
```

Returns a [BorderSide] that's to be used when a Widget is in the specified state. Return null to defer to the default value of the widget or theme.

### lerp()

```dart
WidgetStateProperty<BorderSide?>? lerp(WidgetStateProperty<BorderSide?>? a, WidgetStateProperty<BorderSide?>? b, double t)
```

Linearly interpolate between two [WidgetStateProperty]s of [BorderSide].

# WidgetStateOutlinedBorder

```dart
abstract class WidgetStateOutlinedBorder extends OutlinedBorder implements WidgetStateProperty<OutlinedBorder?> {}
```

Defines an [OutlinedBorder] whose value depends on a set of [WidgetState]s which represent the interactive state of a component.

A [WidgetStateOutlinedBorder] can be created in one of the following ways:

1.  Create a subclass of [WidgetStateOutlinedBorder] and implement the abstract `resolve` method.
2.  Use [WidgetStateOutlinedBorder.resolveWith] and pass in a callback that will be used to resolve the color in the given states.
3.  Use [WidgetStateOutlinedBorder.fromMap] to assign a value using a [WidgetStateMap].

{@tool dartpad} This example defines a subclass of [RoundedRectangleBorder] and an implementation of [WidgetStateOutlinedBorder], that resolves to [RoundedRectangleBorder] when its widget is selected.

** See code in examples/api/lib/widgets/widget_state/widget_state_outlined_border.0.dart ** {@end-tool}

This class should only be used for parameters which are documented to take [WidgetStateOutlinedBorder], otherwise only the default state will be used.

See also:

- [ShapeBorder] the base class for shape outlines.

### WidgetStateOutlinedBorder()

```dart
WidgetStateOutlinedBorder()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### WidgetStateOutlinedBorder.resolveWith()

```dart
WidgetStateOutlinedBorder.resolveWith(WidgetPropertyResolver<OutlinedBorder?> callback)
```

Creates a [WidgetStateOutlinedBorder] using a [WidgetPropertyResolver] callback.

This constructor should only be used with widgets that support [WidgetStateOutlinedBorder], such as [ChipThemeData.shape] (if used as a regular [OutlinedBorder], it acts the same as an empty `RoundedRectangleBorder()` constructor).

### WidgetStateOutlinedBorder.fromMap()

```dart
WidgetStateOutlinedBorder.fromMap(WidgetStateMap<OutlinedBorder?> map)
```

Creates a [WidgetStateOutlinedBorder] from a [WidgetStateMap].

{@macro flutter.widgets.WidgetStateProperty.fromMap} It should only be used with widgets that support [WidgetStateOutlinedBorder], such as [ChipThemeData.shape] (throws an error if used as a regular [OutlinedBorder]).

Resolves to `null` if no keys match, deferring to the default value of the widget or theme.

### resolve()

```dart
OutlinedBorder? resolve(Set<WidgetState> states)
```

Returns an [OutlinedBorder] that's to be used when a component is in the specified state. Return null to defer to the default value of the widget or theme.

# WidgetStateTextStyle

```dart
abstract class WidgetStateTextStyle extends TextStyle implements WidgetStateProperty<TextStyle> {}
```

Defines a [TextStyle] that is also a [WidgetStateProperty].

This class exists to enable widgets with [TextStyle] valued properties to also accept [WidgetStateProperty<TextStyle>] values. A widget state text style property represents a text style which depends on a widget's "interactive state". This state is represented as a [Set] of [WidgetState]s, like [WidgetState.pressed], [WidgetState.focused] and [WidgetState.hovered].

[WidgetStateTextStyle] should only be used with widgets that document their support, like [InputDecoration.labelStyle].

A [WidgetStateTextStyle] can be created in one of the following ways:

1.  Create a subclass of [WidgetStateTextStyle] and implement the abstract `resolve` method.
2.  Use [WidgetStateTextStyle.resolveWith] and pass in a callback that will be used to resolve the text style in the given states.
3.  Use [WidgetStateTextStyle.fromMap] to assign a style using a [WidgetStateMap].

### WidgetStateTextStyle()

```dart
WidgetStateTextStyle()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### WidgetStateTextStyle.resolveWith()

```dart
WidgetStateTextStyle.resolveWith(WidgetPropertyResolver<TextStyle> callback)
```

Creates a [WidgetStateTextStyle] from a [WidgetPropertyResolver<TextStyle>] callback function.

Behaves like an empty `TextStyle()` constructor if used as a regular [TextStyle].

The given callback parameter must return a non-null text style in the default state.

### WidgetStateTextStyle.fromMap()

```dart
WidgetStateTextStyle.fromMap(WidgetStateMap<TextStyle> map)
```

Creates a [WidgetStateTextStyle] from a [WidgetStateMap].

{@macro flutter.widgets.WidgetStateProperty.fromMap} It should only be used with widgets that document support for [WidgetStateTextStyle] objects (throws an error if used as a regular [TextStyle]).

{@macro flutter.widgets.WidgetState.any}

### resolve()

```dart
TextStyle resolve(Set<WidgetState> states)
```

Returns a [TextStyle] that's to be used when a component is in the specified state.

# WidgetStateProperty

```dart
abstract class WidgetStateProperty<T> {}
```

Interface for classes that [resolve] to a value of type `T` based on a widget's interactive "state", which is defined as a set of [WidgetState]s.

Widget state properties represent values that depend on a widget's "state". The state is encoded as a set of [WidgetState] values, like [WidgetState.focused], [WidgetState.hovered], [WidgetState.pressed]. For example the [InkWell.overlayColor] defines the color that fills the ink well when it's pressed (the "splash color"), focused, or hovered. The [InkWell] uses the overlay color's [resolve] method to compute the color for the ink well's current state.

[ButtonStyle], which is used to configure the appearance of buttons like [TextButton], [ElevatedButton], and [OutlinedButton], has many material state properties. The button widgets keep track of their current material state and [resolve] the button style's material state properties when their value is needed.

{@tool dartpad} This example shows how the default text and icon color (the "foreground color") of a [TextButton] can be overridden with a [WidgetStateProperty]. In this example, the button's text color will be colored differently depending on whether the button is pressed, hovered, or focused.

** See code in examples/api/lib/widgets/widget_state/widget_state_property.0.dart ** {@end-tool}

## Performance Consideration

In order for constructed [WidgetStateProperty] objects to be recognized as equivalent, they need to either be `const` objects, or have overrides for [operator==] and [hashCode].

This comes into play when, for instance, two [ThemeData] objects are being compared for equality.

For a concrete `WidgetStateProperty` object that supports stable equality checks, consider using [WidgetStateMapper].

See also:

- [MaterialStateProperty], the Material specific version of `WidgetStateProperty`. {@macro flutter.widgets.WidgetStateProperty.implementations}

### WidgetStateProperty()

```dart
WidgetStateProperty()
```

This abstract constructor allows extending the class.

[WidgetStateProperty] is designed as an interface, so this constructor is only needed for backward compatibility.

### WidgetStateProperty.fromMap()

```dart
WidgetStateProperty.fromMap(WidgetStateMap<T> map)
```

Creates a property that resolves using a [WidgetStateMap].

{@template flutter.widgets.WidgetStateProperty.fromMap} This constructor's [resolve] method finds the first [MapEntry] whose key is satisfied by the set of states, and returns its associated value. {@endtemplate}

Resolves to `null` if no keys match, or if [T] is non-nullable, the method throws an [ArgumentError]. {@macro flutter.widgets.WidgetState.any}

{@macro flutter.widgets.WidgetStateMap}

### resolveAs()

```dart
T resolveAs<T>(T value, Set<WidgetState> states)
```

Resolves the value for the given set of states if `value` is a [WidgetStateProperty], otherwise returns the value itself.

This is useful for widgets that have parameters which can optionally be a [WidgetStateProperty]. For example, [InkWell.mouseCursor] can be a [MouseCursor] or a [WidgetStateProperty<MouseCursor>].

### resolveWith()

```dart
WidgetStateProperty<T> resolveWith<T>(WidgetPropertyResolver<T> callback)
```

Convenience method for creating a [WidgetStateProperty] from a [WidgetPropertyResolver] function alone.

### all()

```dart
WidgetStateProperty<T> all<T>(T value)
```

Convenience method for creating a [WidgetStateProperty] that resolves to a single value for all states.

Prefer using [WidgetStatePropertyAll] directly, which allows for creating `const` values.

### lerp()

```dart
WidgetStateProperty<T?>? lerp<T>(WidgetStateProperty<T>? a, WidgetStateProperty<T>? b, double t, T? Function(T?, T?, double) lerpFunction)
```

Linearly interpolate between two [WidgetStateProperty]s.

### resolve()

```dart
T resolve(Set<WidgetState> states)
```

Returns a value of type `T` that depends on [states].

Widgets like [TextButton] and [ElevatedButton] apply this method to their current [WidgetState]s to compute colors and other visual parameters at build time.

# WidgetStateMap

```dart
typedef WidgetStateMap<T> = Map<WidgetStatesConstraint, T>
```

A [Map] used to resolve to a single value of type `T` based on the current set of Widget states.

{@template flutter.widgets.WidgetStateMap} Example:

```dart
// This WidgetStateMap<Color?> resolves to null if no keys match.
WidgetStateProperty<Color?>.fromMap(<WidgetStatesConstraint, Color?>{
  WidgetState.error: Colors.red,
  WidgetState.hovered & WidgetState.focused: Colors.blueAccent,
  WidgetState.focused: Colors.blue,
  ~WidgetState.disabled: Colors.black,
});

// The same can be accomplished with a WidgetPropertyResolver,
// but it's more verbose:
WidgetStateProperty.resolveWith<Color?>((Set<WidgetState> states) {
  if (states.contains(WidgetState.error)) {
    return Colors.red;
  } else if (states.contains(WidgetState.hovered) && states.contains(WidgetState.focused)) {
    return Colors.blueAccent;
  } else if (states.contains(WidgetState.focused)) {
    return Colors.blue;
  } else if (!states.contains(WidgetState.disabled)) {
    return Colors.black;
  }
  return null;
});
```

A widget state combination can be stored in a variable, and [WidgetState.any] can be used for non-nullable types to ensure that there's a match:

```dart
final WidgetStatesConstraint selectedError = WidgetState.selected & WidgetState.error;

final WidgetStateProperty<Color> color = WidgetStateProperty<Color>.fromMap(
  <WidgetStatesConstraint, Color>{
    selectedError & WidgetState.hovered: Colors.redAccent,
    selectedError: Colors.red,
    WidgetState.any: Colors.black,
  },
);

// The (more verbose) WidgetPropertyResolver implementation:
final WidgetStateProperty<Color> colorResolveWith = WidgetStateProperty.resolveWith<Color>(
  (Set<WidgetState> states) {
    if (states.containsAll(<WidgetState>{WidgetState.selected, WidgetState.error})) {
      if (states.contains(WidgetState.hovered)) {
        return Colors.redAccent;
      }
      return Colors.red;
    }
    return Colors.black;
  },
);
```

{@endtemplate}

# WidgetStateMapper

```dart
class WidgetStateMapper<T> with Diagnosticable implements WidgetStateProperty<T> {}
```

Uses a [WidgetStateMap] to resolve to a single value of type `T` based on the current set of Widget states.

{@macro flutter.widgets.WidgetStateMap}

Classes that extend [WidgetStateMapper] can implement any other interface, but should only be used for fields that document their support for [WidgetStateProperty] objects.

The only exceptions are classes such as [double] that are marked as `base` or `final`, since they can't be implemented—a [double] property can't be set up to also accept [WidgetStateProperty] objects and would need to pick one or the other.

For example, a [WidgetStateColor.fromMap] object can be passed anywhere that accepts either a [Color] or a [WidgetStateProperty] object, but attempting to access a [Color] field (such as [Color.value]) on the mapper object throws a [FlutterError].

### WidgetStateMapper()

```dart
WidgetStateMapper(WidgetStateMap<T> map)
```

Creates a [WidgetStateProperty] object that can resolve to a value of type [T] using the provided [map].

### resolve()

```dart
T resolve(Set<WidgetState> states)
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString({DiagnosticLevel minLevel = DiagnosticLevel.info})
```

### noSuchMethod()

```dart
Never noSuchMethod(Invocation invocation)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties, {String prefix = ''})
```

# WidgetStatePropertyAll

```dart
class WidgetStatePropertyAll<T> implements WidgetStateProperty<T> {}
```

Convenience class for creating a [WidgetStateProperty] that resolves to the given value for all states.

See also:

- [MaterialStatePropertyAll], the Material specific version of `WidgetStatePropertyAll`.

### WidgetStatePropertyAll()

```dart
WidgetStatePropertyAll(T value)
```

Constructs a [WidgetStateProperty] that always resolves to the given value.

### value

```dart
T value
```

The value of the property that will be used for all states.

### resolve()

```dart
T resolve(Set<WidgetState> states)
```

### toString()

```dart
String toString()
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# WidgetStatesController

```dart
class WidgetStatesController extends ValueNotifier<Set<WidgetState>> {}
```

Manages a set of [WidgetState]s and notifies listeners of changes.

Used by widgets that expose their internal state for the sake of extensions that add support for additional states. See [TextButton] for an example.

The controller's [value] is its current set of states. Listeners are notified whenever the [value] changes. The [value] should only be changed with [update]; it should not be modified directly.

The controller's [value] represents the set of states that a widget's visual properties, typically [WidgetStateProperty] values, are resolved against. It is _not_ the intrinsic state of the widget. The widget is responsible for ensuring that the controller's [value] tracks its intrinsic state. For example one cannot request the keyboard focus for a widget by adding [WidgetState.focused] to its controller. When the widget gains the or loses the focus it will [update] its controller's [value] and notify listeners of the change.

When calling `setState` in a [WidgetStatesController] listener, use the [SchedulerBinding.addPostFrameCallback] to delay the call to `setState` after the frame has been rendered. It's generally prudent to use the [SchedulerBinding.addPostFrameCallback] because some of the widgets that depend on [WidgetStatesController] may call [update] in their build method. In such cases, listener's that call `setState` - during the build phase - will cause an error.

See also:

- [MaterialStatesController], the Material specific version of `WidgetStatesController`.

### WidgetStatesController()

```dart
WidgetStatesController([Set<WidgetState>? value])
```

Creates a WidgetStatesController.

### update()

```dart
void update(WidgetState state, bool add)
```

Adds [state] to [value] if [add] is true, and removes it otherwise, and notifies listeners if [value] has changed.
