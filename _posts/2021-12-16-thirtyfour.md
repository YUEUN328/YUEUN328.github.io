---
layout: single
title: 34일차
categories: TIL
tag: SQL
author_profile: false
---

## TIL

- insert into ~ values는 행 하나씩만 insert, insert into ~ select는 여러 행을 insert할 수 있다. 후자를 이용하면 하나의 테이블을 다른 테이블로 간단히 복사할 수 있다.

- 테이블을 생성할 때 컬럼 정의와 제약 조건 정의를 구분하는 방식은  not null이라고 할 수 없다!

  ```sql
  name    varchar2(100) -- 100 byte
          constraint nn_ex02_name not null, 
              
  constraint nn_ex03_name check (name is not null), -- 주의: not null이라고 할 수 없음!            
  ```

- not null은 check 중 하나이다.
- delete/ truncate/ drop 비교
  - delete는 지우개로 지우는 것, rollback이 가능한 DML이다. 
  - truncate는 찢어버리는 것, rollback이 불가능한 DDL이다.
  - drop은 노트를 아예 쓰레기통에 버리는 것, rollback이 불가능한 DDL이다.