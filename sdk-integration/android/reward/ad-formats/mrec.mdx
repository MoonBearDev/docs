---
sidebar_position: 2
---

# MREC 광고

## MREC 형태 소개

- 배너 형태 중 300x250 사이즈를 따로 MREC으로 구분하여 부릅니다.
- 전반적으로 배너와 동일한 특성을 가집니다.

---

## View 생성하기

1. `DaroMBannerView` 를 생성합니다.

   - XML 사용시

     ```kotlin
     <?xml version="1.0" encoding="utf-8"?>
     ...
       <droom.daro.m.bannerDaroMBannerView
         android:layout_width="match_parent"
         android:layout_height="wrap_content"/>

     ...
     ```

   - 코드 내부에서 생성 시

     ```kotlin
     val bannerView = DaroMBannerView(context)
     ```

2. 뷰에 필요한 설정들을 정의합니다.

   ```kotlin
   bannerView.apply{
   	autoDestroy = ...

   	setListener(object: DaroMAdView.DaroMAdViewListener{
   		...
   	})
   }
   ```

   1. 뷰를 선언하면 자체적으로 화면에 맞는 라이프사이클을 찾아 동작을 관리합니다. 따로 resume, pause, destroy를 호출하지 않아도 됩니다.
      - `autoDestroy` 값을 false(default: true)로 설정하는 경우, destroy를 직접 호출해주셔야 합니다.
   2. `setListener` 를 통해서 광고뷰에 리스너를 추가할 수 있습니다.

## 광고 그리기

`load()` 메서드를 호출합니다.

    ```kotlin
    bannerView.load(
        DaroMAdBannerUnit(
          unitId = ${unitId},
          placementName = ${placementName}, //로그 상 보여질 이름입니다. 공백을 보내도 무관합니다.
          bannerSize = DaroMBannerSize.MediumRectangle,
          refreshSeconds = 10,
          apsSlotUUID = ...
        )
    )
    ```

    💡 새로고침을 원하지 않을 경우 `0` 을 설정해주세요.
