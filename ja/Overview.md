## Application Service > Maps > 概要

Mapsサービスは、長年ナビゲーション技術を蓄積してきたinaviサービスをマップ(Web、モバイル)とHTTP REST APIで提供します。
手軽で正確なマップ、検索、道検索など、多様な機能を使用できます。

## 主な機能


### マップAPI

- JavaScript基盤マップAPI
    - マップAPIを使用し、簡単かつ迅速にWebページからベクトル地図および航空写真を使用できます。
    - WebGLとVector Tileを一緒に利用することで、高解像度の滑らかなズーム、背景マップとデータレイヤー間の視覚化効果を様々な形でサポートします。
    - マップ移動、回転、傾き、拡大/縮小、マーカー、情報ウィンドウ、図形、マップタイプ変更、座標変換など、230個以上の多様な機能を提供します。
- モバイルマップSDK
    - Android、iOS用マップSDKを提供して、モバイル環境に最適化されたマップAppサービスの開発が可能です。
    - モバイルアプリケーションでマップ機能を実装できるように、多様なクラスとメソッドを提供します。
    - 鮮明な周期と地形空間データが解像度に合わせて最適化されて表示されます。

### 統合検索

- 統合検索機能の提供
    - 商号名、電話番号、住所(地番&道路名)を一度に検索できます。
- 多様な検索サービスの提供
    - 推薦ワード検索や下位施設の検索など、多様な検索サービスを提供します。
- Geocoding, Reverse Geocoding
    - 住所を座標に、座標を住所に変換するサービスを提供します。

### 道検索サービス(経路探索)

- 道案内サービスの提供
    - inaviナビゲーションと同じ機能の「道検索サービス」を通して、スマートで正確な道案内サービスを利用できます。
    - 詳細情報探索、要約情報探索、複数出発地探索、複数目的地探索機能など、状況に適した複数の探索オプションを提供します。
    
- リアルタイム交通情報の反映
    - リアルタイム交通情報を反映して、より正確で迅速な道案内を提供します。


## 重要用語整理

|用語| 説明|
|---|---|
| WGS84緯度、経度座標 | WGS84楕円体を使用する世界測地系です。緯度、経度球形座標系 |
| TW座標 | THINKWAREマップで使用する座標系(ThinkWare座標) |
| TM座標 | 横メルカトル図法(Transverse Mercator)<br>4個の原点を持ち、該当する原点からの距離を座標で表したものです。<br>任意の地域に対する基準地点を座標原点に決め、原点を中心にTM投影した平面上で原点を通る子午線をX軸、東西方向の緯度線Y軸に各地点の位置をm単位の平面の直角座標系で表示する |
| マップ周期 | 背景マップ上の情報表示データ。位置に合わせて情報を認識できるように表示する情報で、行政名や商号、役所、水系、道路名など、多様な情報のデータがある |
| 一般マップ/航空写真 | 一般マップ：一般背景データのマップで、PC Webマップに最適化されたマップ <br>航空写真：航空機で実際に撮影したマップ<br>
| 行政コード | 行政機関間の行政情報の円滑な共同利用を図るため、各級機関の行政業務に必要な行政コードを標準化し、決められた手続きに沿って制定したコード |
| 旧住所(地番住所) | 洞、里+地番の土地中心の住所体系 |
| 道路名住所 | 道路名+建物番号の建物中心の住所体系 |
| 範囲検索 | 領域、半径内を検索する検索方式<br>Extent検索：左上(X,Y)座標/右下(X,Y)座標の領域内を検索する検索方式 <br> Range検索：中心座標からの半径内を検索する検索方式 |
| POI | 関心地点またはPOI(Point of Interest)は、ナビゲーションなどの電子マップ上に表示された建物と商店などのこと |
| 下位施設 | 該当POIに属する施設情報(e.g.エバーランドの下位施設：1A駐車場、1B駐車場) |
| 経由地 | 経路探索時、出発地と目的地の間で経由する場所 |
| KML(Keyhole Markup Language) | 地理データを表示するためのXML標準基盤のファイル形式<br>Google Earthで使用するために開発され、現在Google、HERE Mapなど、複数の場所でサポートされている |
| GPX(GPS Exchange Format) | インターネットのアプリケーションとWebサービス間でGPSデータを交換するためのXML基盤のファイル形式<br> waypoint、route、trackに分かれ、地点と経路情報を表すことができる |
