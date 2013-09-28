EventEmitter
============

Browser version of <a href="http://nodejs.org/api/events.html#events_class_events_eventemitter">NodeJS EventEmitter.</a>

Description
============

This class provides the same behavior and interface as <a href="http://nodejs.org/api/events.html#events_class_events_eventemitter">NodeJS EventEmitter</a>.
And can be used within browser environment.

Example
------------
```javascript
var emitter = new events.EventEmitter();

/**
 * Special event for listening to new listeners addition.
 */
emitter.on('newListener', function (event, listener) {
    console.log('listener: "%s" was added for "%s" event', listener.toString(), event);
});
/**
 * Special event for listening to listeners removing.
 */
emitter.on('removeListener', function (event, listener) {
    console.log('listener: "%s" was removed from "%s" event', listener.toString(), event);
});

// listener
function myListener() {
    console.log(arguments);
}

/**
 * Add event listeners.
 */
emitter.on('my-event', myListener);
// same but a bit longer.
// emitter.addListener('my-event', myListener);
// add a one-time listener
emitter.once('my-event', myListener);

/**
 * Explore event listeners list.
 */
// with constructor static method
console.log(EventEmitter.listenerCount(emitter, 'my-event')); // 2
// same but with instance method
console.log(emitter.listeners('my-event').length); // 2

/**
 * Event firing
 */
emitter.emit('my-event', 'arg1', 'arg2', 'arg3');

// listener was added with "once" method was removed
console.log(EventEmitter.listenerCount(emitter, 'my-event')); // 1

/**
 * Remove event listeners.
 */
// remove one listener of the specified event
emitter.removeListener('my-event', myListener);
// same but a bit shorter
// emitter.off('my-event', myListener);

// remove all listeners of the specified event
emitter.removeAllListeners('my-event');
// same but a bit shorter
// emitter.off('my-event');

// remove all listeners of all events
emitter.removeAllListeners();
// same but a bit shorter
// emitter.off();

/**
 * Set maximum listeners.
 */
emitter.setMaxListeners(1000);
// Set to zero for unlimited.
emitter.setMaxListeners(0);
```
