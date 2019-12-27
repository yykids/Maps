## Application Service > Maps > Android使用ガイド

AndroidでMapsサービスを使用する方法を説明します。

## API共通情報

### 事前準備
- APIを使用するにはアプリケーションキーが必要です。
- アプリケーションキーは**TOAST Console**上部の**URL & Appkey**メニューで確認できます。

### リクエスト共通情報

#### URL情報
##### [マップAPI]

| 項目      | URL                                      |
| --------- | ---------------------------------------- |
| マップ      | https://api-maps.cloud.toast.com/maps/js/v1.0/map.js |
| 静的(static)マップ | https://api-maps.cloud.toast.com/maps/js/v1.0/staticMap.js |

## マップ

### 1. Android WebViewマップ

AndroidでAPIを呼び出し、コールバック関数でパラメータを受け取る方法を説明します。

#### A. 主要TOAST Maps Android WebView API案内
##### TOAST Maps Android WebView APIの詳細な使用方法は<a href="http://developers1.inavi.com:8086?key=19b6272o5" target="_blank" rel="nofollow">Thinkware API Center</a>を参照してください。

> ※ TOAST Maps APIで使用する座標はTHINKWARE専用座標でのみ使用されます。
> <br>THINKWARE座標を経緯度座標(WGS84)に変換するには、TMWA.getWgs84FromTw()関数を利用します。反対に経緯度座標(WGS84)をTHINKWARE座標に変換するには、TMWA.getTwFromWgs84()関数を利用します。


| APIの名前                                 | パラメータ                | コールバックメソッド         | コールバックパラメータ                                | 説明                                     |
| ---------------------------------------- | --------------------- | ---------------- | ---------------------------------------- | ---------------------------------------- |
| TMWA.initMap(map_div_name, twX, twY, level, arrange_type, map_type) | map_div : String      | initCB <br><br>  | マップ初期化成否<br>'true'：成功<br> 'false'：失敗 | マップを入れるdivタグID<br><br>マップを使用するために最初に呼び出す必要がある初期化関数です。 |
|                                          | twX : Number          |                  |                                          | マップ初期化TW X座標                         |
|                                          | twY : Number          |                  |                                          | マップ初期化TW Y座標                         |
|                                          | level : Number        |                  |                                          | マップ初期化Level<br>- 一般マップ：1～13<br>- 航空写真：1～13 |
|                                          | arrange_type : Number |                  |                                          | マップレイヤーソート方式<br>1：中央ソート方式(resize効果あり)<br>2：全体ローディング方式(resize効果なし)<br> 3：右上ソート方式(resize効果あり) |
|                                          | map_type : String     |                  |                                          | マップタイプ設定<br>'i'：一般マップ<br>'a'：航空写真<br>'s'：要約マップ |
| TMWA.getLevel()                          |                       | getLevelCB       | マップの現在のレベル                              | マップのレベルを取得します。                           |
| TMWA.getCenter()                         |                       | getCenterCB      | マップの現在の中心座標<br> 'twX&#124;twY'           | マップの中心座標を取得します。                         |
| TMWA.getExtent()                         |                       | getExtentCB      | マップの領域座標<br> 'leftX&#124;topY&#124;rightX&#124;bottomY' | 現在のマップが表示されている領域の座標を取得します。                 |
| TMWA.setMoveend()                        |                       | setMoveendCB     | 拡大、縮小、移動後のマップの中心座標とレベル<br>'twX&#124;twY&#124;level' | マップにmoveendイベントを登録します。<br>moveend：マップ拡大、縮小、移動が終わった時 |
| TMWA.removeMoveend()                     |                       |                  |                                          | マップからmoveendイベントを削除します。                 |
| TMWA.setTouchend()                       |                       | setTouchendCB    | タッチしたマップの座標<br> 'twX&#124;twY'             | マップにtouchendイベントを登録します。<br>  touchend：マップのタッチが終わった時 |
| TMWA.removeTouchend()                    |                       |                  |                                          | マップからtouchendイベントを削除します。                |
| TMWA.setZoomend()                        |                       | setZoomendCB     | 拡大、縮小後のマップの中心座標とレベル<br> 'twX&#124;twY&#124;level' | マップにzoomendイベントを登録します。<br> zoomend：マップの拡大、縮小が終わった時 |
| TMWA.removeZoomend()                     |                       |                  |                                          | マップからzoomendイベントを削除します。                 |
| TMWA.setTouchEvent(event_name)           | event_name: String   | setTouchEventCB  | 発生したイベントとタッチしたマップの座標 <br>'event_name&#124;twX&#124;twY' | 登録するイベント名<br> 'touchstart'：マップのタッチを開始した時<br>  'touchend'：マップのタッチが終了した時<br>  'longpress'：マップを長押しした時<br><br>マップにタッチ(touch)関連イベントを登録します。 |
| TMWA.removeTouchEvent(event_name)        | event_name: String   |                  |                                          | 登録するイベント名<br> 'touchstart'：マップのタッチを開始した時<br>  'touchend'：マップのタッチが終了した時<br>  'longpress' ：マップを長押しした時<br><br>マップからtouch関連イベントを削除します。 |
| TMWA.createAndAddMarker(twX, twY, iconWidth, iconHeight, iconUrl, [param]) | twX : Number          | createMarkerCB   | MarkerオブジェクトIDとユーザー変数param<br> 'marker_id&#124;param' | MarkerオブジェクトのTW X座標<br><br>Markerオブジェクトを作成し、マップに追加します。 |
|                                          | twY : Number          |                  |                                          | MarkerオブジェクトのTW Y座標                     |
|                                          | iconWidth : Number    |                  |                                          | Markerイメージの横幅                           |
|                                          | iconHeight : Number   |                  |                                          | Markerイメージの高さ                          |
|                                          | iconURL : String      |                  |                                          | MarkerイメージのURL                          |
|                                          | param : String        |                  |                                          | Markerオブジェクトのユーザー変数                      |
| TMWA.setTouchendMarkerCB(id)             | id : Number           | touchendMarkerCB | イベントを登録する対象MarkerオブジェクトID<br><br>MarkerオブジェクトIDとMarkerオブジェクトのTW X座標、TW Y座標、<br> ユーザー変数param<br> 'marker_id&#124;twX&#124;twY&#124;param' | Markerオブジェクトにtouchendイベントを登録します。          |
| TMWA.removeTouchendMarker(id)            | id : Number           |                  |                                          | イベントを削除する対象MarkerオブジェクトID<br><br>Markerオブジェクトからtouchendイベントを削除します。 |
| TMWA.getTwFromWgs84(lon, lat)            | lon : Number          | getTwFromWgs84CB | 変換されたTW座標<br>'twX&#124;twY'             | 変換するWGS84経度座標<br><br>WGS84座標をTW座標に変換します。 |
|                                          | lat : Number          |                  |                                          | 変換するWGS84緯度座標                        |
| TMWA.getWgs84FromTw(twX, twY)            | twX: Number           | getWgs84FromTwCB | 変換されたWGS84座標<br>'lon&#124;lat'          | 変換するTW X座標<br><br>TW座標をWGS84座標に変換します。 |
|                                          | twY : Number          |                  |                                          | 変換するTW Y座標                            |


