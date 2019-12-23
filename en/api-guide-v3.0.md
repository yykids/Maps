## Application Service > Maps > API v3.0 Guide

아이나비의 오랜 내비 엔진 기술을 이용한 검색, Geocoding, Reverse Geocoding, 경로 탐색(길찾기), Static Map API 사용에 대해 설명합니다.

## API 공통 정보

### 사전 준비

* API를 사용하려면 앱키가 필요합니다.
* 앱키는 **TOAST Console** 상단 **URL & Appkey** 메뉴에서 확인할 수 있습니다.

### 요청 공통 정보

#### URL 정보

| 환경   | 도메인                              |
| ---- | -------------------------------- |
| Real | https://api-maps.cloud.toast.com |

### 응답 공통 정보

#### 검색 API

* 모든 API 요청에 '200 OK'로 응답합니다. 자세한 응답 결과는 응답 본문의 헤더를 참고합니다.

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

### 1\. 통합검색

* 상호명, 전화번호, 주소 등의 키워드에 대해 통합 정보를 검색합니다.

#### 요청

[URI]

| 메서드  | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/searches&query={query}&coordtype&startposition={startposition}&reqcount={reqcount}&spopt={spopt}&radius={radius}&admcode={admcode}&depth={depth}&x1={x1}&y1={y1}&x2={x2}&y2={y2}&sortopt={sortopt}&catecode={catecode} |

[Path parameter]

| 이름     | 타입     | 필수 여부 | 유효 범위 | 설명     |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 필수    |       | 고유의 앱키 |

[Query Parameters]

| 이름            | 타입     | 필수 여부 | 유효 범위 | 설명                                       |
| ------------- | ------ | ----- | ----- | ---------------------------------------- |
| query         | String | 필수    |       | 검색어                                      |
| coordtype     | String | 선택    |       | 좌표 형식<br>0 : TW 좌표<br>1 : WGS84 좌표<br>2 : TM 좌표 |
| startposition | String | 선택    |       | 검색 시작 위치<br>0 : 첫번째 위치, 미입력 시 0으로 조회     |
| reqcount      | String | 선택    |       | 검색 요청 개수<br>0으로 설정 시 Max Count 반환        |
| spopt         | String | 선택    |       | 공간 검색 옵션<br>0 : 공간 검색 사용 안 함<br>1 : Extent 검색<br>2 : Range 검색<br>* spopt값이 설정되지 않은 경우 0으로 설정 |
| radius        | String | 선택    |       | 반경<br>spopt 값이 2인 경우 사용<br>미터 단위              |
| admcode       | String | 선택    |       | 행정코드                                    |
| depth         | String | 선택    |       | 하위 시설물 요구 수준<br>1 : 1 depth 만 요청(최상위 depth)<br>2 : 2 depth 까지 요청<br>3 : 3 depth 까지 요청<br>* depth값이 설정되지 않은 경우 1로 설정<br>* depth 설정 시 아래 Response 처럼 subpoi 상세 정보가 depth에 맞게 반환됨 |
| x1            | String | 선택    |       | X1좌표<br>spopt 값이 0인 경우 기준점 X 좌표<br>spopt 값이 1인 경우 Extent의 왼쪽 상단 X 좌표<br>spopt 값이 2인 경우 기준점 X 좌표 |
| y1            | String | 선택    |       | Y1좌표<br>spopt 값이 0인 경우 기준점 Y 좌표<br>spopt 값이 1인 경우 Extent의 좌상단 Y 좌표<br>spopt 값이 2인 경우 기준점 Y 좌표 |
| x2            | String | 선택    |       | X2좌표<br>spopt 값이 1인 경우 Extent의 우하단 X 좌표, spopt 값이 2인 경우 사용 안함 |
| y2            | String | 선택    |       | Y2좌표<br>spopt 값이 1인 경우 Extent의 우하단 Y 좌표, spopt 값이 2인 경우 사용 안함 |
| sortopt       | String | 선택    |       | 정렬option<br>1 : 명칭순 정렬<br>2 : 거리순 정렬 (좌표를 입력한 경우)<br>3 : 이름매치->거리순 정렬(좌표를 입력한 경우)<br>4 : 검색어 Weight 정렬 (엔진기준)<br>5 : 검색어 Weight 정렬 + length(엔진기준)<br>6 : 선호카테고리 우선 정렬[V8.1.5 미지원]<br>7 : 최신데이터 순 정렬<br>8 : 검색어 Weight 정렬(Landmark>거리>PoiWeight) + 거리순(좌표를 입력한 경우)<br>* sortopt 값이 설정되지 않은 경우 4로 설정 |
| catecode      | String | 선택    |       | 선호 카테고리<br>선호 카테고리 검색 시 검색어에 카테고리 명칭을 입력한 경우, 검색어 우선 정책에 의해 입력한 선호 카테고리보다 검색어를 기준으로 검색됨<br>예) 검색어 : "미용실" , 선호 카테고리 : "100000"(음식점) -> 미용실 기준으로 검색 됨 |

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

