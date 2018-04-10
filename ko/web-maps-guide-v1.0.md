## Application Service > Maps > Web 지도 v1.0 가이드

Maps 웹지도를 사용하는 데 필요한 API를 설명합니다.

## API 공통 정보

### 사전 준비
- API 사용을 위해서는 앱키가 필요합니다.
- 앱 키는 Console 상단 "URL & Appkey" 메뉴에서 확인 가능합니다.

### 요청 공통 정보

#### URL 정보

| 항목 | URL |
| --- | --- |
| 지도 | https://api-maps.cloud.toast.com/maps/js/v1.0/map.js |
| Static 지도 | https://api-maps.cloud.toast.com/maps/js/v1.0/staticMap.js |

## Web 지도

### 1. Web 지도

JavaScript 기반 TOAST Maps API를 이용하여 웹 브라우저에 지도를 표시하는 방법을 설명합니다.
TOAST Maps API는 팅크웨어 좌표를 사용합니다. 축약해서 TW 좌표, TW X좌표, TW Y좌표로 표시합니다.
메소드에서 옵션 매개변수는 [param]으로 표시합니다. 옵션 매개변수는 생략할 수 있습니다.

> ※ TOAST Maps API에서 사용되고 있는 좌표는 팅크웨어 전용 좌표로만 사용되고 있습니다.
<br>팅크웨어 좌표를 위경도 좌표(WGS84)로 변환하기 위해서는 THINKMAP.tw_Wgs84() 함수를 이용하여 변경하시고,
반대로 위경도 좌표(WGS84)를 팅크웨어 좌표로 변환하기 위해서는 THINKMAP.wgs84_Tw() 함수를 이용하시기 바랍니다.


#### 주요 TOAST Maps API 안내
##### 추가적인 TOAST Maps API 사용법은 해당 <a href="http://developers1.inavi.com:8086?key=19b6272o5" target="_blank" rel="nofollow">링크</a>를 참조하시기 바랍니다.

