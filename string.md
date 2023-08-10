# string

```<string>``` : 문자열을 다루는 라이브러리

## string의 선언

```c++
#include<iostream>
#include<string>
using namespace std;

int main(){
    string str1("test1"); 	// string의 선언 방법 1
    string str2 = "test2"; 	// string의 선언 방법 2
}
```

특징 : 

1. 문자의 끝에 null 문자 '\0' 가 포함되지 않는다.
2. 배열처럼 한 문자씩 다룰 수 있다.
3. string 클래스 끼리는 문자열을 합치는 것이 + 연산자 하나만으로 가능 하다.
4. 문자열을 사전순으로 정렬할 때도 string 변수를 사용하면 편하다.



## string의 멤버함수

다음과 같이 선언 되어있다고 가정을 한다.

```c++
#include<iostream>
#include<string>
using namespace std;

int main(){
    string str1("test1"); 	// string의 선언 방법 1
    string str2 = "test2"; 	// string의 선언 방법 2
}
```



### string의 index 접근

- 배열처럼 접근

  ex) str1[1] 는 'e'를 반환. 이 때 반환 되는 문자는 char 형

- .at(index) 

  ex) str1.at(1) 는 'e'를 반환. 이 때 반환 되는 문자는 char 형



### 문자열의 맨앞과 맨 끝 문자 반환

- front() : 맨 앞의 문자 반환

  ex) str1.front()는 't'를 반환

- back() : 맨 끝 문자 반환

  ex) str1.back()는 '1'을 반환



### String의 크기

- str1.size() 또는 str1.length() 를 사용한다.

  ex) str1.size() 는 5를 반환.

- capacity() : string 객체에 할당된 메모리 크기(bytes)를 반환

  ex) str1.capacity() 는 15를 반환한다. 만약 길이가 15를 넘어가면 capacity가 15 + 16 = 31 이된다.

  ​	size가 capacity 넘어설때마다 16의 크기가 증가한다. 길이가 31을 넘어가게되면 31 + 16 = 47로 된다.



### String 크기 재할당

- str1.resize(n) : string을 n만큼의 크기로 만든다. 만약 그 크기가 원래 사이즈 보다 작으면 남은 string을 버린다.

  ​				그 크기가 원래 사이즈 보다 크면 남는 공간을 빈칸으로 채운다.

  ex) str1.resize(3) -> "tes"

  + resize(n,'a') : string의 크기를 resize하고 남는 공간을 'a'로 채운다.

    ex) str1.resize(6) -> str1.resize(10,'b') --> "test1 bbbb"

- str1.shrink_to_fit() :  capacity(메모리)를 줄이는 함수. resize를 통해서 string의 size를 줄여도 capacity는 변화 하지 않는다. 그래서 스트링 길이에 비해 낭비 되고 있는 메모리를 줄이기 위해서 다시 capacity를 할당한다.

  ex) str2.resize(17) -> capacity : 31  =>  str2.resize(3) -> capacity : 31  => str2.shrink_to_fit() -> capacity : 15



### 메모리 사전 할당

- str1.reserve(n) : 문자열을 넣기 전, 사전에 n크기의 string이 들어올것이니 여기에 맞는 capacity를 할당 해달라는 함수이다. 보통 파일을 읽을 때 사용을하는데 while문에서 eof를 이용해서 반복적으로 파일의 끝을 읽게 된다. 이때 size가 계속 늘어나면 capacity를 늘리는 작업이 들어가게되고 여기서 비용이 발생하게 된다. 이를 방지하기위해 미리 메모리를 할당 하는 함수 이다.



### 문자열 삭제

- str1.clear() : 스트링에 들어가 있는 문자열을 지우는 함수 (size와 length는 0이 되고, capacity는 그대로 남게 된다.)

  메모리 해제가 아닌 문자열 값들을 삭제하는 함수.



### 문자열이 비었는지 확인

- str1.empty() : 스트링이 비었는지 확인하는 함수. 비었으면 true를 반환한다. 비었다는 기준은 size,length가 0이면 된다.



### 문자열 스타일 변경

- str1.c_str() : c++스타일의 string 무낮열을 c스타일의 문자열로 변경해준다.

  ex) str1.c_str() => "test1" -> "test1\0"



### 문자열 자르기

- str1.substr(index,len) : index에서 부터 len만큼 잘라서 반환. 기본적으로 len에는 npos라는 -1값이 들어가는데, 이는 문자열의 끝까지 자르겠다는 의미이다.

  ex) str1.substr(2,2) : "test1" -> "st"를 반환 / str1.substr(2) : "test1" -> "st1"를 반환



### 문자열 변경

- str1.replace(index, len, &str) : index위치에서 len길이 까지의 범위를 매개변수로 들어온 str 전체로 대체.

  ex) str1.replace(2,2,"asdf") => "test1" -> "teasdf1"



### 문자열 비교

- str1.compare(&str2) : 매개변수로 들어온 str2을 비교해서 같으면 0을 반환하고 , 다르면 0이 아닌값을 반환.

  매개변수로 들어온 str2값이 사전순으로 빠르면 음수반환, 느리면 양수반환

- str1.compare(index,len,&str2) : str1의 index부터 len만큼의 크기를 str2과 비교한다.

- str1.compare(str1_index,str1_len,&str2,str2_index,str2_len) : str1의 index부터 len만큼의 크기를 str2의 index부터 len만큼의 크기와 비교한다.



### 문자열 복사

- str1.copy(&arr, len, index) : 미리 선언된 c의 문자열 arr에 index부터 len크기만큼의 문자열을 복사해서 붙여넣는다.

  이 함수는 특이하게 len과 index의 위치가 변경되있고 반환값으로는 복사된 길이 즉, arr의 길이를 반환한다.

  이 함수를 진행하여 arr에 문자열을 부여 넣었을때 맨 마지막에 '\0'을 붙여주어야 한다.

  ex) char arr[10] , int arrLen = str1.copy(&arr,2,3) -> "t1"이 arr에 복사될 것이다.

  arr[arrLen] = '\0'을 하여 t1이 arr에 복사된다.



### 문자열 찾기

- str1.find(&str, index) : str1에서 index 부터 매개변수로 받은 str를 찾는다. 일치하는 부분의 첫번째 순서(index)를 반환한다.

ex) 문자열을 찾아 해당 인덱스를 출력하는 알고리즘

```c++
#include<iostream>
#include<string>
using namespace std;

int main(){
	string a = "aabcdfawfeabcasd";
    int pos=-1;
    while(1){
        pos = a.find("abc", pos+1);
        if(pos == -1) // 해당 문자를 찾지 못했을 때 -1을 반환한다.
            break;
       	cout << pos << " ";  // 출력 : 1 10
    }
}
```



### 문자열 붙이기, 빼기

 string은 +연산자를 이용하여 string끼리의 문자열 붙이기가 가능하다. 

또한 함수를 이용하여 함수를 호출하는 스트링의 맨뒤에 문자 한개를 붙이거나 뺄 수도 있다.

- str1.push_back('a') : str1의 맨뒤에 'a'를 붙인다. 

- str1.pop_back() :  str1의 맨뒤에 문자한개를 없앤다.



### String iterator

- str1.begin() :  문자열의 첫 번째 문자 가리킴. (포인터를 반환한다.)

- str1.end() : 문자열의 마지막 바로 다음을 가리킴. (포인터를 반환한다.)



### SWAP(서로 데이터 교체)

- swap(str1, str2) : str1과 str2를 바꾸는데 서로 참조(reference)를 교환해서 스왑을 진행한다.

  st1이 str2가 되고

  str2가 str1이된다.