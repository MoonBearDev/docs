---
sidebar_position: 3
---

# 네이티브 광고

## 네이티브 형태 소개

- 광고 뷰를 미디에이션 SDK가 구현해주는 타 광고 형태와 달리 네이티브 광고 형태는 구성 요소들을 전달받아 앱에서 직접 광고 뷰를 구현합니다.
- UIUX 기반으로 레이아웃을 직접 구현하므로써 위화감을 적게 만들 수 있다는 것이 가장 큰 특징입니다. 단, 유저가 광고가 아닌 컨텐츠로써 착각하는 경우를 방지하기 위해 광고 표시와 함께 최소한의 차별성은 부여해야합니다.

---

## View 생성하기

1. `DaroAdNativeView` 를 생성합니다.

   1. XML 사용시

      ```kotlin
      <?xml version="1.0" encoding="utf-8"?>
      ...
        <droom.daro.lib.banner.DaroAdNativeView
          android:layout_width="match_parent"
          android:layout_height="wrap_content"/>

      ...
      ```

   2. 코드 내부에서 생성 시

   ```kotlin
   val nativeView = DaroAdNativeView(context)
   ```

2. 뷰에 필요한 설정들을 정의합니다.

   ```kotlin
   nativeView.apply{
   	autoDestroy = ...

   	setListener(object: DaroAdView.DaroAdViewListener{
   		...
   	})

   	adNativeOption = DaroAdNativeOption()
   }
   ```

   1. 뷰를 선언하면 자체적으로 화면에 맞는 라이프사이클을 찾아 동작을 관리합니다. 따로 resume, pause, destroy를 호출하지 않아도 됩니다.
      1. `autoDestroy` 값을 false(default: true)로 설정하는 경우, destroy를 직접 호출해주셔야 합니다.
   2. `setListener` 를 통해서 광고뷰에 리스너를 추가할 수 있습니다.
   3. `adNativeOption` 를 통해서 광고 load에 필요한 option을 선언할 수 있습니다.

## 광고 그리기

1. 광고를 받아서 어떻게 그릴지 정의하는 DaroNativeAdRenderer 를 추가합니다.

   ```kotlin
   nativeView.setAdRenderer(
   	object : DaroAdNativeView.DaroNativeAdRenderer(){
       override fun buildAdView(
         context: Context,
         ad: DaroNativeAd,
         adViewContainer: DaroNativeAdViewContainer,
       ): View {

         return LayoutInflater.from(context).inflate(R.layout.layout_native, null).also {
           val title: TextView = it.findViewById(R.id.view_title)
           val icon: ImageView = it.findViewById(R.id.view_icon)
           val body: TextView = it.findViewById(R.id.view_body)
           val cta: TextView = it.findViewById(R.id.button_cta)

   				// 광고 정보를 받아와서 뷰에 설정
           title.text = ad.getHeadline() ?: ""
           body.text = ad.getBody() ?: ""
           cta.text = ad.getCallToAction() ?: ""

           Glide
             .with(context)
             .load(ad.getIcon()?.uri)
             .into(icon)

   				// 광고 컨테이너에 광고 관련 뷰 등록
           adViewContainer.setHeadlineView(title)
           adViewContainer.setIconView(icon)
           adViewContainer.setBodyView(body)
           adViewContainer.setCallToActionView(cta)
         }
       }
     }
   )
   ```

   1. adViewContainer에 내부 뷰에 대한 정보들을 등록해주어야 합니다.
   2. `DaroNativeAdTemplate` 를 통한 기본 템플릿을 제공합니다.

      ```kotlin
      nativeView.setAdRenderer(DaroNativeAdTemplate.LINE)
      nativeView.setAdRenderer(DaroNativeAdTemplate.BANNER)
      nativeView.setAdRenderer(DaroNativeAdTemplate.LINE_CENTER)
      ```

2. `load()` 메서드를 호출합니다.

   ```kotlin
   nativeView.load(
       DaroAdNativeUnit(
         unitId = ${unitId},
         placementName = ${placementName}, //로그 상 보여질 이름입니다. 공백을 보내도 무관합니다.
         refreshSeconds = 3
       )
   )
   ```

- load 호출 전에 반드시 DaroNativeAdRenderer를 선언해주어야 합니다.

💡 새로고침을 원하지 않을 경우 `refreshSeconds`를 `0` 으로 설정해주세요.
