## Application Service > Maps > APIガイド

Mapsサービスを使用するのに必要なAPIを説明します。

## API共通情報

### 事前準備

* APIを使用するには、アプリケーションキーが必要です。
* アプリケーションキーは、**TOAST Console**上部にある**URL & Appkey**メニューで確認できます。

### リクエスト共通情報

#### URL情報

| 環境 | ドメイン                      |
| ---- | -------------------------------- |
| Real | https://api-maps.cloud.toast.com |

### レスポンス共通情報

#### 検索/探索API

* すべてのAPIリクエストに対して「200 OK」を返します。レスポンスの詳細結果は、レスポンス本文のヘッダを参照してください。

```
{
	"header": {
		"isSuccessful": true,
		"resultCode": ,
		"resultMessage": ""
	}
}
```

## 検索

### 1\. 住所検索\(住所→座標\)

* 住所で座標(TW座標/WGS84座標/TM座標)を検索します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v1.0/appkeys/{appkey}/coordinates?query={query}&coordtype={coordtype}&startposition={startposition}&reqcount={reqcount}&admcode={admcode} |

[Path parameter]

| 名前 | タイプ | 必須かどうか | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Query Parameters]

| 名前    | タイプ | 必須かどうか | 有効範囲 | 説明                               |
| ------------- | ------ | ----- | ----- | ---------------------------------------- |
| query         | String | 必須 |       | 検索ワード                                |
| coordtype     | String | 任意 |       | 座標形式<br>0：TW座標<br>1：WGS84座標<br>2：TM座標 |
| startposition | String | 任意 |       | 検索開始位置<br>0：最初の位置<br>未入力時は0で照会 |
| reqcount      | String | 任意 |       | 検索リクエスト数<br>0に設定するとMax Countを返す  |
| admcode       | String | 任意 |       | 行政コード                            |

#### レスポンス

##### レスポンス本文

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
        "address": "京畿道城南市盆唐区板橋洞",
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
        "address": "京畿道城南市盆唐区柏峴洞(板橋洞)",
        "roadname": "",
        "roadjibun": "",
        "accuracy": 3
      }
    ]
  }
}
```

##### フィールド

| 名前               | タイプ | 説明                               |
| ------------------------ | ------- | ---------------------------------------- |
| header                   | Object  | ヘッダ領域                            |
| header.isSuccessful      | Boolean | 成否                            |
| header.resultCode        | Integer | 失敗コード                            |
| header.resultMessage     | String  | 失敗メッセージ                           |
| address                  | Object  | 本文領域                            |
| address.result           | Boolean | 成否                            |
| address.totalcount       | Integer | 全体検索結果対象数                     |
| address.res_type         | String  | 検索結果Type名称<br>名称、カテゴリー、住所、電話番号順<br>(例) NYNN：名称No、カテゴリーYES、住所NO、電話番号NO |
| address.adm              | Array   | 検索結果                             |
| address.adm[0].type      | String  | 検索type<br>1：行政系検索<br>2：地番検索<br>3：新住所検索 |
| address.adm[0].posx      | String  | X座標                             |
| address.adm[0].posy      | String  | Y座標                             |
| address.adm[0].admcode   | String  | 行政コード                            |
| address.adm[0].address   | String  | 住所                               |
| address.adm[0].roadname  | String  | 新住所の道路名                            |
| address.adm[0].roadjibun | String  | 新住所の地番                             |
| address.adm[0].accuracy  | Integer | 地番の正確度<br>0：正確検索<br>1：枝番拡張<br>例) 963-2と検索すると、963-X検索結果を返す<br>2：親番拡張<br>例) 963-2と検索すると、96X検索結果を返す<br>3：法定洞同座標<br>例)三坪洞までのみ入力される場合<br>4：洞単位以上の座標または法定洞座標<br>例)盆唐区までのみ入力される場合 |

### 2\. 座標検索\(座標→住所\)

* 座標(TW座標/WGS84座標)で住所を検索します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v1.0/appkeys/{appkey}/addresses?query={query}&posX={posX}&posY={posY}&coordtype={coordtype} |

[Path parameter]

| 名前 | タイプ | 必須かどうか | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Query Parameters]

| 名前 | タイプ | 必須かどうか | 有効範囲 | 説明                               |
| --------- | ------ | ----- | ----- | ---------------------------------------- |
| posX      | String | 必須 |       | X座標                             |
| posY      | String | 必須 |       | Y座標                             |
| coordtype | String | 任意 |       | リクエスト座標形式<br>0：TW座標<br>1：WGS84座標<br>未入力時、TW座標基準検索 |

#### レスポンス

##### レスポンス本文

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
      "address": "京畿道城南市盆唐区柏峴洞",
      "jibun": "519-7",
      "roadname": "",
      "roadjibun": "",
      "distance": 25
    }
  }
}
```

##### フィールド

| 名前             | タイプ | 説明                               |
| ---------------------- | ------- | ---------------------------------------- |
| header                 | Object  | ヘッダ領域                            |
| header.isSuccessful    | Boolean | 成否                            |
| header.resultCode      | Integer | 失敗コード                            |
| header.resultMessage   | String  | 失敗メッセージ                           |
| location               | Object  | 本文領域                            |
| location.result        | Boolean | 成否                            |
| location.adm           | Object  | 検索結果                            |
| location.adm.posx      | String  | X座標                             |
| location.adm.posy      | String  | Y座標                             |
| location.adm.admcode   | String  | 行政コード                            |
| location.adm.address   | String  | 住所                               |
| location.adm.jibun     | String  | 地番                                 |
| location.adm.roadname  | String  | 新住所の道路名                            |
| location.adm.roadjibun | String  | 新住所の地番                             |
| location.adm.distance  | Integer | 座標との距離(該当する時のみ)                          |
| location.adm.accuracy  | String  | 地番の正確度<br>0：正確検索<br>1：枝番拡張<br>例) 963-2と検索すると、963-X検索結果を返す<br>2：親番拡張<br>例) 963-2と検索すると、96X検索結果を返す<br>3：法定洞同座標<br>例)三坪洞までのみ入力される場合<br>4：洞単位以上の座標または法定洞座標<br>例)盆唐区までのみ入力される場合 |

