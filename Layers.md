## 日本語

## 原文

# Layers

A style's layers property lists all the layers available in that style. The type of layer is specified by the "type" property, and must be one of background, fill, line, symbol, raster, circle, fill-extrusion, heatmap, hillshade, sky.

Except for layers of the background or sky types, each layer must refer to a source. Layers take the data that they get from a [source](https://docs.mapbox.com/help/glossary/source/), optionally filter features, and then define how those features are styled.

Here is an example layers object which could be included in a [style](https://docs.mapbox.com/help/glossary/style/):
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
## Layer properties
### id
Required [string](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string).
Unique layer name.

### type
Required [enum](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum). One of "fill", "line", "symbol", "circle", "heatmap", "fill-extrusion", "raster", "hillshade", "background", "sky".

Rendering type of this layer.

"fill":
A filled polygon with an optional stroked border.

"line":
A stroked line.

"symbol":
An icon or a text label.

"circle":
A filled circle.

"heatmap":
A heatmap.

"fill-extrusion":
An extruded (3D) polygon.

"raster":
Raster map textures such as satellite imagery.

"hillshade":
Client-side hillshading visualization based on DEM data. Currently, the implementation only supports Mapbox Terrain RGB and Mapzen Terrarium tiles.

"background":
The background color or pattern of the map.

"sky":
A spherical dome around the map that is always rendered behind all other layers.

### filter
Optional [expression](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/).

An expression specifying conditions on source features. Only features that match the filter are displayed. Zoom expressions in filters are only evaluated at integer zoom levels. The ["feature-state", ...] expression is not supported in filter expressions. The ["pitch"] and ["distance-from-center"] expressions are supported only for filter expressions on the symbol layer.

### layout
Optional [layout](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property).

Layout properties for the layer.

### maxzoom
Optional [number](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number) between 0 and 24 inclusive.

The maximum zoom level for the layer. At zoom levels equal to or greater than the maxzoom, the layer will be hidden.

### metadata
Optional.

Arbitrary properties useful to track with the layer, but do not influence rendering. Properties should be prefixed to avoid collisions, like 'mapbox:'.

### minzoom
Optional number between 0 and 24 inclusive.

The minimum zoom level for the layer. At zoom levels less than the minzoom, the layer will be hidden.

### paint
Optional [paint](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property).

Default paint properties for this layer.

### source
Optional [string](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string).

Name of a source description to be used for this layer. Required for all layer types except background.

### source-layer
Optional [string](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string).

Layer to use from a vector tile source. Required for vector tile sources; prohibited for all other source types, including GeoJSON sources.

## Layer sub-properties
Layers have two sub-properties that determine how data from that layer is rendered: layout and paint properties.

• Layout properties appear in the layer's "layout" object. They are applied early in the rendering process and define how data for that layer is passed to the GPU. Changes to a layout property require an asynchronous "layout" step.
• Paint properties are applied later in the rendering process. Paint properties appear in the layer's "paint" object. Changes to a paint property are cheap and happen synchronously.


