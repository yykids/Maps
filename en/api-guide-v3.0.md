## Application Service > Maps > API User Guide v3.0

Describes the Search by iNavi's historic engine technology, Geocoding, Reverse Geocoding, Route Navigation (Getting Directions), and Static Map API.

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

#### Search API

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

### 1\. Integrated Search

* Search integrated information on key words, such as business name, phone number, and address.

#### Request

[URI]

| Method | URI                                                          |
| ------ | ------------------------------------------------------------ |
| GET    | /maps/v3.0/appkeys/{appkey}/searches&query={query}&coordtype&startposition={startposition}&reqcount={reqcount}&spopt={spopt}&radius={radius}&admcode={admcode}&depth={depth}&x1={x1}&y1={y1}&x2={x2}&y2={y2}&sortopt={sortopt}&catecode={catecode} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Query Parameters]

| Name          | Type   | Required | Valid Range | Description                                                  |
| ------------- | ------ | -------- | ----------- | ------------------------------------------------------------ |
| query         | String | Required |             | Search word                                                  |
| coordtype     | String | Optional |             | Type of coordinates <br>0: TW coordinates<br>1: WGS84 coordinates<br>2: TM coordinates |
| startposition | String | Optional |             | Start position of search<br>0: Initial location; query by 0, if left blank |
| reqcount      | String | Optional |             | Number of search requests<br>Return max count, if it is set with 0 |
| spopt         | String | Optional |             | Optional space search <br>0: Disabled <br>1: Search of extent <br>2: Search of range <br>*Without spopt value setting, set 0. |
| radius        | String | Optional |             | Radius<br>Enabled when the spopt value is 2<br>Set by meter  |
| admcode       | String | Optional |             | Administrative code                                          |
| depth         | String | Optional |             | Requirements for sub-facilities <br>1: Request by depth 1 only (the highest depth)<br>2: Request by depth 2 <br>3: Request by depth 3 <br>* Set 1, if depth value is not configured <br>* With depth configuration, subpoi detail information is returned for the depth, like Response as below |
| x1            | String | Optional |             | X1 coordinates<br>X coordinate of the control point, if spopt is 0 <br>X coordinate on top left of Extent, if spopt is 1  <br>X coordinate of the control point, if spopt is 2 |
| y1            | String | Optional |             | Y1 coordinates<br>Y coordinate of the control point, if spopt is 0<br>Y coordinate on top left of Extent, if spopt is 1<br>Y coordinate of the control point, if spopt is 2 |
| x2            | String | Optional |             | X2 coordinates<br>X coordinate on bottom right of Extent, if spopt is 1; disabled if spopt is 2 |
| y2            | String | Optional |             | Y2 coordinates<br>Y coordinate on bottom right of Extent, if spopt is 1; disabled if spopt is 2 |
| sortopt       | String | Optional |             | Sorting option<br>1: Sort by name<br>2: Sort by distance (with coordinates)<br>3: Match names ->Sort by distance (with coordinates)<br>4: Sort by weight of a search word (for engine)<br>5: Sort by weight + length of a search word (for engine)<br>6: Sort by preferred category [V8.1.5 is not supported]<br>7: Sort by most-updated data <br>8: Sort by weight in the order of (Landmark>Distance>PoiWeight) + distance (if coordinates are available) of a search word <br>*Set 4, if sortopt is not set |


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
                "name1": "Samhwan HIPEX",
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
                "catename": "company",
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
                            "catename": "company",
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

