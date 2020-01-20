## Application Service > Maps > Guide for Web Maps v1.0 

Describes APIs that are required to use web maps. 

## Common API Information 

### Prerequisites 
- Appkey is required to use APIs. 
- To check your appkey, go to **URL & Appkey** on top of the **TOAST Console**. 

### Common Request Information

#### URL Information

| Item    | URL                                      |
| --------- | ---------------------------------------- |
| Map     | https://api-maps.cloud.toast.com/maps/js/v1.0/map.js |
| Static Map | https://api-maps.cloud.toast.com/maps/js/v1.0/staticMap.js |

## Web Maps 

### 1. Web Maps

Describes how to display maps on the web browser by using Javascript-based TOAST Maps API.  
TOAST Maps API adopts Thinkware coordinates: TW, TW X, or TW Y coordinates, in short. 
Optional parameters are displayed as [param] for method: they can be omitted.

> ※ TOAST Maps API adopts Thinkware-only coordinates. 
> <br>To convert Thinkware coordinates into Latitude/Longitude (WGS84), use the THINKMAP.tw_Wgs84() function. On the contrary, to convert Latitude/Longitude (WGS84) into Thinkware coordinates, use the THINKMAP.wgs84_Tw() function.

#### Guide for Main TOAST Maps APIs
##### For more details on using TOAST Maps APIs, see <a href="http://developers1.inavi.com:8086?key=19b6272o5" target="_blank" rel="nofollow">Thinkware API Center</a>.

