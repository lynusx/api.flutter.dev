The Flutter Scheduler library.

To use, import `package:flutter/scheduler.dart`.

This library is responsible for scheduler frame callbacks, and tasks at given priorities.

The library makes sure that tasks are only run when appropriate. For example, an idle-task is only executed when no animation is running.
