# Queue(큐)
가장 먼저 넣은 데이터를 가장 먼저 꺼내는 `선입선출(FIFO, First Input First Out)`구조

## 종류
1.  선형 큐 (배열, 리스트)
2.  원형 큐

## 선형 큐

### 구조
<img src="https://user-images.githubusercontent.com/46274903/91936518-f69b3e80-ed2a-11ea-943f-e6da28ae6ea9.PNG " height="500">

- front : 데이터를 꺼내는 쪽
- rear : 데이터를 넣는 쪽
- enqueue : 큐에 데이터를 넣는 작업
- dequeue: 큐에서 데이터를 꺼내는 작업 

### 배열 구현
**생성**
```java
public class ArrayQueue {
	private int max;	// 배열 크기
	private Object que[];	// 배열
	private int front;	// 맨 앞 배열
	private int rear;	// 값이 들어있는 마지막 배열
		
	public ArrayQueue(int capacity) {
		max = capacity;
		rear = 0;
		front = 0;
		que = new Object[capacity];
	}
}
```

**추가(enqueue)**
```java
public void enqueue(Object x) {
	if(isFull()) {
		System.out.println("큐가 가득 찼습니다.");
	} else {
		que[rear] = x;	// 끝에 x 추가		
		rear++;
		System.out.println("Insert Item : " + x);
	}
}
```

 - 배열 끝부분을 가리키는 rear에 값을 추가 후 rear 증가

**삭제(dequeue)**
```java
public void dequeue() {
	if(isEmpty()) {
		System.out.println("큐가 비어있습니다.");
	}else {
		Object item = que[front]; // 맨 앞에 있는 배열 값 item에 저장
		System.out.println("Deleted item : " + item);
		que[front++] = null;	//front 값 증가
	}
}
```

 - 배열의 맨 처음인 front가 가리키는 데이터를 꺼낸 후 front 값을 증가

**peek**
```java
public Object peek() {
	if(isEmpty()) {
		System.out.println("큐가 비어있습니다.");
		return 0;
	}else {
		return que[front];
	}	
}
```
**공백, 포화상태 확인**
```java
public boolean isEmpty() {	// 공백
	return (front == rear);
}

public boolean isFull() {	// 포화
	return (rear == max);
}
```
결과
```java
public static void main(String[] args) {
	ArrayQueue num = new ArrayQueue(8);
		
	num.enqueue(10);
	num.enqueue(20);
	num.enqueue(30);
	num.enqueue(40);		
	System.out.println(num);
	System.out.println();
		
	num.dequeue();
	num.dequeue();
	System.out.println(num);
	System.out.println();
	
	System.out.println(num.peek());
}
```
```
Insert Item : 10
Insert Item : 20
Insert Item : 30
Insert Item : 40
[10, 20, 30, 40]

Deleted item : 10
Deleted item : 20
[30, 40]

30	// peek
```
### 문제점

> front와 rear이 계속 증가하여 배열의 사이즈까지 도달하면 더이상 사용할 수 없게 된다.  

### 리스트 구현
**생성**
```java
public class ListQueue {

	private class Node {
		private Object data; // 노드 안의 값
		private Node next; // 다음 노드 정보

		public Node(Object input) {
			this.data = input;
			this.next = null;
		} 
		
		public String toString() {
			return String.valueOf(this.data);
		}
	}
	
	private Node front; // 시작 위치
	private Node rear; // 끝 위치
	private int size=0;
	
	public ListQueue() {
		this.front = null;
		this.rear = null;
	}
}
```

**추가(enqueue)**
```java
public void enqueue(int x) {
	Node newNode = new Node(x);
	if (isEmpty()) {
		front = newNode;
	}else {
		rear.next = newNode;
	}
	rear = newNode;
	size++;
	System.out.println("Inserted Item : " + x);
}
```
1. 새로운 노드(newNode) 생성 후 현재 rear이 가리키는 마지막 노드에 newNode 지정
2. 마지막 노드(rear)를 newNode로 갱신

