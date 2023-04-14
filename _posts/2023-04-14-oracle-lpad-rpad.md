---
title: "[oracle] 특정 문자 채우기(앞 0 채우기), LPAD, RPAD"
categories:
  - oracle
  - sql
tags:
  - oracle
  - '0'
  - LPAD
  - RPAD
  - select/where
  - 오라클
  - 0채우기
---

# LPAD & RPAD
oracle에서 숫자열로 입력된 Data 앞, 뒤에 '0'을 채워 원하는 자리수로 만들기 위해 사용한다. 


# LPAD 
문자열 앞에 원하는 자리 수 만큼 원하는 문자를 추가한다.  

```sql
SELECT LPAD(123,10,0) AS LPAD_10_0   -- 123 앞으로 10자리가 될 때까지 0을 채운다. 
       , 123 AS ORIGIN
  FROM DUAL;
```

![set define on](/assets/images/oracle_lpad.png)




# RPAD 
문자열 뒤에 원하는 자리 수 만큼 원하는 문자를 추가한다.  

```sql
SELECT RPAD(123,10,0) AS LPAD_10_0   -- 123 뒤로 10자리가 될 때까지 0을 채운다. 
       , 123 AS ORIGIN
  FROM DUAL;
```

![set define on](/assets/images/oracle_rpad.png)

