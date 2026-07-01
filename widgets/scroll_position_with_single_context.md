@docImport 'page_storage.dart'; @docImport 'scroll_controller.dart'; @docImport 'scroll_view.dart'; @docImport 'scrollable.dart'; @docImport 'viewport.dart';

# ScrollPositionWithSingleContext

```dart
class ScrollPositionWithSingleContext extends ScrollPosition implements ScrollActivityDelegate {}
```

A scroll position that manages scroll activities for a single [ScrollContext].

This class is a concrete subclass of [ScrollPosition] logic that handles a single [ScrollContext], such as a [Scrollable]. An instance of this class manages [ScrollActivity] instances, which change what content is visible in the [Scrollable]'s [Viewport].

{@macro flutter.widgets.scrollPosition.listening}

See also:

- [ScrollPosition], which defines the underlying model for a position within a [Scrollable] but is agnostic as to how that position is changed.
- [ScrollView] and its subclasses such as [ListView], which use [ScrollPositionWithSingleContext] to manage their scroll position.
- [ScrollController], which can manipulate one or more [ScrollPosition]s, and which uses [ScrollPositionWithSingleContext] as its default class for scroll positions.

### ScrollPositionWithSingleContext()

```dart
ScrollPositionWithSingleContext({required ScrollPhysics physics, required ScrollContext context, double? initialPixels = 0.0, bool keepScrollOffset, ScrollPosition? oldPosition, String? debugLabel})
```

Create a [ScrollPosition] object that manages its behavior using [ScrollActivity] objects.

The `initialPixels` argument can be null, but in that case it is imperative that the value be set, using [correctPixels], as soon as [applyNewDimensions] is invoked, before calling the inherited implementation of that method.

If [keepScrollOffset] is true (the default), the current scroll offset is saved with [PageStorage] and restored it if this scroll position's scrollable is recreated.

### axisDirection

```dart
AxisDirection get axisDirection
```

### setPixels()

```dart
double setPixels(double newPixels)
```

### absorb()

```dart
void absorb(ScrollPosition other)
```

### applyNewDimensions()

```dart
void applyNewDimensions()
```

### beginActivity()

```dart
void beginActivity(ScrollActivity? newActivity)
```

### applyUserOffset()

```dart
void applyUserOffset(double delta)
```

### goIdle()

```dart
void goIdle()
```

### goBallistic()

```dart
void goBallistic(double velocity)
```

Start a physics-driven simulation that settles the [pixels] position, starting at a particular velocity.

This method defers to [ScrollPhysics.createBallisticSimulation], which typically provides a bounce simulation when the current position is out of bounds and a friction simulation when the position is in bounds but has a non-zero velocity.

The velocity should be in logical pixels per second.

### userScrollDirection

```dart
ScrollDirection get userScrollDirection
```

### updateUserScrollDirection()

```dart
void updateUserScrollDirection(ScrollDirection value)
```

Set [userScrollDirection] to the given value.

If this changes the value, then a [UserScrollNotification] is dispatched.

### animateTo()

```dart
Future<void> animateTo(double to, {required Duration duration, required Curve curve})
```

### jumpTo()

```dart
void jumpTo(double value)
```

### pointerScroll()

```dart
void pointerScroll(double delta)
```

### jumpToWithoutSettling()

```dart
void jumpToWithoutSettling(double value)
```

### hold()

```dart
ScrollHoldController hold(VoidCallback holdCancelCallback)
```

### drag()

```dart
Drag drag(DragStartDetails details, VoidCallback dragCancelCallback)
```

### dispose()

```dart
void dispose()
```

### debugFillDescription()

```dart
void debugFillDescription(List<String> description)
```
