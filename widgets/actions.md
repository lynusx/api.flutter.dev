@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

@docImport 'app.dart'; @docImport 'routes.dart'; @docImport 'text_editing_intents.dart';

# Intent

```dart
abstract class Intent with Diagnosticable {}
```

An abstract class representing a particular configuration of an [Action].

This class is what the [Shortcuts.shortcuts] map has as values, and is used by an [ActionDispatcher] to look up an action and invoke it, giving it this object to extract configuration information from.

See also:

- [Shortcuts], a widget used to bind key combinations to [Intent]s.
- [Actions], a widget used to map [Intent]s to [Action]s.
- [Actions.invoke], which invokes the action associated with a specified [Intent] using the [Actions] widget that most tightly encloses the given [BuildContext].

### Intent()

```dart
Intent()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### doNothing

```dart
DoNothingIntent doNothing
```

An intent that is mapped to a [DoNothingAction], which, as the name implies, does nothing.

This Intent is mapped to an action in the [WidgetsApp] that does nothing, so that it can be bound to a key in a [Shortcuts] widget in order to disable a key binding made above it in the hierarchy.

# ActionListenerCallback

```dart
typedef ActionListenerCallback = void Function(Action<Intent> action)
```

The kind of callback that an [Action] uses to notify of changes to the action's state.

To register an action listener, call [Action.addActionListener].

# Action

```dart
abstract class Action<T extends Intent> with Diagnosticable {}
```

Base class for an action or command to be performed.

{@youtube 560 315 https://www.youtube.com/watch?v=XawP1i314WM}

[Action]s are typically invoked as a result of a user action. For example, the [Shortcuts] widget will map a keyboard shortcut into an [Intent], which is given to an [ActionDispatcher] to map the [Intent] to an [Action] and invoke it.

The [ActionDispatcher] can invoke an [Action] on the primary focus, or without regard for focus.

### Action Overriding

When using a leaf widget to build a more specialized widget, it's sometimes desirable to change the default handling of an [Intent] defined in the leaf widget. For instance, [TextField]'s [SelectAllTextIntent] by default selects the text it currently contains, but in a US phone number widget that consists of 3 different [TextField]s (area code, prefix and line number), [SelectAllTextIntent] should instead select the text within all 3 [TextField]s.

An overridable [Action] is a special kind of [Action] created using the [Action.overridable] constructor. It has access to a default [Action], and a nullable override [Action]. It has the same behavior as its override if that exists, and mirrors the behavior of its `defaultAction` otherwise.

The [Action.overridable] constructor creates overridable [Action]s that use a [BuildContext] to find a suitable override in its ancestor [Actions] widget. This can be used to provide a default implementation when creating a general purpose leaf widget, and later override it when building a more specialized widget using that leaf widget. Using the [TextField] example above, the [TextField] widget uses an overridable [Action] to provide a sensible default for [SelectAllTextIntent], while still allowing app developers to change that if they add an ancestor [Actions] widget that maps [SelectAllTextIntent] to a different [Action].

See the article on [Using Actions and Shortcuts](https://flutter.dev/to/actions-shortcuts) for a detailed explanation.

See also:

- [Shortcuts], which is a widget that contains a key map, in which it looks up key combinations in order to invoke actions.
- [Actions], which is a widget that defines a map of [Intent] to [Action] and allows redefining of actions for its descendants.
- [ActionDispatcher], a class that takes an [Action] and invokes it, passing a given [Intent].
- [Action.overridable] for an example on how to make an [Action] overridable.

### Action()

```dart
Action()
```

Creates an [Action].

### Action.overridable()

```dart
Action.overridable({required Action<T> defaultAction, required BuildContext context})
```

Creates an [Action] that allows itself to be overridden by the closest ancestor [Action] in the given [context] that handles the same [Intent], if one exists.

When invoked, the resulting [Action] tries to find the closest [Action] in the given `context` that handles the same type of [Intent] as the `defaultAction`, then calls its [Action.invoke] method. When no override [Action]s can be found, it invokes the `defaultAction`.

An overridable action delegates everything to its override if one exists, and has the same behavior as its `defaultAction` otherwise. For this reason, the override has full control over whether and how an [Intent] should be handled, or a key event should be consumed. An override [Action]'s [callingAction] property will be set to the [Action] it currently overrides, giving it access to the default behavior. See the [callingAction] property for an example.

The `context` argument is the [BuildContext] to find the override with. It is typically a [BuildContext] above the [Actions] widget that contains this overridable [Action].

The `defaultAction` argument is the [Action] to be invoked where there's no ancestor [Action]s can't be found in `context` that handle the same type of [Intent].

This is useful for providing a set of default [Action]s in a leaf widget to allow further overriding, or to allow the [Intent] to propagate to parent widgets that also support this [Intent].

{@tool dartpad} This sample shows how to implement a rudimentary `CopyableText` widget that responds to Ctrl-C by copying its own content to the clipboard.

if `CopyableText` is to be provided in a package, developers using the widget may want to change how copying is handled. As the author of the package, you can enable that by making the corresponding [Action] overridable. In the second part of the code sample, three `CopyableText` widgets are used to build a verification code widget which overrides the "copy" action by copying the combined numbers from all three `CopyableText` widgets.

** See code in examples/api/lib/widgets/actions/action.action_overridable.0.dart ** {@end-tool}

### callingAction

```dart
Action<T>? get callingAction
```

The [Action] overridden by this [Action].

The [Action.overridable] constructor creates an overridable [Action] that allows itself to be overridden by the closest ancestor [Action], and falls back to its own `defaultAction` when no overrides can be found. When an override is present, an overridable [Action] forwards all incoming method calls to the override, and allows the override to access the `defaultAction` via its [callingAction] property.

Before forwarding the call to the override, the overridable [Action] is responsible for setting [callingAction] to its `defaultAction`, which is already taken care of by the overridable [Action] created using [Action.overridable].

This property is only non-null when this [Action] is an override of the [callingAction], and is currently being invoked from [callingAction].

Invoking [callingAction]'s methods, or accessing its properties, is allowed and does not introduce infinite loops or infinite recursions.

{@tool snippet} An example `Action` that handles [PasteTextIntent] but has mostly the same behavior as the overridable action. It's OK to call `callingAction?.isActionEnabled` in the implementation of this `Action`.

```dart
class MyPasteAction extends Action<PasteTextIntent> {
  @override
  Object? invoke(PasteTextIntent intent) {
    print(intent);
    return callingAction?.invoke(intent);
  }

