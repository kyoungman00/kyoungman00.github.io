---
title: "[react-native] 디바이스 별로 스타일 지정, Platform"
categories:
  - react-native
tags:
  - react-native
  - react-nateve platform
---


# IOS, Android OS에 따라 Style지정하기


MD2Colors와 color를 사용하기 위해 다음을 설치해준다. 

> npm i react-native-vector-icons react-native-paper
> npm i color 
> npm i -D @types/color


```javascript Platform StyleSheet 적용 예시.
import {Platform, StyleSheet} from 'react-native'
import { MD2Colors as Colors } from 'react-native-paper'
import color from 'color'

const styles = StyleSheet.create({
  safeAreaView:{backgroundColor:Colors.blue500,flex:1
    , paddingLeft: Platform.select({ios:0, android:20}) },
  text:{fontSize:20, color:color(Colors.blue500).lighten(0.9).string()},
  box:{width:'70%', height:100, backgroundColor:'white',marginBottom:10
    , marginLeft: Platform.select({ios:20, android:0}) },
  border:{borderWidth:10, borderColor:Colors.lime500}
})


