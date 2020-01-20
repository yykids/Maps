## Application Service > Maps > API User Guide 

Describes APIs that are required to use the Maps Service. 

## Common API Information

### Prerequisites 

* Appkey is required to use APIs. 
* To check your appkey, go to **URL & Appkey** on top of the **TOAST Console**. 

### Common Request Information

#### URL Information

| Environment | Domain                           |
| ----------- | -------------------------------- |
| Real        | https://api-maps.cloud.toast.com |

### Common Response Information

#### Search/Navigate API

* Respond with '200 OK' for all API requests. See header at the response body for more detail response results. 

```
{
	"header": {
		"isSuccessful": true,
		"resultCode": 0,
		"resultMessage": ""
	}
}
```

## Search

### 1\. Search of Address \(Search \-\> Coordinates\)

* Search coordinates (TW/WGS84/TM Coordinates) with address.

#### Request

[URI]

| Method | URI                                                          |
| ------ | ------------------------------------------------------------ |
| GET    | /maps/v1.0/appkeys/{appkey}/coordinates?query={query}&coordtype={coordtype}&startposition={startposition}&reqcount={reqcount}&admcode={admcode} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin Appkey |

[Query Parameters]

| Name          | Type   | Required | Valid Range | Description                                                  |
| ------------- | ------ | -------- | ----------- | ------------------------------------------------------------ |
| query         | String | Required |             | Search words                                                 |
| coordtype     | String | Optional |             | Type of Coordinates<br>0: TW <br>1: WGS84 <br>2: TM          |
| startposition | String | Optional |             | Start position of search <br>0: Initial location <br>Query by 0, if left blank |
| reqcount      | String | Optional |             | Number of search requests<br>Return max count, if it is set with 0 |
| admcode       | String | Optional |             | Administrative code                                          |

#### Response 

##### Body 

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
        "address": "Sampyeong-dong, Bundang-gu, Seongnam-si, Gyeonggi-do",
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
        "address": "Baekhyeon-dong (Pangyo-dong), Bundang-gu, Seongnam-si, Gyeonggi-do",
        "roadname": "",
        "roadjibun": "",
        "accuracy": 3
      }
    ]
  }
}
```

##### Field	

| Name                     | Type    | Description                                                  |
| ------------------------ | ------- | ------------------------------------------------------------ |
| header                   | Object  | Header area                                                  |
| header.isSuccessful      | Boolean | Successful or not                                            |
| header.resultCode        | Integer | Failure code                                                 |
| header.resultMessage     | String  | Failure message                                              |
| address                  | Object  | Body area                                                    |
| address.result           | Boolean | Successful or not                                            |
| address.totalcount       | Integer | Total number of search results                               |
| address.res_type         | String  | Name of search result type <br>In the order of Name, Category, Address, and Phone Number<br>(e.g.) NYNN: No for name, Yes for category, No for address, and No for phone number |
| address.adm              | Array   | Search result                                                |
| address.adm[0].type      | String  | Search type<br>1: Search administrative system<br>2: Search land-lot number<br>3:  Search new address system |
| address.adm[0].posx      | String  | X coordinates                                                |
| address.adm[0].posy      | String  | Y coordinates                                                |
| address.adm[0].admcode   | String  | Administrative code                                          |
| address.adm[0].address   | String  | Address                                                      |
| address.adm[0].roadname  | String  | Road name for new address system                             |
| address.adm[0].roadjibun | String  | Land-lot number for new address system                       |
| address.adm[0].accuracy  | Integer | Accuracy of land-lot numbers<br/>0: Search accuracy 
1: Extend the last land-lot number digit 
e.g.) For the search of 963-2, return the search result of 963-X.  
2 : Extend the initial land-lot number digits
e.g) For the search of 963-2, return the search result of 96X 
3: Coordinates of Dong by the administrative unit 
e.g.) In case input is available only down to Sampyeong-dong
4:  Coordinates of Dong or higher unit, or administrative Dong 
e.g.) In case input is available down to Bundang-gu only |

### 2\. Search of Coordinates \(Coordinates \-\> Address\)

* Search address with coordinates (TW/WGS84). 

#### Request

[URI]

| Method | URI                                                          |
| ------ | ------------------------------------------------------------ |
| GET    | /maps/v1.0/appkeys/{appkey}/addresses?query={query}&posX={posX}&posY={posY}&coordtype={coordtype} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Query Parameters]

| Name      | Type   | Required | Valid Range | Description                                                  |
| --------- | ------ | -------- | ----------- | ------------------------------------------------------------ |
| posX      | String | Required |             | X coordinates                                                |
| posY      | String | Required |             | Y coordinates                                                |
| coordtype | String | Optional |             | Requested coordinate type<br>0: TW coordinates<br>1: WGS84 coordinates<br>Search by TW coordinates, if left blank. |

#### Response

##### Body 

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
      "address": "Baekhyeon-dong, Bundang-gu, Seongnam-si, Gyeonggi-do",
      "jibun": "519-7",
      "roadname": "",
      "roadjibun": "",
      "distance": 25
    }
  }
}
```

##### Field	

| Name                   | Type    | Description                                                  |
| ---------------------- | ------- | ------------------------------------------------------------ |
| header                 | Object  | Header area                                                  |
| header.isSuccessful    | Boolean | Successful or not                                            |
| header.resultCode      | Integer | Failure code                                                 |
| header.resultMessage   | String  | Failure message                                              |
| location               | Object  | Body area                                                    |
| location.result        | Boolean | Successful or not                                            |
| location.adm           | Object  | Search result                                                |
| location.adm.posx      | String  | X coordinates                                                |
| location.adm.posy      | String  | Y coordinates                                                |
| location.adm.admcode   | String  | Administrative code                                          |
| location.adm.address   | String  | Address                                                      |
| location.adm.jibun     | String  | Land lot address                                             |
| location.adm.roadname  | String  | Road name for new address system                             |
| location.adm.roadjibun | String  | Land-lot number for new address system                       |
| location.adm.distance  | Integer | Distance from coordinates (if available)                     |
| location.adm.accuracy  | String  | Accuracy of land-lot numbers<br/>0: Search accuracy 
1: Extend the last digit of land-lot numbers
e.g.) For the search of 963-2, return the search result of 963-X.  
2 : Extend the initial digit of land-lot numbers
e.g) For the search of 963-2, return the search result of 96X 
3: Coordinates of Dong by the administrative unit 
e.g.) In case input is available only down to Sampyeong-dong
4:  Coordinates of Dong or higher unit, or administrative Dong 
e.g.) In case input is available down to Bundang-gu only |