| API 명 | Parameter | Returns | 설명 |
|------|------------------------|---------------|---------------|
| THINKMAP.initMap(map_div_name, twX, twY, level, init_cb, arrange_type, map_type) | map_div : String || 지도를 담을 div 태그 ID<br>지도를 사용하기 위해서 최초에 반드시 호출해야 하는 초기화 함수입니다. |
||twX : Number	||지도 초기화 TW X 좌표|
||twY : Number	||지도 초기화 TW Y 좌표|
||level : Number||지도 초기화 Level<br>- 일반지도 : 1~13<br>- 항공지도 : 1~13|
||init_cb : function()||지도 초기화 이후 호출되는 콜백함수|
||arrange_type : Number	||지도 레이어 정렬방식<br>1 : 중앙정렬방식(resize효과 있음)<br>2 : 전체로딩방식(resize효과 없음)<br> 3 : 우상단정렬방식(resize효과 있음)|
||map_type : String	||지도 타입 설정<br>'i' : 일반맵<br>'a' : 항공맵<br>'s' : 요약맵<br>'m' : 모바일|
|THINKMAP.imageMap()|||지도를 일반 지도로 전환합니다.|
|THINKMAP.aerialMap()|||지도를 항공 지도로 전환합니다.|
|THINKMAP.setAerialHybrid(active)|active : Boolean||항공주기 표시 여부  <br>true : 지도위에 항공주기를 표출   <br>false : 지도위에 항공주기 표출안함<br><br>지도 위에 항공지도 주기 표출여부를 설정합니다.|
|THINKMAP.addMapListener(event_name, func_cb)|event_name : String<br> ||지도에 등록할 이벤트 이름<br>'movestart'<br>- 지도가 움직이기 시작했을 때<br>'move'<br> - 지도가 움직일 때<br>'moveend'<br>- 지도 움직임이 끝났을 때<br>'zoomend'<br>- 지도가 확대, 축소가 끝났을 때<br>'mouseover'<br>- 지도위에 마우스가 들어왔을 때<br>'mouseout'<br>- 지도에서 마우스가 나갔을 때<br> 'mousemove'<br>- 지도에서 마우스가 움직일 때<br><br>지도에 이벤트를 등록합니다.<br>(지도에 관련된 이벤트, 확대/축소, 움직임 등)|
||func_cb : function()||지도에서 이벤트가 발생했을 때 호출되는 콜백 함수<br>(콜백함수에 매개변수로 Map 객체가 전달됩니다)|
|THINKMAP.removeMapListener(event_name)|event_name : String||지도에 제거할 이벤트 이름<br>'movestart'<br>- 지도가 움직이기 시작했을 때<br>'move'<br> - 지도가 움직일 때<br>'moveend'<br>- 지도 움직임이 끝났을 때<br>'zoomend'<br>- 지도가 확대, 축소가 끝났을 때<br>'mouseover'<br>- 지도위에 마우스가 들어왔을 때<br>'mouseout'<br>- 지도에서 마우스가 나갔을 때<br> 'mousemove'<br>- 지도에서 마우스가 움직일 때<br><br>지도에 등록한 이벤트를 제거합니다. <br>THINKMAP.addMapListener 메소드로 등록한 event_name에 해당하는 모든 콜백함수를 삭제하므로 주의가 필요합니다.|
|THINKMAP.createMarker(twX, twY, width, height, iconUrl, [param])|twX : Number||<br>Marker 객체 위치 TW X 좌표 <br><br>Marker 객체를 생성합니다. <br>생성한 Marker 객체를 지도에 표출하기 위해서는 THINKMAP.addMarker 메소드로 지도에 Marker 객체를 추가해야합니다.|
||twY : Number	||Marker 객체 위치 TW Y 좌표|
||width : Number||Marker 이미지 너비|
||height : Number ||Marker 이미지의 높이|
||iconURL : String ||Marker 이미지의 URL|
||param : String||Marker 객체의 사용자 변수||
|THINKMAP.addMarker(marker)|marker : Marker||지도에 추가할 대상 Marker 객체<br><br>지도에 Marker 객체를 추가합니다.|
|THINKMAP.featureDrawing(draw_type, style, func_cb)|draw_type : String||사용자가 그릴 Feature 객체 타입<br>'lineDraw' : 선<br>'polygonDraw' : 다각형<br> 'regularPolygonDraw' :   형태가 정해진 다각형<br><br>사용자가 지도에 마우스로 Polyline, Polygon을 직접 그릴 수 있는 그리기모드로 전환합니다.<br>지도 마우스 클릭 시 객체 그리기가 시작되고 마우스를 더블클릭하면 그리기가 완료됩니다. <br>그리기 완료 시 콜백함수로 그려진 Feature 객체를 넘겨줍니다. |
||style : Object||<br> Polygon, Polyline의 스타일을 지정하기 위한 Object<br>strokeColor : 선 색<br>- 'red', '#fff123' <br> strokeWidth : 선 두께<br> - 10<br> strokeOpacity : 선 투명도<br>fillColor : 채우기 색<br>fillOpacity : 채우기 투명도 <br>strokeDashstyle : 선 스타일<br>dot : · · · · · · <br>dash : - - - - - -<br>dashdot : - · - · - · - <br>longdashdot: ㅡ · ㅡ · ㅡ<br> solid : 일반라인  <br> |
||func_cb : function()||사용자가 지도를 더블클릭하여<br>Feature 객체 그리기가 완료되었을 때 호출되는 콜백함수|
|THINKMAP.featureDrawingCancel()|||지도에 사용자가 마우스로 Polyline, Polygon을 직접 그릴 수 있는 그리기모드를 종료합니다. |
|THINKMAP.tw_Wgs84(twX, twY)|twX : Number|coord : Object<br>변환된 WGS84 좌표<br>- coord.curx : WGS84 X 좌표<br>- coord.cury  : WGS84 Y 좌표|변환할 TW X 좌표<br><br>TW 좌표를 WGS84 좌표로 변환합니다. |
||twY : Number||변환할 TW Y 좌표|
|THINKMAP.wgs84_Tw(wgs_lon, wgs_lat)|wgs_lon : Number|coord : Object<br>변환된 TW 좌표 <br>- coord.curx  : TW X 좌표<br>- coord.cury  : TW Y 좌표 |변환할 WGS84 경도 좌표<br><br>WGS84 좌표를 TW 좌표로 변환합니다.|
||wgs_lat : Number||변환할 WGS84 위도 좌표|


#### TOAST Maps API 사용하기
```
// 지도 사용을 위한 js 파일을 선언 합니다.
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v1.0/map.js"></script>
<script>
	// 지도 사용을 위한 인증을 진행 합니다.
	Map.authentification("appKey");
</script>

//지도를 담을 DIV를 생성 합니다.
<div id="div_map"></div>
<script type="text/javascript">

	//선언한 DIV에 지도를 표출 합니다.
	THINKMAP.initMap("div_map", 165406, 500198, 12, init, 2, 'i');

	// 지도 init 후 콜백 함수가 실행 됩니다.
	function init(){
		alert('init!');
	}
</script>
```

