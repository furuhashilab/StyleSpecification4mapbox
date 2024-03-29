## 日本語

# レイヤー
スタイルの`layers`プロパティには、そのスタイルで使用できるすべてのレイヤーが一覧表示されます。レイヤーの種類は`"type"`属性で指定し、background、fill、line、symbol、raster、circle、fill-extrusion、heatmap、hillsshade、sky のいずれかを指定する必要があります。

backgroundまたはskyタイプのレイヤーを除いて、各レイヤーはソースを参照する必要があります。レイヤーは[ソース](https://docs.mapbox.com/help/glossary/source/)から取得したデータを受け取り、オプションでフィーチャーをフィルタリングし、それらのフィーチャーがどのようにスタイリングされるかを定義します。

以下は、[スタイル](https://docs.mapbox.com/help/glossary/style/)に含まれる可能性のある`layers`オブジェクトの例です。
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
[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)は必須です。`"fill"`, `"line"`, `"symbol"`, `"circle"`, `"heatmap"`, `"fill-extrusion"`, `"raster"`, `"hillshade"`, `"background"`, `"sky"`のいずれか。

このレイヤーのレンダリングタイプ。

`"fill"`:
塗りつぶされた多角形で、オプションで描画された境界線があります。

`"line"`：
描画された線。

`"symbol"`:
アイコンまたはテキストラベル。

`"circle"`:
塗りつぶした円。

`"heatmap"`: 
ヒートマップ。

`"fill-extrusion"`:
押し出し（3D）ポリゴン。

`"raster"`: 
衛星画像などのラスターマップテクスチャ。

`"hillsshade"`：
DEMデータに基づくクライアントサイドのヒルシェード視覚化。現在のところ、Mapbox Terrain RGB と Mapzen Terrarium タイルのみをサポートする実装になっています。

`"background"`：
マップの背景色またはパターン。

`"sky"`:
マップを囲む球状のドームで、常に他のすべてのレイヤーの後ろにレンダリングされます。

### [フィルター](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#filter)
オプションの[式](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/)

ソースフィーチャーに対する条件を指定する式。フィルタに一致するフィーチャーのみが表示される。フィルタに含まれるズーム式は、整数のズームレベルにおいてのみ評価される。フィルター式では`["feature-state", ...]`式はサポートされていません。`["pitch"]`および`["distance-from-center"]`式は、シンボルレイヤーのフィルター式でのみサポートされています。

### [レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout)
オプションでレイアウトを指定します。

レイヤーのレイアウトプロパティ。

### [最大ズーム](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#maxzoom)
`0`から`24`までの任意の[数字](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。

レイヤーの最大ズームレベル。maxzoomと同じかそれ以上のズームレベルでは、レイヤーは非表示になります。

### [メタデータ](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#metadata)
任意。

レイヤーを追跡するのに便利な任意のプロパティですが、レンダリングに影響を与えるものではありません。プロパティは 'mapbox:' のように、衝突を避けるためにプレフィックスを付ける必要があります。

### [最小ズーム](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#minzoom)
`0`から`24`までの任意の[数字](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。

レイヤーの最小ズームレベル。minzoomより小さいズームレベルでは、レイヤーは隠されます。

### [ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint)
オプションで[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)を指定します。

このレイヤーのデフォルトのペイントプロパティ。

### [ソース](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#source)
オプションの[文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)

このレイヤーに使用されるソース記述の名前。`background`を除くすべてのレイヤーの種類で必要です。

### [ソースレイヤー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#source-layer)
オプションの[文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)

ベクタータイルソースから使用するレイヤー。ベクトルタイルソースでは必須、GeoJSONソースを含む他のすべてのソースタイプでは禁止です。

## [レイヤーのサブプロパティ](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layer-sub-properties)
レイヤーには、そのレイヤーからのデータのレンダリング方法を決定する2つのサブプロパティがあります。`layout`と`paint`プロパティです。

• レイアウトプロパティは、レイヤーの`"layout"`オブジェクトに表示されます。レイアウトプロパティはレンダリング処理の初期に適用され、そのレイヤーのデータがGPUにどのように渡されるかを定義します。レイアウトプロパティを変更するには、非同期の「レイアウト」手順が必要です。

• ペイントプロパティはレンダリングプロセスの後半に適用されます。ペイントプロパティはレイヤーの`"paint"`オブジェクトに表示されます。ペイントプロパティへの変更は安価で、同期的に行われます。

## [バックグラウンド](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#background)
`background`スタイル層は、マップ全体をカバーしています。背景スタイルレイヤーを使用して、他のすべてのマップコンテンツの下に表示される色またはパターンを構成します。背景レイヤーが透明であるか、スタイルから省略されている場合、別のスタイルレイヤーを表示しないマップビューの部分は透明です。

### [背景色](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#source-layer)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。 任意の[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは`"#000000"`。background-patternによって無効にされています。[`補完`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

背景が描画される色。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [背景の不透明度](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-background-background-opacity)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。 `０`から`１`までのオプションの数値。デフォルトは`１`。[`補完`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

背景が描画される不透明度。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [背景パターン](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-background-background-pattern)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[resolvedImage](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#resolvedImage)。
画像の背景を描画するために使用するスプライト内の画像の名前。シームレスパターンの場合、画像の幅と高さは2倍（2、4、8、...、512）である必要があります。ズームに依存する式は、整数のズームレベルでのみ評価されることに注意してください。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | まだサポートされていません  | まだサポートされていません  | まだサポートされていません | まだサポートされていません  |

### [視認性](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-background-visibility)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"visible"`,`"none"`のいずれか。 デフォルトは`"visible"`です。

このレイヤーが表示されるかどうか。

`"visible"`：
レイヤーが表示されます。

`"none"`：
レイヤーは表示されていません。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

## [塗りつぶし](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#fill)
`fill`スタイルレイヤーは、1つ以上の充填レンダリング（および必要に応じてストローク）マップ上の多角形。塗りつぶしレイヤーを使用して、ポリゴンまたはマルチポリゴンフィーチャの外観を構成できます。

### [塗りつぶし-アンチエイリアス](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-fill-antialias)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。 オプションの[ブール値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは`true`。
塗りつぶしをアンチエイリアス処理する必要があるかどうか。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [塗りつぶしの色](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-fill-color)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。 オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。 デフォルトは`"＃000000"`です。 塗りつぶしパターンによって無効にされます。 [feature-state](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。 移行可能。

このレイヤーの塗りつぶされた部分の色。この色はrgbaアルファコンポーネントと同様に指定でき、色の不透明度は、使用されている場合、1pxストロークの不透明度に影響しません。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.19.0   | > = 5.0.0    | > = 3.5.0 | > = 0.4.0  |

### [塗りつぶしの不透明度](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-fill-opacity)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。 0から1までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`1`です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。 移行可能。

塗りつぶしレイヤー全体の不透明度。`fill-color`とは対照的に、ストロークが使用されている場合、この値は塗りつぶしの周囲の1pxのストロークにも影響します。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.21.0   | > = 5.0.0    | > = 3.5.0 | > = 0.4.0  |

### [塗りつぶし-アウトライン-色](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-fill-outline-color)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。 オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。 塗りつぶしパターンによって無効にされます。 塗りつぶしアンチエイリアスが`true`である必要があります。 [`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。 移行可能。

塗りつぶしの輪郭の色。`fill-color`指定されていない場合の値と一致します。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.19.0   | > = 5.0.0    | > = 3.5.0 | > = 0.4.0  |

### [塗りつぶしパターン](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-fill-pattern)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。 オプションの[resolvedImage](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#resolvedImage)。移行可能。

画像の塗りつぶしの描画に使用するスプライト内の画像の名前。シームレスパターンの場合、画像の幅と高さは2倍（2、4、8、...、512）である必要があります。ズームに依存する式は、整数のズームレベルでのみ評価されることに注意してください。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.49.0   | > = 6.5.0    | > = 4.4.0 | > = 0.11.0  |

### [塗りつぶし-ソートキー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-fill-fill-sort-key)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。 オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。

この値に基づいて機能を昇順で並べ替えます。ソートキーが高い機能は、ソートキーが低い機能の上に表示されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 1.2.0  |> = 9.1.0    | > = 5.8.0 | > = 0.15.0  |
| データ駆動型のスタイリング | > = 1.2.0  | > = 9.1.0 | > = 5.8.0 | > = 0.15.0  |

### [塗りつぶし-変換](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-fill-translate)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。 オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)。 ピクセル単位。 デフォルトは`[0,0]`です。 [`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。 移行可能。

ジオメトリのオフセット。値は[x、y]で、負の値はそれぞれ左と上を示します。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [塗りつぶし-変換-anchor](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-fill-translate-anchor)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"map"`,`"viewport"`のいずれか。デフォルトは`"map"`。`fill-translate`が必要です。

`"map"`：
塗りつぶしは、マップを基準にして変換されます。

`"viewport"`：
塗りつぶしは、ビューポートを基準にして変換されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [視認性](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-fill-visibility)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"visible"`,`"none"`のいずれか。 デフォルトは`"visible"`です。

このレイヤーが表示されるかどうか。

`"visible"`：
レイヤーが表示されます。

`"none"`：
レイヤーは表示されていません。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

## [ライン](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#line)
`line`スタイルレイヤーは、マップ上の一つ以上のストロークポリラインをレンダリングします。ラインレイヤーを使用して、ポリラインまたはマルチポリラインフィーチャの外観を構成できます。

### [ラインブラー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-line-line-blur)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。ピクセル単位の単位。 デフォルトは`0`です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

線に適用されたぼかし（ピクセル単位）。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.29.0    | > = 5.0.0    | > = 3.5.0 | >= 0.4.0  |

### [ラインキャップ](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-line-line-cap)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"butt"`,`"round"`,`"square"`のいずれか。 デフォルトは`"butt"`です。

行末の表示。

`"butt"`：
線の正確な端点に引かれる四角い端のあるキャップ。

`"round"`：
線の幅の半分の半径で線の端点を超えて描画され、線の端点を中心とする丸い端を持つキャップ。

`"square"`：
線の幅の半分の距離で線の端点を超えて描かれる、四角い端を持つキャップ。


| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 2.3.0    | まだサポートされていません    | まだサポートされていません | まだサポートされていません  |

### [ラインの色](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-line-line-color)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは`"＃000000"`です。 line-patternによって無効にされます。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

ラインを引く色。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 2.3.0    | > = 5.0.0    | > = 3.5.0 | >= 0.4.0  |

### [ライン-dasharray](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-line-line-dasharray)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)の[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)。線幅の単位。line-patternによって無効にされます。 移行可能。

ダッシュパターンを形成する交互のダッシュとギャップの長さを指定します。長さは後で線幅によってスケーリングされます。ダッシュの長さをピクセルに変換するには、長さに現在の線幅を掛けます。`lineMetrics: true`指定されたGeoJSONソースは、破線を期待される縮尺でレンダリングしないことに注意してください。また、ズームに依存する式は、整数のズームレベルでのみ評価されることに注意してください。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 2.3.0    | まだサポートされていません    | まだサポートされていません | まだサポートされていません  |

### [ラインギャップ幅](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-line-line-gap-width)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。ピクセル単位の単位。 デフォルトは`0`です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

ラインの実際のパスの外側にラインケーシングを描画します。値は、内側のギャップの幅を示します。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.29.0    | > = 5.0.0    | > = 3.5.0 | >= 0.4.0  |

### [ライングラディエント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-line-line-gradient)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。 line-patternによって無効にされます。ソースが`geojson`である必要があります。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.45.0    | > = 6.5.0   | > = 4.4.0 | > = 0.11.0  |
| データ駆動型のスタイリング | まだサポートされていません   | まだサポートされていません    | まだサポートされていません | まだサポートされていません  |

### [ライン結合](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-line-line-join)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"bevel"`,`"round"`,`"miter"`のいずれか。 デフォルトは`"miter"`です。

結合時の線の表示。

`"bevel"`：
線の幅の半分の距離で線の端点を超えて描画される、四角い端を持つ結合。

`"round"`：
線の幅の半分の半径で線の端点を超えて描画され、線の端点を中心とする丸い端を持つ結合。

`"miter"`：
パスの端点を超えて外側が出会うまで描かれる、鋭く角度の付いたコーナーを持つ結合。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.40.0  | > = 5.2.0    | > = 3.7.0 | > = 0.6.0  |


### [ラインマイターリミット](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-line-line-miter-limit)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。 オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。デフォルトは`2`です。line-joinが`"マイター"`である必要があります。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

鋭角のマイター結合をベベル結合に自動的に変換するために使用されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [ラインオフセット](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-line-line-offset)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。ピクセル単位。 デフォルトは`0`です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

線のオフセット。線形フィーチャの場合、正の値は線の方向に対して右に線をオフセットし、負の値は左にオフセットします。ポリゴンフィーチャの場合、正の値はインセットになり、負の値はアウトセットになります。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.12.1   | > = 3.0.0   | > = 3.1.0 | > = 0.1.0  |
| データ駆動型のスタイリング | > = 0.29.0    | > = 5.0.0    | > = 3.5.0 | >= 0.4.0  |

### [ラインの不透明度](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-line-line-opacity)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`から`1`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`1`です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。


| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 2.3.0    | > = 5.0.0    | > = 3.5.0 | >= 0.4.0  |

### [ラインパターン](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-line-line-pattern)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。 オプションの[resolvedImage](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#resolvedImage)。移行可能。

画像の線を描画するために使用するスプライト内の画像の名前。シームレスパターンの場合、画像の幅は2倍（2、4、8、...、512）である必要があります。ズームに依存する式は、整数のズームレベルでのみ評価されることに注意してください。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.49.0   | > = 6.5.0    | > = 4.4.0 | > = 0.11.0  |

### [ラインラウンドリミット](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-line-line-round-limit)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。 オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。デフォルトは`1.05`。line-joinは`"round"`である必要があります。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

浅い角度のラウンド結合をマイター結合に自動的に変換するために使用されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [ライン-ソートキー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-line-line-sort-key)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。 オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 1.2.0    | > = 9.1.0   | > = 5.8.0 | > = 0.15.0  |
| データ駆動型のスタイリング | > = 1.2.0    | > = 9.1.0   | > = 5.8.0 | > = 0.15.0  |

### [ライン-変換](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-line-line-translate)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)。 ピクセル単位。 デフォルトは`「0,0」`です。

ジオメトリのオフセット。値は「x、y」で、負の値はそれぞれ左と上を示します。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [ライン-変換-anchor](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-line-line-translate-anchor)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"map"`,`"viewport"`のいずれか。 デフォルトは`"map"`です。 行変換が必要です。

`line-translate`の参照フレームを制御します。

`"map"`：
線はマップを基準にして平行移動されます。

`"viewport"`：
線はビューポートを基準にして平行移動されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [ライン-トリム-オフセット](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-line-line-translate)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`00`から`11`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)。デフォルトは`「0,0」`です。ソースが`"geojson"`であることが必要です。

 [trim-start, trim-end] の間のライン部分は、ルート消失の効果を出すために、透明なマークが付けられます。ライントリムオフのオフセットは、ライン全体の範囲 [0.0, 1.0] を基準とします。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 2.9.0    | >= 10.5.0   | >= 10.5.0 | >= 10.5.0 |

### [ライン幅](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-line-line-width)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。ピクセル単位の単位。デフォルトは`1`です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

ストロークの太さ。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.39.0  | > = 5.2.0    | > = 3.7.0 | > = 0.6.0  |

### [視認性](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-line-visibility)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"visible"`,`"none"`のいずれか。 デフォルトは`"visible"`です。

このレイヤーが表示されるかどうか。

`"visible"`：
レイヤーが表示されます。

`"none"`：
レイヤーは表示されていません。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

## [シンボル](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#symbol)
`symbol`スタイル層がポイントで、マップ上のラインに沿ってアイコンとテキストラベルをレンダリングします。シンボルレイヤーを使用して、ベクタータイルのフィーチャのラベルの外観を構成できます。

### [アイコン-allow-overlap](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-icon-allow-overlap)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[ブルー値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは`false`です。 アイコン画像が必要です。

trueの場合、以前に描画された他のシンボルと衝突しても、アイコンは表示されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0 |

### [アイコンアンカー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-icon-anchor)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"center"`,`"left"`,`"right"`,`"top"`,`"bottom"`,`"bottom-left"`,`"bottom-right"`のいずれか。 デフォルトは`"center"`です。 アイコン画像が必要です。

アンカーの最も近くに配置されたアイコンの一部。

`"center"`：
アイコンの中心は、アンカーに最も近い位置に配置されます。

`"left"`：
アイコンの左側は、アンカーに最も近い位置に配置されます。

`"right"`：
アイコンの右側は、アンカーに最も近い位置に配置されます。

`"top"`：
アイコンの上部は、アンカーの最も近くに配置されます。

`"bottom"`：
アイコンの下部は、アンカーの最も近くに配置されます。

`"top-left"`：
アイコンの左上隅は、アンカーの最も近くに配置されます。

`"top-right"`：
アイコンの右上隅は、アンカーの最も近くに配置されます。

`"bottom-left"`：
アイコンの左下隅は、アンカーの最も近くに配置されます。

`"bottom-right"`：
アイコンの右下隅は、アンカーの最も近くに配置されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.40.0   | > = 5.2.0  | > = 3.7.0 | > = 0.6.0  |
| データ駆動型のスタイリング | > = 0.40.0   | > = 5.2.0  | > = 3.7.0 | > = 0.6.0  |

### [アイコンカラー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-symbol-icon-color)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは`"＃000000"`です。アイコン画像が必要です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

アイコンの色。これは、[SDFアイコン](https://docs.mapbox.com/help/troubleshooting/using-recolorable-images-in-mapbox-maps/)でのみ使用できます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.33.0  | > = 5.0.0   | > = 3.5.0 | > = 0.4.0  |

### [アイコン-halo-blur](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-symbol-icon-halo-blur)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。ピクセル単位の単位。 デフォルトは`0`です。アイコン画像が必要です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

ハローを外側に向かってフェードアウトします。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.33.0  | > = 5.0.0   | > = 3.5.0 | > = 0.4.0  |

### [アイコン-halo-color](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-symbol-icon-halo-color)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは`"rgba(0, 0, 0, 0)"`です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

アイコンハローの色。アイコンハローは、[SDFアイコン](https://docs.mapbox.com/help/troubleshooting/using-recolorable-images-in-mapbox-maps/)でのみ使用できます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.33.0  | > = 5.0.0   | > = 3.5.0 | > = 0.4.0  |

### [アイコン-halo-width](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-symbol-icon-halo-width)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。ピクセル単位の単位。 デフォルトは`0`です。アイコン画像が必要です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

アイコンの輪郭までのハローの距離。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.33.0  | > = 5.0.0   | > = 3.5.0 | > = 0.4.0  |

### [アイコン-ignore-placement](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-icon-ignore-placement)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[ブルー値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは`false`です。 アイコン画像が必要です。

trueの場合、アイコンと衝突しても他のシンボルが表示される可能性があります。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0 |

### [アイコン画像](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-icon-image)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[resolvedImage](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#resolvedImage)。

画像の背景を描画するために使用するスプライト内の画像の名前。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.35.0  | > = 5.1.0   | > = 3.6.0 | > = 0.5.0  |

### [アイコン-直立状態を維持](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-icon-keep-upright)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[ブルー値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは`false`です。 アイコン画像が必要です。icon-rotation-alignmentが`"map"`である必要があります。 シンボルの配置は`"line"`または`"line-center"`である必要があります。

trueの場合、アイコンが上下逆にレンダリングされないように、アイコンを反転させることができます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [アイコンオフセット](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-icon-offset)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)の[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)。デフォルトは`[0,0]`です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。 移行可能。

アイコンのアンカーからのオフセット距離。正の値は右と下を示し、負の値は左と上を示します。各コンポーネントにの値を掛けて、`icon-size`ピクセル単位の最終オフセットを取得します。`icon-rotate`オフセットと組み合わせると、回転方向が上にあるかのようになります。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.29.0    | > = 5.0.0    | > = 3.5.0 | >= 0.4.0  |

### [アイコン-不透明度](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-symbol-icon-opacity)
[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`から`1`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`1`です。アイコン画像が必要です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

アイコンが描画される不透明度。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.33.0  | > = 5.0.0   | > = 3.5.0 | > = 0.4.0  |

### [アイコンオプション](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-icon-optional)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[ブルー値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは`false`です。 アイコン画像が必要です。 テキストフィールドが必要です。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [アイコンパディング](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-icon-padding)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。ピクセル単位の単位。 デフォルトは`2`です。アイコン画像が必要です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

シンボルの衝突を検出するために使用されるアイコン境界ボックスの周囲の追加領域のサイズ。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [アイコン-pitch-alignment](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-icon-pitch-alignment)
[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"map"`,`"viewport"`,`"auto"`のいずれか。 デフォルトは`"auto"`です。アイコン画像が必要です。

マップがピッチされたときのアイコンの向き。

"map"：
アイコンはマップの平面に揃えられます。

"viewport"：
アイコンはビューポートの平面に揃えられます。

"auto"：
の値と自動的に一致しますicon-rotation-alignment。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.39.0  | > = 5.2.0   | > = 3.7.0 | > = 0.6.0  |

### [アイコン-回転](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-icon-rotate)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。 オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。度単位。 デフォルトは`0`です。アイコン画像が必要です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

アイコンを時計回りに回転させます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.21.0  | > = 5.0.0   | > = 3.5.0 | > = 0.4.0  |

### [アイコン-rotation-alignment](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-icon-rotation-alignment)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"map"`,`"viewport"`,`"auto"`のいずれか。 デフォルトは`"auto"`です。アイコン画像が必要です。

`symbol-placement`と組み合わせて、アイコンの回転動作を決定します。

`"map"`：
`symbol-placement`が`point`に設定されている場合、アイコンを東西に揃えます。`symbol-placement`が`line`または`line-center`に設定されている場合、アイコンのx軸を線に揃えます。

`"viewport"`：
`symbol-placement`の値に関係なく、x軸がビューポートのx軸に位置合わせされたアイコンを生成します。

`"auto"`：
`symbol-placement`が`point`に設定されている場合、これは`"viewport"`と同等です。`symbol-placement`が`line`または`line-center`に設定されている場合、これは`map`と同等です。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.25.0  | > = 4.2.0  | > = 3.4.0 | > = 0.3.0  |

### [アイコンサイズ](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-icon-size)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。元のアイコンサイズを考慮した単位。デフォルトは`1`です。アイコン画像が必要です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

提供された係数でアイコンの元のサイズを拡大縮小します。 画像の新しいピクセルサイズは、元のピクセルサイズに`icon-size`を掛けたものになります。1は元のサイズです。画像のサイズを3倍にします。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.35.0  | > = 5.1.0   | > = 3.6.0 | > = 0.5.0  |

### [アイコン-text-fit](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-icon-text-fit)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"none"`,`"width"`,`"height"`,`"both"`のいずれか。 デフォルトは`"none"`です。 アイコン画像が必要です。 テキストフィールドが必要です。

`"none"`：
アイコンは、固有のアスペクト比で表示されます。

`"width"`：
アイコンは、テキストの幅に合わせてx次元で拡大縮小されます。

`"height"`：
アイコンは、テキストの高さに合わせてy次元で拡大縮小されます。

`"both"`：
アイコンは、x次元とy次元の両方で拡大縮小されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.21.0   | > = 4.2.0   | > = 3.4.0 | > = 0.2.1  |
| データ駆動型のスタイリング | > = 1.6.0 | > = 9.2.0  | > = 5.8.0 | > = 0.15.0  |

### [アイコン-text-fit-padding](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-icon-text-fit-padding)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)の[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)。ピクセル単位。 デフォルトは`[0,0,0,0]`です。 アイコン画像が必要です。テキストフィールドが必要です。icon-text-fitは、`"both"`,`"width"`,`"height"`である必要があります。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

`icon-text-fit`によって決定される寸法に追加される追加領域のサイズ（時計回りの順序：上、右、下、左）。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.21.0   | > = 4.2.0   | > = 3.4.0 | > = 0.2.1  |

### [アイコン-翻訳](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-symbol-icon-translate)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)の[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)。ピクセル単位。 デフォルトは`[0,0]`です。 アイコン画像が必要です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

アイコンのアンカーが元の配置から移動した距離。正の値は右と下を示し、負の値は左と上を示します。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [アイコン-translate-anchor](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-symbol-icon-translate-anchor)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"map"`,`"viewport"`のいずれか。 デフォルトは`"map"`です。

`icon-translate`の参照フレームを制御します。

`"map"`：
アイコンは、マップを基準にして翻訳されます。

`"viewport"`：
アイコンは、ビューポートを基準にして変換されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [symbol-avoid-edges](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-symbol-avoid-edges)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[ブルー値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは`false`です。 

trueの場合、相互の衝突を避けるために、シンボルはタイルの端を越えません。 衝突を防ぐためにベクタータイルに十分なパディングがないレイヤー、またはラインシンボルレイヤーの後に配置されたポイントシンボルレイヤーの場合に推奨されます。 Mapbox GL JSバージョン0.42.0以降など、グローバルな衝突検出をサポートするクライアントを使用する場合、タイルの境界でラベルがクリップされるのを防ぐために、このプロパティを有効にする必要はありません。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [シンボル配置](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-symbol-placement)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"point"`,`"line"`,`"line-center"`のいずれか。デフォルトは`"point"`です。

ジオメトリに対するラベルの配置。

`"point"`：
ラベルは、ジオメトリが配置されているポイントに配置されます。

`"line"`：
ラベルはジオメトリの線に沿って配置されます。LineStringおよびPolygonジオメトリでのみ使用できます。

`"line-center"`：
ラベルは、ジオメトリの線の中央に配置されます。LineStringおよびPolygonジオメトリでのみ使用できます。ベクトルタイル内の単一のフィーチャに複数のラインジオメトリが含まれる場合があることに注意してください。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.47.0  | > = 6.4.0 | > = 4.3.0 | > = 0.10.0  |

### [シンボルソートキー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-symbol-sort-key)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。 オプションの[番号](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。

この値に基づいて機能を昇順で並べ替えます。ソートキーが低いフィーチャが最初に描画され、配置されます。`icon-allow-overlap`または`text-allow-overlap`の場合`false`、配置時にソートキーが低いフィーチャが優先されます。`icon-allow-overlap`またはが`text-allow-overlap`に設定されている場合`true`、ソートキーが高いフィーチャは、ソートキーが低いフィーチャとオーバーラップします。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.53.0  | > = 7.4.0    | > = 4.11.0 | > = 0.14.0  |
| データ駆動型のスタイリング | > = 0.53.0  | > = 7.4.0    | > = 4.11.0 | > = 0.14.0  |

### [シンボル間隔](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-symbol-spacing)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。`1`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。ピクセル単位。 デフォルトは`250`です。シンボルの配置は`line`である必要があります。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

2つのシンボルアンカー間の距離。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [シンボル-zオーダー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-symbol-z-order)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"auto"`,`"viewport-y"`,`"source"`のいずれか。 デフォルトは`"auto"`です。 

同じレイヤー内の重複するシンボルを、データソースに表示される順序でレンダリングするか、ビューポートに対するy位置でレンダリングするかを決定します。それ以外の場合にシンボルの順序と優先順位を制御するには、`symbol-sort-key`を使用します。

`"auto"`：
設定されている場合、`symbol-sort-key`でシンボルをソートします。 それ以外の場合、`icon-allow-overlap`または`text-allow-overlap`が`true`に設定されているか、`icon-ignore-placement`または`text-ignore-placement`が`false`の場合、ビューポートを基準にしたy位置でシンボルを並べ替えます。

`"viewport-y"`：
`icon-allow-overlap`または`text-allow-overlap`が`true`に設定されているか、`icon-ignore-placement`または`text-ignore-placement`が`false`の場合、ビューポートを基準にしたy位置でシンボルを並べ替えます。

`"source"`：
設定されている場合、`symbol-sort-key`でシンボルをソートします。 それ以外の場合、並べ替えは適用されません。 シンボルは、ソースデータと同じ順序でレンダリングされます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.49.0  | > = 6.6.0  | > = 4.5.0 | > = 0.12.0 |

### [text-allow-overlap](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-allow-overlap)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[ブルー値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは`false`です。 テキストフィールドが必要です。

trueの場合、以前に描画された他のシンボルと衝突しても、テキストは表示されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [テキストアンカー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-anchor)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"center"`,`"left"``"right"`,`"top"`,`"bottom"`,`"top-left"`,`"top-right"`,`"bottom-left"`,`"bottom-right"`のいずれか。 デフォルトは`"center"`です。 テキストフィールドが必要です。 text-variable-anchorによって無効にされます。

アンカーに最も近い位置に配置されたテキストの一部。

`"center"`：
テキストの中心はアンカーに最も近い位置に配置されます。

`"left"`：
テキストの左側は、アンカーに最も近い位置に配置されます。

`"right"`：
テキストの右側は、アンカーに最も近い位置に配置されます。

`"top"`：
テキストの上部はアンカーに最も近い位置に配置されます。

`"bottom"`：
テキストの下部は、アンカーに最も近い位置に配置されます。

`"top-left"`：
テキストの左上隅は、アンカーに最も近い位置に配置されます。

`"top-right"`：
テキストの右上隅は、アンカーの最も近くに配置されます。

`"bottom-left"`：
テキストの左下隅は、アンカーの最も近くに配置されます。

`"bottom-right"`：
テキストの右下隅は、アンカーの最も近くに配置されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.39.0  | > = 5.2.0    | > = 3.7.0 | > = 0.6.0  |

### [テキストの色](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-symbol-text-color)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは`"＃000000"`です。テキストフィールドが必要です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

テキストが描画される色。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.33.0  | > = 5.0.0   | > = 3.5.0 | > = 0.4.0  |

### [テキストフィールド](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-field)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[フォーマット済み](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#formatted)。デフォルトは`""`。

テキストラベルに使用する値。プレーン`string`を提供した場合、デフォルト/継承されたフォーマットオプションで`formatted`されたものとして扱われます。SDF画像はフォーマットされたテキストではサポートされていないため、無視されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.33.0  | > = 5.0.0   | > = 3.5.0 | > = 0.4.0  |

### [テキストフォント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-font)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。[文字列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#string)のオプションの[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)。デフォルトは`["Open Sans Regular","Arial Unicode MS Regular"]`です。 テキストフィールドが必要です。

テキストの表示に使用するフォントスタック。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.43.0 | > = 6.0.0 | > = 4.0.0 | > = 0.7.0 |

### [text-halo-blur](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-symbol-text-halo-blur)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。ピクセル単位。デフォルトは`0`。テキストフィールドが必要です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

ハローの外側へのフェードアウト距離。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.33.0  | > = 5.0.0   | > = 3.5.0 | > = 0.4.0  |

### [text-halo-color](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-symbol-text-halo-color)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは`"rgba(0, 0, 0, 0)"`です。テキストフィールドが必要です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

テキストのハローの色。背景から目立つようになります。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.33.0  | > = 5.0.0   | > = 3.5.0 | > = 0.4.0  |

### [text-halo-width](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-symbol-text-halo-width)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。ピクセル単位。 デフォルトは`0`です。テキストフィールドが必要です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

ハローからフォントのアウトラインまでの距離。最大テキストハロー幅はフォントサイズの1/4です。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.33.0  | > = 5.0.0   | > = 3.5.0 | > = 0.4.0  |

### [text-ignore-placement](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-ignore-placement)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[ブルー値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは`false`です。 テキストフィールドが必要です。

trueの場合、テキストと衝突しても他の記号が表示される可能性があります。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [text-justify](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-justify)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"auto"`,`"left"`,`"center"`,`"right"`のいずれか。 デフォルトは`"center"`です。 テキストフィールドが必要です。

テキストの位置揃えオプション。

`"auto"`：
テキストはアンカー位置に揃えられます。

`"left"`：
テキストは左揃えになります。

`"center"`：
テキストは中央に配置されます。

`"right"`：
テキストは右揃えになります。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.39.0  | > = 5.2.0    | > = 3.7.0 | > = 0.6.0  |
| 自動 | > = 0.54.0  | > = 7.4.0  | > = 4.10.0 | > = 0.14.0 |

### [text-keep-upright](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-keep-upright)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[ブルー値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは`true`です。 テキストフィールドが必要です。text-rotation-alignmentが`"map"`である必要があります。 シンボルの配置は`"line"`または`"line-center"`である必要があります。

trueの場合、テキストが上下逆にレンダリングされないように、テキストを垂直方向に反転させることができます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [テキスト文字の間隔](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-letter-spacing)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。 オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。emsの単位。デフォルトは0。テキストフィールドが必要です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.40.0   | > = 5.2.0  | > = 3.7.0 | > = 0.6.0  |

### [テキスト行の高さ](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-line-height)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。 オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。emsの単位。デフォルトは`1.2`。テキストフィールドが必要です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

複数行テキストのテキスト先行値。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 2.3.0  | まだサポートされていません | まだサポートされていません | まだサポートされていません |

### [text-max-angle](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-max-angle)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。 オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。度単位。 デフォルトは`45`です。テキストフィールドが必要です。 シンボルの配置は`"line"`または`"line-center"`である必要があります。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

隣接するキャラクター間の最大角度変化。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [text-max-width](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-max-width)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。emsの単位。 デフォルトは`10`です。テキストフィールドが必要です。 シンボルの配置は`"point"`である必要があります。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

テキスト折り返しの最大行幅。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.40.0   | > = 5.2.0  | > = 3.7.0 | > = 0.6.0  |

### [テキストオフセット](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-offset)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)の[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)。emsの単位。デフォルトは`[0,0]`。テキストフィールドが必要です。text-radial-offsetによって無効にされます。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

アンカーからのテキストのオフセット距離。正の値は右と下を示し、負の値は左と上を示します。text-variable-anchorとともに使用する場合、入力値は絶対値と見なされます。x軸とy軸に沿ったオフセットは、アンカー位置に基づいて自動的に適用されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.35.0  | > = 5.1.0   | > = 3.6.0 | > = 0.5.0  |

### [テキストの不透明度](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-symbol-text-opacity)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`から`1`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`1`です。テキストフィールドが必要です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

テキストが描画される不透明度。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.33.0  | > = 5.0.0   | > = 3.5.0 | > = 0.4.0  |

### [テキスト-オプション](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-optional)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[ブルー値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは`false`。テキストフィールドが必要です。icon-imageが必要です。 

trueの場合、テキストが他のシンボルと衝突し、アイコンが衝突しない場合、アイコンは対応するテキストなしで表示されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [テキストパディング](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-padding)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。ピクセル単位。 デフォルトは`2`です。テキストフィールドが必要です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

シンボルの衝突を検出するために使用されるテキスト境界ボックスの周囲の追加領域のサイズ。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [text-pitch-alignment](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-pitch-alignment)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"map"`,`"viewport"`,`"auto"`のいずれか。 デフォルトは`"auto"`です。テキストフィールドが必要です。

マップがピッチングされたときのテキストの向き。

`"map"`：
テキストはマップの平面に揃えられます。

`"viewport"`：
テキストはビューポートの平面に揃えられます。

`"auto"`：
の値と自動的に一致しますtext-rotation-alignment。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.21.0	| > = 4.2.0	| > = 3.4.0	| > = 0.2.1 |
|  auto 価値 | > = 0.25.0	|  > = 4.2.0	|  > = 3.4.0	|  > = 0.3.0 |

### [text-radial-offset](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-radial-offset)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。 オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。emsの単位。デフォルトは0。テキストフィールドが必要です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

シンボルのアンカーの方向でのテキストの半径方向のオフセット。`text-variable-anchor`と組み合わせて使用すると便利です。これは、デフォルトで2次元の`text-offset`が存在する場合に使用されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.54.0	| > = 7.4.0	| > = 4.10.0	|  > = 0.14.0  |
| データ駆動型のスタイリング | > = 0.54.0	| > = 7.4.0	| > = 4.10.0	|  > = 0.14.0  |

### [テキスト-回転](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-rotate)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。 オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。度単位。デフォルトは`0`。テキストフィールドが必要です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

テキストを時計回りに回転します。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.35.0  | > = 5.1.0   | > = 3.6.0 | > = 0.5.0  |

### [text-rotation-alignment](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-rotation-alignment)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"map"`,`"viewport"`,`"auto"`のいずれか。 デフォルトは`"auto"`です。テキストフィールドが必要です。

記号の配置と組み合わせて、テキストを形成する個々のグリフの回転動作を決定します。

`"map"`：
`symbol-placement`が`point`に設定されている場合、テキストを東西に揃えます。`symbol-placement`が`line`または`line-center`に設定されている場合、テキストのx軸を線に揃えます。

`"viewport"`：
`symbol-placement`の値に関係なく、x軸がビューポートのx軸と整列しているグリフを生成します。

`"auto"`：
`symbol-placement`が`point`に設定されている場合、これは`viewport`と同等です。`symbol-placement`が`line`または`line-center`に設定されている場合、これは`map`と同等です。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
|  auto 価値 | > = 0.25.0	|  > = 4.2.0	|  > = 3.4.0	|  > = 0.3.0 |

### [文字サイズ](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-size)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。ピクセル単位。デフォルトは`16`です。テキストフィールドが必要です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

フォントサイズ。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.35.0  | > = 5.1.0   | > = 3.6.0 | > = 0.5.0  |

### [テキスト変換](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-transform)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"none"`,`"uppercase"`,`"lowercase"`のいずれか。 デフォルトは`"none"`です。 テキストフィールドが必要です。

`text-transform`CSSプロパティと同様に、テキストを大文字にする方法を指定します。

`"none"`：
テキストは変更されません。

`"uppercase"`：
すべての文字を強制的に大文字で表示します。

`"lowercase"`：
すべての文字を強制的に小文字で表示します。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.33.0  | > = 5.0.0   | > = 3.5.0 | > = 0.4.0  |

### [テキスト翻訳](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-symbol-text-translate)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)の[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)。ピクセル単位。デフォルトは`[0,0]`。テキストフィールドが必要です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

テキストのアンカーが元の配置から移動した距離。正の値は右と下を示し、負の値は左と上を示します。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [text-translate-anchor](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-symbol-text-translate-anchor)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"map"`,`"viewport"`のいずれか。 デフォルトは`"map"`です。テキストフィールドが必要です。テキスト翻訳が必要です。

`text-translate`の参照フレームを制御します。

`"map"`：
テキストはマップを基準にして翻訳されます。

`"viewport"`：
テキストはビューポートを基準にして翻訳されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [text-variable-anchor](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-variable-anchor)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)オプションの[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)。`"center"`,`"left"`,`"right"`,`"top"`,`"bottom"`,`"top-left"`,`"top-right"`,`"bottom-left"`,`"bottom-right"`のいずれか。テキストフィールドが必要です。シンボルの配置は`point`である必要があります。

マップ上に優先度の高いラベルを配置する可能性を高めるために、`text-anchor`場所の配列を提供できます。レンダラーは、次のラベルに移動する前に、各場所に順番にラベルを配置しようとします。`text-justify: auto`アンカー位置に基づいて位置合わせを選択するために使用します。オフセットを適用するには、`text-radial-offset`または2次元を使用し`text-offset`ます。

`"center"`：
テキストの中心はアンカーに最も近い位置に配置されます。

`"left"`：
テキストの左側は、アンカーに最も近い位置に配置されます。

`"right"`：
テキストの右側は、アンカーに最も近い位置に配置されます。

`"top"`：
テキストの上部はアンカーに最も近い位置に配置されます。

`"bottom"`：
テキストの下部は、アンカーに最も近い位置に配置されます。

`"top-left"`：
テキストの左上隅は、アンカーに最も近い位置に配置されます。

`"top-right"`：
テキストの右上隅は、アンカーの最も近くに配置されます。

`"bottom-left"`：
テキストの左下隅は、アンカーの最も近くに配置されます。

`"bottom-right"`：
テキストの右下隅は、アンカーの最も近くに配置されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.54.0  | > = 7.4.0  | > = 4.10.0 | > = 0.14.0 |

### [テキスト書き込みモード](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-text-writing-mode)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)オプションの[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)。`"horizontal"`,`"vertical"`のいずれか。 テキストフィールドが必要です。

このプロパティを使用すると、シンボルの方向を制御できます。 プロパティ値はヒントとして機能するため、言語が指定された方向をサポートしていないシンボルは、自然な方向に配置されることに注意してください。 例：配列値に単一の「垂直」列挙値が含まれている場合でも、英語のポイントシンボルは水平方向にレンダリングされます。 ポイント配置のシンボルの場合、配列内の要素の順序によって、方向バリアントの配置の優先順位が定義されます。 行配置のあるシンボルの場合、デフォルトのテキスト書き込みモードは['horizontal'、 'vertical']または['vertical'、 'horizontal']のいずれかであり、順序は配置に影響しません。

`"horizontal"`：
テキストの言語が水平書き込みモードをサポートしている場合、記号は水平に配置されます。

`"vertical"`：
テキストの言語が垂直書き込みモードをサポートしている場合、記号は垂直に配置されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 1.3.0	|　　> = 8.3.0	|　　　> = 5.3.0	|　　> = 0.15.0 |

### [視認性](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-visibility)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"visible"`,`"none"`のいずれか。 デフォルトは`"visible"`です。

このレイヤーが表示されるかどうか。

`"visible"`：
レイヤーが表示されます。

`"none"`：
レイヤーは表示されていません。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

## [ラスター](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#raster)

スタイルレイヤーは、マップ上に`raster`ラスタータイルをレンダリングします。ラスターレイヤーを使用して、ラスタータイルのカラーパラメーターを構成できます。

### [ラスター-明るさ-最大](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-raster-raster-brightness-max)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`から`1`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`1`です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

画像の明るさを増減します。値は最大輝度です。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [ラスター-明るさ-最小](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-raster-raster-brightness-min)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`から`1`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`0`です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

画像の明るさを増減します。値は最小輝度です。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [ラスター-コントラスト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-raster-raster-contrast)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`-1`から`1`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`0`です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

画像のコントラストを増減します。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [ラスターフェード期間](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-raster-raster-fade-duration)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。ミリ秒単位。 デフォルトは300です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

新しいタイルが追加されたときのフェード期間。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [ラスター-色相-回転](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-raster-raster-hue-rotate)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。度単位。デフォルトは`0`。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

カラーホイールを中心に色相を回転させます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [ラスター不透明度](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-raster-raster-opacity)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`から`1`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`1`です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

画像が描画される不透明度。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [ラスターリサンプリング](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-raster-raster-resampling)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"linear"`、`"nearest"`の1つ。 デフォルトは`"linear"`です。

オーバースケーリングに使用するリサンプリング/補間方法。テクスチャ倍率フィルターとも呼ばれます。

`"linear"`：
（Bi）線形フィルタリングは、最も近い4つの元のソースピクセルの加重平均を使用してピクセル値を補間し、オーバースケールすると滑らかでぼやけた外観を作成します。

`"nearest"`：
最近傍フィルタリングは、最も近い元のソースピクセルを使用してピクセル値を補間し、オーバースケールするとシャープでありながらピクセル化された外観を作成します。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.47.0	 | > = 6.3.0	|  > = 4.2.0	|  > = 0.9.0  |

### [ラスター飽和](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-raster-raster-saturation)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`-1`から`1`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`0`です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

画像の彩度を増減します。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [視認性](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-visibility)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"visible"`,`"none"`のいずれか。 デフォルトは`"visible"`です。

このレイヤーが表示されるかどうか。

`"visible"`：
レイヤーが表示されます。

`"none"`：
レイヤーは表示されていません。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

## [サークル](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#circle)

`circle`スタイルレイヤーは、マップ上に1つ以上の塗りつぶされた円をレンダリングします。円レイヤーを使用して、ベクタータイルのポイントまたはポイントコレクションフィーチャの視覚的な外観を構成できます。円レイヤーは、半径が画面単位で測定される円をレンダリングします。

### [サークルブラー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-circle-circle-blur)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。デフォルトは`0`です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

円をぼかす量。1は、中心点のみが完全に不透明になるように円をぼかします。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.20.0  | > = 5.0.0   | > = 3.5.0 | > = 0.4.0  |

### [サークルカラー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-circle-circle-color)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは`＃000000`です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

円の塗りつぶしの色。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.18.0   | > = 5.0.0    | > = 3.5.0 | > = 0.4.0  |

### [サークルの不透明度](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-circle-circle-opacity)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`から`1`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`1`です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

円が描かれる不透明度。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.20.0  | > = 5.0.0   | > = 3.5.0 | > = 0.4.0  |

### [circle-pitch-alignment](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-circle-circle-pitch-alignment)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"map"`,`"viewport"`のいずれか。 デフォルトは`"viewport"`です。

マップがピッチングされたときの円の方向。

`"map"`：
円はマップの平面に位置合わせされます。

`"viewport"`：
円はビューポートの平面に位置合わせされます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.39.0  | > = 5.2.0    | > = 3.7.0 | > = 0.6.0  |

### [サークルピッチスケール](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-circle-circle-pitch-scale)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"map"`,`"viewport"`のいずれか。 デフォルトは`"map"`です。

マップがピッチングされたときの円のスケーリング動作を制御します。

`"map"`：
円は、カメラまでの見かけの距離に応じて拡大縮小されます。

`"viewport"`：
円はスケーリングされません。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.21.0	|  > = 4.2.0	|  > = 3.4.0	|  > = 0.2.1  |

### [円半径](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-circle-circle-radius)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。ピクセル単位。 デフォルトは`5`です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

円の半径。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |
| データ駆動型のスタイリング | > = 0.18.0   | > = 5.0.0    | > = 3.5.0 | > = 0.4.0  |

### [サークルソートキー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-circle-circle-sort-key)

[レイアウト](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-property)プロパティ。 オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。

この値に基づいて機能を昇順で並べ替えます。ソートキーが高い機能は、ソートキーが低い機能の上に表示されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 1.2.0	|　　　> = 9.2.0	　|　　> = 5.9.0	|　　> = 0.16.0  |
| データ駆動型のスタイリング | > = 1.2.0	|　　　> = 9.2.0	　|　　> = 5.9.0	|　　> = 0.16.0  |

### [サークルストロークカラー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-circle-circle-stroke-color)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは`＃000000`です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

円のストロークの色。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.29.0   | > = 5.0.0	| > = 3.5.0	| > = 0.4.0  |
| データ駆動型のスタイリング |  > = 0.29.0   | > = 5.0.0	| > = 3.5.0	| > = 0.4.0 |

### [サークル-ストローク-不透明度](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-circle-circle-stroke-opacity)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`から`1`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`1`です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

円のストロークの不透明度。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.29.0   | > = 5.0.0	| > = 3.5.0	| > = 0.4.0  |
| データ駆動型のスタイリング |  > = 0.29.0   | > = 5.0.0	| > = 3.5.0	| > = 0.4.0 |

### [サークルストローク幅](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-circle-circle-stroke-width)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。ピクセル単位。 デフォルトは`0`です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

円のストロークの幅。 ストロークは、円の半径の外側に配置されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.29.0   | > = 5.0.0	| > = 3.5.0	| > = 0.4.0  |
| データ駆動型のスタイリング |  > = 0.29.0   | > = 5.0.0	| > = 3.5.0	| > = 0.4.0 |

### [サークル翻訳](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-circle-circle-translate)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)の[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)。ピクセル単位。デフォルトは`[0,0]`。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

ジオメトリのオフセット。値は[x、y]で、負の値はそれぞれ左と上を示します。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [サークル翻訳-アンカー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-circle-circle-translate-anchor)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"map"`,`"viewport"`のいずれか。 デフォルトは`"map"`です。

`circle-translate`の参照フレームを制御します。

`"map"`：
円はマップを基準にして平行移動されます。

`"viewport"`：
円はビューポートを基準にして平行移動されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

### [視認性](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-visibility)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"visible"`,`"none"`のいずれか。 デフォルトは`"visible"`です。

このレイヤーが表示されるかどうか。

`"visible"`：
レイヤーが表示されます。

`"none"`：
レイヤーは表示されていません。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | >= 0.10.0    | >= 2.0.1    | >= 2.0.0 | >= 0.1.0  |

## [塗りつぶし-押し出し](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#fill-extrusion)

`fill-extrusion`スタイルレイヤーは、マップ上に1つ以上の塗りつぶされた（およびオプションでストロークされた）押し出し（3D）ポリゴンをレンダリングします。 塗りつぶし押し出しレイヤーを使用して、ポリゴンまたはマルチポリゴンフィーチャの押し出しと外観を構成できます。

### [fill-extrusion-base](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-extrusion-fill-extrusion-base)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。メートル単位。 デフォルトは`0`です。fill-extrusion-heightが必要です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

このレイヤーのベースを押し出す高さ。`fill-extrusion-heigh`以下である必要があります。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.27.0	| > = 5.1.0	| > = 3.6.0	| > = 0.5.0  |
| データ駆動型のスタイリング | > = 0.27.0	| > = 5.1.0	| > = 3.6.0	| > = 0.5.0  |

### [塗りつぶし-押し出し-色](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-extrusion-fill-extrusion-color)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは`"＃000000"`です。fill-extrusion-patternによって無効にされます。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

押し出した塗りつぶしのベースカラーです。押し出しの表面は、この色とルート`light`の設定の組み合わせによって、異なるシェーディングが行われます。この色がアルファ成分を含む`rgba`として指定された場合、アルファ成分は無視されます。レイヤーの不透明度を設定するには、`fill-extrusion-opacity`を使用してください。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.27.0	| > = 5.1.0	| > = 3.6.0	| > = 0.5.0  |
| データ駆動型のスタイリング | > = 0.27.0	| > = 5.1.0	| > = 3.6.0	| > = 0.5.0  |

### [塗りつぶし-押し出し-高さ](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-extrusion-fill-extrusion-height)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。メートル単位。 デフォルトは`0`です。fill-extrusion-heightが必要です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

このレイヤーのベースを押し出す高さ。fill-extrusion-height以下である必要があります。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.27.0	| > = 5.1.0	| > = 3.6.0	| > = 0.5.0  |
| データ駆動型のスタイリング | > = 0.27.0	| > = 5.1.0	| > = 3.6.0	| > = 0.5.0  |

### [塗りつぶし-押し出し-不透明度](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-extrusion-fill-extrusion-opacity)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`から`1`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`1`です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

塗りつぶし押し出しレイヤー全体の不透明度。これはレイヤー単位でレンダリングされ、フィーチャー単位ではないので、データ駆動型のスタイリングは利用できない。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.27.0	| > = 5.1.0	| > = 3.6.0	| > = 0.5.0  |

### [塗りつぶし押し出しパターン](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-extrusion-fill-extrusion-pattern)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[resolvedImage](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#resolvedImage)。移行可能。

押し出し塗りつぶしに画像を描画するために使用するスプライトの画像の名前。シームレスパターンの場合、画像の幅と高さは2倍（2、4、8、...、512）である必要があります。ズームに依存する式は、整数のズームレベルでのみ評価されることに注意してください。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.27.0	| > = 5.1.0	| > = 3.6.0	| > = 0.5.0  |
| データ駆動型のスタイリング | > = 0.49.0	| > = 6.5.0	| > = 4.4.0	| > = 0.11.0 |

### [塗りつぶし-押し出し-変換](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-extrusion-fill-extrusion-translate)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)の[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)。ピクセル単位。デフォルトは`「0,0」`。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

ジオメトリのオフセット。値は[x、y]で、負の値はそれぞれ左と上（平面上）を示します。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.27.0	| > = 5.1.0	| > = 3.6.0	| > = 0.5.0  |

### [fill-extrusion-translate-anchor](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-extrusion-fill-extrusion-translate-anchor)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"map"`,`"viewport"`のいずれか。 デフォルトは`"map"`です。fill-extrusion-translateが必要です。

fill-extrusion-translateの参照フレームを制御します。

`"map"`：
塗りつぶしの押し出しは、マップを基準にして平行移動されます。

`"viewport"`：
塗りつぶしの押し出しは、ビューポートを基準にして変換されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.27.0	| > = 5.1.0	| > = 3.6.0	| > = 0.5.0  |

### [fill-extrusion-vertical-gradient](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-extrusion-fill-extrusion-vertical-gradient)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[ブルー値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#boolean)。デフォルトは`true`。

塗りつぶし押し出しレイヤーの側面に垂直方向のグラデーションを適用するかどうか。trueの場合、側面はさらに下に向かって少し暗くなります。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.50.0	| > = 7.0.0	| > = 4.7.0	| > = 0.13.0  |

### [視認性](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-visibility)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"visible"`,`"none"`のいずれか。 デフォルトは`"visible"`です。

このレイヤーが表示されるかどうか。

`"visible"`：
レイヤーが表示されます。

`"none"`：
レイヤーは表示されていません。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.27.0	| > = 5.1.0	| > = 3.6.0	| > = 0.5.0  |

## [ヒートマップ](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#heatmap)

スタイルレイヤーは、領域内の`heatmap`ポイントの密度を表すために色の範囲をレンダリングします。

### [ヒートマップカラー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-heatmap-heatmap-color)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは`["interpolate",["linear"],["heatmap-density"],0,"rgba(0, 0, 255, 0)",0.1,"royalblue",0.3,"cyan",0.5,"lime",0.7,"yellow",1,"red"]`。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

ヒートマップの密度値に基づいて、各ピクセルの色を定義します。`["heatmap-density"]`を入力として使用する式である必要があります。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.41.0	| > = 6.0.0	| > = 4.0.0	| > = 0.7.0  |
| データ駆動型のスタイリング | まだサポートされていません	| まだサポートされていません	| まだサポートされていません	| まだサポートされていません |

### [ヒートマップ-強度](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-heatmap-heatmap-intensity)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。デフォルトは`1`です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

`heatmap-weight`に似ていますが、ヒートマップの強度をグローバルに制御します。 主にズームレベルに基づいてヒートマップを調整するために使用されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.41.0	| > = 6.0.0	| > = 4.0.0	| > = 0.7.0  |

### [ヒートマップ-不透明度](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-heatmap-heatmap-opacity)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`から`1`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`1`です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

ヒートマップレイヤーが描画されるグローバルな不透明度。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.41.0	| > = 6.0.0	| > = 4.0.0	| > = 0.7.0  |

### [ヒートマップ-半径](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-heatmap-heatmap-radius)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`1`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。ピクセル単位。デフォルトは`30`です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

1つのヒートマップポイントの影響の半径（ピクセル単位）。 値を大きくすると、ヒートマップはスムーズになりますが、詳細度は低くなります。 ヒートマップレイヤーの`queryRenderedFeatures`は、この半径内のポイントを返します。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.41.0	| > = 6.0.0	| > = 4.0.0	| > = 0.7.0  |
| データ駆動型のスタイリング | > = 0.43.0	| > = 6.0.0	| > = 4.0.0	| > = 0.7.0 |

### [ヒートマップの重み](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-heatmap-heatmap-weight)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`以上のオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。デフォルトは`1`です。[`機能状態`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#feature-state)および[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

個々のポイントがヒートマップにどの程度貢献しているかの尺度。値10は、同じ場所に10ポイントの重み1があることと同じです。クラスタリングと組み合わせると特に便利です。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.41.0	| > = 6.0.0	| > = 4.0.0	| > = 0.7.0  |
| データ駆動型のスタイリング | > = 0.41.0	| > = 6.0.0	| > = 4.0.0	| > = 0.7.0 |

### [視認性](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-visibility)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"visible"`,`"none"`のいずれか。 デフォルトは`"visible"`です。

このレイヤーが表示されるかどうか。

`"visible"`：
レイヤーが表示されます。

`"none"`：
レイヤーは表示されていません。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.41.0	| > = 6.0.0	| > = 4.0.0	| > = 0.7.0  |

## [陰影起伏](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#hillshade)

`hillshade`スタイル層は、クライアント側のデジタル標高モデル（DEM）データをレンダリングします。実装は、Mapbox TerrainRGBおよびMapzenTerrariumタイルのみをサポートします。

### [陰影起伏の色](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-hillshade-hillshade-accent-color)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは`"＃000000"`です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

鋭い崖や峡谷などの起伏の多い地形を強調するために使用される陰影の色。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.43.0	| > = 6.0.0	| > = 4.0.0	| > = 0.7.0 |

### [陰影起伏-誇張](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-hillshade-hillshade-exaggeration)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`から`1`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`0.5`です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

陰影起伏の強さ。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.43.0	| > = 6.0.0	| > = 4.0.0	| > = 0.7.0 |

### [陰影起伏-ハイライト-色](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-hillshade-hillshade-highlight-color)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは`"＃FFFFFF"`です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.43.0	| > = 6.0.0	| > = 4.0.0	| > = 0.7.0 |

### [陰影起伏-照明-アンカー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-hillshade-hillshade-illumination-anchor)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"map"`,`"viewport"`のいずれか。 デフォルトは`"map"`です。

マップを回転させたときの光源の方向。

`"map"`：
陰影起伏の照明は北方向を基準にしています。

`"viewport"`：
陰影起伏の照明は、ビューポートの上部を基準にしています。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.43.0	| > = 6.0.0	| > = 4.0.0	| > = 0.7.0 |

### [陰影起伏-照明-方向](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-hillshade-hillshade-illumination-direction)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`から`359`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。デフォルトは`335`です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

`hillshade-illumination-anchor`が`viewport`に設定されている場合はビューポートの上部として0を使用し、`hillshade-illumination-anchor`が`map`に設定されている場合は真北で、ヒルシェーディングを生成するために使用される光源の方向。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.43.0	| > = 6.0.0	| > = 4.0.0	| > = 0.7.0 |

### [陰影起伏の色](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-hillshade-hillshade-shadow-color)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは`"＃000000"`です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

光源とは反対側の領域のシェーディングカラー。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.43.0	| > = 6.0.0	| > = 4.0.0	| > = 0.7.0 |

### [視認性](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-visibility)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"visible"`,`"none"`のいずれか。 デフォルトは`"visible"`です。

このレイヤーが表示されるかどうか。

`"visible"`：
レイヤーが表示されます。

`"none"`：
レイヤーは表示されていません。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 0.43.0	| > = 6.0.0	| > = 4.0.0	| > = 0.7.0  |

## [空](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#sky)

`sky`スタイルレイヤーは、マップ全体を含む定型化された球形のドームをレンダリングし、すべてのレイヤーの背後に自動的にレンダリングされます。これを使用して、地平線の上の領域を、特定の時刻を表すシミュレートされた空、または定型化されたカスタムグラデーションで埋めることができます。

### [空-大気-色](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-sky-sky-atmosphere-color)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは`"white"`です。 スカイタイプは`"atmosphere"`である必要があります。

主な大気散乱係数を微調整するために使用される色。白を使用すると、デフォルトの係数が適用され、大気に自然な青色が与えられます。この色は、散乱中に対応する波長がどの程度表されるかに影響します。アルファチャネルは、大気の密度を表します。最大密度は1、密度は0です。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 2.0.0	| > = 10.0.0	| > = 10.0.0	| まだサポートされていません  |

### [空-大気-ハローカラー](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-sky-sky-atmosphere-halo-color)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは`"white"`です。 スカイタイプは`"atmosphere"`である必要があります。

大気の太陽の光輪に適用される色。アルファチャネルは、大気の空のレイヤーで太陽のハローがどれだけ強く表現されているかを表します。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 2.0.0	| > = 10.0.0	| > = 10.0.0	| まだサポートされていません  |

### [空-大気-太陽](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-sky-sky-atmosphere-sun)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`00`から`360180`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)の[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)。度単位。スカイタイプは`"atmosphere"`である必要があります。

太陽の中心の位置「方位角、p極角」。方位角は、北緯0度を基準にした太陽の位置を示し、度は時計回りに進みます。極角は太陽の高さを示します。ここで、0°は真上、天頂、90°は地平線です。このプロパティを省略すると、太陽の中心はライトの位置から直接継承されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 2.0.0	| > = 10.0.0	| > = 10.0.0	| まだサポートされていません  |

### [空-大気-太陽の強度](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-sky-sky-atmosphere-sun-intensity)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`から`100`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`10`です。スカイタイプは`"atmosphere"`である必要があります。

大気中の光源としての太陽の強度（0から100までのスケール）。値を大きくすると空が明るくなります。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 2.0.0	| > = 10.0.0	| > = 10.0.0	| まだサポートされていません  |

### [空のグラデーション](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-sky-sky-gradient)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[色](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#color)。デフォルトは`["interpolate",["linear"],["sky-radial-progress"],0.8,"#87ceeb",1,"white"]`です。 スカイタイプは`gradient`である必要があります。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。

空を着色するための放射状のカラーグラデーションを定義します。 色の値は、`sky-radial-progress`を使用した式で補間できます。 内挿の範囲[0、1]は、`sky-gradient-center`で指定された位置を中心とする[0、`sky-gradient-radius`]の半径距離（度単位）をカバーします。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 2.0.0	| > = 10.0.0	| > = 10.0.0	| まだサポートされていません  |
| データ駆動型のスタイリング | まだサポートされていません	| まだサポートされていません	| まだサポートされていません	| まだサポートされていません |

### [空のグラデーションセンター](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-sky-sky-gradient-center)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`00`から`360180`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)の[配列](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#array)。デフォルトは`[0,0]`です。スカイタイプは`"gradient"`である必要があります。

グラデーションの中心の位置「方位角、p極角」。方位角は、北に0度を基準にしたグラデーションの中心の位置を示します。ここで、度は時計回りに進みます。極角は、グラデーションの中心の高さを示します。ここで、0°は真上、天頂、90°は地平線です。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 2.0.0	| > = 10.0.0	| > = 10.0.0	| まだサポートされていません  |

### [空のグラデーション半径](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-sky-sky-gradient-radius)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`から`180`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`90`です。スカイタイプは`gradient`である必要があります。

`sky-gradient-center`からグラデーションが伸びるまでの角距離（度単位で測定）。 値が180の場合、グラデーションは`sky-gradient-center`から反対方向に折り返されます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 2.0.0	| > = 10.0.0	| > = 10.0.0	| まだサポートされていません  |

### [空の不透明度](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-sky-sky-opacity)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。`0`から`1`までのオプションの[数値](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#number)。 デフォルトは`1`です。[`補間`](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/#interpolate)式をサポートします。移行可能。

空のレイヤー全体の不透明度。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 2.0.0	| > = 10.0.0	| > = 10.0.0	| まだサポートされていません  |

### [スカイタイプ](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-sky-sky-type)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"gradient"`,`"atmosphere"`のいずれか。 デフォルトは`"atmosphere"`です。

空のタイプ。

`"gradient"`：
`sky-gradient-radius`と`sky-gradient`で構成できるグラデーションで空をレンダリングします。

`"atmosphere"`：
シミュレートされた大気散乱アルゴリズムを使用して空をレンダリングします。太陽の方向を光の位置に関連付けるか、`sky-atmosphere-sun`を介して明示的に設定できます。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 2.0.0	| > = 10.0.0	| > = 10.0.0	| まだサポートされていません  |

### [視認性](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#layout-symbol-visibility)

[ペイント](https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-property)プロパティ。オプションの[列挙型](https://docs.mapbox.com/mapbox-gl-js/style-spec/types/#enum)。`"visible"`,`"none"`のいずれか。 デフォルトは`"visible"`です。

このレイヤーが表示されるかどうか。

`"visible"`：
レイヤーが表示されます。

`"none"`：
レイヤーは表示されていません。

| SDK サポート  | Mapbox GL JS | Android SDK | iOS SDK  | macOS SDK |
| ------------ | ------------ | ----------- | -------- | --------- |
| 基本機能 | > = 2.0.0	| > = 10.0.0	| > = 10.0.0	| まだサポートされていません  |
