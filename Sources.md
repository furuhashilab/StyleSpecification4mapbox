## 日本語

# Sources

ソース（Sources）は、マップ表示するデータのことを指します。ソースの種類は "type" プロパティで指定し、vector, raster, raster-dem, geojson, image, video のいずれかである必要があります。

[ソース](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=A-,source,-provides%20map%20data)は地図データを提供し、Mapbox GL JS の[スタイル](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=can%20use%20with%20a-,style,-document%20to%20render)ドキュメントを使用することにより様々な視覚化表現を行うことができます。スタイルドキュメントで紹介されているユースケースを用いることで高速道路と一般道レイヤーの異なるタイプの道路の外観を区別するなど、同じソースに異なる方法でスタイルを設定することが可能になります。

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

- タイル型データのソースとして EPSG:3857（または EPSG:900913）をサポートする WMS サーバーへの URL を提供する方法。サーバーの URL には、box パラメータを供給するための「{box-epsg-3857}」置換トークンを含める必要があります。

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

タイルは Mapbox Vector Tile 形式である必要があります。ベクタータイルのすべての幾何学座標は、-1 _ extent と (extent _ 2) - 1 の間で設定する必要があります。ベクターソースを使用するすべてのレイヤーは、"source-layer" 値を指定する必要があります。Mapbox によってホストされるベクタータイルの場合、"url "値は "mapbox://tilesetid" の形式でなければなりません。

```
"mapbox-streets": {
    "type": "vector",
    "url": "mapbox://mapbox.mapbox-streets-v6"
}
```

