---
title: "operator"
excerpt: "Study for operator"
excerpt_separator: "<!--more-->"
categories:
  - operator
tags:
  - Basic
last_modified_at: 2022-03-13T14:42:00
---
# Operator

##  Operator 개념
- 연산자를 더 많은 곳에 내 가 원하는 방향으로 사용하기 위해 구현

##  Operator 예시
```c++
#include <iostream>
using namespace std;

struct node {
	char ch;
};

int operator+(node a, node b) { 
	return int(a.ch) + int(b.ch) ;
}

int main() {
	int check;
	node ch1;
	ch1.ch	= 'A'; // 아스키코드 65
	node ch2;
	ch2.ch = 'B'; // 66
	check = ch1 + ch2;
	cout << check; // 66+65 = 131
	return 0;
}
```