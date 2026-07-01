# ActionIconThemeData

```dart
class ActionIconThemeData with Diagnosticable {}
```

A [ActionIconThemeData] that overrides the default icons of [BackButton], [CloseButton], [DrawerButton], and [EndDrawerButton] with [ActionIconTheme.of] or the overall [Theme]'s [ThemeData.actionIconTheme].

### ActionIconThemeData()

```dart
ActionIconThemeData({WidgetBuilder? backButtonIconBuilder, WidgetBuilder? closeButtonIconBuilder, WidgetBuilder? drawerButtonIconBuilder, WidgetBuilder? endDrawerButtonIconBuilder})
```

Creates an [ActionIconThemeData].

The builders [backButtonIconBuilder], [closeButtonIconBuilder], [drawerButtonIconBuilder], [endDrawerButtonIconBuilder] may be null.

### backButtonIconBuilder

```dart
WidgetBuilder? backButtonIconBuilder
```

Overrides [BackButtonIcon]'s icon.

If [backButtonIconBuilder] is null, then [BackButtonIcon] fallbacks to the platform's default back button icon.

### closeButtonIconBuilder

```dart
WidgetBuilder? closeButtonIconBuilder
```

Overrides [CloseButtonIcon]'s icon.

If [closeButtonIconBuilder] is null, then [CloseButtonIcon] fallbacks to the platform's default close button icon.

### drawerButtonIconBuilder

```dart
WidgetBuilder? drawerButtonIconBuilder
```

Overrides [DrawerButtonIcon]'s icon.

If [drawerButtonIconBuilder] is null, then [DrawerButtonIcon] fallbacks to the platform's default drawer button icon.

### endDrawerButtonIconBuilder

```dart
WidgetBuilder? endDrawerButtonIconBuilder
```

Overrides [EndDrawerButtonIcon]'s icon.

If [endDrawerButtonIconBuilder] is null, then [EndDrawerButtonIcon] fallbacks to the platform's default end drawer button icon.

### copyWith()

```dart
ActionIconThemeData copyWith({WidgetBuilder? backButtonIconBuilder, WidgetBuilder? closeButtonIconBuilder, WidgetBuilder? drawerButtonIconBuilder, WidgetBuilder? endDrawerButtonIconBuilder})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
ActionIconThemeData? lerp(ActionIconThemeData? a, ActionIconThemeData? b, double t)
```

Linearly interpolate between two action icon themes.

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ActionIconTheme

```dart
class ActionIconTheme extends InheritedTheme {}
```

An inherited widget that overrides the default icon of [BackButtonIcon], [CloseButtonIcon], [DrawerButtonIcon], and [EndDrawerButtonIcon] in this widget's subtree.

{@tool dartpad} This example shows how to define custom builders for drawer and back buttons.

** See code in examples/api/lib/material/action_buttons/action_icon_theme.0.dart ** {@end-tool}

### ActionIconTheme()

```dart
ActionIconTheme({dynamic key, required ActionIconThemeData data, required dynamic child})
```

Creates a theme that overrides the default icon of [BackButtonIcon], [CloseButtonIcon], [DrawerButtonIcon], and [EndDrawerButtonIcon] in this widget's subtree.

### data

```dart
ActionIconThemeData data
```

Specifies the default icon overrides for descendant [BackButtonIcon], [CloseButtonIcon], [DrawerButtonIcon], and [EndDrawerButtonIcon] widgets.

### of()

```dart
ActionIconThemeData? of(BuildContext context)
```

Retrieves the [ActionIconThemeData] from the closest ancestor [ActionIconTheme] widget.

If there is no enclosing [ActionIconTheme] widget, then [ThemeData.actionIconTheme] is used.

Typical usage is as follows:

```dart
ActionIconThemeData? theme = ActionIconTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(ActionIconTheme oldWidget)
```
