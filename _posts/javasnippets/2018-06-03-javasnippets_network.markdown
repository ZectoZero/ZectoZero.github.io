---
layout:     post
title:      "Java Snippets - Network"
permalink:  /javasnippets/network
---

개발 시간이 부족할 때 사용할 수 있는, 수정이 쉬운 Java 코드 모음입니다.

<br/>

---
### **상황으로 찾기**
* TCP/IP
  * 간단한 TCP/IP Server
  * 간단한 TCP/IP Client

<br/>
<br/>

---
#### **간단한 TCP/IP Server**
* 종료 처리 하기 전까지 무한 반복하는 방식임

```
ServerSocket server = new ServerSocker([[서버 포트]]);

while (true) {
	Socket socket = server.accept();
	
	//----[ 데이터 받아서 처리하기 ]------------------------------
	
	InputStream       inputStream       = socket.getInputStream();
	InputStreamReader inputStreamReader = new InputStreamReader(inputStream);
	BufferedReader    bufferedReader    = new BufferedReader(inputStreamReader);
	
	String data   = "";
	char[] chars  = new char[256];
	int    length;
	while ((length = bufferedReader.read(chars)) != -1) {
		String newData = new String(chars, 0, length);
		
		// 새로 전송받은 데이터 (newData) 처리
		data += newData;
	}
	
	[[전송받은 전체 데이터 (data) 처리]]
	
	//----[ Client에게 데이터 보내기 ]----------------------------------------
	
	OutputStream       outputStream       = socket.getOutputStream();
	OutputStreamWriter outputStreamWriter = new OutputStreamWriter(outputStream);
	PrintWriter        printWriter        = new PrintWriter(outputStreamWriter);
	
	printWriter.print([[보낼 데이터]]);
	printWriter.flush();
	
	//----[ Client와의 연결 종료 ]----------------------------------------
	
	printWriter.close();
	outputStreamWriter.close();
	outputStream.close();
	
	bufferedReader.close();
	inputStreamReader.close();
	inputStream.close();
	
	socket.close();
	
	// 전송받은 전체 데이터가 종료 명령이면 break
}

server.close();
```

<br/>
<br/>

---
#### **간단한 TCP/IP Client**

```
Socket socket = new Socket("[[IP]]", [[Port]]);

//----[ Server에게 데이터 보내기 ]----------------------------------------

OutputStream       outputStream       = socket.getOutputStream();
OutputStreamWriter outputStreamWriter = new OutputStremWriter(outputStream);
PrintWriter        printWriter        = new PrintWriter(outputStreamWriter);

printWriter.print([[보낼 내용]]);
printWriter.flush();

//----[ Server가 보내는 값 받아서 처리하기 ]----------------------------------------

InputStream       inputStream       = socket.getInputStream();
InputStreamReader inputStreamReader = new InputStreamReader(inputStream);
BuffredReader     bufferedRedaer    = new BufferedReader(inputStreamReader);

String data   = "";
char[] chars  = new char[256];
int    length;
while ((length = bufferedReader.read(chars)) != -1) {
	String newData = new String(chars, 0, length);
	
	// 새로 전송받은 데이터 (newData) 처리
	data += newData;
}

[전송받은 전체 데이터 (data) 처리]]

//----[ Server와의 연결 종료 ]----------------------------------------

bufferedReader.close();
inputStreamReader.close();
inputStream.close();

printWriter.close();
outputStreamWriter.close();
outputStream.close();

socket.close();
```

<br/>
<br/>

