# HtmlElementViewImpl

```dart
extension HtmlElementViewImpl on HtmlElementView {}
```

The platform-specific implementation of [HtmlElementView].

### createFromTagName()

```dart
HtmlElementView createFromTagName({Key? key, required String tagName, bool isVisible = true, ElementCreatedCallback? onElementCreated, required PlatformViewHitTestBehavior hitTestBehavior})
```

Creates an [HtmlElementView] that renders a DOM element with the given [tagName].

### buildImpl()

```dart
Widget buildImpl(BuildContext context)
```

Called from [HtmlElementView.build] to build the widget tree.

This is not expected to be invoked in non-web environments. It throws if that happens.

The implementation on Flutter Web builds a platform view and handles its lifecycle.
