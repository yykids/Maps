## Application Service > Maps > iOS使用ガイド

iOSでMapsサービスを使用する方法を説明します。

## API共通情報

### 事前準備
- APIを使用するにはアプリケーションキーが必要です。
- アプリケーションキーは**TOAST Console**上部の**URL & Appkey**メニューで確認できます。

### リクエスト共通情報

#### URL情報
##### [マップAPI]

| 項目     | URL                                      |
| --------- | ---------------------------------------- |
| マップ     | https://api-maps.cloud.toast.com/maps/js/v1.0/map.js |
| 静的(static)マップ | https://api-maps.cloud.toast.com/maps/js/v1.0/staticMap.js |

## マップ

### 1. iOS WebViewマップ

iOSでAPIを呼び出し、コールバック関数でパラメータを受け取る方法を説明します。


#### A. 主要TOAST Maps iOS WebView API案内
##### TOAST Maps Android WebView APIの詳細な使用方法は<a href="http://developers1.inavi.com:8086?key=19b6272o5" target="_blank" rel="nofollow">Thinkware API Center</a>を参照してください。

> ※ TOAST Maps APIで使用する座標はTHINKWARE専用座標でのみ使用されます。
> <br>THINKWARE座標を経緯度座標(WGS84)に変換するには、TMWA.getWgs84FromTw()関数を利用します。反対に経緯度座標(WGS84)をTHINKWARE座標に変換するには、TMWA.getTwFromWgs84()関数を利用します。

| APIの名前                                | パラメータ               | コールバックメソッド        | コールバックパラメータ                               | 説明                                    |
| ---------------------------------------- | ---------------------------------------- | ---------------- | ---------------------------------------- | ---------------------------------------- |
| TMWI.initMap(map_div_name, twX, twY, level, arrange_type, map_type) | map_div : String<br>	マップを入れるdivタグID    | initCB <br><br>  | マップ初期化成否<br>'true'：成功<br> 'false'：失敗 | マップを使用するために最初に呼び出す必要がある初期化関数です。  |
|                                          | twX : Number	<br>マップ初期化TW X座標       |                  |                                          |                                          |
|                                          | twY : Number	<br>マップ初期化TW Y座標       |                  |                                          |                                          |
|                                          | level : Number	<br>マップ初期化Level<br>- 一般マップ：1～13<br>- 航空写真：1～13 |                  |                                          |                                          |
|                                          | arrange_type : Number	<br>マップレイヤーソート方式<br>1：中央ソート方式(resize効果あり)<br>2：全体ローディング方式(resize効果なし)<br> 3：右上ソート方式(resize効果あり) |                  |                                          |                                          |
|                                          | map_type : String	<br>マップタイプ設定<br>'i'：一般マップ<br>'a'：航空写真<br>'s'：要約マップ |                  |                                          |                                          |
| TMWI.getLevel()                          |                                          | getLevelCB       | マップの現在のレベル                             | マップのレベルを取得します。                           |
| TMWI.getCenter()                         |                                          | getCenterCB      | マップの現在の中心座標<br> 'twX&#124;twY'           | マップの中心座標を取得します。                         |
| TMWI.getExtent()                         |                                          | getExtentCB      | マップの領域座標<br> 'leftX&#124;topY&#124;rightX&#124;bottomY' | 現在マップが表示されている領域座標を取得します。                 |
| TMWI.setMoveend()                        |                                          | moveendCB        | 拡大、縮小、移動後のマップの中心座標とレベル<br>'twX&#124;twY&#124;level' | マップにmoveendイベントを登録します。<br>moveend：マップの拡大、縮小、移動が終わった時 |
| TMWI.removeMoveend()                     |                                          |                  |                                          | マップからmoveendイベントを削除します。                 |
| TMWI.setTouchend()                       |                                          | setTouchendCB    | タッチしたマップの座標<br> 'twX&#124;twY'             | マップにtouchendイベントを登録します。<br>  touchend：マップのタッチが終わった時 |
| TMWI.removeTouchend()                    |                                          |                  |                                          | マップからtouchendイベントを削除します。                |
| TMWI.setZoomend()                        |                                          | zoomendCB        | 拡大、縮小後のマップの中心座標とレベル<br> 'twX&#124;twY&#124;level' | マップにzoomendイベントを登録します。 <br> zoomend ：マップの拡大、縮小が終わった時 |
| TMWI.removeZoomend()                     |                                          |                  |                                          | マップからzoomendイベントを削除します。                 |
| TMWI.setTouchEvent(event_name)           | event_name : String<br>	登録するイベント名<br> 'touchstart'：マップのタッチを開始した時<br>  'touchend'：マップのタッチが終了した時<br>  'longpress'：マップを長押しした時 | setTouchEventCB  | 発生したイベントとタッチしたマップの座標 <br>'event_name&#124;twX&#124;twY' | マップにtouch関連イベントを登録します。                  |
| TMWI.removeTouchEvent(event_name)        | event_name : String<br>	登録するイベント名<br> 'touchstart'：マップのタッチを開始した時<br>  'touchend'：マップのタッチが終了した時<br>  'longpress'：マップを長押しした時 |                  |                                          | マップからtouch関連イベントを削除します。                 |
| TMWI.createAndAddMarker(twX, twY, iconWidth, iconHeight, iconUrl, [param]) | twX : Number<br>MarkerオブジェクトのTW X座標    | createMarkerCB   | MarkerオブジェクトIDとユーザー変数param<br> 'marker_id&#124;param' | Markerオブジェクトを作成し、マップに追加します。               |
|                                          | twY : Number	<br>MarkerオブジェクトのTW Y座標   |                  |                                          |                                          |
|                                          | iconWidth : Number <br>Markerイメージの横幅    |                  |                                          |                                          |
|                                          | iconHeight : Number <br>Markerイメージの高さ  |                  |                                          |                                          |
|                                          | iconURL : String <br>MarkerイメージのURL     |                  |                                          |                                          |
|                                          | param : String <br>Markerオブジェクトのユーザー変数  |                  |                                          |                                          |
| TMWI.setTouchendMarkerCB(id)             | id : Number<br>イベントを登録する対象MarkerオブジェクトID | touchendMarkerCB | MarkerオブジェクトIDとMarkerオブジェクトのTW X座標、TW Y座標、<br> ユーザー変数param<br> 'marker_id&#124;twX&#124;twY&#124;param' | Markerオブジェクトにtouchendイベントを登録します。          |
| TMWI.removeTouchendMarker(id)            | id : Number<br>イベントを削除する対象MarkerオブジェクトID |                  |                                          | Markerオブジェクトからtouchendイベントを削除します。          |
| TMWI.getTwFromWgs84(lon, lat)            | lon : Number<br>変換するWGS84経度座標       | getTwFromWgs84CB | 変換されたTW座標<br>'twX&#124;twY'             | WGS84座標をTW座標に変換します。                  |
|                                          | lat : Number<br>変換するWGS84緯度座標       |                  |                                          |                                          |
| TMWI.getWgs84FromTw(twX, twY)            | twX: Number<br>変換するTW X座標            | getWgs84FromTwCB | 変換されたWGS84座標<br>'lon&#124;lat'          | TW座標をWGS84座標に変換します。                  |
|                                          | twY : Number<br>変換するTW Y座標           |                  |                                          | -                                        |