### 3\. Integrated Search

* Search integrated information, including phone number, address, and POI data. 

#### Request

[URI]

| Method | URI                                                          |
| ------ | ------------------------------------------------------------ |
| GET    | /maps/v1.0/appkeys/{appkey}/searches&query={query}&coordtype&startposition={startposition}&reqcount={reqcount}&spopt={spopt}&radius={radius}&admcode={admcode}&depth={depth}&x1={x1}&y1={y1}&x2={x2}&y2={y2}&sortopt={sortopt}&catecode={catecode} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Query Parameters]

| Name          | Type   | Required | Valid Range | Description                                                  |
| ------------- | ------ | -------- | ----------- | ------------------------------------------------------------ |
| query         | String | Required |             | Search words                                                 |
| coordtype     | String | Optional |             | Type of coordinates <br/>0: TW coordinates
1: WGS84 coordinates
2: TM coordinates |
| startposition | String | Optional |             | Start position of search<br/>0: Initial location; query by 0, if left blank |
| reqcount      | String | Optional |             | Number of search requests<br/>Return max count, if it is set with 0 |
| spopt         | String | Optional |             | Optional space search <br/>0: Disabled 
1: Search of extent 
2: Search of range 
*Without spopt value setting, set 0. |
| radius        | String | Optional |             | Radius<br/>Enabled when the spopt value is 2
Set by meter     |
| admcode       | String | Optional |             | Administrative code                                          |
| depth         | String | Optional |             | Requirements for sub-facilities <br/>1: Request by depth 1 only (the highest depth)
2: Request by depth 2 
3: Request by depth 3 
* Set 1, if depth value is not configured 
* With depth configuration, subpoi detail information is returned for the depth, like Response as below |
| x1            | String | Optional |             | X1 coordinates<br/>X coordinate of the control point, if spopt is 0 
X coordinate on top left of Extent, if spopt is 1  
X coordinate of the control point, if spopt is 2 |
| y1            | String | Optional |             | Y1 coordinates<br/>Y coordinate of the control point, if spopt is 0
Y coordinate on top left of Extent, if spopt is 1
Y coordinate of the control point, if spopt is 2 |
| x2            | String | Optional |             | X2 coordinates<br/>X coordinate on bottom right of Extent, if spopt is 1; disabled if spopt is 2 |
| y2            | String | Optional |             | Y2 coordinates<br/>Y coordinate on bottom right of Extent, if spopt is 1; disabled if spopt is 2 |
| sortopt       | String | Optional |             | Sorting option<br/>1: Sort by name
2: Sort by distance (with coordinates)
3: Match names ->Sort by distance (with coordinates)
4: Sort by weight of a search word (for engine)
5: Sort by weight + length of a search word (for engine)
6: Sort by preferred category [V8.1.5 is not supported]
7: Sort by most-updated data 
8: Sort by weight in the order of (Landmark>Distance>PoiWeight) + distance (if coordinates are available) of a search word 
*Set 4, if sortopt is not set |
| catecode      | String | Optional |             | Preferred Category<br/>If a category name is entered for a search word, for the search of a preferred category, search is made for the search word rather than the preferred category, according to search word-first policy  
e.g.) Search Word: "Beauty salon", Preferred Category: "100000"(restaurant) ->Search is made for a beauty salon |

#### Response	

##### Body 

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
                "name1":"Samhwan HIPEX",
                "name2": "HIPIEX",
                "name3": "Samhwan HIPEX",
                "name4": "HIPEX",
                "admcode": "4113510900",
                "jibun": "678",
                "address": "Sampyeong-dong, Bundang-gu, Seongnam-si, Gyeonggi-do",
                "roadname": "Pangyoyeok-ro, Bundang-gu, Seongnam-si, Gyeonggi-do",
                "roadjibun": "240",
                "detailaddress": "",
                "catecode": "130301",
                "catename": "Company",
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
                            "name1": "Builiding A",
                            "name2": "Sanhwan HIPEX Building A",
                            "name3": "",
                            "name4": "",
                            "admcode": "4113510900",
                            "jibun": "678",
                            "address": "Sampyeong-dong, Bundang-gu, Seongnam-si, Gyeonggi-do",
                            "roadname": "Pangyoyeok-ro, Bundang-gu, Seongnam-si, Gyeonggi-do",
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
                                        "name1": "entrance",
                                        "name2": "",
                                        "name3": "",
                                        "name4": "",
                                        "admcode": "4113510900",
                                        "jibun": "678",
                                        "address": "Sampyeong-dong, Bundang-gu, Seongnam-si, Gyeonggi-do",
                                        "roadname": "",
                                        "roadjibun": "",
                                        "detailaddress": "",
                                        "catecode": "181100",
                                        "catename": "road facilities",
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

##### Field		

