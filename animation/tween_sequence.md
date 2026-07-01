# TweenSequence

```dart
class TweenSequence<T> extends Animatable<T> {}
```

Enables creating an [Animation] whose value is defined by a sequence of [Tween]s.

Each [TweenSequenceItem] has a weight that defines its percentage of the animation's duration. Each tween defines the animation's value during the interval indicated by its weight.

{@tool snippet} This example defines an animation that uses an easing curve to interpolate between 5.0 and 10.0 during the first 40% of the animation, remains at 10.0 for the next 20%, and then returns to 5.0 for the final 40%.

```dart
final Animation<double> animation = TweenSequence<double>(
  <TweenSequenceItem<double>>[
    TweenSequenceItem<double>(
      tween: Tween<double>(begin: 5.0, end: 10.0)
        .chain(CurveTween(curve: Curves.ease)),
      weight: 40.0,
    ),
    TweenSequenceItem<double>(
      tween: ConstantTween<double>(10.0),
      weight: 20.0,
    ),
    TweenSequenceItem<double>(
      tween: Tween<double>(begin: 10.0, end: 5.0)
        .chain(CurveTween(curve: Curves.ease)),
      weight: 40.0,
    ),
  ],
).animate(myAnimationController);
```

{@end-tool}

### TweenSequence()

```dart
TweenSequence(List<TweenSequenceItem<T>> items)
```

Construct a TweenSequence.

The [items] parameter must be a list of one or more [TweenSequenceItem]s.

There's a small cost associated with building a [TweenSequence] so it's best to reuse one, rather than rebuilding it on every frame, when that's possible.

### transform()

```dart
T transform(double t)
```

### toString()

```dart
String toString()
```

# FlippedTweenSequence

```dart
class FlippedTweenSequence extends TweenSequence<double> {}
```

Enables creating a flipped [Animation] whose value is defined by a sequence of [Tween]s.

This creates a [TweenSequence] that evaluates to a result that flips the tween both horizontally and vertically.

This tween sequence assumes that the evaluated result has to be a double between 0.0 and 1.0.

### FlippedTweenSequence()

```dart
FlippedTweenSequence(List<TweenSequenceItem<double>> items)
```

Creates a flipped [TweenSequence].

The [items] parameter must be a list of one or more [TweenSequenceItem]s.

There's a small cost associated with building a `TweenSequence` so it's best to reuse one, rather than rebuilding it on every frame, when that's possible.

### transform()

```dart
double transform(double t)
```

# TweenSequenceItem

```dart
class TweenSequenceItem<T> {}
```

A simple holder for one element of a [TweenSequence].

### TweenSequenceItem()

```dart
TweenSequenceItem({required Animatable<T> tween, required double weight})
```

Construct a TweenSequenceItem.

The [weight] must be greater than 0.0.

### tween

```dart
Animatable<T> tween
```

Defines the value of the [TweenSequence] for the interval within the animation's duration indicated by [weight] and this item's position in the list of items.

{@tool snippet}

The value of this item can be "curved" by chaining it to a [CurveTween]. For example to create a tween that eases from 0.0 to 10.0:

```dart
Tween<double>(begin: 0.0, end: 10.0)
  .chain(CurveTween(curve: Curves.ease))
```

{@end-tool}

### weight

```dart
double weight
```

An arbitrary value that indicates the relative percentage of a [TweenSequence] animation's duration when [tween] will be used.

The percentage for an individual item is the item's weight divided by the sum of all of the items' weights.
