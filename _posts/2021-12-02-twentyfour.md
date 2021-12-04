---
layout: single
title: 24일차
categories: TIL
tag: Java
author_profile: false
---

## TIL

- 패키지 이름은 전부 소문자이다.

- File 객체와 실제 파일은 다르다.

- try-with-resource 구문은 close할 필요가 없고, try-catch 구문은 마지막 Stream만 finally 블록에서  닫으면 된다.

- 지역 변수와 멤버 변수의 이름은 같아도 된다.

<br>

### 연락처 프로그램 ver 0.4

------



```java
package edu.java.contact.fileutil;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.util.ArrayList;
import java.util.List;

import edu.java.contact.model.Contact;

public class ContactFileUtil {
	// 상수(constant variable) 정의 - 데이터 폴더 이름, 데이터 파일 이름
	public static final String DATA_DIR = "data"; // 데이터 폴더 이름
	public static final String DATA_FILE = "contacts.dat"; // 데이터 파일 이름

	// 생성자를 private으로 선언하고 모든 메서드를 static으로 만듦
	private ContactFileUtil() {}

	/**
	 * 연락처 데이터 파일을 저장하는 폴더가 없으면 생성하고 File 객체를 리턴.
	 * 
	 * @return 데이터 폴더를 관리하는 File 객체.
	 */
	public static File initializeDataDir() {
		File dataDir = new File(DATA_DIR); // 상대 경로를 사용해서 File 객체 생성
		
		if (!dataDir.exists()) { // 데이터 폴더가 만들어져 있지 않으면			
			boolean result = dataDir.mkdir(); // 폴더 만듦
			if (result) {
				System.out.println("데이터 폴더 생성 성공");
			} else {
				System.out.println("데이터 폴더 생성 실패");
			}
		} else {
			System.out.println("이미 데이터 폴더가 만들어져 있습니다...");
		}
		
		return dataDir;
	}

	/**
	 * 파라미터에 전달된 File 객체를 사용해서 데이터 파일에 저장된 연락처 정보를 읽어서,
	 * 연락처 정보를 List 객체로 리턴. 
	 * 
	 * @param file 연락처 데이터가 저장된 파일을 관리하는 File 객체.
	 * @return 파일에서 읽은 데이터. ArrayList<Contact> 타입 객체.
	 */
	public static List<Contact> readDataFromFile(File file) {
		List<Contact> list = null; // 리턴할 리스트
		
		FileInputStream in = null;
		BufferedInputStream bin = null;
		ObjectInputStream oin = null;
		try {
			in = new FileInputStream(file);
			bin = new BufferedInputStream(in);
			oin = new ObjectInputStream(bin);
			
			list = (ArrayList<Contact>) oin.readObject();
			
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			try {
				oin.close(); // OIS을 close -> BIS이 close됨 -> FIS도 close됨
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
		
		return list;		
	}
	
	/**
	 * 파라미터에 전달된 data를 file에 씀(write).
	 * 
	 * @param data 파일에 쓸 데이터. Contact 타입을 저장하는 ArrayList.
	 * @param file 데이터 파일을 관리하는 File 객체.
	 */
	public static void writeDataToFile(List<Contact> data, File file) {
		try (FileOutputStream out = new FileOutputStream(file);
				BufferedOutputStream bout = new BufferedOutputStream(out);
				ObjectOutputStream oout = new ObjectOutputStream(bout);) {
			
			oout.writeObject(data);
			
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
	
	/**
	 * 연락처 데이터를 저장하고 있는 파일(data\contacts.dat)이 있는지 없는지 체크해서, 
	 * 데이터 파일이 있으면 파일에서 ArrayList를 읽어서 리턴하고, 
	 * 데이터 파일이 없으면 빈(empty) 리스트(ArrayList)를 생성해서 리턴.
	 * 
	 * @return Contact 객체를 저장하는 ArrayList.
	 */
	public static List<Contact> initializeData() {
		List<Contact> list = null; // 리턴할 리스트
		
		// 데이터 파일(data\contacts.dat)을 관리하는 File 객체를 생성
		File file = new File(DATA_DIR, DATA_FILE);
		if (file.exists()) { // 데이터 파일이 만들어져 있으면
			System.out.println("데이터 로딩 중...");
			list = readDataFromFile(file);
		} else { // 데이터 파일이 없으면
			System.out.println("새 데이터 생성 중...");
			list = new ArrayList<Contact>();
		}
		
		return list;
	}
	
}
```

readDataFromFile 메서드는  try-catch 구문을 이용했고,  writeDataToFile 메서드는 try-with-resource 구문을 이용해서 만들었다. try-with-resource 구문은 close할 필요가 없고, try-catch 구문은 마지막 Stream만 finally 블록에서  닫으면 된다. 따라서 전자가 더 편리하다.

```java
package edu.java.contact.ver04;

import java.io.File;
import java.util.ArrayList;
import java.util.List;

//import edu.java.contact.fileutil.ContactFileUtil;
import edu.java.contact.model.Contact;

import static edu.java.contact.fileutil.ContactFileUtil.*; // 모든 static 멤버(변수, 메서드)를 import

public class ContactDaoImpl implements ContactDao {
	// field(멤버 변수)
	private List<Contact> contacts; // 연락처 정보를 저장할 리스트
	private File dataFile; // 연락처 정보 리스트를 저장할 파일
	private File dataDir; // 연락처 데이터 파일을 가지고 있는 폴더

	// singleton
	private static ContactDaoImpl instance = null;

	private ContactDaoImpl() {
		// 연락처 정보 리스트를 저장하는 파일 관리 객체 생성
		dataFile = new File(DATA_DIR, DATA_FILE);

		// 현재 작업 디렉토리(CWD)에 (data 폴더가 없으면) data 폴더를 생성
		dataDir = initializeDataDir();

		// data 폴더에 있는 contacts.dat 파일을 읽어서 필드 contacts를 초기화
		contacts = initializeData();
	}

	public static ContactDaoImpl getInstance() {
		if (instance == null) {
			instance = new ContactDaoImpl();
		}
		return instance;
	}

	@Override
	public List<Contact> select() {
		return contacts;
	}

	@Override
	public Contact select(int index) {
		Contact result = null;
		if (index >= 0 && index < contacts.size()) { // 파라미터 index가 리스트의 인덱스 범위 안에 있으면
			result = contacts.get(index);
		}

		return result;
	}

	@Override
	public int insert(Contact c) {
		contacts.add(c); // ArrayList가 변경됨
		writeDataToFile(contacts, dataFile); // 파일에 변경된 ArrayList를 씀(write)

		return 1;
	}

	@Override
	public int update(int index, Contact contact) {
		int result = 0;
		if (index >= 0 && index < contacts.size()) { // 파라미터 index가 배열의 인덱스 범위 안에 있으면
			contacts.set(index, contact);
//			contacts.get(index).setName(contact.getName());
//			contacts.get(index).setPhone(contact.getPhone());
//			contacts.get(index).setEmail(contact.getEmail());

			writeDataToFile(contacts, dataFile); // 파일에 변경된 ArrayList를 씀(write)

			result = 1;
		}

		return result;
	}

	@Override
	public int delete(int index) {
		int result = 0;
		if (index >= 0 && index < contacts.size()) {
			contacts.remove(index);

			writeDataToFile(contacts, dataFile); // 파일에 변경된 ArrayList를 씀(write)

			result = 1;
		}

		return result;
	}

}
```

ContactDao와 ContactMain04 파일은 이전 버전 그대로 사용할 수 있다.