| SDK Support  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本設定通り | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [attribution](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#vector-attribution)

[オプション](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)  
マップがユーザーに表示されるときに表示される属性を記載します。

### [bounds](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#vector-bounds)

[オプションの数値の配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)デフォルトは 「-180,-85.051129,180,85.051129」で設定されています。

ソースの[バウンディングボックス](https://wiki.openstreetmap.org/wiki/JA:Bounding_Box)の南西および北東の角の経度と緯度を、以下の順序で設定します。[sw.lng, sw.lat, ne.lng, ne.lat]。このプロパティがソースに含まれている場合、指定した境界の外側のタイルは Mapbox GL によって要求されません。

### [maxzoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#vector-maxzoom)

[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは 22。

タイルが利用可能な最大ズームレベル。maxzoom のタイルからのデータは、より高いズームレベルでマップを表示する際に使用される。

### [minzoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#vector-minzoom)

[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。デフォルトは 0。  
TileJSON 仕様と同様に、タイルが利用可能な最小ズームレベル。

### [promoteId](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=the%20TileJSON%20spec.-,promoteId,-Optional%20promoteId.)

[オプションの promoteId](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#promoteId)  
フィーチャーの ID として使用するプロパティ（フィーチャー状態用）。プロパティ名、または {<sourceLayer>.Object> }形式のオブジェクトのどちらかです。
ベクトル タイル ソースに対して文字列として指定した場合、すべてのソース レイヤーで同じプロパティが使用されます。

### [scheme](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=its%20source%20layers.-,scheme,-Optional%20enum.%20One)

[オプションの列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。xyz", "tms "のうちの 1 つ。デフォルトは "xyz"。  
タイル座標の y 方向に影響する。グローバルメルカトル（別名球面メルカトル）プロファイルが想定されている。

- "xyz":  
  [Slippy マップ](https://wiki.openstreetmap.org/wiki/JA:%E3%82%B9%E3%83%AA%E3%83%83%E3%83%94%E3%83%BC%E3%83%9E%E3%83%83%E3%83%97)のタイル名スキーム。

- " tms":  
  OSGeo 仕様のスキーム

### [tiles](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#vector-tiles)

[オプションの文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)。[オプションの配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)

TileJSON 仕様と同様に、ひとつあるいは複数のタイルソース URL の配列。

### [url](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#vector-url)

[オプションの文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)  
TileJSON リソースへの URL。サポートされている通信プロトコルは、http:、https:、および mapbox://<"TilesetID">。

### [volatile](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#vector-volatile)

[オプションのブール値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは false。  
ソースのタイルをローカルにキャッシュするかどうかを決定するための設定。  
| SDK Support | Mapbox GL JS | Android SDK | iOS SDK | macOS SDK |
| ---- | ---- | ---- | ---- | ---- |
| 基本設定通り | サポートされていません | >= 9.3.0 | >= 5.10.0 | サポートされていません |

# [raster](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster)

Mapbox がホストするラスタータイルの場合、"url" 値は mapbox://tilesetid の形式である必要があります。

```
"mapbox-satellite": {
    "type": "raster",
    "url": "mapbox://mapbox.satellite",
    "tileSize": 256
}
```

| SDK Support  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本設定通り | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [attribution](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-attribution)

[オプション](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)  
マップがユーザーに表示されるときに表示される属性を記載します。

### [bounds](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-bounds)

[オプションの数値の配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)デフォルトは 「-180,-85.051129,180,85.051129」で設定されています。

ソースの[バウンディングボックス](https://wiki.openstreetmap.org/wiki/JA:Bounding_Box)の南西および北東の角の経度と緯度を、以下の順序で設定します。[sw.lng, sw.lat, ne.lng, ne.lat]。このプロパティがソースに含まれている場合、指定した境界の外側のタイルは Mapbox GL によって要求されません。

### [maxzoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-maxzoom)

[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは 22。

タイルが利用可能な最大ズームレベル。maxzoom のタイルからのデータは、より高いズームレベルでマップを表示する際に使用される。

### [minzoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-minzoom)

[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。デフォルトは 0。  
TileJSON 仕様と同様に、タイルが利用可能な最小ズームレベル。

### [scheme](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=the%20TileJSON%20spec.-,scheme,-Optional%20enum.%20One)

[オプションの列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。xyz", "tms "のうちの 1 つ。デフォルトは "xyz"。  
タイル座標の y 方向に影響する。グローバルメルカトル（別名球面メルカトル）プロファイルが想定されている。

- "xyz":  
  [Slippy マップ](https://wiki.openstreetmap.org/wiki/JA:%E3%82%B9%E3%83%AA%E3%83%83%E3%83%94%E3%83%BC%E3%83%9E%E3%83%83%E3%83%97)のタイル名スキーム。

- " tms":  
  OSGeo 仕様のスキーム

### [tiles](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-tiles)

[オプションの文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)。[オプションの配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)

TileJSON 仕様と同様に、ひとつあるいは複数のタイルソース URL の配列。

### [tileSize](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-tileSize)

[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。単位はピクセル。デフォルトは 512。  
レイヤーのタイルを表示するための最小視覚サイズ。ラスターレイヤーに対してのみ設定可能。

### [url](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-url)

[オプションの文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)  
TileJSON リソースへの URL。サポートされている通信プロトコルは、http:、https:、および mapbox://<"TilesetID">。

### [volatile](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-volatile)

[オプションのブール値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは false。  
ソースのタイルをローカルにキャッシュするかどうかを決定するための設定。  
| SDK Support | Mapbox GL JS | Android SDK | iOS SDK | macOS SDK |
| ---- | ---- | ---- | ---- | ---- |
| 基本設定通り | サポートされていません | >= 9.3.0 | >= 5.10.0 | サポートされていません |

# [raster-dem](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-dem)

[Mapbox Terrain-DEM](mapbox://mapbox.mapbox-terrain-dem-v1) のみサポートしています。

```
"mapbox-terrain-dem-v1": {
    "type": "raster-dem",
    "url": "mapbox://mapbox.mapbox-terrain-dem-v1"
}
```

| SDK Support  | Mapbox GL JS | Android SDK            | iOS SDK                | macOS SDK              |
| ------------ | ------------ | ---------------------- | ---------------------- | ---------------------- |
| 基本設定通り | >= 0.43.0    | サポートされていません | サポートされていません | サポートされていません |

### [attribution](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=Not%20yet%20supported-,attribution,-Optional%20string.)

[オプション](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)  
マップがユーザーに表示されるときに表示される属性を記載します。

### [bounds](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-bounds)

[オプションの数値の配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)デフォルトは 「-180,-85.051129,180,85.051129」で設定されています。

ソースの[バウンディングボックス](https://wiki.openstreetmap.org/wiki/JA:Bounding_Box)の南西および北東の角の経度と緯度を、以下の順序で設定します。[sw.lng, sw.lat, ne.lng, ne.lat]。このプロパティがソースに含まれている場合、指定した境界の外側のタイルは Mapbox GL によって要求されません。

### [encoding](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-dem-encoding)

[オプションの列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=Optional-,enum,-.%20One%20of%20%22terrarium)。terrarium", "mapbox "のいずれかを選択可能。デフォルトは "mapbox" 。  
エンコーディングする際に使われるソース。デフォルトでは Mapbox Terrain RGB が使用されます。

- "terrarium"  
  Terrarium 形式の PNG タイル。詳しくは [こちら](https://aws.amazon.com/es/public-datasets/terrain/)を参照してください。

- "mapbox"  
  Mapbox 地形 RGB タイル。詳しくは[こちら](https://www.mapbox.com/help/access-elevation-data/#mapbox-terrain-rgb)を参照してください。

### [maxzoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-dem-maxzoom)

[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは 22。

タイルが利用可能な最大ズームレベル。maxzoom のタイルからのデータは、より高いズームレベルでマップを表示する際に使用される。

### [minzoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-dem-minzoom)

[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。デフォルトは 0。  
TileJSON 仕様と同様に、タイルが利用可能な最小ズームレベル。

### [tiles](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-dem-tiles)

[オプションの文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)。[オプションの配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)

TileJSON 仕様と同様に、ひとつあるいは複数のタイルソース URL の配列。

### [tileSize](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-dem-tileSize)

[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。単位はピクセル。デフォルトは 512。  
レイヤーのタイルを表示するための最小視覚サイズ。ラスターレイヤーに対してのみ設定可能。

### [url](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-dem-url)

[オプションの文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)  
TileJSON リソースへの URL。サポートされている通信プロトコルは、http:、https:、および mapbox://<"TilesetID">。

### [volatile](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#raster-dem-volatile)

[オプションのブール値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは false。  
ソースのタイルをローカルにキャッシュするかどうかを決定するための設定。  
| SDK Support | Mapbox GL JS | Android SDK | iOS SDK | macOS SDK |
| ---- | ---- | ---- | ---- | ---- |
| 基本設定通り | サポートされていません | >= 9.3.0 | >= 5.10.0 | サポートされていません |

# [geojson](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=Not%20yet%20supported-,geojson,-A%20GeoJSON%20source)

データは URL またはインライン GeoJSON 形式のでーたプロパティで提供されなければなりません。

```
"geojson-marker": {
    "type": "geojson",
    "data": {
        "type": "Feature",
        "geometry": {
            "type": "Point",
            "coordinates": [-77.0323, 38.9131]
        },
        "properties": {
            "title": "Mapbox DC",
            "marker-symbol": "monument"
        }
    }
}
```

この GeoJSON ソースの例では、URL を介して外部の GeoJSON ドキュメントを参照しています。GeoJSON ドキュメントは、同じドメイン上にあるか、[CORS](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=or%20accessible%20using-,CORS,-.)を使用してアクセスする必要があります。

```
"geojson-lines": {
    "type": "geojson",
    "data": "./lines.geojson"
}
```

| SDK Support           | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| --------------------- | ------------ | ----------- | -------- | --------- |
| 基本設定通り          | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| クラスタリング        | >= 0.14.0    | >= 4.2.0    | >= 3.4.0 | >= 0.3.0  |
| line distance metrics | >= 0.45.0    | >= 6.5.0    | >= 4.4.0 | >= 0.11.0 |

### [attribution](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=%3E%3D%200.11.0-,attribution,-Optional%20string.)

[オプション](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)  
マップがユーザーに表示されるときに表示される属性を記載します。

### [buffer](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=to%20a%20user.-,buffer,-Optional%20number%20between)

[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=Optional-,number,-between%200%20and)  
0 から 512 までの数字。デフォルトは 128。

各辺のタイルバッファのサイズ。値 0 はバッファを生成しません。512 の値は、タイル自体の幅と同じバッファを生成します。大きな値を設定すると、タイルのエッジ付近のレンダリングアーチファクトが減少し、パフォーマンスが低下します。

### [cluster](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#geojson-cluster)

[オプションのブール値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは false。

データがポイントフィーチャーのコレクションである場合、これを true に設定すると、ポイントがグループに半径でクラスタリングされます。クラスター グループは、追加のプロパティを持つソース内の新しいポイント フィーチャーになります。

- cluster  
  点がクラスタである場合は true になります。
- cluster_id  
  クラスタ検査メソッドで使用するクラスタのユニークな ID
- point_count  
  このクラスタにグループ化された元の点の数
- point_count_abbreviated  
  省略された点数

### [clusterMaxZoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#geojson-clusterMaxZoom)

[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)  
クラスタリングが有効な場合、ポイントをクラスタリングする最大ズームレベル。デフォルトは maxzoom より 1 ズーム小さく設定される（最後のズームフィーチャーがクラスタリングされないため）。クラスタは整数倍のズームレベルで設定されるので例えば、clusterMaxZoom を 14 に設定すると、ズームレベル 15 までクラスタが表示されることになる。

### [clusterProperties](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=Defaults%20to%202.-,clusterProperties,-Optional.)

クラスタリングが有効な場合に、クラスタ化されたポイントからの値を集約して、生成されたクラスタにカスタムプロパティを定義するオブジェクト。形式は{"property_name": [operator, map_expression]}。operator は、少なくとも 2 つのオペランド（例えば、"+"や "max"）が使用できる任意の式関数で、クラスタが含むクラスタ/ポイントからプロパティ値を蓄積します。

- 例) {"sum": ["+", ["get", "scalerank"]]}.

より高度なユースケースでは、operator の代わりに、特別な 「"accumulated"」値を参照するカスタム reduce 式を使用することができます。

- 例) ["accumulated"] value, e.g.: {"sum": [["+", ["accumulated"], ["get", "sum"]], ["get", "scalerank"]]}

### [clusterRadius](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#geojson-clusterRadius)

0 以上の数値[オプション](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=Optional-,number,-greater%20than%20or)。デフォルトは 50。
クラスタリングが有効な場合の各クラスタの半径。値 512 は、タイルの幅に等しい半径を示します。

### [data](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#geojson-data)

設定は任意。  
GeoJSON ファイルへの URL、またはインライン GeoJSON。

### [filter](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#geojson-filter)

設定は任意。  
レンダリングのために処理する前に、フィーチャーをフィルタリングするためのもの。

### [generateId](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=them%20for%20rendering.-,generateId,-Optional%20boolean.%20Defaults)

[オプションのブール値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは false。  
geojson フィーチャーの id を生成するかどうかの設定。有効であると、feature.id プロパティは features 配列内のインデックスに基づいて自動的に割り当てられ、以前の値を上書きします。

### [lineMetrics](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#geojson-lineMetrics)

[オプションのブール値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは false。  
線分距離メトリクスを計算するかどうか。これは、線勾配値を指定するラインレイヤに必要です。

### [maxzoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=line%2Dgradient%20values.-,maxzoom,-Optional%20number.%20Defaults)

[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=Optional-,number,-.%20Defaults%20to%2018)。 デフォルトは 18。  
ベクタータイルを作成する際の最大ズームレベル（高いほど高倍率でより詳細に表示される）。

### [promoteId](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=high%20zoom%20levels).-,promoteId,-Optional%20promoteId.)

[オプションの promoteId](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#promoteId)  
フィーチャー ID として使用するプロパティ（フィーチャー状態用）。プロパティ名、または {<sourceLayer>.Object> 形式のオブジェクトのどちらかで記述する。( 「{<propertyName>}」の形のオブジェクト)。

### [tolerance](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#geojson-tolerance)

[オプションの数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。デフォルトは 0.375 。  
Douglas-Peucker simplification tolerance (高いほどジオメトリが単純になり、パフォーマンスが速くなる)。

# [image](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#image)   

url "の値には画像の位置が含まれます。  
座標"配列には、左上、右上、右下、左下の時計回りに並んだ画像端の [経度, 緯度] のペアを記述します。

```
"image": {
    "type": "image",
    "url": "https://docs.mapbox.com/mapbox-gl-js/assets/radar.gif",
    "coordinates": [
        [-80.425, 46.437],
        [-71.516, 46.437],
        [-71.516, 37.936],
        [-80.425, 37.936]
    ]
}
```

| SDK Support  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本設定通り | >= 0.10.0    | >= 5.2.0    | >= 3.7.0 | >= 0.6.0  |

### [coordinates](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=%3E%3D%200.6.0-,coordinates,-Required%20array%20of)

[数字の配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)が必要になります。  
画像端の緯度経度ペアを指定します。

### [url](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=Required-,string,-.)

[オプションの文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)  
必須の文字列です。画像を指し示す URL を記述してください。

# [video](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=to%20an%20image.-,video,-A%20video%20source)

urls" の値は配列で記述します。配列内の各 URL に対して、動画要素のソースが作成されます。ブラウザをまたいで動画をサポートするために、複数の形式の URL を指定します。  
coordinates" 配列には、時計回りに左上、右上、右下、左下の順に並べた動画の端の [経度, 緯度] のペアを指定します。

```
"video": {
    "type": "video",
    "urls": [
        "https://static-assets.mapbox.com/mapbox-gl-js/drone.mp4",
        "https://static-assets.mapbox.com/mapbox-gl-js/drone.webm"
    ],
    "coordinates": [
        [-122.51596391201019, 37.56238816766053],
        [-122.51467645168304, 37.56410183312965],
        [-122.51309394836426, 37.563391708549425],
        [-122.51423120498657, 37.56161849366671]
    ]
}
SDK Support	Mapbox GL JS	Android SDK	iOS SDK	macOS SDK
```

| SDK Support  | Mapbox GL JS | Android SDK            | iOS SDK                | macOS SDK              |
| ------------ | ------------ | ---------------------- | ---------------------- | ---------------------- |
| 基本設定通り | >= 0.10.0    | サポートされていません | サポートされていません | サポートされていません |

### [coordinates](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=%3E%3D%200.6.0-,coordinates,-Required%20array%20of)

[数字の配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)が必要になります。  
動画端の緯度経度ペアを指定します。

### [urls](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=longitude%2C%20latitude%20pairs.-,urls,-Required%20array%20of)

[オプションの文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#:~:text=myImage%22%5D%2C%20%5B%22image%22%2C%20%22fallbackImage%22%5D%5D%0A%7D-,String,-A%20string%20is)     
動画コンテンツへの URL をユーザに閲覧してほしい順番に並べる。
