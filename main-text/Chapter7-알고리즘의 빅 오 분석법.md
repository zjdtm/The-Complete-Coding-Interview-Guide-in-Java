# 알고리즘의 빅 오 분석법
>알고리즘(영어: algorithm), 셈법은 수학과 컴퓨터과학, 언어학 또는 엮인 분야에서 어떠한 문제를 해결하기 위해 정해진 일련의 절차이다.
 계산을 실행하기 위한 단계적 절차를 의미하기도 한다. 즉, 문제 풀이에 필요한 계산절차 또는 처리과정의 순서를 뜻한다.
 -출처 : 위키백과 -
 
이처럼 문제에서 패턴을 찾아내서 이 패턴을 토대로 문제를 해결하는 절차를 **알고리즘**이라고 한다.

**빅오 표기법 (Big Onotation)** 이란 알고리즘의 효율성을 표기해주는 표기법이다.

## 유추

인터넷에서 좋아하는 해리포터 영화를 발견하였습니다. 영화는 주문하거나 다운로드 할 수 있는데
주문을하면 도착하기까지 하루 정도 걸리고 다운로드는 반나절이 걸립니다.
그러면 당연히 다운로드를 선택할 것입니다. 하지만 해리포터를 다운로드 하려던 찰나에 어벤져스 패키지를 발견하여서
어벤져스도 다운로드 하기로 하였습니다. 이렇게 되면 총 4개의 영화를 다운로드하는데 총 이틀 정도 걸립니다.
하지만 주문을 한다면 똑같이 하루밖에 걸리지 않습니다. 그렇다면 주문을 하는 것이 더 빠릅니다.

위에 예시처럼 품목을 몇개를 주문하든 상관없이 배송 시간은 일정하게 유지되는데 이것을
**O(1) 또는 상수시간** 이라고도 합니다. 
또한 다운로드 시간이 파일 수에 정비례하는데 이것은 **O(n) 또는 점근적 실행 시간**이라고 합니다.

## 빅 오 시간 복잡도