| 이름                               | 타입      | 설명                                       |
| -------------------------------- | ------- | ---------------------------------------- |
| header                           | Object  | 헤더 영역                                    |
| header.isSuccessful              | Boolean | 성공 여부                                    |
| header.resultCode                | Integer | 실패 코드                                    |
| header.resultMessage             | String  | 실패 메시지                                   |
| search                           | Object  | 본문 영역                                    |
| search.result                    | Boolean | 성공 여부                                    |
| search.type                      | Integer | 0 : 일반 검색<br>1 : Reference 검색            |
| search.totalcount                | Integer | 전체 검색 결과 대상 개수                           |
| search.count                     | Integer | 검색 결과 개수                                 |
| search.poitotalcount             | Integer | 전체 검색 결과 대상 개수(Thinkware POI)            |
| search.poicount                  | Integer | 검색 결과 개수(Thinkware POI)                  |
| search.tel_poitotalcount         | Integer | 전체 검색 결과 대상 개수(Tel POI)                  |
| search.tel_poicount              | Integer | 검색 결과 개수(Tel POI)                        |
| search.ucp_poitotalcount         | Integer | 전체 검색 결과 대상 개수(User POI)                 |
| search.ucp_poicount              | Integer | 검색 결과 개수(User POI)                       |
| search.admtotalcount             | Integer | ADM 전체 검색 결과 대상 개수                       |
| search.admcount                  | Integer | ADM 검색 결과 개수                             |
| search.reftotalcount             | Integer | ref 전체 검색 결과 대상 개수                       |
| search.refcount                  | Integer | ref 검색 결과 개수                             |
| search.res_type                  | String  | 검색 결과Type명칭<br>명칭, 카테고리, 주소, 전화번호 순<br>(예) NYNN : 명칭 No, 카테고리 YES, 주소 NO, 전화번호 NO |
| search.poi                       | Array   | POI 검색 결과 목록                             |
| search.poi[0].poiid              | Integer | POI ID                                   |
| search.poi[0].depth              | String  | POI depth                                |
| search.poi[0].dpx                | String  | display X 좌표(WGS84의 경우 longitude)         |
| search.poi[0].dpy                | String  | display Y 좌표(WGS84의 경우 latitude)          |
| search.poi[0].rpx                | String  | 탐색 X 좌표(WGS84의 경우 longitude)              |
| search.poi[0].rpy                | String  | 탐색 Y 좌표(WGS84의 경우 latitude)               |
| search.poi[0].name1              | String  | 정식 명칭                                    |
| search.poi[0].name2              | String  | 축약 명칭                                    |
| search.poi[0].name3              | String  | 확장 명칭 1                                  |
| search.poi[0].name4              | String  | 확장 명칭 2                                  |
| search.poi[0].admcode            | String  | 행정코드                                    |
| search.poi[0].address            | String  | 주소                                       |
| search.poi[0].jibun              | String  | 지번                                       |
| search.poi[0].roadname           | String  | 새주소 도로명                                  |
| search.poi[0].roadjibun          | String  | 새주소 지번                                   |
| search.poi[0].detailaddress      | String  | 상세 주소                                    |
| search.poi[0].catecode           | String  | 분류 코드                                    |
| search.poi[0].catename           | String  | 분류 명칭                                    |
| search.poi[0].dp_catecode        | String  | DP 분류 코드                                 |
| search.poi[0].distance           | Integer | 좌표와의 거리(해당될 때만)                          |
| search.poi[0].tel                | String  | 전화번호                                     |
| search.poi[0].hasoildata         | Boolean | 유가 데이터 존재 여부                             |
| search.poi[0].hasdetailinfo      | Boolean | 상세 정보 존재 여부                              |
| search.poi[0].hassubpoi          | Boolean | 하위 시설물 존재 여부                             |
|| search.poi[0].islandmark         | Boolean | 랜드마크 여부                                  |
| search.poi[0].updateTS           | String  | 최종 변경 일시(Y4-MM-DD HH:mm:ss)포맷            |
| search.poi[0].imagecount         | Integer | POI 이미지 개수                               |
| search.poi[0].oildata            | Object  | 유가 데이터 정보                                |
| search.poi[0].oildata.g_price    | Integer | 휘발유 가격                                   |
| search.poi[0].oildata.hg_price   | Integer | 고급 휘발유 가격                                |
| search.poi[0].oildata.d_price    | Integer | 경유 가격                                    |
| search.poi[0].oildata.l_price    | Integer | LPG 가격                                   |
| search.poi[0].oildata.updatetime | String  | 업데이트 시간                                  |
| search.poi[0].oildata.priceinfo  | String  | 최고, 최저 유가 정보<br>(H : 최고, L : 최저, X : 해당없음)<br>휘발유, 고급휘발유, 경유, LPG 순 |
| search.poi[0].oildata.wash       | Boolean | 세차 시설 여부                                 |
| search.poi[0].oildata.fix        | Boolean | 정비 가능 여부                                 |
| search.poi[0].oildata.mart       | Boolean | 매점 여부                                    |
| search.poi[0].subpoi             | Object  | 하위 시설물 정보                                |
| search.poi[0].subpoi.count       | Integer | 하위 시설물 개수                                |
| search.poi[0].subpoi.poi         | Array   | POI 정보와 동일                               |
| search.tel                       | Array   | TEL 검색 결과 목록 (POI 정보와 동일)                |
| search.adm                       | Array   | ADM 검색 결과 목록                             |
| search.adm[0].type               | String  | 검색 type<br>1 : 행정계 검색<br>2 : 지번 검색<br>3 : 새주소 검색 |
| search.adm[0].posx               | String  | X 좌표(WGS84의 경우 longitude)                 |
| search.adm[0].posy               | String  | Y 좌표(WGS84의 경우 latitude)                  |
| search.adm[0].admcode            | String  | 행정코드                                     |
| search.adm[0].address            | String  | 주소                                       |
| search.adm[0].jibun              | String  | 지번                                       |
| search.adm[0].roadname           | String  | 새주소 도로명                                  |
| search.adm[0].roadjibun          | String  | 새주소 지번                                   |
| search.adm[0].accuracy           | Integer | 지번 정확도<br>0 : 정확 검색<br>1 : 호지번 확장<br>2 : 모지번 확장 |
| search.hasgasstation             | Boolean | 유가 정보 제공 여부                              |
| search.oilprice                  | Object  | 유가 정보                                    |
| search.oilprice.max_g_price      | Integer | 최고 휘발유 가격                                |
| search.oilprice.min_g_price      | Integer | 최저 휘발유 가격                                |
| search.oilprice.avg_g_price      | Integer | 평균 휘발유 가격                                |
| search\.oilprice\.max\_hg\_price | Integer | 최고 고급 휘발유 가격                             |
| search\.oilprice\.min\_hg\_price | Integer | 최저 고급 휘발유 가격                             |
| search\.oilprice\.avg\_hg\_price | Integer | 평균 고급 휘발유 가격                             |
| search.oilprice.max_d_price      | Integer | 최고 경유 가격                                 |
| search.oilprice.min_d_price      | Integer | 최저 경유 가격                                 |
| search.oilprice.avg_d_price      | Integer | 평균 경유 가격                                 |
| search.oilprice.max_l_price      | Integer | 최고 LPG 가격                                |
| search.oilprice.min_l_price      | Integer | 최저 LPG 가격                                |
| search.oilprice.avg_l_price      | Integer | 평균 LPG 가격                                |


### 2\. 추천어 검색

* 검색어의 추천어를 검색합니다.

#### 요청

[URI]

| 메서드  | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/proposers?query={query} |

[Path parameter]

| 이름     | 타입     | 필수 여부 | 유효 범위 | 설명     |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 필수    |       | 고유의 앱키 |

[Query Parameters]

| 이름    | 타입     | 필수 여부 | 유효 범위 | 설명                     |
| ----- | ------ | ----- | ----- | ---------------------- |
| query | String | 필수    | 50바이트 | 한글/영문/숫자 50바이트(한글 25자) |

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

| 이름                            | 타입      | 설명        |
| ----------------------------- | ------- | --------- |
| header                        | Object  | 헤더 영역     |
| header.isSuccessful           | Boolean | 성공 여부     |
| header.resultCode             | Integer | 실패 코드     |
| header.resultMessage          | String  | 실패 메시지    |
| proposer                      | Object  | 본문 영역     |
| proposer.result               | Boolean | 성공 여부     |
| proposer.count                | Integer | 추천 검색어 개수 |
| proposer.keyword              | Array   | 추천 검색어 목록 |
| proposer.keyword[0].keyword   | String  | 추천 검색어    |
| proposer.keyword[0].frequency | Integer | 조회 빈도     |

### 3\. POI 상세 검색

* POI에 대한 상세 정보를 검색합니다.

#### 요청

[URI]

| 메서드  | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/pois?poiid={poiid} |

[Path parameter]

| 이름     | 타입     | 필수 여부 | 유효 범위 | 설명     |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 필수    |       | 고유의 앱키 |

[Query Parameters]

| 이름    | 타입     | 필수 여부 | 유효 범위 | 설명                                       |
| ----- | ------ | ----- | ----- | ---------------------------------------- |
| poiid | String | 필수    | 186개  | POI ID<br>poiid를 구분자 ","와 함께 입력<br>(여러 개 가능 186개까지)<br>예) poiid=123,234,567 |

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
				"poiid": 510835.0,
        "dpx": "127.059664",
        "dpy": "37.508629",
        "rpx": "127.059089",
        "rpy": "37.508779",
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