| Name                           | Type   | Description                             |
| -------------------------------- | ------- | ---------------------------------------- |
| header                           | Object  | Header area                         |
| header.isSuccessful              | Boolean | Successful or not                    |
| header.resultCode                | Integer | Failure code                         |
| header.resultMessage             | String  | Failure message                     |
| search                           | Object  | Body area                            |
| search.result                    | Boolean | Successful or not                    |
| search.type                      | Integer | 0: General search<br>1: Search for reference |
| search.totalcount                | Integer | Total number of search results |
| search.count                     | IntegerS | Number of search results |
| search.poitotalcount             | Integer | Total number of search results (Thinkware POI) |
| search.poicount                  | Integer | Number of search results (Thinkware POI) |
| search.tel_poitotalcount         | Integer | Total number of search results (Tel POI) |
| search.tel_poicount              | Integer | Number of search results (Tel POI) |
| search.ucp_poitotalcount         | Integer | Total number of search results (User POI) |
| search.ucp_poicount              | Integer | Number of search results (User POI) |
| search.admtotalcount             | Integer | Total number of ADM search results |
| search.admcount                  | Integer | Number of ADM search results     |
| search.reftotalcount             | Integer | Total number of ref search results |
| search.refcount                  | Integer | Number of ref search results    |
| search.res_type                  | String  | Name of search result type<br>In the order of Name, Category, Address, and Phone Number<br/>(e.g.) NYNN: No for name, Yes for category, No for address, and No for phone number |
| search.poi                       | Array   | List of POI search results      |
| search.poi[0].poiid              | Integer | POI ID                                   |
| search.poi[0].depth              | String  | POI depth                                |
| search.poi[0].dpx                | String  | X coordinates for display (longitude for WGS84) |
| search.poi[0].dpy                | String  | Y coordinates for display (latitude for WGS84) |
| search.poi[0].rpx                | String  | X coordinates for navigation (longitude for WGS84) |
| search.poi[0].rpy                | String  | Y coordinates for navigation (latitude for WGS84) |
| search.poi[0].name1              | String  | Official name                       |
| search.poi[0].name2              | String  | Short name                         |
| search.poi[0].name3              | String  | Expanded name 1                 |
| search.poi[0].name4              | String  | Expanded name 2                     |
| search.poi[0].admcode            | String  | Administrative code                |
| search.poi[0].address            | String  | Address                                |
| search.poi[0].jibun              | String  | Land-lot number                       |
| search.poi[0].roadname           | String  | Road name for new address system |
| search.poi[0].roadjibun          | String  | Land-lot number for new address system |
| search.poi[0].detailaddress      | String  | Address details                    |
| search.poi[0].catecode           | String  | Classification code               |
| search.poi[0].catename           | String  | Classification name               |
| search.poi[0].dp_catecode        | String  | DP classification code             |
| search.poi[0].distance           | Integer | Distance from coordinates (if available) |
| search.poi[0].tel                | String  | Phone number                         |
| search.poi[0].hasoildata         | Boolean | Availabilty of oil price data         |
| search.poi[0].hasdetailinfo      | Boolean | Availability of detail information       |
| search.poi[0].hassubpoi          | Boolean | Availabiliy of sub-facilities           |
|| search.poi[0].islandmark         | Boolean |
| search.poi[0].updateTS           | String  | Format of last updated date and time (Y4-MM-DD HH:mm:ss) |
| search.poi[0].imagecount         | Integer | Number of POI images            |
| search.poi[0].oildata            | Object  | Oil price data                  |
| search.poi[0].oildata.g_price    | Integer | Gas price                            |
| search.poi[0].oildata.hg_price   | Integer | Premium gas price                       |
| search.poi[0].oildata.d_price    | Integer | Light oil price                          |
| search.poi[0].oildata.l_price    | Integer | LPG price                              |
| search.poi[0].oildata.updatetime | String  | Updated time                             |
| search.poi[0].oildata.priceinfo  | String  | Highest/Lowest oil price data<br/>(H: Highest, L: Lowest, X: N/A)
in the order of gas, premium gas, light oil, and LPG |
| search.poi[0].oildata.wash       | Boolean | Availability of car wash       |
| search.poi[0].oildata.fix        | Boolean | Availability of car repairs     |
| search.poi[0].oildata.mart       | Boolean | Availability of a store        |
| search.poi[0].subpoi             | Object  | Sub-facility information       |
| search.poi[0].subpoi.count       | Integer | Number of sub-facilities      |
| search.poi[0].subpoi.poi         | Array   | Same as POI information           |
| search.tel                       | Array   | List of TEL search results (same on POI information) |
| search.adm                       | Array   | List of ADM search results |
| search.adm[0].type               | String  | Type of search<br>1: Search administrative system<br>2: Search land-lot number<br>3: Search new address |
| search.adm[0].posx               | String  | X coordinates (longitude for WGS84) |
| search.adm[0].posy               | String  | Y coordinates (latitude for WGS84) |
| search.adm[0].admcode            | String  | Administrative code                 |
| search.adm[0].address            | String  | Address                               |
| search.adm[0].jibun              | String  | Land-lot number                       |
| search.adm[0].roadname           | String  | Road name for new address system |
| search.adm[0].roadjibun          | String  | Land-lot number for new address system |
| search.adm[0].accuracy           | Integer | Accuracy of land-lot numbers<br>0: Search accuracy  <br>1: Extend the last digit of land-lot numbers  <br>2: Extend the initial digit of land-lot numbers |
| search.hasgasstation             | Boolean | Availability of oil price data |
| search.oilprice                  | Object  | Oil price data                     |
| search.oilprice.max_g_price      | Integer | Highest gas price          |
| search.oilprice.min_g_price      | Integer | Lowest gas price              |
| search.oilprice.avg_g_price      | Integer | Average gas price                        |
| search\.oilprice\.max\_hg\_price | Integer | Highest premium gas price                |
| search\.oilprice\.min\_hg\_price | Integer | Lowest premium gas price   |
| search\.oilprice\.avg\_hg\_price | Integer | Average premium gas price                |
| search.oilprice.max_d_price      | Integer | Highest light oil price          |
| search.oilprice.min_d_price      | Integer | Lowest light oil price                   |
| search.oilprice.avg_d_price      | Integer | Average light oil price                  |
| search.oilprice.max_l_price      | Integer | Highest LPG price                        |
| search.oilprice.min_l_price      | Integer | Lowest LPG price                       |
| search.oilprice.avg_l_price      | Integer | Average LPG price                        |


### 2\. Search of Recommended Words

* Search recommended words of a search word.

#### Request

[URI]

| Method | URI                                                 |
| ------ | --------------------------------------------------- |
| GET    | /maps/v3.0/appkeys/{appkey}/proposers?query={query} |

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
        "keyword": "Courtyard by Marriott Seoul Pangyo",
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

### 3\. Search of POI Details

* Search details of POI.

#### Request

[URI]

| Method | URI                                            |
| ------ | ---------------------------------------------- |
| GET    | /maps/v3.0/appkeys/{appkey}/pois?poiid={poiid} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Query Parameters]

| Name  | Type   | Required | Valid Range | Description                                                  |
| ----- | ------ | -------- | ----------- | ------------------------------------------------------------ |
| poiid | String | Required | 186         | POI ID<br>Enter poiid, along with the delimiter, ","<br>(multiple input is available up to 186)<br>e.g.) poiid=123,234,567 |

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
				"poiid": 510835.0,
        "dpx": "127.059664",
        "dpy": "37.508629",
        "rpx": "127.059089",
        "rpy": "37.508779",
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
            "name": "Floor Guide 1",
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
| header.isSuccessful                | Boolean | Successful or not                                            |
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
| poi.poiinfo[0].roadjibun           | String  | Land-lot number for new address system                       |
| poi.poiinfo[0].detailaddress       | String  | Address details                                              |
| poi.poiinfo[0].catecode            | String  | Classification code                                          |
| poi.poiinfo[0].catename            | String  | Classification name                                          |
| poi.poiinfo[0].fulladdress         | String  | Entire address (administrative address+ land-lot number+details) |
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
| poi.poiinfo[0].imagecount          | Integer | Number of POI images                                         |
| poi.poiinfo[0].hasoildata          | Boolean | Availability of oil data                                     |
| poi.poiinfo[0].detailinfo          | Array   | Detail classification item                                   |
| poi.poiinfo[0].detailinfo[0].name  | String  | Description of detail classification item                    |
| poi.poiinfo[0].detailinfo[0].value | String  | 분류 상세 항목 내용 Content of detail classification item    |
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

### 4\. Search of POI Sub-Facilities

* Search sub-facilities for a specific POI.

#### Request

[URI]

| Method | URI                                                          |
| ------ | ------------------------------------------------------------ |
| GET    | /maps/v3.0/appkeys/{appkey}/sub-pois?poiid={poiid}&x1={x1}&y1={y1} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Query Parameters]

| Name  | Type   | Required | Valid Range                                                  | Description                                |
| ----- | ------ | -------- | ------------------------------------------------------------ | ------------------------------------------ |
| poiid | String | Required |                                                              | POI ID<br>Multiple number is not supported |
| x1    | String | Optional | Current location or map center coordinates<br>If both X and Y coordinates are NULL or 0, distance is not calculated. |                                            |
| y1    | String | Optional | Current location or map center coordinates <br>If both X and Y coordinates are NULL or 0, distance is not calculated. |                                            |

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
                "name1": "Main entrance",
                "name2": "Thinkware entrance",
                "name3": "",
                "name4": "",
                "admcode": "4113510900",
                "jibun": "678",
                "address": "Sampyeong-dong, Bundang-gu, Seongnam, Gyeonggi Province",
                "roadname": "Pangyoyeok-ro, Bundang-gu, Seongnam, Gyeonggi Province",
                "roadjibun": "240",
                "detailaddress": "",
                "catecode": "181100",
                "catename": "Road facilities",
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

