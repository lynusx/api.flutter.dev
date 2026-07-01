# Placeholder

```dart
class Placeholder extends StatelessWidget {}
```

A widget that draws a box that represents where other widgets will one day be added.

This widget is useful during development to indicate that the interface is not yet complete.

By default, the placeholder is sized to fit its container. If the placeholder is in an unbounded space, it will size itself according to the given [fallbackWidth] and [fallbackHeight].

{@youtube 560 315 https://www.youtube.com/watch?v=LPe56fezmoo}

### Placeholder()

```dart
Placeholder({dynamic key, Color color = const Color(0xFF455A64), double strokeWidth = 2.0, double fallbackWidth = 400.0, double fallbackHeight = 400.0, Widget? child})
```

Creates a widget which draws a box.

### color

```dart
Color color
```

The color to draw the placeholder box.

### strokeWidth

```dart
double strokeWidth
```

The width of the lines in the placeholder box.

### fallbackWidth

```dart
double fallbackWidth
```

The width to use when the placeholder is in a situation with an unbounded width.

See also:

- [fallbackHeight], the same but vertically.

### fallbackHeight

```dart
double fallbackHeight
```

The height to use when the placeholder is in a situation with an unbounded height.

See also:

- [fallbackWidth], the same but horizontally.

### child

```dart
Widget? child
```

The [child] contained by the placeholder box.

Defaults to null.

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
