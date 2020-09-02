# Stack(스택)
제일 마지막에 저장한 데이터를 제일 먼저 꺼내는 후입선출(LIFO, Last Input First Out) 구조

## 구조
<img src="https://user-images.githubusercontent.com/46274903/91826239-43720d00-ec78-11ea-8708-532a6fc7ea77.PNG " height="400">

## 구현
### 1. 배열
**생성**
```java
public class InStack {
	private int max; // 스택 용량
	private int top; // 스택에 쌓여있는 데이터 수(포인터)
	private int[] stk; // 스택 본체
		
	public InStack(int capacity) {
		top = -1;	// 포인터 초기화
		max = capacity;
		try {
			stk = new int[max]; //용량 크기만큼 배열 생성
		}catch(OutOfMemoryError e) {
			max = 0;
		}
	}
}
```
**추가(push)**
```java
public void push(int x) {
	if(isFull()) {	// 스택이 가득 찼을때
		System.out.println("스택이 가득 찼습니다.");
	}else {
		top++;	// 포인터 증가
		stk[top] = x;	// 스택에 x 추가
		System.out.println("push : " + x);
	}
}
```
**빼기(pop)**
```java
public int pop() {
	if(isEmpty()) {	//스택이 비었을 때
		System.out.println("스택이 비어있습니다.");
		return -1;
	}else {	
		System.out.println("pop : " + stk[top]);
		return stk[top--];	// 포인터 감소
	}
}
```
**peek**
스택에서 top이 가리키는 데이터를 읽음
```java
public int peek() {
	if(isEmpty()) {	//스택이 비었을 때
		System.out.println("스택이 비어있습니다.");
	return -1;
	}else {
		System.out.println("peak : " + stk[top]);
		return stk[top];	// top에 있는 스택 값
	}
}
```
**검색**
```java
public int indexOf(int x) {
	for (int i = top; i >= 0; i--) { //top부터 bottom까지 반복
		if (stk[i] == x) {	// x값과 같다면 i 리턴
			return i;
		}
	}
	return -1;	// 검색 실패
}
```
- **스택이 비어있는지 검사**
```java
public boolean isEmpty() {
	return (top == -1);
}
```
- **스택이 가득 차있는지 검사**
```java
public boolean isFull() {
	return (top == max-1);
}
```
- **데이터 수 확인**
```java
public int size() {
	return top+1;
}
```
 **결과**
```java
public static void main(String[] args) {
	InStack num = new InStack(6);
		
	num.push(1);
	num.push(3);
	num.push(4);
	num.push(6);
	num.push(10);
	num.push(23);
	
	num.pop();

	System.out.println(num.indexOf(3));
	System.out.println(num.size());
}
```
```
push : 1
push : 3
push : 4
push : 6
push : 10
push : 23
pop : 23
1	// 3이 들어있는 인덱스
5	// 스택에 들어있는 데이터 수
```

### 2. 연결리스트
**생성**
```java
public class InStack {
	private Node top; // 포인터
	private int size = 0; //데이터 수

	private class Node {
		private Object data; // 노드 안의 값
		private Node next; // 다음 노드 정보
		public Node(Object input) {
			this.data = input;
			this.next = null;
	} // 초기화
}
```
**추가(push)**
```java
public void push(int x) {
	Node newNode = new Node(x); 
	newNode.next = top;	
	top = newNode;
	size++;
		
	System.out.println("push : " + x);
}
```
**빼기(pop)**
```java
public int pop() {
	if(isEmpty()) {	// 비었을 때
		System.out.println("스택이 비어있습니다.");
		return -1;
	}else {
		Node temp = top;
		top = top.next;
		Object returnData = temp.data;
		temp = null;
		System.out.println("pop : " + returnData);
		size--;
		return returnData;
	}
}
```
**peek**
스택에서 top이 가리키는 데이터를 읽음
```java
public int peek() {
	if(isEmpty()) {
		System.out.println("스택이 비어있습니다.");
		return -1;
	}else {
		System.out.println("peak : " + top.data);
		return top.data;
	}
}
```
- **스택이 비어있는지 검사**
```java
public boolean isEmpty() {
	return (top == -1);
}
```
- **데이터 수 확인**
```java
public int size() {
	return top+1;
}
```
