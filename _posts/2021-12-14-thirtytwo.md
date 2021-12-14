---
layout: single
title: 32일차
categories: TIL
tag: SQL
author_profile: false
---

## TIL

- select와 from은 생략이 불가능하다.

- SQL도 from을 썼으면 Ctrl+Space하면 컬럼 이름을 보여준다.

- 레코드는 모든 컬럼을 뜻한다.

- 숫자, 날짜, 문자열 타입들은 모두 크기 (대/소) 비교가 가능하다.

- 날짜는 to_date('87/01/01', 'RR/MM/DD') 이런 형식이 제일 안전하다. 나라마다 날짜 표기가 다르기 때문에.
  - 연/월/일, 월/일/연(미국식), 일/월/연(영국식)

- 특정 문자(열)로 시작 또는 포함하는 단어를 검색할 땐 = 연산자가 아니라 like를 쓴다.

- select, group by, order by는 쉼표(,)로 컬럼 이름을 구분한다.

- and나 or가 하나만 있으면 괄호를 안 써도 되지만, and와 or를 섞어 쓸 땐 괄호를 써라.

- NULLABLE이 Yes면 null이 가능하고, No면 불가능하다.

- select와 from을 맞춰주기 위한 가상 테이블 이름이 dual이다.
  - 예) select (14000 * 12) * (1 + 0.4) from dual;

- 단일 행 함수는 하나가 들어가서 하나가 나오고, 그룹 함수(다중 행 함수)는 여러 개가 들어가서 하나가 나온다.

- select 절에서 만든 별명은 where, group by, having에서는 사용할 수 없고, order by에서만 사용 가능하다!
  - 실행 순서: 1. from, 2. where, 3. group by, 4. having, 5. select, 6. order by

- SELECT 구문 순서
  - select 컬럼, ...
  - from 테이블
  - where (그룹을 묶기 전에 검사할) 조건식
  - group by 그룹을 묶어줄 컬럼, ...
  - having 그룹을 묶은 다음에 검사할 조건식
  - order by 출력 순서를 설정할 컬럼, ...;