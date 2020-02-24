## Application Service > Maps > Android 지도 SDK 가이드
Android 플랫폼에서 아이나비 지도를 사용하기 위한 프로젝트 기본 설정 방법을 설명합니다.

### 사전 준비
- 아이나비 지도를 사용하기 위해서는 인증을 위한 **Appkey**가 필요합니다.

#### 서비스 활성화
- **[NHN TOAST Console]** 에서 서비스 선택 후 Application Service > Maps를 클릭합니다

#### Appkey 확인
- **Appkey**는 **TOAST Console** 상단 **URL & Appkey** 메뉴에서 확인할 수 있습니다.


### Project 환경 구성
다음과 같이 Project 및 App 모듈 레벨의 build.gradle 파일에 아이나비 지도 저장소를 추가하고, 의존성을 설정합니다.
> 아이나비 지도 Android SDK는 Bintray를 통해 배포되며, Beta 기간 종료 후에는 정책에 맞춰 변경될 수 있습니다. (사전 공지 예정)

```gradle
/* Root Project build.gradle */

allprojects {
    repositories {
        google()
        ...
        // 아이나비 지도 저장소
        maven {
            url 'https://dl.bintray.com/inavi-systems/maps/'
        }
    }
}
```

```gradle
/* App Module build.gradle */

dependencies {
    implementation 'com.inavi.mapsdk:inavi-maps-sdk:0.4.0'
}
```


### Appkey 설정
발급받은 Appkey를 설정할 수 있도록 아래의 두 가지 방법을 제공합니다. 

> Appkey가 설정되지 않으면 지도 초기화 단계에서 인증 오류가 발생합니다.

#### 1. AndroidManifest.xml에서 설정
`AndroidManifest.xml`에 `<meta-data>`를 추가하여 Appkey를 설정할 수 있습니다.
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

#### 2. InaviMapSdk API 호출로 설정
Application 생성 시점에 동적으로 [InaviMapSdk] 싱글턴 객체의 함수를 호출하여 Appkey를 설정할 수 있습니다.

```kotlin
// Kotlin
InaviMapSdk.getInstance(context).appKey = "YOUR_APP_KEY"
```

#### 인증 실패
지도 초기화 단계에 인증이 실패하면 SDK 내부에서 등록된 Callback으로 에러 코드와 메시지를 전달합니다.
실패에 대한 Callback을 받으려면 [InaviMapSdk] 싱글턴 객체에 [AuthFailureCallback]을 아래와 같이 설정해야 합니다.
```kotlin
// Kotlin
InaviMapSdk.getInstance(context).authFailureCallback =
    InaviMapSdk.AuthFailureCallback { errCode: Int, msg: String ->
        // 인증 실패 처리
}
```
>인증 실패 Callback을 별도로 설정하지 않으면 기본적으로 에러 코드와 메시지가 팝업 형태로 표출됩니다.

#### 인증 에러 코드
| Code | Description |
| ------ | ------ |
| 300 | APP KEY 유효하지 않음
| 401 | APP KEY 설정되지 않음 |
| 503 | 서버 연결 실패 |
| 504 | 서버 연결 시간 초과 |
| 500 | 알 수 없는 에러 |
| 그 외 | 서버 에러 (추후 정의 시 업데이트) |

### 지도 생성하기
앱 화면에 아이나비 지도를 표출하는 방법을 설명합니다.

#### 지도 표시
액티비티 레이아웃 파일에 아래와 같이 `<fragment>` 태그를 추가하고 [InvMapFragment]를 정의하면 지도를 표출할 수 있습니다.
```xml
<fragment
    android:id="@+id/map_fragment"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:name="com.inavi.mapsdk.maps.InvMapFragment" />
```

#### 지도 객체 접근
지도와 관련된 모든 조작은 [InaviMap] 객체를 통해 이루어집니다.
[InaviMap] 객체에 접근하기 위해서는 우선 [InvMapFragment] 객체의 getMapAsync() 함수를 호출해야 합니다.
지도 초기화가 완료되면 onMapReady() 콜백 함수를 통해 [InaviMap] 객체가 전달됩니다.
```kotlin
// Kotlin
val mapFragment = supportFragmentManager.findFragmentById(R.id.map_fragment) as InvMapFragment
mapFragment.getMapAsync(object : OnMapReadyCallback {
    override fun onMapReady(inaviMap: InaviMap) {
        // InaviMap 객체 접근 가능
    }
})
```

#### 지도 이벤트 설정
지도 클릭, 더블 클릭, 롱 클릭 등 지도와 사용자간 상호작용에 대한 이벤트를 설정할 수 있습니다.
```kotlin
// Kotlin
inaviMap.setOnMapClickListener { pointF, latLng ->
    // pointF : 클릭한 지점의 화면상 좌표
    // latLng : 클릭한 지점의 지도상 좌표
    Toast.makeText(context, "지도 클릭", Toast.LENGTH_SHORT).show()
}
```

#### 마커 표출
마커 객체를 생성하고 `position` 속성과 `map` 속성을 설정하면 마커가 표출됩니다.
```kotlin
// Kotlin
val marker = InvMarker().apply {
    position = LatLng(37.40219, 127.11077)
    title = "타이틀"
    map = inaviMap
}
```

#### 마커 제거
마커 객체의 map 속성을 `null`로 설정하시면 마커가 제거됩니다.
```kotlin
// Kotlin
marker.map = null
```

#### 카메라 이동
[CameraUpdate]의 팩토리 메서드 또는 [CameraUpdateBuilder]를 통해 [CameraUpdate] 객체를 생성한 다음
moveCamera() 함수에 파라미터를 전달하여 호출하면 카메라가 이동됩니다.

애니메이션과 카메라 이벤트에 대한 콜백을 지원하므로, 카메라 이동을 원하는 대로 구현할 수 있습니다.
```kotlin
// Kotlin
val cameraUpdate = CameraUpdate.targetTo(LatLng(36.99473, 127.81832))
cameraUpdate.setAnimationType(CameraAnimationType.Fly, 3000)
inaviMap.moveCamera(cameraUpdate)
```


## 주요 iNavi Maps SDK 안내
추가적인 Maps SDK 사용법은 [iNavi Maps API 센터](http://imapsapi.inavi.com/)를 참고하시기 바랍니다.

[InaviMapSdk] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/android/com/inavi/mapsdk/maps/InaviMapSdk.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/android/com/inavi/mapsdk/maps/InaviMapSdk.html)
[InaviMap] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/android/com/inavi/mapsdk/maps/InaviMap.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/android/com/inavi/mapsdk/maps/InaviMap.html)
[InvMapView] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/android/com/inavi/mapsdk/maps/InvMapView.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/android/com/inavi/mapsdk/maps/InvMapView.html)
[InvMapFragment] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/android/com/inavi/mapsdk/maps/InvMapFragment.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/android/com/inavi/mapsdk/maps/InvMapFragment.html)
[AuthFailureCallback] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/android/com/inavi/mapsdk/maps/InaviMapSdk.AuthFailureCallback.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/android/com/inavi/mapsdk/maps/InaviMapSdk.AuthFailureCallback.html)
[CameraUpdate] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/android/com/inavi/mapsdk/maps/CameraUpdate.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/android/com/inavi/mapsdk/maps/CameraUpdate.html)
[CameraUpdateBuilder] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/android/com/inavi/mapsdk/maps/CameraUpdateBuilder.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/android/com/inavi/mapsdk/maps/CameraUpdateBuilder.html)

[NHN TOAST Console] : [https://console.toast.com/](https://console.toast.com/)
