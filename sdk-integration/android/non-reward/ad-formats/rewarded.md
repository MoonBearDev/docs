---
sidebar-position: 5
---

# 리워드 비디오 광고

## 리워드 비디오 형태 소개

- 광고 시청을 대가로 인앱 가치를 지닌 보상(재화, 기능, 컨텐츠 등)을 제공하는 형태의 광고입니다.
- 보상을 대가로 시청하므로 동영상 광고의 스킵이 불가능하며 일반적인 길이는 30초입니다.

---

## Loader 생성하기

```kotlin
val rewardedLoader = DaroRewardedAdLoader(
    adRewardedUnit = DaroAdRewardedUnit(
      unitId = ${unitId},
      placementName = ${placementName}, //로그 상 보여질 이름입니다. 공백을 보내도 무관합니다.
    )
  )
```

## 광고 로드 및 그리기

1. `load()` 를 호출하면 onSuccess를 콜백을 통해서 [`DaroRewardedAd`](https://delightroom.github.io/daro-android-docs/daro/droom.daro.lib.reward/-daro-rewarded-ad/index.html) 를 얻을 수 있습니다.

   ```kotlin
   rewardedLoader.load(
     context = this,
     onSuccess = { ad ->
       ...
     },
     onFailure = { err ->
       ...
     }
   )
   ```

2. onSuccess 에서 받아온 [`DaroRewardedAd`](https://delightroom.github.io/daro-android-docs/daro/droom.daro.lib.reward/-daro-rewarded-ad/index.html) 에 `show()` 를 호출을 통해서 광고를 보여줄 수 있습니다.

   ```kotlin
   ad.show(
     activity = ...,
     adListener = object : DaroRewardedAdListener {
       override fun onEarnedReward(rewardItem: DaroRewardItem) {
       }

       override fun onFailedToShow(errorMsg: String) {
       }

       override fun onShown() {
       }

       override fun onDismiss() {
       }

       override fun onImpression() {
       }
     }
   )
   ```

   `DaroRewardedAdListener`를 통해서 광고 표시, 리워드 획득 등을 관리할 수 있습니다.
