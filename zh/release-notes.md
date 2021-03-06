## Application Service > Maps > Release Notes

### 2020.01.21
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

### 2019.12.24
#### 기능  개선
* [API] 숫자데이터 8자리 초과시 깨지는 버그 해결
* [API] ReverseGeocoding 엔진변경
* [API] StaticMap IE 버그 해결
* [SDK] 지도 이동 영역을 제한하는 인터페이스 추가
* [SDK] 로고 클릭 이벤트 활성화 여부 설정 I/F 추가
* [SDK] 오픈소스 라이선스, 법적 공지 Activity 호출 Intent 인터페이스 추가 (Android)
* [SDK] 오픈소스 라이선스, 법적 공지 ViewController 호출 인터페이스 추가 (iOS)
* [SDK] 마커 아이콘과 타이틀 사이의 여백을 설정하는 기능 추가.
* [SDK] INVLatLng, INVLatLngBounds의 property readonly 속성으로 변경 (iOS)
* [SDK] INVCameraUpdateParams#scrollTo Deprecated 적용 (targetTo로 대체) (iOS)
* [SDK] INVCameraUpdateParams#scrollBy Deprecated 적용 (targetBy로 대체) (iOS)
* [SDK] INVLatLngBounds#latLngBoundsSouthWest Deprecated 적용 (boundsWithSouthWest로 대체) (iOS)

### 2019.11.26
#### 기능 추가
* [API] 일반 경로 예측 탐색 추가
	* 통계데이터 기반의 출발, 도착 예정시간기준 경로탐색 추가
* [SDK] 일반 경로 예측 탐색 추가
	* LocationIcon 기능 추가(위치 아이콘의 모양과 위치를 변경하는 기능)
	* InvRoute 추가(지도 위에 경로를 표출하는 셰이프)
	* InvMultiLine Deprecated 적용(InvRoute로 대체)

#### 기능개선
* [API] v3.0 API 기본좌표 WGS84로 변경
* StaticMap API Image파일 제공추가
* [SDK] alpha 값을 포함한 색상 설정 시 비정상인 색상으로 표출되는 오류 수정(Android)
* [SDK] 특정 지도 레벨에서 셰이프가 사라지는 오류 수정(iOS)
* [SDK] 간헐적으로 축척바의 거리가 비정상 표출되는 오류 수정(iOS)
* [SDK] 빠르게 지도 레벨 변경 시 지도 주기 아이콘이 겹치는 현상 개선
* [SDK] iOS 10 이하 단말에서 로고 클릭 시 비정상 종료되는 오류 수정(iOS)   
* [SDK] 지도 초기화 전에 InvShape 객체 생성 시 비정상 종료되는 오류 수정(Android)

### 2019.10.29
#### 신규 v3.0 출시

* 신규 Maps 버전에서 아이나비의 최신 기술을 API로 서비스
* 벡터 데이터 기반의 지도 구성을 통해 해상도에 상관 없이 선명하고 빠른 지도 제공
* WebGL과 벡터 타일을 함께 이용함으로써 고해상도의 매끄러운 줌, 배경 지도와 데이터 레이어 간의 시각화 효과를 다양하게 지원

* 지도 배경/주기 품질 향상
    * 지도 배경의 전체적인 색상, 스타일 개선
    * 북한 영역 지도 추가 및 지도 레벨별 도로, 건물, 시설물 형상 데이터 개선
    * 차량 내비 목적지 정보를 활용한 빅데이터 분석, 통계를 통해 주기 데이터 선별 표출
    * 전국 현지 조사를 통해 정기적인 지도 데이터 Update 및 정확하고 빠른 최신 데이터 제공
     
* 웹지도 API 추가
    * 벡터 지도 랜더링 엔진 변경, 지도 회전 설정, 회전 각도/기울기 설정, 지도의 경계 좌표 반환 기능
    * 지도 이벤트(클릭, 더블클릭, 마우스오버, 오른쪽 마우스 클릭, 드래그 등) 설정/제거
    * 마커, 마커 클러스터링, 정보창, 폴리라인/폴리곤/서클, 좌표변환 API 제공

