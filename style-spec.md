# Style Specification スタイル仕様

Mapbox [スタイル](https://docs.mapbox.com/help/glossary/style/)とは、マップの視覚的な外観を定義する文書で、どのデータを描画するか、描画の順番、描画時のデータのスタイルなどを定義するものです。[スタイルドキュメント](https://docs.mapbox.com/help/glossary/style/)とは、マップの視覚的な外観を定義する文書で、どのデータを描画するか、描画の順番、描画時のデータのスタイルなどを定義するものです。スタイルドキュメントは、特定のルート(階層構造の親)レベルとネストされた(階層構造の子要素)プロパティを持つ [JSON](http://www.json.org/) オブジェクトです。本仕様では、これらのプロパティを定義し、説明しているものです。

この仕様書は以下の人を対象に書かれています。

- [Mapbox Studio](https://studio.mapbox.com/) を使用せず、手作業でスタイルを書きたい上級デザイナーやカートグラファーの方。

- [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/api/) または Mapbox Maps SDK for Androidを用いて地図を開発するエンジニア。

- Mapboxスタイルを生成または処理するソフトウェアの作者。

スタイル関連機能のドキュメントについて、Mapbox Maps SDK for iOS を使用する開発者は [iOS SDK API リファレンス](https://docs.mapbox.com/mapbox-gl-js/style-spec/#:~:text=iOS%20SDK%20API%20reference)を、Mapbox Maps SDK for macOS を使用する開発者は [macOS SDK API リファレンス](https://mapbox.github.io/mapbox-gl-native/macos/)を参照してください。

### スタイル ドキュメントの構造
Mapboxスタイルは[ルートプロパティ](https://docs.mapbox.com/mapbox-gl-js/style-spec/#:~:text=a%20set%20of-,root%20properties,-%2C%20some%20of%20which)のセットで構成され、その一部は単一のグローバルプロパティを記述し、一部はネストされたプロパティを含んでいます。[バージョン](https://docs.mapbox.com/mapbox-gl-js/style-spec/#:~:text=root%20properties%2C%20like-,version,-%2C%20name%2C%20and%20metadata)、[名前](https://docs.mapbox.com/mapbox-gl-js/style-spec/root/#name)、[メタデータ](https://docs.mapbox.com/mapbox-gl-js/style-spec/#:~:text=version%2C%20name%2C%20and-,metadata,-%2C%20don%27t%20have%20any)などのルートプロパティには、マップの外観や動作に影響を与えないものもありますが、マップに関連する重要な記述情報を提供します。特に、[レイヤー](https://docs.mapbox.com/mapbox-gl-js/style-spec/#:~:text=map.%20Others%2C%20like-,layers,-and%20sources%2C%20are)や[ソース](https://github.com/furuhashilab/StyleSpecification4mapbox/blob/main/Sources.md)などの他のプロパティの理解は重要で、どのマップ機能をマップに表示するか、またその外観を決定します。[center](https://docs.mapbox.com/mapbox-gl-js/style-spec/#:~:text=Some%20properties%2C%20like-,center,-%2C%20zoom%2C%20pitch%2C%20and)、[zoom](https://docs.mapbox.com/mapbox-gl-js/style-spec/#:~:text=properties%2C%20like%20center%2C-,zoom,-%2C%20pitch%2C%20and%20bearing)、[pitch](https://docs.mapbox.com/mapbox-gl-js/style-spec/#:~:text=like%20center%2C%20zoom%2C-,pitch,-%2C%20and%20bearing%2C%20provide)、[bearing](https://docs.mapbox.com/mapbox-gl-js/style-spec/#:~:text=zoom%2C%20pitch%2C%20and-,bearing,-%2C%20provide%20the%20map) などの一部のプロパティは、マップを最初に表示するときに使用する既定のセットをマップレンダラーに提供します。

## 原文
* https://docs.mapbox.com/mapbox-gl-js/style-spec/
