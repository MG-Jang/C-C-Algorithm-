# vector

## vector 특징 
- vector는 배열의 특징도 가지고 있으며 stack의 특징도 가지고 있다. 
- 가장 큰 장점은 sort 클래스를 이용해서 값을 자신이 원하는 대로 정렬이 가능하다는 점이다.
- vector는 물리적 속도 측면에서는 배열보다 불리하다. 하지만 메모리를 효율적으로 관리하고 예외처리가 쉽다는 장점이 있다.
- tuple과 도 같이 많이 사용된다.

## vector 함수 <hr>

|함수명 | 용도 | 예시|
|---|---|---|
|push_back|vector에 값을 추가|v.psuh_back(10)|
|pop_back|vector 최상단에 저장된 값을 제거|v.pop_back()|
|size|vector 크기 반환 |v.size()|
|clear|모든 원소를 제거|v.clear()|
|begin|첫번째 원소 지칭(sort와 많이 사용)|v.begin()|
|end|마지막 원소 지칭(sort와 많이 사용)|v.end()|
|front|가장 앞의 원소를 출력|v.front()|
|back|가장 뒤의 원소를 출력|v.back()|

## vector 사용법 <hr>

> 기본 사용법
``` c++
// 아래 클래스와 내용은 밑의 예시에서 포함되는 것으로 간주
#include<iostream>
#include<vector>
using namespace std;
```

- 기본 사용법

```c++
vector<int> v;

int main(){
	v.push_back(1);
	v.push_back(2);
	v.push_back(3);
	v.pop_back();
	cout << v[0] << "," << v[1]; // 결과: 1,2
	cout << v.size() << endl; // 결과: 2
	v.clear();
	cout << v.size() << endl; // 결과: 0
	return 0;
}
```

- 크기 할당 및 초기화(많이 사용하지는 않지만 알아두면 도움이 될지도?)
  
```C++
vector<int> v(3); // 0으로 초기화된 3개의 원소를 가지는 vector v를 생성
vector<int> v2(3,1); // 1으로 초기화된 3개의 원소를 가지는 vector v를 생성

int main()
{
	cout << v.size() << endl;  //결과: 3
	cout << v[0] << v[1] << v[2] << endl; //결과: 000 
	// 단 여기서 3이상의 index를 참조하면 참조 오류가 발생 

	cout << v2[0] << v2[1] << v2[2] << endl; //결과: 111 

	cout << v.size() << endl;  //3
	return 0;
}
```

<br>

>  sort 활용 방법
  - 정렬되어 있지 않은 vector를 크기 순대로 정렬이 가능하다.
  - cmp(compare의 약자로 많이 사용하나 굳이 cmp 가 아니여도 됨)를 활용하여 역으로 정렬하거나 더 나아가서 자신이 원하는 대로 정렬이 가능하다.

```c++
#include<algorithm> //추가해야 sort 사용 가능 
vector<int> v;

bool cmp(int i, int j){
	return i > j;
} 

int main(){
	v.push_back(5);
	v.push_back(2);
	v.push_back(4);
	sort(v.begin(), v.end()); // 오름차순 정렬
	cout << v[0] << "," << v[1] << "," << v[2] << endl; // 결과: 2,4,5
	sort(v.begin(), v.end(), cmp); // 내림차순 정렬
	cout << v[0] << "," << v[1] << "," << v[2] << endl; // 결과: 5,4,2
	return 0;
}
```

<br>

>  tuple 활용법 (정말 많이 사용!)

- tuple은 2개 이상의 원소를 한 vector 공간에 저장 할때 많이 사용된다.(주로 r,c 위치를 저장 할 때 많이 사용)
- 최대 몇개까지 저장이 가능한지 test해보지는 않았지만 6개 이상도 한번에 저장이 가능 한것으로 판단된다. 

```C++
#include<tuple> // tuple 추가!
vector<tuple<int,int>> v;

int main()
{
	v.push_back(make_tuple(1,2));
	v.push_back(make_tuple(3,4));

	cout << get<0>(v[0]) << "," << get<1>(v[0]) << endl; //결과: 1,2
	cout << get<0>(v[1]) << "," << get<1>(v[1]) << endl; //결과: 3,4
	return 0;
}
```

<br>

>  tuple , sort  동시 사용

- 많이 사용되지는 않지만 tuple과 sort를 동시에 사용하는 경우도 종종 생긴다.

```C++
#include<algorithm>
#include<tuple> // tuple 추가!

vector<tuple<int,int>> v;

bool cmp(tuple<int,int> i, tuple<int,int> j)
{
	return get<0>(i) < get<0>(j);// 앞 원소를 기준으로 정렬
}

int main()
{
	v.push_back(make_tuple(5, 1));
	v.push_back(make_tuple(3, 7));
	v.push_back(make_tuple(4, 3));
	sort(v.begin(), v.end(), cmp);
	cout << get<0>(v[0]) << "," << get<1>(v[0]) << endl; //결과: 3,7
	cout << get<0>(v[1]) << "," << get<1>(v[1]) << endl; //결과: 4,3
	cout << get<0>(v[2]) << "," << get<1>(v[2]) << endl; //결과: 5,1
	return 0;
}
```

<br>

>  2차원 vector

- vector도 배열처럼 사용이 가능하다.
- 단 배열과 차이점은 미리 선언이 되어있지 않아도 push_back을 이용하여 요소를 추가 할 수 있다.

- 기본 사용 방법
```C++
vector<vector<int>> v(6, vector<int>(5, 0)); // 기본값0으로 6행 5열의 배열 선언

int main()
{
	for (int i = 0; i < 6; i++)
	{
		for (int j = 0; j < 5; j++)
		{
			cout << v[i][j];
		}
		cout << endl;
	}

	// 주의 할 점. size를 하는 경우 아래 와 같이 나온다.
	cout << v.size() << endl; //결과: 6 
	cout << v[0].size() << endl;//결과: 5
	return 0;
}
```