![image](https://user-images.githubusercontent.com/35757620/213962361-5c493fc0-ee5b-4887-8e80-87d3f6a002d3.png)
-출처 : https://en.universaldenker.org/exercises/367 -

O(n!), O(n^2)은 **성능이 끔직**하여서 이 영역의 바깥쪽에 해당하는 알고리즘을 작성하려고 노력해야 한다.
O(nlogn)이 O(n!)보다는 낫지만 여전히 **성능은 나쁘다**. O(n)은 **괜찮은 성능**을 보이지만 O(logn)과 O(1)이 **좋은 성능**을 보인다.

## 빅 오 관련 예제

빅 오의 기본 규칙
- 상수는 제외한다 : 입력 크기가 n이라고 가정하면 n이 증가함에 따라 상수를 제외할 수 있다.
- 비우세항은 제외한다 : 우세항은 입력의 크기가 증가함에 따라 가장 빠르게 증가하는 항이다. 상수를 제외하는 것과 같이 
  비우세항도 제거거 가능하다.
  > f(n) = n^2 + 5n + 200 
    n^2가 더 중요하므로 5n + 200은 삭제가 가능하다.
- 입력이 다르면 변수도 다르다 : 
- 서로 다른 단계를 종합하거나 곱한다.
### O(1) 예제
```java
  
  return 23;
  //상수를 반환하므로 빅 오는 O(1)이다.
  
  int thirdCar = cars[3];
  //배열의 요소 개수와 관계없이 특정 인덱스에서 요소를 가져오는 작업은 
  //상수 연산이다. 따라서 인덱스를 활용해서 배열에 접근하는 시간은 O(1)이다.
  
  Car car = cars.peek();
  //큐의 peek 메서드는 큐의 첫 번째 요소를 검색하지만 제거하지는 않습니다.
  //peek 메서드를 통해 헤드를 검색하는 시간은 O(1)입니다.
```

### O(n) - 선형 시간 알고리즘 예제
```java
  for(int i = 0; i < a.length; i++) {
    System.out.println(a[i]);
  }
  // 빅 오를 결정하려면 'for 문이 몇 번 반복되었는지를 확인'하면 된다.
  // 시간은 주어진 배열(입력)의 크기에 따라 선형적으로 증가한다.
  // 따라서 시간 복잡도는 (O.length) 또는 O(n)으로도 표기한다.
```

### O(n) - 상수 제외 예제
```java
  for(int i = 0; i < a.length; i++){
    System.out.println("Current element:");
    System.out.println(a[i]);
    System.out.println("Current element + 1:");
    System.out.println(a[i]+1);
  }
  // 실행 시간은 입력 크기인 a.length에 관해 선형적이다.
  // 그래서 빅 오는 O(n)이다.
```

### 비우세항 제외 예제
```java
  for(int i = 0; i < a.length; i++){
    System.out.println(a[i]);
  }
  
  for(int i = 0; i < a.length; i++){
    for(int j = 0; j < a.length; j++){
      System.out.println(a[i] + a[j]);
    }
  }
  
  // 첫 번째 for 문은 O(n) 시간 두 번째 for 문은 O(n^2) 시간에 실행된다.
  // 따라서 O(n) + O(n^2) = O(n + n^2) 이라 생각할 수 있지만
  // 배열의 크기가 커지면 n^2이 n보다 증가율에 훨씬 더 많은 영향을 미치기 때문에
  // n은 관련이 없어서 제외가 가능하다.
```

### 입력 데이터가 다르면 변수도 다르게 설정 예제
```java
 for(int i = 0; i < a.length; i++){
 
 }
 
 for(int i = 0; i < a.length; i++){
 
 }
```

```java
 for(int i = 0; i < a.length; i++){
 
 }
 
 for(int i = 0; i < b.length; i++){
 
 }
```

두 개의 코드에 빅 오를 표기하면
첫 번째 코드에는 동일한 배열 a를 for문으로 두 번 실행하였기 때문에 O(n)으로 표기
두 번째 코드에는 서로 다른 배열 a와 b를 for문으로 각 각 실행한다.
이 때 빅 오는 두 for 문의 실행 시간을 반드시 모두 반영해야 하기 때문에 O(a+b)로 표기한다.

### 서로 다른 단계의 합 또는 곱

```java
 for(int i = 0; i < a.length; i++){
  System.out.println(a[i]);
 }
 
 for(int j = 0; j < b.length; j++){
  System.out.println(b[j]);
 }
```

```java
 for(int i = 0; i < a.length; i++){
  for(int j = 0; j < b.length; j++){
   System.out.println(a[i] + b[j]);
  }
 }
```

두 개의 코드에 빅 오를 표기하면
첫 번째 코드에는 2개의 for 문의 실행 시간을 각 각 더해서 O(a+b)로 표기한다.
두 번째 코드에는 배열 a의 각 요소 a[i]에 관해 배열 b를 순회하기 때문에 두 실행 시간을 곱한 O(a*b) 로 표기한다.

### logn 실행 시간 예제

logn 실행 시간을 알기 위해서는 이진 검색 알고리즘을 살펴보면 된다.
> 이진 검색 알고리즘 : 정렬된 리스트에서 특정 요소를 찾으려고 할 때 리스트의 중간 값을 선택 후 중간 값과 크고 작음을 비교하면서 값을 찾는 알고리즘
  ![image](https://user-images.githubusercontent.com/35757620/214208061-d60128bf-4b0d-4cfc-8436-c9a1066ee8a9.png)
  - 출처 : https://commons.wikimedia.org/wiki/File:Binary_Search.png -

만약 16개의 요소에서 값을 찾는다고 가정하면
16 / 2 = 8
8 / 2 = 4
4 / 2 = 2
순으로 요소가 점차 줄어든다. 이를 빅 오로 표현하면 다음과 같다.

$16 * (\frac{1}{2})^{4} = 1$

배열의 크기를 n, 단계 수를 k라고 하면

$n * (\frac{1}{2})^{k} = 1$ -> $2^{k} = n$ -> $\log_{2} n = k$

빅 오를 표현할 때 로그의 밑은 표현 하지 않아서 O(logn) 이다.

### 재귀 실행 시간 예제

```java
 int fibonacci(int k) {
  if (k <= 1){
   return k;
  }
  return fibonacci(k - 2) + fibonacci(k - 1);
 }
```
코드의 빅 오를 표기하면 $O(n^{2})$ 로 생각했지만

트리로 표현하면 차수는 각 노드가 지닌 가지의 개수 (2) 깊이는 k이다.

이럴 때는 $O(차수^{깊이})$로 표현한다.

따라서 $O(2^{n})$ 이다.

### 이진 트리의 중위 순회
포화 이진 검색 트리는 모든 노드가 정확히 2개의 자식 노드를 가지며, 모든
단말 노드가 같은 수준이나 깊이에 있는 이진 검색 트리입니다. 
다음 코드를 빅 오로 표기한다면 
```java
 void printInOrder(Node node){
  if(node != null){
   printInOrder(node.left);
   System.out.print(" " + node.element);
   printInOrder(node.right);
  }
 }
```
$O차수^{깊이} 입니다. 

포화 이진 트리는 깊이가 로그이기 때문에 빅 오로 표기한다면 $O(2^{logn})$으로 표기할 수 있다.

따라서 빅 오는 다음과 같이 나타낼 수 있다.

$2^{logn} = X$ -> $\log_{2}X$ -> $X = n$ -> $O(X) - O(n)$

* 포화 이진 검색 트리는 좀 더 공부를 하고 수정하겠다 *

### n 의 변동

```java
 void printFibonacci(int k) {
  for(int i = 0; i < k; i++){
   System.out.println(i + ": " + fibonacci(i));
  }
 }
 
 int fibonacci(int k){
  if(k <= 1){
   return k;
  }
  return fibonacci(k - 2) + fibonacci(k - 1);
 }
```

위 코드의 빅 오를 표기한다면
먼저 fibonacci 메서드의 빅 오는 $O(2^{n})$이다.
printFibonacci 메서드는 fibonacci 메서드를 n번(코드에서는 k번) 호출하므로
전체 빅 오는 $O(n) * O(2^{n}) = O(n2^{n})$ 이라고 생각할 수 있지만 
실행 과정을 살펴보면 그렇지 않다는 것을 알 수 있다.

$i = 0 -> fibonacci(0) -> 2^{0}$ 

$i = 1 -> fibonacci(1) -> 2^{1}$  

$i = 2 -> fibonacci(2) -> 2^{2}$  

...
     
$i = k - 1 -> fibonacci(k) -> 2^{k-1}$

이 처럼 동일한 코드를 n번 실행한다고 할 수 없기 때문에 빅 오는 $O(2^{n})$이다.

### 메모이제이션
 
```
