# 순열 조합

> ## 기본개념
###  순열
  - 서로 다른 n개 중에 r개를 선택하는 경우의 수를 의미(순서 상관 있음)
</br>
</br>
![캡처](/img/%EC%88%9C%EC%97%B41.JPG)

###  조합
- 서로 다른 n개중에 r개를 선택하는 경우의 수를 의미. (순서 상관 없음)
</br>
</br>
![캡처](/img/%EC%A1%B0%ED%95%A91.JPG)
</br>
###  중복 순열
  - 중복 가능한 n개 중에 r개를 선택하는 경우의 수를 의미(순서 상관 있음)
</br>
</br>
![캡처](/img/%EC%A4%91%EB%B3%B5%EC%88%9C%EC%97%B4.JPG)
## C++ 코드 구현
</br>

dfs(재귀탐색), visited 배열을 이용하여 구현 가능
#### 예를 들어 1, 2, 3 을 순서에 상관있이 2가지를 뽑는다고 가정하자
</br>

> ##  순열
- ## 경우의 수 
  ```C++
  1,2
  1,3
  2,1
  2,3
  3,1
  3,2 
  ```
  총 6가지의 경우의 수
</br>
</br>
- ##  c++ 코드 / visited 배열 (방문여부 확인) 을 이용하여 코드를 구성.
참고: visited 배열 (used 배열) 이름만 다를 뿐 동일 한 역할</br>
보통 visited로 더 많이 표기 하는 느낌. (ssafy의 경우 used 선호) 
```c++
#include <iostream>
#include<vector>
using namespace std;

int visited[3];
int map[3] = { 1,2,3 }; // 카드 종류
int bottom_level = 2;// 뽑을 카드의 갯수
vector<int> vec; // 탐색한 카드 저장 
                 //stack을 사용할 수 도있지만 출력할때 불편함이 있어 vector사용

void dfs(int level) {
	if (level == bottom_level) {
		for (int i = 0; i < vec.size(); i++) cout << vec[i] << " ";
		cout << endl;
		return; 
	}
	for (int i = 0; i < 3; i++) // 카드의 종류크기만큼 
	{
		if (visited[i] == 0) { // 방문여부 확인
			visited[i] = 1; 
			vec.push_back(map[i]);
			dfs(level + 1);
			// dfs종류후 저장된 카드 삭제 및 방문 여부 x로 변경
			vec.erase(vec.end()-1,vec.end()); 
			visited[i] = 0;
		}
	}
}

int main() { 
	dfs(0);
	return 0;
}
```
</br>

>## 조합
- ## 경우의 수
``` c++
1,2
1,3
2,3
```
총 3가지
- ## c++ 코드 / visited 배열 (방문여부 확인) 을 사용 X 
- 대신 선택된 카드보다 작은 카드는 선택하지 않는 조건문 삽입 
```c++
#include <iostream>
#include <stack>
#include<vector>
using namespace std;

//int visited[3];
const int cardnum = 3; // 카드의 갯수
int map[cardnum] = { 1,2,3 }; // 카드 종류
int bottom_level = 2;// 뽑을 카드의 갯수
vector<int> vec; // 탐색한 카드 저장 

void dfs(int level) {
	if (level == bottom_level) {
		for (int i = 0; i < vec.size(); i++) cout << vec[i] << " ";
		cout << endl;
		return;
	}
	for (int i = 0; i < 3; i++) // 카드의 종류크기만큼 
	{
		if (!vec.empty()&& vec[vec.size() - 1] >= map[i])continue; 
        // vec의 크기가 0이 아니고(level이 1이상인 경우) 앞의 값보다 작거나 같은 경우 넣지 않는다. 
		vec.push_back(map[i]);
		dfs(level + 1);
		//dfs종류후 저장된 카드 삭제
		vec.erase(vec.end() - 1, vec.end());
	}
}

int main() {
	dfs(0);
	return 0;
}
```
>## 중복 순열
  ```C++
 1,1
 1,2
1,3
2,1
2,2
2,3
3,1
3,2
3,3
  ```
 총  9가지
> ###  c++ 코드 / visited 배열 (방문여부 확인) 을 사용 X
```C++
#include <iostream>
#include <stack>
#include<vector>
using namespace std;

//int visited[3];
int map[3] = { 1,2,3 }; // 카드 종류
int bottom_level = 2;// 뽑을 카드의 갯수
vector<int> vec; // 탐색한 카드 저장 

void dfs(int level) {
	if (level == bottom_level) {
		for (int i = 0; i < vec.size(); i++) cout << vec[i] << " ";
		cout << endl;
		return; 
	}
	for (int i = 0; i < 3; i++) // 카드의 종류크기만큼 
	{
		//if (visited[i] == 0) { // 방문여부 확인 안함
			// visited[i] = 1;
			vec.push_back(map[i]);
			dfs(level + 1);
			// dfs종류후 저장된 카드 삭제
			vec.erase(vec.end()-1,vec.end()); 
			//visited[i] = 0;
		//}
	}
}

int main() { 
	dfs(0);
	return 0;
}
```
</br>
</br>
이미지출처: 코딩팩토리 https://coding-factory.tistory.com/