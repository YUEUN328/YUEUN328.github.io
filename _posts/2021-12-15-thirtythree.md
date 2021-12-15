---
layout: single
title: 33일차
categories: TIL
tag: SQL
author_profile: false
---

## TIL

- RR/MM/DD는 일반적으로 생각하는 연도, YY/MM/DD는 무조건 현재 세기 기준이다.
  - 80/12/15를 전자는 1980년, 후자는 2080년을 의미한다.
  
- 서브쿼리에서 세미콜론(;)은 맨 마지막에 한 번만 쓴다.

- SQL에서 드래그로 선택한 문장만 실행할 수 있다. 서브쿼리 문장만 테스트 해보는 데 유용하다!

- 다중행 서브쿼리: 서브쿼리의 결과가 행이 2개 이상인 경우

  - 한 개의 값과 단순 비교(=, !=, >, <, ...)를 할 수 없다.
  - in, any, all과 같은 키워드를 함께 사용한다.

- 서브쿼리에서 select 절의 컬럼이 2개면, where 절에서 비교할 컬럼도 2개다. 알아서 같은 것끼리 비교한다.

  ```sql
  where (deptno, sal) in ( 
      select deptno, max(sal) from emp 
      group by deptno
  );
  ```


- 다중행 서브쿼리에서 any와 all

  ```sql
  -- 서브쿼리 결과 전부보다 sal이 작아야 한다.
  select * from emp
  where sal < all (
      select sal from emp where deptno = 10 
  );
  
  -- 서브쿼리 결과 중 어떤 하나보다만 sal이 작으면 된다.
  select * from emp
  where sal < any (
      select sal from emp where deptno = 10 
  );
  ```


- select 절에서 그룹 합수와 그룹 함수가 아닌 게 섞여 있으면, 그룹 함수가 아닌 것은 반드시 group by 절에 있어야 한다.