---
title: "[Solved] React-native Faild to build gem native extension"
categories:
  - React-native
tags:
  - react-native
  - react-nateve error 
  - local.properties error
---


# Error Gem::Ext::BuildError: ERROR: Faild to build gem native extension.

![set define on](/assets/images/react-native-error-error-gem.png)

react-native 프로젝트를 만들던 중 오류가 발생했다. 
Ouccured Error when I make react-native project that is 'Error Gem, Faild to build gem native extension'. 

해당 오류는 build에 필요한 부분을 검토해봐야한다. 
You check the things that used building react-native project.

1. pod --version 으로 cocoapods 가 사용가능한지 확인한다. 
1. Enter 'pod --version' and check whether 'cocoapods' is available.

2. ruby -v 로 ruby가 사용가능한지 확인한다. 
2. Enter 'ruby -v' and check wheter 'ruby' is available.

3. sudo xcodebuild -license 로 xcode licence가 사용가능한지 확인한다. 
3. Enter 'sudo xcodebuild -license' and check wheter 'xcode license' is available.

