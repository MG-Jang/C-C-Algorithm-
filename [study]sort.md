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
참고 사이트: https://hsp1116.tistory.com/33

## O(n^2) Sort

### Selection Sort

- 가장 단순한 정렬 방법.
- 배열의 요소 n개를 모두 조회하여 가장 크거나 작은 원소를 찾고 해당 원소를 마지막 인덱스의 원소와 바꾼다. 이후 마지막 원소를 제외한 n-1 길이의 배열을 가지고 앞선 과정을 재차 거치며 전체 배열을 정렬하게 된다.
- 배열의 요소들을 비교하는 총 횟수는 n(n-1)/2 이며, 수행 시간은 모든 경우에 O(n^2)이다.
- 간소화된 코드

```c++
selectionSort(A[], n)     // A[1...n] 을 정렬
{
  for last <- n downto 2 {
    k <- theLargest(A, last);     // A[1...last] 중 가장 큰 수 A[k] 찾기
    A[k] <-> A[last];     // A[k]와 A[last]의 값을 교환
  }
}
```

- C++ 예시 코드

```c++

```

### Bubble Sort

- 왼쪽부터 이웃한 수를 비교하면서 순서 기준에 맞게 위치를 바꿔나가는 정렬 방법.
- 두 개의 Loop가 존재하며 바깥쪽의 Loop는 n-1번, 안쪽의 Loop는 last-1번 순환한다.
- 즉, 총 순환 횟수는 n(n-1)/2 이며, 수행 시간은 O(n^2)이 된다.
- 간소화된 코드

```c++
bubbleSort(A[], n)    // A[1...n] 을 정렬
{
  for last <- n downto 2
    for i <- 1 to last-1
      if(A[i] > A[i+1])
        then A[i] <-> A[i+1];   //원소 교환
}
```

- C++ 예시 코드

```c++

```

### Insertion Sort

- A[n]의 배열이 있을 때, 첫 요소부터 시작하여 요소를 하나씩 읽어가면서 해당 요소의 자리를 정렬 기준에 맞게 조정(삽입)하는 정렬 방법이다.
- 위 과정에서 위치 조정을 위해 요소가 중간에 삽입되면 해당 요소보다 큰 요소들은 뒤로 한 자리씩 밀리게 된다.
- 바깥 Loop는 n-1번 순환하며, 안쪽 Loop는 최대 i-1번 순환한다. 즉, 최악의 경우 순환 횟수는 n(n-1)/2이며, 최악의 수행 시간은 O(n^2)이다.
- 간소화된 코드

```c++
insertionSort(A[], n)
{
  for i <- 2 to n {
    loc <- i-1;
    newItem <- A[i];
    while(loc >= 1 and newItem < A[loc]) {
      A[loc+1] <- A[loc];
      loc--;
    }
    A[loc+1] <- newItem;
  }
}
```

- C++ 예시 코드

```c++

```

## O(nlogn) Sort

### Merge Sort

- A[n]의 배열을 반으로 나눈 뒤 각각을 정렬하고, 두 배열을 다시 하나로 합치는 과정의 정렬 방법이다.
- 합치는 과정에서는 나눠진 두 배열의 요소들을 정렬 기준에 따라 하나씩 추출하여 정렬한다.
- 병합은 선형 시간이 소요되며, 총 소요시간은 최악의 경우 O(nlogn)이 된다. (시간복잡도를 계산하는 과정은 생략...)
- 간소화된 코드

```c++
mergeSort(A[], p, r)      // A[p...r] 정렬
{
  if(p<r) then {
    q <- p와 r의 중간지점;
    mergeSort(A, p, q);
    mergeSort(A, q+1, r);
    merge(A, p, q, r);
  }
}

merge(A[], p, q, r)
{
  t <- p;
  j <- q+1;
  t <- 1;

  while(i<=q and j<=r) {
    if(A[i]<=A[j])
      then tmp[t++] <- A[i++];
    else
      tmp[t++] <- A[j++];
  }

  while(i<=q) {
    tmp[t++] <- A[i++];
  }

  while(j<=r) {
    tmp[t++] <- A[j++];
  }

  i <- p;
  t <- 1;
  while(i<=r) {
    A[i++] <- tmp[t++];
  }
}
```

- C++ 예시 코드

```c++

```

### Heap Sort

- 힙(Heap)이란 이진 트리의 자료구조로, 최소 힙과 최대 힙으로 나눌 수 있다.
- 힙의 특징
  - 마지막 레벨을 제외한 각 레벨의 노드는 모두 채워져야 한다.
  - 마지막 레벨에서는 왼쪽부터 채워져야 한다.
  - 최소 힙의 경우 부모 노드가 자식 노드보다 항상 작거나 같으며, 최대 힙의 경우 부모 노드가 항상 자식 노드보다 크거나 같다.
- 간소화된 코드

```c++
buildHeap(A[], n)   // A[1...n]을 힙으로 만든다.
{
  for i <- n/2 downto 1 {
    heapify(A, i, n);
  }
}

heapify(A[], k, n)    // A[k]를 루트로 하는 트리를 힙 성질을 만족하도록 한다. A[k]의 두 자식을 루트로 하는 서브 트리는 힙 성질을 만족하는 상태이다.
{
  left <- 2k;
  right <- 2k+1;

  if(right <= n) then {     // 자식 노드가 2개여서 right가 있을 경우
    if(A[left] < A[right]) {
      smaller <- left;
    } else {
      smaller <- right;
    }
  }
  else if (left <= n) {     // 자식 노드가 왼쪽에 하나만 있는 경우
    smaller <- left;
  }
  else {                    // A[k]가 리프노드
    return;
  }

  if (A[smaller] < A[k]) {
    A[k] <-> A[smaller];
    heapify(A.smaller.n);
  }
}

heapSort(A, n)      // A[1...n] 을 정렬
{
  buildHeap(A, n);
  for(i <- downto 2) {
    A[1] <-> A[i];
    heapify(A, 1, i-1);
  }
}
```

- C++ 예시 코드

```c++

```

### Quick Sort

- 평균적으로 가장 좋은 성능을 가진 정렬 알고리즘.
- 기준 원소를 두고, 기준 원소보다 작은 원소는 왼쪽에 큰 원소는 오른쪽에 두며 정렬한다. 마지막에는 작은 원소와 큰 원소 사이의 경계에 기준 원소를 위치시킨다.
- 최악의 경우에는 O(n^2)의 시간복잡도를 가지지만, 평균적으로 O(nlogn)의 시간복잡도를 가진다.
- 간소화된 코드

```c++
quickSort(A[], p, r)
{
  if(p<r) {
    q <- partition(A, p, r);
    quickSort(A, p, q-1);
    quickSort(A, q+1, r);
  }
}

partition(A[], p, r)
{
  x <- A[r];    // 기준원소
  i <- p-1;     // i는 1구역(기준 원소보다 작은 원소 그룹)의 끝지점
  for j <- p to r-1 {     // j는 3구역(아직 정렬되지 않은 원소 그룹)의 시작지점
    if(A[j] <= x) {
      A[++i] <-> A[j];
    }
  }
  A[i+1] <-> A[r];      // 기준 원소와 2구역(기준 원소보다 큰 원소 그룹) 첫 원소 교환
  return i+1;
}
```

- C++ 예시 코드

```c++

```
