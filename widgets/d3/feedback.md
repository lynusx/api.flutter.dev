# Feedback

```dart
abstract final class Feedback {}
```

为特定操作提供平台特定的声音和/或触觉反馈。

例如，要在点击按钮时播放 Android 典型的点击音效，请调用 [forTap]。要在长按元素时触发 Android 特定的振动，请调用 [forLongPress]。另外，你也可以将 [GestureDetector.onTap] 或 [GestureDetector.onLongPress] 回调包装在 [wrapForTap] 或 [wrapForLongPress] 中来实现相同的效果（见下方示例代码）。

此类中的所有方法通常在 [StatelessWidget.build] 方法内部或 [State](https://www.yuque.com/thyname/flutter.widgets/state) 的方法中调用，因为你需要提供一个 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)。

{@tool snippet}

在执行实际回调之前触发平台特定的反馈：

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

另外，你也可以在点击或长按处理程序中直接调用 [forTap] 或 [forLongPress]：

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

为点击提供平台特定的反馈。

在 Android 上会播放点击系统音效。在 iOS 上此方法不执行任何操作。

另请参阅：

- [wrapForTap]，用于在执行 [GestureTapCallback](https://www.yuque.com/thyname/flutter.gestures/gesturetapcallback) 之前触发平台特定的反馈。

### wrapForTap()

```dart
GestureTapCallback? wrapForTap(GestureTapCallback? callback, BuildContext context)
```

包装一个 [GestureTapCallback](https://www.yuque.com/thyname/flutter.gestures/gesturetapcallback)，以便在执行所提供的回调之前为点击提供平台特定的反馈。

在 Android 上会播放平台典型的点击系统音效。在 iOS 上此方法不执行任何操作，因为该平台通常不为点击提供反馈。

另请参阅：

- [forTap]，仅触发平台特定的反馈，而不包装 [GestureTapCallback](https://www.yuque.com/thyname/flutter.gestures/gesturetapcallback)。

### forLongPress()

```dart
Future<void> forLongPress(BuildContext context)
```

为长按提供平台特定的反馈。

在 Android 上会触发平台典型的振动。在 iOS 上会触发重度撞击触觉反馈并伴随点击系统音效，这是在运行 iOS 17.5 版本的 iPhone 15 Pro 实机上观察到的默认行为。

另请参阅：

- [wrapForLongPress]，用于在执行 [GestureLongPressCallback](https://www.yuque.com/thyname/flutter.gestures/gesturelongpresscallback) 之前触发平台特定的反馈。

### wrapForLongPress()

```dart
GestureLongPressCallback? wrapForLongPress(GestureLongPressCallback? callback, BuildContext context)
```

包装一个 [GestureLongPressCallback](https://www.yuque.com/thyname/flutter.gestures/gesturelongpresscallback)，以便在执行所提供的回调之前为长按提供平台特定的反馈。

在 Android 上会触发平台典型的振动。在 iOS 上会触发重度撞击触觉反馈并伴随点击系统音效，这是在运行 iOS 17.5 版本的 iPhone 15 Pro 实机上观察到的默认行为。

另请参阅：

- [forLongPress]，仅触发平台特定的反馈，而不包装 [GestureLongPressCallback](https://www.yuque.com/thyname/flutter.gestures/gesturelongpresscallback)。