| Name                             | Type    | Description                                                  |
| -------------------------------- | ------- | ------------------------------------------------------------ |
| header                           | Object  | Header area                                                  |
| header.isSuccessful              | Boolean | Successful or not                                            |
| header.resultCode                | Integer | Failure code                                                 |
| header.resultMessage             | String  | Failure message                                              |
| search                           | Object  | Body area                                                    |
| search.result                    | Boolean | Successful or not                                            |
| search.type                      | Integer | 0: General search<br>1: Reference search                     |
| search.totalcount                | Integer | Total number of search results                               |
| search.count                     | Integer | Number of search results                                     |
| search.poitotalcount             | Integer | Total number of search results (Thinkware POI)               |
| search.poicount                  | Integer | Number of search results (Thinkware POI)                     |
| search.tel_poitotalcount         | Integer | Total number of search results (Tel POI)                     |
| search.tel_poicount              | Integer | Number of search results (Tel POI)                           |
| search.ucp_poitotalcount         | Integer | Total number of search results (User POI)                    |
| search.ucp_poicount              | Integer | Number of search results (User POI)                          |
| search.admtotalcount             | Integer | Total number of adm search results                           |
| search.admcount                  | Integer | Number of adm search results                                 |
| search.reftotalcount             | Integer | Total number of ref search results                           |
| search.refcount                  | Integer | Number of ref search results                                 |
| search.recommendedQuery          | String  | Provides typo correction result if search result is unavailable (NULL is available) |
| search.recommendedCost           | Integer | Typo correction result Cost (0~10000)                        |
| search.res_type                  | String  | Type name from search result <br>In the order of name, category, address, and phone number<br>(e.g.) NYNN: NO for name, YES for category, NO for address, and NO for phone number |
| search.poi                       | Array   | List of POI search results                                   |
| search.poi[0].poiid              | Integer | POI ID                                                       |
| search.poi[0].depth              | String  | POI depth                                                    |
| search.poi[0].dpx                | String  | X coordinates for display (longitude for WGS84)              |
| search.poi[0].dpy                | String  | Y coordinates for display (latitude for WGS84)               |
| search.poi[0].rpx                | String  | X coordinates for navigation (longitude for WGS84)           |
| search.poi[0].rpy                | String  | Y coordinates for navigation (latitude for WGS84)            |
| search.poi[0].name1              | String  | Official name                                                |
| search.poi[0].name2              | String  | Short name                                                   |
| search.poi[0].name3              | String  | Expanded name 1                                              |
| search.poi[0].name4              | String  | Expanded name 2                                              |
| search.poi[0].admcode            | String  | Administrative code                                          |
| search.poi[0].address            | String  | Address                                                      |
| search.poi[0].jibun              | String  | Land-lot number                                              |
| search.poi[0].roadname           | String  | Road name for new address system                             |
| search.poi[0].roadjibun          | String  | Land lot number for new address system                       |
| search.poi[0].detailaddress      | String  | Address details                                              |
| search.poi[0].catecode           | String  | Classification code                                          |
| search.poi[0].catename           | String  | Classification name                                          |
| search.poi[0].dp_catecode        | String  | DP classification code                                       |
| search.poi[0].distance           | Integer | Distance from coordinates (if available)                     |
| search.poi[0].tel                | String  | Phone number                                                 |
| search.poi[0].hasoildata         | Boolean | Availability of oil price data                               |
| search.poi[0].hasdetailinfo      | Boolean | Availability of detail information                           |
| search.poi[0].hassubpoi          | Boolean | Availability of sub-facility                                 |
| search.poi[0].adv_count          | Integer | Number of ad codes                                           |
| search.poi[0].islandmark         | Boolean | Landmark or not                                              |
| search.poi[0].updateTS           | String  | Format of last updated date (Y4-MM-DD HH:mm:ss)              |
| search.poi[0].data_source        | String  | Category of POI creation data (Thinkware/Tel/User)           |
| search.poi[0].badgeflag          | Boolean | Availability of badge (Not Yet : FALSE, Badged : TRUE)       |
| search.poi[0].userid             | String  | User ID registering POI (only for UCP)                       |
| search.poi[0].imagecount         | Integer | Number of POI images                                         |
| search.poi[0].oildata            | Object  | Oil price data                                               |
| search.poi[0].oildata.g_price    | Integer | Gas price                                                    |
| search.poi[0].oildata.hg_price   | Integer | Premium gas price                                            |
| search.poi[0].oildata.d_price    | Integer | Light oil price                                              |
| search.poi[0].oildata.l_price    | Integer | LPG price                                                    |
| search.poi[0].oildata.updatetime | String  | Updated time                                                 |
| search.poi[0].oildata.priceinfo  | String  | Highest/Lowest oil price data<br>(H: Highest, L: Lowest, X: N/A)<br>in the order of gas, premium gas, light oil, and LPG |
| search.poi[0].oildata.wash       | Boolean | Availability of car wash                                     |
| search.poi[0].oildata.fix        | Boolean | Availability of car repairs                                  |
| search.poi[0].oildata.mart       | Boolean | Availability of a store                                      |
| search.poi[0].AdInfo             | Array   | Ad code of the ad provider                                   |
| search.poi[0].AdInfo.ADCODE      | Integer | Ad codes<br>Assignable from 1 to 99 (up to 99)               |
| search.poi[0].subpoi             | Object  | Sub-facility information                                     |
| search.poi[0].subpoi.count       | Integer | Number of sub-facilities                                     |
| search.poi[0].subpoi.poi         | Array   | Same as POI information                                      |
| search.tel                       | Array   | List of TEL search results (same as POI information)         |
| search.ucp                       | Array   | List of UCP search results (same as POI information)         |
| search.adm                       | Array   | List of DM search results                                    |
| search.adm[0].type               | String  | Type of search<br>1: Search administrative system<br>2: Search land-lot number<br>3: Search new address system |
| search.adm[0].posx               | String  | X coordinates (longitude for WGS84)                          |
| search.adm[0].posy               | String  | Y coordinates (latitude for WGS84)                           |
| search.adm[0].admcode            | String  | Administrative code                                          |
| search.adm[0].address            | String  | Address                                                      |
| search.adm[0].jibun              | String  | Land-lot number                                              |
| search.adm[0].roadname           | String  | Road name for new address system                             |
| search.adm[0].roadjibun          | String  | Land-lot number for new address system                       |
| search.adm[0].accuracy           | Integer | Accuracy of land-lot numbers<br/>0: Search accuracy  
1: Extend the last digit of land-lot numbers  
2: Extend the initial digit of land-lot numbers |
| search.hasgasstation             | Boolean | Availability of oil price data                               |
| search.oilprice                  | Object  | Oil price data                                               |
| search.oilprice.max_g_price      | Integer | Highest gas price                                            |
| search.oilprice.min_g_price      | Integer | Lowest gas price                                             |
| search.oilprice.avg_g_price      | Integer | Average gas price                                            |
| search\.oilprice\.max\_hg\_price | Integer | Highest premium gas price                                    |
| search\.oilprice\.min\_hg\_price | Integer | Lowest premium gas price                                     |
| search\.oilprice\.avg\_hg\_price | Integer | Average premium gas price                                    |
| search.oilprice.max_d_price      | Integer | Highest light oil price                                      |
| search.oilprice.min_d_price      | Integer | Lowest light oil price                                       |
| search.oilprice.avg_d_price      | Integer | Average light oil price                                      |
| search.oilprice.max_l_price      | Integer | Highest LPG price                                            |
| search.oilprice.min_l_price      | Integer | Lowest LPG price                                             |
| search.oilprice.avg_l_price      | Integer | Average LPG price                                            |

