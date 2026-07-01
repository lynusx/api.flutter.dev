@docImport 'form.dart';

# WillPopScope

```dart
class WillPopScope extends StatefulWidget {}
```

Registers a callback to veto attempts by the user to dismiss the enclosing [ModalRoute].

See also:

- [ModalRoute.addScopedWillPopCallback] and [ModalRoute.removeScopedWillPopCallback], which this widget uses to register and unregister [onWillPop].
- [Form], which provides an `onWillPop` callback that enables the form to veto a `pop` initiated by the app's back button.

### WillPopScope()

```dart
WillPopScope({dynamic key, required Widget child, required WillPopCallback? onWillPop})
```

Creates a widget that registers a callback to veto attempts by the user to dismiss the enclosing [ModalRoute].

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### onWillPop

```dart
WillPopCallback? onWillPop
```

Called to veto attempts by the user to dismiss the enclosing [ModalRoute].

If the callback returns a Future that resolves to false, the enclosing route will not be popped.

### createState()

```dart
State<WillPopScope> createState()
```
