---
sidebar_position: 1
---

# 배너 광고

## 배너 형태 소개

import bannerAdExample from './img/darom-ios-banner-ad-example.png';

<img src={bannerAdExample} alt="banner ad example" style={{width: "20%"}}/>

- 앱 레이아웃의 일부를 차지하는 직사각형 광고 형태로 보편적으로 사용됩니다.
- 다양한 사이즈를 지정할 수 있지만 그 중에서도 대부분의 광고 네트워크들이 지원하는 형태인 320x50 사이즈를 가장 많이 사용합니다.

---

## 광고 단위 설정

대시보드에서 발급받은 `ad unit ID`를 사용하여 광고 단위를 설정하세요.

```swift
extension DaroMAdUnit {

    static let timerBanner = DaroMAdUnit(
        adUnitID: "...",
        name: "...",
        format: .banner,
        refreshTimeInterval: 10
    )
}
```

*APS 광고 네트워크를 사용하지 않으시는 경우, 배너 타입에서 SlotUUID 값은 제거해주셔도 무방합니다.


## 배너 광고 구현

### 기본 구현

배너 광고를 로드하고 표시하기 위한 코드 예제입니다.

```swift
// 뷰 선언
// highlight-next-line
var bannerView = DaroMAdView(DaroMAdUnit.timerBanner)

// 로드 호출
// highlight-next-line
bannerView.loadAd()

// (Optional) 필요한 경우 delegate 사용
bannerView.delegate = self
bannerView.impressionDelegate = self
bannerView.clickDelegate = self

extension ExampleViewController: DaroMAdViewDelegate {
    func didExpand(_ ad: DaroM.DaroMAd) { }
    func didCollapse(_ ad: DaroM.DaroMAd) { }
    func didFailToDisplay(ad: DaroM.DaroMAd, with error: DaroM.DaroMError) { }
    func didStartAdRequest(for adUnitIdentifier: String) { }
    func didLoad(_ ad: DaroM.DaroMAd) { }
    func didFailToLoadAd(for adUnitIdentifier: String, with error: DaroM.DaroMError) { }
}

```

### DaroMAdView 사용 샘플 코드

<details>

 <summary>`DaroMAdView`를 사용한 전체 구현 예시입니다.</summary>

```swift
import DaroM
import UIKit

extension DaroMAdViewUnit {
    static let timerBanner = DaroMAdViewUnit(
        adUnitID: "...",
        format: .banner,
        refreshTimeInterval: 7
    )
}

final class DaroExampleViewController: UIViewController {
    var bannerView = DaroMAdView(DaroMAdViewUnit.timerBanner)

    init() {
      super.init(nibName: nil, bundle: nil) 
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = .systemBackground
        bannerView.translatesAutoresizingMaskIntoConstraints = false
        view.addSubview(bannerView)
        NSLayoutConstraint.activate([
            bannerView.centerXAnchor.constraint(equalTo: view.centerXAnchor),
            bannerView.widthAnchor.constraint(equalToConstant: 320),
            bannerView.heightAnchor.constraint(equalToConstant: 50),
            bannerView.bottomAnchor.constraint(equalTo: view.safeAreaLayoutGuide.bottomAnchor),
        ])
        // highlight-next-line
        bannerView.loadAd()
    }

    @available(*, unavailable)
    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
}
```

</details>