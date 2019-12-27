## Application Service > Maps > AndroidマップSDKガイド
Androidプラットフォームでinaviマップを使用するためのプロジェクト基本設定方法を説明します。

### 事前準備
- inaviマップを使用するには、認証用の**Appkey**が必要です。

#### サービス有効化
- **[NHN TOAST Console]**でサービスを選択し、Application Service > Mapsをクリックします。

#### Appkey確認
- **Appkey**は、**TOAST Console**上部の**URL & Appkey**メニューで確認できます。


### Project環境構成
次のようにProjectおよびAppモジュールレベルのbuild.gradleファイルにinaviマップ保存場所を追加し、依存性を設定します。

> inaviマップAndroid SDKはBintrayを通して配布され、Beta期間終了後はポリシーに合わせて変更される場合があります。(事前告知予定)

```gradle
/* Root Project build.gradle */

allprojects {
    repositories {
        google()
        ...
        // inaviマップ保存場所
        maven {
            url 'https://dl.bintray.com/inavi-systems/maps/'
        }
    }
}
```

```gradle
/* App Module build.gradle */

dependencies {
    implementation 'com.inavi.mapsdk:inavi-maps-sdk:0.3.0'
}
```


### Appkey設定
発行したAppkeyを設定する方法は下記のとおりです。

> Appkeyが設定されていない場合、マップ初期化段階で認証エラーが発生します。

#### 1. AndroidManifest.xmlで設定
`AndroidManifest.xml`に`<meta-data>`を追加してAppkeyを設定できます。
```xml
<!-- AndroidManifext.xml -->

<manifest>
    <application>
        <meta-data
            android:name="com.inavi.mapsdk.AppKey"
            android:value="YOUR_APP_KEY" />
    </application>
</manifest>
```

#### 2. InaviMapSdk APIを呼び出して設定
Application作成時点で動的に[InaviMapSdk]シングルトンオブジェクトの関数を呼び出してAppkeyを設定できます。

```kotlin
// Kotlin
InaviMapSdk.getInstance(context).appKey = "YOUR_APP_KEY"
```

#### 認証失敗
マップ初期化段階で認証に失敗した場合、SDK内部に登録されたCallbackでエラーコードとメッセージを伝達します。
失敗のCallbackを受けるには[InaviMapSdk]シングルトンオブジェクトに[AuthFailureCallback]を下記のように設定する必要があります。
```kotlin
// Kotlin
InaviMapSdk.getInstance(context).authFailureCallback =
    InaviMapSdk.AuthFailureCallback { errCode: Int, msg: String ->
        // 認証失敗処理
}
```
>認証失敗Callbackを別途設定していない場合は、エラーコードとメッセージがポップアップ表示されます。

#### 認証エラーコード
| Code | Description |
| ------ | ------ |
| 300 | APP KEYが無効
| 401 | APP KEYが未設定 |
| 503 | サーバー接続失敗 |
| 504 | サーバー接続時間超過 |
| 500 | 不明なエラー |
| その他 | サーバーエラー(今後定義したらアップデート) |

### マップを作成する
アプリ画面にinaviマップを表示する方法を説明します。

#### マップ表示
アクティビティレイアウトファイルに下記のように`<fragment>`タグを追加して[InvMapFragment]を定義するとマップを表示できます。
```xml
<fragment
    android:id="@+id/map_fragment"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:name="com.inavi.mapsdk.maps.InvMapFragment" />
```

#### マップオブジェクトにアクセス
マップに関するすべての操作は[InaviMap]オブジェクトを通して行われます。
[InaviMap]オブジェクトにアクセスするには、まず[InvMapFragment]オブジェクトのgetMapAsync()関数を呼び出す必要があります。
マップの初期化が完了したら、onMapReady()コールバック関数を通して[InaviMap]オブジェクトが伝達されます。
```kotlin
// Kotlin
val mapFragment = supportFragmentManager.findFragmentById(R.id.map_fragment) as InvMapFragment
mapFragment.getMapAsync(object : OnMapReadyCallback {
    override fun onMapReady(inaviMap: InaviMap) {
        // InaviMapオブジェクトアクセス可能
    }
})
```

#### マップイベント設定
マップクリック、ダブルクリック、長押しなど、マップとユーザー間のインタラクションに対するイベントを設定できます。
```kotlin

inaviMap.setOnMapClickListener { pointF, latLng ->
    // pointF：クリックした地点の画面上の座標
    // latLng：クリックした地点のマップ上の座標
    Toast.makeText(context, "マップクリック", Toast.LENGTH_SHORT).show()
}
```

#### マーカー表示
マーカーオブジェクトを作成し、`position`プロパティと`map`プロパティを設定すると、マーカーが表示されます。
```kotlin
// Kotlin
val marker = InvMarker().apply {
    position = LatLng(37.40219, 127.11077)
    title = "タイトル"
    map = inaviMap
}
```

#### マーカー削除
マーカーオブジェクトのmapプロパティを`null`に設定すると、マーカーが削除されます。
```kotlin
// Kotlin
marker.map = null
```

#### カメラ移動
[CameraUpdate]のFactory Methodまたは[CameraUpdateBuilder]を通して[CameraUpdate]オブジェクトを作成した後
moveCamera()関数にパラメータを伝達して呼び出すと、カメラが移動します。

アニメーションとカメライベントに対するコールバックをサポートするため、カメラ移動を自由に実装できます。
```kotlin
// Kotlin
val cameraUpdate = CameraUpdate.targetTo(LatLng(36.99473, 127.81832))
cameraUpdate.setAnimationType(CameraAnimationType.Fly, 3000)
inaviMap.moveCamera(cameraUpdate)
```


## 主要iNavi Maps SDK案内
Maps SDKの使用方法は[iNavi Maps APIセンター](http://imapsapi.inavi.com/)を参照してください。

[InaviMapSdk] : [http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InaviMapSdk.html](http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InaviMapSdk.html)
[InaviMap] : [http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InaviMap.html](http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InaviMap.html)
[InvMapView] : [http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InvMapView.html](http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InvMapView.html)
[InvMapFragment] : [http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InvMapFragment.html](http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InvMapFragment.html)
[AuthFailureCallback] : [http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InaviMapSdk.AuthFailureCallback.html](http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InaviMapSdk.AuthFailureCallback.html)
[CameraUpdate] : [http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/CameraUpdate.html](http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/CameraUpdate.html)
[CameraUpdateBuilder] : [http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/CameraUpdateBuilder.html](http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/CameraUpdateBuilder.html)

[NHN TOAST Console] : [https://console.toast.com/](https://console.toast.com/)

