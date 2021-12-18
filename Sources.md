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

### [minzoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#vector-minzoom)   
[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。デフォルトは0。   
TileJSON 仕様と同様に、タイルが利用可能な最小ズームレベル。   

### [promoteId](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=the%20TileJSON%20spec.-,promoteId,-Optional%20promoteId.)   
[オプションのpromoteId](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#promoteId)    
フィーチャーのIDとして使用するプロパティ（フィーチャー状態用）。プロパティ名、または {<sourceLayer>.Object> }形式のオブジェクトのどちらかです。
ベクトル タイル ソースに対して文字列として指定した場合、すべてのソース レイヤーで同じプロパティが使用されます。   

### [scheme] (https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=its%20source%20layers.-,scheme,-Optional%20enum.%20One)    
[オプションの列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。xyz", "tms "のうちの1つ。デフォルトは "xyz"。   
タイル座標の y 方向に影響する。グローバルメルカトル（別名球面メルカトル）プロファイルが想定されている。   

- "xyz":   
[Slippyマップ](https://wiki.openstreetmap.org/wiki/JA:%E3%82%B9%E3%83%AA%E3%83%83%E3%83%94%E3%83%BC%E3%83%9E%E3%83%83%E3%83%97)のタイル名スキーム。   

- " tms":   
OSGeo仕様のスキーム   

### [tiles](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#vector-tiles)   
[オプションの文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)。[オプションの配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)   

TileJSON 仕様と同様に、ひとつあるいは複数のタイルソース URL の配列。  

### [url](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#vector-url)   
[オプションの文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)   
TileJSONリソースへのURL。サポートされている通信プロトコルは、http:、https:、および mapbox://<"TilesetID">。   

### [volatile](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#vector-volatile)   
[オプションのブール値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトはfalse。   
ソースのタイルをローカルにキャッシュするかどうかを決定するための設定。   
|  SDK Support |  Mapbox GL JS  |  Android SDK  |  iOS SDK | macOS SDK  |
| ---- | ---- | ---- | ---- | ---- |
|  基本設定通り  |  サポートされていません  |  >= 9.3.0 |  >= 5.10.0  |  サポートされていません  |        

# [raster](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster)   
Mapbox がホストするラスタータイルの場合、"url" 値は mapbox://tilesetid の形式である必要があります。   

```
"mapbox-satellite": {
    "type": "raster",
    "url": "mapbox://mapbox.satellite",
    "tileSize": 256
}   
```   

|  SDK Support |  Mapbox GL JS  |  Android SDK  |  iOS SDK | macOS SDK  |
| ---- | ---- | ---- | ---- | ---- |
|  基本設定通り  |  >= 0.10.0  |  >= 2.0.1 |  >= 2.0.0  |  >= 0.1.0 |   

### [attribution](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-attribution)   

 [オプション](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)   
マップがユーザーに表示されるときに表示される属性を記載します。   

### [bounds](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-bounds)   
[オプションの数値の配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)デフォルトは 「-180,-85.051129,180,85.051129」で設定されています。   

ソースの[バウンディングボックス](https://wiki.openstreetmap.org/wiki/JA:Bounding_Box)の南西および北東の角の経度と緯度を、以下の順序で設定します。[sw.lng, sw.lat, ne.lng, ne.lat]。このプロパティがソースに含まれている場合、指定した境界の外側のタイルは Mapbox GL によって要求されません。   

### [maxzoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-maxzoom)   
[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは22。   

タイルが利用可能な最大ズームレベル。maxzoomのタイルからのデータは、より高いズームレベルでマップを表示する際に使用される。   

### [minzoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-minzoom)   
[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。デフォルトは0。   
TileJSON 仕様と同様に、タイルが利用可能な最小ズームレベル。   

### [scheme] (https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=the%20TileJSON%20spec.-,scheme,-Optional%20enum.%20One)    
[オプションの列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。xyz", "tms "のうちの1つ。デフォルトは "xyz"。   
タイル座標の y 方向に影響する。グローバルメルカトル（別名球面メルカトル）プロファイルが想定されている。   

- "xyz":   
[Slippyマップ](https://wiki.openstreetmap.org/wiki/JA:%E3%82%B9%E3%83%AA%E3%83%83%E3%83%94%E3%83%BC%E3%83%9E%E3%83%83%E3%83%97)のタイル名スキーム。   

- " tms":   
OSGeo仕様のスキーム   

### [tiles](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-tiles)   
[オプションの文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)。[オプションの配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)   

TileJSON 仕様と同様に、ひとつあるいは複数のタイルソース URL の配列。  

### [tileSize](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-tileSize)   
[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。単位はピクセル。デフォルトは512。   
レイヤーのタイルを表示するための最小視覚サイズ。ラスターレイヤーに対してのみ設定可能。   


### [url](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-url)   
[オプションの文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)      
TileJSONリソースへのURL。サポートされている通信プロトコルは、http:、https:、および mapbox://<"TilesetID">。   

### [volatile](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-volatile)   
[オプションのブール値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトはfalse。   
ソースのタイルをローカルにキャッシュするかどうかを決定するための設定。   
|  SDK Support |  Mapbox GL JS  |  Android SDK  |  iOS SDK | macOS SDK  |
| ---- | ---- | ---- | ---- | ---- |
|  基本設定通り  |  サポートされていません  |  >= 9.3.0 |  >= 5.10.0  |  サポートされていません  |    

# [raster-dem](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-dem)   
[Mapbox Terrain-DEM](mapbox://mapbox.mapbox-terrain-dem-v1) のみサポートしています。   

```
"mapbox-terrain-dem-v1": {
    "type": "raster-dem",
    "url": "mapbox://mapbox.mapbox-terrain-dem-v1"
}   
```   


















