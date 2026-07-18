@docImport 'editable_text.dart';

# KeyboardListener

```dart
class KeyboardListener extends StatelessWidget {}
```

一个组件，每当用户按下或释放键盘上的按键时都会调用一个回调。

[KeyboardListener](https://www.yuque.com/thyname/flutter.widgets/keyboardlistener) 适用于监听按键事件以及以按键形式表示的硬件按钮，通常由游戏及其他将键盘用于文本输入之外用途的应用程序使用。

对于文本输入场景，请考虑使用 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext)，它可以与屏幕软键盘以及输入法编辑器（IME）集成。

另请参阅：

- [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext)：在文本输入场景中应使用它而非此组件。

### KeyboardListener()

```dart
KeyboardListener({dynamic key, required FocusNode focusNode, bool autofocus = false, bool includeSemantics = true, ValueChanged<KeyEvent>? onKeyEvent, required Widget child})
```

创建一个接收键盘事件的组件。

对于文本输入场景，请考虑使用 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext)，它可以与屏幕软键盘以及输入法编辑器（IME）集成。

`key` 是 Widget 的标识符，与键盘无关。请参阅 [Widget.key]。

### focusNode

```dart
FocusNode focusNode
```

控制此 Widget 是否拥有键盘焦点。

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.Focus.autofocus}

### includeSemantics

```dart
bool includeSemantics
```

{@macro flutter.widgets.Focus.includeSemantics}

### onKeyEvent

```dart
ValueChanged<KeyEvent>? onKeyEvent
```

每当此 Widget 接收到键盘事件时调用。

### child

```dart
Widget child
```

此 Widget 下方的子 Widget。

{@macro flutter.widgets.ProxyWidget.child}
