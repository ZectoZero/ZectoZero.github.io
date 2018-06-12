---
layout:     default
title:      "Java Snippets - Data Management"
permalink:  /javasnippets/data_management
---

개발 시간이 부족할 때 사용할 수 있는, 수정이 쉬운 Java 코드 모음입니다.

<br/>

---
### **상황으로 찾기**
* Array
  * Array 정렬 (int[], String[], ...)
  * Array 정렬 (Class 또는 특수 조건)
* List
  * List 정렬 (List\<Integer\>, List\<String\>, ...)
  * List 정렬 (Class 또는 특수 조건)
* Key & 1 Value (Map)
  * Map을 Key 순서로 정렬한 List 만들기
* Key & Value List
  * Key와 Value List로 이루어진 Map 만들기
* Key+Value Pair
  * KeyValuePair List의 Binary Search

<br/>
<br/>

---
#### **Array 정렬 (int[], String[], ...)**

```
Arrays.sort([[Array]]);
```

<br/>
<br/>

---
#### **Array 정렬 (Class 또는 특수 조건)**

```
Value[] values = [[values 생성]];
Arrays.sort(values, new Comparator<Value>() {
	@Override
	public int compare(Value value0, Value value1) {
		// return Integer.compareTo(value0.getInt(), value1.getInt());
	}
});
```

<br/>
<br/>

---
#### **List 정렬 (List\<Integer\>, List\<String\>, ...)**

```
Collections.sort([[List]]);
```

<br/>
<br/>

---
#### **List 정렬 (Class 또는 특수 조건)**

```
List<Value> values = [[values 생성]];
Collections.sort(values, new Comparator<Value>() {
	@Override
	public int compare(Value value0, Value value1) {
		// return Integer.compareTo(value0.getInt(), value1.getInt());
	}
});
```

<br/>
<br/>

---
#### **Key와 Value List로 이루어진 Map 만들기**

```
private Map<String, List<<[[Value]]>> valuesPerKey;
...

public void load() {

	valuesPerKey = new HashMap<>();
	...
	
	while ([[key와 value가 존재할 때]]) {
		[[key와 value 얻기]]
		List<[[Value]]> values = valuesPerKey.get(key);
		if (values == null) {
			values = new ArrayList<>();
			valuesPerKey.put(key, values);
		}
		values.add(value);
	}
	
	...
}
```

<br/>
<br/>

---
#### **Map을 Key 순서로 정렬한 List 만들기**

```
Map<String, [[Value]]> map = ...;
List<[[KeyValuePairDTO]]> pairs = new ArrayList<>();
String[] keys = map.keySet().toArray(new String[0]);
Arrays.sort(keys);
for (String keyx: keys)
	pairs.add(new [[KeyValuePairDTO]](keyx, ([[Value]])map.get(keyx)));
```

<br/>
<br/>

---
#### **KeyValuePair List의 Binary Search**
* Collections의 Binary Search를 사용하려면 KeyValuePair List는 반드시 먼저 정렬되어 있어야 함

```
// Collections의 Binary Search를 사용하려면 KeyValuePair List는 반드시 먼저 정렬되어 있어야 함
List<[[KeyValuePairDTO]]> values = ...;

int index = Collections.binarySearch(values, new [[KeyValuePairDTO]](code), new Comparator<[[KeyValuePairDTO]]>() {
	@Override
	public int compare([[KeyValuePairDTO]] v1, [[KeyValuePairDTO]] v2) {
		return v1.getKey().compareTo(v2.getKey());
	}
});

if (index >= 0) {
	[[KeyValuePairDTO]] value = values.get(index);
	...
} else {
	...
}
```

<br/>
<br/>