#### TOAST Maps Android WebView API使用

TOAST Maps Android WebView APIを使用するには
<br>Androidプロジェクトパス(/app/src/main/manifest.xml)ファイルにandroid.permission.INTERNET権限を追加する必要があります。
<br>THINKWARE WebView APIは、Webサイトに発行されたアプリケーションキーを宣言して該当WebページをWebViewで呼び出し
<br>発行キーの権限に応じてダウンロードしたAPI(JavaScript)を呼び出し、コールバック関数を接続して使用します。
<br>※コールバック関数を使用する時の注意点：Androidバージョン4.2以上では下記のようにコールバック関数の上に
<br>@JavascriptInterfaceアノテーションを書く必要があります。

```
@JavascriptInterface
public void setMoveendCB(String result){
	String msg = "moveend Event \n twX|twY|level : " + result;
	Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
	toast.show();
}
```


下記は簡単なマップをローディングする方法です。
<br>下記の例で、どのようにWebページとWebView間でAPIを呼び出し、イベント発生時にコールバック関数でどんなパラメータを受け取るかを確認できます。
<br>下記ファイルのパス：プロジェクトパス /app/src/main/assets/www/android_webview.html

```
<!DOCTYPE HTML>
<html>
<head>
	<meta charset="UTF-8">
	<title> Android API TEST </title>
	<script src="http://code.jquery.com/jquery-1.10.1.min.js"></script>
	<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v1.0/map.js"></script>
	<script>
	    // マップを使用するための認証を行います。
	    Map.authentification("appKey");
	</script>
	</head>
<body>
	<div id="div_map" style="position:absolute;top:0px;left:0px;width:100%;height:100%;z-index:10;"></div>
</body>
</html>
```
<center>**android_webview.html**</center>


