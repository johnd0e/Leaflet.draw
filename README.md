|Build Status|Leaflet.draw Chat|Leaflet Chat|
|---|---|---|
|[![Build Status](https://travis-ci.org/Leaflet/Leaflet.draw.svg?branch=master)](https://travis-ci.org/Leaflet/Leaflet.draw)|[![Leaflet.draw Chat](https://badges.gitter.im/Leaflet/Leaflet.draw.svg)](https://gitter.im/Leaflet/Leaflet.draw?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)|[![Leaflet Chat](https://badges.gitter.im/Leaflet/Leaflet.svg)](https://gitter.im/Leaflet/Leaflet?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)|

# Leaflet.draw
Adds support for drawing and editing vectors and markers on [Leaflet maps](https://github.com/Leaflet/Leaflet).

Supports [Leaflet](https://github.com/Leaflet/Leaflet/releases) 0.7.x and 1.0.0+ branches.

Please check out our new [Api Documentation](https://leaflet.github.io/Leaflet.draw/docs/leaflet-draw-latest.html)

#### Upgrading from Leaflet.draw 0.1

Leaflet.draw 0.2.0 changes a LOT of things from 0.1. Please see [BREAKING CHANGES](https://github.com/Leaflet/Leaflet.draw/blob/master/BREAKINGCHANGES.md) for how to upgrade.

## Table of Contents
[Install](#install)  
[CDN](#cdn)  
[Using the plugin](#using)  
[Advanced Options](#options)  
[Common tasks](#commontasks)  
[Thanks](#thanks)

## Install

# npm

To install the plugin run `npm install leaflet-draw` via command line in your project. You must also require this in your project like so: `var leafletDraw = require('leaflet-draw');`
# bower

To install the plugin run `bower install leaflet-draw`.

## CDN

Using unpkg
```
<link rel="stylesheet" href="https://unpkg.com/leaflet-draw@0.4.1/dist/leaflet.draw.css" />
<script src="https://unpkg.com/leaflet-draw@0.4.1/dist/leaflet.draw.js"></script>
```

Using CDNJS
```
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet.draw/0.4.0/leaflet.draw.css"/>
<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet.draw/0.4.0/leaflet.draw.js"></script>
```

## Advanced options

You can configure the plugin by using the different options listed here.

### Control.Draw

These options make up the root object that is used when initialising the Leaflet.draw control.

| Option | Type | Default | Description
| --- | --- | --- | ---
| position | String | `'topleft'` | The initial position of the control (one of the map corners). See [control positions](http://leafletjs.com/reference.html#control-positions).
| draw | [DrawOptions](#drawoptions) | `{}` | The options used to configure the draw toolbar.
| edit | [EditPolyOptions](#editpolyoptions) | `false` | The options used to configure the edit toolbar.

### DrawOptions

These options will allow you to configure the draw toolbar and its handlers.

| Option | Type | Default | Description
| --- | --- | --- | ---
| polyline | [PolylineOptions](#polylineoptions) | `{ }` | Polyline draw handler options. Set to `false` to disable handler.
| polygon | [PolygonOptions](#polygonoptions) | `{ }` | Polygon draw handler options. Set to `false` to disable handler.
| rectangle | [RectangleOptions](#rectangleoptions) | `{ }` | Rectangle draw handler options. Set to `false` to disable handler.
| circle | [CircleOptions](#circleoptions) | `{ }` | Circle draw handler options. Set to `false` to disable handler.
| marker | [MarkerOptions](#markeroptions) | `{ }` | Marker draw handler options. Set to `false` to disable handler.

### Draw handler options

The following options will allow you to configure the individual draw handlers.

#### PolylineOptions

Polyline and Polygon drawing handlers take the same options.

| Option | Type | Default | Description
| --- | --- | --- | ---
| allowIntersection | Bool | `true` | Determines if line segments can cross.
| drawError | Object | [See code](https://github.com/Leaflet/Leaflet.draw/blob/master/src/draw/handler/Draw.Polyline.js#L10) | Configuration options for the error that displays if an intersection is detected.
| guidelineDistance | Number | `20` | Distance in pixels between each guide dash.
| shapeOptions | [Leaflet Polyline options](http://leafletjs.com/reference.html#polyline-options) | [See code](https://github.com/Leaflet/Leaflet.draw/blob/master/src/draw/handler/Draw.Polyline.js#L20) | The options used when drawing the polyline/polygon on the map.
| metric | Bool | `true` | Determines which measurement system (metric or imperial) is used.
| zIndexOffset | Number | `2000` | This should be a high number to ensure that you can draw over all other layers on the map.
| repeatMode | Bool | `false` | Determines if the draw tool remains enabled after drawing a shape.

#### PolygonOptions

Polygon options include all of the Polyline options plus the option to show the approximate area.

| Option | Type | Default | Description
| --- | --- | --- | ---
| showArea | Bool | `false` | Show the area of the drawn polygon in m², ha or km². **The area is only approximate and become less accurate the larger the polygon is.**

#### RectangleOptions

| Option | Type | Default | Description
| --- | --- | --- | ---
| shapeOptions | [Leaflet Path options](http://leafletjs.com/reference.html#path-options) | [See code](https://github.com/Leaflet/Leaflet.draw/blob/master/src/draw/handler/Draw.Rectangle.js#L7) | The options used when drawing the rectangle on the map.
| repeatMode | Bool | `false` | Determines if the draw tool remains enabled after drawing a shape.

#### CircleOptions

| Option | Type | Default | Description
| --- | --- | --- | ---
| shapeOptions | [Leaflet Path options](http://leafletjs.com/reference.html#path-options) | [See code](https://github.com/Leaflet/Leaflet.draw/blob/master/src/draw/handler/Draw.Circle.js#L7) | The options used when drawing the circle on the map.
| repeatMode | Bool | `false` | Determines if the draw tool remains enabled after drawing a shape.

#### MarkerOptions

| Option | Type | Default | Description
| --- | --- | --- | ---
| icon | [Leaflet Icon](http://leafletjs.com/reference.html#icon) | `L.Icon.Default()` | The icon displayed when drawing a marker.
| zIndexOffset | Number | `2000` | This should be a high number to ensure that you can draw over all other layers on the map.
| repeatMode | Bool | `false` | Determines if the draw tool remains enabled after drawing a shape.

### EditPolyOptions

These options will allow you to configure the draw toolbar and its handlers.

| Option | Type | Default | Description
| --- | --- | --- | ---
| featureGroup | [Leaflet FeatureGroup](http://leafletjs.com/reference.html#featuregroup) | `null` | This is the FeatureGroup that stores all editable shapes. **THIS IS REQUIRED FOR THE EDIT TOOLBAR TO WORK**
| edit | [EditHandlerOptions](#edithandleroptions) | `{ }` | Edit handler options. Set to `false` to disable handler.
| remove | [DeleteHandlerOptions](#deletehandleroptions) | `{ }` | Delete handler options. Set to `false` to disable handler.
| poly | [EditPolyOptions](#editpoly) |  `{ }` | Set polygon editing options

#### EditHandlerOptions

| Option | Type | Default | Description
| --- | --- | --- | ---
| selectedPathOptions | [Leaflet Path options](http://leafletjs.com/reference.html#path-options) | [See code](https://github.com/Leaflet/Leaflet.draw/blob/master/src/edit/handler/EditToolbar.Edit.js#L9) | The path options for how the layers will look while in edit mode. If this is set to null the editable path options will not be set.

**Note:** To maintain the original layer color of the layer use `maintainColor: true` within `selectedPathOptions`.

E.g. The edit options below will maintain the layer color and set the edit opacity to 0.3.

````js
{
	selectedPathOptions: {
		maintainColor: true,
		opacity: 0.3
	}
}
````

#### DeleteHandlerOptions

| Option | Type | Default | Description
| --- | --- | --- | ---


#### EditPolyOptions

| Option | Type | Default | Description
| --- | --- | --- | ---
| allowIntersection | Bool | `true` |  Determines if line segments can cross.


#### Customizing language and text in Leaflet.draw

Leaflet.draw uses the `L.drawLocal` configuration object to set any text used in the plugin. Customizing this will allow support for changing the text or supporting another language.

See [Leaflet.draw.js](https://github.com/Leaflet/Leaflet.draw/blob/master/src/Leaflet.draw.js) for the default strings.

E.g.

````js
// Set the button title text for the polygon button
L.drawLocal.draw.toolbar.buttons.polygon = 'Draw a sexy polygon!';

// Set the tooltip start text for the rectangle
L.drawLocal.draw.handlers.rectangle.tooltip.start = 'Not telling...';
````

## Common tasks

The following examples outline some common tasks.

### Example Leaflet.draw config

The following example will show you how to:

1. Change the position of the control's toolbar.
2. Customize the styles of a vector layer.
3. Use a custom marker.
4. Disable the delete functionality.

```js
var cloudmadeUrl = 'http://{s}.tile.cloudmade.com/BC9A493B41014CAABB98F0471D759707/997/256/{z}/{x}/{y}.png',
	cloudmade = new L.TileLayer(cloudmadeUrl, {maxZoom: 18}),
	map = new L.Map('map', {layers: [cloudmade], center: new L.LatLng(-37.7772, 175.2756), zoom: 15 });

var editableLayers = new L.FeatureGroup();
map.addLayer(editableLayers);

var MyCustomMarker = L.Icon.extend({
	options: {
		shadowUrl: null,
		iconAnchor: new L.Point(12, 12),
		iconSize: new L.Point(24, 24),
		iconUrl: 'link/to/image.png'
	}
});

var options = {
	position: 'topright',
	draw: {
		polyline: {
			shapeOptions: {
				color: '#f357a1',
				weight: 10
			}
		},
		polygon: {
			allowIntersection: false, // Restricts shapes to simple polygons
			drawError: {
				color: '#e1e100', // Color the shape will turn when intersects
				message: '<strong>Oh snap!<strong> you can\'t draw that!' // Message that will show when intersect
			},
			shapeOptions: {
				color: '#bada55'
			}
		},
		circle: false, // Turns off this drawing tool
		rectangle: {
			shapeOptions: {
				clickable: false
			}
		},
		marker: {
			icon: new MyCustomMarker()
		}
	},
	edit: {
		featureGroup: editableLayers, //REQUIRED!!
		remove: false
	}
};

var drawControl = new L.Control.Draw(options);
map.addControl(drawControl);

map.on(L.Draw.Event.CREATED, function (e) {
	var type = e.layerType,
		layer = e.layer;

	if (type === 'marker') {
		layer.bindPopup('A popup!');
	}

	editableLayers.addLayer(layer);
});
```

### Changing a drawing handlers options

You can change a draw handlers options after initialisation by using the `setDrawingOptions` method on the Leaflet.draw control.

E.g. to change the colour of the rectangle:

````js
drawControl.setDrawingOptions({
    rectangle: {
    	shapeOptions: {
        	color: '#0000FF'
        }
    }
});
````

### Creating a custom build

If you only require certain handlers (and not the UI), you may wish to create a custom build. You can generate the relevant jake command using the [build html file](https://leaflet.github.io/Leaflet.draw/build/build.html).

See [edit handlers example](https://leaflet.github.io/Leaflet.draw/examples/edithandlers.html) which uses only the edit handlers.

### Testing

To test you can install the npm dependencies:

    npm install

and then use:

    jake test

## Thanks

Touch friendly version of Leaflet.draw was created and maintained by Michael Guild (https://github.com/michaelguild13).

The touch support was initiated due to a demand for it at National Geographic for their Map Maker Projected (http://mapmaker.education.nationalgeographic.com/) that was created by Michael Guild and Daniel Schep (https://github.com/dschep)

Thanks so much to [@brunob](https://github.com/brunob), [@tnightingale](https://github.com/tnightingale), and [@shramov](https://github.com/shramov). I got a lot of ideas from their Leaflet plugins.

All the [contributors](https://github.com/Leaflet/Leaflet.draw/graphs/contributors) and issue reporters of this plugin rock. Thanks for tidying up my mess and keeping the plugin on track.

The icons used for some of the toolbar buttons are either from http://glyphicons.com/ or inspired by them. <3 Glyphicons!

Finally, [@mourner](https://github.com/mourner) is the man! Thanks for dedicating so much of your time to create the gosh darn best JavaScript mapping library around.
