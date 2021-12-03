---
layout: single
title: 25일차
categories: TIL
tag: Java
author_profile: false
---

## TIL

- 지역 변수는 static을 못 붙인다. static은 멤버에만 붙일 수 있다(당연히 static은 main 메서드 시작 전에 이미 만들어져 있는 거니까).

- static은 static만 사용할 수 있다! 
  - static 메서드 안에서는 static이 아닌 멤버는 사용할 수 없다!
  - static (멤버) 내부 클래스는 외부 클래스의 static 멤버들만 접근이 가능하다! static이 아닌 멤버들은 사용할 수 없다!

- 인스턴스 메서드는 인스턴스 변수와 클래스 변수 둘 다 사용 가능하지만, 클래스 메서드(static 메서드)는 클래스 변수(static 변수)만 사용 가능하다.
- 인터페이스는 static, final을  못 붙인다.
- Functional interface인 경우에만 람다 표현식을 사용할 수 있다.

<br>

익명 클래스와 람다 표현식 어렵다... 이해는 가는데 내가 코드를 만들려면 잘 안 된다. 이건 연습만이 방법이겠지.😂