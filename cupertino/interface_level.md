# CupertinoUserInterfaceLevelData

```dart
enum CupertinoUserInterfaceLevelData {}
```

Indicates the visual level for a piece of content. Equivalent to `UIUserInterfaceLevel` from `UIKit`.

See also:

- `UIUserInterfaceLevel`, the UIKit equivalent: https://developer.apple.com/documentation/uikit/uiuserinterfacelevel.

The level for your window's main content.

The level for content visually above [base].

# CupertinoUserInterfaceLevel

```dart
class CupertinoUserInterfaceLevel extends InheritedWidget {}
```

Establishes a subtree in which [CupertinoUserInterfaceLevel.of] resolves to the given visual elevation from the [CupertinoUserInterfaceLevelData]. This can be used to apply style differences based on a widget's elevation.

Querying the current elevation status using [CupertinoUserInterfaceLevel.of] will cause your widget to rebuild automatically whenever the [CupertinoUserInterfaceLevelData] changes.

If no [CupertinoUserInterfaceLevel] is in scope then the [CupertinoUserInterfaceLevel.of] method will throw an exception. Alternatively, [CupertinoUserInterfaceLevel.maybeOf] can be used, which returns null instead of throwing if no [CupertinoUserInterfaceLevel] is in scope.

See also:

- [CupertinoUserInterfaceLevelData], specifies the visual level for the content in the subtree [CupertinoUserInterfaceLevel] established.

### CupertinoUserInterfaceLevel()

```dart
CupertinoUserInterfaceLevel({dynamic key, required CupertinoUserInterfaceLevelData data, required Widget child})
```

Creates a [CupertinoUserInterfaceLevel] to change descendant Cupertino widget's visual level.

### updateShouldNotify()

```dart
bool updateShouldNotify(CupertinoUserInterfaceLevel oldWidget)
```

### of()

```dart
CupertinoUserInterfaceLevelData of(BuildContext context)
```

The data from the closest instance of this class that encloses the given context.

You can use this function to query the user interface elevation level within the given [BuildContext]. When that information changes, your widget will be scheduled to be rebuilt, keeping your widget up-to-date.

See also:

- [maybeOf], which is similar, but will return null if no [CupertinoUserInterfaceLevel] encloses the given context.

### maybeOf()

```dart
CupertinoUserInterfaceLevelData? maybeOf(BuildContext context)
```

The data from the closest instance of this class that encloses the given context, if there is one.

Returns null if no [CupertinoUserInterfaceLevel] encloses the given context.

You can use this function to query the user interface elevation level within the given [BuildContext]. When that information changes, your widget will be scheduled to be rebuilt, keeping your widget up-to-date.

See also:

- [of], which is similar, but will throw an exception if no [CupertinoUserInterfaceLevel] encloses the given context.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
