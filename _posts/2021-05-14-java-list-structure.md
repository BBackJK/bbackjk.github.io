---
date:  2021-05-14
title: '자바 List Interface'
categories:
  - java
tags: 
  - list
  - data structure
  - arraylist
  - likedlist

toc: true
toc_sticky: true

author_profile: true
sidebar_main: true
---

# 자바의 List Interface

오늘은 자바 리스트 인터페이스에 대해서 알아보자.

우선 들어가기 전 밑에 그림을 항상 기억하자.

어느 책에서든지 나오는 중요한 그림이지만 쉽게 잊어먹기 쉽고 가볍게 훑고가는 것이 대부분일 것이다.

왜 중요한가? 전체적으로는 ``OOP 관점에서 추상화에 대한 개념에 대해서도 공부가 가능``하기 때문이다.

![자바 콜렉션 인터페이스](/assets/img/java-list-interface/java-collection-interface-strcuture.png)


오늘 볼 것은 List interface 부분이다.

## List Interface

위에 사진에서 보았듯이 **Interface List**는 Collection을 **확장**하고 있다. 

![자바 리스트 인터페이스](/assets/img/java-list-interface/java-list-interface-pic-1.png)

> 여기서 보면 알 수 있듯이 interface끼리 상속하였을 경우는 **확장** 인 **extends**. interface를 상속받은 구현체(class)는 **implements** 를 사용

이 List Interface는 요소들의 순서를 저장하여 색인(index)를 이용하여 ``특정 위치에 요소를 삽입하거나 접근``이 가능.

이 List Interface의 구현체(클래스)로는 **ArrayList**, **Vector**, **LinkedList** 가 있다.

우선 배열에 대해서 알아보자.
<br/>

### 배열 (array)

이 배열은 정의와 동시에 길이를 지정하며 길이를 변경할 수 없다.

```java
int[] intArr = new int[4];

intArr[0] = 10;
intArr[1] = 20;
intArr[2] = 30;

System.out.println(intArr.length);
```

위와 같이 사용되며 길이는 변경 불가능하다 했으므로 sout으로 찍히는 문구는 '4'이다.

그럼 메모리적으로 보았을 때는 어떻게 되어있을까?

1. 우선 **new** 키워드를 이용하여 선언하였으므로 변수명 intArr은 Stack메모리에 **int[4]의 힙 메모리주소를 값으로 가진** 채로 들아기고
2. 힙 메모리에 int[4]가 할당된다. int형은 4바이트이므로 총 16바이트가 할당되며 4바이트까지는 10이, 8바이트까지는 20, 12바이트까지는 30이 할당되고 나머지 4바이트는 ``비어있는 채로 존재``하게 된다

그런데 우리는 데이터를 다루다 보면 항상 같은 크기의 데이터만을 다루는 것이 아니다.

그리고 만약 같은 크기의 배열을 다룬다고 할지언정 처음에 할당한 그 크기 만큼 사용하지 않는다면, 메모리의 낭비를 불러올 수 있다.

따라서, 이러한 한계를 벗어나기 위해 List interface의 구현체인 ArrayList, Vector, LinkedList 가 나왔다.

그렇다면 이제 하나, 하나 특징을 살펴보자.

<br/>

### ArrayList

상당히 빠르고 크기를 마음대로 조절할 수 있는 배열.

단방향 포인터 구조로 자료에 대한 순차적인 접근에 강점이 있음.

**내부적으로 배열(array)를 이용하여 요소를 저장한다.**

```java
// 기본적인 사용법 예시.
ArrayList<String> strList = new ArrayList<>();

strList.add("A");
strList.add("B");
strList.add("C"); // 요소 추가

strList.remove("A"); // Object로 접근하여 요소 삭제
strList.remove(0); // index로 접근하여 요소 삭제
```
<br/>

### Vector

ArrayList의 구형 버전, 모든 메소드가 동기화 되어있다.

> 잘 사용은 되질 않는다.

### LinkedList

양방향 포인터 구조로 데이터의 삽입, 삭제가 빈번할 경우 빠른 성능을 보장.
스택, 큐, 양방향 큐 등을 만들기 위한 용도로 사용.

> 사용법은 ArrayList와 비슷하다. 같은 List interface의 구현체이기 때문에.. ArrayList와는 다르게 구현되어있으므로 자세한건 찾아보면 좋다.

