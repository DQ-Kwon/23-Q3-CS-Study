## 최소 공통 조상 LCA(Lowest Common Ancestor) 알고리즘이란?
 - LCA는 주어진 두 노드 A,B의 최소 공통 조상을 찾는 알고리즘이다.

   예를들면 위의 그림에서 5번과 6번노드의 LCA는 2번노드이다.

   ## 📝 풀이방법
   - 일반적 풀이
     1.1번 루트노드를 기준으로 DFS를 돌려서 각 노드의 높이와 부모노드를 저장한다.
     2.두 노드의 높이를 같게 맞춰준다(밸런스 맞추는 것 이야기하는 것 같음)
     3.부모노드가 일치할때까지 비교한다.(최대 1번노드)

     하지만 이 방식은 편향된 트리를 만나면 엄청난 연산을 요구하게 된다.
     따라서 더 효율적인 방식을 요구한다.

   - DP
     2^h의 부모를 알면 연산의 횟수가 매우 줄어든다.
     dp[cur][h] = 2차원배열에 현재 노드의 2^h번째 부모노드를 저장한다.
  1. 트리의 최대 높이 h를 구한다.// (Math.log(n)/Math.log(2))-> n= 2^h-1 -> log n = h log 2
     ```
     static int getTreeHeight() {
	return(int)Math.ceil(Math.log(n)/Math.log(2)) +1;
}
     ```
  3. dfs탐색을 통해 각 노드의 높이(depth)를 구한다.+ dp[node][0] = 첫번째 부모노드 (2^0=1)로 초기화
  ```
static void init(int cur, int h, int pa) {
	depth[cur] = h;// 높이 저장
	for(int nxt : list[cur]) {// 하위 노드들에 대하여 
		if(nxt != pa) {// 현 노드와 연결되어 있고 동시에 하향식인 노드들만 
			init(nxt, h+1, cur);// 재귀 
			parent[nxt][0] = cur; // nxt의 부모 cur 
		}
	}
}
```
  4. 남은 2^h-1까지 채운다.
     ```
static void fillParents() {
	for(int i=1; i<h; i++) {// dp[node][h] 이고 0은 위에서 초기화 하였으므로 1부터 시작 ~ h-1까지
		for(int j=1; j<n+1; j++) {//node 전체에 대한 
			parent[j][i] = parent[parent[j][i-1]][i-1];// 노드 15의 2^7번째 부모노드는 15번의 2^6번 부모의 2^6번째부모이다? 
		}
	}
}

     ```
