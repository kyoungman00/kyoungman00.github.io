---
title: "React - Replace, ReplaceAll 처럼 사용하기"
categories:
  - React
tags:
  - React
---

# Replace를 ReplacsAll 처럼 사용하기

javascript에서는 Replace가 전체 문자열에서 특정 문자열을 대체 문자열로 변환하지 않고, 첫 번째 검색된 문자열에대해 처리한다.

```javascript
var date = '2023-03-29';

console.log("value : " + date.replace("-",""));
```


```bash
value : 202303-29
```

전체 문자열에대해 변경하려하면, 정규식을 사용해야한다.

```javascript
var date = '2023-03-29';

console.log("valeu : " + date.replace(/-/g,""));
```

```bash
value : 20230329
```

### Syntax
```javascript
str.replace(/str1/[regex],"str2");
```

> g : 발생할 모든 패턴에대해 적용
> i : 대소문자 구분 안함.
> m : 여러줄 검색