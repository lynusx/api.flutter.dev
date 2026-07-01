@docImport 'binding.dart';

# SchedulerServiceExtensions

```dart
enum SchedulerServiceExtensions {}
```

Service extension constants for the scheduler library.

These constants will be used when registering service extensions in the framework, and they will also be used by tools and services that call these service extensions.

The String value for each of these extension names should be accessed by calling the `.name` property on the enum value.

Name of service extension that, when called, will change the value of [timeDilation], which determines the factor by which to slow down animations for help in development.

See also:

- [timeDilation], which is the field that this service extension exposes.
- [SchedulerBinding.initServiceExtensions], where the service extension is registered.
