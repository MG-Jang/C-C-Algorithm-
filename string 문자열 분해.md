# 문자열 분해

문자열을 분해해서 출력하는 방법에는 여러가지 방법이 존재한다.
이번 설명에서는 내가 찾아 본 방법중에서 가장 간단한 방법을 설명한다.

> sstream과 getline을 이용한 방법
```c++
#include<iostream>
#include<string>
#include<sstream>

using namespace std;

int main() {
	cout << "문자열 분리 시작:" << endl;
	string s = "hello ,worl d,C++";
	char sp = ','; //sp(sperate)의 경우 getline을 사용할때는 char형식만 가능, string은 불가능
	istringstream iss(s); // string의 문자를 분리하는 역할을 한다.
	string s_buf;
	while (getline(iss, s_buf, sp)) {
		cout<< '|' << s_buf << '|' << endl; // 분해 내용을 띄어쓰기까지 확인
	}
	return 0;
}
```

- 이때 istringstream 이란 문자를 분리하는 역할을 한다. <br>
아래 예제를 확인 하자
```c++
int main() {
	istringstream iss("test 123 aaa 456");
	string s1, s2;
	int i1, i2;
	iss >> s1 >> i1 >> s2 >> i2; // 공백을 기준으로 문자열을 parsing하고, 변수 형식에 맞게 변환

	cout << s1 << endl; // test 
	cout << i1 << endl; // 123
	cout << s2 << endl; // aaa
	cout << i2 << endl; // 456
}
```

- 즉 istringstream 이란 문자를 띄어쓰기 단위로 분해를 하게된다. 하지만 getline을 사용하게  되면 띄어쓰기 대신 지정한 요소를 기준으로 분해한다. 
  
- 단 getline의 경우 char형식(문자 한개)만 가능하고 sperate기준을 string이나 char에 문자 두개이상을 넣어서는 불가능 하다.