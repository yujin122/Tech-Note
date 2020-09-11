# 힙정렬(Heap Sort)
'가장 큰 값이 루트에 위치' 하는 힙의 특징을 이용하여 정렬하는 알고리즘

#### 장점

> 추가적인 메모리가 필요 없고 시간 복잡도가 항상 O(NlogN)을 가져 효율적인 정렬법이다.

#### 단점

> 안정성을 보장 받지 못한다.

### 시간복잡도

> O(NlogN)

### 구현
```java
static void heap_sort(int[] a) {
	int n= a.length;
	
	for(int i = n/2-1; i>=0;i--) {
		heapify(a,n,i);
	}
	
	for(int i=n-1;i>0;i--) {
		swap(a,0,i);
		heapify(a,i,0);
	}
}

static void heapify(int[] a, int s,int i) {
	int p = i;
	int l = i*2+1;
	int r = i*2+2;
	
	if(l<s && a[p] < a[l]) {
		p = l;
	}
	
	if(r<s && a[p]<a[r]) {
		p = r;
	}
	
	if(i != p) {
		swap(a,p,i);
		heapify(a,s,p);
	}
		
}
```
### 결과
```java
public class HeapSort {
		
	static void heap_sort(int[] a) {
		int n= a.length;
		
		for(int i = n/2-1; i>=0;i--) {
			heapify(a,n,i);
		}
		
		for(int i=n-1;i>0;i--) {
			swap(a,0,i);
			heapify(a,i,0);
		}
	}
	
	static void heapify(int[] a, int s,int i) {
		int p = i;
		int l = i*2+1;
		int r = i*2+2;
		
		if(l<s && a[p] < a[l]) {
			p = l;
		}
		
		if(r<s && a[p]<a[r]) {
			p = r;
		}
		
		if(i != p) {
			swap(a,p,i);
			heapify(a,s,p);
		}
				
	}
	
	public static void swap(int[] temp,int x,int y) {
		int s_temp = temp[x];
		temp[x]=temp[y];
		temp[y] = s_temp;
		
	}
	
	public static void main(String[] args) {
		int[] num = {10,5,24,3,9,16,7};
		
		heap_sort(num);

		System.out.println("---힙 정렬(heap sort)---");

		String str = "[";
		for (int i = 1; i < num.length; i++) {
			if (i == num.length - 1) {
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
---힙 정렬(heap sort)---
[5, 7, 9, 10, 16, 24]
```
