## Application Service > Maps > Web map v2.0 Guide

Maps 웹지도를 사용하는 데 필요한 API를 설명합니다.

## v2.0 개선 사항
* 지도 표준 관련 기능 확대
	* Html5 기반의 지도 주요 기능을 사용 가능합니다.
	* 지도 내 픽쳐, 마커 등 모든 피처를 객체화하여 사용성 및 성능을 개선하였습니다.
* 지도 회전 가능
	* 모바일에서는 투 핑거를 통해 지도 회전이 가능합니다.
	* PC 버전에서는 Shift+alt+드래그 하거나 원하는 각도를 설정하여 지도 회전이 가능합니다.
* 피처 클러스터(도형 제외)
	* 지도 축소 시에는 근접한 피처를 병합하여 보여주거나 확대 시에는 상세히 나누어서 보여줍니다.
* 지도 이미지 다운로드
	* 지도를 이미지 파일로 다운받을 수 있는 function을 제공합니다.
* 오버뷰
	* 지도를 화면에 하나 이상 표시할 수 있습니다.
* 지도 로드 이벤트 및 애니메이션 효과 추가
	* 타일 이미지에 로드 이벤트를 추가하는 기능을 제공합니다.
	* 이미지 로드에 따른 progress bar 효과 등에 활용할 수 있습니다.
* Preload 타일
	* 한 번 확인했던 영역의 이미지를 캐싱 하여 표시합니다.
* KML/GPX 파일 타입 처리
	* KML/GPX 파일을 불러와 지도에 표시하고, 지도에 표시된 데이터를 KML/GPX 타입으로 반환 가능합니다.

## API 공통 정보

### 사전 준비
- API 사용을 위해서는 앱키가 필요합니다.
- 앱 키는 Console 상단 "URL & Appkey" 메뉴에서 확인 가능합니다.

### 요청 공통 정보

#### URL 정보

| 항목 | URL |
| --- | --- |
| 지도 | https://api-maps.cloud.toast.com/maps/js/v2.0/map.js |
| Static 지도 | https://api-maps.cloud.toast.com/maps/js/v2.0/staticMap.js |

## Web 지도

### 1. Web 지도

Javascript 기반 TOAST Maps API를 이용하여 웹 브라우저에 지도를 표시하는 방법을 설명합니다.
TOAST Maps API는 팅크웨어 좌표를 사용합니다. 축약해서 TW 좌표, TW X좌표, TW Y좌표로 표시합니다.
메소드에서 옵션 매개변수는 [param]으로 표시합니다. 옵션 매개변수는 생략할 수 있습니다.

> ※ TOAST Maps API에서 사용되고 있는 좌표는 팅크웨어 전용 좌표로만 사용되고 있습니다.
<br>팅크웨어 좌표를 위경도 좌표(WGS84)로 변환하기 위해서는 THINKMAP.tw_Wgs84() 함수를 이용하여 변경하시고,
반대로 위경도 좌표(WGS84)를 팅크웨어 좌표로 변환하기 위해서는 THINKMAP.wgs84_Tw() 함수를 이용하시기 바랍니다.


#### 주요 TOAST Maps API 안내
##### 추가적인 TOAST Maps API 사용법은 해당 <a href="http://developers1.inavi.com:8086?key=19b6272o5" target="_blank" rel="nofollow">링크</a>를 참조하시기 바랍니다.

