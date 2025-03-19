---
sidebar_position: 3
---

import LineNativeBannerExample from './img/ios-line-native-template-example.png';

# 네이티브 광고

## 네이티브 형태 소개

- 광고 뷰를 미디에이션 SDK가 구현해주는 타 광고 형태와 달리 네이티브 광고 형태는 구성 요소들을 전달받아 앱에서 직접 광고 뷰를 구현합니다.
- UI/UX 기반으로 레이아웃을 직접 구현하므로써 위화감을 적게 만들 수 있다는 것이 가장 큰 특징입니다. 단, 유저가 광고가 아닌 컨텐츠로써 착각하는 경우를 방지하기 위해 광고 표시와 함께 최소한의 차별성은 부여해야합니다.

---

## 네이티브 뷰 컴포넌트 생성하기

<details>

 <summary>`NativeAdView` 구현 예시입니다.</summary>

```javascript

import { theme } from '@/theme';
import { useRef, useState } from 'react';
import { StyleSheet, View } from 'react-native';
import type { AdInfo, AdLoadFailedInfo, AdRevenueInfo, NativeAdViewHandler } from 'react-native-daro-m';
import { AdvertiserView, BodyView, CallToActionView, IconView, MediaView, NativeAdView, OptionsView, StarRatingView, TitleView } from 'react-native-daro-m';
import { BlurView } from 'expo-blur';

type Props = {
  adUnitId: string;
  isInitialized: boolean;
  log: (str: string) => void;
};

export const NativeAdViewMedium = ({ adUnitId, isInitialized, log }: Props) => {

  const DEFAULT_ASPECT_RATIO = 16 / 9;
  const [aspectRatio, setAspectRatio] = useState(DEFAULT_ASPECT_RATIO);
  const [isNativeAdLoading, setIsNativeAdLoading] = useState(false);

  // Ref for NativeAdView
  const nativeAdViewRef = useRef<NativeAdViewHandler>(null);

  return (
    <View style={{ alignSelf: 'flex-end' }}>
      <BlurView intensity={50} tint="light" style={styles.blurContainer}>
        <NativeAdView
          adUnitId={adUnitId}
          refreshInterval={7}
          ref={nativeAdViewRef}
          style={styles.nativeAd}
          onAdLoaded={(adInfo: AdInfo) => {
            if (adInfo?.nativeAd?.mediaContentAspectRatio) {
              setAspectRatio(adInfo?.nativeAd?.mediaContentAspectRatio);
            }
            log('Native ad loaded from ' + adInfo.networkName);
            setIsNativeAdLoading(false);
          }}
          onAdLoadFailed={(errorInfo: AdLoadFailedInfo) => {
            log('Native ad failed to load with error code ' + errorInfo.code + ' and message: ' + errorInfo.message);
            setIsNativeAdLoading(false);
          }}
          onAdClicked={(adInfo: AdInfo) => {
            log('Native ad clicked on ' + adInfo.adUnitId);
          }}
          onAdImpressionRecorded={(adInfo: AdRevenueInfo) => {
            log('Native ad impression recorded: ' + adInfo.revenue);
          }}
        >
          <View style={styles.assetContainer}>
            <View style={styles.contentContainer}>
              <View style={styles.assetUpperContainer}>
                <IconView style={styles.icon} />
                <View style={styles.assetTitleContainer}>
                  <TitleView numberOfLines={1} style={styles.title} />
                  <AdvertiserView numberOfLines={1} style={styles.advertiser} />
                  <StarRatingView style={styles.starRatingView} />
                </View>
                <OptionsView style={styles.optionsView} />
              </View>
              <BodyView numberOfLines={2} style={styles.body} />
              <MediaView style={styles.mediaView} />
              <CallToActionView style={styles.callToAction} />
            </View>
          </View>
        </NativeAdView>
      </BlurView>
    </View>
  );
};

const styles = StyleSheet.create({
  nativeAd: {
    margin: 10,
    zIndex: 1,
    borderRadius: 8
  },
  icon: {
    width: 48,
    height: 48,
  },
  title: {
    width: 260,
    fontSize: 16,
    textAlign: 'left',
    fontWeight: 'bold',
    color: theme.colorWhite,
  },
  advertiser: {
    marginTop: 4,
    fontSize: 12,
    textAlign: 'left',
    color: theme.colorWhite,
  },
  starRatingView: {
    height: 20,
    color: '#ffe234',
  },
  optionsView: {
    width: 20,
    height: 20,
  },
  body: {
    marginBottom: 10,
    fontSize: 14,
    textAlign: 'center',
    textAlignVertical: 'center',
    color: theme.colorWhite,
  },
  mediaView: {
    height: 200,
    width: '100%',
    zIndex: 1,
  },
  callToAction: {
    margin: 10,
    padding: 10,
    borderRadius: 5,
    fontSize: 18,
    textAlign: 'center',
    fontWeight: 'bold',
    textTransform: 'uppercase',
    color: theme.colorWhite,
    backgroundColor: '#2d545e',
  },
  assetContainer: {
    position: 'relative',
    flexDirection: 'column',
  },
  contentContainer: {
    flexDirection: 'column',
    zIndex: 1,
  },
  assetUpperContainer: {
    flexDirection: 'row',
    justifyContent: 'space-between',
  },
  assetTitleContainer: {
    marginLeft: 10,
    marginBottom: 10,
    flexDirection: 'column',
    flexGrow: 1,
  },
  blurContainer: {
    overflow: 'hidden',
    width: '100%',
    borderRadius: 8,
    margin: 10,
  },
});

```
</details>