| API Name                                | Parameter               | Returns                                  | Description                             |
| ---------------------------------------- | ----------------------- | ---------------------------------------- | ---------------------------------------- |
| THINKMAP.initMap(map_div_name, twX, twY, level, init_cb, arrange_type, map_type) | map_div : String        |                                          | ID in div tags to contain a map<br>Refers to the initialization function which must be called initially to use maps. |
|                                          | twX : Number            |                                          | TW X coordinates for map initialization |
|                                          | twY : Number            |                                          |                            |
|                                          | level : Number          |                                          | Level of map initialization<br>- General Maps: 1~13<br>- Aerial Maps: 1~13 |
|                                          | init_cb : function()    |                                          | Callback function called after map initialization |
|                                          | arrange_type : Number   |                                          | Alignment method of map layers <br>1: Central Alignment (effective in resizing)<br>2: Entire Loading (no resizing effects)<br> 3: Top-right Alignment (effective in resizing) |
|                                          | map_type : String       |                                          | Map Type Settings<br>'i': General Maps<br>'a': Aerial Maps<br>'s': Summary Maps<br>'m': Mobile Maps |
| THINKMAP.imageMap()                      |                         |                                          | Convert maps into general maps. |
| THINKMAP.aerialMap()                     |                         |                                          | Convert maps into aerial maps. |
| THINKMAP.setAerialHybrid(active)         | active: Boolean        |                                          | Whether to expose aerial cycle  <br>true:  Show aerial cycle on the map <br>false: Do not show aerial cycle on the map<br><br>Set whether to show aerial map cycle on the map. |
| THINKMAP.addMapListener(event_name, func_cb) | event_name : String<br> |                                          | Event name for registration on the map <br>'movestart'<br>- When the map starts to move<br>'move'<br> - When the map moves<br>'moveend'<br>- When the map ends movement<br>'zoomend'<br>- When zoom-in/out ends on the map <br>'mouseover'<br>- When the mouse is placed on the map <br>'mouseout'<br>- When the mouse is placed out of the map<br> 'mousemove'<br>- When the mouse moves on the map <br><br>Register events on the map.<br>(map-related events, zoom-in/out, movement, and etc.) |
|                                          | func_cb : function()    |                                          | Callback function which is called when an event occurs on the map<br>(the map object is delivered to callback function via parameters.) |
| THINKMAP.removeMapListener(event_name)   | event_name : String     |                                          | Event name to be removed out of the map <br>'movestart'<br>- When the map starts to move<br>'move'<br> - When the map moves<br>'moveend'<br>- When the map ends movement<br>'zoomend'<br>- When zoom-in/out ends on the map<br>'mouseover'<br>- When the mouse is placed on the map<br>'mouseout'<br>- When the mouse is placed out of the map<br> 'mousemove'<br>- When the mouse moves on the map<br><br>Remove registered events from the map. <br>Caution is required since all callback functions for event_name under the THINKMAP.addMapListener method are to be removed. |
| THINKMAP.createMarker(twX, twY, width, height, iconUrl, [param]) | twX : Number            |                                          | <br>TW X coordinates for marker object location <br><br>Create a marker object.  <br>To mark the created marker object on the map, use the THINKMAP.addMarker method to add the marker object. |
|                                          | twY : Number            |                                          | TW Y coordinates for marker object location |
|                                          | width : Number          |                                          | Width of marker image     |
|                                          | height : Number         |                                          | Height of marker image |
|                                          | iconURL : String        |                                          | URL of marker image       |
|                                          | param : String          |                                          | User variable for marker object |
| THINKMAP.addMarker(marker)               | marker : Marker         |                                          | Marker object to be added on the map <br><br>Add the marker object on the map. |
| THINKMAP.featureDrawing(draw_type, style, func_cb) | draw_type : String      |                                          | Feature object type to be drawn by user <br>'lineDraw': Line<br>'polygonDraw': Polygon<br> 'regularPolygonDraw': Fixed-shape polygon <br><br>Convert into the drawing mode in which user can draw polyline or polygon on the map with a mouse. <br>Object drawing begins at the click of the mouse on the map, and is completed with a double-click. <br>When drawing is done, the drawn feature object is delivered via callback function. |
|                                          | style : Object          |                                          | <br>Object to specify the style for polygon or polyline<br>strokeColor: Color of a stroke <br>- 'red', '#fff123' <br> strokeWidth: Width of a stroke <br> - 10<br> strokeOpacity: Opacity of a storke<br>fillColor : Color of a fill<br>fillOpacity: Opacity of a fill <br>strokeDashstyle: Style of a stroke or dash<br>dot: · · · · · · <br>dash: - - - - - -<br>dashdot : - · - · - · - <br>longdashdot: ㅡ · ㅡ · ㅡ<br> solid: Solid stroke  <br> |
|                                          | func_cb : function()    |                                          | Callback function which is called when a user double clicks the map<br>and drawing feature object is completed |
| THINKMAP.featureDrawingCancel()          |                         |                                          | Close the drawing mode in which the user can draw a polyline or polygon with a mouse. |
| THINKMAP.tw_Wgs84(twX, twY)              | twX : Number            | coord : Object<br>Converted WGS84 coordinates<br>- coord.curx : WGS84 X coordinates<br>- coord.cury  : WGS84 Y coordinates | TW X coordinates to convert <br><br>Convert TW coordinates into WGS84 coordinates. |
|                                          | twY : Number            |                                          | TW Y coordinates to convert   |
| THINKMAP.wgs84_Tw(wgs_lon, wgs_lat)      | wgs_lon : Number        | coord: Object<br>Converted TW coordinates <br>- coord.curx: TW X coordinates<br>- coord.cury: TW Y coordinates | WGS84 longitude coordinates to convert<br><br>Convert WGS84 into TW coordinates. |
|                                          | wgs_lat : Number        |                                          | WGS84 latitude coordinates to convert |


#### Enable TOAST Maps API
```
// Declare js file to use maps.
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v1.0/map.js"></script>
<script>
	// Authenticate to enable maps. 
	Map.authentication("appKey");
</script>

//Create DIV to contain maps. 
<div id="div_map"></div>
<script type="text/javascript">

	// Expose maps on declared DIV. 
	THINKMAP.initMap("div_map", 165406, 500198, 12, init, 2, 'i');

	// After map initialization, callback function is executed.    
	function init(){
		alert('init!');
	}
</script>
```

