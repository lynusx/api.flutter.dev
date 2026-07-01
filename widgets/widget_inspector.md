@docImport 'dart:ui';

# ExitWidgetSelectionButtonBuilder

```dart
typedef ExitWidgetSelectionButtonBuilder = Widget Function(BuildContext context, {required VoidCallback onPressed, required String semanticsLabel, required GlobalKey key})
```

Signature for the builder callback used by [WidgetInspector.exitWidgetSelectionButtonBuilder].

# MoveExitWidgetSelectionButtonBuilder

```dart
typedef MoveExitWidgetSelectionButtonBuilder = Widget Function(BuildContext context, {required VoidCallback onPressed, required String semanticsLabel, bool usesDefaultAlignment})
```

Signature for the builder callback used by [WidgetInspector.moveExitWidgetSelectionButtonBuilder].

# TapBehaviorButtonBuilder

```dart
typedef TapBehaviorButtonBuilder = Widget Function(BuildContext context, {required VoidCallback onPressed, required String semanticsLabel, required bool selectionOnTapEnabled})
```

Signature for the builder callback used by [WidgetInspector.tapBehaviorButtonBuilder].

# RegisterServiceExtensionCallback

```dart
typedef RegisterServiceExtensionCallback = void Function({required String name, required ServiceExtensionCallback callback})
```

Signature for a method that registers the service extension `callback` with the given `name`.

Used as argument to [WidgetInspectorService.initServiceExtensions]. The [BindingBase.registerServiceExtension] implements this signature.

# InspectorSelectionChangedCallback

```dart
typedef InspectorSelectionChangedCallback = void Function()
```

Signature for the selection change callback used by [WidgetInspectorService.selectionChangedCallback].

# InspectorReferenceData

```dart
class InspectorReferenceData {}
```

Structure to help reference count Dart objects referenced by a GUI tool using [WidgetInspectorService].

Does not hold the object from garbage collection.

### InspectorReferenceData()

```dart
InspectorReferenceData(Object object, String id)
```

Creates an instance of [InspectorReferenceData].

### id

```dart
String id
```

The id of the object in the widget inspector records.

### count

```dart
int count
```

The number of times the object has been referenced.

### value

```dart
Object? get value
```

The value.

# WidgetInspectorService

```dart
mixin WidgetInspectorService {}
```

Service used by GUI tools to interact with the [WidgetInspector].