```
public class MainActivity extends AppCompatActivity {
    private WebView mWebView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        //Layoutを設定
        setContentView(R.layout.activity_main);

		//active_mainに宣言したWebviewタイプを作成
        mWebView = (WebView) findViewById(R.id.webView);

        //JavaScript使用
        mWebView.getSettings().setJavaScriptEnabled(true);

        //WebViewクライアントを設定、ページのローディング開始、ローディング終了などのイベントを取得できる
        mWebView.setWebViewClient(new WebViewClientClass());

        // APIからコールバック
        // JavaScriptからコールバック関数発生時、Androidで使用するオブジェクトとJavaScriptで使用するオブジェクトの名前を設定
        mWebView.addJavascriptInterface(new AndroidBridge(), "tmjscall");
        // APIキーで権限が付与されたJavaScript基盤THINKWARE APIをダウンロード
        mWebView.loadUrl("file:///android_asset/www/android_webview.html");

    }

    // WebViewイベント検知
    private class WebViewClientClass extends WebViewClient {

        @Override
        public void onPageFinished(WebView view, String url) { // ページのローディングが終わったら
            // マップを初期化する
            mWebView.loadUrl("javascript:TMWA.initMap('div_map', 163670, 526934, 11, 2, 'i')");
            super.onPageFinished(view, url);
        }

    }

    // Android Bridge
    private class AndroidBridge {
        // TMWA.initMapコールバック関数
        @JavascriptInterface
        public void initCB(String init){
            String msg = "";
            if(init.equals("true")){
                msg = "マップ初期化成功！";
            }else{
                msg = "マップ初期化失敗！";
            }
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

    }

}
```
<center>**MainActivity.java**</center>



[1]マップ初期化と情報取得
<br>1番の例ではマップを初期化し、マップ情報を取得する方法を説明します。
<br>マップを初期化する方法は2つあります。
<br>WebViewでローディングするページandroid_webview.htmlでTHINKMAP.initMapを呼び出す方法と
<br>AndroidプロジェクトでTMWA.initMapを使用する方法です。
<br>マップ初期化後に追加で行う必要がある作業がある場合は、TMWA.initMapを使用してコールバック関数で追加処理を行えます。
<br>この例ではTMWA.initMapを呼び出す方法を使用します。


```
public class MainActivity extends AppCompatActivity {
    private WebView mWebView;

    //ボタン
    Button getLevel, getCenter, getExtent;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

		//Layoutを設定
        setContentView(R.layout.activity_main);

		//active_mainに宣言したWebviewタイプを作成
        mWebView = (WebView) findViewById(R.id.webView);

        //JavaScript使用
        mWebView.getSettings().setJavaScriptEnabled(true);

        //WebViewクライアントを設定、ページのローディング開始、ローディング終了などのイベントを取得できる
        mWebView.setWebViewClient(new WebViewClientClass());

        // JavaScriptからコールバック関数発生時、Androidで使用するオブジェクトとJavaScriptで使用するオブジェクト名を設定
        mWebView.addJavascriptInterface(new AndroidBridge(), "tmjscall");
        // APIキーで権限が付与されたJavaScript基盤THINKWARE APIをダウンロード
        mWebView.loadUrl("file:///android_asset/www/android_webview.html");

        // ボタンイベント接続
        getLevel = (Button) findViewById(R.id.getLevel);
        getLevel.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                mWebView.loadUrl("javascript:TMWA.getLevel()");
            }
        });

        getCenter = (Button) findViewById(R.id.getCenter);
        getCenter.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                mWebView.loadUrl("javascript:TMWA.getCenter()");
            }
        });

        getExtent = (Button) findViewById(R.id.getExtent);
        getExtent.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                mWebView.loadUrl("javascript:TMWA.getExtent()");
            }
        });

    }

    // WebViewイベント検知
    private class WebViewClientClass extends WebViewClient {

        @Override
        public void onPageFinished(WebView view, String url) { // ページのローディングが終わったら
            // マップを初期化する
            mWebView.loadUrl("javascript:TMWA.initMap('div_map', 163670, 526934, 11, 2, 'i')");
            super.onPageFinished(view, url);
        }

    }

    // Android Bridge
    private class AndroidBridge {
        // TMWA.initMapコールバック関数
        @JavascriptInterface
        public void initCB(String init){
            String msg = "";
            if(init.equals("true")){
                msg = "マップ初期化成功！";
            }else{
                msg = "マップ初期化失敗！";
            }
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

        //  TMWA.getLevelコールバック関数
        @JavascriptInterface
        public void getLevelCB(String level){
            String msg = "マップレベル：" + level;

            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();

        }

        // TMWA.getCenterコールバック関数
        @JavascriptInterface
        public void getCenterCB(String cn){
            String msg = "マップ中心： " + cn;

            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

        // TMWA.getExtentコールバック関数
        @JavascriptInterface
        public void getExtentCB(String ex){
            String msg = "現在のマップの領域： " + ex;

            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();

        }

    }

}
```
<center>**MainActivity.java**</center>