**삭제(dequeue)**
```java
public void dequeue() {
	if(isEmpty()) {
		System.out.println("큐가 비어있습니다.");			
	}else {
		Node item = front;
		front = front.next;
		System.out.println("Deleted Item : " + item.data);
		item = null;
		size--;
	}
}
```
1. 노드 item에 현재 front가 가리키는 첫 노드 저장
2.  첫 노드(front)를 front의 다음 노드로 갱신
3.  첫 노드였던 item 삭제

**peek**
```java
public Object peek() {
	if(isEmpty()) {
		System.out.println("큐가 비어있습니다.");		
		return 0;
	}else {
		return front.data;
	}
}
```
**공백 상태 확인**
```java
public boolean isEmpty() {
	return (front == null);
}
```
**결과**
```java
public static void main(String[] args) {
	ListQueue num = new ListQueue();
		
	num.enqueue(50);
	num.enqueue(23);
	num.enqueue(20);
	num.enqueue(85);
	num.enqueue(48);
	System.out.println(num);
	System.out.println();
		
	num.dequeue();
	num.dequeue();
	System.out.println(num);
	System.out.println();
		
	System.out.println(num.peek());
}
```
```
Inserted Item : 50
Inserted Item : 23
Inserted Item : 20
Inserted Item : 85
Inserted Item : 48
[50, 23, 20, 85, 48]

Deleted Item : 50
Deleted Item : 23
[20, 85, 48]

20	//peek
```
### 장점

> 배열큐처럼 삭제한 공간을 낭비하지 않는다.

## Circular Queue(원형큐)
선형큐의 문제점을 보완하기 위한 자료구조, 처음과 끝이 이어져 있는 구조

### 구조
<img src="https://user-images.githubusercontent.com/46274903/91940336-40d3ee00-ed32-11ea-9fe7-33533a6b54eb.PNG " height="400">

- 공백상태와 포화상태를 알기 위해 front부분은 항상 비워둔다.
- `front == (rear+1)%QueueSize` 를 사용하여 공백상태인지 포화상태인지 구분한다.

### 구현
**생성**
```java
public class CircularQueue {
	private int max;	// 크기
	private Object cir[];	// 배열
	private int front;	// 시작 위치
	private int rear;	// 마지막 위치

	public CircularQueue(int x) {
		this.max = x;
		this.cir = new Object[this.max];
		this.front= 0;
		this.rear = 0;	
	}
}
```

**추가(enqueue)**
```java
public void enqueue(Object x) {
	if(front == (rear+1)%max) {
		System.out.println("큐가 가득 찼습니다.");
	}else {
		rear = (rear + 1) % max;
		cir[rear]=x;
			
		System.out.println("Inserted Item : " + x);
	}
}
```

**삭제(dequeue)**
```java
public void dequeue() {
	if(front == rear) {
		System.out.println("큐가 비어있습니다.");
	}else {
		front = (front+1)%max;
		System.out.println("Deleted Item : " + cir[front]);
	}
}
```

**peek**
```java
public Object peek() {
	if(front == rear) {
		System.out.println("큐가 비어있습니다.");
		return 0;
	}else {
		return cir[front+1];
	}
}
```

**결과**
```java
public static void main(String[] args) {
	CircularQueue num = new CircularQueue(8);
		
	num.enqueue(30);
	num.enqueue(50);
	num.enqueue(10);
	num.enqueue(70);
	num.enqueue(80);
	System.out.println(num);
	System.out.println();
		
	num.dequeue();
	num.dequeue();
	System.out.println(num);
		
	System.out.println(num.peek());
}
```
```
Inserted Item : 30
Inserted Item : 50
Inserted Item : 10
Inserted Item : 70
Inserted Item : 80
[30 50 10 70 80 ]

Deleted Item : 30
Deleted Item : 50
[10 70 80 ]
10	//peek
```
