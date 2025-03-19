---
sidebar_position: 1
---

# 배너 광고

## 배너 형태 소개

- 앱 레이아웃의 일부를 차지하는 직사각형 광고 형태로 보편적으로 사용됩니다.
- 다양한 사이즈를 지정할 수 있지만 그 중에서도 대부분의 광고 네트워크들이 지원하는 형태인 320x50 사이즈를 가장 많이 사용합니다.

---

## View 생성하기

1. `DaroAdBannerView` 를 생성합니다.

   - XML 사용시

     ```kotlin
     <?xml version="1.0" encoding="utf-8"?>
     ...
       <droom.daro.lib.banner.DaroAdBannerView
         android:layout_width="match_parent"
         android:layout_height="wrap_content"/>

     ...
     ```

   - 코드 내부에서 생성 시

     ```kotlin
     val bannerView = DaroAdBannerView(context)
     ```

2. 뷰에 필요한 설정들을 정의합니다.

   ```kotlin
   bannerView.apply{
   	autoDestroy = ...

   	setListener(object: DaroAdView.DaroAdViewListener{
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
        DaroAdBannerUnit(
          unitId = ${unitId},
          placementName = ${placementName}, //로그 상 보여질 이름입니다. 공백을 보내도 무관합니다.
          bannerSize = DaroAdBannerSize.Banner,
          refreshSeconds = 10,
        )
    )
    ```

💡 새로고침을 원하지 않을 경우 `refreshSeconds`를 `0` 으로 설정해주세요.
