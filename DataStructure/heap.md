# heap (힙)
`부모의 값이 자식의 값보다 항상 크다(작다)` 는 조건을 만족하는 `완전 이진 트리`
- 최댓값이나 최솟값을 빠르게 찾아내도록 만들어진 구조
- 중복된 값을 허용

## 종류
<img src="https://user-images.githubusercontent.com/46274903/92221621-b4affb00-eed8-11ea-846b-d01affbbc8d1.PNG " width="600">

- max heap (최대힙) : 부모의 값 >= 자식의 값

- min heap (최소힙) : 부모의 값 <= 자식의 값

## 구현

    왼쪽 자식의 인덱스 = 부모 인덱스 * 2
    오른쪽 자식의 인덱스 = 부모 인덱스 * 2 + 1
    부모 인덱스 = 자식 인덱스 / 2

### 생성
#### 최대힙
```java
public class MaxHeap {
	private int max;	// 배열크기
	private int maxHeap[];	// heap 배열
	private int size = 0;	// 인덱스
	
	public MaxHeap(int capacity) {
		max = capacity;
		maxHeap = new int[max];
	}
}	
```
#### 최소힙
```java
public class MinHeap {
	private int max;
	private int minHeap[];
	private int size = 0;

	public MinHeap(int capacity) {
		max = capacity;
		minHeap = new int[max];
	}
}
```

### 삽입
1. 힙에 새로운 요소가 들어오면, 새로운 노드를 힙의 마지막 노드에 삽입
2.  힙의 성질에 맞게 부모 노드와 자식 노드를 교환

#### 최대힙
```java
public void insert(int data) {
	
	if(size == max) {
		System.out.println("heap이 가득 찼습니다.");
	}else {
		maxHeap[++size] = data;	// 인덱스를 증가시킨 후 data 삽입
		for(int i = size; i > 1; i = i / 2) {
			
			if(maxHeap[i/2] < maxHeap[i]) {	// 부모 값이 자식보다 작을 때
				swap(maxHeap,i,i/2);	// 부모와 자식 위치 변경
			}else {
				return;
			}
		}
	}
}	
```

#### 최소힙
```java
public void insert(int data) {

	if (size == max) {
		System.out.println("heap이 가득 찼습니다.");
	} else {
		minHeap[++size] = data;
		for (int i = size; i > 1; i = i / 2) {	
			if (minHeap[i / 2] > minHeap[i]) {	// 부모 값이 자식보다 클 때
				swap(minHeap, i, i / 2);	// 부모와 자식 위치 변경
			} else {
				return;
			}
		}
	}
}
```

### 제거
1. 루트 노드 삭제
2. 삭제된 루트 노드에 마지막 노드를 가져옴
3. 힙의 성질에 맞게 자식 노드와 부모 노드를 교환

#### 최대힙
```java
public int delete() {
	if (size == 0) {
		System.out.println("heap이 비어있습니다.");
		return 0;
	} else {
		// 최대값(삭제할 값)을 변수에 저장	
		int deleteData = maxHeap[1];
		// root(삭제할 값) 위치에 배열 마지막 노드 값을 가져온다.
		maxHeap[1] = maxHeap[size];
		// 마지막 노드 삭제 후 인덱스 감소
		maxHeap[size--] = 0;
		for (int i = 1; i * 2 <= size;) {
			if (maxHeap[i * 2] < maxHeap[i] && maxHeap[i * 2 + 1] < maxHeap[i]) {
			// 현재 노드의 값이 왼쪽 자식의 값과 오른쪽 자식의 값보다 클 때
				break;
			} else if (maxHeap[i * 2] < maxHeap[i * 2 + 1]) {
			//왼쪽 자식의 값보다 오른쪽 자식의 값이 클 때
				swap(maxHeap, i * 2 + 1, i);	// 오른쪽 자식노드와 위치 변경
				i = i * 2 + 1;
			} else {
			//오른쪽 자식의 값보다 왼쪽 자식의 값이 클 때
				swap(maxHeap, i * 2, i);	// 왼쪽 자식노드와 위치 변경
				i = i * 2;
			}
		}
		return deleteData;
	}
}
```

#### 최소힙
```java
public int delete() {
	if (size == 0) {
		System.out.println("heap이 비어있습니다.");
		return 0;
	} else {
		// 최솟값(삭제할 값)을 변수에 저장
		int deleteData = minHeap[1];
		
		// root(삭제할 값) 위치에 배열 마지막 노드 값을 가져온다.
		minHeap[1] = minHeap[size];
		// 마지막 노드 삭제 후 인덱스 감소
		minHeap[size--] = 0;

		for (int i = 1; i * 2 <= size;) {
			if (minHeap[i * 2] > minHeap[i] && minHeap[i * 2 + 1] > minHeap[i]) {
			// 현재 노드의 값이 왼쪽 자식노드의 값과 오른쪽 자식노드의 값보다 작을 때
				break;
			} else if (minHeap[i * 2] > minHeap[i * 2 + 1]) {
			//왼쪽 자식의 값보다 오른쪽 자식의 값이 작을 때
				if(minHeap[i*2+1]==0) {
				// 오른쪽 자식노드의 값이 0일 경우(삭제하기 위해 값 0을 넣어주었기 때문에 최소 값을 부모노드와 변경하면 0이 heap으로 들어오게 됌) 
					break;
				}
				swap(minHeap, i * 2 + 1, i);	// 오른쪽 자식노드와 위치 변경
				i = i * 2 + 1;
			} else {
			//오른쪽 자식의 값보다 왼쪽 자식의 값이 작을 때
				if(minHeap[i*2]==0) {
					break;
				}
				swap(minHeap, i * 2, i);	// 왼쪽 자식노드와 위치 변경
				i = i * 2;
			} 
		}
		
		return deleteData;
	}
}
```

### 결과
```java
public static void main(String[] args) {
	System.out.println("-------최대힙-------");
	MaxHeap maxNum = new MaxHeap(10);
		
	maxNum.insert(5);
	maxNum.insert(25);
	maxNum.insert(24);
	maxNum.insert(13);
	maxNum.insert(8);
	maxNum.insert(40);
	maxNum.insert(34);
	maxNum.insert(20);
	maxNum.insert(4);
	System.out.println(maxNum);
	
	System.out.println(maxNum.delete());
	System.out.println(maxNum);
	System.out.println();
		
	System.out.println("\n-------최소힙-------");
	MinHeap minNum = new MinHeap(10);
	
	minNum.insert(5);
	minNum.insert(25);
	minNum.insert(24);
	minNum.insert(13);
	minNum.insert(8);
	minNum.insert(40);
	minNum.insert(34);
	minNum.insert(20); 
	minNum.insert(4);
	System.out.println(minNum);
	
	System.out.println(minNum.delete());
	System.out.println(minNum);
	System.out.println(minNum.delete());
	System.out.println(minNum);
	System.out.println();
}
```
```
-------최대힙-------
[40, 20, 34, 13, 8, 24, 25, 5, 4]
40
[34, 20, 25, 13, 8, 24, 4, 5]


-------최소힙-------
[4, 5, 24, 8, 13, 40, 34, 25, 20]
4
[5, 8, 24, 20, 13, 40, 34, 25]
5
[8, 13, 24, 20, 25, 40, 34]
```

##### [참고자료]
[enter link description here](https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)