### 3\. 統合検索

* 電話番号、住所、POI情報などの統合情報を検索します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v1.0/appkeys/{appkey}/searches&query={query}&coordtype&startposition={startposition}&reqcount={reqcount}&spopt={spopt}&radius={radius}&admcode={admcode}&depth={depth}&x1={x1}&y1={y1}&x2={x2}&y2={y2}&sortopt={sortopt}&catecode={catecode} |

[Path parameter]

| 名前 | タイプ | 必須かどうか | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Query Parameters]

| 名前    | タイプ | 必須かどうか | 有効範囲 | 説明                               |
| ------------- | ------ | ----- | ----- | ---------------------------------------- |
| query         | String | 必須 |       | 検索ワード                                |
| coordtype     | String | 任意 |       | 座標形式<br>0：TW座標<br>1：WGS84座標<br>2：TM座標 |
| startposition | String | 任意 |       | 検索開始位置<br>0：最初の位置、未入力の時は0で照会 |
| reqcount      | String | 任意 |       | 検索リクエスト数<br>0に設定するとMax Countを返す  |
| spopt         | String | 任意 |       | スペース検索オプション<br>0：スペース検索を使用しない<br>1：Extent検索<br>2：Range検索 *spopt値が設定されていない場合0に設定 |
| radius        | String | 任意 |       | 半径<br>spoptが2の場合使用、m単位      |
| admcode       | String | 任意 |       | 行政コード                            |
| depth         | String | 任意 |       | 下位施設の要求水準<br>1：1 depthのみリクエスト(最上位depth)<br>2：2 depthまでリクエスト<br>3：3 depthまでリクエスト_depth値が設定されていない場合、1に設定<br>_ depth設定時、下記Responseのようにsubpoi詳細情報がdepthに合わせて返される |
| x1            | String | 任意 |       | X1座標<br>spoptが0の場合、基準点X座標<br>spoptが1の場合、Extentの左上X座標<br>spoptが2の場合、基準点X座標 |
| y1            | String | 任意 |       | Y1座標<br>spoptが0の場合、基準点Y座標<br>spoptが1の場合、Extentの最上段Y座標<br>spoptが2の場合、基準点Y座標 |
| x2            | String | 任意 |       | X2座標<br>spoptが1の場合、Extentの右下のX座標、spoptが2の場合は使用しない |
| y2            | String | 任意 |       | Y2座標<br>spoptが1の場合、Extentの右下Y座標、spoptが2の場合は使用しない |
| sortopt       | String | 任意 |       | ソートoption<br>1：名称順ソート<br>2：距離順ソート(座標を入力した場合)<br>3：名前マッチ→距離順ソート(座標を入力した場合)<br>4：検索ワードWeightソート(エンジン基準)<br>5：検索ワードWeightソート + length(エンジン基準)<br>6：好きなカテゴリー優先ソート[V8.1.5未サポート]<br>7：最新データ順ソート<br>8：検索ワードWeightソート(Landmark>距離>PoiWeight) + 距離順(座標を入力した場合)<br>*sortopt値が設定されていない場合4に設定 |
| catecode      | String | 任意 |       | 好きなカテゴリー<br>\- 好きなカテゴリー検索時、検索ワードにカテゴリー名を入力した場合、検索ワード優先ポリシーにより、入力した好きなカテゴリーより検索ワードを基準に検索される<br>例)検索ワード："美容院" 、好きなカテゴリー："100000"(飲食店) →美容院を基準に検索される |

#### レスポンス

##### レスポンス本文

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
                "name2": "HIPEX",
                "name3": "Samhwan HIPEX",
                "name4": "HIPEX",
                "admcode": "4113510900",
                "jibun": "678",
                "address": "京畿道城南市盆唐区三坪洞",
                "roadname": "京畿道城南市盆唐区板橋駅路",
                "roadjibun": "240",
                "detailaddress": "",
                "catecode": "130301",
                "catename": "企業",
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
                            "name1": "A棟",
                            "name2": "Samhwan HIPEX A棟",
                            "name3": "",
                            "name4": "",
                            "admcode": "4113510900",
                            "jibun": "678",
                            "address": "京畿道城南市盆唐区三坪洞",
                            "roadname": "京畿道城南市盆唐区板橋駅路",
                            "roadjibun": "240",
                            "detailaddress": "",
                            "catecode": "130301",
                            "catename": "企業",
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
                                        "name1": "入口",
                                        "name2": "",
                                        "name3": "",
                                        "name4": "",
                                        "admcode": "4113510900",
                                        "jibun": "678",
                                        "address": "京畿道城南市盆唐区三坪洞",
                                        "roadname": "",
                                        "roadjibun": "",
                                        "detailaddress": "",
                                        "catecode": "181100",
                                        "catename": "道路施設",
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

##### フィールド

