# SQL_BASIC 3주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_3rd_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**3주차 과제는 문제 풀이를 중심으로**, 강의에서 제시된 예제 문제 중 **7 문제 이상을 선택하여 직접 풀어본 뒤**, 강의 영상의 풀이와 비교해 **틀린 부분, 맞은 부분, 새롭게 배운 개념**을 구체적으로 정리해주세요. (적어도 3문제는 정리해야 합니다.) 완성된 과제는 Gihub에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_3rd

### 섹션 3. 데이터 탐색 - 조건, 추출, 요약

### 2-6. 연습문제 1~3번

### 2-6. 연습문제 7~9번

### 2-6. 연습문제 10~12번

### 2-6. 연습문제 13~17번

### 2-7. 정리 

### 2-8. 새로운 집계함수



## 섹션 4. 쿼리 잘 작성하기, 쿼리 작성 템플릿 및 오류를 잘 디버깅하기

### 3-1. INTRO

### 3-2. SQL 쿼리 작성하는 흐름

### 3-3. 쿼리 작성 템플릿과 생산성 도구 



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | 🍽️         |
| 5주차 | 섹션 **4-4** ~ **4-9** | 🍽️         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리

## 2-6. 연습문제

~~~
✅ 학습 목표 :
* 연습문제(7문제 이상) 푼 것들 정리하기
~~~

1.
- 조건: type2가 없는
- 어떤 테이블?: pokemon
- 어떤 컬럼: 따로 없음. 포켓만 수만 남기면 됨.
- 어떻게 집계: 포켓몬의 수 => COUNT
- NULL은 IS 연산자 사용

~~~
SELECT
  COUNT(id) AS cnt
FROM basic.pokemon
WHERE
  type2 IS NULL
~~~
- 여러 조건 연결하고 싶으면 AND, () OR ()

2.
- 테이블: pokemon
- 조건: type2가 없는 포켓몬
- 칼럼: type1
- 집계: 포켓몬 수=>COUNT
- 정렬: type1의 포켓몬 수 내림차순

~~~
SELECT
  type1
  COUNT(id) AS pokemon_cnt
FROM basic.pokemon
WHERE
  type2 IS NULL
GROUP BY
  type1
ODER BY
  pokemon_cnt DESC
~~~
- 집계 함수는 GROUP BY와 같이 다님. 집계하는 기준이 없으면 COUNT만 쓸 수 있으나, 집계하는 기준 칼럼이 있다면 GROUP BY에 써줘야함.

3.
- 테이블: pokemon
- 조건: type2 상관없이? 조건인가?
- 컬럼: type1
- 집계: 포켓몬 수=>COUNT

~~~
SELECT
  type1,
  COUNT(id) AS pokemon_cnt
FROM basic.pokemon
GROUP BY
  type1
~~~
- id를 설계할 때, 중복이 없게 설계해서 COUNT(id)=COUNT(DISTINCT id)

4.
- 테이블: pokemon
- 조건: 전설 여부 => 컬럼
- 컬럼: 전설(is_legendary)
- 집계: 포켓몬 수

~~~
SELECT
  is_legendary,
  COUNT(id) AS pokemon_cnt
FROM basic.pokemon
GROUP BY
  is_legendary
~~~

5.
- 테이블: trainer
- 조건: 같은 이름이 2개 이상(동명이인)
- 컬럼: 이름
- 집계: COUNT

~~~
SELECT
  name,
  COUNT(name) AS trainer_cnt
FROM basic.trainer
GROUP BY
  name
HAVING
  trainer_cnt>=2
~~~
- 집계 후 조건 => HAVING, FROM 절의 테이블 조건 => WHERE

6.
- 테이블: trainer
- 조건: 트레이너 이름 = "Iris"
- 컬럼: 정보=>모든 컬럼
- 집계: X

~~~
SELECT
  *
FROM basic.trainer
WEHRE
  name = "Iris"
~~~

7.
- 테이블: trainer
- 조건: 이름 = "Iris","Whitney","Cynthia" 중에 있으면 추출
- 컬럼: 정보->*
- 집계: 없음

~~~
SELECT
  *
FROM basic.trainer
WHERE
  name = IN("Iris","Cynthia","Whitney")
~~~
- IN => name에 괄호 안의 Value가 있는 Row만 추출. OR로 연결하면 너무 기니까 사용.

8.
- 테이블: pokemon
- 조건: x
- 컬럼:
- 집계: 포켓몬 수

~~~
SELECT
  count(id) AS pokemon_cnt
FROM basic.pokemon
~~~

9.
- 테이블: pokemon
- 조건: x
- 컬럼: 세대(generation)
- 집계: 포켓몬 수

~~~
SELECT
  generation,
  COUNT(id) AS pokemon_cnt
