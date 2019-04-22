## Application Service > Maps > Webマップv2.0ガイド

Maps Webマップを使用するのに必要なAPIを説明します。

## v2.0改善事項
* マップの標準関連機能を拡大
  * HTML5基盤マップの主な機能を使用できます。
  * マップ内イメージ、マーカーなど、すべての事物(Feature)をオブジェクト化してユーザビリティおよび性能を改善しました。
* マップの回転が可能
  * モバイルでは、2本の指でマップを回転できます。
  * PCでは、Shift+Alt+ドラッグか、任意の角度を設定してマップを回転できます。
* フィーチャークラスター(図形除外)
  * マップ縮小時には近接したフィーチャーを平行して表示し、拡大時には詳しく分けて表示します。
* マップのイメージをダウンロード
  * マップをイメージファイルでダウンロードできる関数(function)を提供します。
* オーバービュー
  * マップを画面に1つ以上表示できます。
* マップロードイベントおよびアニメーション効果の追加
  * タイルイメージにロードイベントを追加する機能を提供します。
  * イメージロードに伴うプログレスバー(progress bar)効果などに活用できます。
* プリロードタイル
  * 一度確認した領域のイメージをキャッシュして表示します。
* KML/GPX形式ファイルの処理
  * KML/GPXファイルを読み込んでマップに表示し、マップに表示されたデータをKML/GPX形式で返すことができます。

## API共通情報

### 事前準備
- APIを使用するにはアプリケーションキーが必要です。
- アプリケーションキーは、**TOAST Console**上部にある**URL & Appkey**メニューで確認できます。

### リクエスト共通情報

#### URL情報

| 項目 | URL                                      |
| --------- | ---------------------------------------- |
| マップ | https://api-maps.cloud.toast.com/maps/js/v2.0/map.js |
| 静的(static)マップ | https://api-maps.cloud.toast.com/maps/js/v2.0/staticMap.js |

## Webマップ

### 1. Webマップ

JavaScript基盤のTOAST Maps APIを利用して、Webブラウザにマップを表示する方法を説明します。
TOAST Maps APIは、THINKWARE座標を使用します。縮約してTW座標、TW X座標、TW Y座標で表示します。
メソッドでオプションのパラメータは[param]と表示します。オプションのパラメータは省略できます。

> ※ TOAST Maps APIで使用する座標は、THINKWARE専用座標にのみ使用されます。
> <br>THINKWARE座標を経緯度座標(WGS84)に変換するには、THINKMAP.tw_Wgs84()関数を利用します。
> 反対に経緯度座標(WGS84)をTHINKWARE座標に変換するには、THINKMAP.wgs84_Tw()関数を利用します。

#### 主要TOAST Maps API案内
##### TOAST Maps APIの詳細な使用方法は、<a href="http://developers1.inavi.com:8086?key=19b6272o5" target="_blank" rel="nofollow">Thinkware API Center</a>を参照してください。

