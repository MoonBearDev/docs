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

## BANNER 컴포넌트 생성하기

- 컴포넌트 생성 시 광고 단위 ID 를 전달해야합니다. style 사이즈는 320x50 으로 설정해 주세요.

```javascript
import { AdFormat, AdBannerView } from "react-native-daro-m";
import { Platform } from "react-native";

const BANNER_AD_UNIT_ID = Platform.select({
    ios: ${iOS unit Id},
    android: ${Android unit id},
    default: '',
});

<AdBannerView
  refreshInterval={10}
  style={styles.bannerView}
  adFormat={AdFormat.BANNER}
  adUnitId={BANNER_AD_UNIT_ID}
/>
```
