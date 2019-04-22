## Application Service > Maps > iOS 사용 가이드

iOS 기반으로 Maps 서비스를 사용하는 방법을 설명합니다.

## API 공통 정보

### 사전 준비
- API를 사용하려면 앱키가 필요합니다.
- 앱키는 **TOAST Console** 상단 **URL & Appkey** 메뉴에서 확인할 수 있습니다.

### 요청 공통 정보

#### URL 정보
##### [지도 API]

| 항목        | URL                                      |
| --------- | ---------------------------------------- |
| 지도        | https://api-maps.cloud.toast.com/maps/js/v1.0/map.js |
| 정적(static) 지도 | https://api-maps.cloud.toast.com/maps/js/v1.0/staticMap.js |

## 지도

### 1. iOS WebView 지도

iOS에서 API를 호출하고 콜백 함수로 파라미터를 전달받는 방법을 설명합니다.


#### A. 주요 TOAST Maps iOS WebView API 안내
##### 추가적인 TOAST Maps Android WebView API 사용법은 <a href="http://developers1.inavi.com:8086?key=19b6272o5" target="_blank" rel="nofollow">Thinkware API Center</a>를 참고하시기 바랍니다.  

> ※ TOAST Maps API에서 사용되는 좌표는 팅크웨어 전용 좌표로만 사용됩니다.
> <br>팅크웨어 좌표를 경위도 좌표(WGS84)로 변환하려면 TMWA.getWgs84FromTw() 함수를 이용합니다. 반대로 경위도 좌표(WGS84)를 팅크웨어 좌표로 변환하려면 TMWA.getTwFromWgs84() 함수를 이용합니다.

