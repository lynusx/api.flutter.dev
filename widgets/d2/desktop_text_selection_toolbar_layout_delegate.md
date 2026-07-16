@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

@docImport 'text_selection_toolbar_layout_delegate.dart';

# DesktopTextSelectionToolbarLayoutDelegate

```dart
class DesktopTextSelectionToolbarLayoutDelegate extends SingleChildLayoutDelegate {}
```

如果工具栏能够放得下，则将其定位在 [anchor] 处；否则将其移动，使其完全适应屏幕。

另请参阅：

- [desktopTextSelectionControls]，它使用此委托来定位自身。
- [cupertinoDesktopTextSelectionControls]，它使用此委托来定位自身。
- [TextSelectionToolbarLayoutDelegate](https://www.yuque.com/thyname/flutter.widgets/textselectiontoolbarlayoutdelegate)，它为移动端文本选择工具栏执行类似的布局。

### DesktopTextSelectionToolbarLayoutDelegate()

```dart
DesktopTextSelectionToolbarLayoutDelegate({required Offset anchor})
```

创建一个 TextSelectionToolbarLayoutDelegate 实例。

### anchor

```dart
Offset anchor
```

渲染菜单的位置点（如果可行）。

应以本地坐标（local coordinates）提供。

### getConstraintsForChild()

```dart
BoxConstraints getConstraintsForChild(BoxConstraints constraints)
```

### getPositionForChild()

```dart
Offset getPositionForChild(Size size, Size childSize)
```

### shouldRelayout()

```dart
bool shouldRelayout(DesktopTextSelectionToolbarLayoutDelegate oldDelegate)
```
