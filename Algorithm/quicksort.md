# 퀵 정렬(Quick Sort)  
'찰스 앤터니 리처드 호어'가 개발한 정렬 알고리즘  

    1. 배열 안에 1개의 원소 선택(피벗, pivot)  
    2. 피벗을 기준으로 피벗보다 작으면 좌측 크면 우측에 원소들을 배치  
    3. 피벗을 제외한 나뉜 그룹에서 다시 피벗을 정해 정렬  
    4. 그룹에 원소가 하나 남을 때까지 반복  
  

#### 장점
>       
> 속도가 빠르다. 
> 
>  추가 메모리 공간이 필요하지 않는다.     
>  
#### 단점
>       
>    피벗값에 따라 시간 복잡도가 크게 달라진다.   
>    
>    불안정 정렬
>    

### 시간복잡도
#### 평균

> O(NlogN)

#### 최악

> O(N<sup>2</sup>)

### 구현

<img src="https://user-images.githubusercontent.com/46274903/92582635-236fc880-f2cc-11ea-8938-82f307de4543.PNG" width=""  height="">

1. 피벗을 제외한 양끝에서 시작하여 왼쪽은 피벗보다 작은 원소 오른쪽은 피벗보다 큰 원소를 찾아 서로 교환
2. low와 high가 교차할 때까지 반복
3. 피벗 값과 high 값을 교환
4. 피벗을 제외하고 나뉘어진 그룹에서 다시 퀵 정렬
5. 그룹에 원소가 하나 남을 때까지 반복

```java
public static int partition(int[] a, int left, int right) {
	
	int low, high, pivot;
	
	low = left + 1;
	high = right;
	
	pivot = a[left]; 
	
	while (low <= high) {
	
		while (low <= right && a[low] < pivot) {
			low++;
		}
		while (high >= left && a[high] > pivot) {
			high--;
		}
		if (low < high) {
			swap(a, low, high);
		}
	}
	swap(a, left, high);
	return high;
}

public static void quick_sort(int[] a, int left, int right) {
	
	if (left < right) {
		int p = partition(a, left, right);
		
		quick_sort(a, left, p - 1);
		quick_sort(a, p + 1, right);
	}
}
```
### 결과

```
배열 크기 : 8
---배열 값을 입력해주세요--- 
[0] : 12
[1] : 10
[2] : 5
[3] : 26
[4] : 9
[5] : 17
[6] : 25
[7] : 32
---퀵 정렬(quick sort)---
[5, 9, 10, 12, 17, 25, 26, 32]
```

#### [참고자료]
1.[enter link description here](https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html)
