## Application Service > Maps > Webマップv1.0ガイド

Maps Webマップを使用するのに必要なAPIを説明します。

## API共通情報

### 事前準備
- APIを使用するにはアプリケーションキーが必要です。
- アプリケーションキーは、**TOAST Console**上部にある**URL & Appkey**メニューで確認できます。

### リクエスト共通情報

#### URL情報

| 項目 | URL                                      |
| --------- | ---------------------------------------- |
| マップ | https://api-maps.cloud.toast.com/maps/js/v1.0/map.js |
| 静的(static)マップ | https://api-maps.cloud.toast.com/maps/js/v1.0/staticMap.js |

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

| API名                                | Parameter               | Returns                                  | 説明                              |
| ---------------------------------------- | ----------------------- | ---------------------------------------- | ---------------------------------------- |
| THINKMAP.initMap(map_div_name, twX, twY, level, init_cb, arrange_type, map_type) | map_div : String        |                                          | マップ入れるdivタグID<br>マップを使用するために、最初に呼び出す必要がある初期化関数です。 |
|                                          | twX : Number            |                                          | マップ初期化TW X座標                  |
|                                          | twY : Number            |                                          | マップ初期化TW Y座標                  |
|                                          | level : Number          |                                          | マップ初期化レベル<br>- 一般マップ：1～13<br>- 航空写真：1～13 |
|                                          | init_cb : function()    |                                          | マップ初期化後に呼び出されるコールバック関数             |
|                                          | arrange_type : Number   |                                          | マップレイヤーソート方式<br>1：中央ソート方式(resize効果あり)<br>2：全体ローディング方式(resize効果なし)<br> 3：右上ソート方式(resize効果あり) |
|                                          | map_type : String       |                                          | マップタイプ設定<br>'i'：一般マップ<br>'a'：航空写真<br>'s'：要約マップ<br>'m'：モバイルマップ |
| THINKMAP.imageMap()                      |                         |                                          | マップを一般マップに切り替えます。                        |
| THINKMAP.aerialMap()                     |                         |                                          | マップを航空写真に切り替えます。                        |
| THINKMAP.setAerialHybrid(active)         | active: Boolean        |                                          | 航空周期を表示するかどうか <br>true：マップ上に航空周期を表示<br>false：マップ上に航空周期を表示しない<br><br>マップ上に航空写真周期を表示するかどうかを設定します。 |
| THINKMAP.addMapListener(event_name, func_cb) | event_name : String<br> |                                          | マップに登録するイベント名<br>'movestart'<br>- マップが動き始めた時<br>'move'<br> - マップが動く時<br>'moveend'<br>- マップの動きが終わった時<br>'zoomend'<br>- マップの拡大、縮小が終わった時<br>'mouseover'<br>- マップ上にマウスを移動させた時<br>'mouseout'<br>- マップの外にマウスを移動させた時<br> 'mousemove'<br>- マップでマウスが動く時<br><br>マップにイベントを登録します。<br>(マップに関連したイベント、拡大/縮小、動きなど) |
|                                          | func_cb : function()    |                                          | マップでイベントが発生した時に呼び出されるコールバック関数<br>(コールバック関数にパラメータとしてMapオブジェクトが渡されます) |
| THINKMAP.removeMapListener(event_name)   | event_name : String     |                                          | マップから削除するイベント名<br>'movestart'<br>- マップが動き始めた時<br>'move'<br> - マップが動く時<br>'moveend'<br>- マップの動きが終わった時<br>'zoomend'<br>- マップ拡大、縮小が終わった時<br>'mouseover'<br>- マップ上にマウスを移動させた時<br>'mouseout'<br>- マップの外にマウスを移動させた時<br> 'mousemove'<br>- マップでマウスが動く時<br><br>マップに登録したイベントを削除します。 <br>THINKMAP.addMapListenerメソッドに登録したevent_nameに該当するすべてのコールバック関数を削除するので注意してください。 |
| THINKMAP.createMarker(twX, twY, width, height, iconUrl, [param]) | twX : Number            |                                          | <br>Markerオブジェクト位置TW X座標 <br><br>Markerオブジェクトを作成します。 <br>作成したMarkerオブジェクトをマップに表示するには、THINKMAP.addMarkerメソッドでマップにMarkerオブジェクトを追加する必要があります。 |
|                                          | twY : Number            |                                          | Markerオブジェクト位置TW Y座標            |
|                                          | width : Number          |                                          | Markerイメージの幅                        |
|                                          | height : Number         |                                          | Markerイメージの高さ                       |
|                                          | iconURL : String        |                                          | MarkerイメージのURL                          |
|                                          | param : String          |                                          | Markerオブジェクトのユーザー変数               |
| THINKMAP.addMarker(marker)               | marker : Marker         |                                          | マップに追加する対象Markerオブジェクト<br><br>マップにMarkerオブジェクトを追加します。 |
| THINKMAP.featureDrawing(draw_type, style, func_cb) | draw_type : String      |                                          | ユーザーが描写するFeatureオブジェクトタイプ<br>'lineDraw'：線<br>'polygonDraw'：多角形<br> 'regularPolygonDraw'：形が決まっている多角形<br><br>ユーザーがマップにマウスでPolyline、Polygonを直接描写できる描写モードに切り替えます。<br>マップをクリックした時、オブジェクトの描写が始まり、マウスをダブルクリックすると描写が完了します。 <br>描写完了時、コールバック関数に描写したFeatureオブジェクトを渡します。 |
|                                          | style : Object          |                                          | <br> Polygon, Polylineのスタイルを指定するためのObject<br>strokeColor：線の色<br>- 'red', '#fff123' <br> strokeWidth：線の太さ<br> - 10<br> strokeOpacity：線の透明度<br>fillColor：塗りつぶしの色<br>fillOpacity：塗りつぶしの透明度<br>strokeDashstyle：線のスタイル<br>dot：· · · · · · <br>dash: - - - - - -<br>dashdot：- · - · - · - <br>longdashdot:ㅡ·ㅡ·ㅡ<br> solid：実線 <br> |
|                                          | func_cb : function()    |                                          | ユーザーがマップをダブルクリックして<br>Featureオブジェクトの描写が完了した時に呼び出されるコールバック関数 |
| THINKMAP.featureDrawingCancel()          |                         |                                          | マップにユーザーがマウスでPolyline、Polygonを直接描写できる描写モードを終了します。 |
| THINKMAP.tw_Wgs84(twX, twY)              | twX：Number            | coord：Object<br>変換されたWGS84座標<br>- coord.curx：WGS84 X座標<br>- coord.cury：WGS84 Y座標 | 変換するTW X座標<br><br>TW座標をWGS84座標に変換します。 |
|                                          | twY : Number            |                                          | 変換するTW Y座標                     |
| THINKMAP.wgs84_Tw(wgs_lon, wgs_lat)      | wgs_lon：Number        | coord：Object<br>変換されたTW座標 <br>- coord.curx：TW X座標<br>- coord.cury：TW Y座標 | 変換するWGS84経度座標<br><br>WGS84座標をTW座標に変換します。 |
|                                          | wgs_lat : Number        |                                          | 変換するWGS84緯度座標                 |


