---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 힙 정렬 # 제목
excerpt             : 정렬 알고리즘 # 썸네일 한줄 요약
last_modified_at    : 2020-12-28 # 마지막 수정일
categories          : algorithm
tags                : Algorithm Sort DataStructure Heap
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [위키 - Heap (data structure)](https://en.wikipedia.org/wiki/Heap_(data_structure))

사용 언어 자바


## 힙 정렬

힙 정렬에 대해 알아보려는데 문득 그러고보니 힙이 뭘까?  

위키에 의하면 트리 기반의 자료구조로  
최대 힙은 부모가 자식들 보다 크고 최소 힙은 반대다  

아주 적은 시간복잡도로 힙을 만들수 있고  
항상 최고 기준의 노드가 최상위에 있다는 장점이 있다  

이런 힙 구조를 이용해 힙 정렬을 한번 구현해 보자  

### 순서

- 값 교환
- 부분 힙
- 완전 힙
- 정렬



### 배열내 값 교환 Swap

배열과 두 인덱스를 전달받아 범위 확인 후 값을 서로 교환한다

```java
private int[] swap(int[] array, int idxA, int idxB) {
    int temp = array[idxA];
    array[idxA] = array[idxB];
    array[idxB] = temp;
    return array;
}
```
    
### 부분 힙 만들기 (최대 힙 기준)

배열과 부모노드의 인덱스, 배열의 범위를 전달받아  
자식노드가 부모노드보다 크면 교환한다  
교환 후에는 하위 노드들과의 관계가 적합하지 않을수 있다  
재귀로 적합성을 확보한다  

우측 자식노드가 없을 수도 있으므로 유의하자  

```java
private int[] maxHeap(int[] array, int parent, int length) {
    int left = parent * 2 + 1;
    int right = parent * 2 + 2;
    int child = left;

    if (length <= left) return null;

    if ((length > right) && (array[left] < array[right])) child = right;

    if (array[parent] < array[child]) {
        swap(array, parent, child);
        maxHeap(array, child, length);
    }
    return array;
}
```

### 완전 힙 만들기

위에 만든 부모노드가 자식노드들을 확인하는 함수를 이용하면  
맨 밑바닥 노드들부터 확인할 필요없이 마지막 부모노드부터 확인하면 된다
배열을 완전이진트리로 봤을때 (길이 / 2) - 1이 마지막 부모의 인덱스가 된다  
마지막 부모노드부터 꼭대기까지(상향식) 순회하면서 완전한 힙을 만들어준다

```java
private int[] heapify(int[] array, int length) {
    //if (!validRange(array, 0, length - 1)) return null;
    for (int parent = length / 2 - 1; parent >= 0; parent--) {
        maxHeap(array, parent, length);
    }
    return array;
}
```

### 힙 정렬

완전한 힙은 최상단에 최고 기준의 노드가 있으므로  
해당 노드를 맨 뒤 노드와 교환하고 배열의 범위를 줄여 반복해주면  
최대힙의 경우 배열이 오름차 순으로 정렬이 된다  

```java
public int[] heapSort(int[] array) {
    for (int length = array.length; length > 0; length--) {
        heapify(array, length);
        swap(array, 0, length - 1);
    }
    return array;
}
```