FROM basic.pokemon
GROUP BY
  generation
~~~

10.
- 테이블: pokemon
- 조건: type2 IS NOT NULL
- 컬럼: x
- 집계: 포켓몬 수=>COUNT

~~~
SELECT
  *
FROM basic.pokemon
WHERE
  type2 IS NOT NULL
~~~

11.
- 테이블: pokemon
- 조건: type2가 있는
- 컬럼: type1
- 집계: 제일 많은 COUNT

~~~
SELECT
  type1,
  COUNT(id) AS pokemon_cnt
FROM basic.pokemon
WEHRE
  type2 IS NOT NULL
GROUP BY
  type1
ORDER BY
  pokemon_cnt DESC
~~~

17.
- 테이블: trainer_pokemon
- 조건: 풀어준 포켓몬의 비율이 20% 넘어야함
- 컬럼: trainer_id
- 집계: COUNTIF(조건)
~~~
SELECT
  trainer_id,
  COUNTIF(status = "Released") AS released_cnt,
  COUNT(pokemon_id) AS pokemon_cnt,
  COUNTIF(status="Released")/COUNT(pokemon_id) AS released_ratio
FROM basic.trainer_pokemon
GROUP BY
  trainer_id
HAVING
  released_ratio>=0.2
~~~

## 2-8. 새로운 집계함수
 
~~~
✅ 학습 목표 :
* SQL 쿼리 구조를 이해할 수 있다. 
* SELECT, FROM, WHERE을 활용하는 방법을 설명할 수 있다. 
~~~

- 기존
~~~
SELECT
  FirstName AS first_name,
  LastName AS last_name,
  SUM(PointsScored) AS total_points
FROM PlayerStats
GROUP BY
  first_name,
  last_name
~~~

- 신규
~~~
SELECT
  FirstName AS first_name,
  LastName AS last_name,
  SUM(PointsScored) AS total_points
FROM PlayerStats
GROUP BY ALL
~~~
-컬럼 명시 없이 가능


## 3-2. 쿼리를 작성하는 흐름

~~~
✅ 학습 목표 :
* 쿼리를 작성하는 흐름을 설명할 수 있다.
~~~

- 지표 고민: 어떤 문제를 해결하기 위해 데이터가 필요한가?
- 지표 구체화: 추상적이지 않고 구체적인 지표 명시(분자, 분모 표시)
- 지표 탐색: 유사한 문제를 해결한 케이스가 있나 확인 if 존재? 해당 쿼리 리뷰
- 쿼리 작성: 데이터가 있는 테이블 찾기 if 2개 이상? 연결 방법 고민(JOIN)
- 데이터 정합성 확인: 예상한 결과와 동일한지 확인
- 쿼리 가독성: 나중을 위해 깔끔하게 쿼리 작성
- 쿼리 저장: 쿼리는 재사용되므로 문서로 저장

## 3-3. 쿼리 작성 템플릿과 생산성 도구

~~~
✅ 학습 목표 :
* 생산성 도구를 만들 수 있다.
~~~

<!-- 이어질 주차에서 생산성 도구를 활용한 실습이 있습니다.강의에 맞게 제작하여 화면을 캡쳐하여 이 주석을 지우고 올려주세요. -->



<br>
<br>

---

# 2️⃣ 학습 인증란

<img width="403" height="814" alt="image" src="https://github.com/user-attachments/assets/574a85b8-9440-4d8d-baaf-1ef65d64f76a" />




<br><br>



---

# 3️⃣ 확인문제

## 문제 1

> **🧚Q. Q. 포켓몬 연구에 흥미를 느낀 혜인은 각 타입(type1)별 평균 공격력(attack)을 비교해보고 싶었습니다.**
>
> 그래서 다음과 같은 필요한 정보를 미리 정리해보았습니다. 

~~~
조건 : attack이 50 이상인 포켓몬만 포함
보고 싶은 컬럼 : type1
집계 내용 : 각 type1 별 평균 공격력
정렬 기준 : 평균 공격력을 기준으로 내림차순 정렬
~~~

> **이 목표를 바탕으로 혜인은 아래와 같은 쿼리를 작성했지만, 일부 SQL 문법 요소를 빼먹었습니다. 비어 있는 부분인 ㄱ, ㄴ, ㄷ, ㄹ 에 들어갈 알맞은 SQL 구문을 채워보세요:**

~~~sql
SELECT type1, (ㄱ)
FROM pokemon
(ㄴ) attack >= 50
(ㄷ) type1
ORDER BY (ㄱ) (ㄹ);
~~~



~~~
SELECT
  type1,
  AVG(attack) AS avg_attack
FROM basic.pokemon
WHERE attack >= 50
GROUP BY type1
ORDER BY avg_attack DESC;
~~~



### 🎉 수고하셨습니다.