[2]マップイベント
<br>2番の例ではマップにイベントを登録、削除する方法を説明します。

```
public class MainActivity extends AppCompatActivity {
    private WebView mWebView;

    //ボタン
    Button btnMove, btnTouchend, btnZoom, btnTouch;
    Boolean moveFlag = false;
    Boolean touchendFlag = false;
    Boolean zoomFlag = false;
    Boolean touchFlag = false;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        // 共通コード省略(マップ初期化例を参照)

        // ボタンイベント登録
        btnMove = (Button) findViewById(R.id.setMoveend);
        btnMove.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                if(!moveFlag){
                    mWebView.loadUrl("javascript:TMWA.setMoveend()");
                    btnMove.setText("removeMoveend");
                    moveFlag = true;
                }else{
                    mWebView.loadUrl("javascript:TMWA.removeMoveend()");
                    btnMove.setText("setMoveend");
                    moveFlag = false;
                }
            }
        });

        btnTouchend = (Button) findViewById(R.id.setTouchend);
        btnTouchend.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                if(!touchendFlag){
                    mWebView.loadUrl("javascript:TMWA.setTouchend()");
                    btnTouchend.setText("removeTouchend");
                    touchendFlag = true;
                }else{
                    mWebView.loadUrl("javascript:TMWA.removeTouchend()");
                    btnTouchend.setText("setTouchend");
                    touchendFlag = false;
                }
            }
        });

        btnZoom = (Button) findViewById(R.id.setZoomend);
        btnZoom.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                if(!zoomFlag){
                    mWebView.loadUrl("javascript:TMWA.setZoomend()");
                    btnZoom.setText("removeZoomend");
                    zoomFlag = true;
                }else{
                    mWebView.loadUrl("javascript:TMWA.removeZoomend()");
                    btnZoom.setText("setZoomend");
                    zoomFlag = false;
                }

            }
        });

        btnTouch = (Button) findViewById(R.id.setTouchEvent);
        btnTouch.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                if(!touchFlag){
                    //longpressイベント発生時間を2秒に設定。設定しない場合は1.5秒
                    mWebView.loadUrl("javascript:THINKMAP.setLongPressTime(2)");
                    mWebView.loadUrl("javascript:TMWA.setTouchEvent('longpress')");
                    btnTouch.setText("removeTouchEvent");
                    touchFlag = true;
                }else{
                    mWebView.loadUrl("javascript:TMWA.removeTouchEvent('longpress')");
                    btnTouch.setText("setTouchEvent");
                    touchFlag = false;
                }
            }
        });

    }

    // WebViewイベント検知
    private class WebViewClientClass extends WebViewClient {

        @Override
        public void onPageFinished(WebView view, String url) { // ページのローディングが終わったら
            // マップを初期化する
            mWebView.loadUrl("javascript:TMWA.initMap('div_map', 163670, 526934, 11, 2, 'i')");
            super.onPageFinished(view, url);
        }

    }

    // Android Bridge
    private class AndroidBridge {

        // setMoveendコールバック関数
        @JavascriptInterface
        public void setMoveendCB(String result){
            String msg = "moveend Event \n twX|twY|level : " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

        // setTouchendコールバック関数
        @JavascriptInterface
        public void setTouchendCB(String result){
            String msg = "touchend Event \n twX|twY : " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

        // setZoomendコールバック関数
        @JavascriptInterface
        public void setZoomendCB(String result){
            String msg = "zoomend Event \n twX|twY|level : " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

        //setTouchEventコールバック関数
        @JavascriptInterface
        public void setTouchEventCB(String result){
            String msg = "event_name|twX|twY :\n" + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

    }

}
```
<center>**MainActivity.java**</center>