| 名前                       | タイプ | 説明                               |
| -------------------------------- | ------- | ---------------------------------------- |
| header                           | Object  | ヘッダ領域                            |
| header.isSuccessful              | Boolean | 成否                            |
| header.resultCode                | Integer | 失敗コード                            |
| header.resultMessage             | String  | 失敗メッセージ                           |
| search                           | Object  | 本文領域                            |
| search.result                    | Boolean | 成否                            |
| search.type                      | Integer | 0：一般検索<br>1：Reference検索    |
| search.totalcount                | Integer | 全体検索結果対象数                     |
| search.count                     | Integer | 検索結果数                           |
| search.poitotalcount             | Integer | 全体検索結果対象数(Thinkware POI)            |
| search.poicount                  | Integer | 検索結果数(Thinkware POI)                  |
| search.tel_poitotalcount         | Integer | 全体検索結果対象数(Tel POI)                  |
| search.tel_poicount              | Integer | 検索結果数(Tel POI)                        |
| search.ucp_poitotalcount         | Integer | 全体検索結果対象数(User POI)                 |
| search.ucp_poicount              | Integer | 検索結果数(User POI)                       |
| search.admtotalcount             | Integer | adm全体検索結果対象数                 |
| search.admcount                  | Integer | adm検索結果数                       |
| search.reftotalcount             | Integer | ref全体検索結果対象数                 |
| search.refcount                  | Integer | ref検索結果数                       |
| search.recommendedQuery          | String  | 検索結果がない場合、誤字補正結果を提供(NULL可能)         |
| search.recommendedCost           | Integer | 誤字補正結果Cost(0～10000)                   |
| search.res_type                  | String  | 検索結果Type名称<br>名称、カテゴリー、住所、電話番号順<br>(例) NYNN：名称No、カテゴリーYES、住所NO、電話番号NO |
| search.poi                       | Array   | POI検索結果リスト                     |
| search.poi[0].poiid              | Integer | POI ID                                   |
| search.poi[0].depth              | String  | POI depth                                |
| search.poi[0].dpx                | String  | display X座標(WGS84の場合longitude)         |
| search.poi[0].dpy                | String  | display Y座標(WGS84の場合latitude)          |
| search.poi[0].rpx                | String  | 探索X座標(WGS84の場合longitude)              |
| search.poi[0].rpy                | String  | 探索Y座標(WGS84の場合latitude)               |
| search.poi[0].name1              | String  | 正式名称                              |
| search.poi[0].name2              | String  | 略称                              |
| search.poi[0].name3              | String  | 拡張名称1                                  |
| search.poi[0].name4              | String  | 拡張名称2                                  |
| search.poi[0].admcode            | String  | 行政コード                            |
| search.poi[0].address            | String  | 住所                               |
| search.poi[0].jibun              | String  | 地番                                 |
| search.poi[0].roadname           | String  | 新住所道路名                            |
| search.poi[0].roadjibun          | String  | 新住所の地番                             |
| search.poi[0].detailaddress      | String  | 詳細住所                            |
| search.poi[0].catecode           | String  | 分類コード                            |
| search.poi[0].catename           | String  | 分類名称                              |
| search.poi[0].dp_catecode        | String  | DP分類コード                         |
| search.poi[0].distance           | Integer | 座標との距離(該当する時のみ)                          |
| search.poi[0].tel                | String  | 電話番号                             |
| search.poi[0].hasoildata         | Boolean | ガソリン価格データの有無                       |
| search.poi[0].hasdetailinfo      | Boolean | 詳細情報の有無                        |
| search.poi[0].hassubpoi          | Boolean | 下位施設の有無                       |
| search.poi[0].adv_count          | Integer | 広告コード数                           |
| search.poi[0].islandmark         | Boolean | ランドマークかどうか                            |
| search.poi[0].updateTS           | String  | 最終変更日時(Y4-MM-DD HH:mm:ss)フォーマット    |
| search.poi[0].data_source        | String  | POI作成情報区分(Thinkware/Tel/User)        |
| search.poi[0].badgeflag          | Boolean | バッジ有無(Not Yet：FALSE、Badged：TRUE)    |
| search.poi[0].userid             | String  | POI登録ユーザーID (UCPの場合にのみ)                |
| search.poi[0].imagecount         | Integer | POIイメージ数                         |
| search.poi[0].oildata            | Object  | ガソリン価格データ情報                        |
| search.poi[0].oildata.g_price    | Integer | レギュラー価格                           |
| search.poi[0].oildata.hg_price   | Integer | ハイオク価格                        |
| search.poi[0].oildata.d_price    | Integer | 軽油価格                            |
| search.poi[0].oildata.l_price    | Integer | LPG価格                           |
| search.poi[0].oildata.updatetime | String  | アップデート時間                          |
| search.poi[0].oildata.priceinfo  | String  | 最高、最低ガソリン価格情報<br>(H：最高、L：最低、X：該当なし)<br>レギュラー、ハイオク、軽油、LPG順 |
| search.poi[0].oildata.wash       | Boolean | 洗車施設有無                           |
| search.poi[0].oildata.fix        | Boolean | 整備可否                           |
| search.poi[0].oildata.mart       | Boolean | 売店有無                              |
| search.poi[0].AdInfo             | Array   | 広告提供業者広告コード                   |
| search.poi[0].AdInfo.ADCODE      | Integer | 広告コード<br>1 ～ 99まで付与可能(最大99個)          |
| search.poi[0].subpoi             | Object  | 下位施設の情報                        |
| search.poi[0].subpoi.count       | Integer | 下位施設の数                          |
| search.poi[0].subpoi.poi         | Array   | POI情報と同じ                         |
| search.tel                       | Array   | TEL検索結果リスト(POI情報と同じ)                |
| search.ucp                       | Array   | UCP検索結果リスト(POI情報と同じ)                |
| search.adm                       | Array   | ADM検索結果リスト                     |
| search.adm[0].type               | String  | 検索type<br>1：行政系検索<br>2：地番検索<br>3：新住所検索 |
| search.adm[0].posx               | String  | X座標(WGS84の場合longitude)                 |
| search.adm[0].posy               | String  | Y座標(WGS84の場合latitude)                  |
| search.adm[0].admcode            | String  | 行政コード                             |
| search.adm[0].address            | String  | 住所                               |
| search.adm[0].jibun              | String  | 地番                                 |
| search.adm[0].roadname           | String  | 新しい住所の道路名                            |
| search.adm[0].roadjibun          | String  | 新住所の地番                             |
| search.adm[0].accuracy           | Integer | 地番正確度<br>：正確検索<br>1：枝番拡張<br>2：親番拡張 |
| search.hasgasstation             | Boolean | ガソリン価格情報提供するかどうか                        |
| search.oilprice                  | Object  | ガソリン価格情報                            |
| search.oilprice.max_g_price      | Integer | 最高レギュラー価格                        |
| search.oilprice.min_g_price      | Integer | 最低レギュラー価格                        |
| search.oilprice.avg_g_price      | Integer | 平均レギュラー価格                        |
| search\.oilprice\.max\_hg\_price | Integer | 最高ハイオク価格                     |
| search\.oilprice\.min\_hg\_price | Integer | 最低ハイオク価格                     |
| search\.oilprice\.avg\_hg\_price | Integer | 平均ハイオク価格                     |
| search.oilprice.max_d_price      | Integer | 最高軽油価格                         |
| search.oilprice.min_d_price      | Integer | 最低軽油価格                         |
| search.oilprice.avg_d_price      | Integer | 平均軽油価格                         |
| search.oilprice.max_l_price      | Integer | 最高LPG価格                        |
| search.oilprice.min_l_price      | Integer | 最低LPG価格                        |
| search.oilprice.avg_l_price      | Integer | 平均LPG価格                        |

