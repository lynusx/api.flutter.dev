# AssetManifest

```dart
abstract class AssetManifest {}
```

Contains details about available assets and their variants. See [Resolution-aware image assets](https://flutter.dev/to/resolution-aware-images) to learn about asset variants and how to declare them.

### loadFromAssetBundle()

```dart
Future<AssetManifest> loadFromAssetBundle(AssetBundle bundle)
```

Loads asset manifest data from an [AssetBundle] object and creates an [AssetManifest] object from that data.

### listAssets()

```dart
List<String> listAssets()
```

Lists the keys of all main assets. This does not include assets that are variants of other assets.

The logical key maps to the path of an asset specified in the pubspec.yaml file at build time.

See [Specifying assets](https://docs.flutter.dev/ui/assets/assets-and-images#specifying-assets) and [Loading assets](https://docs.flutter.dev/ui/assets/assets-and-images#loading-assets) for more information.

### getAssetVariants()

```dart
List<AssetMetadata>? getAssetVariants(String key)
```

Retrieves metadata about an asset and its variants. Returns null if the key was not found in the asset manifest.

This method considers a main asset to be a variant of itself. The returned list will include it if it exists.

# AssetMetadata

```dart
class AssetMetadata {}
```

Contains information about an asset.

### AssetMetadata()

```dart
AssetMetadata({required String key, required double? targetDevicePixelRatio, required bool main})
```

Creates an object containing information about an asset.

### targetDevicePixelRatio

```dart
double? targetDevicePixelRatio
```

The device pixel ratio that this asset is most ideal for. This is determined by the name of the parent folder of the asset file. For example, if the parent folder is named "3.0x", the target device pixel ratio of that asset will be interpreted as 3.

This will be null if the parent folder name is not a ratio value followed by an "x".

See [Resolution-aware image assets](https://flutter.dev/to/resolution-aware-images) for more information.

### key

```dart
String key
```

The asset's key, which is the path to the asset specified in the pubspec.yaml file at build time.

### main

```dart
bool main
```

Whether or not this is a main asset. In other words, this is true if this asset is not a variant of another asset.
