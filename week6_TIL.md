# SQL_BASIC 6주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_6th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**6주차 과제는 강의 내용을 정리하는 것과 함께, 프로그래머스에서 제공하는 SQL 문제를 직접 풀어보는 실습도 병행합니다.** 강의에서는 **배운 내용을 정리하고 주요 쿼리 예제를 정리**하며, 프로그래머스 문제는 **직접 풀어본 뒤 풀이 과정과 결과, 배운 점을 함께 기록**해주세요. 완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_6th

### 섹션 6. 다량의 자료를 연결 : JOIN 

### 5-1. Intro

### 5-2. JOIN 이해하기

### 5-3. 다양한 JOIN 방법

### 5-4. JOIN 쿼리 작성하기 

### 5-5. JOIN을 처음 공부할 때 헷갈렸던 부분

### 5-6. JOIN 연습문제 1~2번

### 5-6. JOIN 연습문제 3~5번

### 5-7. 정리



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | ✅         |
| 6주차 | 섹션 **5-1** ~ **5-7** | ✅         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<!-- 여기까진 그대로 둬 주세요-->

<br>

---

# 1️⃣ 개념정리

## 5-2. JOIN 이해하기

~~~
✅ 학습 목표 :
* JOIN에 대한 정의와 필요성에 대해 설명할 수 있다.
~~~

SQL JOIN
- SQL을 처음 배울 때, 어려울 수 있는 부분
- 간단하게 "서로 다른 데이터 테이블을 연결하는 것"
- 많은 문제 풀이를 통한 체화
- 공통적으로 존재하는 컬럼(=key)이 있다면, JOIN할 수 있음
- 보통 id 값을 key로 많이 사용하고, 특정 범위(예:Date)로 JOIN도 가능함

~~~
트레이너가 포획한 포켓몬 기준으로 트레이너 데이터를 연결하기 (JOIN)
연결할 수 있는 Key=trainer_id,id
trainer_id 컬럼 기준으로 트레이너 데이터를 연결
~~~

JOIN을 해야하는 이유 - 데이터 저장되는 형태에 대한 이해
- 관계형 데이터베이스(RDBMS) 설계 시 정규화 과정을 거침
- 정규화는 중복을 최소화하게 데이터를 구조화
- User Table은 유저 데이터만, Order table은 주문 데이터만
- 따라서 데이터를 다양한 table에 저장해서 필요할 때 join해서 사용
- 데이터 분석하는 관점에선 미리 JOIN되어 있는 것이 좋지만, 개발 관점에선 분리되어 있는 것이 좋음
- 대신 데이터 웨어하우스에서 JOIN+필요한 연산을 해서 "데이터 마트"를 만들어서 활용

## 5-3. 다양한 JOIN 방법

~~~
✅ 학습 목표 :
* JOIN 방법들의 종류를 설명할 수 있다. 
* 각 JOIN 방법들의 차이점에 대해서 설명할 수 있다. 
~~~

- (INNER) JOIN: 두 테이블의 공통 요소만 연결
- LEFT/RIGHT (OUTER) JOIN: 왼쪽/오른쪽 테이블 기준으로 연결
- FULL (OUTER) JOIN: 양쪽 기준으로 연결
- CROSS JOIN: 두 테이블의 각각의 요소를 곱하기


## 5-4. JOIN 쿼리 작성하기 

~~~
✅ 학습 목표 :
* JOIN을 사용한 문법에 대해 이해하여 적용할 수 있다.
* JOIN 을 활용한 쿼리를 작성할 수 있다. 
~~~

~~~
1. 테이블 확인: 테이블에 저장된 데이터, 컬럼 확인
2. 기준 테이블 정의: 가장 많이 참고할 기준(base) 테이블 정의
3. JOIN Key 찾기: 여러 Table과 연결할 key(ON) 정리
4. 결과 예상하기: 결과 테이블을 예상해서 손, 엑셀로 작성(일종의 정답지 역할)
5. 쿼리 작성/검증: 예상한 결과와 동일한 결과가 나오는지 확인
~~~
~~~
FROM 하단에 JOIN할 Table을 작성하고
ON 뒤에 공통된 컬럼(key)를 작성

SELECT
  A.col1,
  A.col2,
  B.col1 1,
  B.col1 2
FROM table1 AS A
LEFT JOIN table2 AS B
ON A.key=B.key
~~~
~~~
예시
SELECT
  tp.id,
  tp.trainer_id,
  tp.pokemon_id,
  t.id AS trainer_id,
  t.age,
  t.hometown
  p.*
FROM basic.trainer_pokemon AS tp
LEFT JOIN basic.trainer AS t
ON tp.trainer_id=t.id
LEFT JOIN basic.pokemoon AS p #위에까지를 하나의 테이블로 인식
ON tp.pokemon_id=p.id
~~~

