# SensitiveContentHost

```dart
class SensitiveContentHost {}
```

Host of the current content sensitivity for the widget tree that contains some number [SensitiveContent] widgets.

This is not ready for production.

### instance

```dart
SensitiveContentHost instance
```

[SensitiveContentHost] instance for the widget tree.

### calculatedContentSensitivity

```dart
ContentSensitivity? get calculatedContentSensitivity
```

Returns the current content sensitivity as tracked by [_contentSensitivitySetting].

### register()

```dart
Future<void> register(ContentSensitivity desiredSensitivity)
```

Registers a [SensitiveContent] widget that will help determine the [ContentSensitivity] for the widget tree.

### unregister()

```dart
Future<void> unregister(ContentSensitivity widgetSensitivity)
```

Unregisters a [SensitiveContent] widget from the [_ContentSensitivitySetting] tracking the content sensitivity of the widget tree.

# SensitiveContent

```dart
class SensitiveContent extends StatefulWidget {}
```

Widget to set the [ContentSensitivity] of content in the widget tree.

The [sensitivity] of the widget in conjunction with the other [SensitiveContent] widgets in the tree will determine whether or not the screen will be obscured during media projection, e.g. screen sharing.

{@macro flutter.services.ContentSensitivity}

Currently, this widget is only supported on Android API 35+. On all lower Android versions and non-Android platforms, this does nothing; the screen will never be obscured regardless of the [sensitivity] set. To programmatically check if a device supports this widget, call [SensitiveContentService.isSupported].

{@tool dartpad} This example shows how to wrap account details in a [SensitiveContent] widget and change the [ContentSensitivity] used for the current screen during screen sharing.

** See code in examples/api/lib/widgets/sensitive_content/sensitive_content.0.dart ** {@end-tool}

It is possible for a frame to be projected before the screen is updated to match the widget's `sensitivityLevel`, potentially revealing sensitive information during that frame. For example, when navigating from a page with no `SensitiveContent` to a new page in an app using a `Navigator.of(context).pushReplacement` to push a new `PageRouteBuilder` with (1) a `pageBuilder` that includes a [SensitiveContent] widget with `sensitivity` [ContentSensitivity.sensitive] and (2) `transitionDuration: Duration.zero`, one frame showing the app content is projected before the screen is obscured. See https://github.com/flutter/flutter/issues/164820 for for a discussion on known vulnerabilities or to report encountered vulnerabilities.

{@youtube 560 315 https://www.youtube.com/watch?v=WnzHARTIZww}

See also:

- [ContentSensitivity], which are the different content sensitivity that a [SensitiveContent] widget can set.

### SensitiveContent()

```dart
SensitiveContent({dynamic key, required ContentSensitivity sensitivity, required Widget child})
```

Creates a [SensitiveContent] widget.

### sensitivity

```dart
ContentSensitivity sensitivity
```

The sensitivity that the [SensitiveContent] widget should sets for the Android native `View` hosting the widget tree.

### child

```dart
Widget child
```

The child widget of this [SensitiveContent].

If the [sensitivity] is set to [ContentSensitivity.sensitive], then the entire screen will be obscured when the screen is projected irrespective to the parent/child widgets.

{@macro flutter.widgets.ProxyWidget.child}

### createState()

```dart
State<SensitiveContent> createState()
```