### 4\. 推薦ワード検索

* 検索ワードの推薦ワードを検索します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v1.0/appkeys/{appkey}/proposers?query={query} |

[Path parameter]

| 名前 | タイプ | 必須かどうか | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Query Parameters]

| 名前 | タイプ | 必須かどうか | 有効範囲 | 説明             |
| ----- | ------ | ----- | ----- | ---------------------- |
| query | String | 必須 | 50バイト | ハングル/英語/数字50バイト(ハングル25文字) |

#### レスポンス

##### レスポンス本文

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
        "keyword": "板橋駅",
        "frequency": 3729938
      },
      {
        "keyword": "板橋",
        "frequency": 3729326
      },
      {
        "keyword": "板橋IC",
        "frequency": 3729362
      },
      {
        "keyword": "板橋図書館",
        "frequency": 3729514
      },
      {
        "keyword": "板橋ウォンマウル",
        "frequency": 3730051
      },
      {
        "keyword": "板橋ロッテマート",
        "frequency": 3729602
      },
      {
        "keyword": "板橋Innovalley",
        "frequency": 3730186
      },
      {
        "keyword": "板橋博物館",
        "frequency": 3729654
      },
      {
        "keyword": "板橋中学校",
        "frequency": 3730256
      },
      {
        "keyword": "板橋マリオット",
        "frequency": 3729626
      }
    ]
  }
}
```

##### フィールド

| 名前                    | タイプ | 説明 |
| ----------------------------- | ------- | --------- |
| header                        | Object  | ヘッダ領域 |
| header.isSuccessful           | Boolean | 成否 |
| header.resultCode             | Integer | 失敗コード |
| header.resultMessage          | String  | 失敗メッセージ |
| proposer                      | Object  | 本文領域 |
| proposer.result               | Boolean | 成否 |
| proposer.count                | Integer | 推薦検索ワードの個数 |
| proposer.keyword              | Array   | 推薦検索ワードリスト |
| proposer.keyword[0].keyword   | String  | 推薦検索ワード |
| proposer.keyword[0].frequency | Integer | 照会頻度 |

### 5\. POI詳細検索

* POIの詳細情報を検索します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v1.0/appkeys/{appkey}/pois?poiid={poiid} |

[Path parameter]

| 名前 | タイプ | 必須かどうか | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Query Parameters]

| 名前 | タイプ | 必須かどうか | 有効範囲 | 説明                               |
| ----- | ------ | ----- | ----- | ---------------------------------------- |
| poiid | String | 必須 | 186個 | POI ID<br>poiidをセパレータ","で区切って入力<br>(複数可能186個まで)<br>例) poiid=123,234,567 |

#### レスポンス

##### レスポンス本文

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
        "name1": "現代百貨店(貿易センター店)",
        "name2": "現代百貨店貿易センター店",
        "name3": "貿易センター現代百貨店",
        "name4": "",
        "admcode": "1168010500",
        "jibun": "159-7",
        "address": "ソウル特別市江南区三成洞",
        "roadname": "ソウル特別市江南区三成洞テヘラン路",
        "roadjibun": "517",
        "detailaddress": "",
        "fulladdress": "ソウル特別市江南区三成洞159-7 ",
        "zip": "",
        "homepage": "http://www.e-hyundai.com",
        "email": "",
        "howtogo": "",
        "tel1": "025522233",
        "tel2": "",
        "fax1": "",
        "fax2": "",
        "catecode": "110102",
        "catename": "ショッピング",
        "dp_catecode": "250",
        "icode": "493-070-3606",
        "externallink": [],
        "detail_count": 10,
        "etc_count": 2,
        "imagecount": 0,
        "badgeflag": false,
        "detailinfo": [
          {
            "name": "休業日",
            "value": "毎月2回休業"
          },
          {
            "name": "営業時間",
            "value": "10:30～20:00"
          },
          {
            "name": "駐車",
            "value": "1400台可能"
          },
          {
            "name": "駐車料",
            "value": "1万KRW以上購入すると1時間無料"
          },
          {
            "name": "付帯施設1",
            "value": "エメラルドホール(イベントホール)"
          },
          {
            "name": "付帯施設2",
            "value": "テラスガーデン"
          },
          {
            "name": "規模",
            "value": "地上10階地下4階"
          },
          {
            "name": "フロア情報1",
            "value": "1階名品雑貨/2階ファッション雑貨"
          },
          {
            "name": "フロア情報2",
            "value": "3～4階女性衣類/6階ゴルフウェア"
          },
          {
            "name": "フロア情報3",
            "value": "9階飲食店街/10階催事場"
          }
        ],
        "etcinfo": [
          {
            "name": "その他1",
            "value": "金融中心地であるテヘラン路の中心部に位置"
          },
          {
            "name": "その他2",
            "value": "全世界から韓国を訪ねる顧客を満足させられる韓国流通のショウウィンドウ"
          }
        ],
        "hasoildata": false
      },
      ....
    ]
  }
}
```

