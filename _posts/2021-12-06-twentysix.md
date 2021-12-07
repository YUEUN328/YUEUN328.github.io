---
layout: single
title: 26일차
categories: TIL
tag: Java
author_profile: false
---

## TIL

- list, map은 앞으로도 많이 쓰니까 사용방법 숙지하자!

- Exception을 던질 수 있는 메서드는 try-catch로 묶어야 한다! 

- 이탤릭체는 static이다.

- ThreadMain02는 ThreadMain01과 달리 상속이 아니라 인터페이스를 구현한다. 자바는 다중상속이 안 돼서 클래스를 하나밖에 상속받지 못하니까, 이미 다른 클래스를 상속받았을 경우를 가정한 것이다.

- 멤버 변수는 파란색, 지역 변수는 갈색이다.

- 디자인 탭이 안 보일 땐, 파일 오른쪽 클릭 -> Open With -> WindowBuilder Editor

- 스윙은 레이아웃부터 바꾸고 시작하자! getContentPane() 누르고, 레이아웃을 (absolute)로 바꾸면 배치를 원하는대로 할 수 있다. 

- Add event handler -> action -> actionPerformed로 대부분 코드를 자동으로 해결 가능하다. 몇 번째 라인에 있는지 보여주고 이동시켜준다.

- 레이블, 텍스트 필드, 버튼은 모두 Ctrl+c, Ctrl+v 가능하다. 

<br>

### thread

------



```java
// ThreadMain01
class MyThread extends Thread {	
```

```java
// ThreadMain02
class MyRunnable implements Runnable {
```


