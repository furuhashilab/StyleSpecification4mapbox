## 日本語

#  Sources

マップまたはレイヤーのソースは、マップがどのデータを表示すべきかを指定します。ソースの種類は "type" プロパティで指定し、vector, raster, raster-dem, geojson, image, video のいずれかである必要があります。

[ソース](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=A-,source,-provides%20map%20data)は地図データを提供し、Mapbox GL JS の[スタイル](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=can%20use%20with%20a-,style,-document%20to%20render)ドキュメントを使用することにより様々な視覚化表現を行うことができます。スタイルドキュメントで紹介されているユースケースを用いることで高速道路レイヤーの異なるタイプの道路の外観を区別するなど、同じソースに異なる方法でスタイルを設定することが可能になります。

' スタイルの指定  
地図やレイヤにソースを追加するだけでは、データを地図上に表示することはできません。また、各フィーチャー(道路や建物など）の色や幅などのプロパティを指定するために、スタイルを指定する必要があります。'

### [Tiled sources](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#tiled-sources)

タイル状の地図データ（ベクトルおよびラスター）は、TileJSON の仕様に従って詳細を指定する必要があります。指定する方法はいくつかあり、以下にその方法を記載します。

- "tiles"、"minzoom"、"maxzoom "などの TileJSON プロパティをソースに直接指定する方法。

```
"mapbox-streets": {
    "type": "vector",
    "tiles": [
        "http://a.example.com/tiles/{z}/{x}/{y}.pbf",
        "http://b.example.com/tiles/{z}/{x}/{y}.pbf"
    ],
    "maxzoom": 14
}
```

- TileJSON リソースへの "url "を提供する方法

```
"mapbox-streets": {
    "type": "vector",
    "url": "http://api.example.com/tilejson.json"
}
```

- タイル型データのソースとしてEPSG:3857（またはEPSG:900913）をサポートするWMSサーバーへのURLを提供する方法。サーバーのURLには、bboxパラメータを供給するための「{box-epsg-3857}」置換トークンを含める必要があります。

```
"wms-imagery": {
    "type": "raster",
    "tiles": [
        "http://a.example.com/wms?bbox={bbox-epsg-3857}&format=image/png&service=WMS&version=1.1.1&request=GetMap&srs=EPSG:3857&width=256&height=256&layers=example"
    ],
    "tileSize": 256
}
```

# [vector](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=example%22%0A%20%20%20%20%5D%2C%0A%20%20%20%20%22tileSize%22%3A%20256%0A%7D-,vector,-A%20vector%20tile)   

タイルは Mapbox Vector Tile 形式である必要があります。ベクタータイルのすべての幾何学座標は、-1 * extent と (extent * 2) - 1 の間で設定する必要があります。ベクターソースを使用するすべてのレイヤーは、"source-layer" 値を指定する必要があります。Mapboxによってホストされるベクタータイルの場合、"url "値は "mapbox://tilesetid" の形式でなければなりません。   

```
"mapbox-streets": {
    "type": "vector",
    "url": "mapbox://mapbox.mapbox-streets-v6"
}
```

|  SDK Support |  Mapbox GL JS  |  Android SDK  |  iOS SDK | macOS SDK  |
| ---- | ---- | ---- | ---- | ---- |
|  基本設定通り  |  >= 0.10.0  |  >= 2.0.1  |  >= 2.0.0  |  >= 0.1.0  |    


### [attribution](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#vector-attribution)   

 [オプション](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)   
マップがユーザーに表示されるときに表示される属性を記載します。   

### [bounds](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#vector-bounds)   
[オプションの数値の配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)デフォルトは 「-180,-85.051129,180,85.051129」で設定されています。   

ソースの[バウンディングボックス](https://wiki.openstreetmap.org/wiki/JA:Bounding_Box)の南西および北東の角の経度と緯度を、以下の順序で設定します。[sw.lng, sw.lat, ne.lng, ne.lat]。このプロパティがソースに含まれている場合、指定した境界の外側のタイルは Mapbox GL によって要求されません。   

### [maxzoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#vector-maxzoom)   
[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは22。   

タイルが利用可能な最大ズームレベル。maxzoomのタイルからのデータは、より高いズームレベルでマップを表示する際に使用される。





