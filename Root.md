## 日本語

## Root
Mapbox スタイルのルート レベルのプロパティは、マップのレイヤー、タイル ソース、その他のリソースを指定し、他に指定がない場合はカメラの初期位置のデフォルト値を指定します。
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
owner や modified などのルート レベルのプロパティがありますが、これらはスタイルのレンダリング方法には影響しないため、ここではドキュメント化されていません。これらのプロパティの完全なリストとその説明については、Mapbox Styles API [ドキュメントのサンプル スタイル オブジェクト](https://docs.mapbox.com/api/maps/styles/#the-style-object)を参照してください。

## [layer](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#layers)
必要な[layer](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/)の[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)

レイヤーはこの配列の順番で書かれます。
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
## [source](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#sources)
[ソース](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/)での必須項目

データソースの仕様
```
"sources": {
  "mapbox-streets": {
    "type": "vector",
    "url": "mapbox://mapbox.mapbox-streets-v6"
  }
}
```
## [version](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#version)
[enum](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)が必須

スタイル指定番号は必ず8にする。
```
"version": 8
```
## [bearing](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#bearing)
オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)は初期設定は0で単位は度

初期設定の方位でコンパスの「上」の数値です。例えば、方位90°の時は東が上になるように地図を配置します。この値は、他の手段（マップオプションやユーザー操作など）で地図が配置されていない場合にのみ使用されます。
```
"bearing": 29
```
## [center](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#center)
[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)の任意[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)