  @override
  bool get isActionEnabled => callingAction?.isActionEnabled ?? false;

  @override
  bool consumesKey(PasteTextIntent intent) => callingAction?.consumesKey(intent) ?? false;
}
```

{@end-tool}

### intentType

```dart
Type get intentType
```

Gets the type of intent this action responds to.

### isEnabled()

```dart
bool isEnabled(T intent)
```

Returns true if the action is enabled and is ready to be invoked.

This will be called by the [ActionDispatcher] before attempting to invoke the action.

If the action's enable state depends on a [BuildContext], subclass [ContextAction] instead of [Action].

### isActionEnabled

```dart
bool get isActionEnabled
```

Whether this [Action] is inherently enabled.

If [isActionEnabled] is false, then this [Action] is disabled for any given [Intent].

If the enabled state changes, overriding subclasses must call [notifyActionListeners] to notify any listeners of the change.

In the case of an overridable `Action`, accessing this property creates an dependency on the overridable `Action`s `lookupContext`.

### consumesKey()

```dart
bool consumesKey(T intent)
```

Indicates whether this action should treat key events mapped to this action as being "handled" when it is invoked via the key event.

If the key is handled, then no other key event handlers in the focus chain will receive the event.

If the key event is not handled, it will be passed back to the engine, and continue to be processed there, allowing text fields and non-Flutter widgets to receive the key event.

The default implementation returns true.

### toKeyEventResult()

```dart
KeyEventResult toKeyEventResult(T intent, Object? invokeResult)
```

Converts the result of [invoke] of this action to a [KeyEventResult].

This is typically used when the action is invoked in response to a keyboard shortcut.

The [invokeResult] argument is the value returned by the [invoke] method.

By default, calls [consumesKey] and converts the returned boolean to [KeyEventResult.handled] if it's true, and [KeyEventResult.skipRemainingHandlers] if it's false.

Concrete implementations may refine the type of [invokeResult], since they know the type returned by [invoke].

### invoke()

```dart
Object? invoke(T intent)
```

Called when the action is to be performed.

This is called by the [ActionDispatcher] when an action is invoked via [Actions.invoke], or when an action is invoked using [ActionDispatcher.invokeAction] directly.

This method is only meant to be invoked by an [ActionDispatcher], or by its subclasses, and only when [isEnabled] is true.

When overriding this method, the returned value can be any [Object], but changing the return type of the override to match the type of the returned value provides more type safety.

For instance, if an override of [invoke] returned an `int`, then it might be defined like so:

```dart
class IncrementIntent extends Intent {
  const IncrementIntent({required this.index});

