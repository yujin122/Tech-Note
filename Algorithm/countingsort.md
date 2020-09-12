# 계수정렬 (Counting Sort)
숫자의 `빈도`를 카운트해서 정렬하는 알고리즘

- 특정 범위가 정해져 있을 때 사용

#### 장점

> 정렬법 중에서 엄청 빠른 편에 속한다.
> 
> 안정적인 정렬이다.

#### 단점

> 추가적인 메모리가 필요
> 
> 일부 값 때문에 메모리의 낭비가 커질 수 있다. 
> ex) [1,3,5,20000,40000]

### 시간복잡도

> O(N)

### 구현

<img src="https://user-images.githubusercontent.com/46274903/92990042-b0f12980-f513-11ea-8cc8-4f5a7cc07662.PNG " width="600"  height="">

1. 정렬되지 않은 배열 값을 카운팅 배열에 인덱스로 지정하고 값을 +1 해준다
2. 배열이 끝날 때까지 반복
3. 카운팅 배열의 인덱스를 값만큼 반복해서 출력

```java
public static void counting_sort(int[] a) {
	int[] countingArray = new int[6];
	
	for(int i=0;i<a.length;i++) {
		countingArray[a[i]]++;
	}
	
	for (int i = 0; i < 6; i++) {
		for (int j = countingArray[i]; j > 0 && countingArray[j] != 0; j--) {
			System.out.print(i + " ");
		}
	}
}
```
### 결과
```java
public class CountingSort {
	public static void counting_sort(int[] a) {
		int[] countingArray = new int[6];
		
		for(int i=0;i<a.length;i++) {
			countingArray[a[i]]++;
		}
		
		for (int i = 0; i < 6; i++) {
			for (int j = countingArray[i]; j > 0 && countingArray[j] != 0; j--) {
				System.out.print(i + " ");
			}
		}
	}

	public static void main(String[] args) {
		int size;
		int num[];
		Scanner sc=new Scanner(System.in);
		
		System.out.print("배열 크기 : ");
		size = sc.nextInt();
		num = new int[size];
		
		System.out.println("1 ~ 5 사이의 수를 입력하세요.");
		
		for(int i=0;i<size;i++) {
			System.out.print("[" + i + "] : ");
			num[i]=sc.nextInt();
		}
		
		counting_sort(num);
	}

}
```
```
배열 크기 : 10
1 ~ 5 사이의 수를 입력하세요.
[0] : 2
[1] : 3
[2] : 0
[3] : 4
[4] : 5
[5] : 2
[6] : 1
[7] : 3
[8] : 5
[9] : 5
0 1 2 2 3 3 4 5 5 5 
```