| API名                                   | Parameter                        | Returns                                  | 説明                                |
| ---------------------------------------- | -------------------------------- | ---------------------------------------- | ---------------------------------------- |
| new thinkware.maps.Map(map_div, option)  | map_div : String                 |                                          | マップを表示するDOM要素(element)または要素のID             |
|                                          | option.type：String             |                                          | マップのタイプ <br> 'i'：一般マップ、<br> 'm'：モバイルマップ、<br> 's'：要約マップ、<br> 'a'：航空写真、<br> 'm_a'：モバイル航空写真、<br> 's_a'：要約航空写真、<br> 'hybrid'：航空<br>default：'i' |
|                                          | option.center.twX：number       |                                          | マップ中心のX座標：THINKWARE座標単位            |
|                                          | option.center.twY：number       |                                          | マップ中心のY座標：THINKWARE座標単位            |
|                                          | option.level : number            |                                          | マップのレベル                            |
|                                          | option.callback : function()     |                                          | 初期化後に実行する関数                       |
|                                          | option.logo : String             |                                          | ロゴを表示する位置<br> top-left,<br>  top-center,<br>  top-right,<br>  center-left,<br>  center-center,<br>  center-right,<br>  bottom-left,<br>  bottom-center,<br>  bottom-right |
| changeType(type)                         | type : String                    |                                          | マップのタイプ <br> 'i'：一般マップ、<br> 'm'：モバイルマップ、<br> 's'：要約マップ、<br> 'a'：航空写真、<br> 'm_a'：モバイル航空写真、<br> 's_a'：要約航空写真、<br> 'hybrid'：航空<br>default：'i' |
| thinkware.maps.event.addListener(target, event_type, func_cb) | target : Object                  |                                          | リスナーを追加する対象オブジェクト                    |
|                                          | event_type : String              |                                          | wheelup, <br> wheeldown, <br> wheel, <br>zoomend, <br>movestart, <br>move, <br>moveend, <br>tileloadstart, <br>tileloadend, <br>tileloaderror, <br>click, <br>dblclick, <br>rightclick, <br>mousemove, <br>mouseup, <br>mousedown |
|                                          | func_cb : function()             |                                          | 登録するリスナー                           |
| thinkware.maps.event.removeListener(target, event_type, func_cb) | target : Object                  |                                          | リスナーを削除する対象オブジェクト                    |
|                                          | event_type : String              |                                          | wheelup, <br> wheeldown, <br> wheel, <br>zoomend, <br>movestart, <br>move, <br>moveend, <br>tileloadstart, <br>tileloadend, <br>tileloaderror, <br>click, <br>dblclick, <br>rightclick, <br>mousemove, <br>mouseup, <br>mousedown |
|                                          | func_cb : function()             |                                          | 削除するリスナー                           |
| new thinkware.maps.Marker(option)        | option.map : Object              | thinkware.maps.Markerマーカーオブジェクト       | マップオブジェクト                             |
|                                          | option.icon.url : String         |                                          | アイコンURL                                   |
|                                          | option.icon.size.width : number  |                                          | アイコンの幅                                  |
|                                          | option.icon.size.heigth : number |                                          | アイコンの高さ                                  |
|                                          | option.position.twX : number     |                                          | マーカー作成X座標(THINKWARE座標単位)                     |
|                                          | option.position.twY : number     |                                          | マーカー作成Y座標(THINKWARE座標単位)                     |
|                                          | option.positioning : String      |                                          | 座標が位置する場所<br> top-left,<br>  top-center,<br>  top-right,<br>  center-left,<br>  center-center,<br>  center-right,<br>  bottom-left,<br>  bottom-center,<br>bottom-right |
|                                          | option.title : String            |                                          | ツールチップ文字列                            |
|                                          | option.offset.pxX : number       |                                          | pixel単位                             |
|                                          | option.offset.pxY : number       |                                          | pixel単位                             |
|                                          | option.visible : boolean         |                                          | 表示するかどうか                                   |
|                                          | option.draggable : boolean       |                                          | ドラッグ可能かどうか                               |
|                                          | option.zIndex : number           |                                          | z-index値                         |
|                                          | option.opacity : number          |                                          | 透明度                                     |
|                                          | option.stopEvent : boolean       |                                          | マーカー上でマップイベントの実行を防止するかどうか                   |
| thinkware.maps.LineString.drawStart(target, option) | target : Object                  |                                          | マップオブジェクト                             |
|                                          | option.stroke.style：String     |                                          | 線のスタイル<br><br> dot：· · · · · · <br>dash：- - - - - -<br>dashdot：- · - · - · - <br>longdashdot：ㅡ·ㅡ·ㅡ<br> solid：実線 |
|                                          | option.stroke.weight : number    |                                          | 線の太さ(px)                                 |
|                                          | option.stroke.color : String     |                                          | 線の色                                    |
|                                          | option.stroke.opacity : number   |                                          | 線の透明度                                   |
|                                          | option.callback : function()     |                                          | 描写終了後に実行する関数                    |
|                                          | option.measure : boolean         |                                          | 距離測定ポップアップを表示するかどうか                          |
|                                          | option.isOnce : boolean          |                                          | 1回描写後に終了するかどうか                          |
| thinkware.maps.LineString.drawEnd(target) | target : Object                  |                                          | マップオブジェクト                             |
| thinkware.maps.util.getLonLatFromCoordinate(param) | param.twX : number               | Coord座標<br>Object.lon : WGS84<br>Object.lat : WGS84 | THINKWARE  X座標                          |
|                                          | param.twY : number               |                                          | THINKWARE  Y座標                          |
| thinkware.maps.util.getCoordinateFromLonLat(param) | param.lon : number               | TW座標<br>Object.twX: TW X座標<br>Object.twY : TW Y座標 | 経度                                 |
|                                          | param.lat : number               |                                          | 緯度                                 |


#### TOAST Maps APIの使用
```
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v2.0/map.js"></script>
<script>
	//マップを使用するための認証を進行します。
	Map.authentification("appKey");
</script>

<div id="div_map"></div>
<script type="text/javascript">

	//宣言したDIVにマップを表示します。
	var map = new thinkware.maps.Map("div_map", {
		center: {
			twX: 169030,
			twY: 517922
		},
		level: 12,
		type: "i",
		callback: success = function() {
			console.log("map init success!");
		}
	});
</script>
```

#### マップモードの変更
```
<script type="text/javascript">

 	// 作成されたマップオブジェクトのマップTypeを変更します。
 	// 一般：i、モバイル：m、要約：s、航空写真：a、モバイル航空：m_a、要約航空：s_a、航空：hybrid
	// 航空写真に変更します。
	map.changeType('i');

</script>
```

#### マップにイベントを登録
```
<script type="text/javascript">

	//マップにmoveイベントを登録します。
	thinkware.maps.event.addListener(map, 'click', mapEvent_cb)

	 //マップイベント発生時のコールバック関数
    function mapEvent_cb(event){
        console.log("event callback!");
    }

</script>
```

#### マップのイベントを削除
```
<script type="text/javascript">

	//マップからmoveイベントを削除します。
	thinkware.maps.event.removeListener(map, 'move', mapEvent_cb)

</script>
```

