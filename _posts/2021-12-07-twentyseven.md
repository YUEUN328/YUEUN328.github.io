---
layout: single
title: 27일차
categories: TIL
tag: Java
author_profile: false
---

## TIL

- 익명 클래스는 부모 클래스나 인터페이스가 있어야 한다. 아무거나 만들 수 있는 게 아니다.

- textResult.setColumns(10);는 있어도 그만, 없어도 그만이다.

- 레이블, 텍스트 필드, 버튼은 멤버 변수로 선언하는 게 좋다. 지역 변수는 final로 선언해야 내부 클래스에서 접근 가능하기 때문이다. 다른 메서드에서 사용 안 하는 건 지역 변수로 놔둬도 된다.

- setText() 메서드는 파라미터가 String이다. 따라서 아래 두 줄로도 가능하다.

  - textResult.setText(Double.toString(result));

  - textResult.setText("" + result);

- ActionEvent를 처리할 수 있는 클래스가 ActionListener이다.

- 아래 두 가지 방식으로 같은지 다른지 비교 가능하다.

  - e.getSource() == btnMultiply 

  - e.getActionCommand().equals("x")

- 긴 문자열을 계속 나열할 땐 +보다 StringBuffer 객체 생성해서 append() 메서드를 이용하는 게 더 좋은 방법이다. 더 빠르다.

<br>

### swing

------

```java
double result = x + y;
textResult.setText(x + " + " + y + " = " + result);
```

setText() 메서드는 파라미터가 String이다. 따라서 아래 두 줄로도 가능하다. 다만 아래는 값만 나온다.

- textResult.setText(Double.toString(result));

- textResult.setText("" + result);

  <br>

```java
Object source = e.getSource();
String resultMessage = ""; 
if (source == btnMultiply) {
	resultMessage = x + " x " + y + " = " + (x * y);
} else if (source == btnDivide) {
	resultMessage = x + " / " + y + " = " + (x / y);
} 
```

아래 두 가지 방식으로 같은지 다른지 비교 가능하다.

- e.getSource() == btnMultiply  <- 위에서 사용한 방법

- e.getActionCommand().equals("x")

<br>

```java
//		String message = "이름: " + name + "\n"
//				+ "전화번호: " + phone + "\n"
//				+ "이메일: " + email;
		StringBuffer message = new StringBuffer(); // StringBuffer 객체 생성
		message.append("이름: ").append(name).append("\n")
			.append("전화번호: ").append(phone).append("\n")
			.append("이메일: ").append(email);
```

주석 처리한 부분과 아닌 부분은 같은 결과가 나온다. 긴 문자열을 계속 나열할 땐 +보다 StringBuffer 객체를 생성해서 append() 메서드를 이용하는 게 더 좋은 방법이다. 더 빠르다.