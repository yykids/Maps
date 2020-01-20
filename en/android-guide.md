## Application Service > Maps > Android User Guide 

Describes the Maps service for Android users.  

## Common API Information

### Prerequisites 
- Appkey is required to use APIs. 
- To check your appkey, go to **URL & Appkey** on top of the **TOAST Console**. 

### Common Request Information

#### URL Information
##### [Maps API]

| Item    | URL                                      |
| --------- | ---------------------------------------- |
| Map     | https://api-maps.cloud.toast.com/maps/js/v1.0/map.js |
| Static Map | https://api-maps.cloud.toast.com/maps/js/v1.0/staticMap.js |

## Maps 

### 1. Android WebView Map

Describes how to call APIs on Android and get parameters via callback functions.  

#### A. Guide for Main TOAST Maps APIs on Android WebView  
##### For more details on using TOAST Maps APIs on Android Webview, see <a href="http://developers1.inavi.com:8086?key=19b6272o5" target="_blank" rel="nofollow">Thinkware API Center</a>.

> ※ The TOAST Maps API adopts Thinkware-only coordinates.  
> <br>To convert Thinkware coordinates into Latitude/Longitude (WGS84), use the TMWA.getWgs84FromTw() function. On the contrary, to convert Latitude/Longitude (WGS84) into Thinkware coordinates, use the  TMWA.getTwFromWgs84() function. 


| API Name                               | Parameter          | Callback Method | Callback Parameter                 | Description                           |
| ---------------------------------------- | --------------------- | ---------------- | ---------------------------------------- | ---------------------------------------- |
| TMWA.initMap(map_div_name, twX, twY, level, arrange_type, map_type) | map_div : String      | initCB <br><br>  | Successful in map initialization or not<br>'true': Successful<br>'false': Failed | ID in div tags to contain a map  <br><br>Refers to the initialization function which must be called initially to use maps. |
|                                          | twX : Number          |                  |                                          | TW X coordinates for map initialization |
|                                          | twY : Number          |                  |                                          | TW Y coordinates for map initialization |
|                                          | level : Number        |                  |                                          | Level of map initialization<br>- General Maps: 1~13<br>- Aerial Maps: 1~13 |
|                                          | arrange_type : Number |                  |                                          | Alignment method of map layers <br>1: Central Alignment (effective in resizing)<br>2: Entire Loading (no resizing effects)<br> 3: Top-right Alignment (effective in resizing) |
|                                          | map_type : String     |                  |                                          | Map Type Settings<br>'i : General Maps <br>'a': Aerial Maps<br>'s': Summary Maps |
| TMWA.getLevel()                          |                       | getLevelCB       | Current level of the map      | Load the level of the map. |
| TMWA.getCenter()                         |                       | getCenterCB      | Current central coordinates of the map <br> 'twX&#124;twY' | Load the central coordinates of the map. |
| TMWA.getExtent()                         |                       | getExtentCB      | Area coordinates of the map <br> 'leftX&#124;topY&#124;rightX&#124;bottomY' | Load the area coordinates which show the current map. |
| TMWA.setMoveend()                        |                       | setMoveendCB     | Central coordinates and level after zoom-out, zoom-in, and move  <br>'twX&#124;twY&#124;level' | Register moveend events on the map.<br>moveend: When zoom-out, zoom-in, or move ends on the map |
| TMWA.removeMoveend()                     |                       |                  |                                          | Remove  moveend events from the map. |
| TMWA.setTouchend()                       |                       | setTouchendCB    | Touched coordinates of the map <br> 'twX&#124;twY' | Register touchend events on the map.<br> touchend: When touch on the map ends |
| TMWA.removeTouchend()                    |                       |                  |                                          | Remove touchend events from the map. |
| TMWA.setZoomend()                        |                       | setZoomendCB     | Central coordinates and level of the map after zoom-out and zoom-in <br> 'twX&#124;twY&#124;level' | Register zoomend events on the map. <br>zoomend: When zoom-out/zoom-in ends |
| TMWA.removeZoomend()                     |                       |                  |                                          | Remove zoomend events from the map. |
| TMWA.setTouchEvent(event_name)           | event_name: String   | setTouchEventCB  | Coordinates of the map touched with events  <br>'event_name&#124;twX&#124;twY' | Event name to register<br>'touchstart': When touch on the map starts <br> 'touchend': When touch on the map ends<br> 'longpress': When map is pressed long<br><br>Register touch-related events on the map. |
| TMWA.removeTouchEvent(event_name)        | event_name: String   |                  |                                          | Event name to register<br> 'touchstart': When touch on the map starts<br> 'touchend': When touch on the map ends<br> 'longpress': When map is pressed long<br><br>Remove touch-related events from the map. |
| TMWA.createAndAddMarker(twX, twY, iconWidth, iconHeight, iconUrl, [param]) | twX : Number          | createMarkerCB   | Marker object ID and user variable parameters <br> 'marker_id&#124;param' | TW X coordinates of the marker object<br><br>Create a marker object and add it on the map. |
|                                          | twY : Number          |                  |                                          | TW Y coordinates of the marker object |
|                                          | iconWidth : Number    |                  |                                          | Width of the marker image |
|                                          | iconHeight : Number   |                  |                                          | Height of the marker image |
|                                          | iconURL : String      |                  |                                          | URL of the marker image  |
|                                          | param : String        |                  |                                          | User variable of the marker object |
| TMWA.setTouchendMarkerCB(id)             | id : Number           | touchendMarkerCB | Marker object ID to register events for <br><br>ID, TW X coordinates, and TW Y coordinates of the marker object <br>User variable parameters <br> 'marker_id&#124;twX&#124;twY&#124;param' | Register touchend events for the marker object. |
| TMWA.removeTouchendMarker(id)            | id : Number           |                  |                                          | Marker object ID to remove events from<br><br>Remove touchend events from the marker object. |
| TMWA.getTwFromWgs84(lon, lat)            | lon : Number          | getTwFromWgs84CB | Converted TW coordinates <br>'twX&#124;twY' | WGS84 longitude coordinates to convert<br><br>Convert WGS84 coordinates into TW coordinates. |
|                                          | lat : Number          |                  |                                          | WGS84 latitude coordinates to convert |
| TMWA.getWgs84FromTw(twX, twY)            | twX: Number           | getWgs84FromTwCB | Converted WGS84 coordinates <br>'lon&#124;lat' | TW X coordinates to convert<br><br>Convert TW coordinates into WGS84 coordinates. |
|                                          | twY : Number          |                  |                                          | TW Y coordinates to convert   |


