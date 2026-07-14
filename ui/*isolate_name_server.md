# IsolateNameServer

```dart
abstract final class IsolateNameServer {}
```

用于在各个 [Isolate](https://www.yuque.com/thyname/dart.isolate/isolate) 之间简单地共享 [SendPort](https://www.yuque.com/thyname/dart.isolate/sendport) 的静态方法集合。

所有 isolate 共享一个从名称到端口的全局映射。一个 isolate 可以使用 [registerPortWithName] 以给定名称注册一个 [SendPort](https://www.yuque.com/thyname/dart.isolate/sendport)；另一个 isolate 随后可以使用 [lookupPortByName] 查找该端口。

要创建一个 [SendPort](https://www.yuque.com/thyname/dart.isolate/sendport)，首先创建一个 [ReceivePort](https://www.yuque.com/thyname/dart.isolate/receiveport)，然后使用 [ReceivePort.sendPort]。

由于多个 isolate 都可以各自获取与某个特定 [ReceivePort](https://www.yuque.com/thyname/dart.isolate/receiveport) 关联的同一个 [SendPort](https://www.yuque.com/thyname/dart.isolate/sendport)，建立在此机制之上的协议通常应仅包含一条消息。如果需要更复杂的双向通信或多消息通信，建议在第一条消息中建立一个单独的通信通道（例如通过传递一个专用的 [SendPort](https://www.yuque.com/thyname/dart.isolate/sendport)）。

### lookupPortByName()

```dart
SendPort? lookupPortByName(String name)
```

查找与给定名称关联的 [SendPort](https://www.yuque.com/thyname/dart.isolate/sendport)。

如果该名称不存在，则返回 null。要预先注册该名称，请参见 [registerPortWithName]。

`name` 参数不能为 null。

### registerPortWithName()

```dart
bool registerPortWithName(SendPort port, String name)
```

以给定名称注册一个 [SendPort](https://www.yuque.com/thyname/dart.isolate/sendport)。

如果注册成功则返回 true，如果该名称条目已存在（此时先前的注册保持不变）则返回 false。要移除注册，请参见 [removePortNameMapping]。

一旦某个端口以某个名称注册，就可以在任何 [Isolate](https://www.yuque.com/thyname/dart.isolate/isolate) 中使用 [lookupPortByName] 获取它。

多个 isolate 应避免尝试以相同的名称注册端口，因为这样做存在固有的竞争条件。

`port` 和 `name` 参数都不能为 null。

### removePortNameMapping()

```dart
bool removePortNameMapping(String name)
```

根据名称移除一个名称到 [SendPort](https://www.yuque.com/thyname/dart.isolate/sendport) 的映射。

如果映射被成功移除则返回 true，如果该映射不存在则返回 false。要添加注册，请参见 [registerPortWithName]。

一般来说，移除端口名称映射本质上是一个存在竞争条件的操作（另一个 isolate 可能恰好在该名称被移除之前获取到了它，因此即使映射已被移除，该 isolate 仍然能够通过该端口进行通信）。

`name` 参数不能为 null。
