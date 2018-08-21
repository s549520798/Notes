##Custom View 

Here is a high level overview of what you need to know to get started in creating your own View components:

1. Extend an existing View class or subclass with your own class.
2. Override some of the methods from the superclass. The superclass methods to override start with 'on', for example, onDraw(), onMeasure(), and onKeyDown(). This is similar to the on... events in Activity or ListActivity that you override for lifecycle and other functionality hooks.
3. Use your new extension class. Once completed, your new extension class can be used in place of the view upon which it was based.

To create a fully customized component:

1. The most generic view you can extend is, unsurprisingly, View, so you will usually start by extending this to create your new super component.
2. You can supply a constructor which can take attributes and parameters from the XML, and you can also consume your own such attributes and parameters (perhaps the color and range of the VU meter, or the width and damping of the needle, etc.)
3. You will probably want to create your own event listeners, property accessors and modifiers, and possibly more sophisticated behavior in your component class as well.
4. You will almost certainly want to override onMeasure() and are also likely to need to override onDraw() if you want the component to show something. While both have default behavior, the default onDraw() will do nothing, and the default onMeasure() will always set a size of 100x100 — which is probably not what you want.
5. Other on... methods may also be overridden as required.