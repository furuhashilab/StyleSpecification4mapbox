## 日本語

## 原文

## Root

{
    "version": 8,
    "name": "Mapbox Streets",
    "sprite": "mapbox://sprites/mapbox/streets-v8",
    "glyphs": "mapbox://fonts/mapbox/{fontstack}/{range}.pbf",
    "sources": {...},
    "layers": [...]
}

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
