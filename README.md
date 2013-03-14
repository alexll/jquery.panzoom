# jQuery Panzoom

Panzoom is a progressive plugin to create panning and zooming functionality for an element. Panzoom supports the same browsers as jQuery 2.0 and can be used with jQuery 1.9.0+ or jQuery 2.0+.
It uses CSS transforms and matrix functions to take advantage of hardware/GPU acceleration in the browser. Although IE<=8 is not supported, this plugin is future-proof.

jquery.panzoom.min.js (7.0kb), included in this repo, is compressed with [uglifyjs](https://github.com/mishoo/UglifyJS).

## Mobile support

Panzoom includes support for touch gestures and even supports pinch gestures for zooming. It is perfectly suited for both mobile and desktop browsers. You'll be amazed at how well this performs on your iPad or iPhone.

## Dependencies

Panzoom obviously depends on jQuery, but it also depends on [Modernizr](http://modernizr.com/) for its touch gesture support detection.<br>
If Modernizr is not included, touch gestures will simply not be used and it will fail silently.<br>
However, mobile behavior is not supported without Modernizr and its touch support feature detect.

## Loading Panzoom
Panzoom can obviously be included with your scripts at the end of the body, but Panzoom supports AMD for javascript module love.

With script tags:

  <script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
  <script src="/js/plugins/jquery.panzoom.js"></script>

With AMD loader in an anonymous module:

  define([ "jquery", "plugins/jquery.panzoom" ], function( $ ) {
    $(document).ready(function() {
      $(".panzoom-elements").panzoom();
    });
  });

## Initialization

  $(".panzoom-elements").panzoom();

  // Pass options
  $("a.panzoom-elements").panzoom({
    minScale: 0,
    $zoomRange: $("input[type='range']")
  });

## Options

All options can be overridden by passing an object literal like any other plugin,<br>
or with the `"option"` method.<br>

  Panzoom.defaults = {
    // Should always be non-empty
    // Used to bind jQuery events without collisions
    // A guid is not added here as different instantiations/versions of panzoom
    // on the same element is not supported, so don't do it.
    eventNamespace: ".panzoom",

    // Whether or not to transition the scale
    transition: true,

    // The increment at which to zoom
    // adds/subtracts to the scale each time zoomIn/Out is called
    increment: 0.3,

    minScale: 0.4,
    maxScale: 5,

    // Animation duration (ms)
    duration: 200,
    // CSS easing used for scale transition
    easing: "ease-in-out",

    // Zoom buttons/links collection (you can also bind these yourself - e.g. `$button.on("click", function( e ) { e.preventDefault(); $elem.panzooom("zoomIn"); });` )
    $zoomIn: $(),
    $zoomOut: $(),
    // Range input on which to bind zooming functionality
    $zoomRange: $(),
    // Reset buttons/links collection on which to bind the reset method
    $reset: $()
  };

## Methods

Methods can be called in the same way as a widget from the jQuery UI widget factory. Pass a method name when calling panzoom. Strings are interpreted as method names.

### `option`

  // One at a time
  // Sets the scale increment option
  $elem.panzoom( "option", "increment", 0.4 );

  // Several options at once
  $elem.panzoom("option", {
    increment: 0.4,
    minScale: 0.1,
    maxScale: 2,
    duration: 500,
    $reset: $("a.reset-panzoom, button.reset-panzoom")
  });

Any option can be changed. See the defaults above for a list.

### `reset`

  $elem.panzoom("reset");

Reset the transform matrix to its original value. All panning and zooming is reset.

### `zoom( scale, noSetRange )`

@param {Number|Boolean} [scale] The exact scale to which to zoom or a boolean indicating to transition a zoom out
@param {Boolean} [noSetRange] Specify that the method should not set the $zoomRange value (as is the case when $zoomRange is calling zoom on change. No need to set that value. Most of the time though, just ignore this parameter.)


  // Transition a zoom in based on the scale increment, min and max values
  $elem.panzoom("zoom");

  // Transition a zoom out
  $elem.panzoom( "zoom", true );

  // Set the scale immediately without a transition
  $elem.panzoom( "zoom", 1.2 );

Transition a zoom in based on the scale increment, min and max values, and animation duration and easing. This method handles both zooming in and zooming out.<br>
If the method is passed a number, `zoom()` will immediately set that scale without transitioning. This is mostly useful for the range input and pinch gestures.

### `instance`

  var panzoom = $elem.panzoom("instance");

Retrieves the Panzoom instance(s) from the set. If there are multiple, you will get an array of instances. If there is only one, you will just get that instance of Panzoom.

### `destroy`

  $elem.panzoom("destroy");

Unbinds all events and removes all data, including the Panzoom instance on the element.

## Testing

Tests can be run by opening [test/index.html](http://timmywil.github.com/jquery.panzoom/test/) in a browser or by using [`grunt`](http://gruntjs.com/) and [phantomjs](http://phantomjs.org/). See the CONTRIBUTING.md for more info.

Tests are written with [mocha](http://visionmedia.github.com/mocha/) and [chai for bdd-style assertions](http://chaijs.com/api/bdd/).