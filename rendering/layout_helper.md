# ChildLayouter

```dart
typedef ChildLayouter = Size Function(RenderBox child, BoxConstraints constraints)
```

Signature for a function that takes a [RenderBox] and returns the [Size] that the [RenderBox] would have if it were laid out with the given [BoxConstraints].

[ChildLayoutHelper.dryLayoutChild] and [ChildLayoutHelper.layoutChild] adhere to this signature.

# ChildBaselineGetter

```dart
typedef ChildBaselineGetter = double? Function(RenderBox child, BoxConstraints constraints, TextBaseline baseline)
```

Signature for a function that takes a [RenderBox] and returns the baseline offset this [RenderBox] would have if it were laid out with the given [BoxConstraints].

[ChildLayoutHelper.getDryBaseline] and [ChildLayoutHelper.getBaseline] adhere to this signature.

# ChildLayoutHelper

```dart
abstract final class ChildLayoutHelper {}
```

A collection of static functions to layout a [RenderBox] child with the given set of [BoxConstraints].

All of the functions adhere to the [ChildLayouter] signature.

### dryLayoutChild()

```dart
Size dryLayoutChild(RenderBox child, BoxConstraints constraints)
```

Returns the [Size] that the [RenderBox] would have if it were to be laid out with the given [BoxConstraints].

This method calls [RenderBox.getDryLayout] on the given [RenderBox].

This method should only be called by the parent of the provided [RenderBox] child as it binds parent and child together (if the child is marked as dirty, the child will also be marked as dirty).

See also:

- [layoutChild], which actually lays out the child with the given constraints.

### layoutChild()

```dart
Size layoutChild(RenderBox child, BoxConstraints constraints)
```

Lays out the [RenderBox] with the given constraints and returns its [Size].

This method calls [RenderBox.layout] on the given [RenderBox] with `parentUsesSize` set to true to receive its [Size].

This method should only be called by the parent of the provided [RenderBox] child as it binds parent and child together (if the child is marked as dirty, the child will also be marked as dirty).

See also:

- [dryLayoutChild], which does not perform a real layout of the child.

### getDryBaseline()

```dart
double? getDryBaseline(RenderBox child, BoxConstraints constraints, TextBaseline baseline)
```

Convenience function that calls [RenderBox.getDryBaseline].

### getBaseline()

```dart
double? getBaseline(RenderBox child, BoxConstraints constraints, TextBaseline baseline)
```

Convenience function that calls [RenderBox.getDistanceToBaseline].

The given `child` must be already laid out with `constraints`.
