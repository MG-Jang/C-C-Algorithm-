---
title: "Heap, priority_queue"
excerpt: "Study for heap"
excerpt_separator: "<!--more-->"
categories:
  - heap
tags:
  - Basic
last_modified_at: 2022-03-11T14:42:00
---

Heap, priority_queue 정리
=============


##  Heap 개념
- 완전 이진트리의 일종, 우선 순위 큐를 사용 하여 만들어진 자료구조.
- 여러 값들의 최대값 또는 최소값을 빠르게 찾기위해 구현.
- 우선 순위 큐(priority_queue)를 사용하여 만들어진 힙(heap)을 이해 
</br>
</br>

##  Heap 구조
- heap은 보통 반 정렬 상태를 유지
- max heap: 부모 노드의 키값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리

- min heap: 부모 노드의 키 값보다 작거나 같은 완전 이진트리
</br>

![캡처](/img/heapimg.JPG)

출처[heejeong Kwon]

> max heap (오름 차순정렬)
```c++
#include <queue>

priority_queue<int> t;

//priority_queue<int, vector<int>, less<int>> t; 을 간략하게 표현한 것.

```
> min heap (내림차순 정렬)
```c++
#include <queue>

priority_queue<int, vector<int>, greater<int>> t;
```
> min heap (operator 사용 구현)
``` c++
struct cmp { 
    // operator(): 구초체뿐만아니라 다른 형태에도 사용가능  
    // operator <(...): 구조체만 사용가능 
	bool operator()(node back, node front) {  
        // 왜 sort때 사용한 compare과 부등호가 반대일까? pq는 기본적으로 내림차순이므로 오름차순정렬인 경우와 back, front 의 크기가 반대이다.
		if (back.age < front.age) return 0;
		// return back.age < front.age 로하면 back.age < front.age 가 참인 경우 1을 return 함.
		// return 0 인경우 순서를 변경 x return 1 인경우 front 와 back 의 순서를 변경한다. 
		else if (back.age == front.age) {
			if (back.name < front.name)return 0;
			else return 1;
		}
		else return 1;
	}
};
```
##  Heap 예시 코드
```c++
#include <iostream>
#include <queue>
#include <string>
#include<vector>
using namespace std;

// 1.나이가 어린순
// 2.이름은 알파벳순(나이가 동일한 경우)
struct node {
    string name;
    int age;
};

node arr[5] = {
    {"bob",20},{"jason",23},{"choi",20},{"tom",40},{"jenny",18}
};

struct cmp {
	bool operator()(node back, node front) {
		if (back.age < front.age) return 0;
		else if (back.age == front.age) {
			if (back.name < front.name)return 0;
			else return 1;
		}
		else return 1;
	}
};

// 위와 동일함. 조금더 간단하게 표현
//struct cmp {
//    bool operator()(node b, node f)
//    {
//        if (f.age < b.age)return true;
//        if (f.age > b.age)return false;
//        return f.name < b.name;
//    }
//};

int main()
{
    priority_queue<node, vector<node>, cmp>pq;

    for (int x = 0; x < 5; x++)
    {
        pq.push(arr[x]);
    }

    for (int x = 0; x < 5; x++)
    {
        cout << pq.top().name << " " << pq.top().age << endl;
        pq.pop();
    }
    return 0;
}
```