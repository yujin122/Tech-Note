# 버블정렬(bubble sort)
서로 `인접한 두 원소`의 대소를 비교하여 교환하여 정렬하는 알고리즘


> **장점** 
> 구현이 매우 간단하다.
> 
> **단점**  
> 비효율적이다, 최악이든 최선이든 시간 복잡도가 O( N<sup>2</sup>)이다.

### 복잡도

    비교횟수 : (n-1), (n-2), (n-3), ... , 2, 1번으로 n(n-1)/2
    교환횟수 : 최악의 경우 비교횟수와 동일

**시간 복잡도**

> O( N<sup>2</sup>)

### 구현
1. 배열의 첫번째 원소와 두번째 원소를 비교하고 첫번째 원소가 클 경우 교환을 한다. 이런식으로 마지막 원소까지 비교 교환을 한다.

2.  1회전을 수행하면 가장 큰 원소가 맨 뒤로 이동하므로 2회전에서는 맨 끝 원소를 제외하고 수행한다. 이렇게 반복하여 정렬을 완성한다.

```java
public static void bubble_sort(int a[],int size) {
	int temp = 0;
	
	for(int i=size-1;i>0;i--) {
		
		for(int j=0;j<i;j++) {
			
			if(a[j]>a[j+1]) {
				temp = a[j];
				a[j] = a[j+1];
				a[j+1] = temp;
			}
		}
	}
}
```
### 결과
```java
public class BubbleSort {
	public static void bubble_sort(int a[],int size) {
		int temp = 0;
		
		for(int i=size-1;i>0;i--) {
			
			for(int j=0;j<i;j++) {
				
				if(a[j]>a[j+1]) {
					temp = a[j];
					a[j] = a[j+1];
					a[j+1] = temp;
				}
			}
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

		
		bubble_sort(num, size);

		System.out.println("---버블 정렬(bubble sort)---");
		
		
		String str= "[";
		for(int i = 0;i<size;i++) {
			if(i == size-1) {
				str+=num[i]+"]";
			}else {
				str+=num[i]+", ";
			}
		}
		
		System.out.println(str);

	}

}
```
```
배열 크기 : 8
---배열 값을 입력해주세요--- 
[0] : 3
[1] : 15
[2] : 24
[3] : 6
[4] : 13
[5] : 8
[6] : 10
[7] : 5
---버블 정렬(bubble sort)---
[3, 5, 6, 8, 10, 13, 15, 24]
```


##### [참고자료]
1. [enter link description here](https://gmlwjd9405.github.io/2018/05/06/algorithm-bubble-sort.html)
