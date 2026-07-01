@docImport 'dart:ui';

# decodeImageFromList()

```dart
Future<ui.Image> decodeImageFromList(Uint8List bytes)
```

Creates an image from a list of bytes.

This function attempts to interpret the given bytes an image. If successful, the returned [Future] resolves to the decoded image. Otherwise, the [Future] resolves to null.

If the image is animated, this returns the first frame. Consider [instantiateImageCodec] if support for animated images is necessary.

This function differs from [decodeImageFromList] in that it defers to [PaintingBinding.instantiateImageCodecWithSize], and therefore can be mocked in tests.