#### Using TOAST Maps APIs on Android Webview    

To enable TOAST Maps APIs on Android WebView, 
<br>add authority for android.permission.INTERNET to the Android project path file (/app/src/main/manifest.xml). 
<br>For Thinkware WebView API, call the webpage from the Webview by declaring appkey issued on the website. 
<br>Depending on the authority of issued key, call downloaded API (JavaScript) and connect it to the corresponding callback function. 
<br>※ Caution for Using Callback Functions: For Android 4.2 or higher versions, 
<br>make sure to include the @javascriptInterface annotation on the callback function, as below.  

```
@JavascriptInterface
public void setMoveendCB(String result){
	String msg = "moveend Event \n twX|twY|level : " + result;
	Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
	toast.show();
}
```


Below shows how to load simple maps. 
<br>In the example as below, you can find how to call API between webpage and WebView, and which parameters to get via callback function when an event occurs. 
<br>Path of the below file: Project Path /app/src/main/assets/www/android_webview.html

```
<!DOCTYPE HTML>
<html>
<head>
	<meta charset="UTF-8">
	<title> Android API TEST </title>
	<script src="http://code.jquery.com/jquery-1.10.1.min.js"></script>
	<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v1.0/map.js"></script>
	<script>
	    // Authenticate to enable the map service.
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

        //Set Layout
        setContentView(R.layout.activity_main);

		//Create the webview type as declared at active_main
        mWebView = (WebView) findViewById(R.id.webView);

        //Enable JavaScript 
        mWebView.getSettings().setJavaScriptEnabled(true);

        //Load events, including setting the webView client, and starting/closing pages  
        mWebView.setWebViewClient(new WebViewClientClass());

        // Call back from APIs 
        // Set object names for Android or Javascript, when callback function occurs from the JavaScript 
        mWebView.addJavascriptInterface(new AndroidBridge(), "tmjscall");
        // Download Javascript-based Thinkware API authorized by the API key  
        mWebView.loadUrl("file:///android_asset/www/android_webview.html");

    }

    // Detect WebView events  
    private class WebViewClientClass extends WebViewClient {

        @Override
        public void onPageFinished(WebView view, String url) { // When loading page is done
            // initialize the map
            mWebView.loadUrl("javascript:TMWA.initMap('div_map', 163670, 526934, 11, 2, 'i')");
            super.onPageFinished(view, url);
        }

    }

    // Android Bridge
    private class AndroidBridge {
        // TMWA.initMap Callback Function 
        @JavascriptInterface
        public void initCB(String init){
            String msg = "";
            if(init.equals("true")){
                msg = "Successful in map initialization!";
            }else{
                msg = "Failed in map initialization!";
            }
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

    }

}
```
<center>**MainActivity.java**</center>



[1] Initialize maps and load information 
<br>Example no.1 shows how to initialize maps and load map information. 
<br>Maps can be initialized in two ways: 
<br>One is calling THINKMAP.initMap from android_webview.html, which is to be loaded from WebView; 
<br>and the other is using TMWA.initMap on an Android project.  
<br>If there is additional task required after map initialization, use TMWA.initMap to process further via callback function. 
<br>In this example, TMWA.initMap is applied for a call. 