  final int index;
}

class MyIncrementAction extends Action<IncrementIntent> {
  @override
  int invoke(IncrementIntent intent) {
    return intent.index + 1;
  }
}
```

To receive the result of invoking an action, it must be invoked using [Actions.invoke], or by invoking it using an [ActionDispatcher]. An action invoked via a [Shortcuts] widget will have its return value ignored.

If the action's behavior depends on a [BuildContext], subclass [ContextAction] instead of [Action].

### addActionListener()

```dart
void addActionListener(ActionListenerCallback listener)
```

Register a callback to listen for changes to the state of this action.

If you call this, you must call [removeActionListener] a matching number of times, or memory leaks will occur. To help manage this and avoid memory leaks, use of the [ActionListener] widget to register and unregister your listener appropriately is highly recommended.

{@template flutter.widgets.Action.addActionListener} If a listener had been added twice, and is removed once during an iteration (i.e. in response to a notification), it will still be called again. If, on the other hand, it is removed as many times as it was registered, then it will no longer be called. This odd behavior is the result of the [Action] not being able to determine which listener is being removed, since they are identical, and therefore conservatively still calling all the listeners when it knows that any are still registered.

This surprising behavior can be unexpectedly observed when registering a listener on two separate objects which are both forwarding all registrations to a common upstream object. {@endtemplate}

### removeActionListener()

```dart
void removeActionListener(ActionListenerCallback listener)
```

Remove a previously registered closure from the list of closures that are notified when the object changes.

If the given listener is not registered, the call is ignored.

If you call [addActionListener], you must call this method a matching number of times, or memory leaks will occur. To help manage this and avoid memory leaks, use of the [ActionListener] widget to register and unregister your listener appropriately is highly recommended.

{@macro flutter.widgets.Action.addActionListener}

### notifyActionListeners()

```dart
void notifyActionListeners()
```

Call all the registered listeners.

Subclasses should call this method whenever the object changes, to notify any clients the object may have changed. Listeners that are added during this iteration will not be visited. Listeners that are removed during this iteration will not be visited after they are removed.

Exceptions thrown by listeners will be caught and reported using [FlutterError.reportError].

Surprising behavior can result when reentrantly removing a listener (i.e. in response to a notification) that has been registered multiple times. See the discussion at [removeActionListener].

# ActionListener

```dart
class ActionListener extends StatefulWidget {}
```

A helper widget for making sure that listeners on an action are removed properly.

Listeners on the [Action] class must have their listener callbacks removed with [Action.removeActionListener] when the listener is disposed of. This widget helps with that, by providing a lifetime for the connection between the [listener] and the [Action], and by handling the adding and removing of the [listener] at the right points in the widget lifecycle.

If you listen to an [Action] widget in a widget hierarchy, you should use this widget. If you are using an [Action] outside of a widget context, then you must call removeListener yourself.

{@tool dartpad} This example shows how ActionListener handles adding and removing of the [listener] in the widget lifecycle.

** See code in examples/api/lib/widgets/actions/action_listener.0.dart ** {@end-tool}

### ActionListener()

```dart
ActionListener({dynamic key, required ActionListenerCallback listener, required Action<Intent> action, required Widget child})
```

Create a const [ActionListener].

### listener

```dart
ActionListenerCallback listener
```

The [ActionListenerCallback] callback to register with the [action].

### action

```dart
Action<Intent> action
```

The [Action] that the callback will be registered with.

### child

```dart
Widget child
```

{@macro flutter.widgets.ProxyWidget.child}

### createState()

```dart
State<ActionListener> createState()
```

# ContextAction

```dart
abstract class ContextAction<T extends Intent> extends Action<T> {}
```

An abstract [Action] subclass that adds an optional [BuildContext] to the [isEnabled] and [invoke] methods to be able to provide context to actions.

[ActionDispatcher.invokeAction] checks to see if the action it is invoking is a [ContextAction], and if it is, supplies it with a context.

### isEnabled()

```dart
bool isEnabled(T intent, [BuildContext? context])
```

Returns true if the action is enabled and is ready to be invoked.

This will be called by the [ActionDispatcher] before attempting to invoke the action.

The optional `context` parameter is the context of the invocation of the action, and in the case of an action invoked by a [ShortcutManager], via a [Shortcuts] widget, will be the context of the [Shortcuts] widget.

### invoke()

```dart
Object? invoke(T intent, [BuildContext? context])
```

Called when the action is to be performed.

This is called by the [ActionDispatcher] when an action is invoked via [Actions.invoke], or when an action is invoked using [ActionDispatcher.invokeAction] directly.

This method is only meant to be invoked by an [ActionDispatcher], or by its subclasses, and only when [isEnabled] is true.

The optional `context` parameter is the context of the invocation of the action, and in the case of an action invoked by a [ShortcutManager], via a [Shortcuts] widget, will be the context of the [Shortcuts] widget.

When overriding this method, the returned value can be any Object, but changing the return type of the override to match the type of the returned value provides more type safety.

For instance, if an override of [invoke] returned an `int`, then it might be defined like so:

```dart
class IncrementIntent extends Intent {
  const IncrementIntent({required this.index});

