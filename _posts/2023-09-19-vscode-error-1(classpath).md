---
title: "React-native npm run android error 'Could not resolve all task dependencies for configuration ':classpath' "
categories:
  - React-native
tags:
  - react-native
  - react-nateve error 
  - classpath error
---


## vscode에서 npm run android 명령어 실행 오류

> Could not resolve all task dependencies for configuration ':classpath' 

'classpath'를 찾을 수 없다는 오류인줄 알고 'classpath가 뭐길래?'로 엄청난 삽질을 한 결과...

하단에보면 jdk관련 오류 내용인걸 알 수 있었다. 
![set define on](/assets/images/vscode_npm_run_android_error_jdk.png)

react-native는 jdk8 버전부터 지원하여 옛 서적이나 관련 포스팅을 찾는 분들(즉, 나같은 사람..)은 jdk8을 설치하였을 것인데  
최근 부터 jdk8을 거절하고 jdk11을 권장하고 있어 jdk11을 설치해야한다.

jdk8이 설치된 경로에서 jdk8을 삭제하고 jdk11을 설치하여 환경변수까지 맞춰주면 오류가 사라진다.