| 이름                                 | 타입      | 설명                                       |
| ---------------------------------- | ------- | ---------------------------------------- |
| header                             | Object  | 헤더 영역                                    |
| header.isSuccessful                | Boolean | 성공 여부                                    |
| header.resultCode                  | Integer | 실패 코드                                    |
| header.resultMessage               | String  | 실패 메시지                                   |
| poi                                | Object  | 본문 영역                                    |
| poi.result                         | Boolean | 성공 여부                                    |
| poi.totalcount                     | Integer | 전체 검색 결과 대상 개수                           |
| poi.count                          | Integer | 검색 결과 개수                                 |
| poi.poiinfo                        | Array   | POI 검색 결과 목록                             |
| poi.poiinfo[0].poiid               | Integer | POI ID                                   |
| poi.poiinfo[0].dpx                 | String  | display X 좌표(WGS84의 경우 longitude)         |
| poi.poiinfo[0].dpy                 | String  | display Y 좌표(WGS84의 경우 latitude)          |
| poi.poiinfo[0].rpx                 | String  | 탐색 X 좌표(WGS84의 경우 longitude)              |
| poi.poiinfo[0].rpy                 | String  | 탐색 Y 좌표(WGS84의 경우 latitude)               |
| poi.poiinfo[0].name1               | String  | 정식 명칭                                    |
| poi.poiinfo[0].name2               | String  | 축약 명칭                                    |
| poi.poiinfo[0].name3               | String  | 확장 명칭 1                                  |
| poi.poiinfo[0].name4               | String  | 확장 명칭 2                                  |
| poi.poiinfo[0].admcode             | String  | 행정코드                                    |
| poi.poiinfo[0].jibun               | String  | 지번                                       |
| poi.poiinfo[0].address             | String  | 주소                                       |
| poi.poiinfo[0].roadname            | String  | 새주소 도로명                                  |
| poi.poiinfo[0].roadjibun           | String  | 새주소 지번                                   |
| poi.poiinfo[0].detailaddress       | String  | 상세 주소                                    |
| poi.poiinfo[0].catecode            | String  | 분류 코드                                    |
| poi.poiinfo[0].catename            | String  | 분류 명칭                                    |
| poi.poiinfo[0].fulladdress         | String  | 전체 주소(행정주소+지번+상세주소)                      |
| poi.poiinfo[0].zip                 | String  | 우편번호                                     |
| poi.poiinfo[0].homeage             | String  | 홈페이지 url                                 |
| poi.poiinfo[0].email               | String  | 이메일                                      |
| poi.poiinfo[0].howtogo             | String  | 교통편                                      |
| poi.poiinfo[0].tel1                | String  | 전화번호 1                                   |
| poi.poiinfo[0].tel2                | String  | 전화번호 2                                   |
| poi.poiinfo[0].fax1                | String  | 팩스번호 1                                   |
| poi.poiinfo[0].fax2                | String  | 팩스번호 2                                   |
| poi.poiinfo[0].icode               | String  | ICODE                                    |
| poi.poiinfo[0].detail_count        | Integer | 분류 상세 항목 개수                              |
| poi.poiinfo[0].etc_count           | Integer | 분류 기타 항목 개수                              |
| poi.poiinfo[0].imagecount          | Integer | POI 이미지 개수                               |
| poi.poiinfo[0].hasoildata          | Boolean | 유가 데이터 존재 유무                             |
| poi.poiinfo[0].detailinfo          | Array   | 분류 상세 항목                                 |
| poi.poiinfo[0].detailinfo[0].name  | String  | 분류 상세 항목 설명                              |
| poi.poiinfo[0].detailinfo[0].value | String  | 분류 상세 항목 내용                              |
| poi.poiinfo[0].etcinfo             | Array   | 분류 기타 항목                                 |
| poi.poiinfo[0].etcinfo[0].name     | String  | 분류 기타 항목 설명                              |
| poi.poiinfo[0].etcinfo[0].value    | String  | 분류 기타 항목 내용                              |
| poi.poiinfo[0].oildata             | Object  | 유가 데이터 정보                                |
| poi.poiinfo[0].oilda.tag_price     | Integer | 휘발유 가격                                   |
| poi.poiinfo[0].oilda.hg_price      | Integer | 고급휘발유 가격                                 |
| poi.poiinfo[0].oilda.d_price       | Integer | 경유 가격                                    |
| poi.poiinfo[0].oilda.l_price       | Integer | LPG 가격                                   |
| poi.poiinfo[0].oilda.updatetime    | String  | 업데이트 시간                                  |
| poi.poiinfo[0].oilda.priceinfo     | String  | 최고, 최저 유가 정보<br>(H : 최고, L : 최저, X : 해당없음)<br>휘발유, 고급휘발유, 경유, LPG 순 |
| poi.poiinfo[0].oilda.wash          | Boolean | 세차 시설 여부                                 |
| poi.poiinfo[0].oilda.fix           | Boolean | 정비 가능 여부                                 |
| poi.poiinfo[0].oilda.mart          | Boolean | 매점 여부                                    |

### 4\. POI 하위 시설물 검색

* 특정 POI에 대한 하위 시설물을 검색합니다.

#### 요청

[URI]

| 메서드  | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/sub-pois?poiid={poiid}&x1={x1}&y1={y1} |

[Path parameter]

| 이름     | 타입     | 필수 여부 | 유효 범위 | 설명     |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 필수    |       | 고유의 앱키 |

[Query Parameters]

