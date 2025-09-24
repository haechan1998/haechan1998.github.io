---
title: "Java의 조건문과 반복문"
date: 2025-09-24 15:10:00 +0900
categories: [Java]
tags: [Java, Study]
toc: true
comments: true
---

# 배열이란?
* 배열(Array)은 같은 타입, 같은 의미를 가지는 변수를 연속적으로 저장하기 위한 자료구조이다.

* 배열은 여러개의 변수를 따로 선언하지 않고 하나의 이름으로 관리 가능하다.

```java
// 일반적인 변수 선언
int a = 10;
int b = 20;
int c = 30;

// 배열을 사용한 선언

// 배열의 선언 형태

int[] arr; // 배열이 선언만 된 상태(null) > 외부에서 배열을 가져올 경우에만 사용한다.
arr = new int[5]; // 선언한 객체를 생성(초기값 0)

int[] arr1 = new int[5]; // 선언 + 생성 + 자동초기화 // 일반적으로 많이 사용
int[] arr2 = new int[] {1, 2, 3, 4 ,5};
int[] arr3 = {1, 2, 3, 4, 5};

```

## 배열과 Index 구조
* 배열의 각 요소(element)는 인덱스(Index) 로 접근한다.

* Index 는 0 부터 시작한다.

* 배열의 길이는 `.length` 로 확인 가능하다.

*아래 이미지 참고.*

<img src="/assets/img/java/javaArrayIndex.png" alt="Java인덱스" width="600"/>

```java
int[] arr = {5, 10, 15, 20, 25};
System.out.println(arr[0]); // 5 index 0번지의 값
System.out.println(arr[3]); // 20 index 3번지의 값
System.out.println(arr.length); // 5
// legnth 는 index 가 아닌 실제 배열의 길이를 나타낸다.

```

## 배열에서 말하는 주소(Address) 란 무엇일까?
자바에서 배열은 **객체(Object)** 입니다.

배열 변수를 선언하면, 그 변수는 배열 데이터 자체를 담는 것이 아니라 **배열이 저장된 메모리 위치(주소)** 를 가리킵니다.

즉, 배열 변수는 참조변수(Reference Variable) 이고, 배열은(Heap) 메모리에 생성됩니다.

**Heap 메모리란?**

모든 쓰레드를 공유하며, 런타임중에 new 연산자를 통해 객체를 동적으로 생성하는 영역이며, Garbage Collector가 참조되지 않는 메모리를 확인하고 제거하는 영역입니다.

이때 배열의 실제 객체는 Heap 영역에 저장되고, 변수 `int[] arr`은 스택에 저장되며 Heap 영역 객체의 주소값을 참조합니다.

## 자료형 배열과 문자열 배열
배열은 크게 자료형 배열과 문자열 배열로 나타낸다.

```java
// 자료형 배열
int[] intArray = {1, 2, 3, 4};
double[] doubleArray = {1.1, 2.2, 3.3};

// 문자열 배열
String[] strArray = {"Java", "DB", "Spring", "Javascript"};
System.out.println(strArray[2]); // Spring

```

## 배열의 얕은 복사(Shallow Copy), 깊은 복사(Deep Copy)
위 내용을 기반으로 배열에 대한 복사를 알아봅시다.

배열의 복사는 크게 얕은 복사, 깊은 복사로 나눠져있습니다.

### 1. 얕은 복사(Shallow Copy)

주소값만 복사하며 두 변수가 같은 배열 객체를 참조합니다.

따라서 한쪽을 수정하면 다른쪽도 함께 수정됩니다.

```java
int[] original = {1, 2, 3};
int[] shallowCopy = original; // 주소만 복사됨

shallowCopy[0] = 99;

System.out.println(original[0]);    // 99 {99, 2 ,3}
System.out.println(shallowCopy[0]); // 99 {99, 2, 3}

// 하나의 변수만 변경해도 두 변수가 같이 수정되는 모습이다.

```

### 2. 깊은 복사(Deep Copy)
배열의 값 자체를 새로 복사하는 형식이며, 원본 배열과 복사본 배열이 서로 독립적입니다.

반복문을 통해 복사하는것이 일반적이만, 1차원 배열은 `.clone()` 을 통해 복사 할 수 있습니다.

```java
int[] original = {1, 2, 3};
int[] deepCopy = original.clone();  // 깊은 복사

deepCopy[0] = 99;

System.out.println(original[0]); // 1 {1, 2, 3}
System.out.println(deepCopy[0]); // 99 {99, 2, 3}

```

**반복문만을 사용한 2차원 배열의 깊은 복사**

```java
int[][] arr = {% raw %}{{1, 2}, {3, 4}}{% endraw %};

int[][] deepCopy = new int[arr.length][]; // 배열의 행 크기 결정

for(int i = 0; i < arr.length; i++) {
    deepCopy[i] = new int[arr[i].length]; // 행 내부 배열의 크기 결정
    for(int j = 0; j < arr[i].length; j++) {
        deepCopy[i][j] = arr[i][j];
    }
}
deepCopy[0][0] = 50;
System.out.println(Arrays.deepToString(deepCopy)); // [[50, 2], [3, 4]]
```

### 정리
**배열(Array)** 은 같은 자료형의 데이터를 연속적으로 저장할 수 있는 자료구조로, 인덱스를 통해 각 요소에 접근할 수 있습니다. 배열은 선언 시 크기가 고정되며, 생성된 배열은 Heap 영역에 저장되고, 변수는 해당 배열의 **주소값(참조값)** 을 스택에 보관합니다. 따라서 배열 변수를 복사하면 실제 값이 아니라 주소가 전달됩니다.

이렇기 때문에 배열을 복사할 경우에는 단순히 주소값만 복사되지 않도록 **얕은복사** 의 개념과 **깊은복사**의 개념을 숙지하여 의도하지 않은 데이터 변경을 방지하도록 해야합니다.











