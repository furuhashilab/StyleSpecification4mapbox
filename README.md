# StyleSpecification4mapbox
Style Specification Current version: v13.23.0 https://docs.mapbox.com/mapbox-gl-js/style-spec/

## [STYLE SPECIFICATION Mapbox GL JS スタイル仕様](https://github.com/furuhashilab/StyleSpecification4mapbox/blob/main/style-spec.md)
* Root
* Light
* Sources
* Sprite
* Glyphs
* Transition
* Projection
* Terrain
* Fog
* Layers
* Types
* Expressions
* Other

Translated by Furuhashi Lab., UNVT team

# Mapbox style certification日本語訳
Mapbox スタイルとは、マップの視覚的な外観を定義する文書で、どのデータを描画するか、描画の順番、描画時のデータのスタイルなどを定義するものです。スタイル ドキュメントは、特定のルート レベルとネストされたプロパティを持つ JSON オブジェクトです。本仕様では、これらのプロパティを定義し、説明する。
この仕様の想定読者は以下の通りである。  
Mapbox Studio を使用せず、手作業でスタイルを書きたい上級デザイナーやカートグラファーの 方。  
Mapbox GL JS または Mapbox Maps SDK for Android のスタイル関連機能を使用する開発者。  
Mapbox スタイルを生成または処理するソフトウェアの作者。  
スタイル関連機能のプラットフォームに適したドキュメントについては、Mapbox Maps SDK for iOS を使用する開発者は iOS SDK API リファレンスを、Mapbox Maps SDK for macOS を使用する開発者は macOS SDK API リファレンスを参照してください。