| 이름    | 타입     | 필수 여부 | 유효 범위                                    | 설명                  |
| ----- | ------ | ----- | ---------------------------------------- | ------------------- |
| poiid | String | 필수    |                                          | POI ID<br>복수개 지원 안됨 |
| x1    | String | 선택    | 현위치 또는 지도중심좌표<br>X, Y 좌표가 모두 NULL 또는 0일 경우 거리 계산을 수행하지 않음 |                     |
| y1    | String | 선택    | 현위치 또는 지도중심좌표<br>X, Y 좌표가 모두 NULL 또는 0일 경우 거리 계산을 수행하지 않음 |                     |

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
        "totalcount": 1,
        "count": 1,
        "poi": [
            {
                "poiid": 1415980,
                "depth": 1,
                "dpx": "127.110862",
                "dpy": "37.402334",
                "rpx": "127.110862",
                "rpy": "37.402334",
                "name1": "정문",
                "name2": "팅크웨어정문",
                "name3": "",
                "name4": "",
                "admcode": "4113510900",
                "jibun": "678",
                "address": "경기도 성남시 분당구 삼평동",
                "roadname": "경기도 성남시 분당구 판교역로",
                "roadjibun": "240",
                "detailaddress": "",
                "catecode": "181100",
                "catename": "도로시설",
                "dp_catecode": "000",
                "userid": "",
                "imagecount": 0,
                "userimagecount": 0,
                "badgeflag": false,
                "distance": 12164030,
                "tel": "",
                "islandmark": false,
                "visitscore": "0",
                "landmarkscore": "0",
                "popularity": false,
                "pop_tv": false,
                "pop_sns": false,
                "pop_hot": false,
                "pop_hit": false,
                "pop_top": "",
                "updateTS": "1970-01-01 09:00:00",
                "hasoildata": false,
                "hasdetailinfo": false,
                "hassubpoi": false
            }...
    		]
  	}
}
```

##### 필드

| 이름                               | 타입      | 설명                                       |
| -------------------------------- | ------- | ---------------------------------------- |
| header                           | Object  | 헤더 영역                                    |
| header.isSuccessful              | Boolean | 성공 여부                                    |
| header.resultCode                | Integer | 실패 코드                                    |
| header.resultMessage             | String  | 실패 메시지                                   |
| subpoi                           | Object  | 본문 영역                                    |
| subpoi.result                    | Boolean | 성공 여부                                    |
| subpoi.totalcount                | Integer  | 전체 검색결과 대상 개수                            |
| subpoi.count                     | Integer  | 검색 결과 개수                                 |
| subpoi.poi                       | Array   | POI 검색 결과 목록                             |
| subpoi.poi[0].poiid              | Integer | POI ID                                   |
| subpoi.poi[0].depth              | String  | POI depth                                |
| subpoi.poi[0].dpx                | String  | display X 좌표(WGS84의 경우 longitude)         |
| subpoi.poi[0].dpy                | String  | display Y 좌표(WGS84의 경우 latitude)          |
| subpoi.poi[0].rpx                | String  | 탐색 X 좌표(WGS84의 경우 longitude)              |
| subpoi.poi[0].rpy                | String  | 탐색 Y 좌표(WGS84의 경우 latitude)               |
| subpoi.poi[0].name1              | String  | 정식명칭                                     |
| subpoi.poi[0].name2              | String  | 축약명칭                                     |
| subpoi.poi[0].name3              | String  | 확장명칭1                                    |
| subpoi.poi[0].name4              | String  | 확장명칭2                                    |
| subpoi.poi[0].admcode            | String  | 행정코드                                     |
| subpoi.poi[0].address            | String  | 주소                                       |
| subpoi.poi[0].jibun              | String  | 지번                                       |
| subpoi.poi[0].roadname           | String  | 새주소 도로명                                  |
| subpoi.poi[0].roadjibun          | String  | 새주소 지번                                   |
| subpoi.poi[0].detailaddress      | String  | 상세주소                                     |
| subpoi.poi[0].catecode           | String  | 분류코드                                     |
| subpoi.poi[0].catename           | String  | 분류명칭                                     |
| subpoi.poi[0].dp_catecode        | String  | DP 분류코드                                  |
| subpoi.poi[0].distance           | Integer | 좌표와의 거리(해당 될 때만)                         |
| subpoi.poi[0].tel                | String  | 전화번호                                     |
| subpoi.poi[0].hasoildata         | Boolean | 유가 데이터 존재 여부                             |
| subpoi.poi[0].hasdetailinfo      | Boolean | 상세정보 존재 여부                               |
| subpoi.poi[0].hassubpoi          | Boolean | 하위시설물 존재여부                               |
| subpoi.poi[0].adv_count          | Boolean | 광고 코드 개수                                 |
| subpoi.poi[0].islandmark         | Boolean | 랜드마크 여부                                  |
| subpoi.poi[0].updateTS           | String  | 최종변경 일시(Y4-MM-DD HH:mm:ss)포맷             |
| subpoi.poi[0].data_source        | String  | POI 생성 정보 구분 (Thinkware/Tel/User)        |
| subpoi.poi[0].badgeflag          | Boolean | 배지 유무(Not Yet: FALSE, Badged: TRUE)      |
| subpoi.poi[0].userid             | String  | POI 등록 사용자 ID (UCP인 경우에만)                |
| subpoi.poi[0].imagecount         | Integer | POI 이미지 개수                               |
| subpoi.poi[0].oildata            | Object  | 유가 데이터 정보                                |
| subpoi.poi[0].oildata.g_price    | Integer | 휘발유 가격                                   |
| subpoi.poi[0].oildata.hg_price   | Integer | 고급휘발유 가격                                 |
| subpoi.poi[0].oildata.d_price    | Integer | 경유 가격                                    |
| subpoi.poi[0].oildata.l_price    | Integer | LPG 가격                                   |
| subpoi.poi[0].oildata.updatetime | String  | Update 시간                                |
| subpoi.poi[0].oildata.priceinfo  | String  | 최고, 최저 유가 정보<br>(H: 최고, L: 최저, X: 해당없음)<br>휘발유, 고급휘발유, 경유, LPG 순 |
| subpoi.poi[0].oildata.wash       | Boolean | 세차시설여부                                   |
| subpoi.poi[0].oildata.fix        | Boolean | 정비가능여부                                   |
| subpoi.poi[0].oildata.mart       | Boolean | 매점여부                                     |
| subpoi.poi[0].AdInfo             | Array   | 광고 코드 목록                                 |
| subpoi.poi[0].AdInfo[0].ADCODE   | Integer | 광고 코드<br>1~99까지 부여가능(최대99개)              |
| subpoi.poi[0].subpoi             | Object  | 하위 시설물 정보                                |
| subpoi.poi[0].subpoi.count       | Integer | subpoi 개수                                |
| subpoi.poi[0].subpoi.poi         | Array   | POI 정보와 동일                               |

### 5\. 좌표변환

* WGS84 <-> TM 좌표간 변환값을 반환합니다.

#### 요청

[URI]

| 메서드  | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/trans-coordinates?coordtype={coordtype}&x={x}&y={y} |

[Path parameter]

| 이름     | 타입     | 필수 여부 | 유효 범위 | 설명     |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 필수    |       | 고유의 앱키 |

[Query Parameters]

| 이름        | 타입     | 필수 여부 | 유효 범위                                 | 설명                                   |
| --------- | ------ | ----- | ------------------------------------- | ------------------------------------ |
| coordtype | String | 필수    |                                       | 0 : WGS84 -> TM <br> 1 : TM -> WGS84 |
| x         | String | 필수    | 현 위치 또는 지도 중심 좌표<br>WGS84 좌표 혹은 TM 좌표 |                                      |
| y         | String | 필수    | 현 위치 또는 지도 중심 좌표<br>WGS84 좌표 혹은 TM 좌표 |                                      |

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
    "coordtype": "WGS84",
    "x": "128.662952",
    "y": "38.058678"
  }
}
```

##### 필드

| 이름                   | 타입      | 설명       |
| -------------------- | ------- | -------- |
| header               | Object  | 헤더 영역    |
| header.isSuccessful  | Boolean | 성공 여부    |
| header.resultCode    | Integer | 실패 코드    |
| header.resultMessage | String  | 실패 메시지   |
| coordinate           | Object  | 본문 영역    |
| coordinate.coordtype | String  | 변환 좌표 형태 |
| coordinate.x         | String  | 변환 X 좌표   |
| coordinate.y         | String  | 변환 Y 좌표   |


## Geocoding API

### 1\. 주소 검색\(주소 \-\> 좌표\)

* 주소로 좌표(TW 좌표/WGS84 좌표/TM 좌표)를 검색합니다.

#### 요청

[URI]

| 메서드  | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/coordinates?query={query}&coordtype={coordtype}&startposition={startposition}&reqcount={reqcount}&admcode={admcode} |

[Path parameter]

| 이름     | 타입     | 필수 여부 | 유효 범위 | 설명     |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 필수    |       | 고유의 앱키 |

[Query Parameters]