### 4\. Search of Recommended Words

* Search recommended search words. 

#### Request 

[URI]

| Method | URI                                                 |
| ------ | --------------------------------------------------- |
| GET    | /maps/v1.0/appkeys/{appkey}/proposers?query={query} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Query Parameters]

| Name  | Type   | Required | Valid Range | Description                                            |
| ----- | ------ | -------- | ----------- | ------------------------------------------------------ |
| query | String | Required | 50 bytes    | 50 bytes of Korean/English/Numbers (25 Korean letters) |

#### Response		

##### Body 

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
        "keyword": "Pangyo Station",
        "frequency": 3729938
      },
      {
        "keyword": "Pangyo",
        "frequency": 3729326
      },
      {
        "keyword": "Pangyo IC",
        "frequency": 3729362
      },
      {
        "keyword": "Pangyo Library",
        "frequency": 3729514
      },
      {
        "keyword": "Pangyo One Village",
        "frequency": 3730051
      },
      {
        "keyword": "Pangyo Lottemart",
        "frequency": 3729602
      },
      {
        "keyword": "Pangyo Innovalley",
        "frequency": 3730186
      },
      {
        "keyword": "Pangyo Museum",
        "frequency": 3729654
      },
      {
        "keyword": "Pangyo Middle School",
        "frequency": 3730256
      },
      {
        "keyword": "Court by Marriott Seoul Pangyo",
        "frequency": 3729626
      }
    ]
  }
}
```

##### Field	

| Name                          | Type    | Description                        |
| ----------------------------- | ------- | ---------------------------------- |
| header                        | Object  | Header area                        |
| header.isSuccessful           | Boolean | Successful or not                  |
| header.resultCode             | Integer | Failure code                       |
| header.resultMessage          | String  | Failure message                    |
| proposer                      | Object  | Body area                          |
| proposer.result               | Boolean | Successful or not                  |
| proposer.count                | Integer | Number of recommended search words |
| proposer.keyword              | Array   | List of recommended search words   |
| proposer.keyword[0].keyword   | String  | Recommended search words           |
| proposer.keyword[0].frequency | Integer | Query frequency                    |

### 5\. Search of POI Details 

* Search details of POI. 

#### Request

[URI]

| Method | URI                                            |
| ------ | ---------------------------------------------- |
| GET    | /maps/v1.0/appkeys/{appkey}/pois?poiid={poiid} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Query Parameters]

| Name  | Type   | Required | Valid Range | Description                                                  |
| ----- | ------ | -------- | ----------- | ------------------------------------------------------------ |
| poiid | String | Required | 186         | POI ID<br>Enter poiid with the delimiter, ","<br>(multiple input is available, up to 186)<br>e.g.) poiid=123,234,567 |

#### Response		

##### Body

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
        "name1": "Hyundai Department Store(the Trade Center Store)",
        "name2": "Hyundai Department Store Trade Center",
        "name3": "Trade Center Hyundai Department Store",
        "name4": "",
        "admcode": "1168010500",
        "jibun": "159-7",
        "address": "Samseong-dong, Gangnam-gu, Seoul",
        "roadname": "Teheran-ro, Samseong 1-dong, Gangnam-gu, Seoul",
        "roadjibun": "517",
        "detailaddress": "",
        "fulladdress": "159-7 Samseong-dong, Gangnam-gu, Seoul",
        "zip": "",
        "homepage": "http://www.e-hyundai.com",
        "email": "",
        "howtogo": "",
        "tel1": "025522233",
        "tel2": "",
        "fax1": "",
        "fax2": "",
        "catecode": "110102",
        "catename": "shopping",
        "dp_catecode": "250",
        "icode": "493-070-3606",
        "externallink": [],
        "detail_count": 10,
        "etc_count": 2,
        "imagecount": 0,
        "badgeflag": false,
        "detailinfo": [
          {
            "name": "Closed Day",
            "value": "Store closed twice a month"
          },
          {
            "name": "Business Hours",
            "value": "10:30~20:00"
          },
          {
            "name": "Parking lot",
            "value": "Holds around 1400 vehicles"
          },
          {
            "name": "Parking fee",
            "value": "1-hour free ticket for a purchase worth of 10 thousand won or more"
          },
          {
            "name": "Sub-facilities 1",
            "value": "Emerald Hall(Event Hall)"
          },
          {
            "name": "Sub-facilities 2",
            "value": "Terrace garden"
          },
          {
            "name": "Size",
            "value": "10-storey building with 4 underground floors"
          },
          {
            "name": ""Floor Guide 1",
            "value": "1F Luxury Boutique/2F Fashion Accessories"
          },
          {
            "name": "Floor Guide 2",
            "value": "3F~4F Women's Fashion/6F Golf Fashion/Unisex Casual"
          },
          {
            "name": "Floor Guide 3",
            "value": "9F Restaurants/10F Cultural Space"
          }
        ],
        "etcinfo": [
          {
            "name": "Others 1",
            "value": "Located at the heart of the finanial hub of Teheran-ro"
          },
          {
            "name": "Others 2",
            "value": "The show window for the Korean commerce, satisfying global clients"
          }
        ],
        "hasoildata": false
      },
      ....
    ]
  }
}
```

