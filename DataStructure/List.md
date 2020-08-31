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

Linked List

