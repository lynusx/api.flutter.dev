@docImport 'package:flutter/material.dart';

@docImport 'routes.dart'; @docImport 'scroll_controller.dart'; @docImport 'scroll_position.dart'; @docImport 'scroll_view.dart'; @docImport 'scrollable.dart'; @docImport 'single_child_scroll_view.dart';

# PageStorageKey

```dart
class PageStorageKey<T> extends ValueKey<T> {}
```

一种 [Key](https://www.yuque.com/thyname/flutter.foundation/key)，可用于在组件被销毁后将其状态持久化保存到存储中，并在重新创建时恢复该状态。

每个键及其值，加上该组件最近的祖先 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 之间其他 [PageStorageKey](https://www.yuque.com/thyname/flutter.widgets/pagestoragekey) 组成的祖先链，必须在该祖先 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 内保持唯一。为了确保组件重新创建时能够找到已保存的值，键的值不能使用每次创建组件时都会改变标识的对象。

另请参阅：

- [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage)，为使用 [PageStorageKey](https://www.yuque.com/thyname/flutter.widgets/pagestoragekey) 的组件管理数据存储。

### PageStorageKey()

```dart
PageStorageKey(dynamic value)
```

创建一个 [ValueKey](https://www.yuque.com/thyname/flutter.foundation/valuekey)，用于定义 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 值的保存位置。

# PageStorageBucket

```dart
class PageStorageBucket {}
```

与应用中某个页面关联的存储桶（storage bucket）。

可用于存储需要在不同页面之间导航时依然保持的按页状态。

### writeState()

```dart
void writeState(BuildContext context, dynamic data, {Object? identifier})
```

使用指定的标识符，或根据给定的 context 计算出的标识符，将给定的数据写入此页面存储桶。计算出的标识符基于从 context 到拥有此页面存储桶的 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 组件路径上找到的 [PageStorageKey](https://www.yuque.com/thyname/flutter.widgets/pagestoragekey)。

如果未提供显式的标识符，且未找到任何 [PageStorageKey](https://www.yuque.com/thyname/flutter.widgets/pagestoragekey)，则不会保存该 `data`。

### readState()

```dart
dynamic readState(BuildContext context, {Object? identifier})
```

使用指定的标识符，或根据给定的 context 计算出的标识符，从此页面存储桶中读取数据。计算出的标识符基于从 context 到拥有此页面存储桶的 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 组件路径上找到的 [PageStorageKey](https://www.yuque.com/thyname/flutter.widgets/pagestoragekey)。

如果未提供显式的标识符，且未找到任何 [PageStorageKey](https://www.yuque.com/thyname/flutter.widgets/pagestoragekey)，则返回 null。

# PageStorage

```dart
class PageStorage extends StatelessWidget {}
```

建立一个子树，其中的组件可以选择在被销毁后持久化保存其状态。

[PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 用于保存和恢复能够比组件本身存活更久的值。例如，当多个页面组合在标签页中时，切换页面会导致其组件被销毁，其状态也随之丢失。通过在根部添加一个 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage)，并为每个页面添加一个 [PageStorageKey](https://www.yuque.com/thyname/flutter.widgets/pagestoragekey)，页面的部分状态（例如 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 组件的滚动位置）会自动保存到其最近的祖先 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 中，并在切换回该页面时恢复。

通常你不需要显式使用 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage)，因为路由中已经包含了它。

如果启用了 [ScrollController.keepScrollOffset]，[Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 会使用 [PageStorageKey](https://www.yuque.com/thyname/flutter.widgets/pagestoragekey) 来保存其 [ScrollPosition](https://www.yuque.com/thyname/flutter.widgets/scrollposition)。当同一个组件最近的祖先 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage)（例如同一路由）内出现多个可滚动组件（[ListView](https://www.yuque.com/thyname/flutter.widgets/listview)、[SingleChildScrollView](https://www.yuque.com/thyname/flutter.widgets/singlechildscrollview)、[TextField](https://www.yuque.com/thyname/flutter.material/textfield) 等）时，若要独立保存它们各自的位置，必须为每个组件指定唯一的 [PageStorageKey](https://www.yuque.com/thyname/flutter.widgets/pagestoragekey)，或者将其中一些组件的 `keepScrollOffset` 属性设为 false 以阻止保存。

{@tool dartpad} 此示例展示了如何显式使用 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 来存储其子页面的状态。每个页面都包含一个可滚动列表，借助 [PageStorageKey](https://www.yuque.com/thyname/flutter.widgets/pagestoragekey)，在标签页之间切换时会保留其滚动位置。

** See code in examples/api/lib/widgets/page_storage/page_storage.0.dart ** {@end-tool}

另请参阅：

- [ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute)，其中包含此类。

### PageStorage()

```dart
PageStorage({dynamic key, required PageStorageBucket bucket, required Widget child})
```

创建一个为其后代组件提供存储桶的组件。

### child

```dart
Widget child
```

此组件在组件树中的下一级子组件。

{@macro flutter.widgets.ProxyWidget.child}

### bucket

```dart
PageStorageBucket bucket
```

此子树所使用的页面存储桶。

### maybeOf()

```dart
PageStorageBucket? maybeOf(BuildContext context)
```

从包含给定 context 的最近一个 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 组件实例中获取其 [PageStorageBucket](https://www.yuque.com/thyname/flutter.widgets/pagestoragebucket)。

如果不存在这样的祖先，则返回 null。

典型用法如下：

```dart
PageStorageBucket? bucket = PageStorage.of(context);
```

此方法的开销可能较大（它会遍历 element 树）。

另请参阅：

- [PageStorage.of]，与此方法类似，但在未找到 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 祖先时会触发断言。

### of()

```dart
PageStorageBucket of(BuildContext context)
```

从包含给定 context 的最近一个 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 组件实例中获取其 [PageStorageBucket](https://www.yuque.com/thyname/flutter.widgets/pagestoragebucket)。

如果未找到祖先，此方法会在调试模式下触发断言，并在发布模式下抛出异常。

典型用法如下：

```dart
PageStorageBucket bucket = PageStorage.of(context);
```

此方法的开销可能较大（它会遍历 element 树）。

另请参阅：

- [PageStorage.maybeOf]，与此方法类似，但在未找到 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 祖先时返回 null。