  final int index;
}

class MyIncrementAction extends ContextAction<IncrementIntent> {
  @override
  int invoke(IncrementIntent intent, [BuildContext? context]) {
    return intent.index + 1;
  }
}
```

# OnInvokeCallback

```dart
typedef OnInvokeCallback<T extends Intent> = Object? Function(T intent)
```

The signature of a callback accepted by [CallbackAction.onInvoke].

Such callbacks are implementations of [Action.invoke]. The returned value is the return value of [Action.invoke], the argument is the intent passed to [Action.invoke], and so forth.

# CallbackAction

```dart
class CallbackAction<T extends Intent> extends Action<T> {}
```

An [Action] that takes a callback in order to configure it without having to create an explicit [Action] subclass just to call a callback.

See also:

- [Shortcuts], which is a widget that contains a key map, in which it looks up key combinations in order to invoke actions.
- [Actions], which is a widget that defines a map of [Intent] to [Action] and allows redefining of actions for its descendants.
- [ActionDispatcher], a class that takes an [Action] and invokes it using a [FocusNode] for context.

### CallbackAction()

```dart
CallbackAction({required OnInvokeCallback<T> onInvoke})
```

A constructor for a [CallbackAction].

The given callback is used as the implementation of [invoke].

### onInvoke

```dart
OnInvokeCallback<T> onInvoke
```

The callback to be called when invoked.

This is effectively the implementation of [invoke].

### invoke()

```dart
Object? invoke(T intent)
```

# ActionDispatcher

```dart
class ActionDispatcher with Diagnosticable {}
```

An action dispatcher that invokes the actions given to it.

The [invokeAction] method on this class directly calls the [Action.invoke] method on the [Action] object.

For [ContextAction] actions, if no `context` is provided, the [BuildContext] of the [primaryFocus] is used instead.

See also:

- [ShortcutManager], that uses this class to invoke actions.
- [Shortcuts] widget, which defines key mappings to [Intent]s.
- [Actions] widget, which defines a mapping between a in [Intent] type and an [Action].

### ActionDispatcher()

```dart
ActionDispatcher()
```

Creates an action dispatcher that invokes actions directly.

### invokeAction()

```dart
Object? invokeAction(Action<Intent> action, Intent intent, [BuildContext? context])
```

Invokes the given `action`, passing it the given `intent`.

The action will be invoked with the given `context`, if given, but only if the action is a [ContextAction] subclass. If no `context` is given, and the action is a [ContextAction], then the context from the [primaryFocus] is used.

Returns the object returned from [Action.invoke].

The caller must receive a `true` result from [Action.isEnabled] before calling this function (or [ContextAction.isEnabled] with the same `context`, if the `action` is a [ContextAction]). This function will assert if the action is not enabled when called.

Consider using [invokeActionIfEnabled] to invoke the action conditionally based on whether it is enabled or not, without having to check first.

### invokeActionIfEnabled()

```dart
(bool, Object?) invokeActionIfEnabled(Action<Intent> action, Intent intent, [BuildContext? context])
```

Invokes the given `action`, passing it the given `intent`, but only if the action is enabled.

The action will be invoked with the given `context`, if given, but only if the action is a [ContextAction] subclass. If no `context` is given, and the action is a [ContextAction], then the context from the [primaryFocus] is used.

The return value has two components. The first is a boolean indicating if the action was enabled (as per [Action.isEnabled]). If this is false, the second return value is null. Otherwise, the second return value is the object returned from [Action.invoke].

Consider using [invokeAction] if the enabled state of the action is not in question; this avoids calling [Action.isEnabled] redundantly.

# Actions

```dart
class Actions extends StatefulWidget {}
```

A widget that maps [Intent]s to [Action]s to be used by its descendants when invoking an [Action].

{@youtube 560 315 https://www.youtube.com/watch?v=XawP1i314WM}

Actions are typically invoked using [Shortcuts]. They can also be invoked using [Actions.invoke] on a context containing an ambient [Actions] widget.

{@tool dartpad} This example creates a custom [Action] subclass `ModifyAction` for modifying a model, and another, `SaveAction` for saving it.

This example demonstrates passing arguments to the [Intent] to be carried to the [Action]. Actions can get data either from their own construction (like the `model` in this example), or from the intent passed to them when invoked (like the increment `amount` in this example).

This example also demonstrates how to use Intents to limit a widget's dependencies on its surroundings. The `SaveButton` widget defined in this example can invoke actions defined in its ancestor widgets, which can be customized to match the part of the widget tree that it is in. It doesn't need to know about the `SaveAction` class, only the `SaveIntent`, and it only needs to know about a value notifier, not the entire model.

** See code in examples/api/lib/widgets/actions/actions.0.dart ** {@end-tool}

See also:

- [Shortcuts], a widget used to bind key combinations to [Intent]s.
- [Intent], a class that contains configuration information for running an [Action].
- [Action], a class for containing and defining an invocation of a user action.
- [ActionDispatcher], the object that this widget uses to manage actions.

### Actions()

```dart
Actions({dynamic key, ActionDispatcher? dispatcher, required Map<Type, Action<Intent>> actions, required Widget child})
```

Creates an [Actions] widget.

### dispatcher

```dart
ActionDispatcher? dispatcher
```

The [ActionDispatcher] object that invokes actions.

This is what is returned from [Actions.of], and used by [Actions.invoke].

If this [dispatcher] is null, then [Actions.of] and [Actions.invoke] will look up the tree until they find an Actions widget that has a dispatcher set. If no such widget is found, then they will return/use a default-constructed [ActionDispatcher].

### actions

```dart
Map<Type, Action<Intent>> actions
```

{@template flutter.widgets.actions.actions} A map of [Intent] keys to [Action<Intent>] objects that defines which actions this widget knows about.

For performance reasons, it is recommended that a pre-built map is passed in here (e.g. a final variable from your widget class) instead of defining it inline in the build function. {@endtemplate}

### child

```dart
Widget child
```

{@macro flutter.widgets.ProxyWidget.child}

### handler()

```dart
VoidCallback? handler<T extends Intent>(BuildContext context, T intent)
```

Returns a [VoidCallback] handler that invokes the bound action for the given `intent` if the action is enabled, and returns null if the action is not enabled, or no matching action is found.

This is intended to be used in widgets which have something similar to an `onTap` handler, which takes a `VoidCallback`, and can be set to the result of calling this function.

Creates a dependency on the [Actions] widget that maps the bound action so that if the actions change, the context will be rebuilt and find the updated action.

The value returned from the [Action.invoke] method is discarded when the returned callback is called. If the return value is needed, consider using [Actions.invoke] instead.

### find()

```dart
Action<T> find<T extends Intent>(BuildContext context, {T? intent})
```

Finds the [Action] bound to the given intent type `T` in the given `context`.

Creates a dependency on the [Actions] widget that maps the bound action so that if the actions change, the context will be rebuilt and find the updated action.

The optional `intent` argument supplies the type of the intent to look for if the concrete type of the intent sought isn't available. If not supplied, then `T` is used.

If no [Actions] widget surrounds the given context, this function will assert in debug mode, and throw an exception in release mode.

{@macro flutter.widgets.actions.findLimitations}

See also:

- [maybeFind], which is similar to this function, but will return null if no [Actions] ancestor is found.

### maybeFind()

```dart
Action<T>? maybeFind<T extends Intent>(BuildContext context, {T? intent})
```

Finds the [Action] bound to the given intent type `T` in the given `context`.

Creates a dependency on the [Actions] widget that maps the bound action so that if the actions change, the context will be rebuilt and find the updated action.

The optional `intent` argument supplies the type of the intent to look for if the concrete type of the intent sought isn't available. If not supplied, then `T` is used.

If no [Actions] widget surrounds the given context, this function will return null.

{@template flutter.widgets.actions.findLimitations}

## Limitations:

It is strongly recommended that callers explicitly set the type parameter to `Intent` when the `intent` parameter is not null:

```dart
Actions.find<Intent>(context, intent: intent); // GOOD
Actions.find(context, intent: intent); // BAD
```

If the type parameter is not set to `Intent` when the `intent` parameter is not null, this method might be unable to return a perfectly capable `Action`. For instance, this method cannot return an `Action<Intent>` - an action that can be bound to any intent - unless `T` is exactly `Intent`. This will trigger assertions in debug mode. {@endtemplate}

See also:

- [find], which is similar to this function, but will throw if no [Actions] ancestor is found.

### of()

```dart
ActionDispatcher of(BuildContext context)
```

Returns the [ActionDispatcher] associated with the [Actions] widget that most tightly encloses the given [BuildContext].

Will return a newly created [ActionDispatcher] if no ambient [Actions] widget is found.

### invoke()

```dart
Object? invoke<T extends Intent>(BuildContext context, T intent)
```

Invokes the action associated with the given [Intent] using the [Actions] widget that most tightly encloses the given [BuildContext].

This method returns the result of invoking the action's [Action.invoke] method.

If the given `intent` doesn't map to an action, then it will look to the next ancestor [Actions] widget in the hierarchy until it reaches the root.

This method will throw an exception if no ambient [Actions] widget is found, or when a suitable [Action] is found but it returns false for [Action.isEnabled].

### maybeInvoke()

```dart
Object? maybeInvoke<T extends Intent>(BuildContext context, T intent)
```

Invokes the action associated with the given [Intent] using the [Actions] widget that most tightly encloses the given [BuildContext].

This method returns the result of invoking the action's [Action.invoke] method. If no action mapping was found for the specified intent, or if the first action found was disabled, or the action itself returns null from [Action.invoke], then this method returns null.

If the given `intent` doesn't map to an action, then it will look to the next ancestor [Actions] widget in the hierarchy until it reaches the root. If a suitable [Action] is found but its [Action.isEnabled] returns false, the search will stop and this method will return null.

### createState()

```dart
State<Actions> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# FocusableActionDetector

