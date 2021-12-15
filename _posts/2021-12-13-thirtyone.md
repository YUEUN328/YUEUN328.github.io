---
layout: single
title: 31일차
categories: TIL
tag: SQL
author_profile: false
---

## TIL

- Row(행) = Observation = Records = Examples 

- Column(열) = Variables = Fields = Attributes

- 깃허브 Raw에서 마우스 오른쪽 클릭해서 '다른 이름으로 링크 저장하기'를 누르면 파일을 저장할 수 있다.

- 1. 명령어는 대문자로, 테이블 이름과 컬럼 이름은 소문자로 쓰는 방법
  
  2. 전부 소문자로 쓰는 방법
  
  3. 명령어는 소문자로, 테이블 이름과 컬럼 이름은 대문자로 쓰는 방법이 있다.
  
     ```sql
     SELECT deptno, dname FROM dept; -- 1
     select deptno, dname from dept; -- 2
     select DEPTNO, DNAME from DEPT; -- 3
     ```
  
- select와 from은 두 줄로 많이 나눠쓴다.

- SQL에서 문자열은 작은따옴표('')를 사용한다. 별명만 큰따옴표("")를 쓴다. 단, 별명에 공백이 없는 경우에는 큰따옴표를 생략 가능하다.

- 테이블에 저장된 데이터(문자열)는 대/소문자를 구분한다.

- SQL에서는 문자열도 = 연산자로 비교한다.

- \>= A and <= B는 between A and B로 쓸 수 있다.

  ```sql
  where sal >= 2000 and sal <= 3000
  
  where sal between 2000 and 3000
  ```

- or 대신 in ( , , ...)을 쓸 수 있는데, 단 비교 대상이 같아야 한다.

  ```sql
  where deptno = 10 or deptno = 20
  
  where deptno in (10, 20)
  ```