## 日本語

### Sources

マップまたはレイヤーのソースは、マップがどのデータを表示すべきかを指定します。ソースの種類は "type" プロパティで指定し、vector, raster, raster-dem, geojson, image, video のいずれかである必要があります。

[ソース](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=A-,source,-provides%20map%20data)は地図データを提供し、Mapbox GL JS の[スタイル](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#:~:text=can%20use%20with%20a-,style,-document%20to%20render)ドキュメントを使用することにより様々な視覚化表現を行うことができます。スタイルドキュメントで紹介されているユースケースを用いることで高速道路レイヤーの異なるタイプの道路の外観を区別するなど、同じソースに異なる方法でスタイルを設定することが可能になります。

'スタイルの指定  
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
