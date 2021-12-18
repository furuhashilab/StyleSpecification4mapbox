## 日本語

# レイヤー
スタイルのレイヤー プロパティには、そのスタイルで使用できるすべてのレイヤーが一覧表示されます。レイヤーの種類は type 属性で指定し、background、fill、line、symbol、raster、circle、fill-extrusion、heatmap、hillsshade、sky のいずれかを指定する必要があります。

background または sky タイプのレイヤーを除いて、各レイヤーはソースを参照する必要があります。レイヤーは[ソース](https://docs.mapbox.com/help/glossary/source/)から取得したデータを受け取り、オプションでフィーチャーをフィルタリングし、それらのフィーチャーがどのようにスタイリングされるかを定義します。

以下は、[スタイル](https://docs.mapbox.com/help/glossary/style/)に含まれる可能性のあるレイヤーオブジェクトの例です。
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
## [レイヤープロパティ](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layer-properties)
### [id](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#id)

必須の[文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)です。

一意なレイヤー名です。

### [タイプ](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#type)
[列挙](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)は必須です。fill", "line", "symbol", "circle", "heatmap", "fill-extrusion", "raster", "hillshade", "background", "sky "のいずれか。

このレイヤーのレンダリングタイプ。

"fill":
塗りつぶされた多角形で、オプションで描画された境界線があります。

"line"：
描画された線。

"symbol":
アイコンまたはテキストラベル。

"circle":
塗りつぶした円。

"heatmap": 
ヒートマップ。

"fill-extrusion":
押し出し（3D）ポリゴン。

"ラスター": 
衛星画像などのラスターマップテクスチャ。

"hillsshade"：
DEMデータに基づくクライアントサイドのヒルシェード視覚化。現在のところ、Mapbox Terrain RGB と Mapzen Terrarium タイルのみをサポートする実装になっています。

"background"（背景）：
マップの背景色またはパターン。

"sky":
マップを囲む球状のドームで、常に他のすべてのレイヤーの後ろにレンダリングされます。

### [フィルター](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#filter)
オプションの[式](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/)

ソースフィーチャーに対する条件を指定する式。フィルタに一致するフィーチャーのみが表示される。フィルタに含まれるズーム式は、整数のズームレベルにおいてのみ評価される。フィルター式では ["feature-state", ...] 式はサポートされていません。ピッチ] および [中心からの距離] 式は、シンボル レイヤーのフィルター式でのみサポートされています。

### [レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout)
オプションでレイアウトを指定します。

レイヤーのレイアウトプロパティ。

### [最大ズーム](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#maxzoom)
0から24までの[数字](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)

レイヤーの最大ズームレベル。maxzoomと同じかそれ以上のズームレベルでは、レイヤーは非表示になります。

### [メタデータ](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#metadata)
任意。

レイヤーを追跡するのに便利な任意のプロパティですが、レンダリングに影響を与えるものではありません。プロパティは 'mapbox:' のように、衝突を避けるためにプレフィックスを付ける必要があります。

### [最小ズーム](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#minzoom)
0から24までの数字（オプション）。

レイヤーの最小ズームレベル。minzoomより小さいズームレベルでは、レイヤーは隠されます。

### [ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint)
オプションで[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)を指定します。

このレイヤーのデフォルトのペイントプロパティ。

### [ソース](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#source)
オプションの[文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)

このレイヤーに使用されるソース記述の名前。背景を除くすべてのレイヤーの種類で必要です。

### [ソースレイヤー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#source-layer)
オプションの[文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)

ベクタータイルソースから使用するレイヤー。ベクトルタイルソースでは必須、GeoJSON ソースを含む他のすべてのソース タイプでは禁止です。

## [レイヤーのサブプロパティ](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layer-sub-properties)
レイヤーには、そのレイヤーからのデータのレンダリング方法を決定する2つのサブプロパティがあります。レイアウトとペイントプロパティです。

• レイアウトプロパティは、レイヤーの "レイアウト" オブジェクトに表示されます。レイアウトプロパティはレンダリング処理の初期に適用され、そのレイヤーのデータが GPU にどのように渡されるかを定義します。レイアウトプロパティを変更するには、非同期の「レイアウト」手順が必要です。

• ペイントプロパティはレンダリングプロセスの後半に適用されます。ペイントプロパティはレイヤーの "ペイント" オブジェクトに表示されます。ペイントプロパティへの変更は安価で、同期的に行われます。

## [バックグラウンド](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#background)
backgroundスタイル層は、マップ全体をカバーしています。背景スタイルレイヤーを使用して、他のすべてのマップコンテンツの下に表示される色またはパターンを構成します。背景レイヤーが透明であるか、スタイルから省略されている場合、別のスタイルレイヤーを表示しないマップビューの部分は透明です。

### [背景色](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#source-layer)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。 オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは "#000000"。background-patternによって無効にされています。[補完](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

背景が描画される色。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [背景の不透明度](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-background-background-opacity)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。 "0"から"1"までのオプションの数値。デフォルトは"1"。[補完](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。
背景が描画される不透明度。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [背景パターン](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-background-background-pattern)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[解決された画像](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#resolvedImage)。
画像の背景を描画するために使用するスプライト内の画像の名前。シームレスパターンの場合、画像の幅と高さは2倍（2、4、8、...、512）である必要があります。ズームに依存する式は、整数のズームレベルでのみ評価されることに注意してください。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | まだサポートされていません  | まだサポートされていません  | まだサポートされていません | まだサポートされていません  |

### [視認性](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-background-visibility)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。 "visible"、"none"のいずれか。 デフォルトは"visible"です。

このレイヤーが表示されるかどうか。
"visible"：
レイヤーが表示されます。
"none"：
レイヤーは表示されていません。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

## [塗りつぶし](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#fill)


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
## [Layer properties](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layer-properties)
### [id](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#id)

Required [string](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string).

Unique layer name.

### [type](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#type)
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

### [filter](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#filter)
Optional [expression](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/).

An expression specifying conditions on source features. Only features that match the filter are displayed. Zoom expressions in filters are only evaluated at integer zoom levels. The ["feature-state", ...] expression is not supported in filter expressions. The ["pitch"] and ["distance-from-center"] expressions are supported only for filter expressions on the symbol layer.

### [layout](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout)
Optional [layout](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property).

Layout properties for the layer.

### [maxzoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#maxzoom)
Optional [number](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number) between 0 and 24 inclusive.

The maximum zoom level for the layer. At zoom levels equal to or greater than the maxzoom, the layer will be hidden.

### [metadata](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#metadata)
Optional.

Arbitrary properties useful to track with the layer, but do not influence rendering. Properties should be prefixed to avoid collisions, like 'mapbox:'.

### [minzoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#minzoom)
Optional number between 0 and 24 inclusive.

The minimum zoom level for the layer. At zoom levels less than the minzoom, the layer will be hidden.

### [paint](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint)
Optional [paint](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property).

Default paint properties for this layer.

### [source](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#source)
Optional [string](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string).

Name of a source description to be used for this layer. Required for all layer types except background.

### [source-layer](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#source-layer)
Optional [string](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string).

Layer to use from a vector tile source. Required for vector tile sources; prohibited for all other source types, including GeoJSON sources.

## [Layer sub-properties](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layer-sub-properties)
Layers have two sub-properties that determine how data from that layer is rendered: layout and paint properties.

• Layout properties appear in the layer's "layout" object. They are applied early in the rendering process and define how data for that layer is passed to the GPU. Changes to a layout property require an asynchronous "layout" step.

• Paint properties are applied later in the rendering process. Paint properties appear in the layer's "paint" object. Changes to a paint property are cheap and happen synchronously.


