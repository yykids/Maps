## Application Service > Maps > API Guide

Maps 서비스를 사용하는 데 필요한 API를 설명합니다.

## API 공통 정보

### 사전 준비
- API 사용을 위해서는 앱키가 필요합니다.
- 앱 키는 Console 상단 "URL & Appkey" 메뉴에서 확인 가능합니다.

### 요청 공통 정보

#### URL 정보

|환경|	도메인|
|---|---|
|Real|	https://api-maps.cloud.toast.com|

### 응답 공통 정보

#### 검색/탐색 API
- 모든 API 요청에 "200 OK"로 응답합니다. 자세한 응답 결과는 응답 본문의 헤더를 참고합니다.

```
{
	"header": {
		"isSuccessful": true,
		"resultCode": 0,
		"resultMessage": ""
	}
}
```

## 검색

### 1. 주소검색(주소 -> 좌표)
- 주소로 좌표(TW 좌표/WGS84 좌표/TM 좌표)를 검색합니다.

#### 요청

[URI]

| 메서드 |	URI |
|---|---|
|GET|	/maps/v1.0/appkeys/{appkey}/coordinates?query={query}&coordtype={coordtype}&startposition={startposition}&reqcount={reqcount}&admcode={admcode} |

[Path parameter]

| 이름  | 타입 | 필수 여부 | 유효 범위 | 설명 |
|---|---|---|---|---|
| appkey | String | 필수 |  | 고유의 Appkey |

[Query Parameters]

| 이름 | 타입 | 필수 여부 | 유효 범위 |	설명 |
|---|---|---|---|---|
|​ query | String | 필수 |  | 검색어 |
| coordtype |	String | 선택 |  | 좌표형식 <br>0 : TW 좌표<br> 1 : WGS84 좌표<br> 2 : TM 좌표 |
| startposition |	String | 선택 |  | 검색 시작 위치 <br>0 : 첫번째 위치<br>미입력 시 0으로 조회 |
| reqcount | String | 선택 |  | 검색 요청 개수 <br>0으로 설정 시 Max Count 반환 |
| admcode |	String | 선택 |  | 행정코드 |


#### 응답
##### 응답 본문

```
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": ""
  },
  "address": {
    "result": true,
    "totalcount": 2,
    "admtotalcount": 2,
    "admcount": 2,
    "res_type": "NNYN",
    "adm": [
      {
        "type": 2,
        "posx": "168425",
        "posy": "516725",
        "admcode": "4113510800",
        "jibun": "",
        "address": "경기도 성남시 분당구 판교동",
        "roadname": "",
        "roadjibun": "",
        "accuracy": 3
      },
      {
        "type": 2,
        "posx": "167300",
        "posy": "515526",
        "admcode": "4113511000",
        "jibun": "",
        "address": "경기도 성남시 분당구 백현동(판교동)",
        "roadname": "",
        "roadjibun": "",
        "accuracy": 3
      }
    ]
  }
}
```

##### 필드

| 이름 | 타입 | 설명 |
|---|---|---|
| header | Object | 헤더 영역 |
| header.isSuccessful |	Boolean |	성공여부 |
| header.resultCode |	Integer |	실패 코드 |
| header.resultMessage | String |	실패 메시지 |
| address |	Object | 본문 영역 |
| address.result | Boolean | 성공여부 |
| address.totalcount | Integer | 전체 검색결과 대상 개수 |
| address.res_type | String |	검색결과Type명칭 <br>명칭, 카테고리, 주소, 전화번호 순 <br>(ex) NYNN : 명칭 No, 카테고리 YES, 주소 NO, 전화번호 NO |
| address.adm |	Array |	검색결과 |
| address.adm[0].type | String | 검색 type <br>1 : 행정계 검색<br> 2 : 지번 검색<br>3 : 새주소 검색 |
| address.adm[0].posx | String | X좌표 |
| address.adm[0].posy | String | Y좌표 |
| address.adm[0].admcode | String | 행정코드 |
| address.adm[0].address | String |	주소 |
| address.adm[0].roadname | String | 새주소 도로명 |
| address.adm[0].roadjibun | String |	새주소 지번 |
| address.adm[0].accuracy | Integer |	지번 정확도 <br>0 : 정확 검색<br> 1 : 호지번 확장<br>ex) 963-2 검색 시 963-X 검색 결과 반환<br> 2 : 모지번 확장<br>ex) 963-2 검색 시 96X 검색 결과 반환<br>3 : 법정동 동좌표<br>ex) 삼평동 까지만 입력 되는 경우<br>4 : 동단위 이상 좌표 또는 법정동 좌표<br>ex) 분당구 까지만 입력 되는 경우 |


### 2. 좌표검색(좌표 -> 주소)
- 좌표(TW 좌표/WGS84 좌표)로 주소를 검색합니다.

#### 요청

[URI]

| 메서드 |	URI |
|---|---|
|GET|	/maps/v1.0/appkeys/{appkey}/addresses?query={query}&posX={posX}&posY={posY}&coordtype={coordtype} |

[Path parameter]

| 이름  | 타입 | 필수 여부 | 유효 범위 | 설명 |
|---|---|---|---|---|
| appkey | String | 필수 |  | 고유의 Appkey |

[Query Parameters]

| 이름 | 타입 | 필수 여부 | 유효 범위 |	설명 |
|---|---|---|---|---|
|​ posX |	String | 필수 |  | X좌표 |
| ​posY |	String | 필수 |	 | Y좌표 |
| coordtype |	String | 선택 |  | 요청 좌표형식 <br>0 : TW 좌표<br> 1 : WGS84 좌표<br>미 입력 시 TW 좌표 기준 검색 |

#### 응답

##### 응답 본문

```
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": ""
  },
  "location": {
    "result": true,
    "adm": {
      "posx": "168434",
      "posy": "516700",
      "admcode": "4113511000",
      "address": "경기도 성남시 분당구 백현동",
      "jibun": "519-7",
      "roadname": "",
      "roadjibun": "",
      "distance": 25
    }
  }
}
```

##### 필드

| 이름 | 타입 | 설명 |
|---|---|---|
| header | Object |	헤더 영역 |
| header.isSuccessful |	Boolean |	성공여부 |
| header.resultCode |	Integer |	실패 코드 |
| header.resultMessage | String |	실패 메시지 |
| location | Object |	본문 영역 |
| location.result |	Boolean |	성공여부 |
| location.adm | Object |	검색결과 |
| location.adm.posx | String | X좌표 |
| location.adm.posy | String | Y좌표 |
| location.adm.admcode | String | 행정코드 |
| location.adm.address | String |	주소 |
| location.adm.jibun | String |	지번 |
| location.adm.roadname | String | 새주소 도로명 |
| location.adm.roadjibun | String |	새주소 지번 |
| location.adm.distance | Integer |	좌표와의 거리(해당시에만) |
| location.adm.accuracy | String | 지번 정확도 <br>0 : 정확 검색<br> 1 : 호지번 확장<br>ex) 963-2 검색 시 963-X 검색 결과 반환<br> 2 : 모지번 확장<br>ex) 963-2 검색 시 96X 검색 결과 반환<br>3 : 법정동 동좌표<br>ex) 삼평동 까지만 입력 되는 경우<br>4 : 동단위 이상 좌표 또는 법정동 좌표<br>ex) 분당구 까지만 입력 되는 경우 |



