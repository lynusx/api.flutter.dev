# Feedback

```dart
abstract final class Feedback {}
```

Provides platform-specific acoustic and/or haptic feedback for certain actions.

For example, to play the Android-typically click sound when a button is tapped, call [forTap]. For the Android-specific vibration when long pressing an element, call [forLongPress]. Alternatively, you can also wrap your [GestureDetector.onTap] or [GestureDetector.onLongPress] callback in [wrapForTap] or [wrapForLongPress] to achieve the same (see example code below).

All methods in this class are usually called from within a [StatelessWidget.build] method or from a [State]'s methods as you have to provide a [BuildContext].

{@tool snippet}

To trigger platform-specific feedback before executing the actual callback:

```dart
class WidgetWithWrappedHandler extends StatelessWidget {
  const WidgetWithWrappedHandler({super.key});

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: Feedback.wrapForTap(_onTapHandler, context),
      onLongPress: Feedback.wrapForLongPress(_onLongPressHandler, context),
      child: const Text('X'),
    );
  }

  void _onTapHandler() {
    // Respond to tap.
  }

  void _onLongPressHandler() {
    // Respond to long press.
  }
}
```

{@end-tool} {@tool snippet}

Alternatively, you can also call [forTap] or [forLongPress] directly within your tap or long press handler:

```dart
class WidgetWithExplicitCall extends StatelessWidget {
  const WidgetWithExplicitCall({super.key});

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () {
        // Do some work (e.g. check if the tap is valid)
        Feedback.forTap(context);
        // Do more work (e.g. respond to the tap)
      },
      onLongPress: () {
        // Do some work (e.g. check if the long press is valid)
        Feedback.forLongPress(context);
        // Do more work (e.g. respond to the long press)
      },
      child: const Text('X'),
    );
  }
}
```

{@end-tool}

### forTap()

```dart
Future<void> forTap(BuildContext context)
```

Provides platform-specific feedback for a tap.

On Android the click system sound is played. On iOS this is a no-op.

See also:

- [wrapForTap] to trigger platform-specific feedback before executing a [GestureTapCallback].

### wrapForTap()

```dart
GestureTapCallback? wrapForTap(GestureTapCallback? callback, BuildContext context)
```

Wraps a [GestureTapCallback] to provide platform specific feedback for a tap before the provided callback is executed.

On Android the platform-typical click system sound is played. On iOS this is a no-op as that platform usually doesn't provide feedback for a tap.

See also:

- [forTap] to just trigger the platform-specific feedback without wrapping a [GestureTapCallback].

### forLongPress()

```dart
Future<void> forLongPress(BuildContext context)
```

Provides platform-specific feedback for a long press.

On Android the platform-typical vibration is triggered. On iOS a heavy-impact haptic feedback is triggered alongside the click system sound, which was observed to be the default behavior on a physical iPhone 15 Pro running iOS version 17.5.

See also:

- [wrapForLongPress] to trigger platform-specific feedback before executing a [GestureLongPressCallback].

### wrapForLongPress()

```dart
GestureLongPressCallback? wrapForLongPress(GestureLongPressCallback? callback, BuildContext context)
```

Wraps a [GestureLongPressCallback] to provide platform specific feedback for a long press before the provided callback is executed.

On Android the platform-typical vibration is triggered. On iOS a heavy-impact haptic feedback is triggered alongside the click system sound, which was observed to be the default behavior on a physical iPhone 15 Pro running iOS version 17.5.

See also:

- [forLongPress] to just trigger the platform-specific feedback without wrapping a [GestureLongPressCallback].
