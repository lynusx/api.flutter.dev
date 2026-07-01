@docImport 'dart:ui';

# CupertinoFocusHalo

```dart
class CupertinoFocusHalo extends StatefulWidget {}
```

Applies an iOS-style focus border around its child when any of child focus nodes gain focus.

The shape of the focus halo does not automatically adapt to the child widget it encloses. You are responsible for specifying a shape that correctly matches the child's geometry by using the appropriate constructor, such as [CupertinoFocusHalo.withRect] or [CupertinoFocusHalo.withRRect].

See also:

- <https://developer.apple.com/design/human-interface-guidelines/focus-and-selection/>

### CupertinoFocusHalo.withRect()

```dart
CupertinoFocusHalo.withRect({required Widget child, dynamic key})
```

Creates a rectangular [CupertinoFocusHalo] around the child.

For example, to highlight a rectangular section of the widget tree when any button inside that section has focus, one could write:

```dart
CupertinoFocusHalo.withRect(
  child: Column(
    children: <Widget>[
      CupertinoButton(child: const Text('Child 1'), onPressed: () {}),
      CupertinoButton(child: const Text('Child 2'), onPressed: () {}),
    ],
  ),
)
```

### CupertinoFocusHalo.withRRect()

```dart
CupertinoFocusHalo.withRRect({required Widget child, required BorderRadiusGeometry borderRadius, dynamic key})
```

Creates a rounded rectangular [CupertinoFocusHalo] around the child

For example, to highlight a rounded rectangular section of the widget tree when any button inside that section has focus, one could write:

```dart
CupertinoFocusHalo.withRRect(
  borderRadius: BorderRadius.circular(10.0),
  child: Column(
    children: <Widget>[
      CupertinoButton(child: const Text('Child 1'), onPressed: () {}),
      CupertinoButton(child: const Text('Child 2'), onPressed: () {}),
    ],
  ),
)
```

### CupertinoFocusHalo.withRoundedSuperellipse()

```dart
CupertinoFocusHalo.withRoundedSuperellipse({required Widget child, required BorderRadiusGeometry borderRadius, dynamic key})
```

Creates a rounded superellipse-shaped [CupertinoFocusHalo] around the child

For example, to highlight a rounded superellipse-shaped section of the widget tree when any button inside that section has focus, one could write:

```dart
CupertinoFocusHalo.withRoundedSuperellipse(
  borderRadius: BorderRadius.circular(10.0),
  child: Column(
    children: <Widget>[
      CupertinoButton(child: const Text('Child 1'), onPressed: () {}),
      CupertinoButton(child: const Text('Child 2'), onPressed: () {}),
    ],
  ),
)
```

See also:

- [RSuperellipse] and [RoundedSuperellipseBorder] for more introduction on the rounded superellipse shape.

### child

```dart
Widget child
```

The child to draw the focused border around.

Since [CupertinoFocusHalo] can't request focus to itself, this [child] should contain widget(s) that can request focus.

The child widget is responsible for its own visual shape, for example by using an appropriate clipping.

### createState()

```dart
State<CupertinoFocusHalo> createState()
```
