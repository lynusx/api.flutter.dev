@docImport 'circle_avatar.dart'; @docImport 'drawer.dart'; @docImport 'material.dart';

# UserAccountsDrawerHeader

```dart
class UserAccountsDrawerHeader extends StatefulWidget {}
```

A Material Design [Drawer] header that identifies the app's user.

Requires one of its ancestors to be a [Material] widget.

See also:

- [DrawerHeader], for a drawer header that doesn't show user accounts.
- <https://material.io/design/components/navigation-drawer.html#anatomy>

### UserAccountsDrawerHeader()

```dart
UserAccountsDrawerHeader({dynamic key, Decoration? decoration, EdgeInsetsGeometry? margin = const EdgeInsets.only(bottom: 8.0), Widget? currentAccountPicture, List<Widget>? otherAccountsPictures, Size currentAccountPictureSize = const Size.square(72.0), Size otherAccountsPicturesSize = const Size.square(40.0), required Widget? accountName, required Widget? accountEmail, VoidCallback? onDetailsPressed, Color arrowColor = Colors.white})
```

Creates a Material Design drawer header.

Requires one of its ancestors to be a [Material] widget.

### decoration

```dart
Decoration? decoration
```

The header's background. If decoration is null then a [BoxDecoration] with its background color set to the current theme's primaryColor is used.

### margin

```dart
EdgeInsetsGeometry? margin
```

The margin around the drawer header.

### currentAccountPicture

```dart
Widget? currentAccountPicture
```

A widget placed in the upper-left corner that represents the current user's account. Normally a [CircleAvatar].

### otherAccountsPictures

```dart
List<Widget>? otherAccountsPictures
```

A list of widgets that represent the current user's other accounts. Up to three of these widgets will be arranged in a row in the header's upper-right corner. Normally a list of [CircleAvatar] widgets.

### currentAccountPictureSize

```dart
Size currentAccountPictureSize
```

The size of the [currentAccountPicture].

### otherAccountsPicturesSize

```dart
Size otherAccountsPicturesSize
```

The size of each widget in [otherAccountsPicturesSize].

### accountName

```dart
Widget? accountName
```

A widget that represents the user's current account name. It is displayed on the left, below the [currentAccountPicture].

### accountEmail

```dart
Widget? accountEmail
```

A widget that represents the email address of the user's current account. It is displayed on the left, below the [accountName].

### onDetailsPressed

```dart
VoidCallback? onDetailsPressed
```

A callback that is called when the horizontal area which contains the [accountName] and [accountEmail] is tapped.

### arrowColor

```dart
Color arrowColor
```

The [Color] of the arrow icon.

### createState()

```dart
State<UserAccountsDrawerHeader> createState()
```
