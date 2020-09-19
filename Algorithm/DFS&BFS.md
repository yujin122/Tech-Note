# DFS (Depth-First Search, 깊이 우선 탐색)
특정노드에서 시작하여 다음 분기로 넘어가기 전에 해당 분기를 완벽하게 탐색

<img src="https://user-images.githubusercontent.com/46274903/93658313-67559100-fa75-11ea-8299-142247b03e92.PNG " width="600"  height="">

- 모든 노드를 방문할 때 사용
- 순환 알고리즘 형태
- 어떤 노드를 방문했었는지 여부를 반드시 검사해야 한다.

### 장점
> 
> 그래프의 높이 만큼 공간 요구 
> 
> 목표 노드가 깊은 단계에 있을 경우 빠르게 구할 수 있다.

### 시간복잡도
#### 인접리스트 

> O(N+E)

#### 인접행렬 

> O(N<sup>2</sup>)

##### *정점의 수  N, 간선의 수 E*

### 구현
1. 특정(시작) 노드에 다음 노드가 있는지 확인
2. 다음 노드가 방문했던 노드인지 확인
3. 방문했던 노드가 아닐경우 다음노드가 없을 때까지 1, 2를 반복

```java
private int V;	// 노드의 갯수
private LinkedList<Integer> adj[];
	
public Graph(int v) {
	V = v;
	adj = new LinkedList[v];
	for(int i= 0;i<v;i++) {
		adj[i]=new LinkedList();
	}
}

void addEdge(int v, int w) {	// v -> w 연결
	adj[v].add(w);
}
	
void DFSUtil(int v, boolean visited[]) {
	visited[v]=true;
	System.out.print(v+" ");
		
	Iterator<Integer> i = adj[v].listIterator();
	while(i.hasNext()) {	// 다음 노드가 있는 경우
		int n = i.next();	// 다음 노드의 값을 n에 저장
		
		if(!visited[n]) {	// 방문하지 않은 노드일 경우
			DFSUtil(n,visited);
		}
	}
}

void DFS() {
	boolean visited[] = new boolean[V];
	
	for(int i=0;i<V;i++) {
		if(visited[i]==false) {
			DFSUtil(i,visited);
		}
	}
}
```
### 결과
```java
public class Graph {
	private int V;
	private LinkedList<Integer> adj[];
	
	public Graph(int v) {
		V = v;
		adj = new LinkedList[v];
		for(int i= 0;i<v;i++) {
			adj[i]=new LinkedList();
		}
	}
	
	void addEdge(int v, int w) {
		adj[v].add(w);
	}
	
	void DFSUtil(int v, boolean visited[]) {
		visited[v]=true;
		System.out.print(v+" ");
		
		Iterator<Integer> i = adj[v].listIterator();
		while(i.hasNext()) {
			int n = i.next();
			
			if(!visited[n]) {
				DFSUtil(n,visited);
			}
		}
	}
	
	void DFS() {
		boolean visited[] = new boolean[V];
		
		for(int i=0;i<V;i++) {
			if(visited[i]==false) {
				DFSUtil(i,visited);
			}
		}
	}
	
	public static void main(String[] args) {
		Graph g = new Graph(5);
		
		g.addEdge(0, 3);
		g.addEdge(0, 4);
		g.addEdge(0, 2);
		g.addEdge(1, 3);
		g.addEdge(2, 1);
		g.addEdge(2, 4);
		g.addEdge(3, 4);
		g.addEdge(4, 1);
		
		g.DFS();
	}
}
```
```
0 3 4 1 2 
```

# BFS (Breadth-First Search, 너비 우선 탐색)
특정노드에서 시작하여 인접한 노드를 먼저 탐색

<img src="https://user-images.githubusercontent.com/46274903/93659213-e8188b00-fa7d-11ea-9790-3fade4697834.PNG " width="600"  height="">

- 가까운 정점을 먼저 방문, 먼 정점을 나중에 방문하는 방법
- 재귀적으로 동작하지 않음
- 큐(queue)를 사용

### 장점

> 최단경로를 보장

### 단점

> 큐를 이용하기 때문에 노드의 개수가 많을수록 큰 저장공간이 필요

### 시간복잡도
#### 인접리스트 

> O(N+E)

#### 인접행렬 

> O(N<sup>2</sup>)

##### *정점의 수 N, 간선의 수 E*

### 구현
1. 특정(시작) 노드의 값을 큐에 저장
2. 큐의 크기가 0이 아닐경우 다음 노드가 있는지 검사
3. 다음노드가 있을 경우 방문을 했던 노드인지 검사
4. 방문을 하지 않은 노드인 경우 큐에 저장
5. 이를 큐의 크기가 0이 될때까지 반복

```java
private int V;
private LinkedList<Integer> adj[];

public Graph1(int v) {
	V = v;	// 노드의 갯수
	adj = new LinkedList[v];
	
	for(int i=0;i<v;i++) {
		adj[i] = new LinkedList();
	}
}

void addEdge(int v, int w) {	// v -> w 연결
	adj[v].add(w);
}

void BFS(int s) {
	
	boolean visited[] = new boolean[V];
	
	LinkedList<Integer> queue = new LinkedList();
	
	visited[s] = true;
	queue.add(s);
	
	while(queue.size() != 0) {	// 큐에 노드가 있는 경우
		s = queue.poll();	// 큐에 노드 값 추출
		System.out.print(s+" ");
		
		Iterator<Integer> i = adj[s].listIterator();
		
		while(i.hasNext()) {	// 해당 노드에 다음 노드가 있는 경우
			int n = i.next();
			if(!visited[n]) {	// 방문하지 않은 노드인 경우
				visited[n]=true;
				queue.add(n);	// 큐에 노드 값 저장
			}	
		}
	}
}
```
### 결과
```java
public class Graph1 {
	private int V;
	private LinkedList<Integer> adj[];
	
	public Graph1(int v) {
		V = v;
		adj = new LinkedList[v];
		
		for(int i=0;i<v;i++) {
			adj[i] = new LinkedList();
		}
	}
	
	void addEdge(int v, int w) {
		adj[v].add(w);
	}
	
	void BFS(int s) {
		
		boolean visited[] = new boolean[V];
		
		LinkedList<Integer> queue = new LinkedList();
		
		visited[s] = true;
		queue.add(s);
		
		while(queue.size() != 0) {
			s = queue.poll();
			System.out.print(s+" ");
			
			Iterator<Integer> i = adj[s].listIterator();
			
			while(i.hasNext()) {
				int n = i.next();
				if(!visited[n]) {
					visited[n]=true;
					queue.add(n);
				}
			}
		}
	}
	
	public static void main(String[] args) {
		Graph1 g = new Graph1(5);
		
		g.addEdge(0, 3);
		g.addEdge(0, 4);
		g.addEdge(0, 2);
		g.addEdge(1, 3);
		g.addEdge(1, 2);
		g.addEdge(2, 1);
		g.addEdge(2, 4);
		g.addEdge(3, 4);
		g.addEdge(4, 1);
		
		g.BFS(0);
	}

}
```
```
0 3 4 2 1 
```

##### [참고자료]
1. [BFS](https://gmlwjd9405.github.io/2018/08/15/algorithm-bfs.html)
2. [DFS](https://gmlwjd9405.github.io/2018/08/14/algorithm-dfs.html)