| 이름            | 타입     | 필수 여부 | 유효 범위 | 설명                                       |
| ------------- | ------ | ----- | ----- | ---------------------------------------- |
| query         | String | 필수    |       | 검색어                                      |
| coordtype     | String | 선택    |       | 좌표 형식<br>0 : TW 좌표<br>1 : WGS84 좌표<br>2 : TM 좌표 |
| startposition | String | 선택    |       | 검색 시작 위치<br>0 : 첫번째 위치<br>미입력 시 0으로 조회   |
| reqcount      | String | 선택    |       | 검색 요청 개수<br>0으로 설정 시 Max Count 반환        |
| admcode       | String | 선택    |       | 행정코드                                    |

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
        "totalcount": 6.0,
        "admtotalcount": 6.0,
        "admcount": 3.0,
        "res_type": "NNYN",
        "adm": [
            {
                "type": 2.0,
                "posx": "126.689009",
                "posy": "36.157903",
                "admcode": "4477038000",
                "jibun": "",
                "address": "충청남도 서천군 판교면",
                "roadname": "",
                "roadjibun": "",
                "accuracy": 3.0,
                "distance": 1.2081825E7
            },
            {
                "type": 2.0,
                "posx": "126.521977",
                "posy": "36.547422",
                "admcode": "4480037030",
                "jibun": "",
                "address": "충청남도 홍성군 서부면 판교리",
                "roadname": "",
                "roadjibun": "",
                "accuracy": 3.0,
                "distance": 1.2082085E7
            },
            {
                "type": 2.0,
                "posx": "126.699108",
                "posy": "36.167844",
                "admcode": "4477038021",
                "jibun": "",
                "address": "충청남도 서천군 판교면 판교리",
                "roadname": "",
                "roadjibun": "",
                "accuracy": 3.0,
                "distance": 1.2083048E7
            }
        ]
    }
}
```

##### 필드

| 이름                       | 타입      | 설명                                       |
| ------------------------ | ------- | ---------------------------------------- |
| header                   | Object  | 헤더 영역                                    |
| header.isSuccessful      | Boolean | 성공 여부                                    |
| header.resultCode        | Integer | 실패 코드                                    |
| header.resultMessage     | String  | 실패 메시지                                   |
| address                  | Object  | 본문 영역                                    |
| address.result           | Boolean | 성공 여부                                    |
| address.totalcount       | Integer | 전체 검색 결과 대상 개수                           |
| address.res_type         | String  | 검색 결과Type명칭<br>명칭, 카테고리, 주소, 전화번호 순<br>(예) NYNN : 명칭 No, 카테고리 YES, 주소 NO, 전화번호 NO |
| address.adm              | Array   | 검색결과                                     |
| address.adm[0].type      | String  | 검색 type<br>1 : 행정계 검색<br>2 : 지번 검색<br>3 : 새주소 검색 |
| address.adm[0].posx      | String  | X 좌표                                     |
| address.adm[0].posy      | String  | Y 좌표                                     |
| address.adm[0].admcode   | String  | 행정코드                                    |
| address.adm[0].address   | String  | 주소                                       |
| address.adm[0].roadname  | String  | 새주소 도로명                                  |
| address.adm[0].roadjibun | String  | 새주소 지번                                   |
| address.adm[0].accuracy  | Integer | 지번 정확도<br>0 : 정확 검색<br>1 : 호지번 확장<br>예) 963-2 검색 시 963-X 검색 결과 반환<br>2 : 모지번 확장<br>예) 963-2 검색 시 96X 검색 결과 반환<br>3 : 법정동 동좌표<br>예) 삼평동 까지만 입력 되는 경우<br>4 : 동단위 이상 좌표 또는 법정동 좌표<br>예) 분당구까지만 입력 되는 경우 |



## Reverse Geocoding API

### 1\. 좌표검색\(좌표 \-\> 주소\)

* 좌표(TW 좌표/WGS84 좌표)로 주소를 검색합니다.

#### 요청

[URI]

| 메서드  | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/addresses?posX={posX}&posY={posY}&coordtype={coordtype} |

[Path parameter]

| 이름     | 타입     | 필수 여부 | 유효 범위 | 설명     |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 필수    |       | 고유의 앱키 |

[Query Parameters]

| 이름        | 타입     | 필수 여부 | 유효 범위 | 설명                                       |
| --------- | ------ | ----- | ----- | ---------------------------------------- |
| posX      | String | 필수    |       | X 좌표                                     |
| posY      | String | 필수    |       | Y 좌표                                     |
| coordtype | String | 선택    |       | 요청 좌표 형식<br>0 : TW 좌표<br>1 : WGS84 좌표<br>미 입력 시 TW 좌표 기준 검색 |

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
        "posx": "126.947265",
        "posy": "37.384033",
        "roadname": "경기도 안양시 동안구 귀인로",
        "roadjibun": "59",
        "adm_address": {
            "address": "경기도 안양시 동안구 범계동",
            "admcode": "4117361000",
            "address_category3": "범계동",
            "address_category4": "",
            "jibun": "921",
            "address_category1": "경기도",
            "address_category2": "안양시 동안구",
            "cut_address": "경기 안양시 동안구 범계동"
        },
        "legal_address": {
            "address": "경기도 안양시 동안구 호계동",
            "admcode": "4117310400",
            "address_category3": "호계동",
            "address_category4": "",
            "jibun": "921",
            "address_category1": "경기도",
            "address_category2": "안양시 동안구",
            "cut_address": "경기 안양시 동안구 호계동"
        }
    }
}
```

##### 필드

| 이름                     | 타입      | 설명                                       |
| ---------------------- | ------- | ---------------------------------------- |
| header                 | Object  | 헤더 영역                                    |
| header.isSuccessful    | Boolean | 성공 여부                                    |
| header.resultCode      | Integer | 실패 코드                                    |
| header.resultMessage   | String  | 실패 메시지                                   |
| location               | Object  | 본문 영역                                    |
| location.result        | Boolean | 성공 여부                                    |
| location.posx      | String  | X 좌표                                     |
| location.posy      | String  | Y 좌표                                     |
| location.roadname  | String  | 새주소 도로명                                  |
| location.roadjibun | String  | 새주소 지번                                   |
| location.adm_address           | Object  | 행정동 주소 정보                           |
| location.adm_address.admcode   | String  | 행정코드                                    |
| location.adm_address.address   | String  | 주소                                       |
| location.adm_address.jibun     | String  | 지번                                       |
| location.adm_address.address_category1     | String  |   도/시                      |
| location.adm_address.address_category2     | String  |   시/군/구                   |
| location.adm_address.address_category3     | String  |   읍/면/동                 |
| location.adm_address.address_category4     | String  |   리                  |
| location.adm_address.cut_address     | String  |                         |
| location.legal_address           | Object  | 행정동 주소 정보                           |
| location.legal_address.admcode   | String  | 행정코드                                    |
| location.legal_address.address   | String  | 주소                                       |
| location.legal_address.jibun     | String  | 지번                                       |
| location.legal_address.address_category1     | String  |  도/시                       |
| location.legal_address.address_category2     | String  |  시/군/구                      |
| location.legal_address.address_category3     | String  |  읍/면/동                      |
| location.legal_address.address_category4     | String  |  리                       |
| location.legal_address.cut_address     | String  |                         |





## 탐색

### 1\. 경로 탐색

* 출발지와 목적지 (경유지 옵션) 좌표를 이용하여 탐색된 상세 정보와 경로 정보를 반환합니다.

#### 요청

[URI]

| 메서드  | URI                                      |
| ---- | ---------------------------------------- |
| GET,POST  | /maps/v3.0/appkeys/{appkey}/route-normal?option={option}&coordType={coordType}&carType={carType}&startX={startX}&startY={startY}&endX={endX}&endY={endY}&via1X={via1X}&via1Y={via1Y}&via2X={via2X}&via2Y={via2Y}&via3X={via3X}&via3Y={via3Y}&via4X={via4X}&via4Y={via4Y}&via5X={via5X}&via5Y={via5Y}&guideTop={guideTop}&groupByTrafficColor={groupByTrafficColor}&saveFile={saveFile} |

[Path parameter]

| 이름     | 타입     | 필수 여부 | 유효 범위 | 설명     |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 필수    |       | 고유의 앱키 |

[Request Parameters]

| 이름       | 타입     | 필수 여부 | 유효 범위 | 설명                                       |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| startX   | String | 필수    |       | 출발지 X 좌표                                 |
| startY   | String | 필수    |       | 출발지 Y 좌표                                 |
| endX     | String | 필수    |       | 도착지 X 좌표                                 |
| endY     | String | 필수    |       | 도착지 Y 좌표                                 |
| via1X    | String | 선택    |       | 경유지 1 X 좌표                               |
| via1Y    | String | 선택    |       | 경유지 1 Y 좌표                               |
| via2X    | String | 선택    |       | 경유지 2 X 좌표                               |
| via2Y    | String | 선택    |       | 경유지 2 Y 좌표                               |
| via3X    | String | 선택    |       | 경유지 3 X 좌표                               |
| via3Y    | String | 선택    |       | 경유지 3 Y 좌표                               |
| via4X    | String | 선택    |       | 경유지 4 X 좌표                               |
| via4Y    | String | 선택    |       | 경유지 4 Y 좌표                               |
| via5X    | String | 선택    |       | 경유지 5 X 좌표                               |
| via5Y    | String | 선택    |       | 경유지 5 Y 좌표                               |
| option   | String | 필수    |       | 경로 탐색 옵션<br>탐색 옵션 하나만 가능<br>예) option=real_traffic<br>real_traffic : 실시간 추천1<br>real\_traffic\_freeroad : 실시간 \(무료\)<br>real_traffic2 : 실시간 추천2<br>short\_distance\_priority : 단거리<br>motorcycle: 이륜차 |
| carType   | Integer | 선택    |       | 톨게이트비 계산을 위한 차종(1~6), default : 1 |
| coordType   | String | 필수    |       | input, output 좌표 타입, 하나만 입력가능 (tw, wgs84) |
|guideTop	|Integer| 선택 ||표출할 안내정보 개수 |
|groupByTrafficColor	| Boolean| 선택| |세부경로목록 (paths) 정보를 교통색상별로 그룹핑하여 반환할지 여부	|
|saveFile	| Boolean| 선택| |경로 주변 POI 검색을 위한 binary 파일 저장 여부	|



#### 응답

