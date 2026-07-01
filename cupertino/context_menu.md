@docImport 'context_menu_action.dart';

# CupertinoContextMenuBuilder

```dart
typedef CupertinoContextMenuBuilder = Widget Function(BuildContext context, Animation<double> animation)
```

A function that builds the child and handles the transition between the default child and the preview when the CupertinoContextMenu is open.

# CupertinoContextMenu

```dart
class CupertinoContextMenu extends StatefulWidget {}
```

A full-screen modal route that opens when the [child] is long-pressed.

When open, the [CupertinoContextMenu] shows the child in a large full-screen [Overlay] with a list of buttons specified by [actions]. The child/preview is placed in an [Expanded] widget so that it will grow to fill the Overlay if its size is unconstrained.

When closed, the [CupertinoContextMenu] displays the child as if the [CupertinoContextMenu] were not there. Sizing and positioning is unaffected. The menu can be closed like other [PopupRoute]s, such as by tapping the background or by calling `Navigator.pop(context)`. Unlike [PopupRoute], it can also be closed by swiping downwards.

{@tool dartpad} This sample shows a very simple [CupertinoContextMenu] for the Flutter logo. Long press on it to open.

** See code in examples/api/lib/cupertino/context_menu/cupertino_context_menu.0.dart ** {@end-tool}

{@tool dartpad} This sample shows a similar CupertinoContextMenu, this time using [builder] to add a border radius to the widget.

** See code in examples/api/lib/cupertino/context_menu/cupertino_context_menu.1.dart ** {@end-tool}

See also:

- <https://developer.apple.com/design/human-interface-guidelines/ios/controls/context-menus/>

### CupertinoContextMenu()

```dart
CupertinoContextMenu({dynamic key, required List<Widget> actions, required Widget? child, bool enableHapticFeedback = false})
```

Create a context menu.

The [actions] parameter cannot be empty.

### CupertinoContextMenu.builder()

```dart
CupertinoContextMenu.builder({dynamic key, required List<Widget> actions, required CupertinoContextMenuBuilder builder, bool enableHapticFeedback = false})
```

Creates a context menu with a custom [builder] controlling the widget.

Use instead of the default constructor when it is needed to have a more custom animation.

The [actions] parameter cannot be empty.

### kOpenBorderRadius

```dart
double kOpenBorderRadius
```

Exposes the default border radius for matching iOS 16.0 behavior. This value was eyeballed from the iOS simulator running iOS 16.0.

{@tool snippet}

Below is example code in order to match the default border radius for an iOS 16.0 open preview.

```dart
CupertinoContextMenu.builder(
  actions: <Widget>[
    CupertinoContextMenuAction(
      child: const Text('Action one'),
      onPressed: () {},
    ),
  ],
  builder:(BuildContext context, Animation<double> animation) {
    final Animation<BorderRadius?> borderRadiusAnimation = BorderRadiusTween(
      begin: BorderRadius.zero,
      end: BorderRadius.circular(CupertinoContextMenu.kOpenBorderRadius),
    ).animate(
      CurvedAnimation(
        parent: animation,
        curve: Interval(
          CupertinoContextMenu.animationOpensAt,
          1.0,
        ),
      ),
    );

    final Animation<Decoration> boxDecorationAnimation = DecorationTween(
      begin: const BoxDecoration(
       boxShadow: <BoxShadow>[],
      ),
      end: const BoxDecoration(
       boxShadow: CupertinoContextMenu.kEndBoxShadow,
      ),
     ).animate(
       CurvedAnimation(
        parent: animation,
        curve: Interval(
          0.0,
          CupertinoContextMenu.animationOpensAt,
        ),
      )
    );

    return Container(
      decoration:
        animation.value < CupertinoContextMenu.animationOpensAt ? boxDecorationAnimation.value : null,
      child: FittedBox(
        fit: BoxFit.cover,
        child: ClipRSuperellipse(
          borderRadius: borderRadiusAnimation.value ?? BorderRadius.zero,
          child: SizedBox(
            height: 150,
            width: 150,
            child: Image.network('https://flutter.github.io/assets-for-api-docs/assets/widgets/owl-2.jpg'),
          ),
        ),
      )
    );
  },
)
```

{@end-tool}

### kEndBoxShadow

```dart
List<BoxShadow> kEndBoxShadow
```

Exposes the final box shadow of the opening animation of the child widget to match the default behavior of the native iOS widget. This value was eyeballed from the iOS simulator running iOS 16.0.

### animationOpensAt

```dart
double animationOpensAt
```

The point at which the CupertinoContextMenu begins to animate into the open position.

