## Application Service > Maps > Webマップガイド

Maps Webマップを使用するのに必要なJavaScript基盤Web APIを説明します。


## API共通情報

### 事前準備
- APIを使用するにはアプリケーションキーが必要です。
- アプリケーションキーは、**TOAST Console**上部にある**URL & Appkey**メニューで確認できます。

### リクエスト共通情報

#### URL情報

| 項目     | URL                                      |
| --------- | ---------------------------------------- |
| マップ     | https://api-maps.cloud.toast.com |


## Webマップ

### 1. Webマップ

JavaScript基盤のTOAST Maps APIを利用してWebブラウザにマップを表示する方法を説明します。
TOAST Maps APIは、WGS84(EPSG:4326)座標を使用します。


#### 主要Maps API案内
##### Maps APIの詳細な使用方法は<a href="http://imapsapi.inavi.com/" target="_blank" rel="nofollow">iNavi Maps API Center</a>を参照してください。 <p>


| API名                                 | Parameter                        | Returns                                  | 説明                              |
| ---------------------------------------- | -------------------------------- | ---------------------------------------- | ---------------------------------------- |
| new inavi.maps.Map(options)  | options.container : string                 | inavi.maps.Mapマップオブジェクト | マップを表示するDOMエレメントのID             |
|                                          | options.type : string             |                                          | マップのタイプ <br> 'NORMAL' ：一般マップ、<br> 'SATTELITE' ：航空写真<br>default: 'NORMAL' |
|                                          | options.center : LngLatLike       |                                          | マップの中心座標               |
|                                          | options.zoom : number            |                                          | マップのレベル                                |
|                                          | options.heading : number             |                                          | 北を基準に反時計方向に回転した角度 |
|                                          | options.tilt : number             |                                          | マップを横にした時の傾き |
|                                          | options.maxZoom : number             |                                          | 北を基準に反時計方向に回転した角度 |
|                                          | options.heading : number             |                                          | 最大拡大レベル |
|                                          | options.hash : boolean             |                                          | アドレス表示バーにマップ情報を表示するかどうか |
|                                          | options.zoomable : boolean             |                                          | 拡大可否 |
|                                          | options.draggable : boolean             |                                          | ドラッグ可否 |
|                                          | options.rotatable : boolean             |                                          | 回転可否 |
|                                          | options.keyboard : boolean             |                                          | キーボードを使用したマップ移動可否 |
|                                          | options.disableDefaultUI : boolean             |                                          | 基本コントロールを隠すかどうか |
|                                          | options.logoScaleControl : LogoScaleControlOptions             |                                          | ロゴおよびスケール表示コントロールオプション |
|                                          | options.compassControl : CompassControlOptions             |                                          | 羅針盤表示コントロールオプション |
|                                          | options.zoomControl : ZoomControlOptions             |                                          | 拡大縮小表示コントロールオプション |
| changeType(type)                         | type : string                    |                                          | マップのタイプ <br> 'NORMAL'：一般マップ、<br> 'SATTELITE'：航空<br>default：'NORMAL' |
| on(eventType, listener) | eventType : string              |                                          | load,<br>zoomstart, zoom, zoomend,<br>rotatestart, rotate, rotateend,<br>tiltstart, tilt, tiltend,<br>click, dblclick,<br>mousedown, mouseup, mousemove,<br>mouseenter, mouseleave, mouseover, mouseout,<br>contextmenu,<br>wheel,<br>touchstart, touchend, touchcancel, touchmove,<br>movestart, move, moveend,<br>dragstart, drag, dragend|
|                                          | listener : Function             |                                          | 登録するリスナー                               |
| once(eventType, listener) | eventType : string              |                                          | load,<br>zoomstart, zoom, zoomend,<br>rotatestart, rotate, rotateend,<br>tiltstart, tilt, tiltend,<br>click, dblclick,<br>mousedown, mouseup, mousemove,<br>mouseenter, mouseleave, mouseover, mouseout,<br>contextmenu,<br>wheel,<br>touchstart, touchend, touchcancel, touchmove,<br>movestart, move, moveend,<br>dragstart, drag, dragend|
|                                          | listener : Function             |                                          | 登録するリスナー                               |
| off(eventType, listener) | eventType : string              |                                          | load,<br>zoomstart, zoom, zoomend,<br>rotatestart, rotate, rotateend,<br>tiltstart, tilt, tiltend,<br>click, dblclick,<br>mousedown, mouseup, mousemove,<br>mouseenter, mouseleave, mouseover, mouseout,<br>contextmenu,<br>wheel,<br>touchstart, touchend, touchcancel, touchmove,<br>movestart, move, moveend,<br>dragstart, drag, dragend|
|                                          | listener : Function             |                                          | 削除するリスナー                               |
| new inavi.maps.Marker(option)        | option.map : Map              | inavi.maps.Markerマーカーオブジェクト | マップオブジェクト                                 |
|                                          | option.icon : string         |                                          | アイコンURL                                   |
|                                          | option.position : LngLatLike     |                                          | マーカー作成座標                 |
|                                          | option.anchor : string      |                                          | 座標が位置する場所<br> top-left, top, top-right,<br>left, center, right,<br>bottom-left, bottom, bottom-right |
|                                          | option.title : string            |                                          | ツールチップ文字列                                |
|                                          | option.offset : Array       |                                          | ピクセル単位オフセット                                  |
|                                          | option.draggable : boolean       |                                          | ドラッグ可否                              |
|                                          | option.zIndex : number           |                                          | z-index値                             |
|                                          | option.opacity : number          |                                          | 透明度                                    |
| inavi.maps.LngLat.convertToPixel(lngLat) | lngLat.lng : number               | 画面ピクセル座標 | WGS84経度                              |
|                                          | lngLat.lat : number               |                                          | WGS84緯度                              |
| inavi.maps.Pixel.convertToLngLat(pixel) | pixel.pxX : number               | 経緯度座標 | 画面ピクセルx座標                                    |
|                                          | pixel.pxY : number               |                                          | 画面ピクセルy座標                                    |


