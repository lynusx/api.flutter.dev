# SemanticsDebugger

```dart
class SemanticsDebugger extends StatefulWidget {}
```

A widget that visualizes the semantics for the child.

This widget is useful for understand how an app presents itself to accessibility technology.

### SemanticsDebugger()

```dart
SemanticsDebugger({dynamic key, required Widget child, TextStyle labelStyle = const TextStyle(color: Color(0xFF000000), fontSize: 10.0, height: 0.8)})
```

Creates a widget that visualizes the semantics for the child.

[labelStyle] dictates the [TextStyle] used for the semantics labels.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### labelStyle

```dart
TextStyle labelStyle
```

The [TextStyle] to use when rendering semantics labels.

### createState()

```dart
State<SemanticsDebugger> createState()
```