```dart
class FocusableActionDetector extends StatefulWidget {}
```

A widget that combines the functionality of [Actions], [Shortcuts], [MouseRegion] and a [Focus] widget to create a detector that defines actions and key bindings, and provides callbacks for handling focus and hover highlights.

{@youtube 560 315 https://www.youtube.com/watch?v=R84AGg0lKs8}

This widget can be used to give a control the required detection modes for focus and hover handling. It is most often used when authoring a new control widget, and the new control should be enabled for keyboard traversal and activation.

{@tool dartpad} This example shows how keyboard interaction can be added to a custom control that changes color when hovered and focused, and can toggle a light when activated, either by touch or by hitting the `X` key on the keyboard when the "And Me" button has the keyboard focus (be sure to use TAB to move the focus to the "And Me" button before trying it out).

This example defines its own key binding for the `X` key, but in this case, there is also a default key binding for [ActivateAction] in the default key bindings created by [WidgetsApp] (the parent for [MaterialApp], and [CupertinoApp]), so the `ENTER` key will also activate the buttons.

** See code in examples/api/lib/widgets/actions/focusable_action_detector.0.dart ** {@end-tool}

This widget doesn't have any visual representation, it is just a detector that provides focus and hover capabilities.

It hosts its own [FocusNode] or uses [focusNode], if given.

### FocusableActionDetector()

```dart
FocusableActionDetector({dynamic key, bool enabled = true, FocusNode? focusNode, bool autofocus = false, bool descendantsAreFocusable = true, bool descendantsAreTraversable = true, Map<ShortcutActivator, Intent>? shortcuts, Map<Type, Action<Intent>>? actions, ValueChanged<bool>? onShowFocusHighlight, ValueChanged<bool>? onShowHoverHighlight, ValueChanged<bool>? onFocusChange, MouseCursor mouseCursor = MouseCursor.defer, bool includeFocusSemantics = true, required Widget child})
```

Create a const [FocusableActionDetector].

### enabled

```dart
bool enabled
```

Is this widget enabled or not.

If disabled, will not send any notifications needed to update highlight or focus state, and will not define or respond to any actions or shortcuts.

When disabled, adds [Focus] to the widget tree, but sets [Focus.canRequestFocus] to false.

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.Focus.autofocus}

