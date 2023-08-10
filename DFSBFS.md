DFS BFS 정리
=============

DFS(Depth First Search) 깊이 우선 탐색
-------------
- 재귀 or stack 를 사용
- 검색속도는 BFS보다 느림
- 미로찾기 문제에 사용

###  인접 행렬로 표현된 그래프 : O(N^2)
  <figure>
    <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbnq3DH%2FbtqECLCRbrI%2Fu2Jx4k9dNsWOdkTrUHwdFK%2Fimg.png"  width="400" height="200" >
</figure>


### 인접 리스트로 표현된 그래프 : O(N+E)
 <figure>
    <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F9eAcs%2FbtqECiuoGCw%2FNQLMAp4OJccfVcN0pONTck%2Fimg.png"width="400" height="200">
</figure>

<br/>
BFS(Breath First Search) 너비 우선 탐색
-------------
- queue 를 사용
- 두 노드사이의 최단 경로를 찾을때 사용
<br/>
<br/>
<figure>
    <img src="https://mblogthumb-phinf.pstatic.net/MjAyMDA4MTdfNDkg/MDAxNTk3NjYzMjU3NzEx.kWpe6nTeQ4DWOetDD0pAPmbzB_YX4XgZV5gtnOd9eF4g.UWPfIfxmT99eQb1pVeotsmrPisVzO4Sw3RK0CpAVdFIg.JPEG.zzaxowns/bandicam_2020-08-17_19-59-26-102.jpg?type=w800"width="600" height="250">
</figure>
<br/>


DFS 예시 코드 
-------------
---------------------------------------
- 인접 행렬
```C++
int map[10][10];
int n;

void input()
{
	cin >> n;
	for (int y = 0; y < n; y++) {
		for (int x = 0; x < n; x++) {
			cin >> map[y][x];
		}
	}
}

void DFS(int now)
{
	cout << now << " ";

	for (int i = 0; i < n; i++) {
		if (map[now][i] == 1) {
			DFS(i);
		}
	}
}

int main()
{
	input();
	DFS(0);

	return 0;
}
```
- 인접 리스트 (노드:n  간선:m)
```C++
int n, m;
vector<int> adj[10];
int main() {
    cin >> n >> m;
    for (int i=0; i<n; i++) {
      int a, b;
      cin >> a >> b;
      adj[a].push_back(b);
      adj[b].push_back(a);
    }
}
```
BFS 예시 코드 
-------------
---------------------------------------

```C++
int map[6][6]; 
int start; 
void input() {
	map[0][2] = 1; 
	map[0][3] = 1; 
	map[0][5] = 1; 
	map[1][3] = 1; 
	map[1][4] = 1; 
	map[1][5] = 1; 
	map[2][4] = 1; 
	map[2][5] = 1; 
	map[4][0] = 1; 
	map[4][5] = 1; 
	cin >> start; 
}
int visited[6]; 
void bfs(int now) {
	cout << now << " ";
	for (int next = 0; next < 6; next++) {
		if (map[now][next] == 0) continue;
		if (visited[next] == 1) continue; 
		visited[next] = 1; 
		dfs(next); 
	}
}
int main()
{
	input(); 
	
	visited[start] = 1; 
	bfs(start); 
	return 0; 
}
```