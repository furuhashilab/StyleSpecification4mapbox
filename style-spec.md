# Style Specification

## 日本語訳
Mapbox スタイルとは、マップの視覚的な外観を定義する文書で、どのデータを描画するか、描画の順番、描画時のデータのスタイルなどを定義するものです。スタイル ドキュメントは、特定のルート レベルとネストされたプロパティを持つ JSON オブジェクトです。本仕様では、これらのプロパティを定義し、説明する。
この仕様の想定読者は以下の通りである。
<br>
<br>
Mapbox Studio を使用せず、手作業でスタイルを書きたい上級デザイナーやカートグラファーの 方。
<br>
<br>
Mapbox GL JS または Mapbox Maps SDK for Android のスタイル関連機能を使用する開発者。
<br>
<br>
Mapbox スタイルを生成または処理するソフトウェアの作者。  
スタイル関連機能のプラットフォームに適したドキュメントについては、Mapbox Maps SDK for iOS を使用する開発者は iOS SDK API リファレンスを、Mapbox Maps SDK for macOS を使用する開発者は macOS SDK API リファレンスを参照してください。

## 原文
A Mapbox style is a document that defines the visual appearance of a map: what data to draw, the order to draw it in, and how to style the data when drawing it. A style document is a JSON object with specific root level and nested properties. This specification defines and describes these properties.
The intended audience of this specification includes:
<br>
<br>
Advanced designers and cartographers who want to write styles by hand rather than use Mapbox Studio.
<br>
<br>
Developers using style-related features of Mapbox GL JS or the Mapbox Maps SDK for Android.
<br>
<br>
Authors of software that generates or processes Mapbox styles.
<br>
<br>
For platform-appropriate documentation of style-related features, developers using the Mapbox Maps SDK for iOS should consult the iOS SDK API reference, and developers using the Mapbox Maps SDK for macOS should consult the macOS SDK API reference.



