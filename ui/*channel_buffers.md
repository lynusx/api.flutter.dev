# DrainChannelCallback

```dart
typedef DrainChannelCallback = Future<void> Function(ByteData? data, PlatformMessageResponseCallback callback)
```

已弃用。请迁移至 [ChannelCallback]。

[ChannelBuffers.drain] 的 `callback` 参数的函数签名。

第一个参数是插件发送的数据。

第二个参数是一个闭包，调用它可以将消息发回给插件。

# ChannelCallback

```dart
typedef ChannelCallback = void Function(ByteData? data, PlatformMessageResponseCallback callback)
```

[ChannelBuffers.setListener] 的 `callback` 参数的函数签名。

第一个参数是插件发送的数据。

第二个参数是一个闭包，调用它可以将消息发回给插件。

另请参阅：

- [PlatformMessageResponseCallback]，用于回复的类型。

# ChannelBuffers

```dart
class ChannelBuffers {}
```

引擎侧插件发送的消息与框架侧对应插件代码之间的缓冲与分发机制。

某个通道的消息会一直存储，直到通过 [setListener] 为该通道设置了监听器。每个通道最多只能配置一个监听器。

通常，一旦在 Flutter 框架的 [BinaryMessenger] 上设置了回调，这些缓冲区就会被清空。（参见 [setListener]。）

## 通道名称

按照惯例，通道通常以反向 DNS 前缀加斜杠再加特定领域名称来命名。例如，`com.example/demo`。

通道名称不能包含 U+0000 NULL 字符，因为它们会通过使用以 null 结尾的字符串的 API 传递。

## 缓冲区容量与溢出

每个通道都有一个有限的缓冲区容量，当超出容量时，消息会以先进先出（FIFO）的方式被删除。

默认情况下，缓冲区为每个通道存储一条消息，当消息溢出时，在调试模式下会向控制台打印一条消息。该消息内容类似如下：

> A message on the com.example channel was discarded before it could be
> handled.
> This happens when a plugin sends messages to the framework side before the
> framework has had an opportunity to register a listener. See the
> ChannelBuffers API documentation for details on how to configure the channel
> to expect more messages, or to expect messages to get discarded:
> https://api.flutter.dev/flutter/dart-ui/ChannelBuffers-class.html

任何大小的选择都存在权衡取舍。应根据通道的语义来选择合适的大小。要修改大小，插件可以按照下文所述，通过控制通道发送一条消息。

大小为 0 适用于希望在引擎和框架尚未就绪时发送的消息被忽略的通道。例如，一个每当辐射传感器检测到电离事件就通知框架的插件，可能会将其大小设置为零，因为过去的电离事件通常并不重要，只有即时读数才有意义。

大小为 1 适用于电平触发型插件。例如，一个通知框架当前压力传感器数值的插件可能会将其大小保持为 1（默认值），同时持续发送消息；一旦框架侧的插件在该通道注册，它将立即收到最新的数值，而更早的消息将被丢弃。

大于 1 的大小适用于每条消息都很重要的插件。例如，一个自身向另一个已经缓冲了事件的系统注册，并立即转发所有先前缓冲事件的插件，可能希望避免任何消息被丢弃。在这种情况下，选择一个能够避免溢出的大小非常重要。同时还需要考虑框架侧可能永远无法完全初始化的情况（例如，用户启动了应用程序，但很快就终止了它，这段时间足够让插件的平台侧运行，但框架侧却来不及运行）。

## 控制通道

插件可以通过向控制通道 `dev.flutter/channel-buffers`（参见 [kControlChannelName]）发送消息来配置其通道的缓冲区。

可以向该控制通道发送两种消息，分别用于调整缓冲区大小和禁用溢出警告。有关这些消息的详细信息，请参见 [handleMessage]。

### ChannelBuffers()

```dart
ChannelBuffers()
```

为平台消息创建一个缓冲池。

通常不需要创建此类的实例；引擎所使用的是全局的 [channelBuffers] 实例。

### kDefaultBufferSize

```dart
int kDefaultBufferSize
```

通道缓冲区默认存储的消息数量。

### kControlChannelName

```dart
String kControlChannelName
```

插件用于与通道缓冲区系统通信的通道名称。

这些消息由 [handleMessage] 处理。

### push()

```dart
void push(String name, ByteData? data, PlatformMessageResponseCallback callback)
```

将一条消息（`data`）添加到指定名称的通道缓冲区（`name`）中。

`callback` 参数是一个闭包，调用它可以将消息发回给插件。

如果消息导致某个通道溢出，且该通道未被配置为预期会发生溢出，那么在调试模式下，控制台会打印一条溢出警告消息。

通道名称不能包含 U+0000 NULL 字符，因为它们会通过使用以 null 结尾的字符串的 API 传递。

### setListener()

```dart
void setListener(String name, ChannelCallback callback)
```

为指定通道设置监听器。

当存在监听器时，消息会被立即发送。

每个通道一次最多只能设置一个监听器。为已有监听器的通道设置新的监听器会清除之前的监听器。

回调会在其自身的调用栈帧中被调用，并使用注册该回调时所处的 zone。

## 清空缓冲区（Draining）

如果在添加监听器之前有消息已排队等待，这些消息会在此方法返回后异步清空。

每条消息都在其各自的微任务（microtask）中处理。在队列清空期间，插件无法排队新消息，但处理程序自身排队的任何微任务都会在处理下一条消息之前被执行。

如果监听器被移除，清空过程将停止。

### clearListener()

```dart
void clearListener(String name)
```

清除指定通道的监听器。

当没有监听器时，该通道上的消息会被排队，最多可排队 [kDefaultBufferSize] 条（或通过控制通道配置的大小），之后会以先进先出的方式被丢弃。

### sendChannelUpdate()

```dart
void sendChannelUpdate(String name, {required bool listening})
```

### drain()

```dart
Future<void> drain(String name, DrainChannelCallback callback)
```

已弃用。请迁移至 [setListener]。

移除并处理指定通道中所有已存储的消息。

应在通道准备好处理消息时（即在框架中设置好消息处理程序时）调用此方法。

消息通过调用给定的 `callback` 进行处理。每条消息都在其各自的微任务中处理。

### handleMessage()

```dart
void handleMessage(ByteData data)
```

处理一条控制消息。

此方法用于由平台消息调度器调用，将消息从插件转发至 [kControlChannelName] 通道。

消息使用 [StandardMethodCodec] 格式。支持两种方法：`resize` 和 `overflow`。`resize` 方法用于更改缓冲区的大小，`overflow` 方法用于控制是否预期会发生溢出。

## `resize`

`resize` 方法接受一个包含两个值的列表作为参数，第一个是通道名称（一个长度小于 254 字节、不包含任何 null 字节的 UTF-8 字符串），第二个是该通道缓冲区允许的大小（一个介于 0 到 2147483647 之间的整数）。

收到该消息后，通道的缓冲区会被调整大小。如有必要，消息会被静默丢弃，以确保缓冲区大小不超过指定值。

出于历史原因，该消息也可以使用一种特殊格式发送，该格式由一个 UTF-8 编码的字符串组成，其三个部分之间以 U+000D 回车符（CR）分隔，这三个部分分别是字符串 `resize`、通道名称字符串，以及新通道缓冲区大小的十进制字符串。例如：`resize\rchannel\r1`

## `overflow`

`overflow` 方法接受一个包含两个值的列表作为参数，第一个是通道名称（一个长度小于 254 字节、不包含任何 null 字节的 UTF-8 字符串），第二个是一个布尔值，若预期会发生溢出则为 true，否则为 false。

此操作会在调试模式下为该通道设置一个标志。在发布模式下，该消息会被静默忽略。该标志表示此通道上是否预期会发生溢出。当该标志被设置时，消息会被静默丢弃。当该标志被清除时（默认情况），该通道上发生的任何溢出都会导致控制台打印一条警告消息，提示有消息丢失。

### resize()

```dart
void resize(String name, int newSize)
```

更改与给定通道关联的队列的容量。

如果 newSize 小于队列的当前长度，可能会导致消息被丢弃。

此方法预期由特定平台的插件代码调用（通过控制通道间接调用），而非由框架侧的代码调用。参见 [handleMessage]。

从框架代码中调用此方法是多余的，因为框架代码运行时，可以直接订阅相关通道，因此无需任何缓冲。

### allowOverflow()

```dart
void allowOverflow(String name, bool allowed)
```

切换该通道在因溢出而丢弃消息时是否显示警告消息。

此方法预期由特定平台的插件代码调用（通过控制通道间接调用），而非由框架侧的代码调用。参见 [handleMessage]。

从框架代码中调用此方法是多余的，因为框架代码运行时，可以直接订阅相关通道，因此不需要任何消息发生溢出。

此方法在发布（release）构建中不起作用。

# channelBuffers

```dart
ChannelBuffers channelBuffers
```

[ChannelBuffers]，用于在引擎（Engine）和框架（Framework）之间存储消息。通常，无法投递的消息会被存储在这里，直到框架能够处理它们为止。

另请参阅：

- [BinaryMessenger]，[ChannelBuffers] 通常在此处被读取。
