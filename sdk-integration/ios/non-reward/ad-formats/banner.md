---
sidebar_position: 1
---

# 배너 광고

## 배너 형태 소개

- 앱 레이아웃의 일부를 차지하는 직사각형 광고 형태로 보편적으로 사용됩니다.
- 다양한 사이즈를 지정할 수 있지만 그 중에서도 대부분의 광고 네트워크들이 지원하는 형태인 320x50 사이즈를 가장 많이 사용합니다.

---

## 광고 단위 설정

대시보드에서 발급받은 `ad unit ID`를 사용하여 광고 단위를 설정하세요.

```swift
extension DaroAdBannerViewUnit {
    static let banner = DaroAdBannerViewUnit(
        id: "...",
        name: "banner",
        size: .banner,
        refreshTimeInterval: 10
    )
}
```

### 배너 사이즈 타입

- `DaroAdBannerViewUnit` 배너 유닛을 정의할 때 파라미터로 Banner Size를 정할 수 있습니다.
- 배너사이즈 타입은 아래와 같습니다. 기본값은 `.banner (320 x 50)` 입니다.

| Type | Size | name |
|------|------|------|
| banner | CGSize(width: 320, height: 50) | Banner (Default) |
| largeBanner | CGSize(width: 320, height: 100) | Large Banner |
| iabMediumRectangle | CGSize(width: 300, height: 250) | IAB medium rectangle |
| iabFullSizeBanner | CGSize(width: 468, height: 60) | IAB full-size banner |
| iabLeaderBoard | CGSize(width: 728, height: 90) | IAB leaderboard |

## 배너 광고 구현

### 기본 구현

배너 광고를 로드하고 표시하기 위한 코드 예제입니다.

```swift
// 뷰 선언
var bannerView = DaroAdBannerView(adUnit: .banner)

// 로드 호출
bannerView.loadAd()

// 필요한 경우 delegate 사용
bannerView.delegate = self
extension ExampleViewController: DaroAdBannerViewDelegate { }
```

### DaroAdBannerView 사용 샘플 코드

<details>

<summary>`DaroAdBannerView`를 사용한 전체 구현 예시입니다.</summary>

```swift
import Daro
import UIKit

extension DaroAdBannerViewUnit {
    static let exampleBannerUnit = DaroAdBannerViewUnit(
        id: "...",
        name: "...",
        size: .banner,
        refreshTimeInterval: 10
    )
}

final class DaroExampleViewController: UIViewController {
    var bannerView = DaroAdBannerView(adUnit: .exampleBannerUnit)

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
        
        bannerView.loadAd()
    }

    @available(*, unavailable)
    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
}

```

</details>