@docImport 'text_input.dart';

# LiveText

```dart
abstract final class LiveText {}
```

Utility methods for interacting with the system's Live Text.

For example, the Live Text input feature of iOS turns the keyboard into a camera view for directly inserting text obtained through OCR into the active field.

See also:

- <https://developer.apple.com/documentation/uikit/uiresponder/3778577-capturetextfromcamera>
- <https://support.apple.com/guide/iphone/use-live-text-iphcf0b71b0e/ios>

### isLiveTextInputAvailable()

```dart
Future<bool> isLiveTextInputAvailable()
```

Returns true if the Live Text input feature is available on the current device.

### startLiveTextInput()

```dart
Future<void> startLiveTextInput()
```

Start Live Text input.

If any [TextInputConnection] is currently active, calling this method will tell the text field to start Live Text input. If the current device doesn't support Live Text input, nothing will happen.
