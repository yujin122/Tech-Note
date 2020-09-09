# 선택정렬(Selection Sort)  
현재 위치에 들어갈 값을 찾아 정렬하는 알고리즘  
  

#### 장점
>    
> 비교 횟수는 많지만 실제로 교환횟수는 적기 때문에 교환이 많이 일어나야 하는 배열에 유리하다.   
> 
> 구현이 단순하다. 
> 
#### 단점 
>   
> 시간복잡도가 O(N<sup>2</sup>) 이기 때문에 비효율적이다.  
> 
> 불안정한 정렬

  
### 복잡도  

    비교 횟수 : (n-1), (n-2), (n-3), ... , 2, 1번으로 n(n-1)/2  

**시간복잡도**  

> O(N<sup>2</sup>)

  
### 구현  
<img src="https://user-images.githubusercontent.com/46274903/92555831-8305ae00-f2a3-11ea-9ff1-8f7126aba369.PNG " width="600"  height="">


원소 중 `가장 작은 원소`를 아직 정렬하지 않은 부분의 `첫 번째 원소`와 `교환`
```java
public static void selection_sort(int[] a, int size) {
	for (int i = 0; i < size - 1; i++) {
		int min = i;
		for (int j = i + 1; j < size; j++) {
			if (a[j] < a[min]) {
				min = j;
			}
		}
		swap(a, i, min);
	}
}
```

### 결과
```java
public class SelectionSort {
	public static void selection_sort(int[] a, int size) {

		for (int i = 0; i < size - 1; i++) {
			int min = i;

			for (int j = i + 1; j < size; j++) {

				if (a[j] < a[min]) {
					min = j;
				}
			}

			swap(a, i, min);
		}
	}

	public static void swap(int[] temp, int x, int y) {
		int s_temp = temp[x];
		temp[x] = temp[y];
		temp[y] = s_temp;

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

		selection_sort(num, size);

		System.out.println("---선택 정렬(selection sort)---");

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
[0] : 3
[1] : 25
[2] : 13
[3] : 24
[4] : 33
[5] : 10
[6] : 5
[7] : 9
---선택 정렬(selection sort)---
[3, 5, 9, 10, 13, 24, 25, 33]
```
