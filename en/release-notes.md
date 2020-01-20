## Application Service > Maps > Release Notes

### Jan. 21, 2020
#### 기능  추가
* [API] 주변 카테고리 검색 API 추가
	* 기준 좌표X,Y 공간 및 반경 카테고리 검색 추가
#### 기능  개선
* [API] ReverseGeocoding 건물명, 우편번호 추가
* [API] 통합검색 catecode 삭제
* [SDK] 마커 표출 상태 변경 시 애니메이션 기본값 비활성화로 변경
* [SDK] 마커 표출 상태 변경 시 애니메이션 설정 API 추가
* [SDK] INVMarker#infoWindow 속성 nullable로 변경 (iOS)
#### Bug fixes
* [API] 통합검색 spopt 2일때 vaildation check 개선
* [API] POI 하위시설물조회 vaildation check 개선
* [SDK] 마커 타이틀에 “^” 문자 포함 시 줄바꿈되는 오류 수정
* [SDK] Fly 애니메이션 타입 카메라 이동 시 자연스럽지 않은 오류 수정 (iOS)
* [SDK] 줌 컨트롤러에 지도의 Padding 값이 적용되지 않는 오류 수정 (iOS)

### Dec. 24, 2019 
#### Feature Updates
* [API] Fixed the bug in which numbers exceeding the 8th digit are broken 
* [API] Changed the ReverseGeocoding engine  
* [API] Fixed the StaticMap IE bug
* [SDK] Added an interface restricting the area for map movement 
* [SDK] Added I/F for enabling/disabling logo-click events  
* [SDK] Added the intent interface calling open-source license, or legal announcement activity (Android)
* [SDK] Added the Call ViewController interface for open-source license or legal announcement (iOS)
* [SDK] Added the feature of setting space between marker icon and title 
* [SDK] Changed the property of INVLatLng and INVLatLngBounds as readonly (iOS)
* [SDK] Applied Deprecated for INVCameraUpdateParams#scrollTo  (replaced by targetTo) (iOS)
* [SDK] Applied Deprecated for INVCameraUpdateParams#scrollBy  (replaced by targetBy) (iOS)
* [SDK] Applied Deprecated for INVLatLngBounds#latLngBoundsSouthWest (replaced by boundsWithSouthWest) (iOS)

### Nov. 26, 2019 
#### More Features
* [API] Added estimated search of general routes
	* Added the search navigation for estimated departure/arrival time based on statistics 
* [SDK] Added estimated navigation of general routes 
	* Added the LocationIcon feature (changing the shape and position of location icons)
	* Added InvRoute (to expose routes on the map)
	* Applied Deprecated for InvMultiLine (replaced by InvRoute)
#### Feature Updates
* [API] Changed to WGS84, which is the default coordinates of v3.0 API   
* Added StaticMap API Image files 
* [SDK] Fixed the error in which color is not properly displayed, with the setup of colors, including the alpha value. (Android)
* [SDK] Fixed the error in which shape disappears from a particular map level (iOS)
* [SDK] Fixed the error of infrequently abnormal exposure of distance on a scale bar (iOS)
* [SDK] Improved the overlapped map cycle icons when the map level is fast changed  
* [SDK] Fixed the error in which it is abnormally closed with a click of the log on iOS 10 or lower versions  (iOS)   
* [SDK] Fixed the error in which it is abnormally closed with the creation of InvShape before map initialization. (Android)

### Oct. 29, 2019 
#### Release of v3.0 

* Service the most updated iNavi technology with APIs on the new Maps version
* Clear and fast map service is available due to vector-based map configuration, regardless of resolution
* By using both WebGL and vector files, flawless zooming on high-resolution, as well as a variety of visualization, are supported between background maps and data layer 

* Quality Upgraded for Map Background/Cycle 
    * Improved the overall color and style of the map background
    * Added the North Korean region on the map, and improved the configuration data of roads, buildings, and facilities on each map level
    * Selectively show cycle data based on big data analysis and statistics by using destination information from the on-vehicle navigation system 
    * Conduct on-site nationwide investigation so as to update map data on a regular basis and provide the most updated data precisely and fast 

* Added Web Maps API 
    * Available to change engine for vector map rendering, set map rotation, rotation angle/tilting level, and return boundary coordinates on the map 
    * Set/Undo map events (e.g. clicks, double-clicks, mouse-over, right-clicks, and dragging)
    * APIs provided for marker, marker clustering, information window, polyline/polygon/circle, and coordinate conversion 

* Added API v3.0 
    * Added an API integrating with iNavi's new route navigation engine
    * Guide for optimized routes and fast search of directions based on real-time traffic data 
    * Added an API which navigates multiple destinations, allowing the query of each navigation time and distance data from one-time navigation. 
    * Added an API for multiple departure navigation, allowing the query of each navigation time and distance data from one-time navigation. 
    * Added Static Maps API
    * Added API creating static map images with the map size in need and marker images.  
    * As part of vector map characteristics, map rotation, angle setting, and double zoom-ins are available, hence creating a brighter map. 

* Added development guides for Maps SDK and Sample Apps for Android and iOS 
    * Allows creating/setting map object, coordinates object, camera movement, zoom-in/out, tilting and rotation
    * Features of marker (creating, specifying icons or locations, and etc.), caption (text exposed along with a marker), style setting (color, size, opacity, overlapping, and Z-index)
    * Allows creating/setting information window (tool-tips), setting adapter or events, creating polyline/polygon/circle, and setting styles. 

### Nov. 27, 2018
#### More Features 
* [API] Added Coordinates Conversion API 
	* Added conversion API between coordinates (WGS84 coordintes <-> TM coordinates)

### April 24, 2018
#### Feature Updates 
* [Batch] Changed the mechanism for the operations of statistics batch 
    * Changed the Log Creation Time: Changed from 00 sec 00 minute of every hour, into 30 sec 00 min of every hour  
    * Changed the method of creating base date and time on column: On batch server time 

#### Guide Updates 
* Deleted Android and iOS User Guides
    * Integrated into Mobile Web Map within User Guide of Web Maps 

### March 22, 2018
#### More Features 
* [API] Added Web Maps v.2.0 API
    * Main map features based on HTML5
    * Map rotation is availabe
        * Mobile: Use two fingers
        * PC : Shift+alt+drag or set an angle in need 
    * Provides Overview which displays more than one map on the screen
    * Added the effects of map loading events and animation 
    * Preload Tiles
        * Mark by caching once-confirmed area images 
    * Processing KML/GPX File Type
        * Load KML/GPX files and mark onto the map; map data can be returned into KML/GPX types  
* [Console] Added Web Maps v2.0 
    * Added example script for Web Maps v2.0
    * Added Web Maps v2.0 for the statistics item

### June 22, 2017 
#### Bug Fixes
* [Console] Fixed the bug in which the search result of Execution-Integrated Search example is not properly queried

### April 20, 2017 
#### Feature Updates 
* [API] Search of coordinates (coordinates -> address)
	* Added a type of coordinates available for query (TW coordinates only -> TW and WGS84 coordinates)

### March 23, 2017 
#### New Product Releases 
* The API service is an optimized web map solution based on the web map service, providing web maps, integrated search, and route navigation.  
    * All API services are available at once, including iNavi's specialized maps, search, and getting directions. 
    * Various map features are available via web maps API, including movement, zoom-in/out, and aerial maps. 
    * Integrated search is available for building name, phone number, land-lot number-based address (old address system), and road name-based address (new address system). 
    * With traffic data reflected on route navigation, getting a direction becomes faster and easier.   
