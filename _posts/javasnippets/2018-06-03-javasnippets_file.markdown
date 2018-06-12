---
layout:     post
title:      "Java Snippets - File"
permalink:  /javasnippets/file
---

개발 시간이 부족할 때 사용할 수 있는, 수정이 쉬운 Java 코드 모음입니다.

<br/>

---
### **상황으로 찾기**
* 텍스트 방식
  * 읽기
    * 텍스트 파일 한 번에 모두 읽기 (Utility 타입)
    * 텍스트 파일 라인 단위로 읽어서 처리
  * 쓰기
    * 텍스트 파일 쓰기 (Utility 타입)
* 바이트 방식
  * 읽기
    * 파일의 특정 바이트로부터 특정 길이만큼 읽기
* 파일 관리
  * 폴더 내 파일 리스트 처리

<br/>
<br/>

---
#### **텍스트 파일 한 번에 모두 읽기 (Utility 타입)**
* 대용량 파일일 때는 메모리가 부족할 수 있으므로 '텍스트 파일 라인 단위로 읽어서 처리' 방식을 사용

```
public static String read(String filePath) throws IOException {

	StringBuilder  stringBuilder;
	FileReader     fileReader     = null;
	BufferedReader bufferedReader = null;
	try {
		stringBuilder  = new StringBuilder();
		fileReader     = new FileReader(filePath);
		bufferedReader = new BufferedReader(fileReader);
		String line;
		while ((line = bufferedReader.readLine()) != null)
			stringBuilder.append(line).append('\n');
		
	} finally {
		if (bufferedReader != null) try { bufferedReader.close(); } catch (Exception ex) { /* Do Nothing */ }
		if (fileReader     != null) try { fileReader    .close(); } catch (Exception ex) { /* Do Nothing */ }
	}
	
	return stringBuilder.toString();
}
```

<br/>
<br/>

---
#### **텍스트 파일 라인 단위로 읽어서 처리**

```
FileReader     fileReader     = null;
BufferedReader bufferedReader = null;
try {
	fileReader     = new FileReader(filePath);
	bufferedReader = new BufferedReader(fileReader);
	String line;
	while ((line = bufferedReader.readLine()) != null) {
		[[line 값 처리]]
	}
	
} finally {
	if (bufferedReader != null) try { bufferedReader.close(); } catch (Exception ex) { /* Do Nothing */ }
	if (fileReader     != null) try { fileReader    .close(); } catch (Exception ex) { /* Do Nothing */ }
}
```

<br/>
<br/>

---
#### **텍스트 파일 쓰기 (Utility 타입)**

```
public static void write(String filePath, String content) throws IOException {

	FileWriter     fileWriter     = null;
	BufferedWriter bufferedWriter = null;
	try {
		fileWriter     = new FileWriter(filePath);
		bufferedWriter = new BufferedWriter(fileWriter);
		bufferedWriter.write(content);
		
	} finally {
		if (bufferedReader != null) try { bufferedReader.close(); } catch (Exception ex) { /* Do Nothing */ }
		if (fileReader     != null) try { fileReader    .close(); } catch (Exception ex) { /* Do Nothing */ }
	}
} 
```

<br/>
<br/>

---
#### **폴더 내 파일 리스트 처리**

```
File folder = new File([[폴더 경로]]);
for (File filex: folder.listFiles()) {
	String fileName     = filex.getName();
	String absolutePath = filex.getAbsolutePath();
	[[파일 처리]]
}
```

<br/>
<br/>

---
#### **파일의 특정 바이트로부터 특정 길이만큼 읽기**
* offset 위치를 계산할 때는 New Line 문자 ('\n' or '\r\n')의 길이도 계산에 포함할 지 검토해야 함

```
public static byte[] readBytes(String filePath, int offset, int length) throws IOException {

	RandomAccessFile randomFile = null;
	try {
		randomFile = new RandomAccessFile(filePath, "r");
		randomFile.seek(offset);
		
		byte[] dataBytes = new byte[length];
		randomFile.readFully(dataBytes);
		
		return dataBytes;
		
	} finally {
		if (randomFile != null) try { randomFile.close(); } catch (Exception ex) { /* Do Nothing */ }
	}
}
```

<br/>
<br/>

