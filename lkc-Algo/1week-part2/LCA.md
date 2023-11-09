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
5. 이 후 LCA의 조건을 맞춰 진행한다.
- a와 b노드가 주어지면 해당 노드의 높이가 낮은 노드를 기준으로 높이를 맞춰준다.
이 때 dp에 저장된 2^h부모노드의 정보를 활용하여 연산 횟수를 단축시켜준다.
높이를 맞췄는데 a==b이면 LCA = a이므로 바로 출력해준다. (LCA가 1일때 예외처리이기도 함)
a와 b노드의 dp값을 비교해가며 LCA를 찾아준다.
```
static int LCA(int a, int b) {
	int ah = depth[a];// 노드 1
	int bh = depth[b];// 노드 2
	 // ah > bh로 세팅
	if(ah < bh) {
		int tmp = a;
		a = b;
		b = tmp;
	} // swap 
	// 1. 높이 맞추기 
	for (int i=h-1; i>=0; i--) {
		if(Math.pow(2, i) <= depth[a] - depth[b]){// 두 노드간의 높이 차가 2의I승보다 같거나 작아질 때 한 노드의 부모로 변환함으로써 높이를 맞춰준다.
			a = parent[a][i];
		}
	}
	if(a==b) return a;
    
	// 2. LCA찾기
	for(int i=h-1; i>=0; i--) {
		if(parent[a][i] != parent[b][i]) {// 부모 같을때까지 쭉쭉 타고 간다 LCA구하는거임 
			a = parent[a][i];
			b = parent[b][i];
		}
	}
	return parent[a][0];
}
```
- 위의 방법이 LCA와 DP를 사용한 방법이고 세그먼트 트리를 사용한 방법도 존재한다.
  <이해하고 올리겠습니다..>
https://loosie.tistory.com/364 <링크 참조>
