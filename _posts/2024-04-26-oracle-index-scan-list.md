---
title: "[oracle] index scan 종류"
categories:
  - oralce
tags:
  - oracle index scan
  - oracle
---

# Oracle Index Scan 종류


### Index Range Scan  

B*Tree의 가장 일반적이고 정상적인 형태의 엑세스 방법  
Index Root에서 리프 블록까지 수직적 탐색 후에 필요한 범위만 Scan.  


> SELECT STATEMENT Optimizer=ALL_ROWS  
>   TABLE ACCESS (BY INDEX ROWID) OF ‘TABLE_NAME’ (TABLE)  
>     INDEX (RANGE SCAN) OF ‘TABLE_INDEX_01’ (INDEX)  



### Index Full Scan  

수직적 탐색 없이 Index 리프 블록을 처음 수평적 탐색하는 방법.  
최적의 index가 없을 때 차선으로 선택된다.   

> SELECT STATEMENT Optimizer=ALL_ROWS  
>   TABLE ACCESS (BY INDEX ROWID) OF ‘TABLE_NAME’ (TABLE)  
>  INDEX (FULL SCAN) OF ‘TABLE_INDEX_01’ (INDEX)  

인덱스 선두 컬럼이 없어 Table Full Scan을 하려는데 대용량 테이블인 경우 Index Full Scan을 차선으로 선택한다.   
→ 찾고자하는 데이터가 극히 일부일 때 해당되며, 찾는 데이터가 대부분인 경우에는 Table Full Scan이 더 좋다.   
→ 선두 컬럼이 없이 Index 컬럼으로 조건이 되어있는 경우만 사용가능하지, index 컬럼이 사용되지 않은 경우에는 Table Full Scan할 수 밖에 없다.   



### index Unique Scan

수직적 탐색으로만 데이터를 찾는 스캔 방식.  
Unique Index를 ‘=’ 로만 찾는 경우.
→ Index는 데이터를 찾는 것이 아닌 데이터 시작 지점을 찾는 것이라 하였지만 이처럼 Unique Scan인 경우에는 Index와 데이터가 매칭되므로 데이터를 찾을 수 있다.   

> SELCT STATEMENT Optimizer=ALL_ROWS  
>   TALBE ACCESS (BY INDEX ROWID) OF ‘TABLE_NAME’ (TABLE)  
>     INDEX (UNIQUE SCAN) OF ‘PK_INDEX’ (UNIQUE)  


UNIQUE INDEX를 ‘=’ 아닌 범위 조건으로 사용하면 INDEX RANGE SCAN이 된다.  



### INDEX SKIP SCAN

인덱스 선두 컬럼을 사용하지 않으면 TABLE FULL SCAN을 혹은 TALBE FULL SCAN보다 I/O를 줄일 수 있다면 INDEX FULL SCAN을 사용한다.  
Oracle 9i 부터 Index Skip Scan을 사용할 수 있다.  


조건절에 빠진 인덱스 선두 컬럼의 Distinct Value 개수가 적고 후행 컬럼의 Distinct Value 개수가 많을 때 유리하다.   
Hint는 Index_ss, no_index_ss로 설정, 해제 할수 있다.  


> SELECT STATEMENT Optimizer=ALL_ROWS  
>   TABLE ACCESS (BY INDEX ROWID) OF ‘TABLE_NAME’ (TABLE)  
>     INDEX (INDEX SKIP SCAN) OF ‘TABLE_INDEX_01’ (INDEX)  


선두 컬럼인 성별에 해당하는 값이 ‘남’, ‘여’  2가지로 적었기 때문에 효율이 좋다.   
만약 그 보다 많은 값을 가지고 있었다면 남 < 800 과 남 > 100000 이상의 Index를 계속해서 탐색해야 하기 때문이다.   
- 인덱스 선두 컬럼의 Distinct Value가 적고 ,, 후행 컬럼의 Distinct Value 개수가 많을 때 효과적  
- 중간 Index가 없는 경우 사용할 수 있음.  
- 선두 컬럼이 범위 조건 (부등호, BETWEEN, LIKE) 인 경우도 사용할 수 있음.  

→ 이것은 통계정보가 정확하여 Distinct Value 개수 혹은 Value의 분포가 고른 경우 사용에 효율성이 나온다.   


데이터가 특정 Value에 치우쳐있다면 해당 조건을 Index Full Scan이 유리할 수 있다.   



### Index Fast Full Scan

논리적 인덱스 트리구조를 무시하고 Index 세그먼트 전체를 Multiblock I/O 방식으로 스캔함.  
Hint는 index_ff, no_index_ff로 설정, 해제 할 수 있다.  


논리적 구조가 아닌 물리적 저장 구조로 Multiblock을 가져오기 때문에 I/O를 줄여 속도롤 높인다.
하지만 논리적 구조를 따르지 않기 때문에 인덱스 키 순서대로 정렬되지 않으며, 쿼리에 사용된 컬럼이 모두 인덱스에 포함되어 있을 때 사용할 수 있다.   


또한 Index가 파티션 되어있지 않아도 병렬 쿼리가 가능하다.  

> 병렬 쿼리 : 여러개의 시스템 자원을 사용하여 DML을 분산처리하는 방식  


> alter session enable parallel dml; — parallel dml enable 처리  
> select */*+ parallel(A,4) */* from tmp A;  — **/*+ parallel(테이블, 코어수) */ 로 Hint**  

→ A table을 4개의 CPU를 사용하여 병렬 쿼리하는 것으로 서로 겹쳐지지 않게 파티션되어있을 때 사용할 수 있는 것 같다.   


| Index Full Scan | Index Fase Full Scan |  
| --- | --- |  
| 1. 인덱스 구조를 따라 스캔(논리적) | 1. 세그먼트 전체를 스캔(물리적) |  
| 2. 결과집합 순서 보장 | 2. 결과집합 순서 보장 안됨. |  
| 3. Single block I/O | 4. Multiblock I/O |  
| 4. 파티션 되어있어야 병렬스캔 가능 | 4. 파티션 되어있지 않아도 병렬 스캔 가능 |  
| 5. 인덱스에 포함되지 않은 컬럼 조회 시에도 사용 가능 | 5. 인덱스에 포함된 컬럼만으로 조회할 때 사용 가능 |  



### Index Range Scan Descending

Index Range Scan과 동일한 스캔 방식으로 뒤에서 부터 앞으로 조회하여 내림차순으로 정렬된 결과집합을 얻음. 
Hint는 index_desc로 설정할 수 있다.  

> SELECT STATEMENT Optimizer=ALL_ROWS  
>   TABLE ACCESS (BY INDEX ROWID) OF ‘TABLE_NAME’ (TABLE)  
>     INDEX (RANGE SCAN DESCENDING) OF ‘TABLE_INDEX_01’ (INDEX)  


Max() 값을 구할 때 사용한다. 
 
> SELECT STATEMENT Optimizer=ALL_ROWS  
  SORT (AGGREGATE)   
>     FIRST ROW  
>       INDEX (RANGE SCAN (MIN/MAX)) OF ‘TABLE_INDEX_01’ (INDEX)  
>   TABLE ACCESS (FULL) OF ‘TABLE_NAME’ (TABLE)  