#### TOAST Maps APIの使用
```
// マップを使用するためのjsファイルを宣言します。
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v1.0/map.js"></script>
<script>
	// マップを使用するための認証を進行します。
	Map.authentification("appKey");
</script>

//マップを入れるDIVを作成します。
<div id="div_map"></div>
<script type="text/javascript">

	//宣言したDIVにマップを表示します。
	THINKMAP.initMap("div_map", 165406, 500198, 12, init, 2, 'i');

	// マップinit後、コールバック関数が実行されます。
	function init(){
		alert('init!');
	}
</script>
```

#### マップモードの変更
```
<script type="text/javascript">
	//マップを一般マップに切り替え
	THINKMAP.imageMap();

	//マップを航空写真に切り替え
	THINKMAP.aerialMap();

	//マップ上に航空周期を表示するかどうかを設定
	THINKMAP.setAerialHybrid(active);
</script>
```
#### マップにイベントを登録
```
<script type="text/javascript">
	//マップにmoveイベントを登録する。
	THINKMAP.addMapListener('move', mapEvent_cb);

	//マップイベント発生時のコールバック関数
	function mapEvent_cb(map){
	    console.log("event callback!");
	}
</script>
```
#### マップのイベントを削除
```
<script type="text/javascript">
	//マップからmoveイベントを削除する。
	THINKMAP.removeMapListener('move');
</script>
```