#### Maps API使用
```html
<script type="text/javascript" src="https://api-maps.cloud.toast.com/maps/v3.0/appkeys/{appkey}/maps?callback=initMap"></script>
<div id="div_map"></div>
<script type="text/javascript">
    function initMap() {
        //宣言したDIVにマップを表示します。
        var map = new inavi.maps.Map({
            container: "div_map",
            center: {
                lng: 127.11,
                lat: 37.40
            },
            zoom: 12,
            type: "NORMAL"
        });
    }
</script>
```

#### マップモードの変更
```html
<script type="text/javascript">
    // 作成されたマップオブジェクトのマップTypeを変更します。
    // 一般：NORMAL、航空写真：SATTELITE
    // 航空写真に変更します。
    map.setType("SATTELITE");
</script>
```

#### マップにイベントを登録
```html
<script type="text/javascript">
    //マップにmoveイベントを登録します。
    map.addListener("click", clickHandler)

    //マップイベント発生時のコールバック関数
    function clickHandler(event){
        console.log("event callback!");
    }
</script>
```

#### マップのイベントを削除
```html
<script type="text/javascript">
    //マップのmoveイベントを削除します。
    map.off("move", moveHandler)
</script>
```

#### マップマーカーの追加
```html
<script type="text/javascript">
    // マップにマーカーオブジェクトを追加します。
    var marker = new inavi.maps.Marker({
        map: map,
        position: {
            lng: 127.11,
            lat: 37.40
        }
    });

    // マーカーオブジェクトを移動させます。
    marker.setPosition({lng: 127.2, lat: 37.5});
</script>
```

#### 画面ピクセル座標をWGS座標に変換
```html
<script type="text/javascript">
    // 画面ピクセル座標をWGS座標に変換します。
    var screen_pixel = {
        pxX: 100,
        pxY: 100
    };

    var wgs84 = inavi.maps.Pixel.convertToLngLat(screen_pixel);
    console.log(wgs84.lon);
    console.log(wgs84.lat);
</script>
```

#### WGS座標を画面ピクセル座標に変換
```html
<script type="text/javascript">
    // WGS座標を画面ピクセル座標に変換します。
    var wgs84 = {
        lon: 127.11074994024005,
        lat: 37.40215870673785
    };

    var screen_pixel = inavi.maps.LngLat.convertToPixel(wgs84);
    console.log(screen_pixel.pxX);
    console.log(screen_pixel.pxY);
</script>
```