### 3. 통합검색
- 전화번호, 주소, POI 정보 등 통합정보를 검색합니다.

#### 요청

[URI]

| 메서드 |	URI |
|---|---|
|GET|	/maps/v1.0/appkeys/{appkey}/searches&query={query}&coordtype&startposition={startposition}&reqcount={reqcount}&spopt={spopt}&radius={radius}&admcode={admcode}&depth={depth}&x1={x1}&y1={y1}&x2={x2}&y2={y2}&sortopt={sortopt}&catecode={catecode} |

[Path parameter]

| 이름  | 타입 | 필수 여부 | 유효 범위 | 설명 |
|---|---|---|---|---|
| appkey | String | 필수 |  | 고유의 Appkey |

[Query Parameters]

| 이름 | 타입 | 필수 여부 | 유효 범위 |	설명 |
|---|---|---|---|---|
|​ query | String | 필수 |  | 검색어 |
| coordtype |	String | 선택 |  | 좌표형식 <br>0 : TW 좌표<br> 1 : WGS84 좌표<br> 2 : TM 좌표 |
| startposition |	String | 선택 |  | 검색 시작 위치 <br>0 : 첫번째 위치, 미입력 시 0으로 조회 |
| reqcount | String | 선택 |  | 검색 요청 개수 <br>0으로 설정 시 Max Count 반환 |
| spopt |	String | 선택 |  | 공간검색 option <br>0 : 공간검색 사용 안함<br>1 : Extent 검색<br>2 : Range 검색 *spopt값이 설정되지 않은 경우 0으로 설정 |
| radius | String | 선택 |  | 반경 <br>spopt가 2인 경우 사용 Meter 단위 |
| admcode |	String | 선택 |  | 행정코드 |
| depth |	String | 선택 |  | 하위시설물 요구 depth <br>1 : 1 depth 만 요청(최상위 depth)<br>2 : 2 depth 까지 요청<br> 3 : 3 depth 까지 요청 *depth값이 설정되지 않은 경우 1로 설정<br>* depth 설정 시 아래 Response 처럼 subpoi 상세 정보가 depth에 맞게 반환됨 |
| x1 | String | 선택 |  | X1좌표 <br>spopt가 0인 경우 기준점 X좌표<br> spopt가 1인 경우 Extent의 좌상단 X좌표<br> spopt가 2인 경우 기준점 X좌표 |
| y1 | String | 선택 |  |	Y1좌표 <br>spopt가 0인 경우 기준점 Y좌표<br> spopt가 1인 경우 Extent의 좌상단 Y좌표<br> spopt가 2인 경우 기준점 Y좌표 |
| x2 | String | 선택 |  |	X2좌표 <br>spopt가 1인 경우 Extent의 우하단 X좌표, spopt가 2인 경우 사용 안함 |
| y2 | String | 선택 |	| Y2좌표 <br>spopt가 1인 경우 Extent의 우하단 Y좌표, spopt가 2인 경우 사용 안함 |
| sortopt |	String | 선택 |	 | 정렬option <br>1 : 명칭순 정렬<br> 2 : 거리순 정렬 (좌표를 입력한 경우)<br> 3 : 이름매치->거리순 정렬(좌표를 입력한 경우)<br> 4 : 검색어 Weight 정렬 (엔진기준)<br> 5 : 검색어 Weight 정렬 + length(엔진기준)<br> 6 : 선호카테고리 우선 정렬[V8.1.5 미지원]<br>7 : 최신데이터 순 정렬<br> 8 : 검색어 Weight 정렬(Landmark>거리>PoiWeight) + 거리순(좌표를 입력한 경우)<br> *sortopt값이 설정되지 않은 경우 4로설정 |
| catecode | String | 선택 |  | 선호 카테고리 <br>- 선호 카테고리 검색 시 검색어에 카테고리 명칭을 입력한 경우, 검색어 우선 정책에 의해 입력한 선호 카테고리보다 검색어를 기준으로 검색 됨<br>ex) 검색어 : "미용실" , 선호 카테고리 : "100000"(음식점) -> 미용실 기준으로 검색 됨 |

#### 응답

