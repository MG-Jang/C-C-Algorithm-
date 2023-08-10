
# string <-> 숫자(int형) 변환

string을 숫자로 단숫히 변경하기는 어렵지는 않지만 손이 많이 간다. 예를 들어 1234 라는 string 을 숫자로 변경하기 위해서 1*1000 + 2*100 + 3*10  +4 이런 식으로 계산해야한다. 이를 간단하게 해결해줄 두가지 함수를 소개하겠다.

- string -> 숫자:  stoi()
- 숫자 -> string: string_to()

아래 예시를 통해 확인하자
```c++
string ss; 
ss += '1';
ss += '2';
ss += '3';
cout << typeid(ss).name() <<": " << ss << endl;
int k = stoi(ss);
cout << typeid(k).name() << ": " << k << endl;
string s_num = to_string(k);
cout << typeid(s_num).name() << ": " << s_num << endl;
```
출력:
```
class std::basic_string<char,struct std::char_traits<char>,class std::allocator<char> >: 123
int: 123
class std::basic_string<char,struct std::char_traits<char>,class std::allocator<char> >: 123
```
* 참고: string은 typeid 로 확인한경우 위 출력과 같이 string이 아닌 다른 방식으로 표현된다.