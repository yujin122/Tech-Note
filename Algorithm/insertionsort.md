# 삽입정렬(Insertion Sort)
선택한 원소를 그보다 더 앞쪽의 알맞은 위치에 `삽입`하는 알고리즘

#### 장점
> 
> 최선의 경우 시간복잡도가 O(N)이기 때문에 효율성이 좋다. 
> 
> 안정한 정렬 방법
> 
#### 단점
> 
> 최악의 경우 시간복잡도가 O(N<sup>2</sup>)이기 때문에 효율성이 나쁘다. 
> 
> 데이터 상태 및 데이터 크기에 따라서 성능 편차가 심하다.

### 시간복잡도

> O(N<sup>2</sup>)

### 구현
<img src="https://user-images.githubusercontent.com/46274903/92563035-e4347e00-f2b1-11ea-89c2-d98c31f945fc.PNG " width="600"  height="">

1. 두번째 배열 원소부터 순차적으로 선택하여 그 앞쪽의 배열과 대소 비교
2. 선택한 원소보다 클 경우 위치를 뒤로 이동시킨다, 이를 알맞은 위치를 찾을 때까지 반복
3. 알맞은 위치를 찾은 경우 선택된 원소를 삽입

```java
public static void insertion_sort(int[] a, int size) {
	int i,j,key;
	
	for(i=1;i<size;i++) {
		key = a[i];
		
		for(j=i-1;j>=0;j--) {
			if(a[j]>key) {
				a[j+1]=a[j];
			}else {
				break;
			}
		}
		
		a[j+1] = key;
	}
}
```

### 결과
```java
public class InsertionSort {
	public static void insertion_sort(int[] a, int size) {
		int i,j,key;
		
		for(i=1;i<size;i++) {
			key = a[i];
			
			for(j=i-1;j>=0;j--) {
				if(a[j]>key) {
					a[j+1]=a[j];
				}else {
					break;
				}
			}
			
			a[j+1] = key;
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

		insertion_sort(num, size);

		System.out.println("---삽입 정렬(insertion sort)---");

		String str = "[";
		for (int i = 0; i < size; i++) {
			if (i == size - 1) {
				str += num[i] + "]";
			} else {
				str += num[i] + ", ";
			}
		}

		System.out.println(str);

	}

}
```
```
배열 크기 : 8
---배열 값을 입력해주세요--- 
[0] : 12
[1] : 24
[2] : 10
[3] : 5
[4] : 26
[5] : 3
[6] : 9
[7] : 18
---삽입 정렬(insertion sort)---
[3, 5, 9, 10, 12, 18, 24, 26]
```

##### [참고자료]
1. [enter link description here](https://gmlwjd9405.github.io/2018/05/06/algorithm-insertion-sort.html)