[3]マップマーカー
<br> 3番の例では、マップにマーカーを追加した後、マーカーにイベントを登録、削除する方法を説明します。

```
public class MainActivity extends AppCompatActivity {
    private WebView mWebView;

    Button btnMarker;
    String marker_id = "";

    Button btnTouchend;

    Button btnRemoveTouchEnd;

    String imgUrl = "'http://dev.m.map.inavi.com/guide/img/img.png'";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        // 共通コード省略(マップ初期化例参照)

        // ボタンイベント接続
        btnMarker = (Button) findViewById(R.id.createMarker);
        btnMarker.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if(marker_id.equals("")){
                    String imgUrl = "'http://dev.m.map.inavi.com/guide/img/img.png'";
                    mWebView.loadUrl("javascript:TMWA.createAndAddMarker(163670, 526934, 47, 46, " + imgUrl + ", 'Marker')");
                }

            }
        });


        btnTouchend = (Button) findViewById(R.id.setTouchEnd);
        btnTouchend.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                if(!marker_id.equals("")){
                    mWebView.loadUrl("javascript:TMWA.setTouchendMarkerCB(" + marker_id + ")");
                    Log.d("setEvent", "Marker");
                }
            }
        });

        btnRemoveTouchEnd = (Button) findViewById(R.id.removeTouchEnd);
        btnRemoveTouchEnd.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                if(!marker_id.equals("")){
                    mWebView.loadUrl("javascript:TMWA.removeTouchendMarker(" + marker_id + ")");
                    Log.d("removeEvent", "Marker");
                }
            }
        });

    }

    // WebViewイベント検知
    private class WebViewClientClass extends WebViewClient {

        @Override
        public void onPageFinished(WebView view, String url) { // ページのローディングが終わったら
            // マップを初期化する
            mWebView.loadUrl("javascript:TMWA.initMap('div_map', 163670, 526934, 11, 2, 'i')");
            super.onPageFinished(view, url);
        }

    }

    // Android Bridge
    private class AndroidBridge {

        @JavascriptInterface
        public void createMarkerCB(String result){
            StringTokenizer st = new StringTokenizer(result, "|");

            if(st.hasMoreTokens())
                marker_id = st.nextToken();

            String msg = "Create Marker \n marker_id|param : " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();

            Log.d("marker_id", marker_id);
        }

        @JavascriptInterface
        public void touchendMarkerCB(String result){
            String msg = "Touch End \n marker_id|twX|twY|param : " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

    }

}
```
<center>**MainActivity.java**</center>

[4]その他
<br>4番の例では住所検索、経路探索、座標変換と計算方法を説明します。

```
public class MainActivity extends AppCompatActivity {
    private WebView mWebView;

    Button btnTwFromWgs84, btnWgs84FromTw;

    String lon = "37.573264";
    String lat = "126.979594";
    String twX = "163670";
    String twY = "526934";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        // 共通コード省略(マップ初期化例参照)

        // ボタンイベント接続
        btnTwFromWgs84 = (Button) findViewById(R.id.twFromWgs84);
        btnTwFromWgs84.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                mWebView.loadUrl("javascript:TMWA.getTwFromWgs84(" + lon + "," +  lat + ")");
            }
        });

        btnWgs84FromTw = (Button) findViewById(R.id.wgs84FromTw);
        btnWgs84FromTw.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                mWebView.loadUrl("javascript:TMWA.getWgs84FromTw(" + twX + "," +  twY + ")");
            }
        });

    }

    // WebViewイベント検知
    private class WebViewClientClass extends WebViewClient {

        @Override
        public void onPageFinished(WebView view, String url) { // ページのローディングが終わったら
            // マップを初期化する
            mWebView.loadUrl("javascript:TMWA.initMap('div_map', 163670, 526934, 11, 2, 'i')");
            super.onPageFinished(view, url);
        }

    }
    // Android Bridge
    private class AndroidBridge {
        // WGS84 -> TWコールバック
        @JavascriptInterface
        public void getTwFromWgs84CB(String result){
            String msg ="twX, twY -> " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }
        // WGS84 -> TWコールバック
        @JavascriptInterface
        public void getWgs84FromTwCB(String result){
            String msg ="lon, lat -> " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }
    }

}
```
<center>**MainActivity.java**</center>

