# Tree(트리)
`노드`로 이루어진 `비선형` 자료구조
대상 정보의 각 항목들을 계층적으로 연관되도록 구조화 시키고자 할 때 사용.

- 사이클(cycle)이 없는 하나의 연결그래프
- DAG(Directed Acyclic Graphs, 방향성이 있는 비순환 그래프) 의 한 종류이다.

## 구조
<img src="https://user-images.githubusercontent.com/46274903/92094299-3f2c2800-ee0f-11ea-9458-b24ca1741fcc.PNG " height="400">

| |  |
|--|--|
| node  | 트리를 구성하고 있는 각 요소 |
| edge(간선) | 트리를 구성하기 위해 노드와 노드를 연결하는 선 |
| root(루트) |  부모가 없는 노드, 가장 윗부분에 위치, 1개 트리에 1개 루트|
| leaf node(단말 노드) |자식이 없는 노드, 트리 가장 아랫부분에 위치  |
| internal(내부) |단말노드가 아닌 노드  |
| child(자식)| 어떤 노드로부터 가지로 연결된 아래쪽 노드 |
| parent(부모) | 어떤 노드에서 가지로 연겨로딘 위쪽 노드 |
| sibling(형제) | 같은 부모를 가지는 노드 |
| level(레벨) | 특정 깊이를 가진 Node의 집합 |
| depth(노드의 깊이) | 루트에서 어떤 노드에 도달하기 위해 거쳐야하는 간선의 수 |
| size(노드의 크기) | 자신을 포함한 모든 자손 노드의 개수 |
| degree(노드의 차수) | 하위 트리 개수 / 간선 수 , 각 노드가 지닌 가지의 수 |
| degree of tree(트리의 차수) | 트리의 최대 차수 |
| height(트리의 높이)  | 루트 노드에서 가장 깊숙히 있는 노드의 깊이
 |
 
## 종류
1. 이진트리 ( Binary Tree)
2. 이진탐색트리 (Binary Search Tree)
3. 균형트리 ( AVL)
4.  이진 힙

## 이진트리(Binary Tree)
각 노드가 `최대 2개`의 자식을 갖는 트리

### 완전 이진 트리(Complete Binary Tree)
<img src="https://user-images.githubusercontent.com/46274903/92094389-59fe9c80-ee0f-11ea-8295-85904226b9dd.PNG " height="400">

 - 마지막 레벨을 제외한 레벨은 노드로 가득 채운다. 
 - 마지막 레벨은 왼쪽에서 오른쪽 방향으로 노드를 채우되 끝까지 채울 필요는
   없다.

### 포화 이진 트리(Perfect Binary Tree)
<img src="https://user-images.githubusercontent.com/46274903/92094416-6256d780-ee0f-11ea-8c29-99d99b2742e7.PNG " width="650" height="400">

 - 모든 레벨이 꽉 찬 이진 트리

### 순회
1. **전위순회 (Preorder)**
< root -> left -> right >
```java
public void preOrder(Node node) {
	if(node != null) {
		System.out.print(node.data + " ");	// root
		preOrder(node.left);	//left
		preOrder(node.right);	// right
	}
}
```
2. **중위순회 (Inorder)**
< left -> root -> right>
```java
public void inOrder(Node node) {
	if(node != null) {
		inOrder(node.left);	// left
		System.out.print(node.data + " ");	//root
		inOrder(node.right);	//right
	}
}
```
3. **후위순회 (Postoder)**
< left -> right -> root >
```java
public void postOrder(Node node) {
	if(node != null) {
		postOrder(node.left);	//left
		postOrder(node.right);	//right
		System.out.print(node.data + " ");	//root
	}
}
```

## 이진 검색 트리 (Binary Search Tree)

 - 어떤 노드 N을 기준으로 왼쪽 서브트리노드의 모든 값이 N 값보다 작아야 되고 오른쪽은 N 값보다 커야한다.

 - 왼쪽 서브트리노드 < N < 오른쪽 서브트리노드
 - 같은 값은 존재하지 않는다.

<img src="https://user-images.githubusercontent.com/46274903/92095329-7b13bd00-ee10-11ea-9c83-7317e51b3706.PNG " width="550" height="400">

### 구현
**생성**
```java
public class BinarySearchTree {
	private Node root;	
	
	private class Node{		
		int data;
		
		Node left;	// 왼쪽 노드
		Node right;	// 오른쪽 노드
		
		public Node(int data){
			this.data = data;
			this.left = null;
			this.right = null;
		}		
	}
	
	public BinarySearchTree() {
		root = null;
	}
	public Node getRoot() {
		return this.root;
	}
}
```

**삽입**
```java
public void insert(int data) {
	if(find(data) != null) return;	// 트리에 동일한 data가 있으면 나옴
	
	Node newNode = new Node(data);
	
	if(root == null) {	// 첫 노드일 경우
		root = newNode;	// root에 노드 지정
	}else {
		Node currentNode = root;
		Node parentNode;	// 부모 노드
		
		while(true) {
			parentNode = currentNode;
			
			if(data < parentNode.data) {	//data가 현재 노드의 data보다 작을 때
				currentNode = parentNode.left;	// 왼쪽으로 이동
				
				if(currentNode == null) {	// 왼쪽 노드가 비어있을 때
					parentNode.left = newNode;	
					return;
					
				}
			}else {	//data가 현재 노드의 data보다 클 때
				currentNode = parentNode.right;	// 오른쪽으로 이동
				
				if(currentNode == null) {	// 오른쪽 노드가 비어있을 때
					parentNode.right = newNode; 
					return;
				}
			}
		}
	}
}
```
- 입력된 값이 현재 노드의 값보다 작을 경우 왼쪽 노드에, 클 경우 오른쪽 노드에 삽입