##### Field	

| Name                               | Type    | Description                                                  |
| ---------------------------------- | ------- | ------------------------------------------------------------ |
| header                             | Object  | Header area                                                  |
| header.isSuccessful                | Boolean | Successful                                                   |
| header.resultCode                  | Integer | Failure code                                                 |
| header.resultMessage               | String  | Failure message                                              |
| poi                                | Object  | Body area                                                    |
| poi.result                         | Boolean | Successful or not                                            |
| poi.totalcount                     | Integer | Total number of search results                               |
| poi.count                          | Integer | Number of search results                                     |
| poi.poiinfo                        | Array   | List of POI search results                                   |
| poi.poiinfo[0].poiid               | Integer | POI ID                                                       |
| poi.poiinfo[0].dpx                 | String  | X coordinates for display (longitude for WGS84)              |
| poi.poiinfo[0].dpy                 | String  | Y coordinates for display (latitude for WGS84)               |
| poi.poiinfo[0].rpx                 | String  | X coordinates for navigation (longitude for WGS84)           |
| poi.poiinfo[0].rpy                 | String  | Y coordinates for navigation (latitude for WGS84)            |
| poi.poiinfo[0].name1               | String  | Official name                                                |
| poi.poiinfo[0].name2               | String  | Short name                                                   |
| poi.poiinfo[0].name3               | String  | Expanded name 1                                              |
| poi.poiinfo[0].name4               | String  | Expanded name 2                                              |
| poi.poiinfo[0].admcode             | String  | Administrative code                                          |
| poi.poiinfo[0].jibun               | String  | Land-lot number                                              |
| poi.poiinfo[0].address             | String  | Address                                                      |
| poi.poiinfo[0].roadname            | String  | Road name for new address system                             |
| poi.poiinfo[0].roadjibun           | String  | Land lot number for new address system                       |
| poi.poiinfo[0].detailaddress       | String  | Address details                                              |
| poi.poiinfo[0].catecode            | String  | Classification code                                          |
| poi.poiinfo[0].catename            | String  | Classification name                                          |
| poi.poiinfo[0].fulladdress         | String  | Entire address (Administrative address+land-lot number+details) |
| poi.poiinfo[0].zip                 | String  | Zip code                                                     |
| poi.poiinfo[0].homeage             | String  | URL for website                                              |
| poi.poiinfo[0].email               | String  | Email                                                        |
| poi.poiinfo[0].howtogo             | String  | How to access                                                |
| poi.poiinfo[0].tel1                | String  | Phone number 1                                               |
| poi.poiinfo[0].tel2                | String  | Phone number 2                                               |
| poi.poiinfo[0].fax1                | String  | Fax number 1                                                 |
| poi.poiinfo[0].fax2                | String  | Fax number 2                                                 |
| poi.poiinfo[0].icode               | String  | ICODE                                                        |
| poi.poiinfo[0].detail_count        | Integer | Number of detail classification items                        |
| poi.poiinfo[0].etc_count           | Integer | Number of other classification items                         |
| poi.poiinfo[0].badgeflag           | Boolean | Availability of badge (Not Yet:FALSE, Badged:TRUE)           |
| poi.poiinfo[0].imagecount          | Integer | Number of POI images                                         |
| poi.poiinfo[0].hasoildata          | Boolean | Availability of oil price data                               |
| poi.poiinfo[0].detailinfo          | Array   | Detail classification item                                   |
| poi.poiinfo[0].detailinfo[0].name  | String  | Description of detail classification item                    |
| poi.poiinfo[0].detailinfo[0].value | String  | Content of detail classification item                        |
| poi.poiinfo[0].etcinfo             | Array   | Other classification item                                    |
| poi.poiinfo[0].etcinfo[0].name     | String  | Description of other classification item                     |
| poi.poiinfo[0].etcinfo[0].value    | String  | Content of other classification item                         |
| poi.poiinfo[0].oildata             | Object  | Oil price data                                               |
| poi.poiinfo[0].oilda.tag_price     | Integer | Gas price                                                    |
| poi.poiinfo[0].oilda.hg_price      | Integer | Premium gas price                                            |
| poi.poiinfo[0].oilda.d_price       | Integer | Light oil price                                              |
| poi.poiinfo[0].oilda.l_price       | Integer | LPG price                                                    |
| poi.poiinfo[0].oilda.updatetime    | String  | Updated time                                                 |
| poi.poiinfo[0].oilda.priceinfo     | String  | Highest/Lowest oil price data<br>(H: Highest, L: Lowest, X: N/A)<br>In the order of gas, premium gas, light oil, and LPG |
| poi.poiinfo[0].oilda.wash          | Boolean | Availability of car wash                                     |
| poi.poiinfo[0].oilda.fix           | Boolean | Availability of car repairs                                  |
| poi.poiinfo[0].oilda.mart          | Boolean | Availability of a store                                      |

### 6\. Search of POI Sub-Facilities 

* Search sub-facilities for a specific POI. 

#### Request

[URI]

| Method | URI                                                          |
| ------ | ------------------------------------------------------------ |
| GET    | /maps/v1.0/appkeys/{appkey}/sub-pois?poiid={poiid}&x1={x1}&y1={y1} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Query Parameters]

| Name  | Type   | Required | Valid Range                                                  | Description                                |
| ----- | ------ | -------- | ------------------------------------------------------------ | ------------------------------------------ |
| poiid | String | Required |                                                              | POI ID<br>Multiple number is not supported |
| x1    | String | Optional | Current location or map center coordinates<br>If both X and Y coordinates are NULL or 0, distance is not calculated. |                                            |
| y1    | String | Optional | Current location or map center coordinates<br>If both X and Y coordinates are NULL or 0, distance is not calculated. |                                            |

