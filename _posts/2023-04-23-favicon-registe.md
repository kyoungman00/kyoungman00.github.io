---
title: "[github page] Github Page Favicon 등록하기, icon적용. register favicon"
categories:
  - github page
tags:
  - github page
  - favicon
  - favicon 등록
  - icon 등록
---

## registe favicon

"root\_includes\head\" 경로의 **custom.html** 파일을 수정합니다.   
*Modify **custom.html** in the path "root\_includes\head\".*



**custom.html** 파일에 아래 내용을 추가합니다.   
*Add the following to the **custom.html** file.*


```html
<!-- insert favicons. use https://realfavicongenerator.net/ -->
<link rel="apple-touch-icon" sizes="180x180" href="{{site.baseurl}}/assets/images/logo.ico/apple-touch-icon.png">
<link rel="icon" type="image/png" sizes="32x32" href="{{site.baseurl}}/assets/images/logo.ico">
<link rel="icon" type="image/png" sizes="16x16" href="{{site.baseurl}}/assets/images/logo.ico">
<link rel="mask-icon" href="{{site.baseurl}}/assets/images/logo.ico/safari-pinned-tab.svg" color="#5bbad5">
<meta name="msapplication-TileColor" content="#da532c">
<meta name="theme-color" content="#ffffff">

```


"root\assets\images\" 경로의 **logo.ico** 파일을 추가하는 내용입니다.  
*that's about adding the **logo.ico** file in the path "root\assets\images\".*



## result
![set define on](/assets/images/favicon_1.png)