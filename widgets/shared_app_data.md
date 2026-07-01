@docImport 'app.dart';

# SharedAppDataInitCallback

```dart
typedef SharedAppDataInitCallback<T> = T Function()
```

The type of the [SharedAppData.getValue] `init` parameter.

This callback is used to lazily create the initial value for a [SharedAppData] keyword.

# SharedAppData

```dart
class SharedAppData extends StatefulWidget {}
```

Enables sharing key/value data with its `child` and all of the child's descendants.

- `SharedAppData.getValue(context, key, initCallback)` creates a dependency on the key and returns the value for the key from the shared data table. If no value exists for key then the initCallback is used to create the initial value.

- `SharedAppData.setValue(context, key, value)` changes the value of an entry in the shared data table and forces widgets that depend on that entry to be rebuilt.

A widget whose build method uses SharedAppData.getValue(context, keyword, initCallback) creates a dependency on the SharedAppData. When the value of keyword changes with SharedAppData.setValue(), the widget will be rebuilt. The values managed by the SharedAppData are expected to be immutable: intrinsic changes to values will not cause dependent widgets to be rebuilt.

An instance of this widget is created automatically by [WidgetsApp].

There are many ways to share data with a widget subtree. This class is based on [InheritedModel], which is an [InheritedWidget]. It's intended to be used by packages that need to share a modest number of values among their own components.

SharedAppData is not intended to be a substitute for Provider or any of the other general purpose application state systems. SharedAppData is for situations where a package's custom widgets need to share one or a handful of immutable data objects that can be lazily initialized. It exists so that packages like that can deliver custom widgets without requiring the developer to add a package-specific umbrella widget to their application.

A good way to create an SharedAppData key that avoids potential collisions with other packages is to use a static `Object()` value. The `SharedObject` example below does this.

{@tool dartpad} The following sample demonstrates using the automatically created [SharedAppData]. Button presses cause changes to the values for keys 'foo', and 'bar', and those changes only cause the widgets that depend on those keys to be rebuilt.

** See code in examples/api/lib/widgets/shared_app_data/shared_app_data.0.dart ** {@end-tool}

{@tool dartpad} The following sample demonstrates how a single lazily computed value could be shared within an app. A Flutter package that provided custom widgets might use this approach to share a (possibly private) value with instances of those widgets.

** See code in examples/api/lib/widgets/shared_app_data/shared_app_data.1.dart ** {@end-tool}

### SharedAppData()

```dart
SharedAppData({dynamic key, required Widget child})
```

Creates a widget based on [InheritedModel] that supports build dependencies qualified by keywords. Descendant widgets create such dependencies with [SharedAppData.getValue] and they trigger rebuilds with [SharedAppData.setValue].

This widget is automatically created by the [WidgetsApp].

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### createState()

```dart
State<StatefulWidget> createState()
```

### getValue()

```dart
V getValue<K extends Object, V>(BuildContext context, K key, SharedAppDataInitCallback<V> init)
```

Returns the app model's value for `key` and ensures that each time the value of `key` is changed with [SharedAppData.setValue], the specified context will be rebuilt.

If no value for `key` exists then the `init` callback is used to generate an initial value. The callback is expected to return an immutable value because intrinsic changes to the value will not cause dependent widgets to be rebuilt.

A widget that depends on the app model's value for `key` should use this method in their `build` methods to ensure that they are rebuilt if the value changes.

The type parameter `K` is the type of the keyword and `V` is the type of the value.

### setValue()

```dart
void setValue<K extends Object, V>(BuildContext context, K key, V value)
```

Changes the app model's `value` for `key` and rebuilds any widgets that have created a dependency on `key` with [SharedAppData.getValue].

If `value` is `==` to the current value of `key` then nothing is rebuilt.

The `value` is expected to be immutable because intrinsic changes to the value will not cause dependent widgets to be rebuilt.

Unlike [SharedAppData.getValue], this method does _not_ create a dependency between `context` and `key`.

The type parameter `K` is the type of the value's keyword and `V` is the type of the value.