**탐색**
```java
public Node find(int data) {
	if(root == null) return null;	// 트리에 아무것도 없을 때
	
	Node currentNode = root;
	
	while (currentNode.data != data) {	
		if (currentNode.data > data) {	// 입력된 data의 값이 현재 노드의 data보다 작을 경우
			currentNode = currentNode.left;
		} else {	// 입력된 data의 값이 현재 노드의 data보다 클 경우
			currentNode = currentNode.right;
		}
		
		if(currentNode == null) {	// 동일한 데이터를 찾지 못한 경우
			return null;	
		}
	}
	
	return currentNode;
}
```

**삭제**
1.  자식 노드가 없는 경우
	- 해당 노드 삭제

2.  하나의 자식 노드를 갖는 경우
	- 자식 노드가 왼쪽에 있는지 오른쪽에 있는지 확인 후 부모 노드와 삭제할 노드의 자식 노드를 연결	
3.  두개의 자식 노드를 갖는 경우

<img src="https://user-images.githubusercontent.com/46274903/92104238-047cbc80-ee1c-11ea-91ce-30ea3d29065c.PNG " height="">

- 삭제할 노드 오른쪽 서브트리에서 가장 작은 값을 삭제할 노드 위치에 대체


```java
public boolean delete(int data) {
	Node parentNode = root;
	Node currentNode = root;
	boolean isLeftChild = false;
	
	while(currentNode.data != data) {
		parentNode = currentNode;
		if(currentNode.data>data) {	// 입력된 data의 값이 현재 노드의 data보다 작을 경우
			isLeftChild = true;
			currentNode = currentNode.left;	// 왼쪽으로 이동
		}else {	// 입력된 data의 값이 현재 노드의 data보다 클 경우
			isLeftChild = false;
			currentNode = currentNode.right;	// 오른쪽으로 이동
		}
		if(currentNode == null) {	// 동일한 데이터가 없을 경우
			return false;
		}
	}
	
	// 1. 자식 노드가 없는 경우
	if(currentNode.left == null && currentNode.right == null) {
		if(currentNode == root) {	// 삭제할 노드가 root
			root = null;
		}
		if(isLeftChild) {	// 삭제할 노드가 왼쪽 노드일 경우
			parentNode.left = null;	 
		}else {	// 삭제할 노드가 오른쪽 노드일 경우
			parentNode.right = null;
		}// 2. 자식 노드가 하나인 경우
	}// 삭제할 노드의 자식 노드가 왼쪽 노드일 경우
	else if(currentNode.right == null) {	
	
		if(currentNode == root) {
				root = currentNode.left;
			}// 부모 노드에 삭제할 노드의 자식 노드를 연결
			else if(isLeftChild) {
				parentNode.left = currentNode.left;
			}else {
				parentNode.right = currentNode.left;
			}
	// 삭제할 노드의 자식 노드가 오른쪽 노드일 경우
	}else if(currentNode.left ==null) {	
	
		if(currentNode == root) {
				root = currentNode.right;
			}// 부모 노드에 삭제할 노드의 자식 노드를 연결
			else if(isLeftChild) {
				parentNode.left = currentNode.right;
			}else {
				parentNode.right = currentNode.right;
			}

	}else { //3. 자식이 노드가 둘인 경우
		Node rightNode = currentNode.right;	// 삭제될 노드의 오른쪽 노드
		
		Node replacementNode = getMinimum(currentNode.right);	// 삭제될 노드 자리에 올 새로운 노드
		
		if(currentNode == root) {
			root = replacementNode;
		}else if(isLeftChild){
			parentNode.left = replacementNode;
		}else {
			parentNode.right = replacementNode;
		}
		
		replacementNode.right = rightNode;	// 삭제할 노드의 오른쪽 노드들을 연결
		
		if(replacementNode == rightNode) {	// 삭제할 노드의 오른쪽에 노드가 하나 밖에 없는 경우
			replacementNode.right =null;
		}
		
		replacementNode.left = currentNode.left;	// 삭제할 노드의 왼쪽 노드들을 연결
	}
	
	return true;
}
// 삭제 될 노드에 올 새로운 노드 탐색 메서드
public Node getMinimum(Node deleteRightNode) {
	Node parentNode = deleteRightNode;
	Node currentNode = deleteRightNode;
	
	while(currentNode.left != null) {
		parentNode = currentNode;
		currentNode = currentNode.left;
	}
	
	parentNode.left = null;
	return currentNode;
}
```

### 결과
```java
public static void main(String[] args) {
	BinarySearchTree bst = new BinarySearchTree();
	
	bst.insert(20);
	bst.insert(16);
	bst.insert(30);
	bst.insert(5);
	bst.insert(1);
	bst.insert(13);
	bst.insert(9);
	bst.insert(23);
	bst.insert(26);
	bst.insert(24);
	
	
	System.out.print("전위순회 : ");
	bst.preOrder(bst.getRoot());
	System.out.println();
	System.out.print("중위순회 : ");
	bst.inOrder(bst.getRoot());
	System.out.println();
	System.out.print("후위순회 : ");
	bst.postOrder(bst.getRoot());
	System.out.println();
	
	System.out.println("\n5, 24 삭제");
	bst.delete(5);
	bst.delete(24);
	System.out.print("중위순회 : ");
	bst.inOrder(bst.getRoot());
	System.out.println();
}
```
```
전위순회 : 20 16 5 1 13 9 30 23 26 24 
중위순회 : 1 5 9 13 16 20 23 24 26 30 
후위순회 : 1 9 13 5 16 24 26 23 30 20 

5, 24 삭제
중위순회 : 1 9 13 16 20 23 26 30 
```