* API v3.0 추가
    * 아이나비 신규 경로 탐색 엔진 연동 API 추가
    * 실시간 교통정보를 반영한 최적의 경로와 빠른 길찾기 안내
    * 여러 목적지에 대해 한번에 탐색하여 각각의 탐색 시간과 거리 정보를 조회 할 수 있는 다중 목적지 탐색 API 추가
    * 여러 출발지에서 목적지까지 한번에 탐색하여 각각의 탐색 시간과 거리 정보를 조회 할 수 있는 다중 출발지 탐색 API 추가
    * Static Map API 추가
    * 원하는 지도 영역(Size)과 마커 이미지로 정적 지도 이미지 생성 API 추가
    * 벡터 지도의 특성으로 지도의 회전과 각도 설정, 2배줌 확대 옵션, 선명한 지도 생성
    
* Android, iOS 지도 SDK 및 샘플 App, 개발 가이드 추가
    * 지도 객체 생성 및 설정 기능, 좌표 객체, 카메라 이동, 확대/축소, 기울기, 회전 기능 제공
    * 마커(생성, 아이콘 지정, 위치 지정 등), 캡션(마커와 함께 노출되는 텍스트), 스타일 설정(색상, 크기, 투명도, 겹침, Z-index 등) 기능
    * 정보창(말풍선) 생성/설정 기능, adapter 설정, 이벤트 기능, 폴리라인/폴리곤/서클 생성, 스타일 설정 기능

### 2018.11.27
#### 기능 추가
* [API] 좌표 변환 API 추가
	* 좌표간 변환 API 추가(WGS84 좌표 <-> TM 좌표)

### 2018.04.24
#### 기능 개선/변경
* [Batch] 통계 Batch 동작 기제 변경
    * 로그 생성 시간 변경 : 매시간 00분 00초에서 매시간 00분 30초로 변경
    * 기준 날짜, 시간 컬럼값 생성 방식 변경 : Batch 서버 시간 이용

#### 가이드 수정
* Android 사용 가이드, iOS 사용 가이드 삭제
    * Web 지도 가이드 내 Mobile Web 지도 항목으로 통합

### 2018.03.22
#### 기능 추가
* [API] Web 지도 v2.0 API 추가
    * Html5 기반의 지도 주요 기능 사용 가능
    * 지도 회전 가능
        * 모바일 : 투 핑거를 통해 지도 회전
        * PC : Shift+alt+드래그 하거나 원하는 각도를 설정하여 지도 회전
    * 지도를 화면에 하나 이상 표시할 수 있는 오버뷰 기능 제공
    * 지도 로드 이벤트 및 애니메이션 효과 추가
    * Preload 타일
        * 한 번 확인했던 영역의 이미지를 캐싱 하여 표시
    * KML/GPX 파일 타입 처리
        * KML/GPX 파일을 불러와 지도에 표시하고, 지도에 표시된 데이터를 KML/GPX 타입으로 반환 가능
* [Console] Web 지도 v2.0 항목 추가
    * Web 지도 v2.0 예제 스크립트 추가
    * 통계 항목에 Web 지도 v2.0 항목 추가

### 2017.06.22
#### 버그 수정
* [Console] 실행예제 - 통합 검색 예제 검색 결과가 정상적으로 조회되지 않는 버그 수정

### 2017.04.20
#### 기능 개선/변경
* [API] 좌표검색(좌표 -> 주소)
	* 좌표검색 이용 시 조회 가능한 좌표 타입 추가(기존 TW 좌표 -> TW 좌표, WGS84 좌표)

### 2017.03.23
#### 신규 상품 출시
* 웹 지도, 통합검색, 경로탐색을 제공하는 API 서비스로 웹 지도 서비스를 이용하여 상품을 개발할 수 있는 최적의 웹 지도 솔루션
    * 아이나비의 특화된 지도, 검색, 길 찾기 등의 API를 한번에 이용 가능
    * 웹 지도 API를 통하여 지도 이동, 확대/축소, 항공지도 등 다양한 지도 기능 제공
    * 통합된 검색 기능을 통하여 건물명, 전화번호, 지번 주소(구주소), 도로명 주소(신주소)를 한번에 모두 검색 할 수 있는 기능 제공
    * 교통정보를 반영한 Smart한 경로 탐색을 통해 빠르고 쉬운 길 찾기 서비스 제공