#### 지도 모드  변경 하기
```
<script type="text/javascript">
	//지도를 일반 지도로 전환
	THINKMAP.imageMap();

	//지도를 항공 지도로 전환
	THINKMAP.aerialMap();

	//지도 위에 항공주기 표출여부 설정
	THINKMAP.setAerialHybrid(active);
</script>
```
#### 지도 이벤트 등록 하기
```
<script type="text/javascript">
	//지도에 move 이벤트를 등록 한다.
	THINKMAP.addMapListener('move', mapEvent_cb);

	//지도 이벤트 발생 시 콜백 함수
	function mapEvent_cb(map){
	    console.log("event callback!");
	}
</script>
```
#### 지도 이벤트 제거 하기
```
<script type="text/javascript">
	//지도에 move 이벤트를 제거 한다.
	THINKMAP.removeMapListener('move');
</script>
```

#### 지도 마커 추가 하기
```
<script type="text/javascript">
	//지도에 마커를 객체를 초기화 한다.
	var marker = null;
	function createMarker(){
		if(!marker){
			//마커 객체를 생성 한다.
			marker = THINKMAP.createMarker(163670, 526934, 47, 46, '../img/img.png', 'my_marker');
			//마커를 지도에 추가 한다.
			THINKMAP.addMarker(marker);
			console.log('id : ' + marker._feature_id + ', param : ' + marker._param);
		}
	}
</script>
```


#### 지도 그리기 모드로 전환 하기
```
<script type="text/javascript">
	//지도를 그리기 모드로 전환 한다.
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
		alert("그리기 모드 전환!");
	}
</script>
```

#### 지도 그리기 모드 종료 하기
```
<script type="text/javascript">
	//지도 그리기 모드를 종료 한다.
	THINKMAP.featureDrawingCancel();
</script>
```


#### TW 좌표를 WGS 좌표로 변환 하기
```
<script type="text/javascript">
	var wgs;

	// TW 좌표를 WGS좌표로 변환 한다.
	wgs = THINKMAP.tw_Wgs84(165406, 500198);

	console.log(wgs.curx);
	console.log(wgs.cury);
</script>
```


#### WGS 좌표를 TW 좌표로 변환 하기
```
<script type="text/javascript">
	var tw;

	// WGS 좌표를 TW좌표로 변환 한다.
	wgs = THINKMAP.wgs84_Tw(127.28976653131843, 37.56515136725675);

	console.log(tw.curx);
	console.log(tw.cury);
</script>
```

### 2. Static 지도

#### TOAST Maps API Static 지도 사용하기
```
// Static 지도 사용을 위한 js 파일을 선언 합니다.
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v1.0/staticMap.js"></script>

// 지도를 담을 IMG를 생성 합니다.
<img id='staticMapImg' alt="" src="">

<script>

	// Static 지도 사용을 위한 인증 및 파라미터를 전달 합니다. 	
	StaticMap.authentification('staticMapImg',"appkey",'x=157423&y=266836&width=970&height=300&level=10&maptype=i&mx=158323&my=266836&txt=');

</script>
```

| 이름 | 타입	| 필수 여부 | 설명 |
|---|---|---|---|
| x | Integer | 필수 | 지도 중심 X좌표 |
| y | Integer | 필수 | 지도 중심 Y좌표 |
| mx | Integer | 필수 | 마커 X좌표 |
| my | Integer | 필수 | 마커 Y좌표 |
| width	| Integer | 선택 | 지도 넓이 <br> 미입력 시 기본 600px |
| height | Integer | 선택 | 지도 높이 <br> 미입력 시 기본 600px |
| imgurl | String | 선택 | 마커 이미지 url<br> 미입력 시 기본 마커 사용 |
| level | Integer | 선택 | 지도 레벨 <br> 미입력 시 기본 10 |
| maptype | String | 선택 | 지도 타입 <br> 미입력 시 기본 일반맵 |
| label | String | 선택 | 라벨 내용 |

### 3. Mobile Web 지도

Android / IOS WebView로 하이브리드 형태의 앱을 개발 할때 TOAST Maps API를 이용 하여 Javascript 기반의  Web 지도와 동일한 API로 사용 하실 수 있습니다.
API 관련해서는 [1. Web 지도](#map_guide_web) 를 참고 하시기 바랍니다.