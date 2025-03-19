---
sidebar_position: 3
---

import NativeAdExample from './img/darom-ios-native.jpeg';
import LineNativeBannerExample from './img/ios-line-native-template-example.png';

# 네이티브 광고

## 네이티브 형태 소개

- 광고 뷰를 미디에이션 SDK가 구현해주는 타 광고 형태와 달리 네이티브 광고 형태는 구성 요소들을 전달받아 앱에서 직접 광고 뷰를 구현합니다.
- UI/UX 기반으로 레이아웃을 직접 구현하므로써 위화감을 적게 만들 수 있다는 것이 가장 큰 특징입니다. 단, 유저가 광고가 아닌 컨텐츠로써 착각하는 경우를 방지하기 위해 광고 표시와 함께 최소한의 차별성은 부여해야합니다.

---

### 네이티브 광고 단위 설정

:::note
대시보드에서 발급받은 `ad unit ID`를 사용하여 광고 단위를 설정하세요.
:::

```swift showLineNumbers
static let middleSize = DaroMAdViewUnit(
    adUnitID: "...",
    name: "...", // Optional
    format: .native,
    // highlight-next-line
    refreshTimeInterval: 10
)
```

### 네이티브 광고 구현

`DaroMNativeAdContentView`을 상속하는 뷰를 구현 합니다. 아래는 샘플코드입니다.

<details>

<summary>DaroMNativeAdContentContainerView.swift</summary>