##### フィールド

| 名前                         | タイプ | 説明                               |
| ---------------------------------- | ------- | ---------------------------------------- |
| header                             | Object  | ヘッダ領域                            |
| header.isSuccessful                | Boolean | 成否                            |
| header.resultCode                  | Integer | 失敗コード                            |
| header.resultMessage               | String  | 失敗メッセージ                           |
| poi                                | Object  | 本文領域                            |
| poi.result                         | Boolean | 成否                            |
| poi.totalcount                     | Integer | 全体検索結果対象数                     |
| poi.count                          | Integer | 検索結果数                           |
| poi.poiinfo                        | Array   | POI検索結果リスト                     |
| poi.poiinfo[0].poiid               | Integer | POI ID                                   |
| poi.poiinfo[0].dpx                 | String  | display X座標(WGS84の場合longitude)         |
| poi.poiinfo[0].dpy                 | String  | display Y座標(WGS84の場合latitude)          |
| poi.poiinfo[0].rpx                 | String  | 探索X座標(WGS84の場合longitude)              |
| poi.poiinfo[0].rpy                 | String  | 探索Y座標(WGS84の場合latitude)               |
| poi.poiinfo[0].name1               | String  | 正式名称                              |
| poi.poiinfo[0].name2               | String  | 略称                              |
| poi.poiinfo[0].name3               | String  | 拡張名称1                                  |
| poi.poiinfo[0].name4               | String  | 拡張名称2                                  |
| poi.poiinfo[0].admcode             | String  | 行政コード                            |
| poi.poiinfo[0].jibun               | String  | 地番                                 |
| poi.poiinfo[0].address             | String  | 住所                               |
| poi.poiinfo[0].roadname            | String  | 新住所の道路名                            |
| poi.poiinfo[0].roadjibun           | String  | 新住所の地番                             |
| poi.poiinfo[0].detailaddress       | String  | 詳細住所                            |
| poi.poiinfo[0].catecode            | String  | 分類コード                            |
| poi.poiinfo[0].catename            | String  | 分類名称                              |
| poi.poiinfo[0].fulladdress         | String  | 全体住所(行政住所+地番+詳細住所)                      |
| poi.poiinfo[0].zip                 | String  | 郵便番号                             |
| poi.poiinfo[0].homeage             | String  | Webサイトurl                                 |
| poi.poiinfo[0].email               | String  | メール                              |
| poi.poiinfo[0].howtogo             | String  | 交通手段                                |
| poi.poiinfo[0].tel1                | String  | 電話番号1                                   |
| poi.poiinfo[0].tel2                | String  | 電話番号2                                   |
| poi.poiinfo[0].fax1                | String  | Fax番号1                                   |
| poi.poiinfo[0].fax2                | String  | Fax番号2                                   |
| poi.poiinfo[0].icode               | String  | ICODE                                    |
| poi.poiinfo[0].detail_count        | Integer | 分類詳細項目数                        |
| poi.poiinfo[0].etc_count           | Integer | 分類その他項目数                        |
| poi.poiinfo[0].badgeflag           | Boolean | バッジの有無(Not Yet:FALSE, Badged:TRUE)        |
| poi.poiinfo[0].imagecount          | Integer | POIイメージ数                         |
| poi.poiinfo[0].hasoildata          | Boolean | ガソリン価格データの有無                       |
| poi.poiinfo[0].detailinfo          | Array   | 分類詳細項目                         |
| poi.poiinfo[0].detailinfo[0].name  | String  | 分類詳細項目説明                      |
| poi.poiinfo[0].detailinfo[0].value | String  | 分類詳細項目内容                      |
| poi.poiinfo[0].etcinfo             | Array   | 分類その他項目                         |
| poi.poiinfo[0].etcinfo[0].name     | String  | 分類その他項目説明                      |
| poi.poiinfo[0].etcinfo[0].value    | String  | 分類その他項目内容                      |
| poi.poiinfo[0].oildata             | Object  | ガソリン価格データ情報                        |
| poi.poiinfo[0].oilda.tag_price     | Integer | レギュラー価格                           |
| poi.poiinfo[0].oilda.hg_price      | Integer | ハイオク価格                         |
| poi.poiinfo[0].oilda.d_price       | Integer | 軽油価格                            |
| poi.poiinfo[0].oilda.l_price       | Integer | LPG価格                           |
| poi.poiinfo[0].oilda.updatetime    | String  | アップデート時間                          |
| poi.poiinfo[0].oilda.priceinfo     | String  | 最高、最低ガソリン価格情報<br>(H：最高、L：最低、X：該当なし)<br>レギュラー、ハイオク、軽油、LPG順 |
| poi.poiinfo[0].oilda.wash          | Boolean | 洗車施設有無                           |
| poi.poiinfo[0].oilda.fix           | Boolean | 整備可否                           |
| poi.poiinfo[0].oilda.mart          | Boolean | 売店有無                              |

### 6\. POI下位施設検索

* 特定POIの下位施設を検索します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v1.0/appkeys/{appkey}/sub-pois?poiid={poiid}&x1={x1}&y1={y1} |

[Path parameter]

| 名前 | タイプ | 必須かどうか | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Query Parameters]

| 名前 | タイプ | 必須かどうか | 有効範囲                            | 説明          |
| ----- | ------ | ----- | ---------------------------------------- | ------------------- |
| poiid | String | 必須 |                                          | POI ID<br>複数サポートされない |
| x1    | String | 任意 | 現在地またはマップ中心座標<br>X、Y座標がすべてNULLまたは0の場合、距離計算を実行しない |                     |
| x1    | String | 任意 | 現在地またはマップ中心座標<br>X、Y座標がすべてNULLまたは0の場合、距離計算を実行しない |                     |

