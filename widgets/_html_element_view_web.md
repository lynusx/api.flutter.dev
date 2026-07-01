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

The implementation of [HtmlElementView.build].

This is not expected to be invoked in non-web environments. It throws if that happens.

The implementation on Flutter Web builds an HTML platform view and handles its lifecycle.

Creates the controller and kicks off its initialization.