### descendantsAreFocusable

```dart
bool descendantsAreFocusable
```

{@macro flutter.widgets.Focus.descendantsAreFocusable}

### descendantsAreTraversable

```dart
bool descendantsAreTraversable
```

{@macro flutter.widgets.Focus.descendantsAreTraversable}

### actions

```dart
Map<Type, Action<Intent>>? actions
```

{@macro flutter.widgets.actions.actions}

### shortcuts

```dart
Map<ShortcutActivator, Intent>? shortcuts
```

{@macro flutter.widgets.shortcuts.shortcuts}

### onShowFocusHighlight

```dart
ValueChanged<bool>? onShowFocusHighlight
```

A function that will be called when the focus highlight should be shown or hidden.

This method is not triggered at the unmount of the widget.

### onShowHoverHighlight

```dart
ValueChanged<bool>? onShowHoverHighlight
```

A function that will be called when the hover highlight should be shown or hidden.

This method is not triggered at the unmount of the widget.

### onFocusChange

```dart
ValueChanged<bool>? onFocusChange
```

A function that will be called when the focus changes.

Called with true if the [focusNode] has primary focus.

### mouseCursor

```dart
MouseCursor mouseCursor
```

The cursor for a mouse pointer when it enters or is hovering over the widget.

The [mouseCursor] defaults to [MouseCursor.defer], deferring the choice of cursor to the next region behind it in hit-test order.

