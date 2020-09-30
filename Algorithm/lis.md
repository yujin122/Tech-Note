# LIS(Longest Increasing Subsequence)
`최장증가부분수열`, 증가하는 원소의 부분집합 중 가장 긴 부분집합을 찾는 알고리즘

**ex)**
[**20**, **40**, 30, **50**, 10, **80**, 70]<br/>
-> [20, 40, 50, 80] 으로 LIS는 4이다.
<br/>

### 시간복잡도
**DP** 

> O(N<sup>2</sup>)

<br/>

### 구현

1. **arr[]** : 주어진 배열
2. **dp[index]** : arr[index]의 최대 증가 수열 값
3. default max 값은 1
4. **arr[i] > arr[j] && dp[i] < dp[j] + 1** 
: i의 값이 j의 값보다 클 경우 증가수열므로 dp[j] 값에 +1 해준다. <br/>
(단, dp[j]+1 이 dp[i] 보다 클 경우에만 실행.<br/>
 -> 최대 증가 수열 값을 찾는 것이므로 dp[j]+1이 dp[i]보다 작다면 의미 X)

```java
int[] arr = { 20, 40, 30, 50, 10, 80, 70 };

int[] dp = new int[arr.length]; 

int max = 1;

for (int i = 0; i < arr.length; i++) {
	dp[i] = 1;
	for (int j = 0; j < i; j++) {
		if (arr[i] > arr[j] && dp[i] < dp[j] + 1) {
			dp[i] = dp[j] + 1;
		}
		if (max < dp[i]) {
			max = dp[i];
		}
	}
}

System.out.println("LIS : " + max);
```
```
LIS : 4
```