##### 응답 본문

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    },
    "search": {
        "result": true,
        "type": 0,
        "totalcount": 1,
        "count": 1,
        "poitotalcount": 1,
        "poicount": 1,
        "ucp_poitotalcount": 0,
        "ucp_poicount": 0,
        "tel_poitotalcount": 0,
        "tel_poicount": 0,
        "admtotalcount": 0,
        "admcount": 0,
        "reftotalcount": 0,
        "refcount": 0,
        "res_type": "YYYY",
        "poi": [
            {
                "poiid": 4722977,
                "depth": 0,
                "dpx": "169031",
                "dpy": "517906",
                "rpx": "169039",
                "rpy": "517941",
                "name1": "삼환하이펙스",
                "name2": "하이펙스",
                "name3": "삼환하이팩스",
                "name4": "하이팩스",
                "admcode": "4113510900",
                "jibun": "678",
                "address": "경기도 성남시 분당구 삼평동",
                "roadname": "경기도 성남시 분당구 판교역로",
                "roadjibun": "240",
                "detailaddress": "",
                "catecode": "130301",
                "catename": "기업",
                "dp_catecode": "150",
                "userid": "",
                "imagecount": 0,
                "userimagecount": 0,
                "badgeflag": false,
                "distance": 0,
                "tel": "",
                "islandmark": false,
                "updateTS": "2017-10-12 00:00:00",
                "data_source": "Thinkware",
                "hasoildata": false,
                "hasdetailinfo": false,
                "hassubpoi": true,
                "subpoi": {
                    "count": 5,
                    "poi": [
                        {
                            "poiid": 4828295,
                            "depth": 1,
                            "dpx": "169031",
                            "dpy": "517910",
                            "rpx": "169039",
                            "rpy": "517941",
                            "name1": "A동",
                            "name2": "삼환하이팩스A동",
                            "name3": "",
                            "name4": "",
                            "admcode": "4113510900",
                            "jibun": "678",
                            "address": "경기도 성남시 분당구 삼평동",
                            "roadname": "경기도 성남시 분당구 판교역로",
                            "roadjibun": "240",
                            "detailaddress": "",
                            "catecode": "130301",
                            "catename": "기업",
                            "dp_catecode": "150",
                            "userid": "",
                            "imagecount": 0,
                            "userimagecount": 0,
                            "badgeflag": false,
                            "distance": 0,
                            "tel": "",
                            "islandmark": false,
                            "updateTS": "2017-10-13 00:00:00",
                            "hasoildata": false,
                            "hasdetailinfo": false,
                            "hassubpoi": true,
                            "subpoi": {
                                "count": 36,
                                "poi": [
                                    {
                                        "poiid": 4722978,
                                        "depth": 2,
                                        "dpx": "169039",
                                        "dpy": "517941",
                                        "rpx": "169039",
                                        "rpy": "517941",
                                        "name1": "입구",
                                        "name2": "",
                                        "name3": "",
                                        "name4": "",
                                        "admcode": "4113510900",
                                        "jibun": "678",
                                        "address": "경기도 성남시 분당구 삼평동",
                                        "roadname": "",
                                        "roadjibun": "",
                                        "detailaddress": "",
                                        "catecode": "181100",
                                        "catename": "도로시설",
                                        "dp_catecode": "000",
                                        "userid": "",
                                        "imagecount": 0,
                                        "userimagecount": 0,
                                        "badgeflag": false,
                                        "distance": 0,
                                        "tel": "",
                                        "islandmark": false,
                                        "updateTS": "2017-10-13 00:00:00",
                                        "hasoildata": false,
                                        "hasdetailinfo": false,
                                        "hassubpoi": false
                                    },
		....
		]
	}
}
```

##### 필드

| 이름 | 타입 | 설명 |
|---|---|---|
| header | Object |	헤더 영역 |
| header.isSuccessful |	Boolean |	성공여부 |
| header.resultCode |	Integer |	실패 코드 |
| header.resultMessage | String |	실패 메시지 |
| search |	Object | 본문 영역 |
| search.result |	Boolean |	성공여부 |
| search.type |	Integer |	0 : 일반 검색<br> 1 : Reference 검색 |
| search.totalcount |	Integer |	전체 검색결과 대상 개수 |
| search.count | Integer | 검색 결과 개수 |
| search.poitotalcount | Integer | 전체 검색결과 대상 개수(Thinkware POI) |
| search.poicount |	Integer | 검색 결과 개수(Thinkware POI) |
| search.tel_poitotalcount | Integer | 전체 검색결과 대상 개수(Tel POI) |
| search.tel_poicount |	Integer | 검색 결과 개수(Tel POI) |
| search.ucp_poitotalcount | Integer | 전체 검색결과 대상 개수(User POI) |
| search.ucp_poicount |	Integer | 검색 결과 개수(User POI) |
| search.admtotalcount | Integer | adm 전체 검색결과 대상 개수 |
| search.admcount |	Integer | adm 검색 결과 개수 |
| search.reftotalcount | Integer | ref 전체 검색결과 대상 개수 |
| search.refcount |	Integer | ref 검색 결과 개수 |
| search.recommendedQuery |	String | 검색결과가 없는 경우 오타보정 결과 제공(NULL가능) |
| search.recommendedCost | Integer | 오타보정 결과 Cost(0~10000) |
| search.res_type |	String | 검색결과Type명칭 <br>명칭, 카테고리, 주소, 전화번호 순 <br>(ex) NYNN : 명칭 No, 카테고리 YES, 주소 NO, 전화번호 NO |
| search.poi | Array | POI 검색 결과 리스트 |
| search.poi[0].poiid |	Integer | POI ID |
| search.poi[0].depth |	String | POI depth |
| search.poi[0].dpx |	String | display X좌표(WGS84의 경우 longitude) |
| search.poi[0].dpy |	String | display Y좌표(WGS84의 경우 latitude) |
| search.poi[0].rpx |	String| 탐색 X좌표(WGS84의 경우 longitude) |
| search.poi[0].rpy |	String | 탐색 Y좌표(WGS84의 경우 latitude) |
| search.poi[0].name1 |	String | 정식명칭 |
| search.poi[0].name2 |	String | 축약명칭 |
| search.poi[0].name3 |	String | 확장명칭1 |
| search.poi[0].name4 |	String | 확장명칭2 |
| search.poi[0].admcode |	String | 행정코드 |
| search.poi[0].address |	String | 주소 |
| search.poi[0].jibun |	String | 지번 |
| search.poi[0].roadname | String | 새주소 도로명 |
| search.poi[0].roadjibun |	String | 새주소 지번 |
| search.poi[0].detailaddress |	String | 상세주소 |
| search.poi[0].catecode | String | 분류코드 |
| search.poi[0].catename | String | 분류명칭 |
| search.poi[0].dp_catecode |	String | DP 분류코드 |
| search.poi[0].distance | Integer | 좌표와의 거리(해당시에만) |
| search.poi[0].tel |	String | 전화번호 |
| search.poi[0].hasoildata | Boolean | 유가 데이터 존재여부 |
| search.poi[0].hasdetailinfo |	Boolean | 상세정보 존재여부 |
| search.poi[0].hassubpoi |	Boolean | 하위시설물 존재여부 |
| search.poi[0].adv_count |	Integer | 광고코드 개수 |
| search.poi[0].islandmark | Boolean | 랜드마크 여부 |
| search.poi[0].updateTS | String | 최종변경 일시 (Y4-MM-DD HH:mm:ss)포맷 |
| search.poi[0].data_source |	String | POI 생성 정보 구분 (Thinkware/Tel/User) |
| search.poi[0].badgeflag |	Boolean | Badge 유무(Not Yet : FALSE, Badged : TRUE) |
| search.poi[0].userid | String | POI 등록 사용자 ID (UCP인 경우에만) |
| search.poi[0].imagecount | Integer | POI 이미지 개수 |
| search.poi[0].oildata | Object | 유가 데이터 정보 |
| search.poi[0].oildata.g_price | Integer | 휘발유 가격 |
| search.poi[0].oildata.hg_price | Integer | 고급휘발유 가격 |
| search.poi[0].oildata.d_price | Integer | 경유 가격 |
| search.poi[0].oildata.l_price | Integer | LPG 가격 |
| search.poi[0].oildata.updatetime | String | Update 시간 |
| search.poi[0].oildata.priceinfo | String | 최고, 최저 유가 정보<br>(H : 최고, L : 최저, X : 해당없음)<br>휘발유, 고급휘발유, 경유, LPG 순 |
| search.poi[0].oildata.wash | Boolean | 세차시설여부 |
| search.poi[0].oildata.fix | Boolean | 정비가능여부 |
| search.poi[0].oildata.mart | Boolean | 매점여부 |
| search.poi[0].AdInfo | Array | 광고제공업체 광고 코드 |
| search.poi[0].AdInfo.ADCODE | Integer | 광고코드<br>1 ~ 99까지 부여가능(최대99개) |
| search.poi[0].subpoi | Object | 하위 시설물 정보 |
| search.poi[0].subpoi.count | Integer | 하위 시설물 개수 |
| search.poi[0].subpoi.poi | Array | POI 정보와 동일 |
| search.tel | Array | TEL 검색 결과 리스트 (POI 정보와 동일) |
| search.ucp | Array | UCP 검색 결과 리스트 (POI 정보와 동일) |
| search.adm | Array | ADM 검색 결과 리스트 |
| search.adm[0].type | String | 검색 type <br>1 : 행정계 검색<br> 2 : 지번 검색<br>3 : 새주소 검색 |
| search.adm[0].posx | String | X좌표(WGS84의 경우 longitude) |
| search.adm[0].posy | String | Y좌표(WGS84의 경우 latitude) |
| search.adm[0].admcode | String | 행정코드 |
| search.adm[0].address | String |	주소 |
| search.adm[0].jibun | String |	지번 |
| search.adm[0].roadname | String | 새주소 도로명 |
| search.adm[0].roadjibun | String |	새주소 지번 |
| search.adm[0].accuracy | Integer |	지번 정확도 <br>0 : 정확 검색<br> 1 : 호지번 확장<br> 2 : 모지번 확장 |
| search.hasgasstation | Boolean | oilprice 정보 제공 여부 |
| search.oilprice | Object | 유가정보 |
| search.oilprice.max_g_price | Integer | 최고 휘발유 가격 |
| search.oilprice.min_g_price | Integer | 최저 휘발유 가격 |
| search.oilprice.avg_g_price | Integer | 평균 휘발유 가격 |
| search.oilprice.max_hg_price | Integer | 최고 고급 휘발유 가격 |
| search.oilprice.min_hg_price | Integer | 최저 고급 휘발유 가격 |
| search.oilprice.avg_hg_price | Integer | 평균 고급 휘발유 가격 |
| search.oilprice.max_d_price | Integer | 최고 경유 가격 |
| search.oilprice.min_d_price | Integer | 최저 경유 가격 |
| search.oilprice.avg_d_price | Integer | 평균 경유 가격 |
| search.oilprice.max_l_price | Integer | 최고 LPG 가격 |
| search.oilprice.min_l_price | Integer | 최저 LPG 가격 |
| search.oilprice.avg_l_price | Integer | 평균 LPG 가격 |

### 4. 추천어 검색
- 검색어의 추천어를 검색합니다.

#### 요청

[URI]

| 메서드 |	URI |
|---|---|
|GET|	/maps/v1.0/appkeys/{appkey}/proposers?query={query} |

[Path parameter]

| 이름  | 타입 | 필수 여부 | 유효 범위 | 설명 |
|---|---|---|---|---|
| appkey | String | 필수 |  | 고유의 Appkey |

[Query Parameters]

| 이름 | 타입 | 필수 여부 | 유효 범위 |	설명 |
|---|---|---|---|---|
|​ query | String | 필수 | 50Byte | 한글/영문/숫자 50Byte(한글 25자) |


#### 응답

##### 응답 본문

```
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": ""
  },
  "proposer": {
    "result": true,
    "count": 10,
    "keyword": [
      {
        "keyword": "판교역",
        "frequency": 3729938
      },
      {
        "keyword": "판교",
        "frequency": 3729326
      },
      {
        "keyword": "판교IC",
        "frequency": 3729362
      },
      {
        "keyword": "판교도서관",
        "frequency": 3729514
      },
      {
        "keyword": "판교원마을",
        "frequency": 3730051
      },
      {
        "keyword": "판교롯데마트",
        "frequency": 3729602
      },
      {
        "keyword": "판교이노밸리",
        "frequency": 3730186
      },
      {
        "keyword": "판교박물관",
        "frequency": 3729654
      },
      {
        "keyword": "판교중학교",
        "frequency": 3730256
      },
      {
        "keyword": "판교메리어트",
        "frequency": 3729626
      }
    ]
  }
}
```

##### 필드

| 이름 | 타입 | 설명 |
|---|---|---|
| header | Object |	헤더 영역 |
| header.isSuccessful |	Boolean |	성공여부 |
| header.resultCode |	Integer |	실패 코드 |
| header.resultMessage | String |	실패 메시지 |
| proposer | Object |	본문 영역 |
| proposer.result |	Boolean |	성공 여부 |
| proposer.count | Integer | 추천 검색어 개수 |
| proposer.keyword | Array | 추천 검색어 리스트 |
| proposer.keyword[0].keyword |	String | 추천 검색어 |
| proposer.keyword[0].frequency |	Integer |	조회 빈도 |


### 5. POI 상세 검색
- POI에 대한 상세 정보를 검색합니다.

#### 요청

[URI]

| 메서드 |	URI |
|---|---|
|GET|	/maps/v1.0/appkeys/{appkey}/pois?poiid={poiid} |

[Path parameter]

| 이름  | 타입 | 필수 여부 | 유효 범위 | 설명 |
|---|---|---|---|---|
| appkey | String | 필수 |  | 고유의 Appkey |

[Query Parameters]

| 이름 | 타입 | 필수 여부 | 유효 범위 |	설명 |
|---|---|---|---|---|
|​ poiid | String | 필수 | 186개 | POI ID<br>poiid를 구분자 ","와 함께 입력<br>(복수개 가능 186개까지) <br>ex) poiid=123,234,567 |


#### 응답

##### 응답 본문

```
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": ""
  },
  "poi": {
    "result": true,
    "totalcount": 2,
    "count": 2,
    "poiinfo": [
      {
        "poiid": 510835,
        "dpx": "164939",
        "dpy": "530708",
        "rpx": "164929",
        "rpy": "530731",
        "name1": "현대백화점(무역센터점)",
        "name2": "현대백화점무역센터점",
        "name3": "무역센터현대백화점",
        "name4": "",
        "admcode": "1168010500",
        "jibun": "159-7",
        "address": "서울특별시 강남구 삼성동",
        "roadname": "서울특별시 강남구 삼성동 테헤란로",
        "roadjibun": "517",
        "detailaddress": "",
        "fulladdress": "서울특별시 강남구 삼성동 159-7 ",
        "zip": "",
        "homepage": "http://www.e-hyundai.com",
        "email": "",
        "howtogo": "",
        "tel1": "025522233",
        "tel2": "",
        "fax1": "",
        "fax2": "",
        "catecode": "110102",
        "catename": "쇼핑",
        "dp_catecode": "250",
        "icode": "493-070-3606",
        "externallink": [],
        "detail_count": 10,
        "etc_count": 2,
        "imagecount": 0,
        "badgeflag": false,
        "detailinfo": [
          {
            "name": "휴무일",
            "value": "매월 2회휴무"
          },
          {
            "name": "영업시간",
            "value": "10:30~20:00"
          },
          {
            "name": "주차",
            "value": "1400여대 가능"
          },
          {
            "name": "주차료",
            "value": "1만원이상 구매시 1시간 무료"
          },
          {
            "name": "부대시설1",
            "value": "에메랄드홀(이벤트홀)"
          },
          {
            "name": "부대시설2",
            "value": "테라스가든"
          },
          {
            "name": "규모",
            "value": "지상10층 지하 4층"
          },
          {
            "name": "층별정보1",
            "value": "1층 명품잡화/2층 패션잡화"
          },
          {
            "name": "층별정보2",
            "value": "3~4층 여성의류/6층 골프유니캐주얼"
          },
          {
            "name": "층별정보3",
            "value": "9층 식당가/10층 문화의 광장"
          }
        ],
        "etcinfo": [
          {
            "name": "기타1",
            "value": "금융 중심지인 테헤란로의 심장부에 위치"
          },
          {
            "name": "기타2",
            "value": "전세계에서 한국을 찾아온 고객들을 만족시킬 수 있는 한국 유통의 쇼윈도우"
          }
        ],
        "hasoildata": false
      },
      ....
    ]
  }
}
```

##### 필드

| 이름 | 타입 | 설명 |
|---|---|---|
| header | Object |	헤더 영역 |
| header.isSuccessful |	Boolean |	성공여부 |
| header.resultCode |	Integer |	실패 코드 |
| header.resultMessage | String |	실패 메시지 |
| poi |	Object | 본문 영역 |
| poi.result | Boolean | 성공여부 |
| poi.totalcount | Integer | 전체 검색결과 대상 개수 |
| poi.count |	Integer |	검색 결과 개수 |
| poi.poiinfo |	Array | POI 검색 결과 리스트 |
| poi.poiinfo[0].poiid | Integer | POI ID |
| poi.poiinfo[0].dpx | String | display X좌표(WGS84의 경우 longitude) |
| poi.poiinfo[0].dpy | String | display Y좌표(WGS84의 경우 latitude) |
| poi.poiinfo[0].rpx | String | 탐색 X좌표(WGS84의 경우 longitude) |
| poi.poiinfo[0].rpy | String | 탐색 Y좌표(WGS84의 경우 latitude) |
| poi.poiinfo[0].name1 | String | 정식명칭 |
| poi.poiinfo[0].name2 | String | 축약명칭 |
| poi.poiinfo[0].name3 | String | 확장명칭1 |
| poi.poiinfo[0].name4 | String | 확장명칭2 |
| poi.poiinfo[0].admcode | String | 행정코드|
| poi.poiinfo[0].jibun | String | 지번 |
| poi.poiinfo[0].address | String | 주소 |
| poi.poiinfo[0].roadname | String | 새주소 도로명 |
| poi.poiinfo[0].roadjibun | String | 새주소 지번 |
| poi.poiinfo[0].detailaddress | String | 상세주소 |
| poi.poiinfo[0].catecode | String | 분류코드 |
| poi.poiinfo[0].catename | String | 분류명칭 |
| poi.poiinfo[0].fulladdress | String | 전체주소(행정주소+지번+상세주소) |
| poi.poiinfo[0].zip | String | 우편번호 |
| poi.poiinfo[0].homeage | String | 홈페이지 url |
| poi.poiinfo[0].email | String | email |
| poi.poiinfo[0].howtogo | String | 교통편 |
| poi.poiinfo[0].tel1 | String | 전화번호1 |
| poi.poiinfo[0].tel2 | String | 전화번호2 |
| poi.poiinfo[0].fax1 | String | 팩스번호1 |
| poi.poiinfo[0].fax2 | String | 팩스번호2 |
| poi.poiinfo[0].icode | String | ICODE |
| poi.poiinfo[0].detail_count | Integer | 분류상세항목개수 |
| poi.poiinfo[0].etc_count | Integer | 분류기타항목개수 |
| poi.poiinfo[0].badgeflag | Boolean | Badge 유무(Not Yet:FALSE, Badged:TRUE) |
| poi.poiinfo[0].imagecount | Integer | POI 이미지 개수 |
| poi.poiinfo[0].hasoildata | Boolean | 유가 데이터 존재 유무 |
| poi.poiinfo[0].detailinfo | Array | 분류상세항목 |
| poi.poiinfo[0].detailinfo[0].name | String | 분류상세항목설명 |
| poi.poiinfo[0].detailinfo[0].value | String | 분류상세항목내용 |
| poi.poiinfo[0].etcinfo | Array | 분류기타항목 |
| poi.poiinfo[0].etcinfo[0].name | String | 분류기타항목설명 |
| poi.poiinfo[0].etcinfo[0].value | String | 분류기타항목내용 |
| poi.poiinfo[0].oildata | Object | 유가 데이터 정보 |
| poi.poiinfo[0].oilda.tag_price | Integer | 휘발유 가격 |
| poi.poiinfo[0].oilda.hg_price | Integer | 고급휘발유 가격 |
| poi.poiinfo[0].oilda.d_price | Integer | 경유 가격 |
| poi.poiinfo[0].oilda.l_price | Integer | LPG 가격 |
| poi.poiinfo[0].oilda.updatetime | String | Update 시간 |
| poi.poiinfo[0].oilda.priceinfo | String | 최고, 최저 유가 정보<br>(H : 최고, L : 최저, X : 해당없음)<br>휘발유, 고급휘발유, 경유, LPG 순 |
| poi.poiinfo[0].oilda.wash | Boolean | 세차시설여부 |
| poi.poiinfo[0].oilda.fix | Boolean | 정비가능여부 |
| poi.poiinfo[0].oilda.mart | Boolean | 매점여부 |

### 6. POI 하위 시설물 검색
- 특정 POI에 대한 하위 시설물을 검색합니다.

#### 요청

[URI]

| 메서드 |	URI |
|---|---|
|GET|	/maps/v1.0/appkeys/{appkey}/sub-pois?poiid={poiid}&x1={x1}&y1={y1} |

[Path parameter]

| 이름  | 타입 | 필수 여부 | 유효 범위 | 설명 |
|---|---|---|---|---|
| appkey | String | 필수 |  | 고유의 Appkey |

[Query Parameters]

| 이름 | 타입 | 필수 여부 | 유효 범위 |	설명 |
|---|---|---|---|---|
|​ poiid | String |	필수 |  | POI ID<br>복수개 지원 안됨 |
| ​x1 |	String | 선택 | 현위치 또는 지도중심좌표<br>x, y좌표가 모두 NULL 또는 0일 경우 거리 계산을 수행하지 않음 |
| ​y1 |	String | 선택 | 현위치 또는 지도중심좌표<br>x, y좌표가 모두 NULL 또는 0일 경우 거리 계산을 수행하지 않음 |

#### 응답

##### 응답 본문

```
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": ""
  },
  "subpoi": {
    "result": true,
    "totalcount": 5,
    "count": 5,
    "poi": [
      {
        "poiid": 4521976,
        "depth": 1,
        "dpx": "169172",
        "dpy": "517030",
        "rpx": "169172",
        "rpy": "517030",
        "name1": "환승주차장",
        "name2": "",
        "name3": "",
        "name4": "",
        "admcode": "4113511000",
        "jibun": "",
        "address": "경기도 성남시 분당구 백현동",
        "roadname": "",
        "roadjibun": "",
        "detailaddress": "",
        "catecode": "161701",
        "catename": "주차장",
        "dp_catecode": "360",
        "userid": "",
        "imagecount": 0,
        "userimagecount": 0,
        "badgeflag": false,
        "distance": 0,
        "tel": "",
        "islandmark": false,
        "updateTS": "1970-01-01 09:00:00",
        "hasoildata": false,
        "hasdetailinfo": false,
        "hassubpoi": false
      },
      {
        "poiid": 4521977,
        "depth": 1,
        "dpx": "169088",
        "dpy": "517090",
        "rpx": "169088",
        "rpy": "517090",
        "name1": "1번출구",
        "name2": "",
        "name3": "",
        "name4": "",
        "admcode": "4113511000",
        "jibun": "",
        "address": "경기도 성남시 분당구 백현동",
        "roadname": "",
        "roadjibun": "",
        "detailaddress": "",
        "catecode": "173000",
        "catename": "지하철",
        "dp_catecode": "370",
        "userid": "",
        "imagecount": 0,
        "userimagecount": 0,
        "badgeflag": false,
        "distance": 0,
        "tel": "",
        "islandmark": false,
        "updateTS": "1970-01-01 09:00:00",
        "hasoildata": false,
        "hasdetailinfo": false,
        "hassubpoi": false
      },
      ...
    ]
  }
}
```

##### 필드

| 이름 | 타입 | 설명 |
|---|---|---|
| header | Object |	헤더 영역 |
| header.isSuccessful |	Boolean |	성공여부 |
| header.resultCode |	Integer |	실패 코드 |
| header.resultMessage | String |	실패 메시지 |
| subpoi | Object |	본문 영역 |
| subpoi.result |	Boolean |	성공여부 |
| subpoi.totalcount |	String | 전체 검색결과 대상 개수 |
| subpoi.count | String |	검색 결과 개수 |
| subpoi.poi | Array | POI 검색 결과 리스트 |
| subpoi.poi[0].poiid | Integer | POI ID |
| subpoi.poi[0].depth | String | POI depth |
| subpoi.poi[0].dpx | String | display X좌표(WGS84의 경우 longitude) |
| subpoi.poi[0].dpy | String | display Y좌표(WGS84의 경우 latitude) |
| subpoi.poi[0].rpx | String | 탐색 X좌표(WGS84의 경우 longitude) |
| subpoi.poi[0].rpy | String | 탐색 Y좌표(WGS84의 경우 latitude) |
| subpoi.poi[0].name1 | String | 정식명칭 |
| subpoi.poi[0].name2 | String | 축약명칭 |
| subpoi.poi[0].name3 | String | 확장명칭1 |
| subpoi.poi[0].name4 | String | 확장명칭2 |
| subpoi.poi[0].admcode | String | 행정코드 |
| subpoi.poi[0].address | String | 주소 |
| subpoi.poi[0].jibun | String | 지번 |
| subpoi.poi[0].roadname | String | 새주소 도로명 |
| subpoi.poi[0].roadjibun | String | 새주소 지번 |
| subpoi.poi[0].detailaddress | String | 상세주소 |
| subpoi.poi[0].catecode | String | 분류코드 |
| subpoi.poi[0].catename | String | 분류명칭 |
| subpoi.poi[0].dp_catecode | String | DP 분류코드 |
| subpoi.poi[0].distance | Integer | 좌표와의 거리(해당시에만) |
| subpoi.poi[0].tel | String | 전화번호 |
| subpoi.poi[0].hasoildata | Boolean | 유가 데이터 존재 여부 |
| subpoi.poi[0].hasdetailinfo | Boolean | 상세정보 존재 여부 |
| subpoi.poi[0].hassubpoi | Boolean | 하위시설물 존재여부 |
| subpoi.poi[0].adv_count | Boolean | 광고코드 개수 |
| subpoi.poi[0].islandmark | Boolean | 랜드마크 여부 |
| subpoi.poi[0].updateTS | String | 최종변경 일시(Y4-MM-DD HH:mm:ss)포맷 |
| subpoi.poi[0].data_source | String | POI 생성 정보 구분 (Thinkware/Tel/User) |
| subpoi.poi[0].badgeflag | Boolean | Badge 유무(Not Yet : FALSE, Badged : TRUE) |
| subpoi.poi[0].userid | String | POI 등록 사용자 ID (UCP인 경우에만) |
| subpoi.poi[0].imagecount | Integer | POI 이미지 개수 |
| subpoi.poi[0].oildata | Object | 유가 데이터 정보 |
| subpoi.poi[0].oildata.g_price | Integer | 휘발유 가격 |
| subpoi.poi[0].oildata.hg_price | Integer | 고급휘발유 가격 |
| subpoi.poi[0].oildata.d_price | Integer | 경유 가격 |
| subpoi.poi[0].oildata.l_price | Integer | LPG 가격 |
| subpoi.poi[0].oildata.updatetime | String | Update 시간 |
| subpoi.poi[0].oildata.priceinfo | String | 최고, 최저 유가 정보<br>(H : 최고, L : 최저, X : 해당없음)<br>휘발유, 고급휘발유, 경유, LPG 순 |
| subpoi.poi[0].oildata.wash | Boolean | 세차시설여부 |
| subpoi.poi[0].oildata.fix | Boolean | 정비가능여부 |
| subpoi.poi[0].oildata.mart | Boolean | 매점여부 |
| subpoi.poi[0].AdInfo | Array | 광고코드 리스트 |
| subpoi.poi[0].AdInfo[0].ADCODE | Integer |광고코드<br>1 ~ 99까지 부여가능(최대99개) |
| subpoi.poi[0].subpoi | Object | 하위 시설물 정보 |
| subpoi.poi[0].subpoi.count | Integer | subpoi 개수 |
| subpoi.poi[0].subpoi.poi | Array | POI 정보와 동일 |

### 7\. 좌표변환

* WGS84 <-> TM 좌표간 변환값을 반환합니다.

#### 요청

[URI]

| 메서드 | URI |
| --- | --- |
| GET | /maps/v1.0/appkeys/{appkey}/trans-coordinates?coordtype={coordtype}&x={x}&y={y}|

[Path parameter]

| 이름 | 타입 | 필수 여부 | 유효 범위 | 설명 |
| --- | --- | ----- | ----- | --- |
| appkey | String | 필수 |  | 고유의 Appkey |

[Query Parameters]

| 이름 | 타입 | 필수 여부 | 유효 범위 | 설명 |
| --- | --- | ----- | ----- | --- |
| coordtype | String | 필수 |  | 0 : WGS84 -> TM <br> 1 : TM -> WGS84 |
| x | double | 필수 | 현위치 또는 지도중심좌표<br>WGS84 좌표 혹은 TM 좌표 |  |
| y | double | 필수 | 현위치 또는 지도중심좌표<br>WGS84 좌표 혹은 TM 좌표 |  |

#### 응답

##### 응답 본문

```
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": ""
  },
  "coordinate": {
    "x": 207824.82237863893,
    "y": 431128.41980473,
    "coordtype": "TM"
  }
}
```

##### 필드

| 이름 | 타입 | 설명 |
| --- | --- | --- |
| header | Object | 헤더 영역 |
| header.isSuccessful | Boolean | 성공여부 |
| header.resultCode | Integer | 실패 코드 |
| header.resultMessage | String | 실패 메시지 |
| coordinate| Object | 본문 영역 |
| coordinate.x | Double | 변환x좌표 |
| coordinate.y | Double | 변환y좌표 |
| coordinate.coordtype | String | 변환좌표형태 |

## 탐색

### 1. 경로 탐색 요약
- 입력한 좌표들에 대한 경로 탐색 결과 요약 정보를 검색합니다.

#### 요청

[URI]

| 메서드 |	URI |
|---|---|
|GET|	/maps/v1.0/appkeys/{appkey}/routes?startX={startX}&startY={startY}&endX={endX}&endY={endY}&viaCount={viaCount}&via1X={via1X}&via1Y={via1Y}&via2X={via2X}&via2Y={via2Y}&option={option} |

[Path parameter]

| 이름  | 타입 | 필수 여부 | 유효 범위 | 설명 |
|---|---|---|---|---|
| appkey | String | 필수 |  | 고유의 Appkey |

[Query Parameters]

| 이름 | 타입 | 필수 여부 | 유효 범위 |	설명 |
|---|---|---|---|---|
| ​startX | String | 필수 |  | 출발지 X좌표 |
| ​startY | String | 필수 |  | 출발지 Y좌표 |
| ​endX | String | 필수 |  | 도착지 X좌표 |
| ​endY | String | 필수 | | 도착지 Y좌표 |
| ​viaCount | String | 선택 |  | 경유지 개수 |
| ​via1X | String | 선택 |  | 경유지1 X좌표 |
| ​via1Y | String | 선택 |  | 경유지1 Y좌표 |
| ​via2X | String | 선택 |  | 경유지2 X좌표 |
| ​via2Y | String | 선택 |  | 경유지2 Y좌표 |
| ​option | String | 필수 |  | 경로탐색 옵션<br>탐색 option "," 단위로 요청<br>ex) option=real_traffic,real_traffic2<br>freeroad_priority : 무료<br>highway_priority : 고속도로<br>real_traffic : 실시간<br>real_traffic_freeroad : 실시간 (무료)<br>real_traffic : 추천1<br>real_traffic2 : 추천2<br>rt_stats : 실시간통계<br>rt_stats_freeroad : 실시간통계(무료)<br>short_distance_priority : 단거리<br>stats : 통계<br>stats_freeroad : 통계(무료)<br>motorcycle : 이륜차 |

#### 응답

##### 응답 본문

```
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": ""
  },
  "route": {
    "SummaryResult": [
      [
        "freeroad_priority",
        68418,
        122
      ],
      [
        "highway_priority",
        77303,
        89
      ],
      [
        "real_traffic",
        63641,
        94
      ],
      [
        "real_traffic_freeroad",
        64469,
        119
      ],
      [
        "recoomendation1",
        4294967295,
        0
      ],
      ...
    ]
  }
}
```

##### 필드

| 이름 | 타입 | 설명 |
|---|---|---|
| header | Object |	헤더 영역 |
| header.isSuccessful |	Boolean |	성공여부 |
| header.resultCode |	Integer |	실패 코드 |
| header.resultMessage | String |	실패 메시지 |
| route |	Object | 본문 영역 |
| route.SummaryResult |	Array |	요청 경로 결과 리스트 |
| route.SummaryResult[0].0 | String |	옵션 명 |
| route.SummaryResult[0].1 | Integer | 경로 탐색 거리 (단위 : m) |
| route.SummaryResult[0].2 | Integer | 경로 탐색 시간 (단위 : 분) |

### 2. 경로 탐색 상세
- 입력한 좌표들에 대한 경로 탐색 결과 상세 정보를 검색합니다.

#### 요청

[URI]

| 메서드 |	URI |
|---|---|
|GET|	/maps/v1.0/appkeys/{appkey}/route-details?startX={startX}&startY={startY}&endX={endX}&endY={endY}&viaCount={viaCount}&via1X={via1X}&via1Y={via1Y}&via2X={via2X}&via2Y={via2Y}&option={option} |

[Path parameter]

| 이름  | 타입 | 필수 여부 | 유효 범위 | 설명 |
|---|---|---|---|---|
| appkey | String | 필수 |  | 고유의 Appkey |

[Query Parameters]

| 이름 | 타입 | 필수 여부 | 유효 범위 |	설명 |
|---|---|---|---|---|
|​ startX | String | 필수 |  | 출발지 X좌표 |
| ​startY | String | 필수 |  | 출발지 Y좌표 |
| ​endX | String | 필수 |  | 도착지 X좌표 |
| ​endY | String | 필수 |  | 도착지 Y좌표 |
| ​viaCount | String | 선택 |  | 경유지 개수 |
| ​via1X | String | 선택 |  | 경유지1 X좌표 |
| ​via1Y | String | 선택 |  | 경유지1 Y좌표 |
| ​via2X | String | 선택 |  | 경유지2 X좌표 |
| ​via2Y | String | 선택 |  | 경유지2 Y좌표 |
| ​option | String | 필수 |  | 경로탐색 옵션<br>탐색 option 하나만 가능<br>ex) option=real_traffic<br>freeroad_priority : 무료<br>highway_priority : 고속도로<br>real_traffic : 실시간<br>real_traffic_freeroad : 실시간 (무료)<br>real_traffic : 추천1<br>real_traffic2 : 추천2<br>rt_stats : 실시간통계<br>rt_stats_freeroad : 실시간통계(무료)<br>short_distance_priority : 단거리<br>stats : 통계<br>stats_freeroad : 통계(무료)<br>motorcycle : 이륜차 |

#### 응답

##### 응답 본문

```
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": ""
  },
  "routeDetail": {
    "DtlInfoRec": [
      [
        8,
        0,
        0,
        -1,
        -1,
        5,
        1
      ],
      [
        79,
        12,
        1,
        -1,
        -1,
        5,
        2
      ],
      ...
    ],
    "NameRec": [
      "일반도로",
      "판교역로242번길",
      "판교역로226번길",
      "일반도로",
      "대왕판교로644번길",
      "우회전",
      "우회전",
      "우회전",
      "백현동,판교(판교테크노밸리)역"
    ],
    "RestRec": [],
    "RouteInfo": {
      "cross_name_cnt": 0,
      "dir_name_cnt": 1,
      "dist": 456,
      "dtl_cnt": 6,
      "max_x": 169113,
      "max_y": 517952,
      "min_x": 169034,
      "min_y": 517648,
      "rd_name_cnt": 5,
      "rest_cnt": 0,
      "sec_cnt": 5,
      "time": 3,
      "toll_cnt": 0,
      "vtx_cnt": 11
    },
    "SecInfoRec": [
      [
        8,
        0,
        0,
        1,
        0
      ],
      [
        126,
        14,
        1,
        2,
        1
      ],
      ...
    ],
    "VtxRec": [
      [
        169038,
        517943
      ],
      [
        169038,
        517952
      ],
      [
        169109,
        517952
      ],
      ...
    ]
  }
}
```

##### 필드

| 이름 | 타입 | 설명 |
|---|---|---|
| header | Object |	헤더 영역 |
| header.isSuccessful |	Boolean |	성공여부 |
| header.resultCode |	Integer |	실패 코드 |
| header.resultMessage | String |	실패 메시지 |
| routeDetail |	Object | 본문 영역 |
| RouteInfo |	Object | 경로 정보 |
| RouteInfo.dist | Integer | 경로의 총 길이 (단위 : m) |
| RouteInfo.time | Integer | 경로의 총 소요시간 (단위 : 분) |
| RouteInfo.sec_cnt | Integer |	구간정보 레코드 개수 |
| RouteInfo.dtl_cnt | Integer |	구간 상세정보 레코드 개수 |
| RouteInfo.rd_name_cnt | Integer |	도로 명칭 레코드 개수 |
| RouteInfo.guide_name_cnt | Integer | 안내 명칭 레코드 개수 |
| RouteInfo.cross_name_cnt | Integer | 교차로 명칭 레코드 개수 |
| RouteInfo.dir_name_cnt | Integer | 방면 명칭 레코드 개수 |
| RouteInfo.vtx_cnt | Integer |	보간점(경로 벡터 좌표) 개수 |
| RouteInfo.rest_cnt | Integer | 휴게소 개수 |
| RouteInfo.toll_cnt | Integer | 요금소 개수 |
| RouteInfo.max_x | Integer |	보간점 레코드 중 최대 X 좌표 |
| RouteInfo.max_y | Integer |	보간점 레코드 중 최대 Y 좌표 |
| RouteInfo.min_x | Integer |	보간점 레코드 중 최소 X 좌표 |
| RouteInfo.min_y | Integer |	보간점 레코드 중 최소 Y 좌표 |
| SecInfoRec | Array | 구간정보 레코드 |
| SecInfoRec[0].0 |	Integer |	구간의 거리(미터) |
| SecInfoRec[0].1 |	Integer |	구간 속도 |
| SecInfoRec[0].2 |	Integer |	도로번호 혹은 도로 명칭 인덱스 |
| SecInfoRec[0].3 |	String | 구간 상세 정보 레코드 개수 |
| SecInfoRec[0].4 |	String | 구간 상세 정보 테이블 인덱스 |
| DtlInfoRec | Array | 구간상세정보 레코드 |
| DtlInfoRec[0].0 |	Integer |	구간 상세 거리 |
| DtlInfoRec[0].1 |	Integer |	구간 상세 속도 |
| DtlInfoRec[0].2 |	String | 안내명칭 인덱스 |
| DtlInfoRec[0].3 |	String | 교차로명칭 인덱스 |
| DtlInfoRec[0].4 |	String | 방면명칭 인덱스 |
| DtlInfoRec[0].5 |	String | 도로 종별 |
| DtlInfoRec[0].6 |	Integer |	안내지점 보간점 인덱스 |
| NameRec |	Array |	명칭레코드 |
| NameRec[0].0 | String |	고속도로명칭 or 안내명칭 or 교차로명칭 or 방면명칭 |
| VtxRec | Array | 보간점 레코드 - 경로 벡터 좌표 배열<br>[[twX1, twY1], [twX2, twY2], … [twXn, twYn]] |
| VtxRec[0].0 |	Integer |	twX |
| VtxRec[0].1 |	Integer |	twY |
| RestRec |	Array |	명칭레코드 |
| RestRec[0].0 | String |	고속모드 코드 |
| RestRec[0].1 | String |	주유소 업체 코드 <br>(0 : 없음, 1 : LG 주유소, 2 : SK 주유소, 3 : 쌍용 주유소, 4 : 한화 주유소, 5 : 현대 주유소) |
| RestRec[0].2 | String |	LPG 유무 <br>[0 : 없음, 1 : 있음] |
| RestRec[0].3 | String |	정비소 유무 <br>[0 : 없음, 1 : 있음] |
| RestRec[0].4 | String |	고속모드 타입 |
| RestRec[0].5 | String |	Reserved |
| RestRec[0].6 | String |	휴게소 명칭 |

### 3. 경로 탐색 상세(json Parsing)

#### 경로 탐색 결과 값을 보기 쉽게 Parsing

```
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v1.0/route.js" > </script>
<script type="text/javascript">
function fnRouteParse(data){ // 경로 탐색 상세 결과값

  var routeParsing = route.jsonParsing(data);
  routeParsing.routeSummaryInfo;		// 탐색 결과 종합
  routeParsing.routeDetailInfo;		// 탐색 경로 리스트
  routeParsing.vtxInfo; 			// 지도 그리기용 좌표 리스트
}
</script>

