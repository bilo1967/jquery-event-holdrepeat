# jquery-event-hold
On Mouse Hold event handling component for JQuery

This plugin extends jQuery to support "hold" events, which are triggered when an element is pressed and held at least for a specified duration. During the hold, the event is triggered repeatedly at a configurable interval, with optional acceleration to decrease the interval over time (and increase the trigger rate).

Features:
- Customizable initial delay before the first hold event.
- Configurable repeat interval between hold events.
- Optional acceleration to dynamically adjust the interval.
- Support for both mouse and touch events.
- Works with direct event binding and event delegation.
- Prevents accidental clicks during hold interactions (ghost clicks).

Usage Example:
```javascript
// Basic usage
$('#element').on('hold', function(e) {
    console.log(``Hold iteration ${e.iteration} at ${e.currentInterval}ms`);
});
```

Usage with custom options:
```javascript
$('#element').on('hold', {
    initialDelay: 300,        // Delay before first hold event (ms)
    repeatInterval: 100,      // Base interval between hold events (ms)
    acceleration: 0.8,        // Acceleration factor (0-1)
    accelerateAfter: 5,       // Start acceleration after N iterations
    minRepeatInterval: 30,    // Minimum interval (ms)
    maxIterationsPerHold: 50, // Maximum iterations per hold, to prevent infinite
                              // loops. Can be set to Infinity
}, function(e) {
    console.log(`Hold iteration ${e.iteration + 1} at ${e.currentInterval}ms`);
});
```

Example with event delegation

```javascript
$(document).on('hold', '.dynamic-element', function(e) {
    console.log(`Hold on dynamically added element`);
});
```

Triggered events:
- holdstart: Triggered when the initial delay expires.
- hold: Triggered repeatedly during the hold.
- holdstop: Triggered when the hold ends.

Event Object Properties:
- originalEvent: The native mouse/touch event.
- iteration: The current hold iteration (starts at 0).
- startTime: Timestamp when the hold started.
- currentInterval: The current interval between events (ms).
- duration: (holdstop only) Total duration of the hold (ms).
- accelerating: true, if acceleration is on

Dependencies:
- jQuery 1.7+

Browser Support:
- Chrome, Firefox, Safari, and other modern browsers.
- Touch devices (with optional scroll prevention).
- Does *NOT* support Internet Explorer (any version).
