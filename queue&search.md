# Queue

##  기본 queue
	자료구조의 한 형태
	FIFO 방식 (First In First Out)
- function 
	>  push(x) => 마지막에 x를 넣음
		pop() => 첫번째 원소를 없앰
		empty() => 큐가 비어있는지 확인
		front() => 첫 번째 원소 반환
		back() => 마지막 원소 반환
- 기본 명령어
	>- queue<자료형>q 
	</br>
	>- q.push(데이터)
	</br>
	>- q.front()
	>- q.pop()
## Priority Queue

	우선 순위 큐
	우선 순위를 두어 가장 우선순위가 큰 것 부터 pop함

- 우선 순위 결정 방법

		struct Node {
			int n;
			string str;
		};

		bool operator<(Node a,Node b){
			return a.n < b.n;
		}
		
		priority_queue<Node> pq;
	
	위 코드에서 operator로 우선순위를 직접 줄 수 있음. 
	반환 값이 true일때 두번째 인자 (  b ) 가 더 큰 우선순위를 가지게 됨. 
	즉, Node의 n값이 클 수록 우선 순위를 가지게 됨

 - function
	 > push(x) => x 값 삽입 (자동으로 순위 결정됨)
		 front() => 가장 우선순위가 큰 값 반환
		 pop() => 가장 우선순위가 큰 값 삭제
		 empty() => 비어있는지 확인 
- 기본 명령어 (queue와 동일) 
  > 단! 값을 출력하는 경우 pq는 front 대신 pq.top() 을 사용 
- 사용예시
```c++
struct node{
	char ch;
	int age;
};

queue<node> q;

int main(){
	q.push({'A',10});
	//위와 동일한 방식
	//node tmp;
	//tmp.ch= 'A';
	//tmp.age = 10;
	q.push(tmp);
	cout <<q.top().ch << "," << q.top().age; // A,10
	q.pop();
	cout << q.size(); // 0
	return 0;
}
```
# Search

## 완전탐색
	
	가능한 모든 경우의 수를 다 탐색

- 종류
	 > 단순 brute-force
	 > 재귀
	 > 비트마스크
	 > DFS/BFS

### Brute-force

	주로 for문으로 사용함
	단순하게 모든 부분을 다 서치하는 방법
	

## 이진탐색
		
		bineary search
		두 갈래로 나누어 탐색
		O(logn)

- 방법
	 > 범위의 가운데를 기준으로 잡음
		 서치하려는 값이 기준에 왼쪽인지 오른쪽인지 판별
		 - 왼쪽 : 범위의 끝을 가운데로 바꿈
		 -  오른쪽 : 범위의 첫번째를 가운데로 바꿈
		다시 반복

- 구현
```C++
bool abc(int start, int finish, int x){
	int mid =(start+finish)/2;
	
	if(start == finish){
		if(start ==x) return true;
		else false;
	}

	if(mid < x){
		abc(mid+1,finish,x);
	}else{
		abc(start,mid-1,x);
	}
}
```

  이런 식으로 구현 가능.

STL이용 또한 가능 -> algorithm 해더

```C++
int arr[n];
bineary_search(arr, arr+n, 70);
```
bool값으로 return됨 
만약 index값을 알고 싶다면 직접 구현!




		
			 