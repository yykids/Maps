## Application Service > Maps > Guide for Web Maps 

Describes JavaScript-based web APIs required to use web maps. 


## Common API Information 

### Prerequisites 
- Appkey is required to use APIs. 
- To check your appkey, go to **URL & Appkey** on top of the **TOAST Console**. 

### Common Request Information

#### URL Information 

| Item | URL                              |
| ---- | -------------------------------- |
| Maps | https://api-maps.cloud.toast.com |


## Web Maps

### 1. Web Maps

Describes how to show maps on the web browser by using Javascript-based TOAST Maps API. 
TOAST Maps API adopts Thinkware coordinates


#### Guide for Maps API
##### For more details on Maps API, see <a href="http://imapsapi.inavi.com/" target="_blank" rel="nofollow">iNavi Maps API Center</a>. <p>


| API Name                                | Parameter                        | Returns                                  | Description                            |
| ---------------------------------------- | -------------------------------- | ---------------------------------------- | ---------------------------------------- |
| new inavi.maps.Map(options)  | options.container : string                 | inavi.maps. map object | ID of DOM element to mark maps |
|                                          | options.type : string             |                                          | Map type <br> 'NORMAL': General maps,<br> 'SATTELITE': Aerial maps<br>default: 'NORMAL' |
|                                          | options.center : LngLatLike       |                                          | Central coordinates on the map |
|                                          | options.zoom : number            |                                          | Level of a map        |
|                                          | options.heading : number             |                                          | Counter clockwise angle on north |
|                                          | options.tilt : number             |                                          | Tilt of a map |
|                                          | options.maxZoom : number             |                                          | Counter clockwise angle on north |
|                                          | options.heading : number             |                                          | Maximum zoom-in level |
|                                          | options.hash : boolean             |                                          | If map information shows on the address bar |
|                                          | options.zoomable : boolean             |                                          | If zoom-in is available |
|                                          | options.draggable : boolean             |                                          | If a drag is available |
|                                          | options.rotatable : boolean             |                                          | If rotation is available |
|                                          | options.keyboard : boolean             |                                          | If map movement on keyboard is available |
|                                          | options.disableDefaultUI : boolean             |                                          | If default control can be hidden |
|                                          | options.logoScaleControl : LogoScaleControlOptions             |                                          | Log and scale mark control option |
|                                          | options.compassControl : CompassControlOptions             |                                          | Compass mark control option |
|                                          | options.zoomControl : ZoomControlOptions             |                                          | Zoom-in/out mark control option |
| changeType(type)                         | type : string                    |                                          | Map Type <br> 'NORMAL': General maps,<br> 'SATTELITE': Aerial <br>default: 'NORMAL' |
| on(eventType, listener) | eventType : string              |                                          | load,<br>zoomstart, zoom, zoomend,<br>rotatestart, rotate, rotateend,<br>tiltstart, tilt, tiltend,<br>click, dblclick,<br>mousedown, mouseup, mousemove,<br>mouseenter, mouseleave, mouseover, mouseout,<br>contextmenu,<br>wheel,<br>touchstart, touchend, touchcancel, touchmove,<br>movestart, move, moveend,<br>dragstart, drag, dragend|
|                                          | listener : Function             |                                          | Listener for registration        |
| once(eventType, listener) | eventType : string              |                                          | load,<br>zoomstart, zoom, zoomend,<br>rotatestart, rotate, rotateend,<br>tiltstart, tilt, tiltend,<br>click, dblclick,<br>mousedown, mouseup, mousemove,<br>mouseenter, mouseleave, mouseover, mouseout,<br>contextmenu,<br>wheel,<br>touchstart, touchend, touchcancel, touchmove,<br>movestart, move, moveend,<br>dragstart, drag, dragend|
|                                          | listener : Function             |                                          | Listener for registration   |
| off(eventType, listener) | eventType : string              |                                          | load,<br>zoomstart, zoom, zoomend,<br>rotatestart, rotate, rotateend,<br>tiltstart, tilt, tiltend,<br>click, dblclick,<br>mousedown, mouseup, mousemove,<br>mouseenter, mouseleave, mouseover, mouseout,<br>contextmenu,<br>wheel,<br>touchstart, touchend, touchcancel, touchmove,<br>movestart, move, moveend,<br>dragstart, drag, dragend|
|                                          | listener : Function             |                                          | Listener for removal        |
| new inavi.maps.Marker(option)        | option.map : Map              | inavi.maps.Marker object | Map object                         |
|                                          | option.icon : string         |                                          | Icon URL                               |
|                                          | option.position : LngLatLike     |                                          | Marker creation coordinates |
|                                          | option.anchor : string      |                                          | To be located by coordinates <br> top-left, top, top-right,<br>left, center, right,<br>bottom-left, bottom, bottom-right |
|                                          | option.title : string            |                                          | Character strings for tool-tips   |
|                                          | option.offset : Array       |                                          | Offset by pixel                    |
|                                          | option.draggable : boolean       |                                          | If a drag is available   |
|                                          | option.zIndex : number           |                                          | z-index value                           |
|                                          | option.opacity : number          |                                          | Opacity level                |
| inavi.maps.LngLat.convertToPixel(lngLat) | lngLat.lng : number               | Screen pixel coordinates | WGS84 longitude                        |
|                                          | lngLat.lat : number               |                                          | WGS84 latitude                         |
| inavi.maps.Pixel.convertToLngLat(pixel) | pixel.pxX : number               | Longitude/latitude coordinates | Screen pixel x coordinates               |
|                                          | pixel.pxY : number               |                                          | Screen pixel y coordinates               |


