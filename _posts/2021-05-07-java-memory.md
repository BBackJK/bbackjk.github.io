---
date:  2021-05-07
title: '자바 메모리 할당'
categories:
  - java
tags: 
  - stack
  - heap
  - memory

toc: true
toc_sticky: true

author_profile: true
sidebar_main: true
---


# 자바의 자료형

자바의 자료형에는 기본형 (Primitive Type)과 참조형 (Reference Type)이 존재.

* **자바의 기본형 (원시형 = primitive type)**

1. byte (1 byte)
2. short (2 bype)
3. int (4 byte)
4. long (8 byte)
5. float (4 byte)
6. double (8 byte)
7. char (2 byte)
8. boolean (1 byte)

> 각 원시형마다 바이트 크기는 중요..!
> 자주 사용하는 String은 기본형이 아니다..!
> 또한 이러한 원시형은 null 값을 가질 수 없다..!

<br/>

* **자바의 참조형 (Reference Type)**

자바의 참조형은 원시형이 ``아닌`` **new로 생성된** 데이터 타입을 참조형이라고 한다.

예를 들어, 자주 사용하는 String 은 다음과 같이 사용할 때

```java
String a = "hello world";
```

내부적으로는

```java
String a = new String("hello world");
```

와 같이 동작한다.

**즉, 자바에서는 기본형(=원시형)을 제외한 나머지는 모든 객체가 클래스타입 (참조형) 이다.**


# 각 타입별 할당

자 그럼 이제 기본형과 참조형의 메모리 할당에 대해서 알아보자.

## 기본형

기본형(=원시형)은 변수를 선언하게 되면 ``Stack 메모리 영역에 할당``되어진다.

그리고 그 메모리에는 stack메모리의 주소값과 실제 할당되어진 값이 저장된다.

> stack메모리의 주소값은 컴퓨터가 이 주소값을 알아야 할당된 값에 접근이 가능하다.

자주사용하는 int형으로 예를 들어보자.

```java
int a = 128;
int b = 128;

System.out.println(a == b);
```

각 변수 a, b에 '128' 이라는 값을 각각 할당하였다.

원시형에 값 128을 할당하였으므로

변수 a, b는 Stack 메모리 영역에 할당되어진다.

다음과 같이
![메모리할당 예제1](/assets/img/java-memory/primitive-memory-allocation-example-1.png)

자 그럼 ``a == b``는 어떤 값이 출력될까?

두 개의 값을 비교하므로 답은 **true** 이다.

<br/>

## 참조형

참조형은 기본형을 제외하며, ``new`` 연산자로 생성된 모든 클래스 객체를 의미한다.

그럼 어떻게 메모리에 할당되어지는지 보자.

```java
public class Test {
  private int data;

  public Test(int data) {
    this.data = data;
  }

  public void print() {
    System.out.println(this.data);
  }


  public static void main(String[] args) {

    Test test = new Test(10);

    test.print();
  }
}
```

여기서 주목해야할 것은 new 연산자로 할당된 부분이다.

```java
Test test = new Test(10)
```


이 라인은 다음과 같이 할당되어진다.

![reference-memory-allocation-example](/assets/img/java-memory/reference-memory-allocation-example-1.png)

즉, ``new Test(10)`` 은 **힙 메모리에서의 주소값**이라고 생각하면 쉽다.


그래서 만약.. 다음과 같이 한다면..

```java
public class Test {
  private int data;

  public Test(int data) {
    this.data = data;
  }

  public void print() {
    System.out.println(this.data);
  }


  public static void main(String[] args) {

    Test test = new Test(10);

    Test test2 = test;

    test.print();
  }
}
```

**변수 test** 에는 int data = 10으로 할당된 **Test 객체의 힙 메모리 주소값** 이 들어가 있어서 이 힙 메모리 주소값을 그대로 타입이 Test인 변수 test2에 대입한다면

다음과 같이 되어진다.

![reference-memory-allocation-example](/assets/img/java-memory/reference-memory-allocation-example-2.png)


즉, ``같은 힙 메모리의 주소값을 공유``하는 것이다.


<br/>

## 번외


자 그럼 기본형(=원시형)인 **int** 의 **wrapper class** 인 **Integer**로 선언하면 어떻게 되는지 보자.

Integer 객체 a, b에 각각 128이라는 값을 저장하고 두 객체를 비교해본다면?

```java
Integer a = 128;
Integer b = 128;

System.out.println(a == b);
```

출력값은 **false** 이다.

Integer는 Int형의 Wrapper Class 이므로

다음과 같이 할당되어 진다.


![reference-memory-allocation-example](/assets/img/java-memory/reference-memory-allocation-example-3.png)

즉, a와 b는 각각 다른 힙 메모리의 주소값을 ``참조``하고 있으므로 **false** 이다.

<br/>

그럼 이건 어떻게 될까?


```java
Integer a = 127;
Integer b = 127;

System.out.println(a == b);
```

놀랍게도 답은 **false**가 아닌 **true** 이다.

이렇게 나오는 이유를 알려면 **Integer**라고 하는 wrapper class가 어떻게 동작하고 있는지 알아야한다.

자 그럼, Integer 클래스를 파헤쳐보자.

![integer-wrapper-class-example](/assets/img/java-memory/integer-example-1.png)

위에서부터 천천히 보면은 **최솟값** 과 **최댓값** 이 차례대로 상수형태로 지정해놓은 것을 볼 수 있다.

자 그럼.. 밑으로 내려가서 보다보면 아래와 같은 코드를 볼 수 있다.

![integer-wrapper-class-example](/assets/img/java-memory/integer-example-2.png)

보면 이렇게 나와있다

> 지정된 int 값을 나타내는 Integer 인스턴스를 반환합니다. 새 인스턴스가 필요하지 않은 경우! 이 메소드는 자주 요청되는 값을 **캐싱** 하여 더 나은 공간 및 시간 성능을 제공하므로 Integer(int) 생성자 보다 이 메소드를 사용하셔야 합니다. 이 메소드의 범위는 -128 ~ 127 의 범위의 값을 캐시합니다.

자 답은 나온 것 같다.

즉 사진에 나와있는 ``if문`` 이 true라면 (= **IntegerCache** 의 최솟값(?)과 최댓값(?) 의 사이라면) ``캐시된 값을 리턴`` 해 주고, 그렇지 않다면 **new 연산자** 를 활용하여 새로운 객체를 반환해준다.

<hr/>

기본형(=원시형)과 참조형이 메모리에 어떻게 할당되어지는지 구체적이라면 구체적으로.. 대략적이라면 대략적으로.. 알아보았다.

사실 아직 객체 안에 멤버변수로 다른 객체가 계속 해서 있는 경우는 어떻게 참조되어지는지 **정확하게는 모르겠다..^^;**

> 대충은 알겠지만..

다음에는 메모리 할당을 배운 것을 활용하여 ``call of value`` 와 ``call of reference`` 를 알아보거나 번외로 한 Wrapper Class에 대해서 알아볼수도 있겠다.. 나도 내가 무엇을 하고 싶을지 몰라..