#### マップマーカーの追加
```
<script type="text/javascript">
	//マップのマーカーオブジェクトを初期化する。
	var marker = null;
	function createMarker(){
		if(!marker){
			//マーカーオブジェクトを作成する。
			marker = THINKMAP.createMarker(163670, 526934, 47, 46, '../img/img.png', 'my_marker');
			//マーカーをマップに追加する。
			THINKMAP.addMarker(marker);
			console.log('id : ' + marker._feature_id + ', param : ' + marker._param);
		}
	}
</script>
```


#### マップ描写モードに切り替え
```
<script type="text/javascript">
	//マップを描写モードに切り替える。
	var style = {
		strokeColor: '#fff123',
		strokeWidth: 5,
		strokeDashstyle: 'solid',		
		strokeOpacity: 0.8,
		fillColor: 'blue',
		fillopacity: 1
	};

	THINKMAP.featureDrawing("lineDraw", style, drawEvent_cb);

	function drawEvent_cb(){
		alert("描写モードに切り替え！");
	}
</script>
```

#### マップ描写モードの終了
```
<script type="text/javascript">
	//マップ描写モードを終了する。
	THINKMAP.featureDrawingCancel();
</script>
```


#### TW座標をWGS座標に変換
```
<script type="text/javascript">
	var wgs;

	// TW座標をWGS座標に変換する。
	wgs = THINKMAP.tw_Wgs84(165406, 500198);

	console.log(wgs.curx);
	console.log(wgs.cury);
</script>
```


#### WGS座標をTW座標に変換
```
<script type="text/javascript">
	var tw;

	// WGS座標をTW座標に変換する。
	wgs = THINKMAP.wgs84_Tw(127.28976653131843, 37.56515136725675);

	console.log(tw.curx);
	console.log(tw.cury);
</script>
```

### 2. 静的(static)マップ

#### TOAST Maps API静的(static)マップ使用
```
// 静的(static)マップを使用するためのjsファイルを宣言します。
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v1.0/staticMap.js"></script>

// マップを入れるIMGを作成します。
<img id='staticMapImg' alt="" src="">

<script>

	// 静的(static)マップを使用するための認証およびパラメータを渡します。 	
	StaticMap.authentification('staticMapImg',"appkey",'x=157423&y=266836&width=970&height=300&level=10&maptype=i&mx=158323&my=266836&txt=');

</script>
```

| 名前 | タイプ | 必須かどうか | 説明                   |
| ------- | ------- | ----- | ----------------------------- |
| x       | Integer | 必須 | マップ中心のX座標           |
| y       | Integer | 必須 | マップ中心のY座標           |
| mx      | Integer | 必須 | マーカーのX座標              |
| my      | Integer | 必須 | マーカーのY座標              |
| width   | Integer | 任意 | マップの幅<br>未入力時は基本600px     |
| height  | Integer | 任意 | マップの高さ<br>未入力時は基本600px     |
| imgurl  | String  | 任意 | マーカーイメージURL<br> 未入力時は基本マーカーを使用 |
| level   | Integer | 任意 | マップレベル <br> 未入力時は基本10        |
| maptype | String  | 任意 | マップタイプ <br> 未入力時は基本一般マップ  |
| label   | String  | 任意 | ラベルの内容                |

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
		<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v1.0/map.js"></script>
		<script>
			// マップを使用するための認証を進行します。
			Map.authentification("appKey");
		</script>
	</head>

	<body>
		//マップを入れるDIVを作成します。
		<div id="div_map"></div>
		<script type="text/javascript">

			//宣言したDIVにマップを表示します。(モバイルマップタイプの'm'を宣言します。)
			THINKMAP.initMap("div_map", 165406, 500198, 12, init, 2, 'm');

			// マップinit後、コールバック関数が実行されます。
			function init(){
				alert('init!');
			}
		</script>
	</body>

</html>
```