| API 이름                                   | 파라미터                                     | 콜백 메서드           | 콜백 파라미터                                  | 설명                                       |
| ---------------------------------------- | ---------------------------------------- | ---------------- | ---------------------------------------- | ---------------------------------------- |
| TMWI.initMap(map_div_name, twX, twY, level, arrange_type, map_type) | map_div : String<br>	지도를 담을 div 태그 ID    | initCB <br><br>  | 지도 초기화 성공여부<br>'true' : 성공<br> 'false' : 실패 | 지도를 사용하려면 최초에 반드시 호출해야 하는 초기화 함수입니다.  |
|                                          | twX : Number	<br>지도 초기화 TW X 좌표          |                  |                                          |                                          |
|                                          | twY : Number	<br>지도 초기화 TW Y 좌표          |                  |                                          |                                          |
|                                          | level : Number	<br>지도 초기화 Level<br>- 일반 지도 : 1~13<br>- 항공 지도 : 1~13 |                  |                                          |                                          |
|                                          | arrange_type : Number	<br>지도 레이어 정렬 방식<br>1: 중앙 정렬 방식(resize효과 있음)<br>2: 전체 로딩 방식(resize효과 없음)<br> 3: 오른쪽 상단 정렬 방식(resize효과 있음) |                  |                                          |                                          |
|                                          | map_type : String	<br>지도 타입 설정<br>'i': 일반맵<br>'a': 항공맵<br>'s': 요약맵 |                  |                                          |                                          |
| TMWI.getLevel()                          |                                          | getLevelCB       | 지도의 현재 레벨                                | 지도의 레벨을 가져옵니다.                           |
| TMWI.getCenter()                         |                                          | getCenterCB      | 지도의 현재 중심 좌표<br> 'twX&#124;twY'           | 지도의 중심 좌표를 가져옵니다.                         |
| TMWI.getExtent()                         |                                          | getExtentCB      | 지도의 영역 좌표<br> 'leftX&#124;topY&#124;rightX&#124;bottomY' | 현재 지도가 표출되는 영역 좌표를 가져옵니다.                 |
| TMWI.setMoveend()                        |                                          | moveendCB        | 확대, 축소, 이동 후 지도 중심 좌표와 레벨 <br>'twX&#124;twY&#124;level' | 지도에 moveend 이벤트를 등록합니다.<br>moveend : 지도 확대, 축소, 이동이 끝났을 때 |
| TMWI.removeMoveend()                     |                                          |                  |                                          | 지도에서 moveend 이벤트를 제거합니다.                 |
| TMWI.setTouchend()                       |                                          | setTouchendCB    | 터치한 지도 좌표<br> 'twX&#124;twY'             | 지도에 touchend 이벤트를 등록합니다.<br>  touchend : 지도 터치가 끝났을 때 |
| TMWI.removeTouchend()                    |                                          |                  |                                          | 지도에서 touchend 이벤트를 제거합니다.                |
| TMWI.setZoomend()                        |                                          | zoomendCB        | 확대, 축소 후 지도 중심좌표와 레벨<br> 'twX&#124;twY&#124;level' | 지도에 zoomend 이벤트를 등록합니다. <br> zoomend : 지도 확대, 축소가 끝났을 때 |
| TMWI.removeZoomend()                     |                                          |                  |                                          | 지도에서 zoomend 이벤트를 제거합니다.                 |
| TMWI.setTouchEvent(event_name)           | event_name : String<br>	등록할 이벤트 이름<br> 'touchstart' : 지도 터치를 시작했을때<br>  'touchend' : 지도 터치가 끝났을 때<br>  'longpress' : 지도를 길게 눌렀을 때 | setTouchEventCB  | 발생한 이벤트와 터치한 지도 좌표 <br>'event_name&#124;twX&#124;twY' | 지도에 touch 관련 이벤트를 등록합니다.                  |
| TMWI.removeTouchEvent(event_name)        | event_name : String<br>	등록할 이벤트 이름<br> 'touchstart' : 지도 터치를 시작했을때<br>  'touchend' : 지도 터치가 끝났을 때<br>  'longpress' : 지도를 길게 눌렀을 때 |                  |                                          | 지도에서 touch 관련 이벤트를 제거합니다.                 |
| TMWI.createAndAddMarker(twX, twY, iconWidth, iconHeight, iconUrl, [param]) | twX : Number<br>Marker 객체의 TW X 좌표       | createMarkerCB   | Marker 객체 아이디와 사용자 변수 param<br> 'marker_id&#124;param' | Marker 객체를 생성하고 지도에 추가합니다.               |
|                                          | twY : Number	<br>Marker 객체의 TW Y 좌표      |                  |                                          |                                          |
|                                          | iconWidth : Number <br>Marker 이미지 너비     |                  |                                          |                                          |
|                                          | iconHeight : Number <br>Marker 이미지의 높이   |                  |                                          |                                          |
|                                          | iconURL : String <br>Marker 이미지의 URL     |                  |                                          |                                          |
|                                          | param : String <br>Marker 객체의 사용자 변수     |                  |                                          |                                          |
| TMWI.setTouchendMarkerCB(id)             | id : Number<br>이벤트를 등록할 대상 Marker 객체 아이디 | touchendMarkerCB | Marker 객체 아이디와 Marker 객체의 TW X좌표, TW Y좌표,<br> 사용자 변수 param<br> 'marker_id&#124;twX&#124;twY&#124;param' | Marker 객체에 touchend 이벤트를 등록합니다.          |
| TMWI.removeTouchendMarker(id)            | id : Number<br>이벤트를 제거할 대상 Marker 객체 아이디 |                  |                                          | Marker 객체에 touchend 이벤트를 제거합니다.          |
| TMWI.getTwFromWgs84(lon, lat)            | lon : Number<br>변환할 WGS84 경도 좌표          | getTwFromWgs84CB | 변환된 TW 좌표 <br>'twX&#124;twY'             | WGS84 좌표를 TW 좌표로 변환합니다.                  |
|                                          | lat : Number<br>변환할 WGS84 위도 좌표          |                  |                                          |                                          |
| TMWI.getWgs84FromTw(twX, twY)            | twX: Number<br>변환할 TW X 좌표               | getWgs84FromTwCB | 변환된 WGS84 좌표 <br>'lon&#124;lat'          | TW 좌표를 WGS84 좌표로 변환합니다.                  |
|                                          | twY : Number<br>변환할 TW Y 좌표              |                  |                                          | -                                        |
