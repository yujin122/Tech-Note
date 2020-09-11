# 병합정렬(Merge Sort)
앞부분과 뒷부분으로 나누어 각각 정렬한 다음 `병합`하는 알고리즘

#### 장점

> 안정적인 정렬 
> 
> 시간복잡도가 항상 O(NlogN)

#### 단점

> 추가적인 메모리가 필요

### 시간복잡도

> O(NlogN)

### 구현

<img src="https://user-images.githubusercontent.com/46274903/92869441-cac03d00-f43d-11ea-9fef-75c76a04ac0f.PNG" width=""  height="500">

1. 하나의 원소가 될 때까지 배열을 나눈다.
2. 나뉜 배열 값을 하나씩 비교하여 더 작은 값을 새로운 배열에 옮긴다.
3. 모든 배열의 값이 정렬될 때까지 병합정렬을 반복한다.
4. 둘 중 하나의 배열이 끝나면 남은 배열을 그대로 새로운 배열에 복사한다.
5. 정렬이 완료된 새로운 배열을 기존 배열에 옮긴다. 

```java
public static void merge(int[] a, int left, int mid, int right) {
	int list[] = new int[right + 1];	// 새로운 배열
	int i = left;
	int j = mid + 1;
	int k = left;

	while (i <= mid && j <= right) {
		if (a[i] <= a[j]) {
			list[k++] = a[i++];
		} else {
			list[k++] = a[j++];
		}
	}
	
	if (i > mid) {	// 앞 배열의 정렬이 끝난 경우
		for (int l = j; l <= right; l++) {
			list[k++] = a[l];
		}
	} else {	// 뒷 배열의 정렬이 끝난 경우
		for (int l = i; l <= mid; l++) {
			list[k++] = a[l];
		}
	}
	for (int l = left; l <= right; l++) {	// 기존 배열에 정렬이 완료된 새로운 배열을 옮긴다.
		a[l] = list[l];
	}
}
	
public static void merge_sort(int[] a,int left,int right) {
	int mid;
	
	if(left<right) {
		mid = (left+right)/2;
		
		merge_sort(a,left,mid);
		merge_sort(a,mid+1,right);
		
		merge(a,left,mid,right);
	}
}
```

결과
```java
public class MergeSort {

	public static void merge(int[] a, int left, int mid, int right) {
		int list[] = new int[right + 1];
		int i = left;
		int j = mid + 1;
		int k = left;

		while (i <= mid && j <= right) {

			if (a[i] <= a[j]) {
				list[k++] = a[i++];
			} else {
				list[k++] = a[j++];
			}
		}

		if (i > mid) {
			for (int l = j; l <= right; l++) {
				list[k++] = a[l];
			}
		} else {
			for (int l = i; l <= mid; l++) {
				list[k++] = a[l];
			}
		}

		for (int l = left; l <= right; l++) {
			a[l] = list[l];
		}

	}
	
	public static void merge_sort(int[] a,int left,int right) {
		int mid;
		
		if(left<right) {
			mid = (left+right)/2;
			
			merge_sort(a,left,mid);
			merge_sort(a,mid+1,right);
			
			merge(a,left,mid,right);
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

		merge_sort(num, 0, size - 1);

		System.out.println("---병합 정렬(merge sort)---");

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
[0] : 5
[1] : 3
[2] : 10
[3] : 2
[4] : 4
[5] : 6
[6] : 8
[7] : 3
---병합 정렬(merge sort)---
[2, 3, 3, 4, 5, 6, 8, 10]
```
