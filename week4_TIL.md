# SQL_BASIC 4주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_4th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**4주차 과제부터는 강의 내용을 정리하는 것과 함께, 프로그래머스에서 제공하는 SQL 문제를 직접 풀어보는 실습도 병행합니다.** 강의에서는 **배운 내용을 정리하고 주요 쿼리 예제를 정리**하며, 프로그래머스 문제는 **직접 풀어본 뒤 풀이 과정과 결과, 배운 점을 함께 기록**해주세요. 완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_4th

### 섹션 4. 쿼리 잘 작성하기, 쿼리 작성 템플릿 및 오류를 잘 디버깅하기

### 3-4. 오류를 잘 디버깅하는 방법



## 섹션 5. 데이터 탐색 - 변환

### 4-1. INTRO

### 4-2. 데이터 타입과 데이터 변환(CAST, SAFE_CAST)

### 4-3. 문자열 함수(CONCAT, SPLIT, REPLACE, TRIM, UPPER)

### 4-4. 날짜 및 시간 데이터 이해하기(1) (타임존, UTC, Millisecond, TIMESTAMP/DATETIME)



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | 🍽️         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리

## 3-4. 오류를 디버깅하는 방법

~~~
✅ 학습 목표 :
* 오류의 정의에 대해 설명할 수 있다. 
* 오류 메시지를 보고 디버깅이라는 과정을 수행할 수 있다. 
~~~

- 대표적인 오류 카테고리 : Syntax error (문법 오류)
- 문법을 지키지 않아 생기는 오류
- error message를 보고 번역 또는 해석한 후, 해결 방법 찾아보기

~~~
SELECT list must not be empty at [10:1]
: SELECT 목록은 [10:1]에서 비어 있으면 안됩니다

SELECT
  col => 이 부분이 비어있기에 생기는 오류
FROM
~~~

~~~
Number of arguments does not match for aggregate function COUNT

SELECT
  COUNT(id,kor_name)
FROM basic.pokemon

COUNT() ()안에는 1개의 인자만 가능함
~~~

~~~
Expected end of input but got keyword SELECT

하나의 쿼리엔 SELECT가 1개만 있어야함.
혹은 쿼리가 끝나는 부분에 ; 붙이고 실행할 부분만 드래그 앤 드랍해서 실행하기
~~~

~~~
Expected end of input but got keyword WHERE at [5:1]

LIMIT 은 가장 마지막에 있어야하는데 WHERE 전에 있음
~~~


## 4-2. 데이터 타입과 데이터 변환(CAST, SAFE_CAST)

~~~
✅ 학습 목표 :
* 데이터 타입의 종류를 설명할 수 있다. 
* 데이터 타입을 변환하는 방법을 설명할 수 있다. 
~~~

- SELECT 문에서 데이터를 변환시킬 수 있음 (or WHERE의 조건문에서도 사용 가능)
- 데이터의 타입에 따라 다양한 함수가 존재
- 보이는 것과 저장된 것의 차이가 존재하기 때문에 데이터 타입이 중요함.

~~~
자료 타입을 변경하는 함수: CAST

SELECT
  CAST(1 AS STRING) #숫자 1을 문자 1로 변경
if)CAST("카일스쿨" AS INT64) #오류 SAFE_CAST로 바꾸면 NULL로 반환
~~~

~~~
수학 함수는 수학연산(평균, 표준편차, 코사인 등)이 존재

TIP)
나누기를 할 경우
x/y 대신 SAFE_DIVIDE 함수 사용하기
SAFE_DIVIDE(x,y)
x,y 중 하나라도 0인 경우 그냥 나누면 zero error가 발생
~~~


## 4-3. 문자열 함수(CONCAT, SPLIT, REPLACE, TRIM, UPPER)

~~~
✅ 학습 목표 :
* 문자열 함수들의 종류를 이해하고 어떠한 상황에서 사용하는지 설명할 수 있다. 
~~~

~~~
SELECT
  CONCAT("안녕","하세요") AS result
:안녕하세요

SELECT
  SPLIT("가, 나, 다, 라",",") AS result
:가 나 다 라
SPLIT(문자열 원본, 나눌 기준이 되는 문자)

SELECT
  REPLACE("안녕하세요", "안녕", "실천") AS result
REPLACE(문자열 원본, 찾을 단어, 바꿀 단어)

SELECT
  TRIM("안녕하세요", "하세요") AS result
TRIM(문자열 원본, 자를 단어)

SELECT
  UPPER("abc") AS result
UPPER(문자열 원본)
~~~

## 4-4. 날짜 및 시간 데이터 이해하기(1) (타임존, UTC, Millisecond, TIMESTAMP/DATETIME)

~~~
✅ 학습 목표 :
* 날짜 및 시간 데이터 타입과 UTC의 개념을 설명할 수 있다. 
* DATE, DATETIME, TIMESTAMP 에 대해서 설명할 수 있다.
* 시간함수들의 종류와 시간의 차이를 추출하는 방법을 설명할 수 있다. 
~~~

- 타임존
- UTC: Universal Time Coordinated(한국 시간: UTC+9)
- 국제적인 표준 시간
- 협정 세계시
- 타임존이 존재한다 = 특정 지역의 표준 시간대

- TIMESTAMP
- 시간 도장
- UTC부터 경과한 시간을 나타내는 값
- Time Zone 정보 있음
- 2023-12-31 14:00:00 UTC

millisecond(ms)
- 시간의 단위, 천 분의 1초
microsecond
- 1/1,000ms

~~~
SELECT
  TIMESTAMP_MILLIS(1734242) AS milli_to_timestamp_value,
  TIMESTAMP_MICROS(1738424000) AS micro_to_timestamp_value,
  DATETIME(TIMESTAMP_MICROS(14338314000) AS datetime_value;
~~~

- 많은 회사들의 Table에 시간이 TIMESTAMP로 저장된 경우가 많음(or DATETIME)
- TIMESTAMP<->DATETIME 변환을 해야할 수 있음

- UTC가 있다? TIMESTAMP. 한국 시간 -9시간
- T가 나옴? DATETIME. 한국 시간과 동일

<br>

<br>

---

# 2️⃣ 확인문제 & 문제 인증

## 프로그래머스 문제 

> 조건에 맞는 도서 리스트 출력하기
>
> **먼저 문제를 풀고 난 이후에 확인 문제를 확인해주세요**
>
> 문제 링크 
>
> :  https://school.programmers.co.kr/learn/courses/30/lessons/144853

<!-- 문제를 풀기 위하여 로그인이  필요합니다. -->

<!-- 정답을 맞추게 되면, 정답입니다. 라는 칸이 생성되는데 이 부분을 캡처해서 이 주석을 지우시고 첨부해주시면 됩니다. --> 



## 문제 1

> **🧚Q. 프로그래머스 문제를 풀던 규서는 여러 번의 시행착오 끝에 결국 혼자 해결하기 어려워 오류 메시지를 공유하며 도움을 요청했습니다. 여러분들이 오류 메시지를 확인하고, 해당 SQL 쿼리에서 어떤 부분이 잘못되었는지 오류 메시지를 해석하고 찾아 설명해주세요.**

~~~sql
# 조건에 맞는 도서 리스트 출력하기
# 규서의 SQL 첫 번째 풀이
SELECT BOOK_ID, PUBLISHED_DATE
FROM BOOK
WHERE CATEGORY = '인문'
  AND YEAR(PUBLISHED_DATE, 2021);
  
오류 메시지 : Error: Number of arguments does not match for function YEAR
~~~



~~~
여기에 답을 작성해주세요!
~~~



### 🎉 수고하셨습니다.
