---
layout:     default
title:      "Java Snippets - Thread"
permalink:  /javasnippets/thread
---

개발 시간이 부족할 때 사용할 수 있는, 수정이 쉬운 Java 코드 모음입니다.

<br/>

---
### **상황으로 찾기**
* 간단한 Thread 사용 
  * 간단한 Thread 사용
* Thread 관리 필요
  * 정해진 수의 Thread만 사용하는 ThreadPool
  * 최대 최소 Thread 수, 일정 시간 이상 노는 Thread는 자동으로 제거하는 ThreadPool
* 참고

<br/>
<br/>

---
#### **간단한 Thread 사용**

```
Runnable runnable = new Runnable() {
	@Override
	public void run() {
		try {
			String threadName = Thread.currentThread().getName();
			[[처리 로직]]
		} catch (IntrruptedException e) {
			e.printStackTrace();
		}
	}
};

Thread thread = new Thread(runnable);
thread.start();
```

<br/>
<br/>

---
#### **정해진 수의 Thread만 사용하는 ThreadPool**

```
ExecutorService threadPool = Executors.newFixedThreadPool(
	// CPU 코어의 수만큼 최대 Thread를 사용하는 ThreadPool을 생성
	Runtime.getRuntime().availableProcessors()
);

Future future = threadPool.submit(new Runnable() {
	@Override
	public void run() {
		[[처리 로직 또는 다른 메서드 호출]]
	}
});

future.get();

// 작업 큐에 대기하고 있는 모든 작업을 처리한 뒤에 ThreadPool을 종료
threadPool.shutdown();
```

<br/>
<br/>

---
#### **최대 최소 Thread 수, 일정 시간 이상 노는 Thread는 자동으로 제거하는 ThreadPool**

```
ExecutorService threadPool = Executors.newFixedThreadPool(
	3,									// 코어 Thread 개수
	100,								// 최대 Thread 개수
	120L,								// 놀고 있는 시간
	TimeUnit.SECONDS,					// 놀고 있는 시간 단위
	new SynchronousQueue<Runnable>()	// 작업 큐
);

Future future = threadPool.submit(new Runnable() {
	@Override
	public void run() {
		[[처리 로직 또는 다른 메서드 호출]]
	}
});

future.get();

// 작업 큐에 대기하고 있는 모든 작업을 처리한 뒤에 ThreadPool을 종료
threadPool.shutdown();
```

<br/>
<br/>

---
#### **참고**

* http://blog.eomdev.com/java/2016/04/06/Multi-Thread.html

<br/>
<br/>
