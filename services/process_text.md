# ProcessTextAction

```dart
class ProcessTextAction {}
```

A data structure describing text processing actions.

### ProcessTextAction()

```dart
ProcessTextAction(String id, String label)
```

Creates text processing actions based on those returned by the engine.

### id

```dart
String id
```

The action unique id.

### label

```dart
String label
```

The action localized label.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# ProcessTextService

```dart
abstract class ProcessTextService {}
```

Determines how to interact with the text processing feature.

### queryTextActions()

```dart
Future<List<ProcessTextAction>> queryTextActions()
```

Returns a [Future] that resolves to a [List] of [ProcessTextAction]s containing all text processing actions available.

If there are no actions available, an empty list will be returned.

### processTextAction()

```dart
Future<String?> processTextAction(String id, String text, bool readOnly)
```

Returns a [Future] that resolves to a [String] when the text action returns a transformed text or null when the text action did not return a transformed text.

The `id` parameter is the text action unique identifier returned by [queryTextActions].

The `text` parameter is the text to be processed.

The `readOnly` parameter indicates that the transformed text, if it exists, will be used as read-only.

# DefaultProcessTextService

```dart
class DefaultProcessTextService implements ProcessTextService {}
```

The service used by default for the text processing feature.

Any widget may use this service to get a list of text processing actions and send requests to activate these text actions.

This is currently only supported on Android and it requires adding the following '<queries>' element to the Android manifest file:

<manifest ...> <application ...> ... </application> <!-- Required to query activities that can process text, see: https://developer.android.com/training/package-visibility and https://developer.android.com/reference/android/content/Intent#ACTION_PROCESS_TEXT.

In particular, this is used by the Flutter engine in io.flutter.plugin.text.ProcessTextPlugin. --> <queries> <intent> <action android:name="android.intent.action.PROCESS_TEXT"/> <data android:mimeType="text/plain"/> </intent> </queries> </manifest>

The '<queries>' element is part of the Android manifest file generated when running the 'flutter create' command.

If the '<queries>' element is not found, `queryTextActions()` will return an empty list of `ProcessTextAction`.

See also:

- [ProcessTextService], the service that this implements.

### DefaultProcessTextService()

```dart
DefaultProcessTextService()
```

Creates the default service to interact with the platform text processing feature via communication over the text processing [MethodChannel].

### setChannel()

```dart
void setChannel(MethodChannel newChannel)
```

Set the [MethodChannel] used to communicate with the engine text processing feature.

This is only meant for testing within the Flutter SDK.

### queryTextActions()

```dart
Future<List<ProcessTextAction>> queryTextActions()
```

### processTextAction()

```dart
Future<String?> processTextAction(String id, String text, bool readOnly)
```

On Android, the readOnly parameter might be used by the targeted activity, see: https://developer.android.com/reference/android/content/Intent#EXTRA_PROCESS_TEXT_READONLY.