#### Enable Maps API 
```html
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/v3.0/appkeys/{appkey}/maps?callback=initMap"></script>
<div id="div_map"></div>
<script type="text/javascript">
    function initMap() {
        //Expose the map on declared DIV. 
        var map = new inavi.maps.Map({
            container: "div_map",
            center: {
                lng: 127.11,
                lat: 37.40
            },
            zoom: 12,
            type: "NORMAL"
        });
    }
</script>
```

#### Change Map Mode 
```html
<script type="text/javascript">
    // Change map type of created map object. 
    // General:NORMAL, Aerial background:SATTELITE
    // Change into aerial background map.
    map.setType("SATTELITE");
</script>
```

#### Register Map Events
```html
<script type="text/javascript">
    //Register move events on the map. 
    map.addListener("click", clickHandler)

    //Callback function when map event occurs
    function clickHandler(event){
        console.log("event callback!");
    }
</script>
```

#### Remove Map Events 
```html
<script type="text/javascript">
    //Remove move events from the map. 
    map.off("move", moveHandler)
</script>
```

#### Add Map Markers 
```html
<script type="text/javascript">
    // Add marker objects on the map. 
    var marker = new inavi.maps.Marker({
        map: map,
        position: {
            lng: 127.11,
            lat: 37.40
        }
    });

    // Move marker objects. 
    marker.setPosition({lng: 127.2, lat: 37.5});
</script>
```

#### Convert Screen Pixel Coordinates into WGS Coordinates 
```html
<script type="text/javascript">
    // Convert screen pixel coordinates into WGS coordinates. 
    var screen_pixel = {
        pxX: 100,
        pxY: 100
    };

    var wgs84 = inavi.maps.Pixel.convertToLngLat(screen_pixel);
    console.log(wgs84.lon);
    console.log(wgs84.lat);
</script>
```

#### Convert WGS Coordinates into Screen Pixel Coordinates 
```html
<script type="text/javascript">
    // Convert WGS coordinates into screen pixel coordinates. 
    var wgs84 = {
        lon: 127.11074994024005,
        lat: 37.40215870673785
    };

    var screen_pixel = inavi.maps.LngLat.convertToPixel(wgs84);
    console.log(screen_pixel.pxX);
    console.log(screen_pixel.pxY);
</script>
```