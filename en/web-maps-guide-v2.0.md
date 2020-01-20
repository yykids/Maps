## Application Service > Maps > Guide for Web Maps v2.0 

Describes APIs that are required to use web maps. 

## Updates for v2.0 
* Basic Map Feature Updated
  * Main HTML5-based map features are available. 
  * All features, like images or markers on the map, become objects so as the usability and performance are upgraded. 
* Map Rotation
  * Maps on a mobile device can be rotated with two fingers. 
  * On a pc, enter Shift+Alt+Drag or set an angle in need to rotate. 
* Feature Cluster (except figures)
  * For a map zoom-out, nearby features are combined to show; for zoom-in, details show in fragments. 
* Downloading Map Images 
  * Map functions are provided to enable image file downloading.  
* Overview 
  * More than one map can be displayed on a screen. 
* Adding Map Road Events and Animation Effects 
  * Road events can be added to a tile image. 
  * Applicable on the progress bar effects for image loading 
* Preload Tiles 
  * Cache and display image of a confirmed area.  
* Processing KML/GPX File Type
  * Load KML/GPX files and mark them on the map, while data displayed on the map into KML/GPX types. 

## Common API Information 

### Prerequisites

- Appkey is required to use APIs. 
- To check your appkey, go to **URL & Appkey** on top of the **TOAST Console**. 

### Common Request Information

#### URL Information

| Item    | URL                                      |
| --------- | ---------------------------------------- |
| Map     | https://api-maps.cloud.toast.com/maps/js/v2.0/map.js |
| Static Map | https://api-maps.cloud.toast.com/maps/js/v2.0/staticMap.js |

## Web Maps

### 1. Web Maps 

Describes how to display maps on the web browser by using Javascript-based TOAST Maps API.  
TOAST Maps API adopts Thinkware coordinates: TW, TW X, or TW Y coordinates, in short. 
Optional parameters are displayed as [param] for method: they can be omitted.

> ※ TOAST Maps API adopts Thinkware-only coordinates. 
> <br>To convert Thinkware coordinates into Latitude/Longitude (WGS84), use the THINKMAP.tw_Wgs84() function. On the contrary, to convert Latitude/Longitude (WGS84) into Thinkware coordinates, use the THINKMAP.wgs84_Tw() function.

#### Guide for Main TOAST Maps APIs 
##### For more details on using TOAST Maps APIs, see <a href="http://developers1.inavi.com:8086?key=19b6272o5" target="_blank" rel="nofollow">Thinkware API Center</a>.

