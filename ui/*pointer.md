# PointerChange

```dart
enum PointerChange {}
```

自上次报告以来指针发生的变化。

来自该指针的输入不再指向此接收方。

设备已开始跟踪该指针。

例如，指针可能悬停在设备上方，但尚未接触设备表面。

设备不再跟踪该指针。

例如，指针可能已漂移出设备的悬停检测范围，或已与系统完全断开连接。

指针在未接触设备的情况下相对于设备发生了移动。

指针已接触设备。

指针在接触设备的情况下相对于设备发生了移动。

指针已停止接触设备。

该指针上已开始一次平移/缩放操作。

此类事件的 kind 始终为 [PointerDeviceKind.trackpad]。

该指针上的平移/缩放操作已更新。

此类事件的 kind 始终为 [PointerDeviceKind.trackpad]。

该指针上的平移/缩放操作已结束。

此类事件的 kind 始终为 [PointerDeviceKind.trackpad]。

# PointerDeviceKind

```dart
enum PointerDeviceKind {}
```

指针设备的类型。

基于触摸的指针设备。

最常见的情况是触摸屏。

当用户在 iOS 上使用触控板操作时，如果 `Info.plist` 中未设置 `UIApplicationSupportsIndirectInputEvents` 或该值返回 NO，点击操作也会派发 kind 为 [touch] 的事件。

另请参阅：

- [UIApplicationSupportsIndirectInputEvents](https://developer.apple.com/documentation/bundleresources/information_property_list/uiapplicationsupportsindirectinputevents?language=objc)。

基于鼠标的指针设备。

最常见的情况是桌面端或 Web 端的鼠标。

当用户在 iOS 上使用触控板操作时，移动指针光标也会派发 kind 为 [mouse] 的事件；如果 `Info.plist` 中未设置 `UIApplicationSupportsIndirectInputEvents` 或该值返回 NO，点击操作也会派发 kind 为 [mouse] 的事件。

另请参阅：

- [UIApplicationSupportsIndirectInputEvents](https://developer.apple.com/documentation/bundleresources/information_property_list/uiapplicationsupportsindirectinputevents?language=objc)。

带触控笔的指针设备。

已反转（倒置）的触控笔指针设备。

来自触控板的手势。

此处的触控板定义为一种基于触摸、且具有间接操作表面的指针设备（用户通过触摸非屏幕区域来操作屏幕）。

当用户在物理触控板上做出缩放、平移、滚动或旋转手势时，支持的平台会派发 kind 为 [trackpad] 的事件。

kind 为 [trackpad] 的事件的 [PointerChange] 只能是 `add`、`remove` 以及与平移缩放相关的值。

部分平台不支持（或未完全支持）触控板手势，可能会将触控板手势转换为模拟拖动的伪指针事件。这些事件通常的 kind 为 [touch] 或 [mouse] 而非 [trackpad]。这包括（但不限于）Web 端，以及 `Info.plist` 中未设置 `UIApplicationSupportsIndirectInputEvents` 或该值返回 NO 时的 iOS。

移动指针光标或使用触控板点击通常会触发 [touch] 或 [mouse] 事件，但绝不会触发 [trackpad] 事件。

另请参阅：

- [UIApplicationSupportsIndirectInputEvents](https://developer.apple.com/documentation/bundleresources/information_property_list/uiapplicationsupportsindirectinputevents?language=objc)。

未知的指针设备。

# PointerSignalKind

```dart
enum PointerSignalKind {}
```

指针信号事件的类型。

该事件与指针信号无关。

指针产生的滚动事件（例如鼠标滚轮或触控板滚动）。

指针产生的滚动惯性取消事件。

指针产生的缩放事件（例如触控板双指捏合）。

未知的指针信号类型。

# PointerDataRespondCallback

```dart
typedef PointerDataRespondCallback = void Function({bool allowPlatformDefault})
```

实现 [PointerData.respond] 方法的函数。

# PointerData

```dart
class PointerData {}
```

有关指针状态的信息。

### PointerData()

```dart
PointerData({int viewId = 0, int embedderId = 0, Duration timeStamp = Duration.zero, PointerChange change = PointerChange.cancel, PointerDeviceKind kind = PointerDeviceKind.touch, PointerSignalKind? signalKind, int device = 0, int pointerIdentifier = 0, double physicalX = 0.0, double physicalY = 0.0, double physicalDeltaX = 0.0, double physicalDeltaY = 0.0, int buttons = 0, bool obscured = false, bool synthesized = false, double pressure = 0.0, double pressureMin = 0.0, double pressureMax = 0.0, double distance = 0.0, double distanceMax = 0.0, double size = 0.0, double radiusMajor = 0.0, double radiusMinor = 0.0, double radiusMin = 0.0, double radiusMax = 0.0, double orientation = 0.0, double tilt = 0.0, int platformData = 0, double scrollDeltaX = 0.0, double scrollDeltaY = 0.0, double panX = 0.0, double panY = 0.0, double panDeltaX = 0.0, double panDeltaY = 0.0, double scale = 0.0, double rotation = 0.0, PointerDataRespondCallback? onRespond})
```

创建一个表示指针状态的对象。

### viewId

```dart
int viewId
```

此 [PointerEvent] 所源自的 [FlutterView] 的 ID。

### embedderId

```dart
int embedderId
```

将 [PointerEvent] 与创建它的嵌入端事件相关联的唯一标识符。

任意两个指针事件都不会拥有相同的 [embedderId]。这与用于命中测试的 [pointerIdentifier] 不同，[embedderId] 用于标识平台事件。

### timeStamp

```dart
Duration timeStamp
```

事件派发的时间，相对于某个任意时间线。

### change

```dart
PointerChange change
```

自上次报告以来指针发生的变化。

### kind

```dart
PointerDeviceKind kind
```

产生该事件的输入设备类型。

### signalKind

```dart
PointerSignalKind? signalKind
```

指针信号事件的信号类型。

### device

```dart
int device
```

指针设备的唯一标识符，在多次交互中保持复用。

### pointerIdentifier

```dart
int pointerIdentifier
```

指针的唯一标识符。

该字段在每次新的指针按下事件中都会发生变化。框架使用此标识符来确定命中测试结果。

### physicalX

```dart
double physicalX
```

指针在全局坐标空间中的位置的 X 坐标，以物理像素为单位。

### physicalY

```dart
double physicalY
```

指针在全局坐标空间中的位置的 Y 坐标，以物理像素为单位。

### physicalDeltaX

```dart
double physicalDeltaX
```

指针在 X 坐标上移动的距离，以物理像素为单位。

### physicalDeltaY

```dart
double physicalDeltaY
```

指针在 Y 坐标上移动的距离，以物理像素为单位。

### buttons

```dart
int buttons
```

使用 \*Button 常量（primaryMouseButton、secondaryStylusButton 等）表示的位字段。例如，如果该值为 6，且 [kind] 为 [PointerDeviceKind.invertedStylus]，则表示这是一支倒置的触控笔，且其主按钮和次按钮均处于按下状态。

### obscured

```dart
bool obscured
```

若来自不同安全域的应用以任何方式遮挡了本应用的窗口，则设置此项。（此为预期功能，目前尚未实现。）

### synthesized

```dart
bool synthesized
```

若此指针数据是由指针数据包转换器合成的，则设置此项。当指针数据包转换器接收到的输入序列不合法时，会合成额外的指针数据。

例如，如果转换器在指针尚未按下的情况下收到一个移动指针数据，则会合成一个按下指针数据。

### pressure

```dart
double pressure
```

触摸的压力值，取值范围从 0.0（表示没有可感知压力的触摸）到 1.0（表示"正常"压力的触摸），也可能超过 1.0，表示更强的触摸。对于不检测压力的设备（例如鼠标），返回 1.0。

### pressureMin

```dart
double pressureMin
```

该指针 [pressure] 可返回的最小值。对于不检测压力的设备（例如鼠标），返回 1.0。此值始终小于或等于 1.0。

### pressureMax

```dart
double pressureMax
```

该指针 [pressure] 可返回的最大值。对于不检测压力的设备（例如鼠标），返回 1.0。此值始终大于或等于 1.0。

### distance

```dart
double distance
```

检测到的对象与输入表面之间的距离（例如触控笔或手指与触摸屏之间的距离），单位为任意（不一定线性）的相对单位。若指针已按下，则根据定义此值为 0.0。

### distanceMax

```dart
double distanceMax
```

该指针 distance 可返回的最大值。如果此输入设备无法检测"悬停触摸"输入事件，则此值为 0.0。

### size

```dart
double size
```

屏幕被按压区域的面积，缩放为 0 到 1 之间的值。size 的值可用于判定粗大触摸事件。此值仅在 Android 上设置，是设备特定的近似值，取值范围为可检测值的范围。例如，0.1 可能表示指尖触摸，0.2 表示整个手指的触摸，0.3 表示整个手掌的触摸。

### radiusMajor

```dart
double radiusMajor
```

接触椭圆沿主轴方向的半径，以逻辑像素为单位。

### radiusMinor

```dart
double radiusMinor
```

接触椭圆沿次轴方向的半径，以逻辑像素为单位。

### radiusMin

```dart
double radiusMin
```

该指针的 radiusMajor 和 radiusMinor 可报告的最小值，以逻辑像素为单位。

### radiusMax

```dart
double radiusMax
```

该指针的 radiusMajor 和 radiusMinor 可报告的最小值，以逻辑像素为单位。

### orientation

```dart
double orientation
```

对于 PointerDeviceKind.touch 事件：

接触椭圆的角度，以弧度表示，范围为：

-pi/2 < orientation <= pi/2

……表示椭圆长轴与 y 轴的夹角（负角度表示沿左上/右下对角线方向的朝向，正角度表示沿右上/左下对角线方向的朝向，零则表示与 y 轴平行）。

对于 PointerDeviceKind.stylus 和 PointerDeviceKind.invertedStylus 事件：

触控笔的角度，以弧度表示，范围为：

-pi < orientation <= pi

……表示触控笔投影到输入表面上的轴线，相对于该表面正 y 轴的角度（因此 0.0 表示若将触控笔投影到该表面上，会从接触点垂直向上沿正 y 轴方向延伸；pi 表示触控笔会沿负 y 轴方向向下延伸；pi/4 表示触控笔向右上方延伸；-pi/2 表示触控笔指向左侧，依此类推）。

### tilt

```dart
double tilt
```

对于 PointerDeviceKind.stylus 和 PointerDeviceKind.invertedStylus 事件：

触控笔的倾斜角度，以弧度表示，范围为：

0 <= tilt <= pi/2

……表示触控笔轴线相对于输入表面法线的夹角（因此 0.0 表示触控笔与输入表面正交，而 pi/2 表示触控笔平放在该表面上）。

### platformData

```dart
int platformData
```

与事件关联的平台特定不透明数据。

### scrollDeltaX

```dart
double scrollDeltaX
```

对于 signalKind 为 PointerSignalKind.scroll 的事件：

X 方向上要滚动的量，以物理像素为单位。

### scrollDeltaY

```dart
double scrollDeltaY
```

对于 signalKind 为 PointerSignalKind.scroll 的事件：

Y 方向上要滚动的量，以物理像素为单位。

### panX

```dart
double panX
```

对于 change 为 PointerChange.panZoomUpdate 的事件：

平移/缩放操作在 X 方向上的当前平移幅度，以物理像素为单位。

### panY

```dart
double panY
```

对于 change 为 PointerChange.panZoomUpdate 的事件：

平移/缩放操作在 Y 方向上的当前平移幅度，以物理像素为单位。

### panDeltaX

```dart
double panDeltaX
```

对于 change 为 PointerChange.panZoomUpdate 的事件：

自上一个 panZoomUpdate 事件以来，平移/缩放操作在 X 方向上的平移差值，以物理像素为单位。

### panDeltaY

```dart
double panDeltaY
```

对于 change 为 PointerChange.panZoomUpdate 的事件：

自上一个 panZoomUpdate 事件以来，平移/缩放操作在 Y 方向上的平移差值，以物理像素为单位。

### scale

```dart
double scale
```

对于 change 为 PointerChange.panZoomUpdate 的事件：

平移/缩放操作的当前缩放比例（无单位），初始缩放比例为 1.0。

### rotation

```dart
double rotation
```

对于 change 为 PointerChange.panZoomUpdate 的事件：

平移/缩放操作的当前旋转角度，以弧度表示，初始角度为 0.0。

### respond()

```dart
void respond({required bool allowPlatformDefault})
```

框架/应用可调用此方法，以响应触发此 [PointerData] 的原生事件。

参数 [allowPlatformDefault] 设置为 `true` 时，允许平台执行与该原生事件关联的默认操作。

此方法可被调用任意次数，但一旦 `allowPlatformDefault` 被设置为 `true`，就不能再将其设回 `false`。

如果 `allowPlatformDefault` 从未被设置为 `true`，Flutter 引擎将消费该事件，使其不会被平台看到。在 Web 端，这意味着在触发该 `PointerData` 的 DOM 事件上会调用 `preventDefault`。参见 [Event: preventDefault() method in MDN][EpDmiMDN]。

此方法的具体实现由 [PointerData] 构造函数的 `onRespond` 参数配置。

另请参阅 [PointerDataRespondCallback]。

[EpDmiMDN]: https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault

### toString()

```dart
String toString()
```

### toStringFull()

```dart
String toStringFull()
```

返回描述此对象中信息的完整文本。

# PointerDataPacket

```dart
class PointerDataPacket {}
```

关于指针状态的一系列报告。

### PointerDataPacket()

```dart
PointerDataPacket({List<PointerData> data = const <PointerData>[]})
```

创建一个指针数据报告的数据包。

### data

```dart
List<PointerData> data
```

此数据包中各个指针的相关数据。

此列表可能包含同一指针的多条数据。