#### Change Map Modes 
```
<script type="text/javascript">
	//Convert map into general map 
	THINKMAP.imageMap();

	//Covert map into aerial map 
	THINKMAP.aerialMap();

	//Set whether to display aerial cycle on the map
	THINKMAP.setAerialHybrid(active);
</script>
```
#### Register Map Events 
```
<script type="text/javascript">
	//Register move events on the map.
	THINKMAP.addMapListener('move', mapEvent_cb);

	//Callback function when map event occurs  
	function mapEvent_cb(map){
	    console.log("event callback!");
	}
</script>
```
#### Remove Map Events
```
<script type="text/javascript">
	//Remove move events from the map. 
	THINKMAP.removeMapListener('move');
</script>
```

#### Add Map Marker
```
<script type="text/javascript">
	//Initialize marker objects on the map. 
	var marker = null;
	function createMarker(){
		if(!marker){
			//Create marker object. 
			marker = THINKMAP.createMarker(163670, 526934, 47, 46, '../img/img.png', 'my_marker');
			//Add marker on the map. 
			THINKMAP.addMarker(marker);
			console.log('id : ' + marker._feature_id + ', param : ' + marker._param);
		}
	}
</script>
```


#### Convert to Map Drawing Mode 
```
<script type="text/javascript">
	//Convert into the map drawing mode. 
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
		alert("Convert to drowing mode!");
	}
</script>
```

#### Close Map Drawing Mode 
```
<script type="text/javascript">
	//Close the map drawing mode. 
	THINKMAP.featureDrawingCancel();
</script>
```


#### Convert TW to WGS Coordinates 
```
<script type="text/javascript">
	var wgs;

	// Convert TW coordinates into WGS coordinates.  
	wgs = THINKMAP.tw_Wgs84(165406, 500198);

	console.log(wgs.curx);
	console.log(wgs.cury);
</script>
```


#### Convert WGS to TW Coordinates 
```
<script type="text/javascript">
	var tw;

	// Convert WGS coordinates into TW coordinates. 
	wgs = THINKMAP.wgs84_Tw(127.28976653131843, 37.56515136725675);

	console.log(tw.curx);
	console.log(tw.cury);
</script>
```

### 2. Static Maps

#### Enable Static TOAST Maps API 
```
// Declare js file to enable static maps. 
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v1.0/staticMap.js"></script>

// Create IMG to contain maps. 
<img id='staticMapImg' alt="" src="">

<script>

	// Authenticate to enable static maps and deliver parameters. 
	StaticMap.authentification('staticMapImg',"appkey",'x=157423&y=266836&width=970&height=300&level=10&maptype=i&mx=158323&my=266836&txt=');

</script>
```

| Name    | Type    | Required | Description                                      |
| ------- | ------- | -------- | ------------------------------------------------ |
| x       | Integer | Required | X coordinates at map center                      |
| y       | Integer | Required | Y coordinates at map center                      |
| mx      | Integer | Required | Marker x coordinates                             |
| my      | Integer | Required | Marker y coordinates                             |
| width   | Integer | Optional | Map width <br>600px by default                   |
| height  | Integer | Optional | Map height <br>600px by default                  |
| imgurl  | String  | Optional | URL for marker image <br>Basic marker by default |
| level   | Integer | Optional | Map level <br>10 by default                      |
| maptype | String  | Optional | Map type <br>Basic general map by default        |
| label   | String  | Optional | Content of label                                 |

### 3. Mobile Web Maps

Enable TOAST Maps API, which serves as the same API for Javascript-based web maps, to develop hybrid apps with Android/iOS WebView. 
Regarding the API, see [1. Web Maps](#1-web) . 

#### Available for TOAST Maps API Mobile
```
<!DOCTYPE html>
<html>
    <head>
		// Set viewport for each mobile device. 
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

		// Declare js file to enable maps. 
		<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v1.0/map.js"></script>
		<script>
			// Authenticate to enable the maps. 
			Map.authentification("appKey");
		</script>
	</head>

	<body>
		//Create DIV to contain maps. 
		<div id="div_map"></div>
		<script type="text/javascript">

			//Mark maps on declared DIV (declare 'm' for the mobile map type.)
			THINKMAP.initMap("div_map", 165406, 500198, 12, init, 2, 'm');

			// Callback function is executed after map initialization. 
			function init(){
				alert('init!');
			}
		</script>
	</body>

</html>
```
