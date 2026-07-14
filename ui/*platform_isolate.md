# runOnPlatformThread()

```dart
Future<R> runOnPlatformThread<R>(FutureOr<R> Function() computation)
```

在平台线程上运行 [computation] 并返回结果。

此方法可能会在单独的 isolate 中运行该计算。该 isolate 将被复用于后续的 [runOnPlatformThread](https://www.yuque.com/thyname/dart.ui/runonplatformthread) 调用，这意味着该 isolate 中的全局状态会在多次调用之间保持不变。

[computation] 及其捕获的任何状态都可能被发送到该 isolate。有关可发送类型的信息，请参阅 [SendPort.send]。

如果 [computation] 是异步的（返回 `Future<R>`），则该 future 会在新的 isolate 中被等待，待整个异步计算完成后再返回结果。

如果 [computation] 抛出异常，此函数返回的 `Future` 将以该错误结束。

[computation] 函数及其结果（或错误）必须可在 isolate 之间发送。无法发送的对象包括已打开的文件和套接字（详见 [SendPort.send]）。

此方法只能从主 isolate 调用。

此 API 目前处于实验阶段。

# isRunningOnPlatformThread

```dart
bool isRunningOnPlatformThread
```

判断当前 isolate 是否正在平台线程上运行。