##### Field

| Name                           | Type   | Description                             |
| -------------------------------- | ------- | ---------------------------------------- |
| header                           | Object  | Header area                          |
| header.isSuccessful              | Boolean | Successful or not                    |
| header.resultCode                | Integer | Failure code                  |
| header.resultMessage             | String  | Failure message                      |
| subpoi                           | Object  | Body area                            |
| subpoi.result                    | Boolean | Successful or not                    |
| subpoi.totalcount                | Integer  | Total number of search results |
| subpoi.count                     | Integer  | Number of search results |
| subpoi.poi                       | Array   | List of POI search results     |
| subpoi.poi[0].poiid              | Integer | POI ID                                   |
| subpoi.poi[0].depth              | String  | POI depth                                |
| subpoi.poi[0].dpx                | String  | X coordinates for display (longtitude for WGS84) |
| subpoi.poi[0].dpy                | String  | Y coorinates for display (latitude for WGS84) |
| subpoi.poi[0].rpx                | String  | X coordinates for navigation (longtitude for WGS84) |
| subpoi.poi[0].rpy                | String  | Y coordinates for navigation (latitude for WGS84) |
| subpoi.poi[0].name1              | String  | Official name                        |
| subpoi.poi[0].name2              | String  | Short name                           |
| subpoi.poi[0].name3              | String  | Expanded name 1                      |
| subpoi.poi[0].name4              | String  | Expanded name 2                      |
| subpoi.poi[0].admcode            | String  | Administrative code                  |
| subpoi.poi[0].address            | String  | Address                                |
| subpoi.poi[0].jibun              | String  | Land-lot number                       |
| subpoi.poi[0].roadname           | String  | Road name for new address system |
| subpoi.poi[0].roadjibun          | String  | Land-lot number for new address system |
| subpoi.poi[0].detailaddress      | String  | Address details                      |
| subpoi.poi[0].catecode           | String  | Classification code                |
| subpoi.poi[0].catename           | String  | Classfication name                 |
| subpoi.poi[0].dp_catecode        | String  | DP classification code               |
| subpoi.poi[0].distance           | Integer | Distance from coordinates (if available) |
| subpoi.poi[0].tel                | String  | Phone number                        |
| subpoi.poi[0].hasoildata         | Boolean | Availability of oil price data |
| subpoi.poi[0].hasdetailinfo      | Boolean | Availability of detail information |
| subpoi.poi[0].hassubpoi          | Boolean | Availability of sub-facilities |
| subpoi.poi[0].adv_count          | Boolean | Number of ad codes               |
| subpoi.poi[0].islandmark         | Boolean | Landmark or not                  |
| subpoi.poi[0].updateTS           | String  | Format of last updated date and time (Y4-MM-DD HH:mm:ss) |
| subpoi.poi[0].data_source        | String  | Category of POI creation data (Thinkware/Tel/User) |
| subpoi.poi[0].badgeflag          | Boolean | Availability of badge (Not Yet: FALSE, Badged: TRUE) |
| subpoi.poi[0].userid             | String  | User ID for POI registration (only for UCP) |
| subpoi.poi[0].imagecount         | Integer | Number of POI images           |
| subpoi.poi[0].oildata            | Object  | Oil price data                          |
| subpoi.poi[0].oildata.g_price    | Integer | Gas price                           |
| subpoi.poi[0].oildata.hg_price   | Integer | Premium gas price                        |
| subpoi.poi[0].oildata.d_price    | Integer | Light oil price                     |
| subpoi.poi[0].oildata.l_price    | Integer | LPG price                                |
| subpoi.poi[0].oildata.updatetime | String  | Updated time                             |
| subpoi.poi[0].oildata.priceinfo  | String  | Highest/Lowest oil price data<br/>(H: Highest, L: Lowest, X: N/A)
In the order of gas, premium gas, light oil, and LPG |
| subpoi.poi[0].oildata.wash       | Boolean | Availability of car wash           |
| subpoi.poi[0].oildata.fix        | Boolean | Availability of car repairs        |
| subpoi.poi[0].oildata.mart       | Boolean | Availability of a store              |
| subpoi.poi[0].AdInfo             | Array   | List of ad codes                 |
| subpoi.poi[0].AdInfo[0].ADCODE   | Integer | Ad codes<br/>Assignable from 1 to 99 (up to 99) |
| subpoi.poi[0].subpoi             | Object  | Sub-facility data            |
| subpoi.poi[0].subpoi.count       | Integer | Number of subpois               |
| subpoi.poi[0].subpoi.poi         | Array   | Same as POI information        |

### 5\. Conversion of Coordinates

* Return conversion value between WGS84 <-> TM coordinates.

#### Request

[URI]

| Method | URI                                                          |
| ------ | ------------------------------------------------------------ |
| GET    | /maps/v3.0/appkeys/{appkey}/trans-coordinates?coordtype={coordtype}&x={x}&y={y} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Query Parameters]

| Name      | Type   | Required | Valid Range                                                  | Description                          |
| --------- | ------ | -------- | ------------------------------------------------------------ | ------------------------------------ |
| coordtype | String | Required |                                                              | 0 : WGS84 -> TM <br> 1 : TM -> WGS84 |
| x         | String | Required | Current location or map center coordinates<br/>WGS84 or TM coordinates |                                      |
| y         | String | Required | Current location or map center coordinates<br/>WGS84 or TM coordinates |                                      |

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


### 6\. 주변 카테고리 검색

* 기준 좌표를 기준으로 주변 카테고리 검색기능을 지원합니다.

#### 요청

[URI]

| 메서드  | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/nearby-category-searches?depth={depth}&x1={x1}&y1={y1}&x2={x2}&y2={y2}&radius={radius}&catecode={catecode}&coordtype={coordtype}&reqcount={reqcount}  |

[Path parameter]

| 이름     | 타입     | 필수 여부 | 유효 범위 | 설명     |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 필수    |       | 고유의 앱키 |

[Query Parameters]