```

#### 필드

| 이름 | 타입 | 설명 |
|---|---|---|
| routeSummaryInfo | Object |	탐색 결과 종합 |
| routeSummaryInfo.distance |	Integer |	경로 총길이 (단위 : m) |
| routeSummaryInfo.time |	Integer |	경로의 총 소요시간 (단위 :분) |
| routeSummaryInfo.max_x | String |	보간점 레코드 중 최대 X 좌표 |
| routeSummaryInfo.max_y | String |	보간점 레코드 중 최대 Y 좌표 |
| routeSummaryInfo.min_x | String |	보간점 레코드 중 최소 X 좌표 |
| routeSummaryInfo.min_y | String |	보간점 레코드 중 최소 Y 좌표 |
| routeDetailInfo |	Array |	탐색 경로 리스트 |
| routeDetailInfo.distance | Integer | 구간 상세거리 (단위 : m) |
| routeDetailInfo.speed |	Integer |	구간 상세 속도 (단위 : km/h) |
| routeDetailInfo.roadName | String |	도로명 |
| routeDetailInfo.direction |	String | 방향 정보 |
| routeDetailInfo.district | String |	방면 정보 |
| routeDetailInfo.cross |	String | 안내 정보 |
| routeDetailInfo.directionDetail |	String | 상세 경로 설명 |
| vtxInfo |	Array |	지도 그리기용 좌표 리스트 |
| vtxInfo[0].0 | Integer | twX |
| vtxInfo[0].1 | Integer | twY |
