@docImport 'package:flutter/material.dart';

# NotchedShape

```dart
abstract class NotchedShape {}
```

A shape with a notch in its outline.

Typically used as the outline of a 'host' widget to make a notch that accommodates a 'guest' widget. e.g the [BottomAppBar] may have a notch to accommodate the [FloatingActionButton].

See also:

- [ShapeBorder], which defines a shaped border without a dynamic notch.
- [AutomaticNotchedShape], an adapter from [ShapeBorder] to [NotchedShape].

### NotchedShape()

```dart
NotchedShape()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### getOuterPath()

```dart
Path getOuterPath(Rect host, Rect? guest)
```

Creates a [Path] that describes the outline of the shape.

The `host` is the bounding rectangle of the shape.

The `guest` is the bounding rectangle of the shape for which a notch will be made. It is null when there is no guest.

# CircularNotchedRectangle

```dart
class CircularNotchedRectangle extends NotchedShape {}
```

A rectangle with a smooth circular notch.

See also:

- [CircleBorder], a [ShapeBorder] that describes a circle.

### CircularNotchedRectangle()

```dart
CircularNotchedRectangle({bool inverted = false})
```

Creates a [CircularNotchedRectangle].

The same object can be used to create multiple shapes.

### inverted

```dart
bool inverted
```

If [inverted] is true, the notch is placed at the bottom of the rectangle.

### getOuterPath()

```dart
Path getOuterPath(Rect host, Rect? guest)
```

Creates a [Path] that describes a rectangle with a smooth circular notch.

`host` is the bounding box for the returned shape. Conceptually this is the rectangle to which the notch will be applied.

`guest` is the bounding box of a circle that the notch accommodates. All points in the circle bounded by `guest` will be outside of the returned path.

The notch is curve that smoothly connects the host's top edge and the guest circle.

# AutomaticNotchedShape

```dart
class AutomaticNotchedShape extends NotchedShape {}
```

A [NotchedShape] created from [ShapeBorder]s.

Two shapes can be provided. The [host] is the shape of the widget that uses the [NotchedShape] (typically a [BottomAppBar]). The [guest] is subtracted from the [host] to create the notch (typically to make room for a [FloatingActionButton]).

### AutomaticNotchedShape()

```dart
AutomaticNotchedShape(ShapeBorder host, [ShapeBorder? guest])
```

Creates a [NotchedShape] that is defined by two [ShapeBorder]s.

The [guest] may be null, in which case no notch is created even if a guest rectangle is provided to [getOuterPath].

### host

```dart
ShapeBorder host
```

The shape of the widget that uses the [NotchedShape] (typically a [BottomAppBar]).

This shape cannot depend on the [TextDirection], as no text direction is available to [NotchedShape]s.

### guest

```dart
ShapeBorder? guest
```

The shape to subtract from the [host] to make the notch.

This shape cannot depend on the [TextDirection], as no text direction is available to [NotchedShape]s.

If this is null, [getOuterPath] ignores the guest rectangle.

### getOuterPath()

```dart
Path getOuterPath(Rect hostRect, Rect? guestRect)
```