자 그럼 여기까지 각 List Interface의 구현체들의 특징에 대해서 알아보았다.

그럼, 이제 각 구현체를 비교하면서 특징을 좀 더 머리속에 넣어보자.

## ArrayList vs Vector

위에서 언급하였듯이 **Vector** 는 **ArrayList** 의 구형 버전이다.

그럼 어떤 것이 다르기에 구형 버전인 Vector가 그대로 떡하니 존재하는가?

- **동기화 (Synchronize)**

  Vector는 동기화.
  ArrayList는 동기화가 되지 않은 상태.

  무슨 의미인가 ? 

  Vector는 동기화가 되어서 ``한번에 하나의 스레드만`` 접근이 가능.

  ArrayList는 ``동시에 여러 스레드가 작업``이 가능.

  > ArrayList에서 여러 스레드가 동시에 엑세스하는 경우 개발자가 명시적으로 동기화하는 코드를 추가하여야 한다.

- **스레드 안전 (Thread Safe)**

  Vector는 동기화가 되어있으므로 한번에 하나의 스레드만 접근이 가능하므로 스레드가 **안전**하다.

  ArrayList는 동기화가 되어있질 않기 때문에 명시적으로 동기화할 필요가 있다. (위에서도 언급)

- **성능**

  ArrayList가 동기화 된 Vector보다 빠르다.

- **크기 증가**

  두 구현체 전부 동적 배열 클래스로 최대 인덱스를 초과할 때 추가되는 인덱스 수가 다르다.

  Vector의 경우 현재 크기의 100% 증가.
  ArrayList의 경우 현재 크기의 50% 증가.


> 결론적으로 여러가지를 종합하였을 경우 ArrayList를 사용하는 것이 바람직해 보인다.


## ArrayList vs LinkedList

둘 다 List interface의 구현체이지만, 추상화된 부모는 다르다.

사진을 보자.

![자바 arraylist extends](/assets/img/java-list-interface/java-array-list-example-1.png)

![자바 linkedlist extends](/assets/img/java-list-interface/java-linked-list-example-1.png)


보면 ArrayList는 ``AbstractList``를 확장하고 있고,

LinkedList는 ``AbstractSequentialList``를 확장하고 있다.


이게 무슨 의미냐?

ArrayList는 데이터(요소)들이 순서대로 쭉~ 늘어선 **배열의 형식** 을 취하는 반면,

LinkedList는 순서대로 늘어선 것이 아니라! **자료의 주소 값으로 서로 연결되어 있는 구조**를 하고 있다.

![자바 linkedlist arraylist 비교](/assets/img/java-list-interface/java-arraylist-linkedlist-example-1.png)


이러한 구조는 어떠한 것을 나타내는 것인가?

메모리 구조적으로 알아보자.

- **데이터를 찾는 경우**

  ArrayList는 배열의 확장이다. 배열처럼 색인(Index)를 가지고 있다. 이 의미는 시간복잡도가 O(1) 란 의미. 즉, **드럽게 빠르다.**

  LinkedList는 내부적으로 각 **노드** 들이 연결되어 있는 구조 이므로 데이터를 찾는 경우 제일 윗대가리(HEAD NODE) 에서 부터 해당 원소까지 차근 차근 읽어야 하기 때문에 O(n) 이다. 즉, ArrayList보다 느리다.

  > 크기가 그렇게 크지않다면 별 상관은 없지만. 이것도 무시할 수 없다.

- **데이터를 추가하거나 삭제하는 경우**

  ArrayList는 내부적으로 배열로 지정되어있으며, 기본 사이즈는 10이다.

  따라서 요소를 추가하는 연산을 하였을 때, 배열의 크기가 10보다 커진다거나, 그 이상으로 점차적으로 증가하였을 경우 **배열의 크기를 점진적으로 늘려주어야 하는 연산이 추가**적으로 들어가게 된다.
  
  따라서 O(n)의 시간복잡도가 소요.


LinkedList는 두 가지를 체크해야한다.

**일반적으로 추가하는 경우** 와 **시작이나 마지막에 추가하는 경우**.

* **일반적으로 추가하는 경우 (= 중간에 값을 추가하는 경우)**

  - 추가를 원하는 index에 도달할 때까지 순차 접근을 하므로 O(n)의 시간복잡도를 가지며, **index-1 노드의 next** 와 **index+1 노드의 prev** 를 새로 추가한 노드에 연결하는 작업은 n에 영향을 받지 않음.
  **따라서 O(n).**

