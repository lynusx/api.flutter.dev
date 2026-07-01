@docImport 'animated_icons.dart'; @docImport 'icon_button.dart';

# PlatformAdaptiveIcons

```dart
final class PlatformAdaptiveIcons implements Icons {}
```

A set of platform-adaptive Material Design icons.

Use [Icons.adaptive] to access a static instance of this class.

### arrow_back

```dart
IconData get arrow_back
```

Platform-adaptive icon for <i class="material-icons md-36">arrow_back</i> — material icon named "arrow back" and <i class="material-icons md-36">arrow_back_ios</i> — material icon named "arrow back ios".;

### arrow_back_outlined

```dart
IconData get arrow_back_outlined
```

Platform-adaptive icon for <i class="material-icons-outlined md-36">arrow_back</i> — material icon named "arrow back" (outlined) and <i class="material-icons-outlined md-36">arrow_back_ios</i> — material icon named "arrow back ios" (outlined).;

### arrow_back_rounded

```dart
IconData get arrow_back_rounded
```

Platform-adaptive icon for <i class="material-icons-round md-36">arrow_back</i> — material icon named "arrow back" (round) and <i class="material-icons-round md-36">arrow_back_ios</i> — material icon named "arrow back ios" (round).;

### arrow_back_sharp

```dart
IconData get arrow_back_sharp
```

Platform-adaptive icon for <i class="material-icons-sharp md-36">arrow_back</i> — material icon named "arrow back" (sharp) and <i class="material-icons-sharp md-36">arrow_back_ios</i> — material icon named "arrow back ios" (sharp).;

### arrow_forward

```dart
IconData get arrow_forward
```

Platform-adaptive icon for <i class="material-icons md-36">arrow_forward</i> — material icon named "arrow forward" and <i class="material-icons md-36">arrow_forward_ios</i> — material icon named "arrow forward ios".;

### arrow_forward_outlined

```dart
IconData get arrow_forward_outlined
```

Platform-adaptive icon for <i class="material-icons-outlined md-36">arrow_forward</i> — material icon named "arrow forward" (outlined) and <i class="material-icons-outlined md-36">arrow_forward_ios</i> — material icon named "arrow forward ios" (outlined).;

### arrow_forward_rounded

```dart
IconData get arrow_forward_rounded
```

Platform-adaptive icon for <i class="material-icons-round md-36">arrow_forward</i> — material icon named "arrow forward" (round) and <i class="material-icons-round md-36">arrow_forward_ios</i> — material icon named "arrow forward ios" (round).;

### arrow_forward_sharp

```dart
IconData get arrow_forward_sharp
```

Platform-adaptive icon for <i class="material-icons-sharp md-36">arrow_forward</i> — material icon named "arrow forward" (sharp) and <i class="material-icons-sharp md-36">arrow_forward_ios</i> — material icon named "arrow forward ios" (sharp).;

### flip_camera

```dart
IconData get flip_camera
```

Platform-adaptive icon for <i class="material-icons md-36">flip_camera_android</i> — material icon named "flip camera android" and <i class="material-icons md-36">flip_camera_ios</i> — material icon named "flip camera ios".;

### flip_camera_outlined

```dart
IconData get flip_camera_outlined
```

Platform-adaptive icon for <i class="material-icons-outlined md-36">flip_camera_android</i> — material icon named "flip camera android" (outlined) and <i class="material-icons-outlined md-36">flip_camera_ios</i> — material icon named "flip camera ios" (outlined).;

### flip_camera_rounded

```dart
IconData get flip_camera_rounded
```

Platform-adaptive icon for <i class="material-icons-round md-36">flip_camera_android</i> — material icon named "flip camera android" (round) and <i class="material-icons-round md-36">flip_camera_ios</i> — material icon named "flip camera ios" (round).;

### flip_camera_sharp

```dart
IconData get flip_camera_sharp
```

Platform-adaptive icon for <i class="material-icons-sharp md-36">flip_camera_android</i> — material icon named "flip camera android" (sharp) and <i class="material-icons-sharp md-36">flip_camera_ios</i> — material icon named "flip camera ios" (sharp).;

### more

```dart
IconData get more
```

