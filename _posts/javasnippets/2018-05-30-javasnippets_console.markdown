---
layout:     default
title:      "Java Snippets - Console"
permalink:  /javasnippets/console
---

개발 시간이 부족할 때 사용할 수 있는, 수정이 쉬운 Java 코드 모음입니다.

<br/>

---
### **상황으로 찾기**
* 입력 받기
  * 사용자에게서 1개의 값 입력 받기
  * 사용자에게서 계속 값 입력 받기

<br/>
<br/>

---
#### **사용자에게서 1개의 값 입력 받기**

```
Scanner scanner = new Scanner(System.in);

// 값 입력 전에 Console에 표시할 내용. println()이 아니고 print()임.
System.out.print("Value: ");

// 값 받기
String value = scanner.nextLine();

scanner.close();

[[값 처리]]
```

<br/>
<br/>

---
#### **사용자에게서 계속 값 입력 받기**

```
Scanner scanner = new Scanner(System.in);
		
while (true) {
	// 값 입력 전에 Console에 표시할 내용. println()이 아니고 print()임.
	System.out.println("Value: ");
			
	// 값 받기
	String value = scanner.nextLine();
			
	// 종료 문자면 break
	if ("q".equals(value)) break;
			
	[[값 처리]]
}
		
scanner.close();
```

<br/>
<br/>
