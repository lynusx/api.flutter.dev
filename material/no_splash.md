@docImport 'button_style.dart'; @docImport 'elevated_button.dart'; @docImport 'theme.dart';

# NoSplash

```dart
class NoSplash extends InteractiveInkFeature {}
```

An [InteractiveInkFeature] that doesn't paint a splash.

Use [NoSplash.splashFactory] to defeat the default ink splash drawn by an [InkWell] or [ButtonStyle]. For example, to create an [ElevatedButton] that does not draw the default "ripple" ink splash when it's tapped:

```dart
ElevatedButton(
  style: ElevatedButton.styleFrom(
    splashFactory: NoSplash.splashFactory,
  ),
  onPressed: () { },
  child: const Text('No Splash'),
)
```

### NoSplash()

```dart
NoSplash({required MaterialInkController controller, required dynamic referenceBox, required dynamic color, dynamic onRemoved})
```

Create an [InteractiveInkFeature] that doesn't paint a splash.

### splashFactory

```dart
InteractiveInkFeatureFactory splashFactory
```

Used to specify this type of ink splash for an [InkWell], [InkResponse] material [Theme], or [ButtonStyle].

### paintFeature()

```dart
void paintFeature(Canvas canvas, Matrix4 transform)
```

### confirm()

```dart
void confirm()
```

### cancel()

```dart
void cancel()
```