### includeFocusSemantics

```dart
bool includeFocusSemantics
```

Whether to include semantics from [Focus].

Defaults to true.

### child

```dart
Widget child
```

The child widget for this [FocusableActionDetector] widget.

{@macro flutter.widgets.ProxyWidget.child}

### createState()

```dart
State<FocusableActionDetector> createState()
```

# VoidCallbackIntent

```dart
class VoidCallbackIntent extends Intent {}
```

An [Intent] that keeps a [VoidCallback] to be invoked by a [VoidCallbackAction] when it receives this intent.

### VoidCallbackIntent()

```dart
VoidCallbackIntent(VoidCallback callback)
```

Creates a [VoidCallbackIntent].

### callback

```dart
VoidCallback callback
```

The callback that is to be called by the [VoidCallbackAction] that receives this intent.

# VoidCallbackAction

```dart
class VoidCallbackAction extends Action<VoidCallbackIntent> {}
```

An [Action] that invokes the [VoidCallback] given to it in the [VoidCallbackIntent] passed to it when invoked.

See also:

- [CallbackAction], which is an action that will invoke a callback with the intent passed to the action's invoke method. The callback is configured on the action, not the intent, like this class.

### invoke()

```dart
Object? invoke(VoidCallbackIntent intent)
```

# DoNothingIntent

```dart
class DoNothingIntent extends Intent {}
```

An [Intent] that is bound to a [DoNothingAction].

Attaching a [DoNothingIntent] to a [Shortcuts] mapping is one way to disable a keyboard shortcut defined by a widget higher in the widget hierarchy and consume any key event that triggers it via a shortcut.

This intent cannot be subclassed.

See also:

- [DoNothingAndStopPropagationIntent], a similar intent that will not handle the key event, but will still keep it from being passed to other key handlers in the focus chain.

### DoNothingIntent()

```dart
DoNothingIntent()
```

Creates a const [DoNothingIntent].

# DoNothingAndStopPropagationIntent

```dart
class DoNothingAndStopPropagationIntent extends Intent {}
```

An [Intent] that is bound to a [DoNothingAction], but, in addition to not performing an action, also stops the propagation of the key event bound to this intent to other key event handlers in the focus chain.

Attaching a [DoNothingAndStopPropagationIntent] to a [Shortcuts.shortcuts] mapping is one way to disable a keyboard shortcut defined by a widget higher in the widget hierarchy. In addition, the bound [DoNothingAction] will return false from [DoNothingAction.consumesKey], causing the key bound to this intent to be passed on to the platform embedding as "not handled" with out passing it to other key handlers in the focus chain (e.g. parent `Shortcuts` widgets higher up in the chain).

This intent cannot be subclassed.

See also:

- [DoNothingIntent], a similar intent that will handle the key event.

### DoNothingAndStopPropagationIntent()

```dart
DoNothingAndStopPropagationIntent()
```

Creates a const [DoNothingAndStopPropagationIntent].

# DoNothingAction

```dart
class DoNothingAction extends Action<Intent> {}
```

An [Action] that doesn't perform any action when invoked.

Attaching a [DoNothingAction] to an [Actions.actions] mapping is a way to disable an action defined by a widget higher in the widget hierarchy.

If [consumesKey] returns false, then not only will this action do nothing, but it will stop the propagation of the key event used to trigger it to other widgets in the focus chain and tell the embedding that the key wasn't handled, allowing text input fields or other non-Flutter elements to receive that key event. The return value of [consumesKey] can be set via the `consumesKey` argument to the constructor.

This action can be bound to any [Intent].

See also:

- [DoNothingIntent], which is an intent that can be bound to a [KeySet] in a [Shortcuts] widget to do nothing.
- [DoNothingAndStopPropagationIntent], which is an intent that can be bound to a [KeySet] in a [Shortcuts] widget to do nothing and also stop key event propagation to other key handlers in the focus chain.

