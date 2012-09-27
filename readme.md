# Backbone.EventBinder

Manage your Backbone events better.

## About Backbone.EventBinder

Backbone's events are a great way to decouple parts of your system, but 
they have some limitations and behaviors that you need to be aware of
which can cause 
[zombie objects and memory leaks](http://lostechies.com/derickbailey/2011/09/15/zombies-run-managing-page-transitions-in-backbone-apps/) 
if you're not careful.

Backbone.EventBinder provides a simple mechanism for cleaning up your
event bindings, including the ability to clean up anonymous callback
functions!

## Downloads And Source

Grab the source from the `src` folder above. Grab the most recent builds
from the links below.

### Standard Builds

* Development: [backbone.eventbinder.js](https://raw.github.com/marionettejs/backbone.eventbinder/master/lib/backbone.eventbinder.js)

* Production: [backbone.eventbinder.min.js](https://raw.github.com/marionettejs/backbone.eventbinder/master/lib/backbone.eventbinder.min.js)

### RequireJS (AMD) Builds

* Development: [backbone.eventbinder.js](https://raw.github.com/marionettejs/backbone.eventbinder/master/lib/amd/backbone.eventbinder.js)

* Production: [backbone.eventbinder.min.js](https://raw.github.com/marionettejs/backbone.eventbinder/master/lib/amd/backbone.eventbinder.min.js)

## Documentation

The `EventBinder` object provides event binding management for related
events, across any number of objects that trigger the events. This allows
events to be grouped together and unbound with a single call during the 
clean-up of an object that is bound to the events.

### Bind Events

```js
var binder = new Backbone.EventBinder();

var model = new MyModel();

var handler = {
  doIt: function(){}
}

binder.bindTo(model, "change:foo", handler.doIt);
```

You can optionally specify a 4th parameter as the context in which the callback
method for the event will be executed:

```js
binder.bindTo(model, "change:foo", someCallback, someContext);
```

### Unbind A Single Event

When you call `bindTo`, it returns a "binding" object that can be
used to unbind from a single event with the `unbindFrom` method:

```js
var binding = binder.bindTo(model, "change:foo", someCallback, someContext);

// later in the code
binder.unbindFrom(binding);
```

This will unbind the event that was configured with the binding
object, and remove it from the EventBinder bindings.

### Unbind All Events

You can call `unbindAll` to unbind all events that were bound with the
`bindTo` method:

```js
binder.unbindAll();
```

This even works with in-line callback functions.

### When To Use EventBinder vs `on` Handlers

See the wiki: [When to use the EventBinder](https://github.com/marionettejs/backbone.marionette/wiki/When-to-use-the-EventBinder)

## License

MIT - see [LICENSE.md](https://raw.github.com/marionettejs/backbone.eventbinder/master/LICENSE.md)
