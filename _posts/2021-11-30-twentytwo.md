---
layout: single
title: 22일차
categories: TIL
tag: Java
author_profile: false
---

## TIL

- 한 패키지에 있는 파일을 다른 패키지로 Ctrl+c,  Ctrl+v 하면 파일 내에 패키지 선언문도 자동으로 바뀐다!😲
- 메서드 문서에 throws Exception이 써 있으면 반드시 try-catch 구문 안에 넣어야 한다!
- 파일 입/출력할 때 **class 클래스이름 implements Serializable** 잊지 말기! 
- 오류의 여지가 없는 코드는 바깥으로 빼고, try 블록 안에는 오류의 여지가 있는 코드만 남겨두는 것이 좋다.
- 문자열에 정수를 붙이면 문자열이다.
- 메서드 파라미터에 클래스 타입이 들어가면 객체를 생성(생성자 호출)하면 된다! 자꾸 잊어버린다.😂
- 면접 질문: 오버로딩과 오버라이딩
  - 오버로딩은 하나의 클래스 안에서 파라미터의 개수나 타입이 다를 때, 생성자나 메서드를 같은 이름으로 여러 개 정의하는 것이다. 
  - 오버라이딩은 상위 클래스가 가지고 있는 메서드를 하위 클래스에서 재정의하는 것이다. 오버라이드할 때는 메서드의 시그니처(리턴 타입, 이름, 파라미터)가 같아야 한다.


<br>

### 과제

------



```java
package edu.java.file08;

import java.io.Serializable;

public class Score implements Serializable {
	// field
	private int korean;
	private int english;
	private int math;	
	
	// constructor - 기본 생성자, 파라미터 3개(int, int, int)를 갖는 생성자 - overloading
	public Score() {}
	public Score(int korean, int english, int math) {
		this.korean = korean;
		this.english = english;
		this.math = math;
	}	
	
	// getters & setters
	public int getKorean() {
		return korean;
	}
	public void setKorean(int korean) {
		this.korean = korean;
	}
	public int getEnglish() {
		return english;
	}
	public void setEnglish(int english) {
		this.english = english;
	}
	public int getMath() {
		return math;
	}
	public void setMath(int math) {
		this.math = math;
	}	
	
	// toString 메서드 override
	@Override
	public String toString() {
		return "{korean=" + this.korean + ", english=" + this.english + ", math=" + this.math + "}";
	}

}
```

```java
package edu.java.file08;

import java.io.Serializable;

public class Student implements Serializable {
	// field
	private int id;
	private String name;
	private Score score;
	
	// constructor - 기본 생성자, 파라미터 3개(int, String, Score)를 갖는 생성자
	public Student() {}	
	public Student(int id, String name, Score score) {
		this.id = id;
		this.name = name;
		this.score = score;
	}

	// getters & setters	
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}	
	public String getName() {
		return name;
	}	
	public void setName(String name) {
		this.name = name;
	}	
	public Score getScore() {
		return score;
	}	
	public void setScore(Score score) {
		this.score = score;
	}
	
	// toString 메서드 override
	@Override
	public String toString() {
		return "Student{id=" + this.id + ", name=" + this.name + ", score=" + this.score + "}";
	}
	
}
```

toString 메서드에 this.score는 this.score.toString()라는 것과 마찬가지다.

```java
package edu.java.file08;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.util.ArrayList;
import java.util.Random;

public class FileMain08 {
	private static final String FILE_NAME = "data/student_list.dat";

	public static void main(String[] args) {
		Random rand = new Random();

		// 1: ArrayList<Student>를 생성
		// ArrayList에 Student 객체 5개를 추가
		// ArrayList를 파일에 write (Serialize, 직렬화)
		// ObjectOutputStream ==> BufferedOutputStream ==> FileOutputStream ==> 파일
		ArrayList<Student> list = new ArrayList<>();

		Score score1 = new Score(50, 50, 100);
		Student stu1 = new Student(1, "Aaa", score1);
		System.out.println(stu1);
		list.add(stu1);

		Student stu2 = new Student(2, "Bbb", new Score(100, 100, 50));
		System.out.println(stu2);
		list.add(stu2);

		for (int i = 0; i < 3; i++) {
			Score score = new Score(rand.nextInt(101), rand.nextInt(101), rand.nextInt(101));
			Student stu = new Student(rand.nextInt(100), "학생" + i, score);
			System.out.println(stu);
			list.add(stu);
		}

		try (FileOutputStream out = new FileOutputStream(FILE_NAME);
				BufferedOutputStream bout = new BufferedOutputStream(out);
				ObjectOutputStream oos = new ObjectOutputStream(bout);) {

			oos.writeObject(list);
			System.out.println("파일 생성 성공!");

		} catch (Exception e) {
			e.printStackTrace();
		}

		// 2: 1번에서 저장된 파일에서 객체를 read
		// 객체를 ArrayList로 타입 변환
		// ArrayList에 저장된 원소들을 모두 출력
		// ObjectInputStream <== BufferedInputStream <== FileInputStream <== 파일
		try (FileInputStream in = new FileInputStream(FILE_NAME);
				BufferedInputStream bin = new BufferedInputStream(in);
				ObjectInputStream ois = new ObjectInputStream(bin);) {

			ArrayList<Student> studentList = (ArrayList<Student>) ois.readObject(); // casting(강제 타입 변환)
			// -> 만약 타입 변환이 실패하면 예외(exception)이 발생하고, catch 구문에서 처리할 수 있음

//			Object obj = ois.readObject();
//			if (obj instanceof ArrayList<?>) {
//				ArrayList<Student> studentList = (ArrayList<Student>) obj;

//			System.out.println(studentList);
			System.out.println();
			for (Student s : studentList) {
				System.out.println(s);
			}

		} catch (Exception e) {
			e.printStackTrace();
		}

	}

}
```

문자열에 정수를 붙이면 문자열이다. 그래서 **"학생" + i**는 i까지 문자열이다. 

메서드 파라미터에 클래스 타입이 들어가면 객체를 생성(생성자 호출)하면 된다. 자꾸 잊어버린다!!

전의 코드들과 달리 ArrayList부터 for 문까지 try 바깥으로 뺐다. try 안에 oos.writeObject(list); 한 줄과 출력문뿐이다. 오류가 생길 여지가 없는 코드들은 바깥으로 빼고, try 안에는 오류가 생길 위험이 있는 코드만 남겨두는 것이 좋다.

