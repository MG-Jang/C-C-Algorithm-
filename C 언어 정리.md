# C 명령어 정리

아래 내용은 c++와 다른 c의 문법만을 다룬 내용 입니다.

- 참고: c를 컴파일 할때 scnaf가 오류 발생 2가지 해결법<br>
 1. #define _CRT_SECURE_NO_WARNINGS
 2. sdl 컴파일 검사 -> 아니오로 변경
 3. 
> 출력 printf

||||
|---|---|---|
|%c|하나의 문자|
|%s|문자열|
|%d|부호 있는 10진 정수|
|%i|부호 있는 10진 정수 (%d와 동일)|
|%f|고정 소수점으로 표현한 실수 (소수점 이하 6자리까지 표현)|
|%lf| double형 자료에 사용|
|%o	|부호 없는 8진 정수|
|%u	|부호 없는 10진 정수|
|%x	|부호 없는 16진 정수|
|%x	|부호 없는 16진 정수(소문자로 출력)|
|%X	|부호 없는 16진 정수 (대문자로 출력)||
|%02X	|부호 없는 16진 정수 |1이 01로 출력|
|%e	|부동 소수점으로 표현한 실수 (e-표기법)|
|%E	|부동 소수점으로 표현한 실수 (E-표기법)|
|%g	|값에 따라 %f나 %e를 사용함.|
|%G	|값에 따라 %f나 %E를 사용함.|
|%%	|퍼센트(%) 기호 출력|

> 입력 scanf
-  scanf는 입력받는 변수에 & 를 붙여야함 ex) scanf("%d", &num)
-  문자열 입력시 변수를 char 배열로 선언
```C
char ch1[10];
scanf("%s", &ch1);
printf("%s", ch1);
```
> 입력 gets
- 문자열만을 입력받음
- enter만 눌러도 입력으로 간주 
  - 모든 입력 뒤에 \n을 입력하기 때문
```C++
char str[100];
gets(str);
printf("%s",str);
return 0;
```


> 문자열 비교
- 헤더파일 <string.h> 추가
- strcmp 문자열 비교
```C
char str1[10] = "abce";
char str2[10] = "abcd";
int n; 
n = strcmp(str1, str2);
printf("%d", n);
// str1 < str2 인 경우에는 음수 반환
//str1 > str2 인 경우에는 양수 반환
// str1 == str2 인 경우에는 0을 반환
```
- 대소문자 구별 없이 하고 싶다면
  - strcmpi 사용



###  strlen 문자열 길이 <hr>
```C
ptr[10] = "ABC";
strlen(ptr);  // 결과: 3
```
###  strcat 문자열 붙이기 <hr>
```C
strcat(vect1,vect2);
// vect1 + vect2 문자열
```
###  strcpy 문자열 삽입 <hr>

```C
strcpy(dest, origin);
// dest 안에 origin을 넣는다.
```

###  strstr 문자열안에 문자열검색 <hr>
```C
 char *ptr = strstr(s1, "den");      
 // den으로 시작하는 문자열 검색, 포인터 반환
```

> strct 구조체  사용방식차이
```C
struct node {
	char name[10];
	int age;
};
// C++의 경우 using namspace std; 때문에 사용시 struct 를 쓰지 않아도 되지만
// C의 경우 아래와 같이 struct를 써야한다.
int main(){
struct node tmp;
return 0;
}
```