```swift showLineNumbers
public final class DaroMNativeAdContentContainerView: DaroMNativeAdContentView {

    // MARK: title

    public override var titleLabel: UILabel? {
        get { internalTitleLabel }
        set { super.titleLabel = newValue }
    }

    var internalTitleLabel: UILabel = {
        let label = UILabel()
        label.text = ""
        label.translatesAutoresizingMaskIntoConstraints = false
        label.font = .systemFont(ofSize: 14, weight: .bold)
        label.tag = 1001
        return label
    }()

    // MARK: - Advertiser

    public override var advertiserLabel: UILabel? {
        get { internalAdvertiserLabel }
        set { super.advertiserLabel = newValue }
    }

    var internalAdvertiserLabel: UILabel = {
        let label = UILabel()
        label.translatesAutoresizingMaskIntoConstraints = false
        label.font = .systemFont(ofSize: 10, weight: .medium)
        label.tag = 1002
        return label
    }()

    // MARK: - body

    public override var bodyLabel: UILabel? {
        get { internalBodyLabel }
        set { super.bodyLabel = newValue }
    }

    var internalBodyLabel: UILabel = {
        let label = UILabel()
        label.translatesAutoresizingMaskIntoConstraints = false
        label.textAlignment = .center
        label.font = .systemFont(ofSize: 12, weight: .medium)
        label.tag = 1003
        return label
    }()

    // MARK: icon

    public override var iconImageView: UIImageView? {
        get { internalIconImageView }
        set { super.iconImageView = newValue }
    }

    var internalIconImageView: UIImageView = {
        let imageView = UIImageView()
        imageView.translatesAutoresizingMaskIntoConstraints = false
        imageView.tag = 1004
        return imageView
    }()

    // MARK: - options content view

    public override var optionsContentView: UIView? {
        get { internalOptionsContentView }
        set { super.optionsContentView = newValue }
    }

    var internalOptionsContentView: UIView = {
        let view = UIView()
        view.tag = 1005
        view.translatesAutoresizingMaskIntoConstraints = false
        return view
    }()

    // MARK: - media content view

    public override var mediaContentView: UIView? {
        get { internalMediaContentView }
        set { super.mediaContentView = newValue }
    }

    var internalMediaContentView: UIView = {
        let view = UIView()
        view.tag = 1006
        view.alpha = 0.1
        view.translatesAutoresizingMaskIntoConstraints = false
        return view
    }()

    // MARK: - cta

    public override var callToActionButton: UIButton? {
        get { internalCallToActionButton }
        set { super.callToActionButton = newValue }
    }

    var internalCallToActionButton: UIButton = {
        let button = UIButton()
        button.translatesAutoresizingMaskIntoConstraints = false
        button.clipsToBounds = true
        button.titleLabel?.font = .systemFont(ofSize: 12, weight: .bold)
        button.setTitleColor(.label, for: .normal)
        button.backgroundColor = UIColor.systemGray3
        button.layer.cornerRadius = 4
        button.tag = 1007
        return button
    }()

    // MARK: - star rating content
    public override var starRatingContentView: UIView? {
        get { internalStarRatingContentView }
        set { super.starRatingContentView = newValue }
    }

    var internalStarRatingContentView: UIView = {
        let view = UIView()
        view.tag = 1008
        view.translatesAutoresizingMaskIntoConstraints = false
        return view
    }()

    // MARK: - initializers

    required init() {
        super.init()
        layout()

        let binder = DaroMNativeAdViewBinder.init { builder in
            builder.titleLabelTag = 1001
            builder.advertiserLabelTag = 1002
            builder.bodyLabelTag = 1003
            builder.iconImageViewTag = 1004
            builder.optionsContentViewTag = 1005
            builder.mediaContentViewTag = 1006
            builder.callToActionButtonTag = 1007
            builder.starRatingContentViewTag = 1008
        }

        self.bindViews(with: binder)
        translatesAutoresizingMaskIntoConstraints = false
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    private func layout() {
        internalMediaContentView.translatesAutoresizingMaskIntoConstraints = false
        internalIconImageView.translatesAutoresizingMaskIntoConstraints = false
        internalTitleLabel.translatesAutoresizingMaskIntoConstraints = false
        internalAdvertiserLabel.translatesAutoresizingMaskIntoConstraints = false
        internalBodyLabel.translatesAutoresizingMaskIntoConstraints = false
        internalCallToActionButton.translatesAutoresizingMaskIntoConstraints = false

        addSubview(internalMediaContentView)
        NSLayoutConstraint.activate([
            internalMediaContentView.topAnchor.constraint(equalTo: self.topAnchor),
            internalMediaContentView.bottomAnchor.constraint(equalTo: self.bottomAnchor),
            internalMediaContentView.leftAnchor.constraint(equalTo: self.leftAnchor),
            internalMediaContentView.rightAnchor.constraint(equalTo: self.rightAnchor),
        ])

        addSubview(internalIconImageView)
        NSLayoutConstraint.activate([
            internalIconImageView.topAnchor.constraint(equalTo: self.topAnchor),
            internalIconImageView.leftAnchor.constraint(equalTo: self.leftAnchor),
            internalIconImageView.widthAnchor.constraint(equalToConstant: 32),
            internalIconImageView.heightAnchor.constraint(equalToConstant: 32),
        ])

        addSubview(internalTitleLabel)
        NSLayoutConstraint.activate([
            internalTitleLabel.topAnchor.constraint(equalTo: self.topAnchor),
            internalTitleLabel.leftAnchor.constraint(equalTo: internalIconImageView.rightAnchor, constant: 12),
            internalTitleLabel.rightAnchor.constraint(equalTo: self.rightAnchor, constant: -12),
        ])

        addSubview(internalAdvertiserLabel)
        NSLayoutConstraint.activate([
            internalAdvertiserLabel.topAnchor.constraint(equalTo: internalTitleLabel.bottomAnchor),
            internalAdvertiserLabel.leftAnchor.constraint(equalTo: internalIconImageView.rightAnchor, constant: 12),
            internalAdvertiserLabel.rightAnchor.constraint(equalTo: self.rightAnchor, constant: -12),
        ])

        addSubview(internalBodyLabel)
        NSLayoutConstraint.activate([
            internalBodyLabel.topAnchor.constraint(equalTo: internalIconImageView.bottomAnchor, constant: 12),
            internalBodyLabel.leftAnchor.constraint(equalTo: self.leftAnchor, constant: 12),
            internalBodyLabel.rightAnchor.constraint(equalTo: self.rightAnchor, constant: -12),
        ])

        addSubview(internalCallToActionButton)
        NSLayoutConstraint.activate([
            internalCallToActionButton.topAnchor.constraint(greaterThanOrEqualTo: internalBodyLabel.bottomAnchor, constant: 10),
            internalCallToActionButton.leftAnchor.constraint(equalTo: self.leftAnchor, constant: 20),
            internalCallToActionButton.rightAnchor.constraint(equalTo: self.rightAnchor, constant: -20),
            internalCallToActionButton.bottomAnchor.constraint(equalTo: self.bottomAnchor),
            internalCallToActionButton.centerXAnchor.constraint(equalTo: self.centerXAnchor),
        ])
    }
}
```

</details>


#### 광고를 보여줄 화면에서 네이티브 광고 뷰를 선언합니다.


