# StatusTransitionWidget

```dart
abstract class StatusTransitionWidget extends StatefulWidget {}
```

A widget that rebuilds when the given animation changes status.

### StatusTransitionWidget()

```dart
StatusTransitionWidget({dynamic key, required Animation<double> animation})
```

Initializes fields for subclasses.

### animation

```dart
Animation<double> animation
```

The animation to which this widget is listening.

### build()

```dart
Widget build(BuildContext context)
```

Override this method to build widgets that depend on the current status of the animation.

### createState()

```dart
State<StatusTransitionWidget> createState()
```
