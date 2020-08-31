# List (리스트)
 `순서`를 가지고 일렬로 나열한 구조

#### 종류
1. Array List

3. Linked List

# Array List (배열 리스트)
배열을 이용해서 리스트를 구현한 것

> 장점 : 배열과 같이 index를 이용하여 접근하기 때문에 조회가 빠르다.
> 
> 단점 : 데이터의 추가/삭제가 느리다.

## 구현
#### 생성
```java
ArrayList list = new ArrayList(); //타입 미설정
ArrayList<Integer> num = new ArrayList<>(); // 해당 자료형만 사용 가능
```
### 추가
```java
num.add(10);
num.add(20);
num.add(30);
num.add(40);	// add(val) 맨 뒤에 값 추가
		
num.add(1,15); // add(index, val), 해당 인덱스에 값 추가
```
![3](https://user-images.githubusercontent.com/46274903/91692908-2a4c5c00-eba5-11ea-9a21-3cd2fa9f0fc3.PNG)


- 값이 추가 될 경우 맨 뒤 element 부터 뒤로 한칸씩 이동 후 해당 index의 element에 값을 추가한다.

### 삭제
```java
num.remove(2); // remove(index), 해당 인덱스 값 삭제
```
![4](https://user-images.githubusercontent.com/46274903/91693348-daba6000-eba5-11ea-8f9d-40f0f52d4f78.PNG)

- 해당 index element 를 삭제 후 뒤에 있는 element를 앞으로 한칸씩 이동시킨다.

### 가져오기
```java
num.get(1); // get(index), 해당 인덱스 값 가져오기
```
### list 크기
```java
num.size();
```

### 결과
```
[10, 15, 30, 40] //ArrayList num
15			 //num.get(1)
4			 //num.size()	
```

# Linked List
각 노드가 데이터와 포인터를 가지고 한 줄로 연결시키면서 자료를 저장하는 구조

> 장점 : 데이터의 추가/삭제가 빠르다.
> 
> 단점 : 연결리스트를 처음부터 끝까지 순회해야돼서 조회가 느리다.

## 구조
![5](https://user-images.githubusercontent.com/46274903/91711822-87560b00-ebc1-11ea-852a-39ee9874edb5.PNG)

## 구현
### 생성
```java
LinkedList num = new LinkedList();
```
##### 클래스 
```java
public class LinkedList {
	private Node head; // 시작 위치
	private Node tail; // 끝 위치
	private int size = 0; // list 크기

	private class Node {
		private Object data; // data field, 노드 데이터
		private Node next; // Link field, 다음 노드 정보

		public Node(Object input) {  // 초기화
			this.data = input;
			this.next = null;
		}

		public String toString() {
			return String.valueOf(this.data);
		}
	}
}
```

### 추가
#### < 맨 앞에 추가 >
```java
num.addFirst(30);
num.addFirst(20);
num.addFirst(10);
```
![6](https://user-images.githubusercontent.com/46274903/91714025-d2721d00-ebc5-11ea-81ae-49d564e5fe0d.PNG)

1. 노드 생성
2.  새로운 노드에 HEAD가 가리키는 노드(20)를 지정
3.  HEAD에 새로운 노드 지정 

```java
public void addFirst(Object input) {
	Node newNode = new Node(input); //노드 생성
	newNode.next = head;			// 새 노드의 Linked field에 head(다음노드) 지정
	head = newNode; 				// 헤드에 새 노드 지정
	size++;							// list 크기
	if (head.next == null) {		// 노드가 하나일때
		tail = head;
	} 
}
```
### <맨 뒤에 추가>
```java
num.addLast(10);
num.addLast(20);
num.addLast(30);
```
![7](https://user-images.githubusercontent.com/46274903/91715149-16feb800-ebc8-11ea-82c8-3577707d88df.PNG)

1.  새로운 노드 생성
2.  TAIL이 가리키는 노드(30)의 다음 노드로 새로운 노드를 지정
3.  TAIL 노드에 마지막 노드 갱신  

```java
public void addLast(Object input) {
	Node newNode = new Node(input); //새 노드 생성
	if (size == 0) {				//첫 노드일 경우
		addFirst(input);
	} else {
		tail.next = newNode;	// 마지막 노드에 다음 노드로 새 노드 지정
		tail = newNode;			// 마지막 노드 갱신
		size++;
	}
}
```
### <특정한 위치에 노드 추가>
```java
num.add(2,25);
```
![8](https://user-images.githubusercontent.com/46274903/91716502-c76dbb80-ebca-11ea-9a6d-e4c9c349afdc.PNG)

1. temp1에 k번째 바로 전 노드를 지정
2. temp2에 k번째 노드 지정
3.  새로운 노드 생성
4.  temp1의 다음 노드로 새 노드를 지정
5.  새 노드 다음 노드로 temp2 지정

```java
public void add(int k, Object input) {
	if (k == 0) {			//첫 노드에 추가
		addFirst(input);
	} else {				
		Node temp1 = node(k - 1);	//temp1에 k번째 바로 전 노드를 지정
		Node temp2 = temp1.next;	//temp2에 k번째 노드 지정
		Node newNode = new Node(input); //새 노드 생성
		temp1.next = newNode;		//temp1의 다음 노드로 새 노드를 지정
		newNode.next = temp2;		//새 노드 다음 노드로 temp2 지정
		size++;
		if(newNode.next == null)	//다음 노드가 없을 때(마지막노드)
			tail = newNode;	
	}		
}
```

### 탐색
```java
Node node(int index) {
	Node x = head;	// head 노드 지정
	for (int i = 0; i < index; i++) {
		x = x.next;		
	}
	return x;
}
```

### 삭제
### <맨 앞 노드 삭제>
```java
num.removeFirst();
```
![9](https://user-images.githubusercontent.com/46274903/91717542-aa39ec80-ebcc-11ea-85b8-961153e6dbc4.PNG)

1. temp 에 head(첫번째 노드) 지정
2.  head에 두번째 노드 지정
3.  삭제될 값을 리턴하기 위해 임시 변수에 넣음

```java
public Object removeFirst() {
	Node temp = head;		// temp 에 head(첫번째 노드) 지정
	head = head.next;	// head에 두번째 노드 지정
	Object returnData = temp.data; // 삭제될 값을 리턴하기 위해 임시 변수에 넣음
	temp = null;	// 노드 삭제
	size--;
	
	return returnData;
}
```
### <특정한 위치에 있는 노드 삭제>
```java
num.remove(5);
```

```java
public Object remove(int k) {
	if(k == 0) {	
		return removeFirst();
	}else {
		Node temp = node(k-1);	// k번째 앞 노드의 값을 temp에 지정
		Node todoDeleted = temp.next; // k번째 노드를 todoDeleted에 넣음
		temp.next = temp.next.next;	// k번째 뒷 노드를 temp의 다음 노드로 지정
		Object returnData = todoDeleted.data;
		if(todoDeleted == tail) {	// 삭제하는 노드가 마지막 노드일 때
			tail = temp;	
		}
		todoDeleted = null;	// 노드 삭제
		size--;
		
		return returnData;
	}		
}
```

### 리스트 크기
```java
num.size();
```
```java
public int size() {
	return size;
}
```

### 가져오기
```java
num.get(2);
```
```java
public Object get(int k) {
	Node temp = node(k);
	return temp.data;
}
```
### 결과
```java
public static void main(String[] args) {

	LinkedList num = new LinkedList();
	num.addFirst(30);
	num.addFirst(20);
	num.addFirst(10);

	System.out.println(num);

	num.addLast(10);
	num.addLast(20);
	num.addLast(30);

	System.out.println(num);

	num.add(2, 25);

	System.out.println(num);

	num.removeFirst();
	num.remove(5);

	System.out.println(num);

	System.out.println("size : " + num.size());
	System.out.println("get(2) : " + num.get(2));
}
```

```
[10,20,30]
[10,20,30,10,20,30]
[10,20,25,30,10,20,30]
[20,25,30,10,20]
size : 5
get(2) : 30
```