| API 명 | Parameter | Returns | 설명 |
|------|------------------------|---------------|---------------|
| new thinkware.maps.Map(map_div, option) | map_div : String | | 지도를 표시할 DOM 엘리먼트 또는 엘리먼트의 ID |
| | option.type : String | | 지도의 타입 <br> i(일반),<br> m(모바일),<br> s(요약),<br> a(항공배경),<br> m_a(모바일항공),<br> s_a(요약항공),<br> hybrid(항공) <br>default: i |
| | option.center.twX : number | | 지도의 중심 X 좌표: 팅크웨어 좌표단위 |
| | option.center.twY : number | | 지도의 중심 Y 좌표: 팅크웨어 좌표단위 |
| | option.level : number | | 지도의 레벨 |
| | option.callback : function() | | 초기화 후 실행할 함수 |
| | option.logo : String | | 로고를 표시할 위치 <br> top-left,<br>  top-center,<br>  top-right,<br>  center-left,<br>  center-center,<br>  center-right,<br>  bottom-left,<br>  bottom-center,<br>  bottom-right |
| changeType(type) | type : String | | 지도의 타입 <br> i(일반),<br> m(모바일),<br> s(요약),<br> a(항공배경),<br> m_a(모바일항공),<br> s_a(요약항공),<br> hybrid(항공) <br>default: i |
| thinkware.maps.event.addListener(target, event_type, func_cb) | target : Object | | 리스너를 추가할 대상 객체 |
| | event_type : String | | wheelup, <br> wheeldown, <br> wheel, <br>zoomend, <br>movestart, <br>move, <br>moveend, <br>tileloadstart, <br>tileloadend, <br>tileloaderror, <br>click, <br>dblclick, <br>rightclick, <br>mousemove, <br>mouseup, <br>mousedown |
| | func_cb : function() | | 등록할 리스너 |
| thinkware.maps.event.removeListener(target, event_type, func_cb) | target : Object | | 리스너를 제거할 대상 객체 |
| | event_type : String | | wheelup, <br> wheeldown, <br> wheel, <br>zoomend, <br>movestart, <br>move, <br>moveend, <br>tileloadstart, <br>tileloadend, <br>tileloaderror, <br>click, <br>dblclick, <br>rightclick, <br>mousemove, <br>mouseup, <br>mousedown |
| | func_cb : function() | | 제거할 리스너 |
| new thinkware.maps.Marker(option) | option.map : Object | thinkware.maps.Marker 마커 객체 | 지도 객체 |
| | option.icon.url : String | | 아이콘Url |
| | option.icon.size.width : number | | 아이콘 너비 |
| | option.icon.size.heigth : number | | 아이콘 높이 |
| | option.position.twX : number | | 마커 생성 X좌표(팅크웨어 좌표단위) |
| | option.position.twY : number | | 마커 생성 Y좌표(팅크웨어 좌표단위) |
| | option.positioning : String | | 좌표가 위치할 곳<br> top-left,<br>  top-center,<br>  top-right,<br>  center-left,<br>  center-center,<br>  center-right,<br>  bottom-left,<br>  bottom-center,<br>bottom-right |
| | option.title : String | | 툴팁 문자열 |
| | option.offset.pxX : number | | 픽셀 단위 |
| | option.offset.pxY : number | | 픽셀 단위 |
| | option.visible : boolean | | 표시 여부 |
| | option.draggable : boolean | | 드래그 가능 여부 |
| | option.zIndex : number | | z-index 값 |
| | option.opacity : number | | 투명도 |
| | option.stopEvent : boolean | | 마커상에서 지도 이벤트 실행 방지 여부 |
| thinkware.maps.LineString.drawStart(target, option) | target : Object | | 지도 객체 |
| | option.stroke.style : String | | 선 스타일<br><br> dot : · · · · · · <br>dash : - - - - - -<br>dashdot : - · - · - · - <br>longdashdot: ㅡ · ㅡ · ㅡ<br> solid : 일반라인 |
| | option.stroke.weight : number | | 선 굵기(px) |
| | option.stroke.color : String | | 선 색상 |
| | option.stroke.opacity : number | | 선 투명도 |
| | option.callback : function() | | 그리기 종료 후 실행할 함수 |
| | option.measure : boolean | | 거리 측정 팝업 표시 여부 |
| | option.isOnce : boolean | | 한번 그리기 후 종료 여부 |
| thinkware.maps.LineString.drawEnd(target) | target : Object | | 지도 객체 |
| thinkware.maps.util.getLonLatFromCoordinate(param) | param.twX : number | Coord 좌표<br>Object.lon : WGS84<br>Object.lat : WGS84 | 팅크웨어 X좌표 |
| | param.twY : number | | 팅크웨어 Y좌표 |
| thinkware.maps.util.getCoordinateFromLonLat(param) | param.lon : number | TW 좌표<br>Object.twX: TW X 좌표<br>Object.twY : TW Y 좌표 | 경도 |
| | param.lat : number | | 위도 |