#### Response	

##### Body 

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
        "name1": "Transfer parking lot",
        "name2": "",
        "name3": "",
        "name4": "",
        "admcode": "4113511000",
        "jibun": "",
        "address": "Baekhyeon-dong, Bundang-gu,Seongnam, Gyeonggi Province",
        "roadname": "",
        "roadjibun": "",
        "detailaddress": "",
        "catecode": "161701",
        "catename": "Parking lot",
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
        "name1": "Exit no.1",
        "name2": "",
        "name3": "",
        "name4": "",
        "admcode": "4113511000",
        "jibun": "",
        "address": "Baekhyeon-dong, Bundang-gu,Seongnam, Gyeonggi Province",
        "roadname": "",
        "roadjibun": "",
        "detailaddress": "",
        "catecode": "173000",
        "catename": "Subway",
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

##### Field	

| Name                             | Type    | Description                                                  |
| -------------------------------- | ------- | ------------------------------------------------------------ |
| header                           | Object  | Header area                                                  |
| header.isSuccessful              | Boolean | Successful or not                                            |
| header.resultCode                | Integer | Failure code                                                 |
| header.resultMessage             | String  | Failure message                                              |
| subpoi                           | Object  | Body area                                                    |
| subpoi.result                    | Boolean | Successful or not                                            |
| subpoi.totalcount                | String  | Total number of search results                               |
| subpoi.count                     | String  | Number of search results                                     |
| subpoi.poi                       | Array   | List of POI search results                                   |
| subpoi.poi[0].poiid              | Integer | POI ID                                                       |
| subpoi.poi[0].depth              | String  | POI depth                                                    |
| subpoi.poi[0].dpx                | String  | X coordinates for display (longitude for WGS84)              |
| subpoi.poi[0].dpy                | String  | Y coordinates for display (latitude for WGS84)               |
| subpoi.poi[0].rpx                | String  | X coordinates for navigation (longitude for WGS84)           |
| subpoi.poi[0].rpy                | String  | Y coordinates for navigation (latitude for WGS84)            |
| subpoi.poi[0].name1              | String  | Official name                                                |
| subpoi.poi[0].name2              | String  | Short name                                                   |
| subpoi.poi[0].name3              | String  | Expanded name1                                               |
| subpoi.poi[0].name4              | String  | Expanded name2                                               |
| subpoi.poi[0].admcode            | String  | Administrative code                                          |
| subpoi.poi[0].address            | String  | Address                                                      |
| subpoi.poi[0].jibun              | String  | Land-lot number                                              |
| subpoi.poi[0].roadname           | String  | Road name for new address system                             |
| subpoi.poi[0].roadjibun          | String  | Land-lot number for new address system                       |
| subpoi.poi[0].detailaddress      | String  | Address details                                              |
| subpoi.poi[0].catecode           | String  | Classification code                                          |
| subpoi.poi[0].catename           | String  | Classification name                                          |
| subpoi.poi[0].dp_catecode        | String  | DP classification code                                       |
| subpoi.poi[0].distance           | Integer | Distance from coordinates (if available)                     |
| subpoi.poi[0].tel                | String  | Phone number                                                 |
| subpoi.poi[0].hasoildata         | Boolean | Availability of oil price data                               |
| subpoi.poi[0].hasdetailinfo      | Boolean | Availability of detail information                           |
| subpoi.poi[0].hassubpoi          | Boolean | Availability of sub-facilities                               |
| subpoi.poi[0].adv_count          | Boolean | Number of ad codes                                           |
| subpoi.poi[0].islandmark         | Boolean | Landmark or not                                              |
| subpoi.poi[0].updateTS           | String  | Format of last updated date and time (Y4-MM-DD HH:mm:ss)     |
| subpoi.poi[0].data_source        | String  | Category of POI creation data (Thinkware/Tel/User)           |
| subpoi.poi[0].badgeflag          | Boolean | Availability of badge (Not Yet: FALSE, Badged: TRUE)         |
| subpoi.poi[0].userid             | String  | User ID for POI registration (only for UCP)                  |
| subpoi.poi[0].imagecount         | Integer | Number of POI images                                         |
| subpoi.poi[0].oildata            | Object  | Oil price data                                               |
| subpoi.poi[0].oildata.g_price    | Integer | Gas price                                                    |
| subpoi.poi[0].oildata.hg_price   | Integer | Premium gas price                                            |
| subpoi.poi[0].oildata.d_price    | Integer | Light oil price                                              |
| subpoi.poi[0].oildata.l_price    | Integer | LPG price                                                    |
| subpoi.poi[0].oildata.updatetime | String  | Updated time                                                 |
| subpoi.poi[0].oildata.priceinfo  | String  | Highest/Lowest oil price data<br>(H: Highest, L: Lowest, X: N/A)<br>In the order of gas, premium gas, light oil, and LPG |
| subpoi.poi[0].oildata.wash       | Boolean | Availability of car wash                                     |
| subpoi.poi[0].oildata.fix        | Boolean | Availability of car repairs                                  |
| subpoi.poi[0].oildata.mart       | Boolean | Availability of a store                                      |
| subpoi.poi[0].AdInfo             | Array   | List of ad codes                                             |
| subpoi.poi[0].AdInfo[0].ADCODE   | Integer | Ad codes<br>Assignable from 1 to 99 (up to 99)               |
| subpoi.poi[0].subpoi             | Object  | Sub-facility data                                            |
| subpoi.poi[0].subpoi.count       | Integer | Number of subpois                                            |
| subpoi.poi[0].subpoi.poi         | Array   | Same as POI information                                      |

### 7\. Conversion of Coordinates

* Return conversion value between WGS84 <-> TM coordinates. 

#### Request

[URI]