##### 응답 본문
```
{
    "route": {
        "data": {
            "file_name": "",
            "toll_fee": 0.0,
            "paths": [
                {
                    "coords": [
                        {
                            "x": 127.5313243125899,
                            "y": 37.40142475251763
                        },
                        {
                            "x": 127.5313243125899,
                            "y": 37.40142475251763
                        },
                        ...
                    ],
                    "speed": -1.0,
                    "distance": 258.0,
                    "spend_time": 96.0,
                    "road_code": 5.0,
                    "traffic_color": "#d73a76"
                },
                ...
            ],
            "guides": [
                {
                    "name": "수부촌길",
                    "distance": 440.0,
                    "speed": -1.0,
                    "road_code": 5.0,
                    "score": 880.0,
                    "type": "ROAD",
                    "coords": [
                        {
                            "x": 127.5313243125899,
                            "y": 37.40142475251763
                        },
                        {
                            "x": 127.5313243125899,
                            "y": 37.40142475251763
                        },
                        ...
                    ],
                    "traffic_color": ""
                },
              ...
            ],
            "option": "real_traffic",
            "spend_time": 240.0,
            "distance": 858.0
        }
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### 필드

| 이름                          | 타입      | 설명                                       |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | 헤더 영역                                    |
| header.isSuccessful         | Boolean | 성공 여부                                    |
| header.resultCode           | Integer | 실패 코드                                    |
| header.resultMessage        | String  | 실패 메시지                                   |
| route			                  | Object  | 본문 영역                                    |
| route.data                   | Object  | 경로 정보                                    |
| route.data.file_name          | String | 경로 주변 POI 검색을 위한 binary 파일명                |
| route.data.option              | String | 탐색옵션                        |
| route.data.spend_time           | Integer | 소요시간(초)                              |
| route.data.distance           | Integer | 거리(m)                          |
| route.data.total_fee    | Integer | 톨게이트 요금                             |
| route.data.paths	 | Array | 세부 경로 목록                             |
| route.data.paths[0].coords | Array | 상세좌표 목록                            |
| route.data.paths[0].coords[0].x   | Double | X좌표                             |
| route.data.paths[0].coords[0].y         | Double | Y좌표                         |
| route.data.paths[0].speed          | Integer | 속도                                   |
| route.data.paths[0].spend_time          | Integer | 소요시간(초)                                   |
| route.data.paths[0].distance             | Integer | 거리(m)                        |
| route.data.paths[0].road_code             | Integer | 도로 종별 코드                        |
| route.data.paths[0].traffic_color       | String | 도로 교통 색상                        |
| route.data.guides       | Array | 주요도로정보 목록                        |
| route.data.guides[0].coords       | Array | 상세좌표 목록                        |
| route.data.guides[0].coords[0].x       | Array | X좌표                        |
| route.data.guides[0].coords[0].y       | Array | Y좌표                        |
| route.data.guides[0].distance       | Integer | 거리(m)                        |
| route.data.guides[0].name       | String | 도로명                        |
| route.data.guides[0].road_code       | Integer | 도로 종별 코드                        |
| route.data.guides[0].score       | Integer | 비중                        |
| route.data.guides[0].speed       | Integer | 속도(km)                       |
| route.data.guides[0].type       | String | 도로 타입                        |
| route.data.guides[0].traffic_color       | String | 도로 교통 색상                        |



### 2\. 경로 탐색 요약

* 출발지와 목적지(경유지 옵션) 좌표를 이용하여 탐색된 요약 정보(거리, 시간, 탐색옵션) 정보를 반환합니다.

#### 요청

[URI]

| 메서드  | URI                                      |
| ---- | ---------------------------------------- |
| GET,POST  | /maps/v3.0/appkeys/{appkey}/route-summary?option={option}&coordType={coordType}&startX={startX}&startY={startY}&endX={endX}&endY={endY}&via1X={via1X}&via1Y={via1Y}&via2X={via2X}&via2Y={via2Y}&via3X={via3X}&via3Y={via3Y}&via4X={via4X}&via4Y={via4Y}&via5X={via5X}&via5Y={via5Y} |

[Path parameter]

| 이름     | 타입     | 필수 여부 | 유효 범위 | 설명     |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 필수    |       | 고유의 앱키 |

[Request Parameters]

| 이름       | 타입     | 필수 여부 | 유효 범위 | 설명                                       |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| startX   | String | 필수    |       | 출발지 X 좌표                                 |
| startY   | String | 필수    |       | 출발지 Y 좌표                                 |
| endX     | String | 필수    |       | 도착지 X 좌표                                 |
| endY     | String | 필수    |       | 도착지 Y 좌표                                 |
| via1X    | String | 선택    |       | 경유지 1 X 좌표                               |
| via1Y    | String | 선택    |       | 경유지 1 Y 좌표                               |
| via2X    | String | 선택    |       | 경유지 2 X 좌표                               |
| via2Y    | String | 선택    |       | 경유지 2 Y 좌표                               |
| via3X    | String | 선택    |       | 경유지 3 X 좌표                               |
| via3Y    | String | 선택    |       | 경유지 3 Y 좌표                               |
| via4X    | String | 선택    |       | 경유지 4 X 좌표                               |
| via4Y    | String | 선택    |       | 경유지 4 Y 좌표                               |
| via5X    | String | 선택    |       | 경유지 5 X 좌표                               |
| via5Y    | String | 선택    |       | 경유지 5 Y 좌표                               |
| option   | String | 필수    |       | 경로 탐색 옵션<br>탐색 옵션 하나만 가능<br>예) option=real_traffic<br>real_traffic : 실시간 추천1<br>real\_traffic\_freeroad : 실시간 \(무료\)<br>real_traffic2 : 실시간 추천2<br>short\_distance\_priority : 단거리<br>motorcycle: 이륜차 |
| coordType   | String | 필수    |       | input, output 좌표 타입, 하나만 입력가능 (tw, wgs84) |


#### 응답

##### 응답 본문
```
{
    "route": {
        "data": [
            {
                "option": "real_traffic",
                "spend_time": 240.0,
                "distance": 858.0
            },
            ...
        ]
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### 필드

| 이름                          | 타입      | 설명                                       |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | 헤더 영역                                    |
| header.isSuccessful         | Boolean | 성공 여부                                    |
| header.resultCode           | Integer | 실패 코드                                    |
| header.resultMessage        | String  | 실패 메시지                                   |
| route			                  | Object  | 본문 영역                                    |
| route.data                   | Array  | 경로 정보                                    |
| route.data[0].option              | String | 탐색옵션                        |
| route.data[0].spend_time           | Integer | 소요시간(초)                              |
| route.data[0].distance           | Integer | 거리(m)                          |


### 3\. 다중 출발지 경로 탐색 요약

* 하나 이상의 다중 출발지 좌표와 하나의 목적지 좌표를 탐색하여 각각의 시간과 거리 정보를 반환합니다.

#### 요청

[URI]

| 메서드  | URI                                      |
| ---- | ---------------------------------------- |
| POST  | /maps/v3.0/appkeys/{appkey}/route-start-multi-summary|

[Path parameter]

| 이름     | 타입     | 필수 여부 | 유효 범위 | 설명     |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 필수    |       | 고유의 앱키 |

[Request Parameters]

| 이름       | 타입     | 필수 여부 | 유효 범위 | 설명                                       |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| data    | Array |     |       | 출발지 정보 Array                               |
| data[0].startX   | String | 필수    |       | 출발지 X 좌표                                 |
| data[0].startY   | String | 필수    |       | 출발지 Y 좌표                                 |
| data[0].startIdx   | String | 필수    |       | 출발지 식별ID                                 |
| endX     | String | 필수    |       | 도착지 X 좌표                                 |
| endY     | String | 필수    |       | 도착지 Y 좌표                                 |
| orderby    | String | 필수    |       | 정렬기준 (<br> 0 : distance_desc<br>1 : distance_asc<br>2 : time_desc <br>3 : time_asc<br>)                               |
| coordType    | String | 필수    |       | 좌표 타입(tw, wgs84)
| resultCount    | Integer | 선택    |       | 결과 표출 개수                               |


#### 응답

##### 응답 본문
```
{
    "route": {
        "data": [
            {
                "spend_time": 240.0,
                "distance": 858.0,
                "startX": "127.538593",
                "startY": "37.398322",
                "startIdx": "test"
            },
            {
                "spend_time": 960.0,
                "distance": 8289.0,
                "startX": "127.50940913221785",
                "startY": "37.44046992358892",
                "startIdx": "test2"
            }
        ]
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### 필드

| 이름                          | 타입      | 설명                                       |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | 헤더 영역                                    |
| header.isSuccessful         | Boolean | 성공 여부                                    |
| header.resultCode           | Integer | 실패 코드                                    |
| header.resultMessage        | String  | 실패 메시지                                   |
| route			                  | Object  | 본문 영역                                    |
| route.data                   | Array  | 경로 정보                                    |
| route.data[0].spend_time           | Integer | 소요시간(초)                              |
| route.data[0].distance           | Integer | 거리(m)                          |
| route.data[0].startX           | String | 출발지 X좌표                          |
| route.data[0].startY           | String | 출발지 Y좌표                          |
| route.data[0].startIdx           | String | 출발지 식별 ID                          |



### 4\. 다중 목적지 경로 탐색 요약

* 하나의 출발지 좌표와 하나 이상의 다중 목적지 좌표를 탐색하여 각각의 시간과 거리 정보를 반환합니다.

#### 요청

[URI]

| 메서드  | URI                                      |
| ---- | ---------------------------------------- |
| POST  | /maps/v3.0/appkeys/{appkey}/route-end-multi-summary|

[Path parameter]

| 이름     | 타입     | 필수 여부 | 유효 범위 | 설명     |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 필수    |       | 고유의 앱키 |

[Request Parameters]

| 이름       | 타입     | 필수 여부 | 유효 범위 | 설명                                       |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| data    | Array |     |       | 출발지 정보 Array                               |
| data[0].endX   | String | 필수    |       | 도착지 X 좌표                                 |
| data[0].endY   | String | 필수    |       | 도착지 Y 좌표                                 |
| data[0].endIdx   | String | 필수    |       | 도착지 식별ID                                 |
| startX     | String | 필수    |       | 출발지 X 좌표                                 |
| startY     | String | 필수    |       | 출발지 Y 좌표                                 |
| orderby    | String | 필수    |       | 정렬기준 (<br> 0 : distance_desc<br>1 : distance_asc<br>2 : time_desc <br>3 : time_asc<br>)                               |
| coordType    | String | 필수    |       | 좌표 타입(tw, wgs84)
| resultCount    | Integer | 선택    |       | 결과 표출 개수                               |


#### 응답

##### 응답 본문
```
{
    "route": {
        "data": [
            {
                "spend_time": 240.0,
                "distance": 858.0,
                "endX": "127.538593",
                "endY": "37.398322",
                "endIdx": "test"
            },
            {
                "spend_time": 1020.0,
                "distance": 8303.0,
                "endX": "127.50940913221785",
                "endY": "37.44046992358892",
                "endIdx": "test2"
            }
        ]
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### 필드

| 이름                          | 타입      | 설명                                       |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | 헤더 영역                                    |
| header.isSuccessful         | Boolean | 성공 여부                                    |
| header.resultCode           | Integer | 실패 코드                                    |
| header.resultMessage        | String  | 실패 메시지                                   |
| route			                  | Object  | 본문 영역                                    |
| route.data                   | Array  | 경로 정보                                    |
| route.data[0].spend_time           | Integer | 소요시간(초)                              |
| route.data[0].distance           | Integer | 거리(m)                          |
| route.data[0].endX           | String | 도착지 X좌표                          |
| route.data[0].endY           | String | 도착지 Y좌표                          |
| route.data[0].endIdx           | String | 도착지 식별 ID                          |



### 5\. 경로 예측 탐색

* 출발,도착 예정시간을 기준으로 예측 도착시간 및 출발지와 목적지 (경유지 옵션) 좌표를 이용하여 탐색된 상세 정보와 경로 정보를 반환합니다 .

#### 요청

[URI]

| 메서드  | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/route-time?startX={startX}&startY={startY}&endX={endX}&endY={endY}&type={type}&year={year}&month={month}&day={day}&hour={hour}&minutes={minutes}&via1X={via1X}&via1Y={via1Y}&via2X={via2X}&via2Y={via2Y}&via3X={via3X}&via3Y={via3Y}&via4X={via4X}&via4Y={via4Y}&via5X={via5X}&via5Y={via5Y}&coordType={coordType}&carType={carType}&useTrafficColor={useTrafficColor}&guideTop={guideTop}&groupByTrafficColor={groupByTrafficColor}&beforeCount={beforeCount}&afterCount={afterCount}&interval={interval}|

[Path parameter]

| 이름     | 타입     | 필수 여부 | 유효 범위 | 설명     |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 필수    |       | 고유의 앱키 |

[Request Parameters]

| 이름       | 타입     | 필수 여부 | 유효 범위 | 설명                                       |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| startX    | String | 필수   |       | 출발지 X 좌표
| startY    | String | 필수   |       | 출발지 Y 좌표
| endX   | String | 필수    |       | 도착지 X 좌표                                 |
| endY   | String | 필수    |       | 도착지 Y 좌표                                 |
| type     | String | 필수    |       | 기준시간 (출발,도착)<br> start : 출발시간 기준<br>end : 도착시간 기준                                 |
| year     | Integer | 필수    |       | 기준년(ex.2019)                                 |
| month     | Integer | 필수    |       | 기준월                                 |
| day    | Integer | 필수    |       | 기준일 		|
| hour     | Integer | 필수    |       | 기준시간(시)                                 |
| minutes    | Integer | 필수    |       | 기준시간(분) 		|
| via1X   | String | 선택    |       |  경유지 1 X 좌표                               |
| via1Y   | String | 선택    |       |  경유지 1 Y 좌표                               |
| via2X   | String | 선택    |       |  경유지 2 X 좌표                               |
| via2Y   | String | 선택    |       |  경유지 2 Y 좌표                               |
| via3X   | String | 선택    |       |  경유지 3 X 좌표                               |
| via3Y   | String | 선택    |       |  경유지 3 Y 좌표                               |
| via4X   | String | 선택    |       |  경유지 4 X 좌표                               |
| via4Y   | String | 선택    |       |  경유지 4 Y 좌표                               |
| via5X   | String | 선택    |       |  경유지 5 X 좌표                               |
| via5Y   | String | 선택    |       |  경유지 5 Y 좌표                               |
| coordType    | String | 선택    |       | 좌표 타입(tw, wgs84)<br> default : wgs84
| useTrafficColor   | Boolean | 선택    |       | 도로 교통 색상 반환 유무(true, false)<br> defaut : false |
| guideTop   | Integer | 선택    |       | 표출할 안내 정보 개수 |
| carType   | Integer | 선택    |       | 톨게이트비 계산을 위한 차종(1~6), default : 1 |
|groupByTrafficColor	| Boolean| 선택| |세부경로목록 (paths) 정보를 교통색상별로 그룹핑하여 반환할지 여부	|
| beforeCount   | Integer | 선택    |       | 기준 시간 이전전시간 탐색 개수 |
| afterCount   | Integer | 선택    |       | 기준 시간 이후시간 탐색 개수 |
| interval   | Integer | 선택    |       | 기준 시간 이전/이후 시간 Interval(분) |

#### 응답

##### 응답 본문
```
{
    "route": {
        "data": {
            "distance": 22621.0,
            "spend_time": 1620.0,
            "toll_fee": 0.0,
            "times": [
                {
                    "index": -2.0,
                    "spend_time": 1620.0,
                    "distance": 0.0,
                    "start_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 16.0,
                        "minutes": 0.0
                    },
                    "end_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 16.0,
                        "minutes": 27.0
                    }
                },
                {
                    "index": -1.0,
                    "spend_time": 1620.0,
                    "distance": 0.0,
                    "start_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 16.0,
                        "minutes": 30.0
                    },
                    "end_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 16.0,
                        "minutes": 57.0
                    }
                },
                {
                    "index": 0.0,
                    "spend_time": 1620.0,
                    "distance": 0.0,
                    "start_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 17.0,
                        "minutes": 0.0
                    },
                    "end_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 17.0,
                        "minutes": 27.0
                    }
                },
                {
                    "index": 1.0,
                    "spend_time": 1620.0,
                    "distance": 0.0,
                    "start_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 17.0,
                        "minutes": 30.0
                    },
                    "end_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 17.0,
                        "minutes": 57.0
                    }
                },
                {
                    "index": 2.0,
                    "spend_time": 1620.0,
                    "distance": 0.0,
                    "start_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 18.0,
                        "minutes": 0.0
                    },
                    "end_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 18.0,
                        "minutes": 27.0
                    }
                }
            ],
            "paths": [
                {
                    "coords": [
                        {
                            "x": 126.94730280056565,
                            "y": 37.38419119654106
                        },
                        {
                            "x": 126.94700283437736,
                            "y": 37.38395788491522
                        }
                    ],
                    "speed": -1.0,
                    "distance": 36.0,
                    "spend_time": 10.0,
                    "road_code": 5.0,
                    "traffic_color": "#989898"
                },
                {
                    "coords": [
                        {
                            "x": 126.94700283437736,
                            "y": 37.38395788491522
                        },
                        {
                            "x": 126.94650289104105,
                            "y": 37.383557922382955
                        }
                    ],
                    "speed": -1.0,
                    "distance": 63.0,
                    "spend_time": 20.0,
                    "road_code": 5.0,
                    "traffic_color": "#989898"
                },
                ...
            ],
            "guides": [
                {
                    "name": "경수대로",
                    "distance": 2401.0,
                    "speed": 53.0,
                    "road_code": 3.0,
                    "score": 14406.0,
                    "type": "ROAD",
                    "coords": [
                        {
                            "x": 126.95508976578816,
                            "y": 37.37800871915593
                        },
                        {
                            "x": 126.95518976229994,
                            "y": 37.37780874413099
                        },
                        ...
                    ],
                    "traffic_color": "#00ff60"
                },
                {
                    "name": "봉담과천로",
                    "distance": 13369.0,
                    "speed": 83.0,
                    "road_code": 2.0,
                    "score": 106952.0,
                    "type": "ROAD",
                    "coords": [
                        {
                            "x": 126.97727624066877,
                            "y": 37.34261321883654
                        },
                        {
                            "x": 126.97736373901714,
                            "y": 37.342388246474925
                        },
                        ...
                    ],
                    "traffic_color": "#00ff60"
                }
            ]
        }
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### 필드

| 이름                          | 타입      | 설명                                       |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | 헤더 영역                                    |
| header.isSuccessful         | Boolean | 성공 여부                                    |
| header.resultCode           | Integer | 실패 코드                                    |
| header.resultMessage        | String  | 실패 메시지                                   |
| route			                  | Object  | 본문 영역                                    |
| route.data                   | Object  | 경로 정보                                    |
| route.data.file_name          | String | 경로 주변 POI 검색을 위한 binary 파일명                |
| route.data.option              | String | 탐색옵션                        |
| route.data.spend_time           | Integer | 소요시간(초)                              |
| route.data.distance           | Integer | 거리(m)                          |
| route.data.total_fee    | Integer | 톨게이트 요금                             |
| route.data.times	 | Array | 세부 경로 목록                             |
| route.data.times[0].index	 | Integer | 기준시간 대비 Index(0 이면 기준시간)       |
| route.data.times[0].spend_time	 | Integer | 소요시간(초)       |
| route.data.times[0].start_time	 | Object | 출발시간       |
| route.data.times[0].start_time.year	 | Object | 년       |
| route.data.times[0].start_time.month	 | Object | 월       |
| route.data.times[0].start_time.day	 | Object | 일       |
| route.data.times[0].start_time.hour	 | Object | 시       |
| route.data.times[0].start_time.minutes	 | Object | 분       |
| route.data.times[0].end_time	 | Object | 도착시간       |
| route.data.times[0].end_time.year	 | Object | 년       |
| route.data.times[0].end_time.month	 | Object | 월       |
| route.data.times[0].end_time.day	 | Object | 일       |
| route.data.times[0].end_time.hour	 | Object | 시       |
| route.data.times[0].end_time.minutes	 | Object | 분       |
| route.data.paths	 | Array | 세부 경로 목록                             |
| route.data.paths[0].coords | Array | 상세좌표 목록                            |
| route.data.paths[0].coords[0].x   | Double | X좌표                             |
| route.data.paths[0].coords[0].y         | Double | Y좌표                         |
| route.data.paths[0].speed          | Integer | 속도                                   |
| route.data.paths[0].spend_time          | Integer | 소요시간(초)                                   |
| route.data.paths[0].distance             | Integer | 거리(m)                        |
| route.data.paths[0].road_code             | Integer | 도로 종별 코드                        |
| route.data.paths[0].traffic_color       | String | 도로 교통 색상                        |
| route.data.guides       | Array | 주요도로정보 목록                        |
| route.data.guides[0].coords       | Array | 상세좌표 목록                        |
| route.data.guides[0].coords[0].x       | Array | X좌표                        |
| route.data.guides[0].coords[0].y       | Array | Y좌표                        |
| route.data.guides[0].distance       | Integer | 거리(m)                        |
| route.data.guides[0].name       | String | 도로명                        |
| route.data.guides[0].road_code       | Integer | 도로 종별 코드                        |
| route.data.guides[0].score       | Integer | 비중                        |
| route.data.guides[0].speed       | Integer | 속도(km)                       |
| route.data.guides[0].type       | String | 도로 타입                        |
| route.data.guides[0].traffic_color       | String | 도로 교통 색상                        |


## Static Map

### 1\. Static Map

* 사용자가 지정한 지도 범위에 대해 정적 지도 이미지를 반환합니다.

#### 요청

[URI]

| 메서드  | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/static-maps?lon={lon}&lat{lat}&zoom={zoom}&bearing={bearing}&pitch={pitch}&width={width}&height={height}&x2={x2}&mx={mx}&my={my}&imgUrl={imgUrl}|

[Path parameter]

| 이름     | 타입     | 필수 여부 | 유효 범위 | 설명     |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 필수    |       | 고유의 앱키 |

[Request Query Parameters]

| 이름       | 타입     | 필수 여부 | 유효 범위 | 설명                                       |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| lon   | String | 필수    |       | 요청할 longitude(경도) 좌표           |
| lat   | String | 필수    |       | 요청할 latitude(위도)좌표             |
| zoom   | String | 선택    |       | 요청할 좌표의 확대레벨                                 |
| bearing     | String | 선택    |       | 요청할 좌표의 회전율                                 |
| pitch     | String | 선택    |       | 요청할 좌표의 기울기(0~30)   |
| width    | String | 선택    |       | 요청할 이미지 width 값   |
| height    | String | 선택    |       | 요청할 이미지 height 값 |
| x2    | String | 선택    |       | 이미지 사이즈 * 2 반환 여부  |
| mx    | String | 선택    |       | 마커를 표현할 좌표(longitude)   |
| my    | String | 선택    |       | 마커를 표현할 좌표(latitude)   |
| imgUrl    | String | 선택    |       | 마커를 표현할 이미지URL   |


#### 응답

##### 응답 본문
<img src="http://static.toastoven.net/toastcloud/notice/20191029_Maps_new/map_static.png">
