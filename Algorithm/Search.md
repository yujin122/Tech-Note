# Search Algorithm
1. 선형검색 : 무작위로 늘어놓은 데이터 모임에 사용
2. 이진검색 : 일정한 규칙을 가진 데이터 모임에 사용

## 선형검색(Linear Search)
원하는 키(key) 값을 갖는 요소를 만날 때까지 맨 앞부터 순서대로 요소를 검색

### 복잡도

> O(n)

### 구현
```java
public static int LinearSearch(int[] a, int s, int k) {
	int i = 0;
	
	while(true) {
		if(a[i] == k) {
			return i;
		}
		if(i == s-1) {
			return -1;
		}
		i++;
	}		
}
```
### 결과
```java
public class LinearSearch {
	public static int LinearSearch(int[] a, int s, int k) {
		int i = 0;

		while (true) {
			if (a[i] == k) {
				return i;
			}
			if (i == s - 1) {
				return -1;
			}
			i++;
		}
	}

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		System.out.print("배열 크기 : ");
		int size = sc.nextInt();

		int num[] = new int[size];

		System.out.println("---배열 값을 입력해주세요--- ");
		for (int i = 0; i < size; i++) {
			System.out.print("[" + i + "] : ");
			num[i] = sc.nextInt();
		}

		System.out.print("검색할 값을 입력해주세요 : ");
		int key = sc.nextInt();

		int idx = LinearSearch(num, size, key);

		if (idx == -1) {
			System.out.println("찾는 값이 없습니다.");
		} else {
			System.out.println(key + "는 [" + idx + "]에 있습니다.");
		}
	}
}
```
```
배열 크기 : 6
---배열 값을 입력해주세요--- 
[0] : 21
[1] : 30
[2] : 15
[3] : 9
[4] : 10
[5] : 6
검색할 값을 입력해주세요 : 10
10는 [4]에 있습니다.
```

## 이진검색(Binary Search)
데이터 집합의 중앙요소와 키(key) 값을 비교하여 키 값이 중앙값보다 작으면 좌측으로 이진검색 크면 우측으로 이진검색

- 오름차순 또는 내림차순으로 정렬된 배열에서 검색


<img src="https://user-images.githubusercontent.com/46274903/92437472-f941dc00-f1e1-11ea-8771-4c0d00985c96.PNG " width="700"  height="">

### 복잡도

    

> O(logN)

<img src="https://user-images.githubusercontent.com/46274903/92437923-db28ab80-f1e2-11ea-8758-18451293fd97.PNG " width=""  height="">

### 구현
```java
public static int BinarySearch(int[] a, int s, int k) {
	int mid;
	int left = 0;
	int right = s-1;
	
	mid=(left + right) / 2;
	
	while(left <= right) {
		mid=(left + right) / 2;
		if(a[mid] == k) {
			return mid;
		}else if(a[mid] > k) {
			right = mid-1;
		}else {
			left = mid+1;
		}
	}
	
	return -1;
}
```
### 결과
```java
public class BinarySearch {

	public static int BinarySearch(int[] a, int s, int k) {
		int mid;
		int left = 0;
		int right = s - 1;

		mid = (left + right) / 2;

		while (left <= right) {
			mid = (left + right) / 2;
			if (a[mid] == k) {
				return mid;
			} else if (a[mid] > k) {
				right = mid - 1;
			} else {
				left = mid + 1;
			}
		}

		return -1;
	}

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		System.out.print("배열 크기 : ");
		int size = sc.nextInt();

		int num[] = new int[size];

		System.out.println("---배열 값을 입력해주세요--- ");
		for (int i = 0; i < size; i++) {
			System.out.print("[" + i + "] : ");
			num[i] = sc.nextInt();
		}

		System.out.print("검색할 값을 입력해주세요 : ");
		int key = sc.nextInt();

		int idx = BinarySearch(num, size, key);

		if (idx == -1) {
			System.out.println("찾는 값이 없습니다.");
		} else {
			System.out.println(key + "는 [" + idx + "]에 있습니다.");
		}
	}

}
```
```
배열 크기 : 7
---배열 값을 입력해주세요--- 
[0] : 6
[1] : 13
[2] : 24
[3] : 32
[4] : 19
[5] : 27
[6] : 4
검색할 값을 입력해주세요 : 13
13는 [1]에 있습니다.
```
