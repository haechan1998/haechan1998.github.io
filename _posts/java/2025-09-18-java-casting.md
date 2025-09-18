---
title: "Java의 Casting과 자료형"
date: 2025-09-18 16:00:00 +0900
categories: [Java]
tags: [Java, Study]
toc: true
comments: true
---

# Java의 Casting이란?

Java에서 **Casting(형 변환)**이란 변수의 타입을 다른 타입으로 변환하는 것을 의미합니다.  
형변환을 통해 서로 다른 데이터 타입 간 연산이나 메서드 호출을 원활하게 할 수 있습니다.

---

## 1. 기본 타입 간 Casting

기본 타입 간 크기 비교


<img src="/assets/img/java/java자료형.png" alt="Java자료형" width="600"/>

위 자료를 참조하여 **byte < short < char < int < long** 라는걸 알 수 있다.


### 1-1. 묵시적 형변환 (Implicit Casting)

작은 타입 &rarr; 큰 타입으로 변환될 때 **자동으로 변환**됩니다.


```java
int num = 100;
long bigNum = num; // int → long 자동 형변환
double d = num;    // int → double 자동 형변환
```
### 1-2. 명시적 형변환 (Explicit Casting)

큰 타입 &rarr; 작은 타입으로 변환될 때
직접 명시해서 형 변환 하는것
```java
// double -> int
double num = 3.14;
int bigNum = (int) num; // 3
// 기존 소수점은 사라지고 정수만 남는다.
```

## 2. 문자열 <> 숫자 변환

웹에서 넘어오는 데이터는 "문자열" 로만 들어오기 때문에 변환을 해줘야합니다.
```java
String str = "1234";
int strNum = Integer.parseInt(str);
System.out.println(strNum + 10); // 1244 (자료형)
System.out.println(str + 10); // 123410 (문자열)
		
// 숫자를 문자로
int NumStr = 123456;
String numStr2 = String.valueOf(NumStr);
System.out.println(numStr2 + 10); // 12345610 (문자열)

```

## 3. Casting 주의점 

1. 데이터 손실 가능 : 큰 타입 &rarr; 작은 타입 변환 시 손실 가능

2. 가능한 업캐스팅 사용 권장, 다운캐스팅 최소화
