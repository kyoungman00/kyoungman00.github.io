---
title: "[oracle] sql hint 종류"
categories:
  - oralce
tags:
  - oracle hint
  - oracle
---

# Oracle SQL Hint 종류

## 최적화 목표  
ALL_ROWS : 전체 처리속도 최적화  
FRIST_ROWS(N) : 최초 N건 응답속도 최적화  



## 엑세스 방식  
FULL : Table Full Scan 유도  
Index : Index Scan 유도  
INDEX_DESC : Index 역순으로 Scan 유도  
INDEX_FFS : Index Fast Full Scan 유도  
INDEX_SS : Index Skip Scan 유도  



## 조인 순서  
ORDERED : From 절에 나열된 순서대로 조인  
LEADING : LEADING 힌트 괄호에 기술된 순소대로 조인  
SWAP_JOIN_INPUTS : 해시 조인 시, BUILD INPUT을 명시적으로 선택  



## 조인 방식  
USE_NL : NL 조인으로 유도  
USE_MERGE : 소트 머지 조인 유도  
USE_HASH : 해시 조인 유도  
NL_SJ : NL 세미 조인 유도  
MERGE_SJ : 소트 머지 세미조인 유도  
HASH_SJ : 해시 세미조인 유도  



## 서프쿼리 팩토링  
MATERIALIZE : WITH문으로 정의한 집합을 물리적으로 생성하도록 유도  
INLINE : WITH문으로 정의한 집합을 물리적으로 생성하지 않고 INLINE 처리하도록 유도  



## 쿼리 변환  
MERGE : 뷰 머징 유도  
NO_MERGE : 뷰 머징 방지  
UNNEST : 서브쿼리 Unnesting 유도  
NO_UNNEST : 서브쿼리 Unnesting 방지  
PUSH_PRED : 조인 조건 Pushdown 유도  
NO_PUSH_PRED : 조인 조건 Pushdown 방지  
USE_CONCAT : OR 또는 IN-List 조건을 OR-Expansion으로 유도  
NO_EXPAND : OR 또는 IN-List 조건에 대한 OR-Expansion 방지  



## 병렬 처리  
PARALLEL : 테이블 스캔 또는 DML을 병렬방식으로 처리하도록 유도  
PARALLER_INDEX : 인덱스 스캔을 병렬방식으로 처리하도록 유도  
PQ_DISTRIBUTE : 병렬 수행 시 데이터 분배 방식 결정  



## 기타  
APPEND : Direct-Path Insert 유도  
DRIVING_SITE : DB Link Remote 쿼리에 대한 최적화 및 실행 주체 지정  
PUSH_SUBQ : 서브쿼리를 가급적 빨리 필터링하도록 유도  
NO_PUSH_SUBQ : 서브쿼리를 가급적 늦게 필터링하도록 유도  