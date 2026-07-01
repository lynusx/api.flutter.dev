@docImport 'package:flutter/material.dart';

@docImport 'routes.dart'; @docImport 'scroll_controller.dart'; @docImport 'scroll_position.dart'; @docImport 'scroll_view.dart'; @docImport 'scrollable.dart'; @docImport 'single_child_scroll_view.dart';

# PageStorageKey

```dart
class PageStorageKey<T> extends ValueKey<T> {}
```

A [Key] that can be used to persist the widget state in storage after the destruction and will be restored when recreated.

Each key with its value plus the ancestor chain of other [PageStorageKey]s need to be unique within the widget's closest ancestor [PageStorage]. To make it possible for a saved value to be found when a widget is recreated, the key's value must not be objects whose identity will change each time the widget is created.

See also:

- [PageStorage], which manages the data storage for widgets using [PageStorageKey]s.

### PageStorageKey()

```dart
PageStorageKey(dynamic value)
```

Creates a [ValueKey] that defines where [PageStorage] values will be saved.

# PageStorageBucket

```dart
class PageStorageBucket {}
```

A storage bucket associated with a page in an app.

Useful for storing per-page state that persists across navigations from one page to another.

### writeState()

```dart
void writeState(BuildContext context, dynamic data, {Object? identifier})
```

Write the given data into this page storage bucket using the specified identifier or an identifier computed from the given context. The computed identifier is based on the [PageStorageKey]s found in the path from context to the [PageStorage] widget that owns this page storage bucket.

If an explicit identifier is not provided and no [PageStorageKey]s are found, then the `data` is not saved.

### readState()

```dart
dynamic readState(BuildContext context, {Object? identifier})
```

Read given data from into this page storage bucket using the specified identifier or an identifier computed from the given context. The computed identifier is based on the [PageStorageKey]s found in the path from context to the [PageStorage] widget that owns this page storage bucket.

If an explicit identifier is not provided and no [PageStorageKey]s are found, then null is returned.

# PageStorage

```dart
class PageStorage extends StatelessWidget {}
```

Establish a subtree in which widgets can opt into persisting states after being destroyed.

[PageStorage] is used to save and restore values that can outlive the widget. For example, when multiple pages are grouped in tabs, when a page is switched out, its widget is destroyed and its state is lost. By adding a [PageStorage] at the root and adding a [PageStorageKey] to each page, some of the page's state (e.g. the scroll position of a [Scrollable] widget) will be stored automatically in its closest ancestor [PageStorage], and restored when it's switched back.

Usually you don't need to explicitly use a [PageStorage], since it's already included in routes.

[PageStorageKey] is used by [Scrollable] if [ScrollController.keepScrollOffset] is enabled to save their [ScrollPosition]s. When more than one scrollable ([ListView], [SingleChildScrollView], [TextField], etc.) appears within the widget's closest ancestor [PageStorage] (such as within the same route), to save all of their positions independently, one must give each of them unique [PageStorageKey]s, or set the `keepScrollOffset` property of some such widgets to false to prevent saving.

{@tool dartpad} This sample shows how to explicitly use a [PageStorage] to store the states of its children pages. Each page includes a scrollable list, whose position is preserved when switching between the tabs thanks to the help of [PageStorageKey].

** See code in examples/api/lib/widgets/page_storage/page_storage.0.dart ** {@end-tool}

See also:

- [ModalRoute], which includes this class.

### PageStorage()

```dart
PageStorage({dynamic key, required PageStorageBucket bucket, required Widget child})
```

Creates a widget that provides a storage bucket for its descendants.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### bucket

```dart
PageStorageBucket bucket
```

The page storage bucket to use for this subtree.

### maybeOf()

```dart
PageStorageBucket? maybeOf(BuildContext context)
```

The [PageStorageBucket] from the closest instance of a [PageStorage] widget that encloses the given context.

Returns null if none exists.

Typical usage is as follows:

```dart
PageStorageBucket? bucket = PageStorage.of(context);
```

This method can be expensive (it walks the element tree).

See also:

- [PageStorage.of], which is similar to this method, but asserts if no [PageStorage] ancestor is found.

### of()

```dart
PageStorageBucket of(BuildContext context)
```

The [PageStorageBucket] from the closest instance of a [PageStorage] widget that encloses the given context.

If no ancestor is found, this method will assert in debug mode, and throw an exception in release mode.

Typical usage is as follows:

```dart
PageStorageBucket bucket = PageStorage.of(context);
```

This method can be expensive (it walks the element tree).

See also:

- [PageStorage.maybeOf], which is similar to this method, but returns null if no [PageStorage] ancestor is found.

### build()

```dart
Widget build(BuildContext context)
```
