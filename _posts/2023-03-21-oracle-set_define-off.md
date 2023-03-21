---
title: "oracle '&' 조회 방법 (set define off)"
categories:
  - oracle
  - sql
tags:
  - oracle
  - '&'
  - select/where
  - 오라클
  - ampersand
---

# Set Define Off
'&' 의 기호를 DML에서 문자형태로 사용하기 위해서 조회전 ***set Define off*** 설정을 해줘야한다.  
oracle에서 '&'기호는 바로뒤 문자를 varialble로 인식하여 실행 시 대입을 요청한다.

'&'를 사용한 DML을 Golden6에서 set define 설정을 on/off 하여 실행한 경우의 예시이다.

`SELECT '&use Ampersnad' AS RESULT FROM DUAL;`

*set define off*를 하지 않은  *set define on*에서 실행한 결과이다.  

/assets/images/set_define_on_variable_input.png

*set define off*를 설정한 후 조회한 결과이다.  

/assets/images/set_define_off_result.png