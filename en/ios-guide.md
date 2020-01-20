## Application Service > Maps > iOS User Guide

Desribes the Maps Service for iOS users. 

## Common API Information 

### Prerequisites 
- Appkey is required to use APIs. 
- To check your appkey, go to **URL & Appkey** on top of the **TOAST Console**. 

### Common Request Information

#### URL Information
##### [Maps API]

| Item    | URL                                      |
| --------- | ---------------------------------------- |
| Map       | https://api-maps.cloud.toast.com/maps/js/v1.0/map.js |
| Static Map | https://api-maps.cloud.toast.com/maps/js/v1.0/staticMap.js |

## Maps

### 1. iOS WebView Map

Describes how to call APIs on iOS and get parameters via callback functions. 


#### A. Guide for Main TOAST Maps APIs on iOS WebView 
##### For more details on using TOAST Maps APIs on iOS WebView,  see <a href="http://developers1.inavi.com:8086?key=19b6272o5" target="_blank" rel="nofollow">Thinkware API Center</a>.  

> ※ The TOAST Maps API adopts Thinkware-only coordinates. 
> <br>To convert Thinkware coordinates into Latitude/Longitude coordinates (WGS84), use the TMWA.getWgs84FromTw() function.On the contrary, to convert Latitude/Longitude coordinates (WGS84) into Thinkware coordinates, use the TMWA.getTwFromWgs84() function.  

| API Name                                                     | Parameter                                                    | Callback Method  | Callback Parameter                                           | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| TMWI.initMap(map_div_name, twX, twY, level, arrange_type, map_type) | map_div : String<br>ID in the div tag to contain maps        | initCB <br><br>  | Successful in map initialization <br>'true': Successful<br> 'false': Failed | Refers to the initialization function which must be called initially to use maps. |
|                                                              | twX : Number	<br>TW X coordinates for map initialization  |                  |                                                              |                                                              |
|                                                              | twY : Number	<br>TW Y coordinates for map initialization  |                  |                                                              |                                                              |
|                                                              | level : Number	<br>Level of map initialization<br>- General Maps: 1~13<br>- Aerial Maps: 1~13 |                  |                                                              |                                                              |
|                                                              | arrange_type : Number	<br>Alignment method of map layers<br>1: Central Alignment (effective in resizing)<br>2: Entire Loading (no resizing effects)<br> 3: Top-right Alignment (effective in resizing) |                  |                                                              |                                                              |
|                                                              | map_type : String<br>Map Type Settings<br>'i': General Maps<br>'a': Aerial Maps<br>'s': Summary Maps |                  |                                                              |                                                              |
| TMWI.getLevel()                                              |                                                              | getLevelCB       | Current level of the map                                     | Load the level of the map.                                   |
| TMWI.getCenter()                                             |                                                              | getCenterCB      | Current central coordinates of the map<br> 'twX&#124;twY'    | Load the central coordinates of the map.                     |
| TMWI.getExtent()                                             |                                                              | getExtentCB      | Area coordinates of the map<br> 'leftX&#124;topY&#124;rightX&#124;bottomY' | Load the area coordinates which show the current map.        |
| TMWI.setMoveend()                                            |                                                              | moveendCB        | Central coordinates and level after zoom-out, zoom-in, and move<br>'twX&#124;twY&#124;level' | Register moveend events on the map.<br>moveend: When zoom-out, zoom-in, or move ends on the map |
| TMWI.removeMoveend()                                         |                                                              |                  |                                                              | Remove  moveend events from the map.                         |
| TMWI.setTouchend()                                           |                                                              | setTouchendCB    | Touched coordinates of the map<br> 'twX&#124;twY'            | Register touchend events on the map.<br> touchend: When touch on the map ends |
| TMWI.removeTouchend()                                        |                                                              |                  |                                                              | Remove zoomend events from the map.                          |
| TMWI.setZoomend()                                            |                                                              | zoomendCB        | Central coordinates and level of the map after zoom-out and zoom-in<br> 'twX&#124;twY&#124;level' | Register zoomend events on the map. <br>zoomend: When zoom-out/zoom-in ends |
| TMWI.removeZoomend()                                         |                                                              |                  |                                                              | Remove zoomend events from the map.                          |
| TMWI.setTouchEvent(event_name)                               | event_name : String<br>	Event name to register<br>'touchstart': When touch on the map starts <br> 'touchend': When touch on the map ends<br> 'longpress': When map is pressed long | setTouchEventCB  | Coordinates of the map touched with events <br>'event_name&#124;twX&#124;twY' | Register touch-related events on the map.                    |
| TMWI.removeTouchEvent(event_name)                            | event_name : String<br>	Event name to register<br> 'touchstart': When touch on the map starts<br> 'touchend': When touch on the map ends<br> 'longpress': When map is pressed long |                  |                                                              | Remove touch-related events from the map.                    |
| TMWI.createAndAddMarker(twX, twY, iconWidth, iconHeight, iconUrl, [param]) | twX : Number<br>TW X coordinates of the marker object        | createMarkerCB   | Marker object ID and user variable parameters<br> 'marker_id&#124;param' | Create a marker object and add it on the map.                |
|                                                              | twY : Number	<br>TW Y coordinates of the marker object    |                  |                                                              |                                                              |
|                                                              | iconWidth : Number <br>Width of the marker image             |                  |                                                              |                                                              |
|                                                              | iconHeight : Number <br>Height of the marker image           |                  |                                                              |                                                              |
|                                                              | iconURL : String <br>URL of the marker image                 |                  |                                                              |                                                              |
|                                                              | param : String <br>User variable of the marker object        |                  |                                                              |                                                              |
| TMWI.setTouchendMarkerCB(id)                                 | id : Number<br>Marker object ID to register events           | touchendMarkerCB | ID, TW X coordinates, and TW Y coordinates of the marker object,<br>User variable parameters<br> 'marker_id&#124;twX&#124;twY&#124;param' | Register touchend events for the marker object.              |
| TMWI.removeTouchendMarker(id)                                | id : Number<br>Marker object ID to remove events from        |                  |                                                              | Remove touchend events from the marker object.               |
| TMWI.getTwFromWgs84(lon, lat)                                | lon : Number<br>WGS84 longitude coordinates to convert       | getTwFromWgs84CB | Converted TW coordinates <br>'twX&#124;twY'                  | Convert WGS84 coordinates into TW coordinates.               |
|                                                              | lat : Number<br>WGS84 latitude coordinates to convert        |                  |                                                              |                                                              |
| TMWI.getWgs84FromTw(twX, twY)                                | twX: Number<br>TW X coordinates to convert                   | getWgs84FromTwCB | Converted WGS84 coordinates <br>'lon&#124;lat'               | Convert TW coordinates into WGS84 coordinates.               |
|                                                              | twY : Number<br>TW Y coordinates to convert                  |                  |                                                              | -                                                            |
