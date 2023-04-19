---
title: "[oracle] 같은 컬럼(column)의 이전, 이후 데이터 조회, LAG, LEAD"
categories:
  - oracle
  - sql
tags:
  - oracle
  - before
  - LAG
  - after
  - LEAD
  - select/where
  - 오라클
---


# LAG & LEAD
oracle에서 동일 컬럼의 바로 전, 바로 이후의 데이터 변화 내역을 비교하기위해 사용한다.  
LAG는 window함수 partition 그룹에 대해 order by 기준으로 바로 이전 데이터를 조회한다.  
LEAD는 window함수 partition 그룹에 대해 order by 기준으로 바로 이후 데이터를 조회한다.  


# DATA 구성

LAG, LEAD를 조회하기 위해, With를 사용하여 임시 다음과 같이 데이터를 구성합니다.  
![set define on](/assets/images/oracle_lag_lead_data.png)


# LAG
window함수 partition 그룹에 대해 order by 기준으로 바로 이전 데이터를 조회.  


LAG함수를 사용하여 조회한 결과입니다.  
```sql
WITH DATA AS (
      SELECT 1 AS SEQ,  'A' AS ITEM, '1000' AS VALUE FROM DUAL UNION ALL
      SELECT 2 AS SEQ,  'A' AS ITEM, '1100' AS VALUE FROM DUAL UNION ALL
      SELECT 3 AS SEQ,  'B' AS ITEM, '2000' AS VALUE FROM DUAL UNION ALL
      SELECT 4 AS SEQ,  'B' AS ITEM, '2100' AS VALUE FROM DUAL UNION ALL
      SELECT 5 AS SEQ,  'A' AS ITEM, '1200' AS VALUE FROM DUAL UNION ALL
      SELECT 6 AS SEQ,  'A' AS ITEM, '1300' AS VALUE FROM DUAL UNION ALL
      SELECT 7 AS SEQ,  'B' AS ITEM, '2200' AS VALUE FROM DUAL
)
SELECT A.ITEM
       , A.VALUE
       -- ITEM별로 VALUE의 값을 기준으로 정렬하여 바로 이전 VALUE 조회.
       , LAG(A.VALUE) OVER (PARTITION BY A.ITEM ORDER BY A.VALUE) AS LAG_VALUE 
 FROM DATA A
ORDER BY A.SEQ

```

![set define on](/assets/images/oracle_lag_select.png)


LAG는 이전 값을 조회하므로, 맨 처음 ROW에 대해 LAG값이 조회되지 않습니다.   



# LEAD
window함수 partition 그룹에 대해 order by 기준으로 바로 이후 데이터를 조회.  


LEAD함수를 사용하여 조회한 결과입니다.  
```sql
WITH DATA AS (
      SELECT 1 AS SEQ,  'A' AS ITEM, '1000' AS VALUE FROM DUAL UNION ALL
      SELECT 2 AS SEQ,  'A' AS ITEM, '1100' AS VALUE FROM DUAL UNION ALL
      SELECT 3 AS SEQ,  'B' AS ITEM, '2000' AS VALUE FROM DUAL UNION ALL
      SELECT 4 AS SEQ,  'B' AS ITEM, '2100' AS VALUE FROM DUAL UNION ALL
      SELECT 5 AS SEQ,  'A' AS ITEM, '1200' AS VALUE FROM DUAL UNION ALL
      SELECT 6 AS SEQ,  'A' AS ITEM, '1300' AS VALUE FROM DUAL UNION ALL
      SELECT 7 AS SEQ,  'B' AS ITEM, '2200' AS VALUE FROM DUAL
)
SELECT A.ITEM
       , A.VALUE
       -- ITEM별로 VALUE의 값을 기준으로 정렬하여 바로 이후 VALUE 조회.
       , LEAD(A.VALUE) OVER (PARTITION BY A.ITEM ORDER BY A.VALUE) AS LEAD_VALUE 
 FROM DATA A
ORDER BY A.SEQ

```

![set define on](/assets/images/oracle_lead_select.png)


LEAD는 이후 값을 조회하므로, 맨 마지막 ROW에 대해 LEAD값이 조회되지 않습니다.  


# TIP
> LAG, LEAD 함수와 원본 Value를 비교하려 한다면,  
> LAG는 맨 처음 ROW에대해 null이, LEAD는 맨 마지막 ROW에 대해 null이 Return되므로    
> NVL()를 처리해주는 것이 좋다.   