Calls to this object are typically made from GUI tools such as the [Flutter IntelliJ Plugin](https://github.com/flutter/flutter-intellij/blob/master/README.md) using the [Dart VM Service](https://github.com/dart-lang/sdk/blob/main/runtime/vm/service/service.md). This class uses its own object id and manages object lifecycles itself instead of depending on the [object ids](https://github.com/dart-lang/sdk/blob/main/runtime/vm/service/service.md#getobject) specified by the VM Service Protocol because the VM Service Protocol ids expire unpredictably. Object references are tracked in groups so that tools that clients can use dereference all objects in a group with a single operation making it easier to avoid memory leaks.

All methods in this class are appropriate to invoke from debugging tools using the VM service protocol to evaluate Dart expressions of the form `WidgetInspectorService.instance.methodName(arg1, arg2, ...)`. If you make changes to any instance method of this class you need to verify that the [Flutter IntelliJ Plugin](https://github.com/flutter/flutter-intellij/blob/master/README.md) widget inspector support still works with the changes.

All methods returning String values return JSON.

Ring of cached JSON values to prevent JSON from being garbage collected before it can be requested over the VM service protocol.

### instance

```dart
WidgetInspectorService get instance
```

The current [WidgetInspectorService].

### isSelectMode

```dart
set isSelectMode(bool enabled)
```

Enables select mode for the Inspector.

In select mode, pointer interactions trigger widget selection instead of normal interactions. Otherwise the previously selected widget is highlighted but the application can be interacted with normally.

### instance

```dart
set instance(WidgetInspectorService instance)
```

### selection

```dart
InspectorSelection selection
```

Ground truth tracking what object(s) are currently selected used by both GUI tools such as the Flutter IntelliJ Plugin and the [WidgetInspector] displayed on the device.

### selectionChangedCallback

```dart
InspectorSelectionChangedCallback? selectionChangedCallback
```

Callback typically registered by the [WidgetInspector] to receive notifications when [selection] changes.

The Flutter IntelliJ Plugin does not need to listen for this event as it instead listens for `dart:developer` `inspect` events which also trigger when the inspection target changes on device.

The VM service protocol does not keep alive object references so this class needs to manually manage groups of objects that should be kept alive.

The pubRootDirectories that are currently configured for the widget inspector.

Memoization for [_isLocalCreationLocation].

### registerServiceExtension()

```dart
void registerServiceExtension({required String name, required ServiceExtensionCallback callback, required RegisterServiceExtensionCallback registerExtension})
```

Registers a service extension method with the given name (full name "ext.flutter.inspector.name").

The given callback is called when the extension method is called. The callback must return a value that can be converted to JSON using `json.encode()` (see [JsonEncoder]). The return value is stored as a property named `result` in the JSON. In case of failure, the failure is reported to the remote caller and is dumped to the logs.

Registers a service extension method with the given name (full name "ext.flutter.inspector.name"), which takes no arguments.

Registers a service extension method with the given name (full name "ext.flutter.inspector.name"), which takes a single optional argument "objectGroup" specifying what group is used to manage lifetimes of object references in the returned JSON (see [disposeGroup]). If "objectGroup" is omitted, the returned JSON will not include any object references to avoid leaking memory.

Registers a service extension method with the given name (full name "ext.flutter.inspector.name"), which takes a single argument "enabled" which can have the value "true" or the value "false" or can be omitted to read the current value. (Any value other than "true" is considered equivalent to "false". Other arguments are ignored.)

Calls the `getter` callback to obtain the value when responding to the service extension method being called.

Calls the `setter` callback with the new value when the service extension method is called with a new value.

Sends an event when a service extension's state is changed.

Clients should listen for this event to stay aware of the current service extension state. Any service extension that manages a state should call this method on state change.

`value` reflects the newly updated service extension value.

This will be called automatically for service extensions registered via [BindingBase.registerBoolServiceExtension].

Registers a service extension method with the given name (full name "ext.flutter.inspector.name") which takes an optional parameter named "arg" and a required parameter named "objectGroup" used to control the lifetimes of object references in the returned JSON (see [disposeGroup]).

Registers a service extension method with the given name (full name "ext.flutter.inspector.name"), that takes arguments "arg0", "arg1", "arg2", ..., "argn".

### forceRebuild()

```dart
Future<void> forceRebuild()
```

Cause the entire tree to be rebuilt. This is used by development tools when the application code has changed and is being hot-reloaded, to cause the widget tree to pick up any changed implementations.

This is expensive and should not be called except during development.

Resets the count of errors since the last hot reload.

This data is sent to clients as part of the 'Flutter.Error' service protocol event. Clients may choose to display errors received after the first error differently.

### isStructuredErrorsEnabled()

```dart
bool isStructuredErrorsEnabled()
```

Whether structured errors are enabled.

Structured errors provide semantic information that can be used by IDEs to enhance the display of errors with rich formatting.

### initServiceExtensions()

```dart
void initServiceExtensions(RegisterServiceExtensionCallback registerExtension)
```

Called to register service extensions.

See also:

- <https://github.com/dart-lang/sdk/blob/main/runtime/vm/service/service.md#rpcs-requests-and-responses>
- [BindingBase.initServiceExtensions], which explains when service extensions can be used.

### disposeAllGroups()

```dart
void disposeAllGroups()
```

Clear all InspectorService object references.

Use this method only for testing to ensure that object references from one test case do not impact other test cases.

### resetAllState()

```dart
void resetAllState()
```

Reset all InspectorService state.

Use this method only for testing to write hermetic tests for WidgetInspectorService.

### disposeGroup()

```dart
void disposeGroup(String name)
```

Free all references to objects in a group.

Objects and their associated ids in the group may be kept alive by references from a different group.

### toId()

```dart
String? toId(Object? object, String groupName)
```

Returns a unique id for [object] that will remain live at least until [disposeGroup] is called on [groupName].

### isWidgetTreeReady()

```dart
bool isWidgetTreeReady([String? groupName])
```

Returns whether the application has rendered its first frame and it is appropriate to display the Widget tree in the inspector.

### toObject()

```dart
Object? toObject(String? id, [String? groupName])
```

Returns the Dart object associated with a reference id.

The `groupName` parameter is not required by is added to regularize the API surface of the methods in this class called from the Flutter IntelliJ Plugin.

### toObjectForSourceLocation()

```dart
Object? toObjectForSourceLocation(String id, [String? groupName])
```

Returns the object to introspect to determine the source location of an object's class.

The Dart object for the id is returned for all cases but [Element] objects where the [Widget] configuring the [Element] is returned instead as the class of the [Widget] is more relevant than the class of the [Element].

The `groupName` parameter is not required by is added to regularize the API surface of methods called from the Flutter IntelliJ Plugin.

### disposeId()

```dart
void disposeId(String? id, String groupName)
```

Remove the object with the specified `id` from the specified object group.

If the object exists in other groups it will remain alive and the object id will remain valid.

### setPubRootDirectories()

```dart
void setPubRootDirectories(List<String> pubRootDirectories)
```

Set the list of directories that should be considered part of the local project.

The local project directories are used to distinguish widgets created by the local project from widgets created from inside the framework or other packages.

### resetPubRootDirectories()

```dart
void resetPubRootDirectories()
```

Resets the list of directories, that should be considered part of the local project, to the value passed in [pubRootDirectories].

The local project directories are used to distinguish widgets created by the local project from widgets created from inside the framework or other packages.

### addPubRootDirectories()

```dart
void addPubRootDirectories(List<String> pubRootDirectories)
```

Add a list of directories that should be considered part of the local project.

The local project directories are used to distinguish widgets created by the local project from widgets created from inside the framework or other packages.

### removePubRootDirectories()

```dart
void removePubRootDirectories(List<String> pubRootDirectories)
```

Remove a list of directories that should no longer be considered part of the local project.

The local project directories are used to distinguish widgets created by the local project from widgets created from inside the framework or other packages.

### pubRootDirectories()

```dart
Future<Map<String, dynamic>> pubRootDirectories(Map<String, String> parameters)
```

Returns the list of directories that should be considered part of the local project.

### setSelectionById()

```dart
bool setSelectionById(String? id, [String? groupName])
```

Set the [WidgetInspector] selection to the object matching the specified id if the object is valid object to set as the inspector selection.

Returns true if the selection was changed.

The `groupName` parameter is not required by is added to regularize the API surface of methods called from the Flutter IntelliJ Plugin.

### setSelection()

```dart
bool setSelection(Object? object, [String? groupName])
```

Set the [WidgetInspector] selection to the specified `object` if it is a valid object to set as the inspector selection.

Returns true if the selection was changed.

The `groupName` parameter is not needed but is specified to regularize the API surface of methods called from the Flutter IntelliJ Plugin.

Notify connected tools (e.g. Flutter DevTools, IDE plugins) that a new widget has been selected.

This method triggers two actions:

1.  It calls [developer.inspect] on the provided [object], making it available for inspection in Flutter DevTools.
2.  It posts a 'navigate' [ToolEvent] with the source code location of the selected widget, allowing IDEs to navigate to the corresponding file and line.

If [restrictToProjectFiles] is true and the selected widget is not from the local project (i.e., it's from the Flutter framework or a package), the 'navigate' event will point to the nearest ancestor widget that is part of the local project.

Changes whether widget selection mode is [enabled].

Returns a DevTools uri linking to a specific element on the inspector page.

### devToolsInspectorUri()

```dart
String devToolsInspectorUri(String inspectorRef)
```

Returns the DevTools inspector uri for the given vm service connection and inspector reference.

### getParentChain()

```dart
String getParentChain(String id, String groupName)
```

Returns JSON representing the chain of [DiagnosticsNode] instances from root of the tree to the [Element] or [RenderObject] matching `id`.

The JSON contains all information required to display a tree view with all nodes other than nodes along the path collapsed.

Memoized version of [_isLocalCreationLocationImpl].

Wrapper around `json.encode` that uses a ring of cached values to prevent the Dart garbage collector from collecting objects between when the value is returned over the VM service protocol and when the separate VM service protocol command has to be used to retrieve its full contents.

### getProperties()

```dart
String getProperties(String diagnosticsNodeId, String groupName)
```

Returns a JSON representation of the properties of the [DiagnosticsNode] object that `diagnosticsNodeId` references.

### getChildren()

```dart
String getChildren(String diagnosticsNodeId, String groupName)
```

Returns a JSON representation of the children of the [DiagnosticsNode] object that `diagnosticsNodeId` references.

### getChildrenSummaryTree()

```dart
String getChildrenSummaryTree(String diagnosticsNodeId, String groupName)
```

Returns a JSON representation of the children of the [DiagnosticsNode] object that `diagnosticsNodeId` references only including children that were created directly by user code.

{@template flutter.widgets.WidgetInspectorService.getChildrenSummaryTree} Requires [Widget] creation locations which are only available for debug mode builds when the `--track-widget-creation` flag is enabled on the call to the `flutter` tool. This flag is enabled by default in debug builds. {@endtemplate}

See also:

- [isWidgetCreationTracked] which indicates whether this method can be used.

### objectToDiagnosticsNode()

```dart
DiagnosticsNode? objectToDiagnosticsNode(Object? object)
```

If possible, returns [DiagnosticsNode] for the object.

### getChildrenDetailsSubtree()

```dart
String getChildrenDetailsSubtree(String diagnosticableId, String groupName)
```

Returns a JSON representation of the children of the [DiagnosticsNode] object that [diagnosticableId] references providing information needed for the details subtree view.

The details subtree shows properties inline and includes all children rather than a filtered set of important children.

Returns a new [InspectorSerializationDelegate] if [node] references either an [EnableWidgetInspectorScope] or [DisableWidgetInspectorScope] and the value of `delegate.inDisableInspectorWidgetScope` is updated.

If [EnableWidgetInspectorScope] is encountered and `delegate.inDisableInspectorWidgetScope` is already false, null is returned.

If [DisableWidgetInspectorScope] is encountered and `delegate.inDisableInspectorWidgetScope` is already true, null is returned.

### getRootWidget()

```dart
String getRootWidget(String groupName)
```

Returns a JSON representation of the [DiagnosticsNode] for the root [Element].

### getRootWidgetSummaryTree()

```dart
String getRootWidgetSummaryTree(String groupName)
```

Returns a JSON representation of the [DiagnosticsNode] for the root [Element] showing only nodes that should be included in a summary tree.

### getDetailsSubtree()

```dart
String getDetailsSubtree(String diagnosticableId, String groupName, {int subtreeDepth = 2})
```

Returns a JSON representation of the subtree rooted at the [DiagnosticsNode] object that `diagnosticsNodeId` references providing information needed for the details subtree view.

The number of levels of the subtree that should be returned is specified by the [subtreeDepth] parameter. This value defaults to 2 for backwards compatibility.

See also:

- [getChildrenDetailsSubtree], a method to get children of a node in the details subtree.

### getSelectedWidget()

```dart
String getSelectedWidget(String? previousSelectionId, String groupName)
```

Returns a [DiagnosticsNode] representing the currently selected [Element].

### screenshot()

```dart
Future<ui.Image?> screenshot(Object? object, {required double width, required double height, double margin = 0.0, double maxPixelRatio = 1.0, bool debugPaint = false})
```

Captures an image of the current state of an [object] that is a [RenderObject] or [Element].

The returned [ui.Image] has uncompressed raw RGBA bytes and will be scaled to be at most [width] pixels wide and [height] pixels tall. The returned image will never have a scale between logical pixels and the size of the output image larger than maxPixelRatio. [margin] indicates the number of pixels relative to the un-scaled size of the [object] to include as a margin to include around the bounds of the [object] in the screenshot. Including a margin can be useful to capture areas that are slightly outside of the normal bounds of an object such as some debug paint information.

### getSelectedSummaryWidget()

```dart
String getSelectedSummaryWidget(String? previousSelectionId, String groupName)
```

Returns a [DiagnosticsNode] representing the currently selected [Element] if the selected [Element] should be shown in the summary tree otherwise returns the first ancestor of the selected [Element] shown in the summary tree.

Returns the creation location of the currently selected widget.

If [restrictToSummaryTree] is true and the currently selected widget is not in the summary tree (i.e. not created by the current project), this method will instead return the location of its nearest ancestor widget that is in the summary tree.

### isWidgetCreationTracked()

```dart
bool isWidgetCreationTracked()
```

Returns whether [Widget] creation locations are available.

{@macro flutter.widgets.WidgetInspectorService.getChildrenSummaryTree}

### postEvent()

```dart
void postEvent(String eventKind, Map<Object, Object?> eventData, {String stream = 'Extension'})
```

All events dispatched by a [WidgetInspectorService] use this method instead of calling [developer.postEvent] directly.

This allows tests for [WidgetInspectorService] to track which events were dispatched by overriding this method.

### inspect()

```dart
void inspect(Object? object)
```

All events dispatched by a [WidgetInspectorService] use this method instead of calling [developer.inspect].

This allows tests for [WidgetInspectorService] to track which events were dispatched by overriding this method.

### performReassemble()

```dart
void performReassemble()
```

This method is called by [WidgetsBinding.performReassemble] to flush caches of obsolete values after a hot reload.

Do not call this method directly. Instead, use [BindingBase.reassembleApplication].

Safely get the render object of an [Element].

If the element is not yet mounted, the result will be null.

# WidgetInspector

```dart
class WidgetInspector extends StatefulWidget {}
```

A widget that enables inspecting the child widget's structure.

Select a location on your device or emulator and view what widgets and render object that best matches the location. An outline of the selected widget and terse summary information is shown on device with detailed information is shown in Flutter DevTools.

The inspector has a select mode and a view mode.

In the select mode, tapping the device selects the widget that best matches the location of the touch and switches to view mode. Dragging a finger on the device selects the widget under the drag location but does not switch modes. Touching the very edge of the bounding box of a widget triggers selecting the widget even if another widget that also overlaps that location would otherwise have priority.

In the view mode, the previously selected widget is outlined, however, touching the device has the same effect it would have if the inspector wasn't present. This allows interacting with the application and viewing how the selected widget changes position. Clicking on the select icon in the bottom left corner of the application switches back to select mode.

### WidgetInspector()

```dart
WidgetInspector({dynamic key, required Widget child, required TapBehaviorButtonBuilder? tapBehaviorButtonBuilder, required ExitWidgetSelectionButtonBuilder? exitWidgetSelectionButtonBuilder, required MoveExitWidgetSelectionButtonBuilder? moveExitWidgetSelectionButtonBuilder})
```

Creates a widget that enables inspection for the child.

### child

```dart
Widget child
```

The widget that is being inspected.

### exitWidgetSelectionButtonBuilder

```dart
ExitWidgetSelectionButtonBuilder? exitWidgetSelectionButtonBuilder
```

A builder that is called to create the exit select-mode button.

The `onPressed` callback and key passed as arguments to the builder should be hooked up to the returned widget.

### moveExitWidgetSelectionButtonBuilder

```dart
MoveExitWidgetSelectionButtonBuilder? moveExitWidgetSelectionButtonBuilder
```

A builder that is called to create the button that moves the exit select- mode button to the right or left.

The `onPressed` callback passed as an argument to the builder should be hooked up to the returned widget.

The button UI should respond to the `leftAligned` argument.

### tapBehaviorButtonBuilder

```dart
TapBehaviorButtonBuilder? tapBehaviorButtonBuilder
```

A builder that is called to create the button that changes the default tap behavior when Select Widget mode is enabled.

The `onPressed` callback passed as an argument to the builder should be hooked up to the returned widget.

The button UI should respond to the `selectionOnTapEnabled` argument.

### createState()

```dart
State<WidgetInspector> createState()
```

# EnableWidgetInspectorScope

```dart
class EnableWidgetInspectorScope extends ProxyWidget {}
```

Enables the Flutter DevTools Widget Inspector for a [Widget] subtree.

The widget inspector is enabled by default, so this widget is only useful if it is a descendant of [DisableWidgetInspectorScope] in the widget tree.

See also:

- [DisableWidgetInspectorScope], the widget used to disable the inspector for a widget subtree.
- [WidgetInspector], the widget used to provide inspector support for a widget subtree.

### EnableWidgetInspectorScope()

```dart
EnableWidgetInspectorScope({dynamic key, required Widget child})
```

Enables the Flutter DevTools Widget Inspector for the [Widget] subtree rooted at [child].

### createElement()

```dart
Element createElement()
```

# DisableWidgetInspectorScope

```dart
class DisableWidgetInspectorScope extends ProxyWidget {}
```

Disables the Flutter DevTools Widget Inspector for a [Widget] subtree.

This is useful for hiding implementation details of widgets in contexts where the additional information may be confusing to end users. For example, a widget previewer may display multiple previews of user defined widgets and decide to only display the user defined widgets in the inspector while hiding the scaffolding used to host the widgets in the previewer.

See also:

- [EnableWidgetInspectorScope], the widget used to enable the inspector for a widget subtree.
- [WidgetInspector], the widget used to provide inspector support for a widget subtree.

### DisableWidgetInspectorScope()

```dart
DisableWidgetInspectorScope({dynamic key, required Widget child})
```

Disables the Flutter DevTools Widget Inspector for the [Widget] subtree rooted at [child].

### createElement()

```dart
Element createElement()
```

# InspectorButtonVariant

```dart
enum InspectorButtonVariant {}
```

Defines the visual and behavioral variants for an [InspectorButton].

A standard button with a filled background and foreground icon.

A button that can be toggled on or off, visually representing its state.

The [InspectorButton.toggledOn] property determines its current state.

A button that displays only an icon, typically with a transparent background.

# InspectorButton

```dart
abstract class InspectorButton extends StatelessWidget {}
```

An abstract base class for creating Material or Cupertino-styled inspector buttons.

Subclasses are responsible for implementing the design-specific rendering logic in the [build] method and providing design-specific colors via [foregroundColor] and [backgroundColor].

### InspectorButton()

```dart
InspectorButton({dynamic key, required VoidCallback onPressed, required String semanticsLabel, required IconData icon, GlobalKey? buttonKey, required InspectorButtonVariant variant, bool? toggledOn})
```

Creates an inspector button.

This is the base constructor used by named constructors.

### InspectorButton.filled()

```dart
InspectorButton.filled({dynamic key, required VoidCallback onPressed, required String semanticsLabel, required IconData icon, GlobalKey? buttonKey})
```

Creates an inspector button with the [InspectorButtonVariant.filled] style.

This button typically has a solid background color and a contrasting icon.

### InspectorButton.toggle()

```dart
InspectorButton.toggle({dynamic key, required VoidCallback onPressed, required String semanticsLabel, required IconData icon, bool? toggledOn = true})
```

Creates an inspector button with the [InspectorButtonVariant.toggle] style.

This button can be in an "on" or "off" state, visually indicated. The [toggledOn] parameter defaults to `true`.

### InspectorButton.iconOnly()

```dart
InspectorButton.iconOnly({dynamic key, required VoidCallback onPressed, required String semanticsLabel, required IconData icon})
```

Creates an inspector button with the [InspectorButtonVariant.iconOnly] style.

This button typically displays only an icon with a transparent background.

### onPressed

```dart
VoidCallback onPressed
```

The callback that is called when the button is tapped.

### semanticsLabel

```dart
String semanticsLabel
```

The semantic label for the button, used for accessibility.

### icon

```dart
IconData icon
```

The icon to display within the button.

### buttonKey

```dart
GlobalKey? buttonKey
```

An optional key to identify the button widget.

### variant

```dart
InspectorButtonVariant variant
```

The visual and behavioral variant of the button.

See [InspectorButtonVariant] for available styles.

### toggledOn

```dart
bool? toggledOn
```

For [InspectorButtonVariant.toggle] buttons, this determines if the button is currently in the "on" (true) or "off" (false) state.

### buttonSize

```dart
double buttonSize
```

The standard height and width for the button.

### buttonIconSize

```dart
double buttonIconSize
```

The standard size for the icon when it's not the only element (e.g., in filled or toggle buttons).

For [InspectorButtonVariant.iconOnly], the icon typically takes up the full [buttonSize].

### iconSizeForVariant

```dart
double get iconSizeForVariant
```

Gets the appropriate icon size based on the button's [variant].

Returns [buttonSize] if the variant is [InspectorButtonVariant.iconOnly], otherwise returns [buttonIconSize].

### foregroundColor()

```dart
Color foregroundColor(BuildContext context)
```

Provides the appropriate foreground color for the button's icon.

### backgroundColor()

```dart
Color backgroundColor(BuildContext context)
```

Provides the appropriate background color for the button.

### build()

```dart
Widget build(BuildContext context)
```

# InspectorSelection

```dart
class InspectorSelection with ChangeNotifier {}
```

Mutable selection state of the inspector.

### InspectorSelection()

```dart
InspectorSelection()
```

Creates an instance of [InspectorSelection].

### candidates

```dart
List<RenderObject> get candidates
```

Render objects that are candidates to be selected.

Tools may wish to iterate through the list of candidates.

### candidates

```dart
set candidates(List<RenderObject> value)
```

### index

```dart
int get index
```

Index within the list of candidates that is currently selected.

### index

```dart
set index(int value)
```

### clear()

```dart
void clear()
```

Set the selection to empty.

### clearCandidates()

```dart
void clearCandidates()
```

Clears [candidates] without changing [current] or [currentElement].

Used when the selection is updated from DevTools or another tool so stale on-device hit-test candidates are not drawn on the overlay.

### current

```dart
RenderObject? get current
```

Selected render object typically from the [candidates] list.

Setting [candidates] or calling [clear] resets the selection.

Returns null if the selection is invalid.

### current

```dart
set current(RenderObject? value)
```

### currentElement

```dart
Element? get currentElement
```

Selected [Element] consistent with the [current] selected [RenderObject].

Setting [candidates] or calling [clear] resets the selection.

Returns null if the selection is invalid.

### currentElement

```dart
set currentElement(Element? element)
```

### active

```dart
bool get active
```

Whether the selected render object is attached to the tree or has gone out of scope.

# debugTransformDebugCreator()

```dart
Iterable<DiagnosticsNode> debugTransformDebugCreator(Iterable<DiagnosticsNode> properties)
```

Transformer to parse and gather information about [DiagnosticsDebugCreator].

This function will be registered to [FlutterErrorDetails.propertiesTransformers] in [WidgetsBinding.initInstances].

This is meant to be called only in debug mode. In other modes, it yields an empty list.

# DevToolsDeepLinkProperty

```dart
class DevToolsDeepLinkProperty extends DiagnosticsProperty<String> {}
```

Debugging message for DevTools deep links.

The [value] for this property is a string representation of the Flutter DevTools url.

### DevToolsDeepLinkProperty()

```dart
DevToolsDeepLinkProperty(String description, String url)
```

Creates a diagnostics property that displays a deep link to Flutter DevTools.

The [value] of this property will return a map of data for the Flutter DevTools deep link, including the full `url`, the Flutter DevTools `screenId`, and the `objectId` in Flutter DevTools that this diagnostic references.

# debugIsLocalCreationLocation()

```dart
bool debugIsLocalCreationLocation(Object object)
```

Returns if an object is user created.

This always returns false if it is not called in debug mode.

{@macro flutter.widgets.WidgetInspectorService.getChildrenSummaryTree}

Currently is local creation locations are only available for [Widget] and [Element].

# debugIsWidgetLocalCreation()

```dart
bool debugIsWidgetLocalCreation(Widget widget)
```

Returns true if a [Widget] is user created.

This is a faster variant of `debugIsLocalCreationLocation` that is available in debug and profile builds but only works for [Widget].

# InspectorSerializationDelegate

```dart
class InspectorSerializationDelegate implements DiagnosticsSerializationDelegate {}
```

A delegate that configures how a hierarchy of [DiagnosticsNode]s are serialized by the Flutter Inspector.

### InspectorSerializationDelegate()

```dart
InspectorSerializationDelegate({String? groupName, bool summaryTree = false, int maxDescendantsTruncatableNode = -1, bool expandPropertyValues = true, int subtreeDepth = 1, bool includeProperties = false, required WidgetInspectorService service, Map<String, Object>? Function(DiagnosticsNode, InspectorSerializationDelegate)? addAdditionalPropertiesCallback, bool inDisableWidgetInspectorScope = false})
```

Creates an [InspectorSerializationDelegate] that serialize [DiagnosticsNode] for Flutter Inspector service.

### service

```dart
WidgetInspectorService service
```

Service used by GUI tools to interact with the [WidgetInspector].

### groupName

```dart
String? groupName
```

Optional [groupName] parameter which indicates that the json should contain live object ids.

Object ids returned as part of the json will remain live at least until [WidgetInspectorService.disposeGroup()] is called on [groupName].

### summaryTree

```dart
bool summaryTree
```

Whether the tree should only include nodes created by the local project.

### maxDescendantsTruncatableNode

```dart
int maxDescendantsTruncatableNode
```

Maximum descendants of [DiagnosticsNode] before truncating.

### includeProperties

```dart
bool includeProperties
```

### subtreeDepth

```dart
int subtreeDepth
```

### expandPropertyValues

```dart
bool expandPropertyValues
```

### inDisableWidgetInspectorScope

```dart
bool inDisableWidgetInspectorScope
```

If true, tree nodes will not be reported in responses until an EnableWidgetInspectorScope is encountered.

### addAdditionalPropertiesCallback

```dart
Map<String, Object>? Function(DiagnosticsNode, InspectorSerializationDelegate)? addAdditionalPropertiesCallback
```

Callback to add additional experimental serialization properties.

This callback can be used to customize the serialization of DiagnosticsNode objects for experimental features in widget inspector clients such as [Dart DevTools](https://github.com/flutter/devtools).

### additionalNodeProperties()

```dart
Map<String, Object?> additionalNodeProperties(DiagnosticsNode node, {bool fullDetails = true})
```

### delegateForNode()

```dart
DiagnosticsSerializationDelegate delegateForNode(DiagnosticsNode node)
```

### filterChildren()

```dart
List<DiagnosticsNode> filterChildren(List<DiagnosticsNode> nodes, DiagnosticsNode owner)
```

### filterProperties()

```dart
List<DiagnosticsNode> filterProperties(List<DiagnosticsNode> nodes, DiagnosticsNode owner)
```

### truncateNodesList()

```dart
List<DiagnosticsNode> truncateNodesList(List<DiagnosticsNode> nodes, DiagnosticsNode? owner)
```

### copyWith()

```dart
InspectorSerializationDelegate copyWith({int? subtreeDepth, bool? includeProperties, bool? expandPropertyValues, bool? inDisableWidgetInspectorScope})
```

# widgetFactory

```dart
_WidgetFactory widgetFactory
```

Annotation which marks a function as a widget factory for the purpose of widget creation tracking.

When widget creation tracking is enabled, the framework tracks the source code location of the constructor call for each widget instance. This information is used by the DevTools to provide an improved developer experience. For example, it allows the Flutter inspector to present the widget tree in a manner similar to how the UI was defined in your source code.

[Widget] constructors are automatically instrumented to track the source code location of constructor calls. However, there are cases where a function acts as a sort of a constructor for a widget and a call to such a function should be considered as the creation location for the returned widget instance.

Annotating a function with this annotation marks the function as a widget factory. The framework will then instrument that function in the same way as it does for [Widget] constructors.

Tracking will not work correctly if the function has optional positional parameters.

Currently this annotation is only supported on extension methods.

{@tool snippet}

This example shows how to use the [widgetFactory] annotation to mark an extension method as a widget factory:

```dart
extension PaddingModifier on Widget {
  @widgetFactory
  Widget padding(EdgeInsetsGeometry padding) {
    return Padding(padding: padding, child: this);
  }
}
```

When using the above extension method, the framework will track the creation location of the [Padding] widget instance as the source code location where the `padding` extension method was called:

```dart
// continuing from previous example...
const Text('Hello World!')
    .padding(const EdgeInsets.all(8));
```

{@end-tool}

See also:

- the documentation for [Track widget creation](https://flutter.dev/to/track-widget-creation).

# WeakMap

```dart
class WeakMap<K, V> {}
```

Does not hold keys from garbage collection.

### operator []()

```dart
V? operator [](K key)
```

Returns the value for the given [key] or null if [key] is not in the map or garbage collected.

Does not support records to act as keys.

### operator []=()

```dart
void operator []=(K key, V value)
```

Associates the [key] with the given [value].

### remove()

```dart
V? remove(K key)
```

Removes the value for the given [key] from the map.

### clear()

```dart
void clear()
```

Removes all pairs from the map.