| API Name                                                     | Parameter                        | Returns                                                      | Description                                                  |
| ------------------------------------------------------------ | -------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| new thinkware.maps.Map(map_div, option)                      | map_div : String                 |                                                              | DOM element or ID of the element to show maps                |
|                                                              | option.type : String             |                                                              | Map Type <br> 'i': General maps,<br> 'm': Mobile maps,<br> 's': Summary maps,<br> 'a': Aerial maps,<br> 'm_a': Mobile aerial maps,<br> 's_a': Summary aerial maps,<br> 'hybrid': Aerial <br>default: 'i' |
|                                                              | option.center.twX : number       |                                                              | X coordinates at map center: by Thinkware coordinates        |
|                                                              | option.center.twY : number       |                                                              | Y coordinates at map center: by Thinkware coordinates        |
|                                                              | option.level : number            |                                                              | Level of a map                                               |
|                                                              | option.callback : function()     |                                                              | Function to be executed after initialization                 |
|                                                              | option.logo : String             |                                                              | To be located by logos <br> top-left,<br>  top-center,<br>  top-right,<br>  center-left,<br>  center-center,<br>  center-right,<br>  bottom-left,<br>  bottom-center,<br>  bottom-right |
| changeType(type)                                             | type : String                    |                                                              | Map Type <br> 'i': General maps,<br> 'm': Mobile maps,<br> 's': Summary maps,<br> 'a': Aerial maps,<br> 'm_a': Mobile aerial maps,<br> 's_a':Summary aerial maps,<br> 'hybrid': Aerial<br>default: 'i' |
| thinkware.maps.event.addListener(target, event_type, func_cb) | target : Object                  |                                                              | Target object to add listeners                               |
|                                                              | event_type : String              |                                                              | wheelup, <br> wheeldown, <br> wheel, <br>zoomend, <br>movestart, <br>move, <br>moveend, <br>tileloadstart, <br>tileloadend, <br>tileloaderror, <br>click, <br>dblclick, <br>rightclick, <br>mousemove, <br>mouseup, <br>mousedown |
|                                                              | func_cb : function()             |                                                              | Listener for registration                                    |
| thinkware.maps.event.removeListener(target, event_type, func_cb) | target : Object                  |                                                              | Object to remove listener from                               |
|                                                              | event_type : String              |                                                              | wheelup, <br> wheeldown, <br> wheel, <br>zoomend, <br>movestart, <br>move, <br>moveend, <br>tileloadstart, <br>tileloadend, <br>tileloaderror, <br>click, <br>dblclick, <br>rightclick, <br>mousemove, <br>mouseup, <br>mousedown |
|                                                              | func_cb : function()             |                                                              | Listener for removal                                         |
| new thinkware.maps.Marker(option)                            | option.map : Object              | The thinkware.maps.Marker marker object                      | Map object                                                   |
|                                                              | option.icon.url : String         |                                                              | Icon URL                                                     |
|                                                              | option.icon.size.width : number  |                                                              | Icon width                                                   |
|                                                              | option.icon.size.heigth : number |                                                              | Icon height                                                  |
|                                                              | option.position.twX : number     |                                                              | Marker creation x coordinates (by Thinkware coordinates)     |
|                                                              | option.position.twY : number     |                                                              | Marker creation Y coordinates (by Thinkware coordinates)     |
|                                                              | option.positioning : String      |                                                              | To be located by coordinates<br> top-left,<br>  top-center,<br>  top-right,<br>  center-left,<br>  center-center,<br>  center-right,<br>  bottom-left,<br>  bottom-center,<br>bottom-right |
|                                                              | option.title : String            |                                                              | Character strings for tool-tips                              |
|                                                              | option.offset.pxX : number       |                                                              | By pixel                                                     |
|                                                              | option.offset.pxY : number       |                                                              | By pixel                                                     |
|                                                              | option.visible : boolean         |                                                              | Display or not                                               |
|                                                              | option.draggable : boolean       |                                                              | If a drag is available                                       |
|                                                              | option.zIndex : number           |                                                              | z-index value                                                |
|                                                              | option.opacity : number          |                                                              | Opacity level                                                |
|                                                              | option.stopEvent : boolean       |                                                              | Whether to prevent map event execution on a marker           |
| thinkware.maps.LineString.drawStart(target, option)          | target : Object                  |                                                              | Map object                                                   |
|                                                              | option.stroke.style : String     |                                                              | Style of a stroke<br><br> dot : · · · · · · <br>dash : - - - - - -<br>dashdot : - · - · - · - <br>longdashdot: ㅡ · ㅡ · ㅡ<br> solid: Solid stroke |
|                                                              | option.stroke.weight : number    |                                                              | Thickness of a stroke (px)                                   |
|                                                              | option.stroke.color : String     |                                                              | Color of a stroke                                            |
|                                                              | option.stroke.opacity : number   |                                                              | Opacity of a stroke                                          |
|                                                              | option.callback : function()     |                                                              | Function to be executed after drawing is done                |
|                                                              | option.measure : boolean         |                                                              | Whether to show popups to measure distance                   |
|                                                              | option.isOnce : boolean          |                                                              | Whether to close after one-time drawing                      |
| thinkware.maps.LineString.drawEnd(target)                    | target : Object                  |                                                              | Map object                                                   |
| thinkware.maps.util.getLonLatFromCoordinate(param)           | param.twX : number               | Coordinates<br>Object.lon : WGS84<br>Object.lat : WGS84      | Thinkware X coordinates                                      |
|                                                              | param.twY : number               |                                                              | Thinkware Y coordinates                                      |
| thinkware.maps.util.getCoordinateFromLonLat(param)           | param.lon : number               | TW coordinates<br>Object.twX: TW X coordinates<br>Object.twY : TW Y coordinates | Longitude                                                    |
|                                                              | param.lat : number               |                                                              | Latitude                                                     |


