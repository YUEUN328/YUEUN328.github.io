---
layout: single
title: 28일차
categories: TIL
tag: Java
author_profile: false
---

## TIL

- textField는 한 줄밖에 출력이 안 돼서 줄바꿈이 안 되고, textArea는 줄바꿈이 가능하다.

- 변수 이름 바꿀 때도 Refactor -> Rename을 이용하면 한꺼번에 다 바꿔준다.

- deprecated가 뜨는 건 자바가 업데이트 되면 사라질 수도 있으므로 다른 걸 쓰는 걸 권장한다.

- 파라미터 char[]인 append() 메서드가 있으므로 for 문을 직접 안 만들고 바로 읽어줄 수 있다. 

- id.equals("")로 하는 이유는 id가 String이므로 ==가 아니라 equals()로 비교해야 한다. 잊지 말자!

- UI 만들 때 가장 부모는 Component이다.

- 파라미터로 뭘 넣을지 모르겠을 땐 기본타입이면 0, 참조타입이면 null을 넣어보자.

- YES와 NO의 순서를 바꾸고 싶으면 showOptionDialog를 사용하자.

- 다이얼로그나 프레임 만들 때 메인은 지우자.

- ButtonGroup으로 묶으면 단 하나만 선택 가능하다. 그룹을 안 묶으면 다중선택이 가능하다.

- selected를 true로 하면 처음부터 선택된 상태로 실행된다.

- $ 은 내부 클래스라는 뜻이다.

<br>

### swing

------

```java
private void showIdPassword() {
		String id = textId.getText();		
//		String pw = passwordField.getText();
		// -> JPasswordfield 클래스의 getText 메서드는 deprecated(더이상 사용을 권장하지 않는) 메서드
		// -> 더이상 오류 수정을 하지 않고, Java 버전이 업그레이드될 때 사라질 수 있는 메서드
		// -> getText 대신에 getPassword 메서드를 사용하기를 권장
//		String result = "ID: " + id + "\n + "PW: " + pw;
		char[] pw = passwordField.getPassword();
		
		if (id.equals("")) {
			JOptionPane.showMessageDialog(frame, "아이디 입력 안 됨.");
		}
		if (pw.length == 0) {
			JOptionPane.showMessageDialog(frame, "비밀번호 입력 안 됨.");
		}
		
		StringBuffer result = new StringBuffer();
		result.append("ID: ").append(id).append("\n")
			.append("PW: ").append(pw);

		textArea.setText(result.toString());
	}
```

파라미터 char[]인 append() 메서드가 있으므로 for 문을 직접 안 만들고 바로 pw를 읽어줄 수 있다. 

if 문의 조건에 id.equals("")로 하는 이유는 id가 String이므로 ==가 아니라 equals()로 비교해야 한다. 잊지 말자!

<br>

```java
		StringBuffer buffer = new StringBuffer();
		
		// 라디오버튼들 중에서 선택된 상태
		if (rbPrivate.isSelected()) {
			buffer.append(rbPrivate.getText());
		} else if (rbPackage.isSelected()) {
			buffer.append(rbPackage.getText());
		} else if (rbProtected.isSelected()) {
			buffer.append(rbProtected.getText());
		} else if (rbPublic.isSelected()) {
			buffer.append(rbPublic.getText());
		}
		buffer.append(" 라디오버튼 선택.\n");
		
//		Enumeration<AbstractButton> elements = buttonGroup.getElements();
//		for (; elements.hasMoreElements();) {
//			AbstractButton btn = elements.nextElement();
//			if (btn.isSelected()) {
//				buffer.append(btn.getText()).append(" 라디오버튼 선택.\n");
//			}
//		}
```

주석 처리된 부분처럼 하면 if 문을 일일이 쓰지 않고 간단하게 할 수 있다. 좀 어려운 방법이긴 하다.
