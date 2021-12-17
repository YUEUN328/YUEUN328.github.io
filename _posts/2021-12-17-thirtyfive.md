---
layout: single
title: 35일차
categories: TIL
tag: SQL
author_profile: false
---

## TIL

### SQL

------



- timestamp가 date보다 더 정밀하다. timestamp를 쓰면 자바랑 맞춰줄 수 있다.

- primary key 자동으로 넘버링하는 방법
  - 좌측 테이블 이름에 마우스 우클릭 -> 편집 -> ID열 -> 유형(<u>D</u>): 열 시퀀스 -> 확인
- default 값은 insert할 때만 자동으로 들어가는 거지, update할 때도 자동으로 들어가진 않는다.

### Java

------

-  SQL 문장을 실행시킬 수 있는 Statement 객체 생성
  - 완성된 SQL 문장을 사용할 때: createStatement() 메서드 사용 -> Statement 객체 생성
  - SQL 템플릿을 사용할 때: prepareStatement() 메서드 사용 -> PreparedStatement 객체
- SQL 실행, 결과 확인
  - select 문(DQL): executeQuery() 메서드 사용 -> 리턴 타입: ResultSet
  - insert, update, delete 문(DML): executeUpdate() 메서드 사용 -> 리턴 타입: int