#### TOAST Maps API 사용하기
```
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v2.0/map.js"></script>
<script>
	//지도 사용을 위한 인증을 진행 합니다.
	Map.authentification("appKey");
</script>

<div id="div_map"></div>
<script type="text/javascript">

	//선언한 DIV에 지도를 표출 합니다.
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

#### 지도 모드 변경 하기
```
<script type="text/javascript">

 	// 생성된 지도 객체의 지도 Type을 변경 합니다.
 	// 일반: i, 모바일: m, 요약: s, 항공배경: a, 모바일항공: m_a, 요약항공: s_a, 항공: hybrid
	// 항공배경지도로 변경 합니다.
	map.changeType('i');

</script>
```

#### 지도 이벤트 등록 하기
```
<script type="text/javascript">

	//지도에 move 이벤트를 등록 합니다.
	thinkware.maps.event.addListener(map, 'click', mapEvent_cb)
	
	 //지도 이벤트 발생 시 콜백 함수
    function mapEvent_cb(event){
        console.log("event callback!");
    }

</script>
```

#### 지도 이벤트 제거 하기
```
<script type="text/javascript">
	
	//지도에 move 이벤트를 제거 합니다.
	thinkware.maps.event.removeListener(map, 'move', mapEvent_cb)

</script>
```

#### 지도 마커 추가 하기
```
<script type="text/javascript">
	
	// 지도에 마커 객체를 추가 합니다.
	var marker = new thinkware.maps.Marker({
	    map: map,
	    position: {
	        twX: 169030, 
	        twY: 517922
	    },
	    stopEvent: false
	});
	
	// 지도에 마커 객체를 이동 시킵니다.
	marker.setPosition({twX: 169030, twY: 517922});

</script>
```

#### 지도 그리기 모드로 전환 하기
```
<script type="text/javascript">
	
	// 그리기 모드로 전환 합니다.
	var strokeOpt = {
		style : 'longdash'	// 선 스타일(solid, dash, longdash, ... 또는 segments 를 반환하는 함수 참고) default: "solid"
		, weight : 5		// 선 굵기(px) (default: 3)
		, color : '#3399ff'	//선 색상(default: #3399ff)
		, opacity : 1		//선 투명도(default: 1)
    };
	
	var drawOpt = {
		stroke : strokeOpt
		, callback : mapDraw_cb // 그리기 종료 후 실행할 함수(default: undefined)
		, measure : true 		// 거리 측정 팝업 표시 여부(default: false)
		, isOnce : false		// 한 번 그린 후 종료 여부(default: false)
	};

	//thinkware.maps.LineString.drawStart(map, drawOpt);

	function mapDraw_cb(map){
		console.log("draw finish!!!");
	}
</script>
```

#### 지도 그리기 모드 종료 하기
```
<script type="text/javascript">
	
	// 그리기 모드를 종료 합니다.
	thinkware.maps.LineString.drawEnd(map);

</script>
```

#### TW 좌표를 WGS 좌표로 변환 하기
```
<script type="text/javascript">
	
 	// TW 좌표를 WGS좌표로 변환 합니다.
 	var tws = {
		twX : 169030
		, twY: 517922
 	};
 	
 	var wgs84 = thinkware.maps.util.getLonLatFromCoordinate(tws);
 	console.log(wgs84.lon);
 	console.log(wgs84.lat);
 	
</script>
```

#### WGS 좌표를 TW 좌표로 변환 하기
```
<script type="text/javascript">
	
 	 // WGS 좌표를 TW좌표로 변환 합니다.
	 var wgs84 = {
		lon: 127.11074994024005
		, lat: 37.40215870673785
	};
 	 
	 var tws = thinkware.maps.util.getCoordinateFromLonLat(wgs84);
 	 
 	console.log(tws.twX);
 	console.log(tws.twY);
	
</script>
```

### 2. Static 지도

#### TOAST Maps API Static 지도 사용하기
```
// Static 지도 사용을 위한 js 파일을 선언 합니다.
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v2.0/staticMap.js"></script>

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