```
public class MainActivity extends AppCompatActivity {
    private WebView mWebView;

    //Button
    Button getLevel, getCenter, getExtent;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

		//Set Layout
        setContentView(R.layout.activity_main);

		//Create Webview type as declared at active_main
        mWebView = (WebView) findViewById(R.id.webView);

        //Enable JavaScript
        mWebView.getSettings().setJavaScriptEnabled(true);

        //Set clients and load events, such as start page loading or close loading. 
        mWebView.setWebViewClient(new WebViewClientClass());

        // When callback function occurs from JavaScript, set object names for Android and Javascript. 
        mWebView.addJavascriptInterface(new AndroidBridge(), "tmjscall");
        // Download Javascript-based Thinkware API authorized by API keys  
        mWebView.loadUrl("file:///android_asset/www/android_webview.html");

        // Connect with Button Events 
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

    // Detect WebView Events 
    private class WebViewClientClass extends WebViewClient {

        @Override
        public void onPageFinished(WebView view, String url) { // After page loading ends
            // initialize the map 
            mWebView.loadUrl("javascript:TMWA.initMap('div_map', 163670, 526934, 11, 2, 'i')");
            super.onPageFinished(view, url);
        }

    }

    // Android Bridge
    private class AndroidBridge {
        // TMWA.initMap callback function 
        @JavascriptInterface
        public void initCB(String init){
            String msg = "";
            if(init.equals("true")){
                msg = "Successful in map initialization!";
            }else{
                msg = "Failed in map initialization!";
            }
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

        //  TMWA.getLevel callback function 
        @JavascriptInterface
        public void getLevelCB(String level){
            String msg = "Map level:" + level;

            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();

        }

        // TMWA.getCenter callback function 
        @JavascriptInterface
        public void getCenterCB(String cn){
            String msg = "Map center: " + cn;

            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

        // TMWA.getExtent callback function 
        @JavascriptInterface
        public void getExtentCB(String ex){
            String msg = "Current map area: " + ex;

            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();

        }

    }

}
```
<center>**MainActivity.java**</center>


[2] Maps Event 
<br>Example no.2 describes how to register and remove events from the map. 

```
public class MainActivity extends AppCompatActivity {
    private WebView mWebView;

    //Button
    Button btnMove, btnTouchend, btnZoom, btnTouch;
    Boolean moveFlag = false;
    Boolean touchendFlag = false;
    Boolean zoomFlag = false;
    Boolean touchFlag = false;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        // Common codes missing (see example of map initialization for reference)

        // Register button events  
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
                    //Set 2 seconds for longpress event; or 1.5 seconds, if not set.  
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

    // Detect WebView Events 
    private class WebViewClientClass extends WebViewClient {

        @Override
        public void onPageFinished(WebView view, String url) { // When page loading ends
            // initialize the map 
            mWebView.loadUrl("javascript:TMWA.initMap('div_map', 163670, 526934, 11, 2, 'i')");
            super.onPageFinished(view, url);
        }

    }

    // Android Bridge
    private class AndroidBridge {

        // setMoveend callback function 
        @JavascriptInterface
        public void setMoveendCB(String result){
            String msg = "moveend Event \n twX|twY|level : " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

        // setTouchend callback function
        @JavascriptInterface
        public void setTouchendCB(String result){
            String msg = "touchend Event \n twX|twY : " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

        // setZoomend callback function 
        @JavascriptInterface
        public void setZoomendCB(String result){
            String msg = "zoomend Event \n twX|twY|level : " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

        //setTouchEvent callback function 
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



[3] Map Marker 
<br> Example no.3 describes how to register and remove events from the marker, after a marker is added to the map. 

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
        // Common codes missing (see example of map initialization for reference)

        // Connect with button events
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

    // Detect WebView Events
    private class WebViewClientClass extends WebViewClient {

        @Override
        public void onPageFinished(WebView view, String url) { // After page loading ends
            // initialize the map
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

[4] Others
<br>Example no.4 describes how to search addresses, navigate routes, and convert or calculate coordinates. 

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
        // Common codes missing (see example of map initialization for reference)

        // Connect with button events 
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

    // Detect WebView Events
    private class WebViewClientClass extends WebViewClient {

        @Override
        public void onPageFinished(WebView view, String url) { // After page loading ends
            // initialize the map 
            mWebView.loadUrl("javascript:TMWA.initMap('div_map', 163670, 526934, 11, 2, 'i')");
            super.onPageFinished(view, url);
        }

    }
    // Android Bridge
    private class AndroidBridge {
        // WGS84 -> TW callback
        @JavascriptInterface
        public void getTwFromWgs84CB(String result){
            String msg ="twX, twY -> " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }
        // WGS84 -> TW callback
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
