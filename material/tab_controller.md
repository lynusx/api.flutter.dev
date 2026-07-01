@docImport 'app_bar.dart'; @docImport 'scaffold.dart'; @docImport 'tabs.dart';

# TabController

```dart
class TabController extends ChangeNotifier {}
```

Coordinates tab selection between a [TabBar] and a [TabBarView].

The [index] property is the index of the selected tab and the [animation] represents the current scroll positions of the tab bar and the tab bar view. The selected tab's index can be changed with [animateTo].

A stateful widget that builds a [TabBar] or a [TabBarView] can create a [TabController] and share it directly.

When the [TabBar] and [TabBarView] don't have a convenient stateful ancestor, a [TabController] can be shared by providing a [DefaultTabController] inherited widget.

{@animation 700 540 https://flutter.github.io/assets-for-api-docs/assets/material/tabs.mp4}

{@tool snippet}

This widget introduces a [Scaffold] with an [AppBar] and a [TabBar].

```dart
class MyTabbedPage extends StatefulWidget {
  const MyTabbedPage({ super.key });
  @override
  State<MyTabbedPage> createState() => _MyTabbedPageState();
}

class _MyTabbedPageState extends State<MyTabbedPage> with SingleTickerProviderStateMixin {
  static const List<Tab> myTabs = <Tab>[
    Tab(text: 'LEFT'),
    Tab(text: 'RIGHT'),
  ];

  late TabController _tabController;

  @override
  void initState() {
    super.initState();
    _tabController = TabController(vsync: this, length: myTabs.length);
  }

 @override
 void dispose() {
   _tabController.dispose();
   super.dispose();
 }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        bottom: TabBar(
          controller: _tabController,
          tabs: myTabs,
        ),
      ),
      body: TabBarView(
        controller: _tabController,
        children: myTabs.map((Tab tab) {
          final String label = tab.text!.toLowerCase();
          return Center(
            child: Text(
              'This is the $label tab',
              style: const TextStyle(fontSize: 36),
            ),
          );
        }).toList(),
      ),
    );
  }
}
```

{@end-tool}

{@tool dartpad} This example shows how to listen to page updates in [TabBar] and [TabBarView] when using [DefaultTabController].

** See code in examples/api/lib/material/tab_controller/tab_controller.1.dart ** {@end-tool}

### TabController()

```dart
TabController({int initialIndex = 0, Duration? animationDuration, required int length, required TickerProvider vsync})
```

Creates an object that manages the state required by [TabBar] and a [TabBarView].

The [length] must not be negative. Typically it's a value greater than one, i.e. typically there are two or more tabs. The [length] must match [TabBar.tabs]'s and [TabBarView.children]'s length.

The `initialIndex` must be valid given [length]. If [length] is zero, then `initialIndex` must be 0 (the default).

### animation

```dart
Animation<double>? get animation
```

An animation whose value represents the current position of the [TabBar]'s selected tab indicator as well as the scrollOffsets of the [TabBar] and [TabBarView].

The animation's value ranges from 0.0 to [length] - 1.0. After the selected tab is changed, the animation's value equals [index]. The animation's value can be [offset] by +/- 1.0 to reflect [TabBarView] drag scrolling.

If this [TabController] was disposed, then return null.

### animationDuration

```dart
Duration get animationDuration
```

Controls the duration of TabController and TabBarView animations.

Defaults to kTabScrollDuration.

### length

```dart
int length
```

The total number of tabs.

Typically greater than one. Must match [TabBar.tabs]'s and [TabBarView.children]'s length.

### index

```dart
int get index
```

The index of the currently selected tab.

Changing the index also updates [previousIndex], sets the [animation]'s value to index, resets [indexIsChanging] to false, and notifies listeners.

To change the currently selected tab and play the [animation] use [animateTo].

The value of [index] must be valid given [length]. If [length] is zero, then [index] will also be zero.

### index

```dart
set index(int value)
```

### previousIndex

```dart
int get previousIndex
```

The index of the previously selected tab.

Initially the same as [index].

### indexIsChanging

```dart
bool get indexIsChanging
```

True while we're animating from [previousIndex] to [index] as a consequence of calling [animateTo].

This value is true during the [animateTo] animation that's triggered when the user taps a [TabBar] tab. It is false when [offset] is changing as a consequence of the user dragging (and "flinging") the [TabBarView].

### animateTo()

```dart
void animateTo(int value, {Duration? duration, Curve curve = Curves.ease})
```

Immediately sets [index] and [previousIndex] and then plays the [animation] from its current value to [index].

While the animation is running [indexIsChanging] is true. When the animation completes [offset] will be 0.0.

### offset

```dart
double get offset
```

The difference between the [animation]'s value and [index].

The offset value must be between -1.0 and 1.0.

This property is typically set by the [TabBarView] when the user drags left or right. A value between -1.0 and 0.0 implies that the TabBarView has been dragged to the left. Similarly a value between 0.0 and 1.0 implies that the TabBarView has been dragged to the right.

### offset

```dart
set offset(double value)
```

### dispose()

```dart
void dispose()
```

# DefaultTabController

```dart
class DefaultTabController extends StatefulWidget {}
```

The [TabController] for descendant widgets that don't specify one explicitly.

{@youtube 560 315 https://www.youtube.com/watch?v=POtoEH-5l40}

[DefaultTabController] is an inherited widget that is used to share a [TabController] with a [TabBar] or a [TabBarView]. It's used when sharing an explicitly created [TabController] isn't convenient because the tab bar widgets are created by a stateless parent widget or by different parent widgets.

{@animation 700 540 https://flutter.github.io/assets-for-api-docs/assets/material/tabs.mp4}

```dart
class MyDemo extends StatelessWidget {
  const MyDemo({super.key});

  static const List<Tab> myTabs = <Tab>[
    Tab(text: 'LEFT'),
    Tab(text: 'RIGHT'),
  ];

  @override
  Widget build(BuildContext context) {
    return DefaultTabController(
      length: myTabs.length,
      child: Scaffold(
        appBar: AppBar(
          bottom: const TabBar(
            tabs: myTabs,
          ),
        ),
        body: TabBarView(
          children: myTabs.map((Tab tab) {
            final String label = tab.text!.toLowerCase();
            return Center(
              child: Text(
                'This is the $label tab',
                style: const TextStyle(fontSize: 36),
              ),
            );
          }).toList(),
        ),
      ),
    );
  }
}
```

### DefaultTabController()

```dart
DefaultTabController({dynamic key, required int length, int initialIndex = 0, required Widget child, Duration? animationDuration})
```

Creates a default tab controller for the given [child] widget.

The [length] argument is typically greater than one. The [length] must match [TabBar.tabs]'s and [TabBarView.children]'s length.

### length

```dart
int length
```

The total number of tabs.

Typically greater than one. Must match [TabBar.tabs]'s and [TabBarView.children]'s length.

### initialIndex

```dart
int initialIndex
```

The initial index of the selected tab.

Defaults to zero.

### animationDuration

```dart
Duration? animationDuration
```

Controls the duration of DefaultTabController and TabBarView animations.

Defaults to kTabScrollDuration.

### child

```dart
Widget child
```

The widget below this widget in the tree.

Typically a [Scaffold] whose [AppBar] includes a [TabBar].

{@macro flutter.widgets.ProxyWidget.child}

### maybeOf()

```dart
TabController? maybeOf(BuildContext context)
```

The closest instance of [DefaultTabController] that encloses the given context, or null if none is found.

{@tool snippet} Typical usage is as follows:

```dart
TabController? controller = DefaultTabController.maybeOf(context);
```

{@end-tool}

Calling this method will create a dependency on the closest [DefaultTabController] in the [context], if there is one.

See also:

- [DefaultTabController.of], which is similar to this method, but asserts if no [DefaultTabController] ancestor is found.

### of()

```dart
TabController of(BuildContext context)
```

The closest instance of [DefaultTabController] that encloses the given context.

If no instance is found, this method will assert in debug mode and throw an exception in release mode.

Calling this method will create a dependency on the closest [DefaultTabController] in the [context].

{@tool snippet} Typical usage is as follows:

```dart
TabController controller = DefaultTabController.of(context);
```

{@end-tool}

See also:

- [DefaultTabController.maybeOf], which is similar to this method, but returns null if no [DefaultTabController] ancestor is found.

### createState()

```dart
State<DefaultTabController> createState()
```
