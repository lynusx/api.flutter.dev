# FontLoader

```dart
class FontLoader {}
```

A class that enables the dynamic loading of fonts at runtime.

The [FontLoader] class provides a builder pattern, where the caller builds up the assets that make up a font family, then calls [load] to load the entire font family into a running Flutter application.

### FontLoader()

```dart
FontLoader(String family)
```

Creates a new [FontLoader] that will load font assets for the specified [family].

The font family will not be available for use until [load] has been called.

### family

```dart
String family
```

The font family being loaded.

The family groups a series of related font assets, each of which defines how to render a specific [FontWeight] and [FontStyle] within the family.

### addFont()

```dart
void addFont(Future<ByteData> bytes)
```

Registers a font asset to be loaded by this font loader.

The [bytes] argument specifies the actual font asset bytes. Currently, only OpenType (OTF) and TrueType (TTF) fonts are supported.

The [load] method will load fonts in the order this is called.

### load()

```dart
Future<void> load()
```

Loads this font loader's font [family] and all of its associated assets into the Flutter engine, making the font available to the current application.

This method should only be called once per font loader. Attempts to load fonts from the same loader more than once will cause a [StateError] to be thrown.

The returned future will complete with an error if any of the font asset futures yield an error.

### loadFont()

```dart
Future<void> loadFont(Uint8List list, String family)
```

Hook called to load a font asset into the engine.

Subclasses may override this to replace the default loading logic with custom logic (for example, to mock the underlying engine API in tests).
