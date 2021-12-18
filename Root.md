## 日本語

## 原文

## Root

Root level properties of a Mapbox style specify the map's layers, tile sources and other resources, and default values for the initial camera position when not specified elsewhere.
```
{
    "version": 8,
    "name": "Mapbox Streets",
    "sprite": "mapbox://sprites/mapbox/streets-v8",
    "glyphs": "mapbox://fonts/mapbox/{fontstack}/{range}.pbf",
    "sources": {...},
    "layers": [...]
}
```

There are some root level properties, including owner and modified, that are not documented here because they do not affect how a style is rendered. For the full list of these properties and their descriptions, see the [example style object](https://docs.mapbox.com/api/maps/styles/#the-style-object) in the Mapbox Styles API documentation.

## [layers](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/?fbclid=IwAR0NUepnn4i-OW34EZ54LHmtel9cBS9pweaT3o1KsHkbCit_sKf4B14vltM#layers)
Required [array](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array) of [layers](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/).

Layers will be drawn in the order of this array.

```
"layers": [
  {
    "id": "water",
    "source": "mapbox-streets",
    "source-layer": "water",
    "type": "fill",
    "paint": {
      "fill-color": "#00ffff"
    }
  }
]
```

## [sources](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/?fbclid=IwAR0NUepnn4i-OW34EZ54LHmtel9cBS9pweaT3o1KsHkbCit_sKf4B14vltM#sources)
Required object with [source](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/) values.
Data source specifications.
```
"sources": {
  "mapbox-streets": {
    "type": "vector",
    "url": "mapbox://mapbox.mapbox-streets-v6"
  }
}
```

## [version](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/?fbclid=IwAR0NUepnn4i-OW34EZ54LHmtel9cBS9pweaT3o1KsHkbCit_sKf4B14vltM#version)
Required [enum](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum).
Style specification version number. Must be 8.
```
"version": 8
```

## [bearing](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/?fbclid=IwAR0NUepnn4i-OW34EZ54LHmtel9cBS9pweaT3o1KsHkbCit_sKf4B14vltM#bearing)
Optional [number](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number). Units in degrees. Defaults to 0.
Default bearing, in degrees. The bearing is the compass direction that is "up"; for example, a bearing of 90° orients the map so that east is up. This value will be used only if the map has not been positioned by other means (e.g. map options or user interaction).
```
"bearing": 29
```

## [center](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#center)
Optional [array](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array) of [numbers](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number).
Default map center in longitude and latitude. The style center will be used only if the map has not been positioned by other means (e.g. map options or user interaction).
```
"center": [
  -73.9749,
  40.7736
]
```

## [fog](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#fog)
Optional [fog](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#fog).
A global effect that fades layers and markers based on their distance to the camera. The fog can be used to approximate the effect of atmosphere on distant objects and enhance the depth perception of the map when used with terrain or 3D features.

## [glyphs](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#glyphs)
Optional [string](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string).
A URL template for loading signed-distance-field glyph sets in PBF format. The URL must include ```{fontstack} ```and ```{range} ```tokens. This property is required if any layer uses the ```text-field``` layout property. The URL must be absolute, containing the [scheme, authority and path components](https://en.wikipedia.org/wiki/URL#Syntax).
```"glyphs": "mapbox://fonts/mapbox/{fontstack}/{range}.pbf"```