```swift
var nativeAdView = DaroMNativeAdView(
    nativeAdContentViewType: DaroMNativeAdContentContainerView.self,
    adUnit: .middleSize
)

...

// 광고 레이아웃 설정
// 아래는 샘플 코드 입니다
addSubview(nativeAdView)
NSLayoutConstraint.activate([
    nativeAdView.leftAnchor.constraint(equalTo: leftAnchor),
    nativeAdView.rightAnchor.constraint(equalTo: rightAnchor),
    nativeAdView.topAnchor.constraint(equalTo: topAnchor),
    nativeAdView.bottomAnchor.constraint(equalTo: bottomAnchor),
])

...
nativeAdView.delegate = self
nativeAdView.impressionDelegate = self
// highlight-next-line
nativeAdView.loadAd()

...

extension ExampleVC: DaroMAdImpressionDelegate {
    public func didRecordImpression(for ad: DaroMAd) { }
}

extension ExampleVC: DaroMNativeAdDelegate {
    public func didLoadNativeAd(_ ad: DaroMAd) { }
    public func didFailToLoadNativeAd(_ adUnitIdentifier: String, error: DaroMError) { }
    public func didClickNativeAd(_ ad: DaroMAd) {
    public func didExpireNativeAd(_ ad: DaroMAd) { }
}

```

### 네이티브 광고 라인 템플릿


#### 템플릿 뷰 선언

```swift
// 높이는 36 ~ 40 정도로 잡으시면 됩니다
let lineNativeBannerView = DaroMAdLineNativeBannerView(adUnit: .middleSize)

```

#### UITabBarController 하단 광고 예제 코드

<details>

<summary>RootViewController.swift</summary>

```swift
import DaroM

final class RootViewController: UIViewController {

    let tabBarViewController = TabBarViewController()
    let lineNativeBannerView = DaroMAdLineNativeBannerView(adUnit: .nativeMiddleSize)

    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = UIColor.secondarySystemBackground
        layout()
    }

    func layout() {
        addChild(tabBarViewController)
        tabBarViewController.willMove(toParent: self)

        tabBarViewController.view.translatesAutoresizingMaskIntoConstraints = false
        view.addSubview(tabBarViewController.view)

        NSLayoutConstraint.activate([
            tabBarViewController.view.topAnchor.constraint(equalTo: view.topAnchor),
            tabBarViewController.view.leftAnchor.constraint(equalTo: view.leftAnchor),
            tabBarViewController.view.rightAnchor.constraint(equalTo: view.rightAnchor),
        ])
        tabBarViewController.didMove(toParent: self)

        #if DEBUG
        lineNativeBannerView.layer.borderColor = UIColor.yellow.cgColor
        lineNativeBannerView.layer.borderWidth = 1.0
        #endif

        lineNativeBannerView.translatesAutoresizingMaskIntoConstraints = false
        view.addSubview(lineNativeBannerView)
        NSLayoutConstraint.activate([
            lineNativeBannerView.topAnchor.constraint(equalTo: tabBarViewController.view.bottomAnchor),
            lineNativeBannerView.leftAnchor.constraint(equalTo: view.leftAnchor),
            lineNativeBannerView.rightAnchor.constraint(equalTo: view.rightAnchor),
            lineNativeBannerView.bottomAnchor.constraint(equalTo: view.bottomAnchor, constant: -10),
            lineNativeBannerView.heightAnchor.constraint(equalToConstant: 36),
        ])
    }
}
```

</details>



<details>
<summary>TabBarViewController.swift</summary>


```swift
final class TabBarViewController: UITabBarController {

    private let timerListVC: UIViewController = {
        ...
        nav.tabBarItem = UITabBarItem(title: I18N.timers, image: UIImage(systemName: "rectangle.grid.1x2.fill"), tag: 0)
        return nav
    }()

    private let soundsGalleryVC: UINavigationController = {
        ...
        nav.tabBarItem = UITabBarItem(title: I18N.relax, image: UIImage(systemName: "powersleep"), tag: 1)
        nav.navigationBar.prefersLargeTitles = true
        return nav
    }()

    private let settingsVC: UINavigationController = {
        ...
        nav.tabBarItem = UITabBarItem(title: I18N.settings, image: UIImage(systemName: "gearshape.fill"), tag: 3)
        nav.navigationBar.prefersLargeTitles = true
        return nav
    }()

    override func viewDidLoad() {
        super.viewDidLoad()
        viewControllers = [timerListVC, soundsGalleryVC, settingsVC]
    }
}
```

</details>

#### 사용 화면

<img src={LineNativeBannerExample} alt="line native template example" style={{width: "50%"}}/>
