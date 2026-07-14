# KeyEventType

```dart
enum KeyEventType {}
```

按键事件的类型。

按键被按下。

按键被释放。

按键被持续按住，从而产生重复的按键输入。

### label

```dart
String get label
```

# KeyEventDeviceType

```dart
enum KeyEventDeviceType {}
```

按键事件的来源设备。

并非所有平台都能提供准确的类型。

设备是键盘。

设备是类似电视遥控器等设备上的方向键（D-pad）。

设备是游戏手柄按钮。

设备是摇杆按钮。

设备是连接到 HDMI 总线的设备。

### label

```dart
String get label
```

# KeyData

```dart
class KeyData {}
```

关于某次按键事件的信息。

### KeyData()

```dart
KeyData({required Duration timeStamp, required KeyEventType type, required int physical, required int logical, required String? character, required bool synthesized, KeyEventDeviceType deviceType = KeyEventDeviceType.keyboard})
```

创建一个表示按键事件的对象。

### timeStamp

```dart
Duration timeStamp
```

事件分发的时间，相对于任意的时间线。

对于合成（synthesized）事件，[timeStamp] 可能并非按键按下或释放的实际发生时间。

### type

```dart
KeyEventType type
```

该事件的类型。

### deviceType

```dart
KeyEventDeviceType deviceType
```

描述此事件源自哪种类型的设备（键盘、方向键等）。

### physical

```dart
int physical
```

发生变化的物理按键的键码。

### logical

```dart
int logical
```

发生变化的逻辑按键的键码。

### character

```dart
String? character
```

事件对应的字符输入。

对于 up 事件将被忽略。

### synthesized

```dart
bool synthesized
```

如果 [synthesized] 为 true，则表示该事件并非对应于一次原生（native）事件。

尽管 Flutter 的大多数键盘事件都是从原生事件转换而来，但也有一些事件并非基于原生事件，而仅仅是为了符合 Flutter 的按键事件模型（如框架中 `HardwareKeyboard` 类的文档所述）而合成的。

例如，当窗口失去焦点时，某些按键的按下或释放事件可能会丢失。一些平台提供了查询某个按键是否处于按住状态的方法。如果嵌入层（embedder）检测到其内部记录与系统返回的状态之间存在不一致，嵌入层将合成一个相应的事件，以在不破坏事件模型的前提下同步状态。

另一个例子是，macOS 对 CapsLock 的处理方式比较特殊：它会在每次交替按下时，在按下的时刻同时发送按下和释放事件，以表示锁定状态切换的方向，而不是表示物理按键实际的按下或释放状态。macOS 的嵌入层应当通过以下方式使行为标准化：将原生的按下事件转换为一个按下事件，紧接着再跟一个合成的释放事件；同样地，也将原生的释放事件转换为一个按下事件，紧接着再跟一个合成的释放事件。

合成事件不具有可信的 [timeStamp]，不应被当作按键在回调发生的那一刻真正按下或释放来处理。

[KeyRepeatEvent] 永远不会被合成。

### toString()

```dart
String toString()
```

### toStringFull()

```dart
String toStringFull()
```

返回此对象中信息的完整文本描述。
