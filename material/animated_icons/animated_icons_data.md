# AnimatedIcons

```dart
abstract final class AnimatedIcons {}
```

Identifier for the supported Material Design animated icons.

Use with [AnimatedIcon] class to show specific animated icons.

{@tool dartpad} This example shows how to create an animated icon. The icon is animated forward and reverse in a loop.

** See code in examples/api/lib/material/animated_icon/animated_icons_data.0.dart ** {@end-tool}

See also:

- [Icons], for the list of available static Material Icons.

### add_event

```dart
AnimatedIconData add_event
```

The Material Design add to event icon animation.

{@animation 72 72 https://flutter.github.io/assets-for-api-docs/assets/widgets/add_event.mp4}

### arrow_menu

```dart
AnimatedIconData arrow_menu
```

The Material Design arrow to menu icon animation.

{@animation 72 72 https://flutter.github.io/assets-for-api-docs/assets/widgets/arrow_menu.mp4}

### close_menu

```dart
AnimatedIconData close_menu
```

The Material Design close to menu icon animation.

{@animation 72 72 https://flutter.github.io/assets-for-api-docs/assets/widgets/close_menu.mp4}

### ellipsis_search

```dart
AnimatedIconData ellipsis_search
```

The Material Design ellipsis to search icon animation.

{@animation 72 72 https://flutter.github.io/assets-for-api-docs/assets/widgets/ellipsis_search.mp4}

### event_add

```dart
AnimatedIconData event_add
```

The Material Design event to add icon animation.

{@animation 72 72 https://flutter.github.io/assets-for-api-docs/assets/widgets/event_add.mp4}

### home_menu

```dart
AnimatedIconData home_menu
```

The Material Design home to menu icon animation.

{@animation 72 72 https://flutter.github.io/assets-for-api-docs/assets/widgets/home_menu.mp4}

### list_view

```dart
AnimatedIconData list_view
```

The Material Design list to view icon animation.

{@animation 72 72 https://flutter.github.io/assets-for-api-docs/assets/widgets/list_view.mp4}

### menu_arrow

```dart
AnimatedIconData menu_arrow
```

The Material Design menu to arrow icon animation.

{@animation 72 72 https://flutter.github.io/assets-for-api-docs/assets/widgets/menu_arrow.mp4}

### menu_close

```dart
AnimatedIconData menu_close
```

The Material Design menu to close icon animation.

{@animation 72 72 https://flutter.github.io/assets-for-api-docs/assets/widgets/menu_close.mp4}

### menu_home

```dart
AnimatedIconData menu_home
```

The Material Design menu to home icon animation.

{@animation 72 72 https://flutter.github.io/assets-for-api-docs/assets/widgets/menu_home.mp4}

### pause_play

```dart
AnimatedIconData pause_play
```

The Material Design pause to play icon animation.

{@animation 72 72 https://flutter.github.io/assets-for-api-docs/assets/widgets/pause_play.mp4}

### play_pause

```dart
AnimatedIconData play_pause
```

The Material Design play to pause icon animation.

{@animation 72 72 https://flutter.github.io/assets-for-api-docs/assets/widgets/play_pause.mp4}

### search_ellipsis

```dart
AnimatedIconData search_ellipsis
```

The Material Design search to ellipsis icon animation.

{@animation 72 72 https://flutter.github.io/assets-for-api-docs/assets/widgets/search_ellipsis.mp4}

### view_list

```dart
AnimatedIconData view_list
```

The Material Design view to list icon animation.

{@animation 72 72 https://flutter.github.io/assets-for-api-docs/assets/widgets/view_list.mp4}

# AnimatedIconData

```dart
abstract class AnimatedIconData {}
```

Vector graphics data for icons used by [AnimatedIcon].

Instances of this class are currently opaque because we have not committed to a specific animated vector graphics format.

See also:

- [AnimatedIcons], a class that contains constants that implement this interface.

### AnimatedIconData()

```dart
AnimatedIconData()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### matchTextDirection

```dart
bool get matchTextDirection
```

Whether this icon should be mirrored horizontally when text direction is right-to-left.

See also:

- [TextDirection], which discusses concerns regarding reading direction in Flutter.
- [Directionality], a widget which determines the ambient directionality.
