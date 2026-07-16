@docImport 'app.dart';

# DefaultTextEditingShortcuts

```dart
class DefaultTextEditingShortcuts extends StatelessWidget {}
```

一个包含默认文本编辑行为所用快捷键的 Widget。

可以通过在该 Widget 下方的 Widget 树中放置一个 [Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts) Widget 来覆盖此默认行为。有关将 [Intent](https://www.yuque.com/thyname/flutter.widgets/intent) 重新映射为自定义 [Action](https://www.yuque.com/thyname/flutter.widgets/action) 的示例，请参阅 [Action](https://www.yuque.com/thyname/flutter.widgets/action) 类。

[Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts) Widget 通常优先于系统按键绑定。如果你要覆盖的快捷键也被系统使用，请谨慎操作。例如，覆盖 [LogicalKeyboardKey.backspace] 可能导致在 iOS 上进行文本组合（text composition）期间按下退格键时，CJK 输入法丢弃的文本比预期的更多。

{@macro flutter.widgets.editableText.shortcutsAndTextInput}

{@tool snippet}

此示例展示了如何使用额外的 [Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts) Widget 来覆盖部分默认文本编辑键盘快捷键，以实现新的行为。按下 alt + 上/下箭头键将切换焦点所在的 Widget，而不是移动光标。

```dart
@override
Widget build(BuildContext context) {
  // If using WidgetsApp or its descendants MaterialApp or CupertinoApp,
  // then DefaultTextEditingShortcuts is already being inserted into the
  // widget tree.
  return const DefaultTextEditingShortcuts(
    child: Center(
      child: Shortcuts(
        shortcuts: <ShortcutActivator, Intent>{
          SingleActivator(LogicalKeyboardKey.arrowDown, alt: true): NextFocusIntent(),
          SingleActivator(LogicalKeyboardKey.arrowUp, alt: true): PreviousFocusIntent(),
        },
        child: Column(
          children: <Widget>[
            TextField(
              decoration: InputDecoration(
                hintText: 'alt + down moves to the next field.',
              ),
            ),
            TextField(
              decoration: InputDecoration(
                hintText: 'And alt + up moves to the previous.',
              ),
            ),
          ],
        ),
      ),
    ),
  );
}
```

{@end-tool}

{@tool snippet}

此示例展示了如何使用额外的 [Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts) Widget 来覆盖默认文本编辑快捷键，以实现由自定义 Intent 和 Action 定义的完全自定义行为。这里，上/下箭头键用于递增/递减一个计数器，而不是移动光标。

```dart
class IncrementCounterIntent extends Intent {}
class DecrementCounterIntent extends Intent {}

class MyWidget extends StatefulWidget {
  const MyWidget({ super.key });

  @override
  MyWidgetState createState() => MyWidgetState();
}

class MyWidgetState extends State<MyWidget> {

  int _counter = 0;

  @override
  Widget build(BuildContext context) {
    // If using WidgetsApp or its descendants MaterialApp or CupertinoApp,
    // then DefaultTextEditingShortcuts is already being inserted into the
    // widget tree.
    return DefaultTextEditingShortcuts(
      child: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            const Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.headlineMedium,
            ),
            Shortcuts(
              shortcuts: <ShortcutActivator, Intent>{
                const SingleActivator(LogicalKeyboardKey.arrowUp): IncrementCounterIntent(),
                const SingleActivator(LogicalKeyboardKey.arrowDown): DecrementCounterIntent(),
              },
              child: Actions(
                actions: <Type, Action<Intent>>{
                  IncrementCounterIntent: CallbackAction<IncrementCounterIntent>(
                    onInvoke: (IncrementCounterIntent intent) {
                      setState(() {
                        _counter++;
                      });
                      return null;
                    },
                  ),
                  DecrementCounterIntent: CallbackAction<DecrementCounterIntent>(
                    onInvoke: (DecrementCounterIntent intent) {
                      setState(() {
                        _counter--;
                      });
                      return null;
                    },
                  ),
                },
                child: const TextField(
                  maxLines: 2,
                  decoration: InputDecoration(
                    hintText: 'Up/down increment/decrement here.',
                  ),
                ),
              ),
            ),
            const TextField(
              maxLines: 2,
              decoration: InputDecoration(
                hintText: 'Up/down behave normally here.',
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

{@end-tool}

另请参阅：

- [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp)，它会创建一个 DefaultTextEditingShortcuts。

### DefaultTextEditingShortcuts()

```dart
DefaultTextEditingShortcuts({dynamic key, required Widget child})
```

创建一个 [DefaultTextEditingShortcuts](https://www.yuque.com/thyname/flutter.widgets/defaulttexteditingshortcuts) Widget，为当前平台提供默认的文本编辑快捷键。

### child

```dart
Widget child
```

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

# intentForMacOSSelector()

```dart
Intent? intentForMacOSSelector(String selectorName)
```

如果该选择器（selector）是可识别的，则将来自 NSStandardKeyBindingResponding 的选择器映射到对应的 Intent。