#### Enable TOAST Maps API
```
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v2.0/map.js"></script>
<script>
	// Authenticate to enable maps. 
	Map.authentification("appKey");
</script>

<div id="div_map"></div>
<script type="text/javascript">

	//Expose the map on declared DIV. 
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

#### Change Map Modes
```
<script type="text/javascript">

 	// Change map type of created map object.
 	// General: i, Mobile: m, Summary: s, Aerial background: a, Mobile aerial: m_a, Summary aerial: s_a, Aerial: hybrid
	// Change into aerial background map. 
	map.changeType('i');

</script>
```

#### Register Map Events 
```
<script type="text/javascript">

	//Register move events on the map.
	thinkware.maps.event.addListener(map, 'click', mapEvent_cb)

	 //Callback function when map event occurs
    function mapEvent_cb(event){
        console.log("event callback!");
    }

</script>
```

#### Remove Map Events
```
<script type="text/javascript">

	//Remove move events from the map.
	thinkware.maps.event.removeListener(map, 'move', mapEvent_cb)

</script>
```

#### Add Map Markers 
```
<script type="text/javascript">

	// Add marker objects on the map. 
	var marker = new thinkware.maps.Marker({
	    map: map,
	    position: {
	        twX: 169030,
	        twY: 517922
	    },
	    stopEvent: false
	});

	// Move marker objects on the map.
	marker.setPosition({twX: 169030, twY: 517922});

</script>
```

#### Convert to Map Drawing Mode
```
<script type="text/javascript">

	// Convert into the map drawing mode.
	var strokeOpt = {
		style : 'longdash'	// Stroke style (solid, dash, longdash, ... or refer to functions that return segments) default: "solid"
		, weight : 5		// Thinkness of a stroke (px) (default: 3)
		, color : '#3399ff'	//Color of a stroke (default: #3399ff)
		, opacity : 1		//Opacity of a stroke (default: 1)
    };

	var drawOpt = {
		stroke : strokeOpt
		, callback : mapDraw_cb // Function to be executed after drawing is done (default: undefined)
		, measure : true 		// Whether to display popup to measure distance (default: false)
		, isOnce : false		// Whether to close after one drawing (default: false)
	};

	//thinkware.maps.LineString.drawStart(map, drawOpt);

	function mapDraw_cb(map){
		console.log("draw finish!!!");
	}
</script>
```

#### Close Map Drawing Mode
```
<script type="text/javascript">

	// Close the map drawing mode.
	thinkware.maps.LineString.drawEnd(map);

</script>
```

#### Convert TW to WGS Coordinates
```
<script type="text/javascript">

 	// Convert TW coordinates into WGS coordinates. 
 	var tws = {
		twX : 169030
		, twY: 517922
 	};

 	var wgs84 = thinkware.maps.util.getLonLatFromCoordinate(tws);
 	console.log(wgs84.lon);
 	console.log(wgs84.lat);

</script>
```

#### Convert WGS Coordinates into TW Coordinates
```
<script type="text/javascript">

 	 // Convert WGS coordinates into TW coordinates.
	 var wgs84 = {
		lon: 127.11074994024005
		, lat: 37.40215870673785
	};

	 var tws = thinkware.maps.util.getCoordinateFromLonLat(wgs84);

 	console.log(tws.twX);
 	console.log(tws.twY);

</script>
```

### 2. Static Maps

#### Enable Static TOAST Maps API 
```
// Declare js file to enable static maps.
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v2.0/staticMap.js"></script>

// Create IMG to contain maps. 
<img id='staticMapImg' alt="" src="">

<script>

	//  Authenticate to enable static maps and deliver parameters. 	
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
		//  Set viewport for each mobile device.
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
		<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v2.0/map.js"></script>
		<script>
			// uthenticate to enable the maps. 
			Map.authentification("appKey");
		</script>
	</head>

	<body>

		//Create DIV to contain maps. 
		<div id="div_map"></div>
		<script type="text/javascript">

			//Mark maps on declared DIV (declare 'm' for the mobile map type.)
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