| Method | URI                                                          |
| ------ | ------------------------------------------------------------ |
| GET    | /maps/v1.0/appkeys/{appkey}/trans-coordinates?coordtype={coordtype}&x={x}&y={y} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Query Parameters]

| Name      | Type   | Required | Valid Range                                                  | Description                          |
| --------- | ------ | -------- | ------------------------------------------------------------ | ------------------------------------ |
| coordtype | String | Required |                                                              | 0 : WGS84 -> TM <br> 1 : TM -> WGS84 |
| x         | double | Required | Current location or map center coordinates<br>WGS84 or TM coordinates |                                      |
| y         | double | Required | Current location or map center coordinates<br>WGS84 or TM coordinates |                                      |

#### Response	

##### Body

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

##### Field	

| Name               | Type   | Description |
| -------------------- | ------- | -------- |
| header               | Object  | Header area |
| header.isSuccessful  | Boolean | Successful or not |
| header.resultCode    | Integer | Failure code |
| header.resultMessage | String  | Failure message |
| coordinate           | Object  | Body area |
| coordinate.coordtype | String  | Conversion type of coordinates |
| coordinate.x         | String  | X coordinates for conversion |
| coordinate.y         | String  | Y coordinates for conversion |

## Navigate 

### 1\. Summary of Route Navigation 

* Search summary information on route navigation results for coordinates.

#### Request

[URI]

| Method | URI                                                          |
| ------ | ------------------------------------------------------------ |
| GET    | /maps/v1.0/appkeys/{appkey}/routes?startX={startX}&startY={startY}&endX={endX}&endY={endY}&viaCount={viaCount}&via1X={via1X}&via1Y={via1Y}&via2X={via2X}&via2Y={via2Y}&option={option} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Query Parameters]

| Name     | Type   | Required | Valid Range | Description                                                  |
| -------- | ------ | -------- | ----------- | ------------------------------------------------------------ |
| startX   | String | Required |             | X coordinates at departure                                   |
| startY   | String | Required |             | Y coordinates at departure                                   |
| endX     | String | Required |             | X coordinates at destination                                 |
| endY     | String | Required |             | Y coordinates at destination                                 |
| viaCount | String | Optional |             | Number of stopovers                                          |
| via1X    | String | Optional |             | X coordinates at stopover 1                                  |
| via1Y    | String | Optional |             | Y coordinates at stopover 1                                  |
| via2X    | String | Optional |             | X coordinates at stopover 2                                  |
| via2Y    | String | Optional |             | Y coordinates at stopover 2                                  |
| option   | String | Required |             | Optional route navigation <br>Request by the navigation option, "," br>ex\) option=real\_traffic\,real\_traffic2<br>freeroad_priority: Free<br>highway_priority: Highway<br>real_traffic: Real-time<br>real\_traffic\_freeroad: Real-time \(free\)<br>real_traffic: Recommendation 1<br>real_traffic2: Recommendation 2<br>rt_stats: Real-time statistics<br>rt\_stats\_freeroad: Real-time statistics \(free\)<br>short\_distance\_priority: Short distance<br>stats: Statistics<br>stats_freeroad: Statistics (free)<br>motorcycle: Two-wheeler |

#### Response

##### Body

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

##### Field

| Name                     | Type    | Description                             |
| ------------------------ | ------- | --------------------------------------- |
| header                   | Object  | Header area                             |
| header.isSuccessful      | Boolean | Successful or not                       |
| header.resultCode        | Integer | Failure code                            |
| header.resultMessage     | String  | Failure message                         |
| route                    | Object  | Body area                               |
| route.SummaryResult      | Array   | List of route request result            |
| route.SummaryResult[0].0 | String  | Name of option                          |
| route.SummaryResult[0].1 | Integer | Distance of route navigation (unit: m)  |
| route.SummaryResult[0].2 | Integer | Time of route navigation (unit: minute) |

### 2\. Route Navigation Details 

* Search detail information of route navigation results on coordinates. 

#### Request

[URI]

| Method | URI                                                          |
| ------ | ------------------------------------------------------------ |
| GET    | /maps/v1.0/appkeys/{appkey}/route-details?startX={startX}&startY={startY}&endX={endX}&endY={endY}&viaCount={viaCount}&via1X={via1X}&via1Y={via1Y}&via2X={via2X}&via2Y={via2Y}&option={option} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Query Parameters]

| Name     | Type   | Required | Valid Range | Description                                                  |
| -------- | ------ | -------- | ----------- | ------------------------------------------------------------ |
| startX   | String | Required |             | X coordinates at departure                                   |
| startY   | String | Required |             | Y coordinates at departure                                   |
| endX     | String | Required |             | X coordinates at destination                                 |
| endY     | String | Required |             | Y coordinates at destination                                 |
| viaCount | String | Optional |             | Number of stopovers                                          |
| via1X    | String | Optional |             | X coordinates at stopover 1                                  |
| via1Y    | String | Optional |             | Y coordinates at stopover 1                                  |
| via2X    | String | Optional |             | X coordinates at stopover 2                                  |
| via2Y    | String | Optional |             | Y coordinates at stopover 2                                  |
| option   | String | Required |             | Optional route navigation<br>Only one navigation option is available<br>e.g.) option=real_traffic<br>freeroad_priority: Free<br>highway_priority: Highway<br>real_traffic: Real-time<br>real\_traffic\_freeroad: Real-time \(free\)<br>real_traffic: Recommendation 1<br>real_traffic2: Recommendation 2<br>rt_stats: Real-time statistics<br>rt\_stats\_freeroad: Real-time statistics \(free\)<br>short\_distance\_priority: Short distance<br>stats: Statistics<br>stats_freeroad: Statistics (free)<br>motorcycle: Two-wheeer |

#### Response

##### Body 

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
      "National Road",
      "Pangyoyeok-ro 242beon-gil",
      "Pangyoyeok-ro 226beon-gil",
      "Natioal Road",
      "Daewangpangyo-ro 644beon-gil",
      "Turn riht",
      "Turn right",
      "Turn right",
      "Pangyo (Pangyo Techno Valley) station, Baekhyeon-dong"
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

