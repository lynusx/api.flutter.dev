@docImport 'app.dart';

# DefaultTextEditingShortcuts

```dart
class DefaultTextEditingShortcuts extends StatelessWidget {}
```

A widget with the shortcuts used for the default text editing behavior.

This default behavior can be overridden by placing a [Shortcuts] widget lower in the widget tree than this. See the [Action] class for an example of remapping an [Intent] to a custom [Action].

The [Shortcuts] widget usually takes precedence over system keybindings. Proceed with caution if the shortcut you wish to override is also used by the system. For example, overriding [LogicalKeyboardKey.backspace] could cause CJK input methods to discard more text than they should when the backspace key is pressed during text composition on iOS.

{@macro flutter.widgets.editableText.shortcutsAndTextInput}

{@tool snippet}

This example shows how to use an additional [Shortcuts] widget to override some default text editing keyboard shortcuts to have new behavior. Instead of moving the cursor, alt + up/down will change the focused widget.

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

This example shows how to use an additional [Shortcuts] widget to override default text editing shortcuts to have completely custom behavior defined by a custom Intent and Action. Here, the up/down arrow keys increment/decrement a counter instead of moving the cursor.

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

See also:

- [WidgetsApp], which creates a DefaultTextEditingShortcuts.

### DefaultTextEditingShortcuts()

```dart
DefaultTextEditingShortcuts({dynamic key, required Widget child})
```

Creates a [DefaultTextEditingShortcuts] widget that provides the default text editing shortcuts on the current platform.

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

Maps the selector from NSStandardKeyBindingResponding to the Intent if the selector is recognized.