#### マップマーカーの追加
```
<script type="text/javascript">

	// マップにマーカーオブジェクトを追加します。
	var marker = new thinkware.maps.Marker({
	    map: map,
	    position: {
	        twX: 169030,
	        twY: 517922
	    },
	    stopEvent: false
	});

	// マップにマーカーオブジェクトを移動させます。
	marker.setPosition({twX: 169030, twY: 517922});

</script>
```

#### マップ描写モードに切り替え
```
<script type="text/javascript">

	// 描写モードに切り替えます。
	var strokeOpt = {
		style : 'longdash'	// 線のスタイル(solid, dash, longdash, ... またはsegmentsを返す関数を参照) default: "solid"
		, weight : 5		// 線の太さ(px) (default: 3)
		, color : '#3399ff'	//線の色(default: #3399ff)
		, opacity : 1		//線の透明度(default: 1)
    };

	var drawOpt = {
		stroke : strokeOpt
		, callback : mapDraw_cb // 描写終了後に実行する関数(default: undefined)
		, measure : true 		// 距離測定ポップアップを表示するかどうか(default: false)
		, isOnce : false		// 1回描写後に終了するかどうか(default: false)
	};

	//thinkware.maps.LineString.drawStart(map, drawOpt);

	function mapDraw_cb(map){
		console.log("draw finish!!!");
	}
</script>
```

#### マップ描写モードの終了
```
<script type="text/javascript">

	// 描写モードを終了します。
	thinkware.maps.LineString.drawEnd(map);

</script>
```

#### TW座標をWGS座標に変換
```
<script type="text/javascript">

 	// TW座標をWGS座標に変換します。
 	var tws = {
		twX : 169030
		, twY: 517922
 	};

 	var wgs84 = thinkware.maps.util.getLonLatFromCoordinate(tws);
 	console.log(wgs84.lon);
 	console.log(wgs84.lat);

</script>
```

#### WGS座標をTW座標に変換
```
<script type="text/javascript">

 	 // WGS座標をTW座標に変換します。
	 var wgs84 = {
		lon: 127.11074994024005
		, lat: 37.40215870673785
	};

	 var tws = thinkware.maps.util.getCoordinateFromLonLat(wgs84);

 	console.log(tws.twX);
 	console.log(tws.twY);

</script>
```

### 2. 静的(static)マップ

#### TOAST Maps APIで静的マップの使用
```
// 静的マップを使用するためのjsファイルを宣言します。
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v2.0/staticMap.js"></script>

// マップを入れるIMGを作成します。
<img id='staticMapImg' alt="" src="">

<script>

	// 静的マップを使用するための認証およびパラメータを渡します。 	
	StaticMap.authentification('staticMapImg',"appkey",'x=157423&y=266836&width=970&height=300&level=10&maptype=i&mx=158323&my=266836&txt=');

</script>
```

| 名前 | タイプ | 必須かどうか | 説明                     |
| ------- | ------- | ----- | ----------------------------- |
| x       | Integer | 必須 | マップ中心のX座標              |
| y       | Integer | 必須 | マップ中心のY座標              |
| mx      | Integer | 必須 | マーカーのX座標                 |
| my      | Integer | 必須 | マーカーのY座標                 |
| width   | Integer | 任意 | マップの幅<br>未入力時は基本600px     |
| height  | Integer | 任意 | マップの高さ<br>未入力時は基本600px     |
| imgurl  | String  | 任意 | マーカーイメージURL<br> 未入力時は基本マーカーを使用 |
| level   | Integer | 任意 | マップレベル <br> 未入力時は基本10        |
| maptype | String  | 任意 | マップタイプ <br> 未入力の時は基本一般マップ      |
| label   | String  | 任意 | ラベルの内容                  |

### 3. モバイルWebマップ

Android/iOS WebViewで使用できるハイブリッド型のアプリを開発する時、TOAST Maps APIを利用し、JavaScript基盤のWebマップと同じAPIで使用できます。
APIの詳細は、[1. Webマップ](#1-web)を参照してください。

#### TOAST Maps APIをMobileで使用
```
<!DOCTYPE html>
<html>
    <head>
		// モバイル端末に合わせてviewportを設定します。
        <meta name="viewport" content="width=device-width, initial-scale=1,user-scalable=no">

		<style>
			body {
	    		margin: 0;
	      	}

  			#div_map {
				position: absolute;
				width: 100%;
				height: 100%;
			}
    	</style>

		// マップを使用するためのjsファイルを宣言します。
		<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v2.0/map.js"></script>
		<script>
			// マップを使用するための認証を進行します。
			Map.authentification("appKey");
		</script>
	</head>

	<body>

		//マップを入れるDIVを作成します。
		<div id="div_map"></div>
		<script type="text/javascript">

			//宣言したDIVにマップを表示します。(モバイルマップタイプで'm'を宣言します。)
			var map = new thinkware.maps.Map("div_map", {
				center: {
					twX: 169030,
					twY: 517922
				},
				level: 12,
				type: "m",
				callback: success = function() {
					console.log("map init success!");
				}
			});
		</script>
	</body>

</html>
```