| 이름        | 타입     | 필수 여부 |  설명                                   |
| --------- | ------ | ----- |  ------------------------------------ |
| depth | Integer | 필수    | 0 : 전체 depth <br> 1 : depth1 <br> 2 : depth2 <br> 3 : depth3|
| spopt         | Integer | 필수   | 1 : Extent(x1,y1,x2,y2) <br> 2 : 반경검색(x1,y1,radius)                                   |
| catecode         | String | 필수   | 카테고리 코드 |
| x1         | String | 필수(spopt 참조)    | 기준 X1좌표 |
| y1         | String | 필수(spopt 참조)    | 기준 Y1좌표 |
| x2         | String | 필수(spopt 참조)    | 기준 X2좌표 |
| y2         | String | 필수(spopt 참조)    | 기준 Y2 좌표 |
| radius         | String | 필수(spopt 참조)    | 반경(m) |

#### 응답

##### 응답 본문

```
{
    "cate": {
        "result": true,
        "totalcount": 7,
        "count": 1,
        "poi": [
            {
                "poiid": 717788,
                "depth": 0,
                "dpx": "127.110762",
                "dpy": "37.402184",
                "rpx": "127.110862",
                "rpy": "37.402334",
                "name1": "팅크웨어(주)",
                "name2": "아이나비(본사)",
                "name3": "THINKWARE",
                "name4": "INAVI",
                "admcode": "4113510900",
                "jibun": "678",
                "address": "경기도 성남시 분당구 삼평동",
                "roadname": "경기도 성남시 분당구 판교역로",
                "roadjibun": "240",
                "detailaddress": "삼환하이펙스 A동 8층,9층",
                "catecode": "130600",
                "catename": "기업",
                "dp_catecode": "000",
                "userid": "",
                "imagecount": 0,
                "userimagecount": 0,
                "badgeflag": false,
                "distance": 40,
                "tel": "15774242",
                "islandmark": true,
                "visitscore": "7.12",
                "landmarkscore": "10",
                "popularity": false,
                "pop_tv": false,
                "pop_sns": false,
                "pop_hot": false,
                "pop_hit": false,
                "pop_top": "경기_,분당구_2",
                "updateTS": "2019-05-02 00:00:00",
                "hasoildata": false,
                "hasdetailinfo": true,
                "hassubpoi": true,
                "subpoi": {
                    "count": 1
                }
            }
        ],
        "hasgasstation": false
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### 필드

##### 필드

| 이름                                 | 타입      | 설명                                       |
| ---------------------------------- | ------- | ---------------------------------------- |
| header                             | Object  | 헤더 영역                                    |
| header.isSuccessful                | Boolean | 성공 여부                                    |
| header.resultCode                  | Integer | 실패 코드                                    |
| header.resultMessage               | String  | 실패 메시지                                   |
| cate                                | Object  | 본문 영역                                    |
| cate.result                         | Boolean | 성공 여부                                    |
| cate.totalcount                     | Integer | 전체 검색 결과 대상 개수                           |
| cate.count                          | Integer | 검색 결과 개수                                 |
| cate.poi                        | Array   | POI 검색 결과 목록                             |
| cate.poi[0].poiid               | Integer | POI ID                                   |
| cate.poi[0].dpx                 | String  | display X 좌표(WGS84의 경우 longitude)         |
| cate.poi[0].dpy                 | String  | display Y 좌표(WGS84의 경우 latitude)          |
| cate.poi[0].rpx                 | String  | 탐색 X 좌표(WGS84의 경우 longitude)              |
| cate.poi[0].rpy                 | String  | 탐색 Y 좌표(WGS84의 경우 latitude)               |
| cate.poi[0].name1               | String  | 정식 명칭                                    |
| cate.poi[0].name2               | String  | 축약 명칭                                    |
| cate.poi[0].name3               | String  | 확장 명칭 1                                  |
| cate.poi[0].name4               | String  | 확장 명칭 2                                  |
| cate.poi[0].admcode             | String  | 행정코드                                    |
| cate.poi[0].jibun               | String  | 지번                                       |
| cate.poi[0].address             | String  | 주소                                       |
| cate.poi[0].roadname            | String  | 새주소 도로명                                  |
| cate.poi[0].roadjibun           | String  | 새주소 지번                                   |
| cate.poi[0].detailaddress       | String  | 상세 주소                                    |
| cate.poi[0].catecode            | String  | 분류 코드                                    |
| cate.poi[0].catename            | String  | 분류 명칭                                    |
| cate.poi[0].fulladdress         | String  | 전체 주소(행정주소+지번+상세주소)                      |
| cate.poi[0].zip                 | String  | 우편번호                                     |
| cate.poi[0].homeage             | String  | 홈페이지 url                                 |
| cate.poi[0].email               | String  | 이메일                                      |
| cate.poi[0].howtogo             | String  | 교통편                                      |
| cate.poi[0].tel1                | String  | 전화번호 1                                   |
| cate.poi[0].tel2                | String  | 전화번호 2                                   |
| cate.poi[0].fax1                | String  | 팩스번호 1                                   |
| cate.poi[0].fax2                | String  | 팩스번호 2                                   |
| cate.poi[0].icode               | String  | ICODE                                    |
| cate.poi[0].detail_count        | Integer | 분류 상세 항목 개수                              |
| cate.poi[0].etc_count           | Integer | 분류 기타 항목 개수                              |
| cate.poi[0].imagecount          | Integer | POI 이미지 개수                               |
| cate.poi[0].hasoildata          | Boolean | 유가 데이터 존재 유무                             |
| cate.poi[0].detailinfo          | Array   | 분류 상세 항목                                 |
| cate.poi[0].detailinfo[0].name  | String  | 분류 상세 항목 설명                              |
| cate.poi[0].detailinfo[0].value | String  | 분류 상세 항목 내용                              |
| cate.poi[0].etcinfo             | Array   | 분류 기타 항목                                 |
| cate.poi[0].etcinfo[0].name     | String  | 분류 기타 항목 설명                              |
| cate.poi[0].etcinfo[0].value    | String  | 분류 기타 항목 내용                              |
| cate.poi[0].oildata             | Object  | 유가 데이터 정보                                |
| cate.poi[0].oilda.tag_price     | Integer | 휘발유 가격                                   |
| cate.poi[0].oilda.hg_price      | Integer | 고급휘발유 가격                                 |
| cate.poi[0].oilda.d_price       | Integer | 경유 가격                                    |
| cate.poi[0].oilda.l_price       | Integer | LPG 가격                                   |
| cate.poi[0].oilda.updatetime    | String  | 업데이트 시간                                  |
| cate.poi[0].oilda.priceinfo     | String  | 최고, 최저 유가 정보<br>(H : 최고, L : 최저, X : 해당없음)<br>휘발유, 고급휘발유, 경유, LPG 순 |
| cate.poi[0].oilda.wash          | Boolean | 세차 시설 여부                                 |
| cate.poi[0].oilda.fix           | Boolean | 정비 가능 여부                                 |
| cate.poi[0].oilda.mart          | Boolean | 매점 여부                                    |
| cate.poi[0].hassubpoi          | Boolean | 하위 시설물 데이터 존재 유무          |
| cate.poi[0].subpoi          | Object | 하위 시설물 정보                                 |
| cate.poi[0].subpoi.count          | Integer | 하위 시설물 개수                                 |
| cate.poi[0].subpoi.poi          | Array |  POI 정보와 동일                            |

## Geocoding API

### 1\. Search of Address \(Address \-\> Coordinates\)

* Search coordinates (TW/WGS84/TM) with address.

#### Request

[URI]

| Method | URI                                                          |
| ------ | ------------------------------------------------------------ |
| GET    | /maps/v3.0/appkeys/{appkey}/coordinates?query={query}&coordtype={coordtype}&startposition={startposition}&reqcount={reqcount}&admcode={admcode} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Query Parameters]

| Name          | Type   | Required | Valid Range | Description                                                  |
| ------------- | ------ | -------- | ----------- | ------------------------------------------------------------ |
| query         | String | Required |             | Search word                                                  |
| coordtype     | String | Optional |             | Type of coordinates <br/>0: TW coordinates
1: WGS84 coordinates
2: TM coordinates |
| startposition | String | Optional |             | Start position of search<br/>0: Initial location; query by 0, if left blank |
| reqcount      | String | Optional |             | Number of search requests<br/>Return max count, if it is set with 0 |
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
                "address": "Pangyo-myeon, Seocheon-gun, Chungcheongnam-do",
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
                "address": "Pangyo-ri,Seobu-myeon, Hongseong-gun, Chungcheongnam-do",
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
                "address": "Pangyo-ri, Pangyo-myeon, Seocheon-gun, Chungcheongnam-do",
                "roadname": "",
                "roadjibun": "",
                "accuracy": 3.0,
                "distance": 1.2083048E7
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
| address.res_type         | String  | Name of search result type<br/>In the order of Name, Category, Address, and Phone Number
(e.g.) NYNN: No for name, Yes for category, No for address, and No for phone number |
| address.adm              | Array   | Search results                                               |
| address.adm[0].type      | String  | Type of search<br>1:  Search administrative system<br>2: Search land-lot number<br>3: Search new address system |
| address.adm[0].posx      | String  | X coordinates                                                |
| address.adm[0].posy      | String  | Y coordinates                                                |
| address.adm[0].admcode   | String  | Administrative code                                          |
| address.adm[0].address   | String  | Addresss                                                     |
| address.adm[0].roadname  | String  | Road name for new address system                             |
| address.adm[0].roadjibun | String  | Land-lot number for new address system                       |
| address.adm[0].accuracy  | Integer | Accuracy of land-lot numbers<br>0: Search accuracy <br>1: Extend the last digit of land-lot numbers<br>e.g.) For the search of 963-2, return the search result of 963-X.  <br>2 : Extend the initial digit of land-lot numbers<br>e.g) For the search of 963-2, return the search result of 96X <br>3: Coordinates of Dong by the administrative unit <br>e.g.) In case input is available only down to Sampyeong-dong<br>4:  Coordinates of Dong or higher unit, or administrative Dong <br>e.g.) In case input is available down to Bundang-gu only |



## Reverse Geocoding API

### 1\. Search of Coordinates \(Coordinates \-\> Address\)

* Search address with coordinates (TW/WGS84 coordinates).

#### Request

[URI]

| Method | URI                                                          |
| ------ | ------------------------------------------------------------ |
| GET    | /maps/v3.0/appkeys/{appkey}/addresses?posX={posX}&posY={posY}&coordtype={coordtype} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Query Parameters]

| Name      | Type   | Required | Valid Range | Description                                                  |
| --------- | ------ | -------- | ----------- | ------------------------------------------------------------ |
| posX      | String | Required |             | X coordinates                                                |
| posY      | String | Required |             | Y coordinates                                                |
| coordtype | String | Optional |             | Requested type of coordinates<br>0: TW coordinates<br>1: WGS84 coordinates<br>Search by TW coordinates, if left blank |

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
        "hasAdmAddress": true,
        "adm": {
            "posx": "126.947265",
            "posy": "37.384033",
            "address": "경기도 안양시 동안구 호계동",
            "distance": 0,
            "bldname": "",
            "admcode": "4117310400",
            "postcode": "14079",
            "jibun": "921",
            "roadname": "경기도 안양시 동안구 귀인로",
            "roadjibun": "59"
        },
        "adm_address": {
            "address": "경기도 안양시 동안구 호계2동",
            "admcode": "4117359000",
            "address_category3": "호계2동",
            "address_category4": "",
            "jibun": "921",
            "address_category1": "경기도",
            "address_category2": "안양시 동안구",
            "cut_address": "경기 안양시 동안구 호계2동"
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

##### Field


| 이름                     | 타입      | 설명                                       |
| ---------------------- | ------- | ---------------------------------------- |
| header                 | Object  | 헤더 영역                                    |
| header.isSuccessful    | Boolean | 성공 여부                                    |
| header.resultCode      | Integer | 실패 코드                                    |
| header.resultMessage   | String  | 실패 메시지                                   |
| location               | Object  | 본문 영역                                    |
| location.result        | Boolean | 성공 여부                                    |
| location.hasAdmAddress        | Boolean | 행정 주소 반환 여부                                    |
| location.adm           | Object  | 법정 주소 정보                           |
| location.adm.posx      | String  | X 좌표                                     |
| location.adm.posy      | String  | Y 좌표                                     |
| location.adm.admcode  | String  | 법정코드                                  |
| location.adm.address  | String  | 주소                                  |
| location.adm.jibun  | String  | 지번                                  |
| location.adm.roadname  | String  | 새주소 도로명                                  |
| location.adm.roadjibun | String  | 새주소 지번                                   |
| location.adm.bldname  | String  | 건물명(해당될 때만)                              |
| location.adm.postcode  | String  | 우편번호                   |
| location.adm_address           | Object  | 행정동 주소 정보                           |
| location.adm_address.admcode   | String  | 행정코드                                    |
| location.adm_address.address   | String  | 주소                                       |
| location.adm_address.jibun     | String  | 지번                                       |
| location.adm_address.address_category1     | String  |   도/시                      |
| location.adm_address.address_category2     | String  |   시/군/구                   |
| location.adm_address.address_category3     | String  |   읍/면/동                 |
| location.adm_address.address_category4     | String  |   리                  |
| location.adm_address.cut_address     | String  |                         |
| location.legal_address           | Object  | 법정동 주소 정보                           |
| location.legal_address.admcode   | String  | 법정코드                                    |
| location.legal_address.address   | String  | 주소                                       |
| location.legal_address.jibun     | String  | 지번                                       |
| location.legal_address.address_category1     | String  |  도/시                       |
| location.legal_address.address_category2     | String  |  시/군/구                      |
| location.legal_address.address_category3     | String  |  읍/면/동                      |
| location.legal_address.address_category4     | String  |  리                       |
| location.legal_address.cut_address     | String  |                         |





## Navigate

### 1\. Route Navigation

* Use departure and destination coordinates (including optional stopovers) to return navigated details and route information.

#### Request

[URI]

| Method | URI                                      |
| ---- | ---------------------------------------- |
| GET,POST  | /maps/v3.0/appkeys/{appkey}/route-normal?option={option}&coordType={coordType}&carType={carType}&startX={startX}&startY={startY}&endX={endX}&endY={endY}&via1X={via1X}&via1Y={via1Y}&via2X={via2X}&via2Y={via2Y}&via3X={via3X}&via3Y={via3Y}&via4X={via4X}&via4Y={via4Y}&via5X={via5X}&via5Y={via5Y}&guideTop={guideTop}&groupByTrafficColor={groupByTrafficColor}&saveFile={saveFile} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Request Parameters]

| Name   | Type  | Required | Valid Range | Description                             |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| startX   | String | Required |       | X coordinates at departure       |
| startY   | String | Required |       | Y coordinates at departure       |
| endX     | String | Required |       | X coordinates at destination     |
| endY     | String | Required |       | Y coordinates at destination     |
| via1X    | String | Optional |       | X coordinates at stopover 1  |
| via1Y    | String | Optional |       | Y coordinates at stopover 1   |
| via2X    | String | Optional |       | X coordinates at stopover 2    |
| via2Y    | String | Optional |       | Y coordinates at stopover 2    |
| via3X    | String | Optional |       | X coordinates at stopover 3     |
| via3Y    | String | Optional |       | Y coordinates at stopover 3      |
| via4X    | String | Optional |       | X coordinates at stopover 4      |
| via4Y    | String | Optional |       | Y coordinates at stopover 4      |
| via5X    | String | Optional |       | X coordinates at stopover 5      |
| via5Y    | String | Optional |       | Y coordinates at stopover 5   |
| option   | String | Required |       | Optional route navigation<br>Only one option is available<br>e.g.) option=real_traffic<br>real_traffic: Real-time recommendation1<br>real\_traffic\_freeroad: Real-time \(free\)<br>real_traffic2: Real-time recommendation2<br>short\_distance\_priority: Short distance<br>motorcycle: Two-wheeler |
| carType   | Integer | Optional |       | Vehicle types to calculate toll fees (1~6); default is 1 |
| coordType   | String | Required |       | Only one is available out of Input/Output coordinate types (TW or WGS84) |
|guideTop	|Integer| Optional ||Guide data count to expose |
|groupByTrafficColor	| Boolean| Optional | |Return list of route details by each group of traffic color	|
|saveFile	| Boolean| Optional | |Save binary files to search POI around the route	|



#### Response

##### Body
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
                    "name": "Subuchon-gil",
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

##### Field

| Name                      | Type   | Description                             |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | Header area                     |
| header.isSuccessful         | Boolean | Successful or not                   |
| header.resultCode           | Integer | Failure code                             |
| header.resultMessage        | String  | Failure message                          |
| route			                  | Object  | Body area                                |
| route.data                   | Object  | Route data                   |
| route.data.file_name          | String | Binary file name to search POI around the route 경로 주변 POI 검색을 위한 binary 파일명 |
| route.data.option              | String | Navigation option |
| route.data.spend_time           | Integer | Required time (second)          |
| route.data.distance           | Integer | Distance (m)                 |
| route.data.toLl_fee    | Integer | Toll fee                    |
| route.data.paths	 | Array | List of route details       |
| route.data.paths[0].coords | Array | List of coordinate details |
| route.data.paths[0].coords[0].x   | Double | X coordinates                 |
| route.data.paths[0].coords[0].y         | Double | Y coordinates             |
| route.data.paths[0].speed          | Integer | Speed                             |
| route.data.paths[0].spend_time          | Integer | Required time (second)           |
| route.data.paths[0].distance             | Integer | Distance (m)               |
| route.data.paths[0].road_code             | Integer | Road type code |
| route.data.paths[0].traffic_color       | String | Road traffic color  |
| route.data.guides       | Array | List of main road information |
| route.data.guides[0].coords       | Array | List of coordinate details |
| route.data.guides[0].coords[0].x       | Array | X coordinates           |
| route.data.guides[0].coords[0].y       | Array | Y coordinates           |
| route.data.guides[0].distance       | Integer | Distance (m)               |
| route.data.guides[0].name       | String | Road name               |
| route.data.guides[0].road_code       | Integer | Road type code         |
| route.data.guides[0].score       | Integer | Weight                 |
| route.data.guides[0].speed       | Integer | Speed (km)             |
| route.data.guides[0].type       | String | Road type              |
| route.data.guides[0].traffic_color       | String | Road traffic color |



### 2\. Summary of Route Navigation

* Use departure and destination coordinates (including optional stopovers) to return navigated summary data (e.g. distance, time, and, navigation options).

#### Request

[URI]

| Method | URI                                      |
| ---- | ---------------------------------------- |
| GET,POST  | /maps/v3.0/appkeys/{appkey}/route-summary?option={option}&coordType={coordType}&startX={startX}&startY={startY}&endX={endX}&endY={endY}&via1X={via1X}&via1Y={via1Y}&via2X={via2X}&via2Y={via2Y}&via3X={via3X}&via3Y={via3Y}&via4X={via4X}&via4Y={via4Y}&via5X={via5X}&via5Y={via5Y} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Request Parameters]

| Name | Type   | Required | Valid Range | Description                              |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| startX   | String | Required |       | X coordinates at departure     |
| startY   | String | Required |       | Y coordinates at departure         |
| endX     | String | Required |       | X coordinates at destination       |
| endY     | String | Required |       | Y coordinates at destination       |
| via1X    | String | Optional |       | X coordinates at stopover 1 |
| via1Y    | String | Optional |       | Y coordinates at stopover 1    |
| via2X    | String | Optional |       | X coordinates at stopover 2   |
| via2Y    | String | Optional |       | Y coordinates at stopover 2   |
| via3X    | String | Optional |       | X coordinates at stopover 3   |
| via3Y    | String | Optional |       | Y coordinates at stopover 3   |
| via4X    | String | Optional |       | X coordinates at stopover 4   |
| via4Y    | String | Optional |       | Y coordinates at stopover 4   |
| via5X    | String | Optional |       | X coordinates at stopover 5   |
| via5Y    | String | Optional |       | Y coordinates at stopover 5   |
| option   | String | Required |       | Optional search navigation<br>Only one navigation option is available <br>e.g.) option=real_traffic<br>real_traffic: Real-time recommendation1<br>real\_traffic\_freeroad: Real-time (free of charge\)<br>real_traffic2: Real-time recommendation2<br>short\_distance\_priority: Short distance<br>motorcycle: Two-wheeler |
| coordType   | String | Required |       | Only one is available out of Input/Output coordinate types (TW or WGS84) |


#### Response

##### Body
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

##### Field

| Name                      | Type    | Description                              |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | Header area                              |
| header.isSuccessful         | Boolean | Successful or not                        |
| header.resultCode           | Integer | Failure code                             |
| header.resultMessage        | String  | Failure message                          |
| route			                  | Object  | Body area                                |
| route.data                   | Array  | Route data                               |
| route.data[0].option              | String | Navigation option         |
| route.data[0].spend_time           | Integer | Required time (second)         |
| route.data[0].distance           | Integer | Distance (m)               |


### 3\. Summary of Navigation Routes with Multiple Departures

* Navigate coordinates of multiple departures and one departure, and return each time and distance data.

#### Request

[URI]

| Method | URI                                      |
| ---- | ---------------------------------------- |
| POST  | /maps/v3.0/appkeys/{appkey}/route-start-multi-summary|

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Request Parameters]

| Name   | Type   | Required | Valid Range | Description                            |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| data    | Array |     |       | Array information at departure      |
| data[0].startX   | String | Required |       | X coordinates at departure         |
| data[0].startY   | String | Required |       | Y coordinates at departure       |
| data[0].startIdx   | String | Required |       | ID at departure                  |
| endX     | String | Required |       | X coordinates at destination |
| endY     | String | Required |       | Y coordinates at destination    |
| orderby    | String | Required |       | Sorting criteria (<br> 0 : distance_desc<br>1 : distance_asc<br>2 : time_desc <br>3 : time_asc<br>)               |
| coordType    | String | Required    |       | Type of coordinates (TW, or WGS84)
| resultCount    | Integer | Optional    |       | Number of exposed results             |


#### Response

##### Body
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

##### Field

| Name                      | Type   | Description                             |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | Header area                          |
| header.isSuccessful         | Boolean | Successful or not                    |
| header.resultCode           | Integer | Failure code                         |
| header.resultMessage        | String  | Failure message                     |
| route			                  | Object  | Body area                            |
| route.data                   | Array  | Route data                    |
| route.data[0].spend_time           | Integer | Required time (second)  |
| route.data[0].distance           | Integer | Distance (m)                 |
| route.data[0].startX           | String | X coordinates at departure |
| route.data[0].startY           | String | Y coordinates at departure |
| route.data[0].startIdx           | String | ID at departure           |



### 4\. Summary of Navigation Routes with Multiple Destinations

* Navigate coordinates of one departure and multiple destinations, and return each time and distance data.

#### Request

[URI]

| Method | URI                                      |
| ---- | ---------------------------------------- |
| POST  | /maps/v3.0/appkeys/{appkey}/route-end-multi-summary|

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Request Parameters]

| Name   | Type  | Required | Valid Range | Description                             |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| data    | Array |     |       | Array information at departure      |
| data[0].endX   | String | Required |       | X coordinates at destination    |
| data[0].endY   | String | Required |       | Y coordinates at destination     |
| data[0].endIdx   | String | Required |       | ID at destination               |
| startX     | String | Required |       | X coordinates at departure       |
| startY     | String | Required |       | Y coordinates at departure       |
| orderby    | String | Required |       | Sorting criteria (<br> 0 : distance_desc<br>1 : distance_asc<br>2 : time_desc <br>3 : time_asc<br>)               |
| coordType    | String | Required    |       | Type of coordinates (TW or WGS84)
| resultCount    | Integer | Optional    |       | Number of exposed results                           |


#### Response

##### Body
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

##### Field

| Name                      | Type   | Description                             |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | Header area                         |
| header.isSuccessful         | Boolean | Successful or not                      |
| header.resultCode           | Integer | Failure code                             |
| header.resultMessage        | String  | Failure message                          |
| route			                  | Object  | Body area                                |
| route.data                   | Array  | Route data                               |
| route.data[0].spend_time           | Integer | Required time (second)          |
| route.data[0].distance           | Integer | Distance (m)                 |
| route.data[0].endX           | String | X coordinates at destination |
| route.data[0].endY           | String | Y coordinates at destination |
| route.data[0].endIdx           | String | ID at destination         |



### 5\. Search of Estimated Routes

* Use estimated arrival time based on estimated start and arrival time, as well as coordinates at departure and destination (including optional stopovers), and return navigated details and route information.  

#### Request

[URI]

| Method | URI                                                          |
| ------ | ------------------------------------------------------------ |
| GET    | /maps/v3.0/appkeys/{appkey}/route-time?startX={startX}&startY={startY}&endX={endX}&endY={endY}&type={type}&year={year}&month={month}&day={day}&hour={hour}&minutes={minutes}&via1X={via1X}&via1Y={via1Y}&via2X={via2X}&via2Y={via2Y}&via3X={via3X}&via3Y={via3Y}&via4X={via4X}&via4Y={via4Y}&via5X={via5X}&via5Y={via5Y}&coordType={coordType}&carType={carType}&useTrafficColor={useTrafficColor}&guideTop={guideTop}&groupByTrafficColor={groupByTrafficColor}&beforeCount={beforeCount}&afterCount={afterCount}&interval={interval} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Request Parameters]

| Name	      | Type     | Required | Valid Range | Description                                       |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| startX    | String | Required   |       | X coordinates at departure
| startY    | String | Required   |       | Y coordinates at departure
| endX   | String | Required |       | x coordinates at destination                                 |
| endY   | String | Required    |       | Y coordinates at destination                                 |
| type     | String | Required    |       | Base time (Departure, Arrival)<br>start: Based on departure time<br>end : Based on arrival time                                  |
| year     | Integer | Required   |       | Base year (ex.2019)                                 |
| month     | Integer | Required   |       | Base month                                 |
| day    | Integer | Required   |       | Base day 		|
| hour     | Integer | Required    |       | Base time (hour)                                |
| minutes    | Integer | Required    |       | Base time (minute) 		|
| via1X   | String | Optional    |       |  X coordinates at stopover 1                |
| via1Y   | String | Optional  |       |  Y coordinates at stopover 1                 |
| via2X   | String | Optional   |       |  X coordinates at stopover 2                |
| via2Y   | String | Optional    |       | Y coordinates at stopover 2               |
| via3X   | String | Optional   |       |  X coordinates at stopover 3               |
| via3Y   | String | Optional   |       |  Y coordinates at stopover 3               |
| via4X   | String | Optional   |       |  X coordinates at stopover 4               |
| via4Y   | String | Optional   |       |  Y coordinates at stopover 4               |
| via5X   | String | Optional   |       |  X coordinates at stopover 5               |
| via5Y   | String | Optional    |      |  Y coordinates at stopover 5               |
| coordType    | String | Optional    |       | Type of coordinates (TW, WGS84)<br> default : wgs84
| useTrafficColor   | Boolean | Optional    |       | Return road traffic color (True, False)<br> defaut : false |
| guideTop   | Integer | Optional   |       |Guide data count to expose |
| carType   | Integer | Optional    |       | Vehicle type to calculate toll fees (1~6), default : 1 |
|groupByTrafficColor	| Boolean| Optional| |Return list of route details by each group of traffic color	|
| beforeCount   | Integer | Optional  |      | Navigation count before base time  |
| afterCount   | Integer | Optional    |       | Navigation count after base time |
| interval   | Integer | Optional    |       | Inverval (minute) before/after base time  |

#### Response

##### Body
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
                    "name": "Gyeongsu-daero",
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
                    "name": "Bongdam-Gwacheon Ro",
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

##### Field

| Name                      | Type   | Description                             |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | Header area                        |
| header.isSuccessful         | Boolean | Successful or not                   |
| header.resultCode           | Integer | Failure code                             |
| header.resultMessage        | String  | Failure message                          |
| route			                  | Object  | Body area                                |
| route.data                   | Object  | Route data                               |
| route.data.file_name          | String | Binary file name to search POI around the route |
| route.data.option              | String | Navigation option           |
| route.data.spend_time           | Integer | Required time (second)         |
| route.data.distance           | Integer | Distance (m)                 |
| route.data.toLl_fee    | Integer | Toll fee                    |
| route.data.times	 | Array | List of route details |
| route.data.times[0].index	 | Integer | Index as compared to base time (which is applied for 0) |
| route.data.times[0].spend_time	 | Integer | Required time (second) |
| route.data.times[0].start_time	 | Object | Start time |
| route.data.times[0].start_time.year	 | Object | Year   |
| route.data.times[0].start_time.month	 | Object | Month   |
| route.data.times[0].start_time.day	 | Object | Day     |
| route.data.times[0].start_time.hour	 | Object | Hour    |
| route.data.times[0].start_time.minutes	 | Object | Minute  |
| route.data.times[0].end_time	 | Object | Arrival time |
| route.data.times[0].end_time.year	 | Object | Year    |
| route.data.times[0].end_time.month	 | Object | Month   |
| route.data.times[0].end_time.day	 | Object | Day     |
| route.data.times[0].end_time.hour	 | Object | Hour    |
| route.data.times[0].end_time.minutes	 | Object | Minute |
| route.data.paths	 | Array | List of route details |
| route.data.paths[0].coords | Array | List of coordinate details |
| route.data.paths[0].coords[0].x   | Double | X coordinates                |
| route.data.paths[0].coords[0].y         | Double | Y coordinates              |
| route.data.paths[0].speed          | Integer | Speed                              |
| route.data.paths[0].spend_time          | Integer | Required time (second)                   |
| route.data.paths[0].distance             | Integer | Distance (m)               |
| route.data.paths[0].road_code             | Integer | Road type code       |
| route.data.paths[0].traffic_color       | String | Road traffic color |
| route.data.guides       | Array | List of main road information |
| route.data.guides[0].coords       | Array | List of coordinate details |
| route.data.guides[0].coords[0].x       | Array | X coordinates            |
| route.data.guides[0].coords[0].y       | Array | Y coordinates           |
| route.data.guides[0].distance       | Integer | Distance (m)               |
| route.data.guides[0].name       | String | Road name               |
| route.data.guides[0].road_code       | Integer | Road type code         |
| route.data.guides[0].score       | Integer | Weight                 |
| route.data.guides[0].speed       | Integer | Speed (km)                 |
| route.data.guides[0].type       | String | Road type              |
| route.data.guides[0].traffic_color       | String | Road traffic color     |


## Static Map

### 1\. Static Map

* Return static map images within user-defined map range.

#### Request

[URI]

| Method | URI                                                          |
| ------ | ------------------------------------------------------------ |
| GET    | /maps/v3.0/appkeys/{appkey}/static-maps?lon={lon}&lat{lat}&zoom={zoom}&bearing={bearing}&pitch={pitch}&width={width}&height={height}&x2={x2}&mx={mx}&my={my}&imgUrl={imgUrl} |

[Path parameter]

| Name   | Type   | Required | Valid Range | Description   |
| ------ | ------ | -------- | ----------- | ------------- |
| appkey | String | Required |             | Origin appkey |

[Request Query Parameters]

| Name   | Type  | Required | Valid Range | Description                             |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| lon   | String | Required |       | Longitude coordinates to be requested |
| lat   | String | Required |       | Latitude coordinates to be requested |
| zoom   | String | Optional |       | Zoom-in level of coordinates to be requested |
| bearing     | String | Optional |       | Rotation rate of coordinates to be requested |
| pitch     | String | Optional |       | Tilting level of coordinates to be requested (0~30) |
| width    | String | Optional |       | Width value of image to be requested |
| height    | String | Optional |       | Height value of image to be requested |
| x2    | String | Optional |       | Return image size * 2 |
| mx    | String | Optional |       | Coordinates (logitude) to represent a marker |
| my    | String | Optional |       | Coordinates (latitude) to represent a marker |
| imgUrl    | String | Optional |       | URL of image to represent a marker |


#### Response

##### Body
<img src="http://static.toastoven.net/toastcloud/notice/20191029_Maps_new/map_static.png">
