Flutter 调度器（Scheduler）库。

要使用此库，请导入 `package:flutter/scheduler.dart`。

此库负责调度帧回调，以及按给定优先级调度任务。

该库确保任务只在适当的时候运行。例如，空闲任务（idle-task）只有在没有动画运行时才会执行。