## 5-6. JOIN 연습문제 1~5번 

~~~
✅ 학습 목표 :
* 연습문제(3문제 이상) 푼 것들 정리하기
~~~

1
~~~
#연산량 관점에서 필터링 먼저 해서 row 수를 줄이고 JOIN 하는게 효율적임.
#table을 그대로 사용해야 하는가, 혹은 줄이고 쓰는게 내 목적에 맞는가 확인하기!
#JOIN에서 사용하는 테이블에 중복된 컬럼 이름 있으면 꼭 어떤 테이블의 컬럼인지 명시해야 함.

SELECT
  kor_name,
  COUNT(tp.id) AS pokemon_cnt
FROM(
SELECT
  id,
  trainer_id,
  pokemon_id,
  status
FROM basic.trainer_pokemon
WHERE
  status IN ("Active", "Training")
) AS tp
LEFT JOIN basic.pokemon AS p
ON tp.pokemon_id=p.id
GROUP BY
  kor_name
ORDER BY
   pokemon_cnt DESC
~~~

2
~~~
SELECT
  tp.*,
  p.type1
  COUNT(tp.id) AS pokemon_Cnt
FROM (
  SELECT
    id,
    trainer_id,
    pokemon_id,
    status
  FROM basic.trainer_pokemon
  WHERE
    status IN ("Active","Training")
) AS tp
LEFT JOIN basic.pokemon AS p
ON tp.pokemon_id=p.id
WHERE
  type1="Grass"
GROUP BY
  type1
ORDER BY
  2 DESC
~~~

3
~~~
SELECT
  COUNT(DISTINCT tp.trainer_id) AS trainer_uniq,
FROM basic.trainer_pokemon AS tp
LEFT JOIN basic.trainer AS t
ON t.id=tp.trainer_id
WHERE
  tp.location IS NOT NULL
  AND t.hometown = tp.location

-trainer엔 특정 트레이너의 정보가 1개 들어있음(1 row = 1 data)
-JOIN을 하다보면 RIGHT에서 LEFT의 기준에 여러개가 있을 때 데이터가 더 많아지는 것처럼 보임
-trainer_pokemon에 Goh가 6마리 포켓몬을 가지고 있어서 이렇게 결과가 합쳐진 것임
-LEFT에 메타 정보를 두면 헷갈릴 수 있음
-trainer 중에 포켓몬을 잡아보지 못한 trainer가 있으면 NULL 조건을 걸어줘야 함
~~~

4
~~~
SELECT
  type1,
  COUNT(tp.id) AS pokemon_Cnt
FROM(
  SELECT
    id,
    trainer_id,
    pokemon_id,
    status
  FROM basic.trainer_pokemon
  WHERE
    status IN ("Active","Training")
) AS tp
LEFT JOIN basic.pokemon AS p
ON tp.pokemon_id=p.id
LEFT JOIN basic.trainer AS t
ON tp.trainer_id=t.id
WHERE
  t.achievement_level="Master"
GROUP BY
  type1
ORDER BY
  2 DESC
LIMIT 1

-LEFT JOIN을 N번 연속으로 사용 가능하다
~~~



<br>

<br>

---

# 2️⃣ 확인문제 & 문제 인증

## 프로그래머스 문제 

https://school.programmers.co.kr/learn/courses/30/lessons/131533

> 상품 별 오프라인 매출 구하기

https://school.programmers.co.kr/learn/courses/30/lessons/133027

> 주문량이 많은 아이스크림들 조회하기

<img width="1710" height="1069" alt="image" src="https://github.com/user-attachments/assets/f1e9fab4-c2da-4920-84a8-dc83be4dc225" />
<img width="1710" height="1069" alt="image" src="https://github.com/user-attachments/assets/8ba28876-c358-488c-9dba-066988369e3b" />





---

# 3️⃣ 참고자료

JOIN 에 대해서 그림으로 쉽게 이해할 수 있는 자료들도 있어서 첨부합니다. 아래의 블로그도 학습할 때 같이 참고해주세요.

1. https://data-marketing-bk.tistory.com/entry/SQL-JOIN-%ED%95%9C-%EB%B0%A9%EC%97%90-%EC%A0%95%EB%A6%AC-%EA%B0%9C%EB%85%90%EB%B6%80%ED%84%B0-%EC%BD%94%EB%93%9C%EA%B9%8C%EC%A7%80-%EC%9D%B4%EA%B2%83%EB%A7%8C-%EB%B3%B4%EC%9E%90



2. https://velog.io/@wijoonwu/JOIN

<br>

### 🎉 수고하셨습니다.
