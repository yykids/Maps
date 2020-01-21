## Application Service > Maps > SDK User Guide for Android Maps
Describes the basic project configuration method to enable iNavi maps on Android.  

### Prerequisites 
- To enable iNavi maps, **Appkey** is required for authentication. 

#### Enable Service 
- Go to **[NHN TOAST Console]**, select a service and click Application Service > Maps. 

#### Check Appkey 
- To check your appkey, go to **URL & Appkey** on top of the **TOAST Console**. 


### Project Configuration
Add a repository for iNavi maps in the build.gradle file of the project and the app module level, as below, and set dependency. 

> The Andriod SDK for iNavi Maps shall be deployed via Bintray, and it may change depending on policy after Beta period ends (to be posted before schedule). 

```gradle
/* Root Project build.gradle */

allprojects {
    repositories {
        google()
        ...
        // Repository for iNavi maps 
        maven {
            url 'https://dl.bintray.com/inavi-systems/maps/'
        }
    }
}
```

```gradle
/* App Module build.gradle */

dependencies {
    implementation 'com.inavi.mapsdk:inavi-maps-sdk:0.3.2'
}
```


### Setting Appkey 
Appkeys can be set in two methods as below: 

> Without appkey setup, authentication error may occur during map initialization. 

#### 1. Set on AndroidManifest.xml
Add `<meta-data>` to`AndroidManifest.xml` to set an appkey. 
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

#### 2. Call InaviMapSdk API 
To set appkey, call function of the [InaviMapSdk] singleton object dynamically at the time when application is created. 

```kotlin
// Kotlin
InaviMapSdk.getInstance(context).appKey = "YOUR_APP_KEY"
```

#### Authentication Failure 
If authentication fails for map initialization, the error code and message is delivered via callback registered within SDK.  
To receive callbacks on failure, set [AuthFailureCallback] for the [InaviMapSdk] singleton object as below:

```kotlin
// Kotlin
InaviMapSdk.getInstance(context).authFailureCallback =
    InaviMapSdk.AuthFailureCallback { errCode: Int, msg: String ->
        // Process failure in authentication
}
```
>Unless callback for authentication failure is set, error codes and messages are displayed on popups by default. 

#### Authentication Error Codes
| Code | Description |
| ------ | ------ |
| 300 | Appkey is invalid 
| 401 | Appkey is not set  |
| 503 | Server connection failed |
| 504 | Exceeded server connection time |
| 500 | Unknown error |
| Others | Server error (to be updated with definition) |

### Creating Maps
Describes how to display iNavi maps on the app. 

#### Display Maps
Add the  `<fragment>` tag in the activity layout file as below and define [InvMapFragment], and the map is displayed. 
```xml
<fragment
    android:id="@+id/map_fragment"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:name="com.inavi.mapsdk.maps.InvMapFragment" />
```

#### Access Map Objects
All map-related operations are made available by the [InaviMap] object. 
To access the [InaviMap] object, call the getMapAsync() function of the [InvMapFragment] object. 
When map is fully initialized, the [InaviMap] object is delivered via the onMapReady()  callback function. 

```kotlin
// Kotlin
val mapFragment = supportFragmentManager.findFragmentById(R.id.map_fragment) as InvMapFragment
mapFragment.getMapAsync(object : OnMapReadyCallback {
    override fun onMapReady(inaviMap: InaviMap) {
        // Access available to InaviMap 
    }
})
```

#### Set Map Events
Events can be set for interactions between map and user, such as clicks on map, double-clicks, or long-clicks. 
```kotlin
// Kotlin
inaviMap.setOnMapClickListener { pointF, latLng ->
    // pointF: Coordinates on screen of clicked point
    // latLng: Coordinates on map of clicked point 
    Toast.makeText(context, "Click on Map", Toast.LENGTH_SHORT).show()
}
```

#### Expose Markers
Create a marker object, and set `position` and `map` attributes, and the marker is displayed. 
```kotlin
// Kotlin
val marker = InvMarker().apply {
    position = LatLng(37.40219, 127.11077)
    title = "Title"
    map = inaviMap
}
```

#### Remove Markers
Set  `null` for the map attribute of the marker object, and the marker is removed. 
```kotlin
// Kotlin
marker.map = null
```

#### Move Cameras
Create the [CameraUpdate] object via factory method or [CameraUpdateBuilder], and deliver parameters to the moveCamera() function and call, then you can move the camera. 

Since callback is supported for animation and camera events, you can implement camera movement as much as you need. 
```kotlin
// Kotlin
val cameraUpdate = CameraUpdate.targetTo(LatLng(36.99473, 127.81832))
cameraUpdate.setAnimationType(CameraAnimationType.Fly, 3000)
inaviMap.moveCamera(cameraUpdate)
```


## Guide for Main iNavi Maps SDK
For more details on Maps SDK, see [API Center for iNavi Maps](http://imapsapi.inavi.com/).

[InaviMapSdk] : [http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InaviMapSdk.html](http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InaviMapSdk.html)
[InaviMap] : [http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InaviMap.html](http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InaviMap.html)
[InvMapView] : [http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InvMapView.html](http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InvMapView.html)
[InvMapFragment] : [http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InvMapFragment.html](http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InvMapFragment.html)
[AuthFailureCallback] : [http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InaviMapSdk.AuthFailureCallback.html](http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/InaviMapSdk.AuthFailureCallback.html)
[CameraUpdate] : [http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/CameraUpdate.html](http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/CameraUpdate.html)
[CameraUpdateBuilder] : [http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/CameraUpdateBuilder.html](http://imapsapi.inavi.com/Android/com/inavi/mapsdk/maps/CameraUpdateBuilder.html)

[NHN TOAST Console] : [https://console.toast.com/](https://console.toast.com/)
