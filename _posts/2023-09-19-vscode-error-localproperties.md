---
title: "React-native npm run android error 'local.properties' "
categories:
  - React-native
tags:
  - react-native
  - react-nateve error 
  - local.properties error
---


## could not determine the dependencies of task ':app:compileDebugJavaWithJavac'.

![set define on](/assets/images/vscode_npm_run_android_error_localProperties.png)

SDK localtion 을 찾을 수 없다는 오류로 내용이다. 

error message에는 SDK location이 ANDROID_HOME 환경변수에 정의되거나, 프로젝트 경로에 'local.properties' 파일에 명시하라고되어있다.  


프로젝트 경로로 이동하여 'local.properties' 파일을 생성한 후. 아래 내용을 입력 저장한 후 vscode를 재시작하여 빌드한다.

> sdk.dir=/Users/km/Library/Android/sdk