##### Field	

| Name                        | Type    | Description                                                  |
| --------------------------- | ------- | ------------------------------------------------------------ |
| header                      | Object  | Header area                                                  |
| header.isSuccessful         | Boolean | Successful or not                                            |
| header.resultCode           | Integer | Failure code                                                 |
| header.resultMessage        | String  | Failure message                                              |
| routeDetail                 | Object  | Body area                                                    |
| RouteInfo                   | Object  | Route information                                            |
| RouteInfo.dist              | Integer | Total length of a route (Unit: m)                            |
| RouteInfo.time              | Integer | Total required time for a route (unit: minute)               |
| RouteInfo.sec_cnt           | Integer | Number of section information records                        |
| RouteInfo.dtl_cnt           | Integer | Number of section detail records                             |
| RouteInfo\.rd\_name\_cnt    | Integer | Number of road name records                                  |
| RouteInfo\.guide\_name\_cnt | Integer | Number of guide name records                                 |
| RouteInfo\.cross\_name\_cnt | Integer | Number of intersection name records                          |
| RouteInfo\.dir\_name\_cnt   | Integer | Number of direction name records                             |
| RouteInfo.vtx_cnt           | Integer | Number of interpolation points (route vector coordinates)    |
| RouteInfo.rest_cnt          | Integer | Number of rest areas                                         |
| RouteInfo.toll_cnt          | Integer | Number of toll gates                                         |
| RouteInfo.max_x             | Integer | Maximum x coordinates among interpolation point records      |
| RouteInfo.max_y             | Integer | Maximum y coordinates among interpolation point records      |
| RouteInfo.min_x             | Integer | Minimum x coordinates among interpolation point records      |
| RouteInfo.min_y             | Integer | Minimum y coordinates among interpolation point records      |
| SecInfoRec                  | Array   | Section information records                                  |
| SecInfoRec[0].0             | Integer | Distance of section (meter)                                  |
| SecInfoRec[0].1             | Integer | Speed of section                                             |
| SecInfoRec[0].2             | Integer | Road number or road name index                               |
| SecInfoRec[0].3             | String  | Number of detail section information records                 |
| SecInfoRec[0].4             | String  | Table index for section details                              |
| DtlInfoRec                  | Array   | Record of section details                                    |
| DtlInfoRec[0].0             | Integer | Detail distance of section                                   |
| DtlInfoRec[0].1             | Integer | Detail speed of section                                      |
| DtlInfoRec[0].2             | String  | Guide name index                                             |
| DtlInfoRec[0].3             | String  | Intersection name index                                      |
| DtlInfoRec[0].4             | String  | Direction name index                                         |
| DtlInfoRec[0].5             | String  | By road type                                                 |
| DtlInfoRec[0].6             | Integer | Interpolation point at guide point index                     |
| NameRec                     | Array   | Name record                                                  |
| NameRec[0].0                | String  | Highway Name or Guide Name or Intersection Name or Direction Name |
| VtxRec                      | Array   | Array of coordinates for interpolation record - route vector <br>[[twX1, twY1], [twX2, twY2], … [twXn, twYn]] |
| VtxRec[0].0                 | Integer | twX                                                          |
| VtxRec[0].1                 | Integer | twY                                                          |
| RestRec                     | Array   | Name record                                                  |
| RestRec[0].0                | String  | High-speed mode code                                         |
| RestRec[0].1                | String  | Gas station code<br>(0: N/A, 1: LG, 2: SK, 3: Ssang-yong, 4: Hanhwa, 5: Hyundai) |
| RestRec[0].2                | String  | Availability of LPG <br>[0: N/A, 1: Available]               |
| RestRec[0].3                | String  | Availability of repair shop <br>[0: N/A, 1: Available]       |
| RestRec[0].4                | String  | High-speed mode                                              |
| RestRec[0].5                | String  | Reserved                                                     |
| RestRec[0].6                | String  | Name of rest area                                            |

### 3\.  Route Navigation Details \(json Parsing\)

#### Parsing for easy view of route navigation results 

```
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v1.0/route.js" > </script>
<script type="text/javascript">
function fnRouteParse(data){ // Detail result of route navigation 

  var routeParsing = route.jsonParsing(data);
  routeParsing.routeSummaryInfo;		// Summary of navigation results 
  routeParsing.routeDetailInfo;		// List of navigation routes 
  routeParsing.vtxInfo; 			// List of coordinates for map drawing 
}
</script>
```

#### Field

| Name                            | Type    | Description                                             |
| ------------------------------- | ------- | ------------------------------------------------------- |
| routeSummaryInfo                | Object  | Summary of navigation results                           |
| routeSummaryInfo.distance       | Integer | Total length of route (unit: m)                         |
| routeSummaryInfo.time           | Integer | Total time required for route (unit: minute)            |
| routeSummaryInfo.max_x          | String  | Maximum x coordinates among interpolation point records |
| routeSummaryInfo.max_y          | String  | Maximum y coordinates among interpolation point records |
| routeSummaryInfo.min_x          | String  | Minimum x coordinates among interpolation point records |
| routeSummaryInfo.min_y          | String  | Minimum y coordinates among interpolation point records |
| routeDetailInfo                 | Array   | List of navigation routes                               |
| routeDetailInfo.distance        | Integer | Detail section distance (unit: m)                       |
| routeDetailInfo.speed           | Integer | Detail section speed (unit: km/h)                       |
| routeDetailInfo.roadName        | String  | Road name                                               |
| routeDetailInfo.direction       | String  | Direction information                                   |
| routeDetailInfo.district        | String  | District information                                    |
| routeDetailInfo.cross           | String  | Guide information                                       |
| routeDetailInfo.directionDetail | String  | Description of route details                            |
| vtxInfo                         | Array   | List of coordinates for map drawing                     |
| vtxInfo[0].0                    | Integer | twX                                                     |
| vtxInfo[0].1                    | Integer | twY                                                     |