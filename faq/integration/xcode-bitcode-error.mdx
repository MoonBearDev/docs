---
sidebar_position: 4
---

# Xcode 16 환경에서의 bitcode 에러 이슈

Xcode 16에서 Daro iOS SDK 활용시 bitcode에 대한 에러와 함께 배포가 되지 않는 이슈에 대한 안내입니다.

## 현상

조치 없이 SDK 연동을 진행했을 때, 빌드하고 디바이스에 디버깅 설치로 테스트까지 진행이 되지만 이후 testflight 등에 올리기 위한 목적으로 배포 하는 과정에 특정 프레임워크에서 bitcode를 포함하고 있다는 내용과 함께 Asset validation failed 발생.

## 원인

- 애플에서 Xcode 16부터 bitcode를 deprecation하면서 bitcode를 활용하고 있는 다양한 외부 프레임워크에 대해서도 이슈가 발생합니다.
- Daro iOS SDK가 활용하고 있는 일부 프레임워크도 bitcode를 포함하고 있으며, 이들 프레임워크를 포함하여 앱에서 활용하는 다른 프레임워크에서도 bitcode를 활용중인지 확인하고 조치를 취할 필요가 있습니다.
- 추후 SDK 프레임워크를 제작한 외부 업체에서 bitcode를 SDK에서 제거하면 해당 이슈는 해결될 것으로 보이나, 현재는 과도기적인 상황으로 메뉴얼하게 제거를 진행해야 합니다.


## 솔루션

- Podfile 최 하단에 아래 코드를 붙여서 다시 빌드하고 배포를 시도합니다. bitcode를 활용하고 있는 프레임워크에서 bitcode_strip을 통해 bitcode를 제거하고 빌드하는 방법입니다.

  ```ruby
  post_install do |installer|

    installer.pods_project.targets.each do |target|

      if target.name == 'OpenWrapSDK'
        `xcrun -sdk iphoneos bitcode_strip -r Pods/OpenWrapSDK/OpenWrapSDK/OMSDK_Pubmatic.xcframework/ios-arm64/OMSDK_Pubmatic.framework/OMSDK_Pubmatic -o Pods/OpenWrapSDK/OpenWrapSDK/OMSDK_Pubmatic.xcframework/ios-arm64/OMSDK_Pubmatic.framework/OMSDK_Pubmatic`
      end

      if target.name == 'HyBid'
        `xcrun -sdk iphoneos bitcode_strip -r Pods/HyBid/PubnativeLite/PubnativeLite/OMSDK-1.4.10/OMSDK_Pubnativenet.xcframework/ios-arm64/OMSDK_Pubnativenet.framework/OMSDK_Pubnativenet -o Pods/HyBid/PubnativeLite/PubnativeLite/OMSDK-1.4.10/OMSDK_Pubnativenet.xcframework/ios-arm64/OMSDK_Pubnativenet.framework/OMSDK_Pubnativenet`
      end

      if target.name == 'smaato-ios-sdk'
        `xcrun -sdk iphoneos bitcode_strip -r Pods/smaato-ios-sdk/vendor/OMSDK_Smaato.xcframework/ios-arm64_armv7/OMSDK_Smaato.framework/OMSDK_Smaato -o Pods/smaato-ios-sdk/vendor/OMSDK_Smaato.xcframework/ios-arm64_armv7/OMSDK_Smaato.framework/OMSDK_Smaato`
      end
    end
  end
  ```