## Application Service > Maps > iOS 지도 SDK 가이드
iOS 플랫폼에서 아이나비 지도를 사용하기 위한 프로젝트 기본 설정 방법을 설명합니다.

### 사전 준비
- 아이나비 지도를 사용하기 위해서는 인증을 위한 **Appkey**가 필요합니다.

#### 서비스 활성화
- **[NHN TOAST Console]** 에서 서비스 선택 후 Application Service > Maps를 클릭합니다

#### Appkey 확인
- **Appkey**는 **TOAST Console** 상단 **URL & Appkey** 메뉴에서 확인할 수 있습니다.


### Project 환경 구성
다음과 같이 Podfile을 생성하여 아이나비 지도 SDK에 대한 Pod 의존성을 설정합니다.

> `아이나비 지도 iOS SDK는 CocoaPods를 통해 배포되며, Beta 기간 종료 후에는 정책에 맞춰 변경될 수 있습니다. (사전 공지 예정)`

```ruby
# Podfile
target 'iNaviMapsDemoiOS' do
  use_frameworks!
  ...
  pod 'inavi-maps-sdk'
  ...
end
```

의존성 설정 후 Terminal에서 프로젝트 path로 이동한 다음, 아래 명령어를 실행하여 아이나비 지도 SDK를 설치합니다.
```
pod install --repo-update
```

### Appkey 설정
발급받은 Appkey를 설정할 수 있도록 아래의 두 가지 방법을 제공합니다. 

> `Appkey가 설정되지 않으면 지도 초기화 단계에서 인증 오류가 발생합니다.`

#### 1. 프로젝트 info.plist에서 설정
`info.plist`파일 내부에 Appkey를 설정할 수 있습니다.
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

#### 2. INVMapSdk API 호출로 설정
Application 생성 시점에 동적으로 [INVMapSdk] 싱글턴 객체의 함수를 호출하여 Appkey를 설정할 수 있습니다.

```swift
// Swift
INVMapSdk.sharedInstance().appKey = "YOUR_APP_KEY"
```

#### 인증 실패
지도 초기화 단계에 인증이 실패하면 SDK 내부에서 등록된 Callback으로 에러 코드와 메시지를 전달합니다.\
실패에 대한 Callback을 받으려면 [INVMapSdk] 싱글턴 객체에 [INVMapSdkDelegate]을 아래와 같이 설정해야 합니다.
```swift
// Swift
INVMapSdk.sharedInstance().delegate = self

func authFailure(_ errorCode: Int, message: String) {
    // 인증 실패 처리
}

```
인증 실패 Callback을 별도로 설정하지 않으면 기본적으로 에러 코드와 메시지가 팝업 형태로 표출됩니다.

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
UIViewController에서 직접 [InaviMapView]를 생성하고 추가하는 예제입니다.
```swift
// Swift
override func viewDidLoad() {
    super.viewDidLoad()

    let mapView = InaviMapView(frame: view.bounds)
    view.addSubview(mapView)
}
```
Interface Builder를 사용하여 지도를 추가하려면 XIB나 Storyboard에 UIView를 추가한 다음\
Identity Inspector패널의 Custom Class 항목을 [InaviMapView]로 설정하면 됩니다.

#### 지도 이벤트 설정
[INVMapViewDelegate]를 구현하고 [InaviMapView]의 `delegate` 속성을 설정하면 지도 클릭, 더블 클릭 등 지도와 사용자간 상호작용에 대한 이벤트를 설정할 수 있습니다.
```swift
// Swift
override func viewDidLoad() {
    super.viewDidLoad()
    ...
    inaviMapView.delegate = self
}

func didTapMapView(_ point: CGPoint, latLng latlng: INVLatLng) {
    // point : 클릭한 지점의 화면상 좌표
    // latlng : 클릭한 지점의 지도상 좌표
}
```

#### 마커 표출
마커 객체를 생성하고 `position` 속성과 `map` 속성을 설정하면 마커가 표출됩니다.
```swift
// Swift
let marker = INVMarker(position: INVLatLng(lat: 37.40219, lng : 127.11077))
marker.title = "타이틀"
marker.mapView = mapView
```

#### 마커 제거
마커 객체의 map 속성을 `null`로 설정하시면 마커가 제거됩니다.
```swift
// Swift
marker.mapView = nil
```

#### 카메라 이동
[INVCameraUpdate]의 팩토리 메서드 또는 [INVCameraUpdateParams]를 통해 [INVCameraUpdate] 객체를 생성한 다음\
[moveCamera()] 함수에 파라미터를 전달하여 호출하면 카메라가 이동됩니다.

애니메이션과 카메라 이벤트에 대한 콜백을 지원하므로, 카메라 이동을 원하는 대로 구현할 수 있습니다.
```swift
// Swift
let camUpdate = INVCameraUpdate.init(scrollTo: INVLatLng(lat: 37.40219, lng : 127.11077))
camUpdate.animation = .fly
camUpdate.animationDuration = 2
mapView.moveCamera(camUpdate)
```

## 주요 Maps SDK 안내
추가적인 Maps SDK 사용법은 [iNavi Maps API 센터](http://imapsapi.inavi.com/)를 참고하시기 바랍니다.

[INVMapSdk] : [http://imapsapi.inavi.com/iOS/Classes/INVMapSdk.html](http://imapsapi.inavi.com/iOS/Classes/INVMapSdk.html)
[INVMapSdkDelegate] : [http://imapsapi.inavi.com/iOS/Protocols/INVMapSdkDelegate.html](http://imapsapi.inavi.com/iOS/Protocols/INVMapSdkDelegate.html)

[InaviMapView] : [http://imapsapi.inavi.com/iOS/Classes/InaviMapView.html](http://imapsapi.inavi.com/iOS/Classes/InaviMapView.html)

[INVMapViewDelegate] : [http://imapsapi.inavi.com/iOS/Protocols/INVMapViewDelegate.html](http://imapsapi.inavi.com/iOS/Protocols/INVMapViewDelegate.html)

[INVCameraUpdate] : [http://imapsapi.inavi.com/iOS/Classes/INVCameraUpdate.html](http://imapsapi.inavi.com/iOS/Classes/INVCameraUpdate.html)
[INVCameraUpdateParams] : [http://imapsapi.inavi.com/iOS/Classes/INVCameraUpdateParams.html](http://imapsapi.inavi.com/iOS/Classes/INVCameraUpdateParams.html)

[moveCamera()] : [http://imapsapi.inavi.com/iOS/Classes/InaviMapView.html#/c:objc(cs)InaviMapView(im)moveCamera:](http://imapsapi.inavi.com/iOS/Classes/InaviMapView.html#/c:objc(cs)InaviMapView(im)moveCamera:)

[NHN TOAST Console] : [https://console.toast.com/](https://console.toast.com/)
