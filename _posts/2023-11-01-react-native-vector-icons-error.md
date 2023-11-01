---
title: "[react native] react-native-vector-icons/materialcommunityicons 깨짐 오류"
categories:
  - react-native
tags:
  - react-native
  - react-nateve react-native-vector-icons
  - react-native-vector-icons
  - materialcommunityicons
  - react-native-vector-icons/materialcommunityicons
---

# react-native-vector-icons/materialcommunityicons 깨짐 오류

## Android 

{project}\android\app\build.gradle 파일을 열어 아래 코드를 넣어준다.  
넣는 위치는 상관 없지만, 맨 아래 넣어주었다. 

```php
apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
``` 

코드를 붙여넣기 한 후에 npm run android 실행한다.

> npm run android

## iOS 

project cmd+p에서 info.plst를 검색한다. 

<plist><dict>의 맨 아래에 아래 코드를 붙여넣는다.  

```xml
	<key>UIAppFonts</key>  
	<array>  
		<string>AntDesign.ttf</string>  
		<string>Entypo.ttf</string>  
		<string>EvilIcons.ttf</string>  
		<string>Feather.ttf</string>  
		<string>FontAwesome.ttf</string>  
		<string>FontAwesome5_Brands.ttf</string>  
		<string>FontAwesome5_Regular.ttf</string>  		<string>FontAwesome5_Solid.ttf</string>  
		<string>Foundation.ttf</string>  
		<string>Ionicons.ttf</string>  
		<string>MaterialIcons.ttf</string>  
		<string>MaterialCommunityIcons.ttf</string>  
		<string>SimpleLineIcons.ttf</string>  
		<string>Octicons.ttf</string>  
		<string>Zocial.ttf</string>  
```

코드 붙여 넣은 후 yarn iOS || npm run IOS 실행한다.

 