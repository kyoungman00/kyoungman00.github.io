---
title: "[oracle] 배열 처리 인터페이스(Array Interface)"
categories:
  - oralce
tags:
  - oracle Array Interface
  - oracle 배열처리
  - 오라클 배열
---

# Oracle 배열 처리 인터페이스
로우 프리페치를 사용하여 데이터를 데이터베이스에 배열 형태로 전달하는 방식

## 동작 방식
배열 처리 인터페이스를 사용하면 단순 값(scalar value)이 아닌 배열을 바인드 할 수 있다.  

이는 DML 구문에서 여러 로우를 삽입하거나 변경할 경우에 매우 유용하다.  

## 언어별 처리 방법
### PL/SQL
```pl/sql  
DECLARE  
  TYPE t_id IS TABLE OF t.id%type;  
  TYPE t_pad IS TABLE OF t.pad%type;  
  l_id t_id := t.id();  
  l_pad t_pad := t.pad();  
BEGIN  
  -- Data Ready  
  l.id.excute(100000);  
  l.pad.exute(100000);  


  FOR i In 1...1000000  
  LOOP  
    l_id(i) := i;  
    l_pad(i) := rpad('*',100,'*');  
  END LOOP;  


  -- Data Insert  
  FORALL i In l_id.FIRST..l_id.LAST  
    INSERT INTO t VALUES (l_id(i), l_pad(i));  
  END;
  ```  


### JDBC

```java
sql = "INSERT INTO t VALUES (?,?)";  
statement = connection.prepareStatement(sql);  


for (int i=1; i<=100000; i++){  
  statement.setInt(1,i);  
  statement.setString(2,"... sme text ...");  
  statement.addBatch();  
}  


counts = statement.excuteBatch();  
statement.close();  
```  



