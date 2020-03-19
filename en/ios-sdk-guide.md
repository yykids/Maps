## Application Service > Maps > SDK User Guide for iOS Maps
Describes the basic project configuration method to enable iNavi maps on iOS. 

### Prerequisites 
- To enable iNavi maps, **Appkey** is required for authentication. 

#### Enable Service 
- Go to **[NHN TOAST Console]**, select a service and click Application Service > Maps. 

#### Check Appkey 
- To check your appkey, go to **URL & Appkey** on top of the **TOAST Console**. 


### Project Configuration 
아이나비 지도 SDK를 사용하기 위해서는 다음과 같은 순서로 프로젝트의 환경을 구성해주어야 합니다.

#### Git LFS 설치
SDK 용량이 크기 때문에 Pod 의존성 설치 전 [Git Large File Storage(LFS)](https://git-lfs.github.com/) 설치가 필요합니다.
> `git-lfs가 설치되어 있지 않으면 SDK 의존성 설치가 정상적으로 진행되지 않아 빌드 시 오류가 발생합니다.`

```
brew install git-lfs
git lfs install
```

#### Podfile 구성
Create a podfile like below and set pod dependency for iNavi maps SDK.  
> The iOS SDK for iNavi Maps shall be deployed via CocoaPods, and it may change depending on policy after Beta period ends (to be posted before schedule). 

```ruby
# Podfile
target 'iNaviMapsDemoiOS' do
  use_frameworks!
  ...
  pod 'inavi-maps-sdk'
  ...
end
```

#### SDK 설치
After dependency setting, go to protect path at the terminal, execute the command as below and install iNavi maps SDK. 
> `SDK 의존성 설치가 완료되었을 때 프레임워크 용량은 약 150MB 입니다.`
```
pod install --repo-update
```

#### CocoaPods 캐시 삭제
간혹 이전에 다운로드 받은 SDK 의존성의 캐시가 남아있어 빌드에 오류가 발생할 수 있습니다.\
아래 명령어를 통해 아이나비 지도 SDK의 CocoaPods 캐시를 삭제할 수 있습니다.
```
pod cache clean inavi-maps-sdk
pod update inavi-maps-sdk
```

### Setting Appkey 
Appkeys can be set in two methods as below: 

> Without appkey setup, authentication error may occur during map initialization. 

#### 1. Set on Project info.plist  
An appkey can be set within the `info.plist` file. 
```xml
<!-- info.plist -->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	...
	<key>iNaviAppKey</key>
	<string>YOUR_APP_KEY</string>
	...
</dict>
</plist>
```

#### 2. Call INVMapSdk API 
To set appkey, call function of the [INVMapSdk] singleton object dynamically at the time when application is created.  

```swift
// Swift
INVMapSdk.sharedInstance().appKey = "YOUR_APP_KEY"
```

#### Authentication Failure 
If authentication fails for map initialization, the error code and message is delivered via callback registered within SDK. To receive callbacks on failure, set [INVMapSdkDelegate] for the [INVMapSdk] singleton object as below: 
```swift
// Swift
INVMapSdk.sharedInstance().delegate = self

func authFailure(_ errorCode: Int, message: String) {
    // Process failure in authentication 
}

```
Unless callback for authentication failure is set, error codes and messages are displayed on popups by default. 

#### Authentication Error Codes 
| Code | Description |
| ------ | ------ |
| 300 | Appkey is invalid |
| 401 | Appkey is not set |
| 503 | Server connection failed |
| 504 | Exceeded server connection time  |
| 500 | Unknown error |
| Others | Server error  (to be updated with definition) |


### Creating Maps 
Describes how to display iNavi on the app. 

#### Display Maps
Create and add [InaviMapView] on the UIViewController, like the example shows. 
```swift
// Swift
import iNaviMaps

override func viewDidLoad() {
    super.viewDidLoad()

    let mapView = InaviMapView(frame: view.bounds)
    view.addSubview(mapView)
}
```
To add maps by using Interface Builder, add UIview to XIB or Storyboard, and set [InaviMapView] for Custom Class of the Identity Inspector panel. 

#### Set Map Events
With [INVMapViewDelegate] implemented and  `delegate` is set for [InaviMapView], events can be set for interactions between map and user, such as clicks on the map, double-clicks, or long-clicks. 
```swift
// Swift
override func viewDidLoad() {
    super.viewDidLoad()
    ...
    mapView.delegate = self
}

func didTapMapView(_ point: CGPoint, latLng latlng: INVLatLng) {
    // point: Coordinates on screen of clicked point
    // latlng: Coordinates on map of clicked point 
}
```

#### Expose Markers
Create a marker object, and set `position` and `map` attributes, and the marker is displayed. 
```swift
// Swift
let marker = INVMarker(position: INVLatLng(lat: 37.40219, lng : 127.11077))
marker.title = "Title"
marker.mapView = mapView
```

#### Remove Markers 
Set `nil` for the map attribute of the marker object, and the marker is removed. 
```swift
// Swift
marker.mapView = nil
```

#### Move Cameras 
Create the [INVCameraUpdate] object via factory method or [INVCameraUpdateParams], and deliver parameters to the [moveCamera()] function and call, then you can move the camera.  

Since callback is supported for animation and camera events, you can implement camera movement as much as you need. 
```swift
// Swift
let camUpdate = INVCameraUpdate.init(targetTo: INVLatLng(lat: 36.99473, lng : 127.81832))
camUpdate.animation = .fly
camUpdate.animationDuration = 3
mapView.moveCamera(camUpdate)
```


### Guide for Main Maps SDK 
For more details on Maps SDK, see [API Center for iNavi Maps](http://imapsapi.inavi.com/).

[INVMapSdk] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVMapSdk.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVMapSdk.html)
[INVMapSdkDelegate] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Protocols/INVMapSdkDelegate.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Protocols/INVMapSdkDelegate.html)

[InaviMapView] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/InaviMapView.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/InaviMapView.html)

[INVMapViewDelegate] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Protocols/INVMapViewDelegate.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Protocols/INVMapViewDelegate.html)

[INVCameraUpdate] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVCameraUpdate.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVCameraUpdate.html)
[INVCameraUpdateParams] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVCameraUpdateParams.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVCameraUpdateParams.html)

[moveCamera()] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/InaviMapView.html#/c:objc(cs)InaviMapView(im)moveCamera:](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/InaviMapView.html#/c:objc(cs)InaviMapView(im)moveCamera:)

[NHN TOAST Console] : [https://console.toast.com/](https://console.toast.com/)