#### レスポンス

##### レスポンス本文

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
        "name1": "乗り換え駐車場",
        "name2": "",
        "name3": "",
        "name4": "",
        "admcode": "4113511000",
        "jibun": "",
        "address": "京畿道城南市盆唐区柏峴洞",
        "roadname": "",
        "roadjibun": "",
        "detailaddress": "",
        "catecode": "161701",
        "catename": "駐車場",
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
        "name1": "1番出口",
        "name2": "",
        "name3": "",
        "name4": "",
        "admcode": "4113511000",
        "jibun": "",
        "address": "京畿道城南市盆唐区柏峴洞",
        "roadname": "",
        "roadjibun": "",
        "detailaddress": "",
        "catecode": "173000",
        "catename": "地下鉄",
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

##### フィールド

| 名前                       | タイプ | 説明                               |
| -------------------------------- | ------- | ---------------------------------------- |
| header                           | Object  | ヘッダ領域                            |
| header.isSuccessful              | Boolean | 成否                            |
| header.resultCode                | Integer | 失敗コード                            |
| header.resultMessage             | String  | 失敗メッセージ                           |
| subpoi                           | Object  | 本文領域                            |
| subpoi.result                    | Boolean | 成否                            |
| subpoi.totalcount                | String  | 全体検索結果対象数                      |
| subpoi.count                     | String  | 検索結果数                           |
| subpoi.poi                       | Array   | POI検索結果リスト                     |
| subpoi.poi[0].poiid              | Integer | POI ID                                   |
| subpoi.poi[0].depth              | String  | POI depth                                |
| subpoi.poi[0].dpx                | String  | display X座標(WGS84の場合longitude)         |
| subpoi.poi[0].dpy                | String  | display Y座標(WGS84の場合latitude)          |
| subpoi.poi[0].rpx                | String  | 探索X座標(WGS84の場合longitude)              |
| subpoi.poi[0].rpy                | String  | 探索Y座標(WGS84の場合latitude)               |
| subpoi.poi[0].name1              | String  | 正式名称                               |
| subpoi.poi[0].name2              | String  | 略称                               |
| subpoi.poi[0].name3              | String  | 拡張名称1                                    |
| subpoi.poi[0].name4              | String  | 拡張名称2                                    |
| subpoi.poi[0].admcode            | String  | 行政コード                             |
| subpoi.poi[0].address            | String  | 住所                               |
| subpoi.poi[0].jibun              | String  | 地番                                 |
| subpoi.poi[0].roadname           | String  | 新住所の道路名                            |
| subpoi.poi[0].roadjibun          | String  | 新住所の地番                             |
| subpoi.poi[0].detailaddress      | String  | 詳細住所                             |
| subpoi.poi[0].catecode           | String  | 分類コード                             |
| subpoi.poi[0].catename           | String  | 分類名称                               |
| subpoi.poi[0].dp_catecode        | String  | DP分類コード                          |
| subpoi.poi[0].distance           | Integer | 座標との距離(該当する時のみ)                         |
| subpoi.poi[0].tel                | String  | 電話番号                             |
| subpoi.poi[0].hasoildata         | Boolean | ガソリン価格データの有無                       |
| subpoi.poi[0].hasdetailinfo      | Boolean | 詳細情報の有無                         |
| subpoi.poi[0].hassubpoi          | Boolean | 下位施設の有無                         |
| subpoi.poi[0].adv_count          | Boolean | 広告コード数                           |
| subpoi.poi[0].islandmark         | Boolean | ランドマークかどうか                            |
| subpoi.poi[0].updateTS           | String  | 最終変更日時(Y4-MM-DD HH:mm:ss)フォーマット     |
| subpoi.poi[0].data_source        | String  | POI作成情報区分(Thinkware/Tel/User)        |
| subpoi.poi[0].badgeflag          | Boolean | バッジ有無(Not Yet: FALSE, Badged: TRUE)      |
| subpoi.poi[0].userid             | String  | POI登録ユーザーID (UCPの場合にのみ)                |
| subpoi.poi[0].imagecount         | Integer | POIイメージ数                         |
| subpoi.poi[0].oildata            | Object  | ガソリン価格データ情報                        |
| subpoi.poi[0].oildata.g_price    | Integer | レギュラー価格                           |
| subpoi.poi[0].oildata.hg_price   | Integer | ハイオク価格                         |
| subpoi.poi[0].oildata.d_price    | Integer | 軽油価格                            |
| subpoi.poi[0].oildata.l_price    | Integer | LPG価格                           |
| subpoi.poi[0].oildata.updatetime | String  | Update時間                        |
| subpoi.poi[0].oildata.priceinfo  | String  | 最高、最低ガソリン価格情報<br>(H：最高、L：最低、X：該当なし)<br>レギュラー、ハイオク、軽油、LPG順 |
| subpoi.poi[0].oildata.wash       | Boolean | 洗車施設有無                             |
| subpoi.poi[0].oildata.fix        | Boolean | 整備可否                             |
| subpoi.poi[0].oildata.mart       | Boolean | 売店有無                               |
| subpoi.poi[0].AdInfo             | Array   | 広告コードリスト                         |
| subpoi.poi[0].AdInfo[0].ADCODE   | Integer | 広告コード<br>1～99まで付与可能(最大99個)              |
| subpoi.poi[0].subpoi             | Object  | 下位施設情報                        |
| subpoi.poi[0].subpoi.count       | Integer | subpoi数                          |
| subpoi.poi[0].subpoi.poi         | Array   | POI情報と同じ                         |

### 7\. 座標変換

* WGS84 <-> TM座標間の変換値を返します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v1.0/appkeys/{appkey}/trans-coordinates?coordtype={coordtype}&x={x}&y={y} |

