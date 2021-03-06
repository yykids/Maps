﻿## Application Service > Maps > iOSマップSDKガイド
iOSプラットフォームでinaviマップを使用するためのプロジェクト基本設定方法を説明します。

### 事前準備
- inaviマップを使用するには認証用の**Appkey**が必要です。

#### サービス有効化
- **[NHN TOAST Console]**でサービスを選択し、Application Service > Mapsをクリックします。

#### Appkey確認
- **Appkey**は、**TOAST Console**上部の**URL & Appkey**メニューで確認できます。


### Project環境構成
아이나비 지도 SDK를 사용하기 위해서는 다음과 같은 순서로 프로젝트의 환경을 구성해주어야 합니다.

#### Git LFS 설치
SDK 용량이 크기 때문에 Pod 의존성 설치 전 [Git Large File Storage(LFS)](https://git-lfs.github.com/) 설치가 필요합니다.
> `git-lfs가 설치되어 있지 않으면 SDK 의존성 설치가 정상적으로 진행되지 않아 빌드 시 오류가 발생합니다.`

```
brew install git-lfs
git lfs install
```

#### Podfile 구성
次のようにPodfileを作成してinaviマップSDKに対するPod依存性を設定します。
> inaviマップiOS SDKはCocoaPodsを通して配布され、Beta期間終了後はポリシーに合わせて変更される場合があります。(事前告知予定)

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
依存性設定を行った後、Terminalでプロジェクトpathに移動し、下記のコマンドを実行してinaviマップSDKをインストールします。
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

### Appkey設定
発行したAppkeyを設定する方法は下記のとおりです。

> Appkeyが未設定の場合、マップ初期化段階で認証エラーが発生します。

#### 1. プロジェクトinfo.plistで設定
`info.plist`ファイル内部にAppkeyを設定できます。
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

#### 2. INVMapSdk APIを呼び出して設定
Application作成時点で動的に[INVMapSdk]シングルトンオブジェクトの関数を呼び出してAppkeyを設定できます。

```swift
// Swift
INVMapSdk.sharedInstance().appKey = "YOUR_APP_KEY"
```

#### 認証失敗
マップ初期化段階で認証に失敗すると、SDK内部に登録されたCallbackにエラーコードとメッセージを伝達します。
失敗のCallbackを受け取るには、[INVMapSdk]シングルトンオブジェクトに[INVMapSdkDelegate]を下記のように設定する必要があります。
```swift
// Swift
INVMapSdk.sharedInstance().delegate = self

func authFailure(_ errorCode: Int, message: String) {
    // 認証失敗処理
}

```
認証失敗Callbackを別途設定していない場合、エラーコードとメッセージがポップアップ表示されます。

#### 認証エラーコード
| Code | Description |
| ------ | ------ |
| 300 | Appkeyが無効
| 401 | Appkeyが未設定 |
| 503 | サーバー接続失敗 |
| 504 | サーバー接続時間超過 |
| 500 | 不明なエラー |
| その他 | サーバーエラー(今後定義したらアップデート) |


### マップを作成する
アプリ画面にinaviマップを表示する方法を説明します。

#### マップ表示
UIViewControllerで直接[InaviMapView]を作成して追加する例です。
```swift
// Swift
import iNaviMaps

override func viewDidLoad() {
    super.viewDidLoad()

    let mapView = InaviMapView(frame: view.bounds)
    view.addSubview(mapView)
}
```
Interface Builderを使用してマップを追加するには、XIBまたはStoryboardにUIViewを追加した後
Identity InspectorパネルのCustom Class項目を[InaviMapView]に設定してください。

#### マップイベント設定
[INVMapViewDelegate]を実装し、[InaviMapView]の`delegate`プロパティを設定すると、マップクリック、ダブルクリックなどのマップとユーザー間のインタラクションに対するイベントを設定できます。
```swift
// Swift
override func viewDidLoad() {
    super.viewDidLoad()
    ...
    mapView.delegate = self
}

func didTapMapView(_ point: CGPoint, latLng latlng: INVLatLng) {
    // point :クリックした地点の画面上の座標
    // latLng ：クリックした地点のマップ上の座標
}
```

#### マーカー表示
マーカーオブジェクトを作成し、`position`プロパティと`map`プロパティを設定すると、マーカーが表示されます。
```swift
// Swift
let marker = INVMarker(position: INVLatLng(lat: 37.40219, lng : 127.11077))
marker.title = "タイトル"
marker.mapView = mapView
```

#### マーカー削除
マーカーオブジェクトのmapプロパティを`nil`に設定すると、マーカーが削除されます。
```swift
// Swift
marker.mapView = nil
```

#### カメラ移動
[INVCameraUpdate]のFactory Methodまたは[INVCameraUpdateParams]を通して[INVCameraUpdate]オブジェクトを作成した後
[moveCamera()]関数にパラメータを伝達して呼び出すと、カメラが移動します。

アニメーションとカメライベントに対するコールバックをサポートするため、カメラ移動を自由に実装できます。
```swift
// Swift
let camUpdate = INVCameraUpdate.init(targetTo: INVLatLng(lat: 36.99473, lng : 127.81832))
camUpdate.animation = .fly
camUpdate.animationDuration = 3
mapView.moveCamera(camUpdate)
```


### 主要Maps SDK案内
Maps SDKの使用方法は[iNavi Maps APIセンター](http://imapsapi.inavi.com/)を参照してください。

[INVMapSdk] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVMapSdk.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVMapSdk.html)
[INVMapSdkDelegate] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Protocols/INVMapSdkDelegate.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Protocols/INVMapSdkDelegate.html)

[InaviMapView] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/InaviMapView.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/InaviMapView.html)

[INVMapViewDelegate] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Protocols/INVMapViewDelegate.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Protocols/INVMapViewDelegate.html)

[INVCameraUpdate] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVCameraUpdate.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVCameraUpdate.html)
[INVCameraUpdateParams] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVCameraUpdateParams.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVCameraUpdateParams.html)

[moveCamera()] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/InaviMapView.html#/c:objc(cs)InaviMapView(im)moveCamera:](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/InaviMapView.html#/c:objc(cs)InaviMapView(im)moveCamera:)

[NHN TOAST Console] : [https://console.toast.com/](https://console.toast.com/)