Platform-adaptive icon for <i class="material-icons md-36">more_vert</i> — material icon named "more vert" and <i class="material-icons md-36">more_horiz</i> — material icon named "more horiz".;

### more_outlined

```dart
IconData get more_outlined
```

Platform-adaptive icon for <i class="material-icons-outlined md-36">more_vert</i> — material icon named "more vert" (outlined) and <i class="material-icons-outlined md-36">more_horiz</i> — material icon named "more horiz" (outlined).;

### more_rounded

```dart
IconData get more_rounded
```

Platform-adaptive icon for <i class="material-icons-round md-36">more_vert</i> — material icon named "more vert" (round) and <i class="material-icons-round md-36">more_horiz</i> — material icon named "more horiz" (round).;

### more_sharp

```dart
IconData get more_sharp
```

Platform-adaptive icon for <i class="material-icons-sharp md-36">more_vert</i> — material icon named "more vert" (sharp) and <i class="material-icons-sharp md-36">more_horiz</i> — material icon named "more horiz" (sharp).;

### share

```dart
IconData get share
```

Platform-adaptive icon for <i class="material-icons md-36">share</i> — material icon named "share" and <i class="material-icons md-36">ios_share</i> — material icon named "ios share".;

### share_outlined

```dart
IconData get share_outlined
```

Platform-adaptive icon for <i class="material-icons-outlined md-36">share</i> — material icon named "share" (outlined) and <i class="material-icons-outlined md-36">ios_share</i> — material icon named "ios share" (outlined).;

### share_rounded

```dart
IconData get share_rounded
```

Platform-adaptive icon for <i class="material-icons-round md-36">share</i> — material icon named "share" (round) and <i class="material-icons-round md-36">ios_share</i> — material icon named "ios share" (round).;

### share_sharp

```dart
IconData get share_sharp
```

Platform-adaptive icon for <i class="material-icons-sharp md-36">share</i> — material icon named "share" (sharp) and <i class="material-icons-sharp md-36">ios_share</i> — material icon named "ios share" (sharp).;

# Icons

```dart
abstract final class Icons {}
```

Identifiers for the supported [Material Icons](https://material.io/resources/icons).

Use with the [Icon] class to show specific icons. Icons are identified by their name as listed below, e.g. [Icons.airplanemode_on].

Search and find the perfect icon on the [Google Fonts](https://material.io/resources/icons) website.

To use this class, make sure you set `uses-material-design: true` in your project's `pubspec.yaml` file in the `flutter` section. This ensures that the Material Icons font is included in your application. This font is used to display the icons. For example:

```yaml
name: my_awesome_application
flutter:
  uses-material-design: true
```

{@tool snippet} This example shows how to create a [Row] of [Icon]s in different colors and sizes. The first [Icon] uses a [Icon.semanticLabel] to announce in accessibility modes like TalkBack and VoiceOver.

![The following code snippet would generate a row of icons consisting of a pink heart, a green musical note, and a blue umbrella, each progressively bigger than the last.](https://flutter.github.io/assets-for-api-docs/assets/widgets/icon.png)

```dart
const Row(
  mainAxisAlignment: MainAxisAlignment.spaceAround,
  children: <Widget>[
    Icon(
      Icons.favorite,
      color: Colors.pink,
      size: 24.0,
      semanticLabel: 'Text to announce in accessibility modes',
    ),
    Icon(
      Icons.audiotrack,
      color: Colors.green,
      size: 30.0,
    ),
    Icon(
      Icons.beach_access,
      color: Colors.blue,
      size: 36.0,
    ),
  ],
)
```

{@end-tool}

See also:

- [Icon]
- [IconButton]
- <https://material.io/resources/icons>
- [AnimatedIcons], for the list of available animated Material Icons.

### adaptive

```dart
PlatformAdaptiveIcons get adaptive
```

A set of platform-adaptive Material Design icons.

Provides a convenient way to show a certain set of platform-appropriate icons on Apple platforms.

Use with the [Icon] class to show specific icons.

{@tool snippet} This example shows how to create a share icon that uses the material icon named "share" on non-Apple platforms, and the icon named "ios share" on Apple platforms.

```dart
Icon(
  Icons.adaptive.share,
)
```

{@end-tool}

See also:

- [Icon]
- [IconButton]
- <https://design.google.com/icons/>