[Path parameter]

| 名前 | タイプ | 必須かどうか | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Query Parameters]

| 名前 | タイプ | 必須かどうか | 有効範囲                         | 説明                           |
| --------- | ------ | ----- | ------------------------------------- | ------------------------------------ |
| coordtype | String | 必須 |                                       | 0：WGS84 -> TM <br> 1：TM -> WGS84 |
| x         | double | 必須 | 現在地またはマップ中心座標<br>WGS84座標またはTM座標 |                                      |
| y         | double | 必須 | 現在地またはマップ中心座標<br>WGS84座標またはTM座標 |                                      |

#### レスポンス

##### レスポンス本文

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

##### フィールド

| 名前           | タイプ | 説明 |
| -------------------- | ------- | -------- |
| header               | Object  | ヘッダ領域 |
| header.isSuccessful  | Boolean | 成否 |
| header.resultCode    | Integer | 失敗コード |
| header.resultMessage | String  | 失敗メッセージ |
| coordinate           | Object  | 本文領域 |
| coordinate.coordtype | String  | 変換座標形式 |
| coordinate.x         | String  | 変換X座標 |
| coordinate.y         | String  | 変換Y座標 |

## 探索

### 1\. 経路探索の要約

* 入力した座標への経路探索結果要約情報を検索します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v1.0/appkeys/{appkey}/routes?startX={startX}&startY={startY}&endX={endX}&endY={endY}&viaCount={viaCount}&via1X={via1X}&via1Y={via1Y}&via2X={via2X}&via2Y={via2Y}&option={option} |

[Path parameter]

| 名前 | タイプ | 必須かどうか | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Query Parameters]

| 名前 | タイプ | 必須かどうか | 有効範囲 | 説明                               |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| startX   | String | 必須 |       | 出発地X座標                          |
| startY   | String | 必須 |       | 出発地Y座標                          |
| endX     | String | 必須 |       | 到着地X座標                          |
| endY     | String | 必須 |       | 到着地Y座標                          |
| viaCount | String | 任意 |       | 経由地数                             |
| via1X    | String | 任意 |       | 経由地1 X座標                         |
| via1Y    | String | 任意 |       | 経由地1 Y座標                         |
| via2X    | String | 任意 |       | 経由地2 X座標                         |
| via2Y    | String | 任意 |       | 経由地2 Y座標                         |
| option   | String | 必須 |       | 経路探索オプション<br>探索option ","単位でリクエスト<br>ex\) option=real\_traffic\,real\_traffic2<br>freeroad_priority：無料<br>highway_priority：高速道路<br>real_traffic：リアルタイム<br>real\_traffic\_freeroad：リアルタイム\(無料\)<br>real_traffic：推薦1<br>real_traffic2：推薦2<br>rt_stats：リアルタイム統計<br>rt\_stats\_freeroad：リアルタイム統計\(無料\)<br>short\_distance\_priority：短距離<br>stats：統計<br>stats_freeroad：統計(無料)<br>motorcycle：二輪車 |

#### レスポンス

##### レスポンス本文

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

##### フィールド

| 名前               | タイプ | 説明      |
| ------------------------ | ------- | --------------- |
| header                   | Object  | ヘッダ領域   |
| header.isSuccessful      | Boolean | 成否   |
| header.resultCode        | Integer | 失敗コード   |
| header.resultMessage     | String  | 失敗メッセージ  |
| route                    | Object  | 本文領域   |
| route.SummaryResult      | Array   | リクエスト経路結果リスト |
| route.SummaryResult[0].0 | String  | オプション名   |
| route.SummaryResult[0].1 | Integer | 経路探索距離(単位: m) |
| route.SummaryResult[0].2 | Integer | 経路探索時間(単位：分) |

### 2\. 経路探索詳細

* 入力した座標への経路探索結果詳細情報を検索します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v1.0/appkeys/{appkey}/route-details?startX={startX}&startY={startY}&endX={endX}&endY={endY}&viaCount={viaCount}&via1X={via1X}&via1Y={via1Y}&via2X={via2X}&via2Y={via2Y}&option={option} |

[Path parameter]

| 名前 | タイプ | 必須かどうか | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Query Parameters]

| 名前 | タイプ | 必須かどうか | 有効範囲 | 説明                               |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| startX   | String | 必須 |       | 出発地X座標                         |
| startY   | String | 必須 |       | 出発地Y座標                         |
| endX     | String | 必須 |       | 到着地X座標                         |
| endY     | String | 必須 |       | 到着地Y座標                         |
| viaCount | String | 任意 |       | 経由地数                             |
| via1X    | String | 任意 |       | 経由地1 X座標                       |
| via1Y    | String | 任意 |       | 経由地1 Y座標                       |
| via2X    | String | 任意 |       | 経由地2 X座標                       |
| via2Y    | String | 任意 |       | 経由地2 Y座標                       |
| option   | String | 必須 |       | 経路探索オプション<br>探索オプション1つのみ可能<br>例) option=real_traffic<br>freeroad_priority：無料<br>highway_priority：高速道路<br>real_traffic：リアルタイム<br>real\_traffic\_freeroad：リアルタイム\(無料\)<br>real_traffic：推薦1<br>real_traffic2：推薦2<br>rt_stats：リアルタイム統計<br>rt\_stats\_freeroad：リアルタイム統計\(無料\)<br>short\_distance\_priority：短距離<br>stats：統計<br>stats_freeroad：統計(無料)<br>motorcycle：二輪車 |

#### レスポンス

##### レスポンス本文

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
      "一般道路",
      "板橋駅路242番道",
      "板橋駅路226番道",
      "一般道路",
      "大王板橋路644番道",
      "右折",
      "右折",
      "右折",
      "柏峴洞、板橋(板橋テクノバレー)駅"
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

##### フィールド

