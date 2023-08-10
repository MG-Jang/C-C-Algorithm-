# while 사용

while 문은 무한루프를 사용하거나 특정 조건을 만족할 때 까지 루프를 돌리는 경우 사용된다. 다만 사용하면서 약간 착각이 들만한 부분들이 존재한다.

> while문 무한 루프는 어떤 숫자든 다 가능한가?

과연 아래 구문들은 모두 무한 루프일까? -> 예 
- 왜냐하면 while 문은 0이상의 상수에서 무한 루프가 돌아간다.
- 단 0 이하가 되면 0, -1, -0.01 무한 루프는 종료된다.
```c++
while(2) cout << "hi" ; 
while(0.1) cout << "hi" ; 
```

> while문은 언제 종료 될까??

아래코드를 확인해보면 0hi까지 출력이된다. 즉 while문의 가장 아래까지 실행후
while문 안의 조건을 확인한다. 즉 아래 두번째 식과 동일한 의미를 가진다.

```c++
int k = 3;
while(k--) {
    cout <<  k ;
    cout << "hi"  << endl;
} 

/* 정답
2hi
1hi
0hi 
*/

while(1){
    if(k <= 0) break;
    cout << k;
    cout << "hi"  << endl;
}
```

> do while

아래 코드를 무조건 한번 실행 시킨후 while문을 실행

``` C
int main()
{
    int i = 0;

    do     // 처음 한 번은 아래 코드가 실행됨
    {
        printf("Hello, world! %d\n", i);    // Hello, world!와 i의 값을 함께 출력
        i++;                                // i를 1씩 증가시킴
    } while (i < 100);    // i가 100보다 작을 때 반복. 0부터 99까지 증가하면서 100번 반복

    return 0;
}

```