### DoNothingAction()

```dart
DoNothingAction({bool consumesKey = true})
```

Creates a [DoNothingAction].

The optional [consumesKey] argument defaults to true.

### consumesKey()

```dart
bool consumesKey(Intent intent)
```

### invoke()

```dart
void invoke(Intent intent)
```

# ActivateIntent

```dart
class ActivateIntent extends Intent {}
```

An [Intent] that activates the currently focused control.

This intent is bound by default to the [LogicalKeyboardKey.space] key on all platforms, and also to the [LogicalKeyboardKey.enter] key on all platforms except the web, where ENTER doesn't toggle selection. On the web, ENTER is bound to [ButtonActivateIntent] instead.

See also:

- [WidgetsApp.defaultShortcuts], which contains the default shortcuts used in apps.
- [WidgetsApp.shortcuts], which defines the shortcuts to use in an application (and defaults to [WidgetsApp.defaultShortcuts]).

### ActivateIntent()

```dart
ActivateIntent()
```

Creates an intent that activates the currently focused control.

# ButtonActivateIntent

```dart
class ButtonActivateIntent extends Intent {}
```

An [Intent] that activates the currently focused button.

This intent is bound by default to the [LogicalKeyboardKey.enter] key on the web, where ENTER can be used to activate buttons, but not toggle selection. All other platforms bind [LogicalKeyboardKey.enter] to [ActivateIntent].

See also:

- [WidgetsApp.defaultShortcuts], which contains the default shortcuts used in apps.
- [WidgetsApp.shortcuts], which defines the shortcuts to use in an application (and defaults to [WidgetsApp.defaultShortcuts]).

### ButtonActivateIntent()

```dart
ButtonActivateIntent()
```

Creates an intent that activates the currently focused control, if it's a button.

# ActivateAction

```dart
abstract class ActivateAction extends Action<ActivateIntent> {}
```

An [Action] that activates the currently focused control.

This is an abstract class that serves as a base class for actions that activate a control. By default, is bound to [LogicalKeyboardKey.enter], [LogicalKeyboardKey.gameButtonA], and [LogicalKeyboardKey.space] in the default keyboard map in [WidgetsApp].

# SelectIntent

```dart
class SelectIntent extends Intent {}
```

An [Intent] that selects the currently focused control.

### SelectIntent()

```dart
SelectIntent()
```

Creates an intent that selects the currently focused control.

# SelectAction

```dart
abstract class SelectAction extends Action<SelectIntent> {}
```

An action that selects the currently focused control.

This is an abstract class that serves as a base class for actions that select something. It is not bound to any key by default.

# DismissIntent

```dart
class DismissIntent extends Intent {}
```

An [Intent] that dismisses the currently focused widget.

The [WidgetsApp.defaultShortcuts] binds this intent to the [LogicalKeyboardKey.escape] and [LogicalKeyboardKey.gameButtonB] keys.

See also:

- [ModalRoute] which listens for this intent to dismiss modal routes (dialogs, pop-up menus, drawers, etc).

### DismissIntent()

```dart
DismissIntent()
```

Creates an intent that dismisses the currently focused widget.

# DismissAction

```dart
abstract class DismissAction extends Action<DismissIntent> {}
```

An [Action] that dismisses the focused widget.

This is an abstract class that serves as a base class for dismiss actions.

# PrioritizedIntents

```dart
class PrioritizedIntents extends Intent {}
```

An [Intent] that evaluates a series of specified [orderedIntents] for execution.

The first intent that matches an enabled action is used.

### PrioritizedIntents()

```dart
PrioritizedIntents({required List<Intent> orderedIntents})
```

Creates an intent that is used with [PrioritizedAction] to specify a list of intents, the first available of which will be used.

### orderedIntents

```dart
List<Intent> orderedIntents
```

List of intents to be evaluated in order for execution. When an [Action.isEnabled] returns true, that action will be invoked and progression through the ordered intents stops.

# PrioritizedAction

```dart
class PrioritizedAction extends ContextAction<PrioritizedIntents> {}
```

An [Action] that iterates through a list of [Intent]s, invoking the first that is enabled.

The [isEnabled] method must be called before [invoke]. Calling [isEnabled] configures the object by seeking the first intent with an enabled action. If the actions have an opportunity to change enabled state, [isEnabled] must be called again before calling [invoke].

### isEnabled()

```dart
bool isEnabled(PrioritizedIntents intent, [BuildContext? context])
```

### invoke()

```dart
void invoke(PrioritizedIntents intent, [BuildContext? context])
```