| 名前                  | タイプ | 説明                               |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | ヘッダ領域                            |
| header.isSuccessful         | Boolean | 成否                            |
| header.resultCode           | Integer | 失敗コード                            |
| header.resultMessage        | String  | 失敗メッセージ                           |
| routeDetail                 | Object  | 本文領域                            |
| RouteInfo                   | Object  | 経路情報                            |
| RouteInfo.dist              | Integer | 経路の総距離(単位：m)                          |
| RouteInfo.time              | Integer | 経路の総所要時間(単位：分)                        |
| RouteInfo.sec_cnt           | Integer | 区間情報レコード数                        |
| RouteInfo.dtl_cnt           | Integer | 区間詳細情報レコード数                     |
| RouteInfo\.rd\_name\_cnt    | Integer | 道路名称レコード数                       |
| RouteInfo\.guide\_name\_cnt | Integer | 案内名称レコード数                       |
| RouteInfo\.cross\_name\_cnt | Integer | 交差点名称レコード数                      |
| RouteInfo\.dir\_name\_cnt   | Integer | 方面名称レコード数                       |
| RouteInfo.vtx_cnt           | Integer | 補間点(経路ファクター座標)数                   |
| RouteInfo.rest_cnt          | Integer | 休憩所数                             |
| RouteInfo.toll_cnt          | Integer | 料金所数                             |
| RouteInfo.max_x             | Integer | 補間点レコード中最大X座標                |
| RouteInfo.max_y             | Integer | 補間点レコード中最大Y座標                |
| RouteInfo.min_x             | Integer | 補間点レコード中最小X座標                |
| RouteInfo.min_y             | Integer | 補間点レコード中最小Y座標                |
| SecInfoRec                  | Array   | 区間情報レコード                         |
| SecInfoRec[0].0             | Integer | 区間の距離(m)                               |
| SecInfoRec[0].1             | Integer | 区間速度                            |
| SecInfoRec[0].2             | Integer | 道路番号または道路名称インデックス                  |
| SecInfoRec[0].3             | String  | 区間詳細情報レコード数                    |
| SecInfoRec[0].4             | String  | 区間詳細情報テーブルインデックス                   |
| DtlInfoRec                  | Array   | 区間詳細情報レコード                     |
| DtlInfoRec[0].0             | Integer | 区間詳細距離                           |
| DtlInfoRec[0].1             | Integer | 区間詳細速度                         |
| DtlInfoRec[0].2             | String  | 案内名称インデックス                          |
| DtlInfoRec[0].3             | String  | 交差点名称インデックス                         |
| DtlInfoRec[0].4             | String  | 方面名称インデックス                          |
| DtlInfoRec[0].5             | String  | 道路の種別                              |
| DtlInfoRec[0].6             | Integer | 案内地点補間点インデックス                      |
| NameRec                     | Array   | 名称レコード                           |
| NameRec[0].0                | String  | 高速道路名称or案内名称or交差点名称or方面名称 |
| VtxRec                      | Array   | 補間点レコード - 経路ファクター座標配列<br>[[twX1, twY1], [twX2, twY2], … [twXn, twYn]] |
| VtxRec[0].0                 | Integer | twX                                      |
| VtxRec[0].1                 | Integer | twY                                      |
| RestRec                     | Array   | 名称レコード                           |
| RestRec[0].0                | String  | 高速モードコード                         |
| RestRec[0].1                | String  | ガソリンスタンド業者コード<br>(0：なし、1：LG , 2：SK, 3：双竜、4：ハンファ、5：現代) |
| RestRec[0].2                | String  | LPG有無<br>[0：なし、1：あり]               |
| RestRec[0].3                | String  | 整備所の有無<br>[0：なし、1：あり]               |
| RestRec[0].4                | String  | 高速モードタイプ                         |
| RestRec[0].5                | String  | Reserved                                 |
| RestRec[0].6                | String  | 休憩所の名称                             |

### 3\. 経路探索詳細\(json Parsing\)

#### 経路探索結果値を見やすくParsing

```
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/js/v1.0/route.js" > </script>
<script type="text/javascript">
function fnRouteParse(data){ // 経路探索詳細結果値

  var routeParsing = route.jsonParsing(data);
  routeParsing.routeSummaryInfo;		// 探索結果総合
  routeParsing.routeDetailInfo;		// 探索経路リスト
  routeParsing.vtxInfo; 			// マップ描写用座標リスト
}
</script>
```

#### フィールド

| 名前                      | タイプ | 説明           |
| ------------------------------- | ------- | -------------------- |
| routeSummaryInfo                | Object  | 探索結果総合       |
| routeSummaryInfo.distance       | Integer | 経路の総距離(単位：m)      |
| routeSummaryInfo.time           | Integer | 経路の総所要時間(単位：分)   |
| routeSummaryInfo.max_x          | String  | 補間点レコード中、最大X座標 |
| routeSummaryInfo.max_y          | String  | 補間点レコード中、最大Y座標 |
| routeSummaryInfo.min_x          | String  | 補間点レコード中、最小X座標 |
| routeSummaryInfo.min_y          | String  | 補間点レコード中、最小Y座標 |
| routeDetailInfo                 | Array   | 探索経路リスト     |
| routeDetailInfo.distance        | Integer | 区間詳細距離(単位：m)     |
| routeDetailInfo.speed           | Integer | 区間詳細速度(単位：km/h) |
| routeDetailInfo.roadName        | String  | 道路名            |
| routeDetailInfo.direction       | String  | 方向情報        |
| routeDetailInfo.district        | String  | 方面情報        |
| routeDetailInfo.cross           | String  | 案内情報        |
| routeDetailInfo.directionDetail | String  | 詳細経路説明     |
| vtxInfo                         | Array   | マップ描写用座標リスト |
| vtxInfo[0].0                    | Integer | twX                  |
| vtxInfo[0].1                    | Integer | twY                  |