A value between 0.0 and 1.0 corresponding to a point in [builder]'s animation. When passing in an animation to [builder] the range before [animationOpensAt] will correspond to the animation when the widget is pressed and held, and the range after is the animation as the menu is fully opening. For an example, see the documentation for [builder].

### kBackgroundColor

```dart
Color kBackgroundColor
```

The background color of a [CupertinoContextMenuAction] and a [CupertinoContextMenu] sheet.

### builder

```dart
CupertinoContextMenuBuilder builder
```

A function that returns a widget to be used alternatively from [child].

The widget returned by the function will be shown at all times: when the [CupertinoContextMenu] is closed, when it is in the middle of opening, and when it is fully open. This will overwrite the default animation that matches the behavior of an iOS 16.0 context menu.

This builder can be used instead of the child when the intended child has a property that would conflict with the default animation, such as a border radius or a shadow, or if a more custom animation is needed.

In addition to the current [BuildContext], the function is also called with an [Animation]. The complete animation goes from 0 to 1 when the CupertinoContextMenu opens, and from 1 to 0 when it closes, and it can be used to animate the widget in sync with this opening and closing.

The animation works in two stages. The first happens on press and hold of the widget from 0 to [animationOpensAt], and the second stage for when the widget fully opens up to the menu, from [animationOpensAt] to 1.

{@tool snippet}

Below is an example of using [builder] to show an image tile setup to be opened in the default way to match a native iOS 16.0 app. The behavior will match what will happen if the simple child image was passed as just the [child] parameter, instead of [builder]. This can be manipulated to add more customizability to the widget's animation.

```dart
CupertinoContextMenu.builder(
  actions: <Widget>[
    CupertinoContextMenuAction(
      child: const Text('Action one'),
      onPressed: () {},
    ),
  ],
  builder:(BuildContext context, Animation<double> animation) {
    final Animation<BorderRadius?> borderRadiusAnimation = BorderRadiusTween(
      begin: BorderRadius.zero,
      end: BorderRadius.circular(CupertinoContextMenu.kOpenBorderRadius),
    ).animate(
      CurvedAnimation(
        parent: animation,
        curve: Interval(
          CupertinoContextMenu.animationOpensAt,
          1.0,
        ),
      ),
     );

    final Animation<Decoration> boxDecorationAnimation = DecorationTween(
      begin: const BoxDecoration(
       boxShadow: <BoxShadow>[],
      ),
      end: const BoxDecoration(
       boxShadow: CupertinoContextMenu.kEndBoxShadow,
      ),
     ).animate(
       CurvedAnimation(
        parent: animation,
        curve: Interval(
          0.0,
          CupertinoContextMenu.animationOpensAt,
        ),
      ),
    );

    return Container(
      decoration:
        animation.value < CupertinoContextMenu.animationOpensAt ? boxDecorationAnimation.value : null,
      child: FittedBox(
        fit: BoxFit.cover,
        child: ClipRSuperellipse(
          borderRadius: borderRadiusAnimation.value ?? BorderRadius.zero,
          child: SizedBox(
            height: 150,
            width: 150,
            child: Image.network('https://flutter.github.io/assets-for-api-docs/assets/widgets/owl-2.jpg'),
          ),
        ),
      ),
    );
  },
)
```

{@end-tool}

{@tool dartpad} Additionally below is an example of a real world use case for [builder].

If a widget is passed to the [child] parameter with properties that conflict with the default animation, in this case the border radius, unwanted behaviors can arise. Here a boxed shadow will wrap the widget as it is expanded. To handle this, a more custom animation and widget can be passed to the builder, using values exposed by [CupertinoContextMenu], like [CupertinoContextMenu.kEndBoxShadow], to match the native iOS animation as close as desired.

** See code in examples/api/lib/cupertino/context_menu/cupertino_context_menu.1.dart ** {@end-tool}

### child

```dart
Widget? child
```

The widget that can be "opened" with the [CupertinoContextMenu].

When the [CupertinoContextMenu] is long-pressed, the menu will open and this widget will be moved to the new route and placed inside of an [Expanded] widget. This allows the child to resize to fit in its place in the new route, if it doesn't size itself.

When the [CupertinoContextMenu] is "closed", this widget acts like a [Container], i.e. it does not constrain its child's size or affect its position.

### actions

```dart
List<Widget> actions
```

The actions that are shown in the menu.

These actions are typically [CupertinoContextMenuAction]s.

This parameter must not be empty.

### enableHapticFeedback

```dart
bool enableHapticFeedback
```

If true, clicking on the [CupertinoContextMenuAction]s will produce haptic feedback.

Uses [HapticFeedback.heavyImpact] when activated. Defaults to false.

### createState()

```dart
State<CupertinoContextMenu> createState()
```
