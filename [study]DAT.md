---
title: "Sort"
excerpt: "Study for Sort"
excerpt_separator: "<!--more-->"
categories:
  - Sort
tags:
  - Basic
last_modified_at: 2022-03-10T14:42:00
---

<!--more-->

<br>

## DAT(Direct Address Table)

- DAT란 해시 테이블의 일종으로, 한 테이블의 키 값을 주소로 사용하는 테이블을 말한다.
- for 문을 돌려 배열을 탐색하는 것보다 빠르고 효율적으로 탐색을 진행할 수 있다.
- 속도가 빠르나, 값이 index로 쓰이기에 지나치게 인덱스가 크거나 인덱스가 음수로 가는 경우에는 사용하기 어려우며, 사용할 키값이 문자열일 경우에도 사용이 어렵다.
- 위의 맹점을 보완하기 위해 사용하는 방법은 다른 hash table(dictionary같이 key:value 구조를 갖는 것)이나 binary search tree가 있다.
- C++ 예시 코드

```C++
#include <iostream>
using namespace std;


int main() {
	char arr[9];
	cin >> arr;

	int dat[28] = { 0 };

	char max;
	int cnt = 0;

	for (int i = 0; i < 9; i++) {
		dat[arr[i]-'A'] += 1;

		if (arr[i] == '\0') {
			break;
		}

		if (dat[arr[i]-'A'] > cnt) {
			max = arr[i];
			cnt = dat[arr[i]-'A'];
		}
	}

	cout << (max);

	return 0;
}
```

## Hash Table(추가 조사 필요)

- 해시 테이블의 의의
- 보안 분야 관련 해시 테이블의 중요도
- 해시 함수를 사용할 때 중요한 것(충돌, 적재율)
- 충돌 처리 기법