* **시작이나 마지막에 추가하는 경우**

  - LinkedList는 위에 사진에도 보았듯이 HEAD와 TAIL을 동시에 가지고 있기 때문에 시작이나 마지막에 추가할 경우, O(1)의 시간복잡도를 가짐.



- **정리**


  | 메소드 | ArrayList | LinkedList|
  |:---:|:---:|:---:|
  |get / set| O(1)|O(n)|
  |add / remove (시작)|O(n)|O(1)|
  |add / remove (끝)|O(1)|O(1)|
  |add / remove (일반)|O(n)|O(n)|

> 상황에 따라 다르기 때문에 무조건 하나가 다른하나보다 빠르다 라는 개념이 아닌 시간복잡도를 가지고 생각해야 할 문제 인것 같다.


## 번외

실무에서 개발하거나 수많은 구글링 자료들 중 보면 리스트 구현체를 선언할 때 이렇게 되어있다.

```java
List<String> strList = new ArrayList<>();
```

왜 위에 같이 사용하고 밑에와 같이 사용하지 않을까?

```java
ArrayList<String> strList = new ArrayList<>();
```

처음에는 다른 사람이 이렇게 쓰니까, 아무 생각 없이 사용하곤 했는데.. 진짜 난 병신이다..

위에서부터 말했지만 List는 **인터페이스**이고 ArrayList는 **구현체** 이다.

즉, 위 코드의 (편의상 전자, 후자로 함) 전자, 후자 둘다 이상은 없지만 OOP 관점으로 보았을 때 ``전자`` 처럼 사용하는 쪽이 맞다.

왜 그런지 하나 예를 들어보자..

만약 이걸 보는 너가 인터페이스를 하나 만들었다고 가정하자.. (물론 이렇게 만들진 않겠지만..)

아래와 같이 말이다.

```java
public interface iamInterface {
  
  List<ExampleObject> getExampleObjectList(ArrayList<String> strArr);
}
```

그리고 너는 이 인터페이스에 대해서 구현체를 만들었다. (만든 코드는 생략하겠다. 인터페이스의 사용 목적에는 큰 영향이 없기 때문에)

인터페이스 이름을 보자.

String형의 ArrayList를 인자로 받고 그걸 구현체에서 처리하여서 ExampleObject형의 List를 반환한다.

그럼 이제 이 인터페이스를 **다른 사람** 이 사용한다고 생각해보자.

만약 ``A`` 라는 어떤 사람이 **LinkedList** 로 만들어진 배열을 통해서 ExampleObject형의 List를 얻고싶다..

그럼 이 A라는 사람은 만들어진 LinkedList를 가공해서 ArrayList로 변환한 뒤 인터페이스를 사용해야할 것이다..

너무 로직이 복잡해지지 않는가?

즉, ArrayList를 인자로 사용한다면 전달 인자는 **ArrayList만 허용이 되지만** 이걸 만약 아래와 같이 바꾼다면?

```java
public interface iamInterface {
  
  List<ExampleObject> getExampleObjectList(List<String> strArr);
}
```

이제 getExampleObjectList 메소드는 전달받는 인자의 타입이 ArrayList 던지, LinkedList 던지 , Vector 던지 상관없이 데이터를 전달할 수 있다.


이게 아무리 ``당연한 것`` 처럼 보여도 이런 사소한 생각 차이가 OOP의 특징을 나타낼 수 있는 코드인가, 아닌가가 결정된다고 생각한다..



# 마치면서..

너무 두서없이 쓴거 같은데 뭐 어떤가, 나만 일단 알아보면 됐지..^^;

타인을 위한 포스팅을 한다고 다짐하면 그 때 가서 다시 한번 공부하면서 다시 정리하도록 할 예정..

오늘은 List Interface에 대해서 알아보았다..

더불어 ``구현체``라는 개념과 ``추상화``에 대해서 아주 얕ㅡㅡㅡㅡㅡㅡㅡ게 훑어봤는데

다음 포스팅엔 ``다형성``에 관해서 포스팅할 예정인데, 다형성하면 나오는 **오버라이딩** 이 메모리적으로 어떻게 할당되면서 동작하는지 좀 알아볼 예정이다.