デフォルトの地図の中心。このスタイルの中心は、他の手段 (マップ オプションやユーザー インタラクションなど) によってマップの位置が設定されていない場合にのみ使用されます。
```
"center": [
  -73.9749,
  40.7736
]
```
## [fog](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#fog)
[霧](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#fog)のオプション

レイヤーやマーカーをカメラとの距離に応じてフェードさせるグローバルエフェクトです。フォグは、地形や3D建造物と併用することで、遠くのオブジェクトに対する大気の効果を近似的に表現し、マップの奥行き感を強調することができます。
## [glyphs](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#glyphs)
オプションの[文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)

PBF 形式の符号付き距離フィールドグリフセットを読み込むためのURLのテンプレートです。URLは```{fontstack}```と```{range}```トークンを含む必要があ り ます。このプロパティは、いずれかのレイヤーで```text-field layout```プロパティが使われている場合に必要です。URL は絶対的なものでなければならず、[scheme、authority、path](https://en.wikipedia.org/wiki/URL#Syntax) の各要素を含んでいなければなりません。
```
"glyphs": "mapbox://fonts/mapbox/{fontstack}/{range}.pbf"
```
## [light](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#light)
[光](https://docs.mapbox.com/mapbox-gl-js/style-spec/light/)のオプション

世界共通のライトオプション
```
"light": {
  "anchor": "viewport",
  "color": "white",
  "intensity": 0.4
}
```
## [metadeta](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#metadata)
オプション

スタイルシートで追跡するのに役立つが、レンダリングには影響しない任意のプロパティ。プロパティは 'mapbox:' のように衝突を避けるためにプレフィックスを付ける必要があります。
## [name](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#name)
オプションの[文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)

人間にとって読みやすいスタイルの名前
```
"name": "Bright"
```
## [pitch](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#pitch)
オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。単位は°。デフォルトは０

デフォルトのピッチを度数で指定します。0 は地表に垂直で、マップを真下に見ることができ、60 のような大きな値は水平線に向かって前方を見ることができます。このスタイルピッチは、マップが他の手段（マップオプションやユーザーとの対話など）で位置決めされていない場合にのみ使用されます。
```
"pitch": 50
```
## [projection](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#projection)
オプションの[プロジェクター](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#projection)

地図がレンダリングされる投影図。サポートされている投影法は、Albers, Equal Earth, Equirectangular (WGS84), Lambert conformal conic, Mercator, Natural Earth, および Winkel Tripel です。地形、霧、空、CustomLayerInterfaceは、mercator以外の投影ではサポートされていません。
```
"projection": {
  "name": "albers",
  "center": [
    -154,
    50
  ],
  "parallels": [
    55,
    65
  ]
}
```
## [sprite](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#sprite)
[地形](https://docs.mapbox.com/mapbox-gl-js/style-spec/terrain/)のオプション

DEMデータソースを元にレイヤーやマーカーを映し出させるグローバルモディファイアです。
## [transition](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#transition)
オプションの[トランジション](https://docs.mapbox.com/mapbox-gl-js/style-spec/transition/)

プロパティ固有の遷移が設定されていない場合に、ある値と次の値との間のタイミング遷移に使用される、プロパティ間でデフォルトとして使用するグローバルな遷移定義です。衝突に基づく記号のフェージングは、スタイルの```transition```プロパティとは独立して制御されます。
```
"transition": {
  "duration": 300,
  "delay": 0
}
```
## [zoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#zoom)
オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)

デフォルトのズームレベル。スタイルズームは,マップオプションやユーザーインタラクションなどによってマップの位置が決定されなかった場合にのみ使用されます。
```
"zoom": 12.5
```

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
```
"glyphs": "mapbox://fonts/mapbox/{fontstack}/{range}.pbf"
```

## [light](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#light)
Optional [light](https://docs.mapbox.com/mapbox-gl-js/style-spec/light/).

The global light source.
```
"light": {
  "anchor": "viewport",
  "color": "white",
  "intensity": 0.4
}
```

## [metadata](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#metadata)
Optional.

Arbitrary properties useful to track with the stylesheet, but do not influence rendering. Properties should be prefixed to avoid collisions, like 'mapbox:'.

## [neme](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#name)
Optional [string](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string).

A human-readable name for the style.
```"name": "Bright"```

## [pitch](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#pitch)
Optional [number](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number). Units in degrees. Defaults to 0.

Default pitch, in degrees. Zero is perpendicular to the surface, for a look straight down at the map, while a greater value like 60 looks ahead towards the horizon. The style pitch will be used only if the map has not been positioned by other means (e.g. map options or user interaction).
```"pitch": 50```

## [projection](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#projection)
Optional [projection](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#projection).

The projection the map should be rendered in. Suported projections are Albers, Equal Earth, Equirectangular (WGS84), Lambert conformal conic, Mercator, Natural Earth, and Winkel Tripel. Terrain, fog, sky and CustomLayerInterface are not supported for projections other than mercator.
```
"projection": {
  "name": "albers",
  "center": [
    -154,
    50
  ],
  "parallels": [
    55,
    65
  ]
}
```

## [sprite](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#sprite)
Optional [string](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string).

A base URL for retrieving the sprite image and metadata. The extensions ```.png```, ```.json``` and scale factor ```@2x.png``` will be automatically appended. This property is required if any layer uses the ```background-pattern```, ```fill-pattern```, ```line-pattern```, ```fill-extrusion-pattern```, or ```icon-image``` properties. The URL must be absolute, containing the [scheme, authority and path components](https://en.wikipedia.org/wiki/URL#Syntax).
```
"sprite": "mapbox://sprites/mapbox/bright-v8"
```

## [terrain](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#terrain)
Optional [terrain](https://docs.mapbox.com/mapbox-gl-js/style-spec/terrain/).

A global modifier that elevates layers and markers based on a DEM data source.

## [transition](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#transition)
Optional [transition](https://docs.mapbox.com/mapbox-gl-js/style-spec/transition/).

A global transition definition to use as a default across properties, to be used for timing transitions between one value and the next when no property-specific transition is set. Collision-based symbol fading is controlled independently of the style's ```transition``` property.
```
"transition": {
  "duration": 300,
  "delay": 0
}
```

## [zoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#zoom)
Optional [number](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number).

Default zoom level. The style zoom will be used only if the map has not been positioned by other means (e.g. map options or user interaction).
```
"zoom": 12.5
```
