@docImport 'package:flutter/widgets.dart';

# ContentSensitivity

```dart
enum ContentSensitivity {}
```

The possible values for a widget tree's content sensitivity.

{@template flutter.services.ContentSensitivity} There are three [ContentSensitivity] levels, and these can be set via the `SensitiveContent` widget.

[ContentSensitivity.sensitive] is the highest prioritized setting, and if it is set, it will cause the tree to remain marked sensitive even if there are other `SensitiveContent` widgets in the tree.

[ContentSensitivity.autoSensitive] is the second most prioritized setting, and it will cause the tree to remain marked auto-sensitive if there are no sensitive `SensitiveContent` widgets elsewhere in the tree.

[ContentSensitivity.notSensitive] is the least prioritized setting, and it will cause the tree to remain marked auto-sensitive if there are no sensitive `SensitiveContent` widgets elsewhere in the tree. If there are no `SensitiveContent` widgets in the tree, the default setting as queried from the embedding will be used. This could be set by a Flutter developer in native Android; otherwise, Android uses [ContentSensitivity.autoSensitive] by default; see https://developer.android.com/reference/android/view/View#getContentSensitivity(). {@endtemplate}

- See `SensitiveContent` for how to set a [ContentSensitivity] level in order for sensitive content to be obscured when the Flutter screen is shared.

Content sensitivity is auto-detected by the native platform.

When this level is set via a `SensitiveContent` widget, the window hosting the screen will only be marked as sensitive if other `SensitiveContent` widgets in the Flutter app with the [sensitive] level are present in the widget tree.

See https://developer.android.com/reference/android/view/View#CONTENT_SENSITIVITY_AUTO for how this mode behaves on native Android.

For Android `View`s, this mode attempts to auto detect passwords, 2factor tokens, and other sensitive content. As of API 35, Android cannot determine if Flutter `View`s contain sensitive content automatically, and thus will never obscure the screen.

The widget tree contains sensitive content.

When this level is set via a `SensitiveContent` widget, the window hosting the screen will be marked as sensitive during an active media projection session.

See https://developer.android.com/reference/android/view/View#CONTENT_SENSITIVITY_SENSITIVE.

The widget tree does not contain sensitive content.

When this level is set via a `SensitiveContent` widget, the window hosting the screen will only be marked as sensitive if other `SensitiveContent` widgets in the Flutter app with the [sensitive] level are present in the widget tree.

See https://developer.android.com/reference/android/view/View#CONTENT_SENSITIVITY_NOT_SENSITIVE.

The sensitivity content level is unknown to Flutter.

This mode may represent the current content sensitivity of the window if, for example, Android adds a new mode that is not recognized by the `SensitiveContent` widget.

This mode cannot be used to set the sensitivity level of a `SensitiveContent` widget.

# SensitiveContentService

```dart
class SensitiveContentService {}
```

Service for setting the content sensitivity of the native app window (Android `View`) that contains the app's widget tree.

This service is only currently supported on Android API 35+.

### SensitiveContentService()

```dart
SensitiveContentService()
```

Creates service to set content sensitivity of an app window (Android `View`) via communication over the sensitive content [MethodChannel].

### sensitiveContentChannel

```dart
MethodChannel sensitiveContentChannel
```

The channel used to communicate with the shell side to get and set the content sensitivity of an app window (Android `View`).

### setContentSensitivity()

```dart
Future<void> setContentSensitivity(ContentSensitivity contentSensitivity)
```

Sets content sensitivity level of the app window (Android `View`) that contains the app's widget tree to the level specified by [contentSensitivity] via a call to the native embedder.

### getContentSensitivity()

```dart
Future<ContentSensitivity> getContentSensitivity()
```

Gets content sensitivity level of the app window (Android `View`) that contains the app's widget tree.

### isSupported()

```dart
Future<bool> isSupported()
```

Returns whether or not setting content sensitivity levels is supported by the device.

This method must be called before attempting to call [getContentSensitivity] or [setContentSensitivity].

This feature is only supported on Android 35+ currently. Its return value will not change and thus, is safe to cache.
