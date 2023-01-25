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
**$O(1)$ 또는 상수시간** 이라고도 합니다. 
또한 다운로드 시간이 파일 수에 정비례하는데 이것은 **$O(n)$ 또는 점근적 실행 시간**이라고 합니다.

## 빅 오 시간 복잡도

![image](https://user-images.githubusercontent.com/35757620/213962361-5c493fc0-ee5b-4887-8e80-87d3f6a002d3.png)
-출처 : https://en.universaldenker.org/exercises/367 -

$O(n!) (팩토리얼 시간), O(n^{2}) (제곱 시간)$은 **성능이 끔직**하여서 이 영역의 바깥쪽에 해당하는 알고리즘을 작성하려고 노력해야 한다.

$O(nlogn) (로그시간)$이 $O(n!)(팩토리얼 시간)$보다는 낫지만 여전히 **성능은 나쁘다**.

$O(n) (선형 시간)$은 **괜찮은 성능**을 보이지만 $O(logn) (로그 시간)$과 $O(1) (상수 시간)$이 **좋은 성능**을 보인다.

## 빅 오 관련 예제

빅 오의 기본 규칙
- 상수는 제외한다 : 입력 크기가 n이라고 가정하면 n이 증가함에 따라 상수를 제외할 수 있다.
- 비우세항은 제외한다 : 우세항은 입력의 크기가 증가함에 따라 가장 빠르게 증가하는 항이다. 상수를 제외하는 것과 같이 비우세항도 제거거 가능하다.
        예시) $f(n) = n^2 + 5n + 200$ 함수가 있다고 가정하면 $n^{2}$가 더 중요하므로 $5n + 200$은 삭제가 가능하다.       
- 입력이 다르면 변수도 다르다.
- 서로 다른 단계를 종합하거나 곱한다.
### O(1) 예제
```java
  
  return 23; //상수를 반환하므로 빅 오는 O(1)이다.
  
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
  // 따라서 시간 복잡도는 $(O.length)$ 또는 $O(n)$으로도 표기한다.
```

### O(n) - 상수 제외 예제
```java
  for(int i = 0; i < a.length; i++){
    System.out.println("Current element:");
    System.out.println(a[i]);
    System.out.println("Current element + 1:");
    System.out.println(a[i]+1);
  }
  /* 
    실행 시간은 입력 크기인 a.length에 관해 선형적이다.
    빅 오는 코드 라인 수에 의존하지 않고 실행 시간 증가율에 따라 달라지며, 
    상수 시간 연산에 의해 바뀌지 않는다.
    그래서 빅 오는 $O(n)$이다.
  */
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
 
> 메모이제이션 : 
컴퓨터 프로그램이 동일한 계산을 반복해야 할 때, 이전에 계산한 값을 메모리에 저장함으로써 동일한 계산의 반복 수행을 
제거하여 프로그램 실행 속도를 빠르게 하는 기술

출처 : https://ko.wikipedia.org
 
```java
 void printFibonacci(int k) {
  int[] cache = new int[k];
  for(int i = 0; i < k; i++){
   System.out.println(i + ": " + fibonacci(i, cache));
  }
 }
 
 int fibonacci(int k, int[] cache) {
  if(k <= 1){
   return k;
 }else if(cache[k] > 0){
  return cache[k];
 }
 cache[k] = fibonacci(k - 2, cache) + fibonacci(k - 1, cache);
 return cache[k];
}
```

fibonacci 메서드는 재귀 호출하는 메서드이기 때문에 빅 오는 $O(2^{n})$이다.

각 fibonacci(k) 메서드는 저장된 fibonacci(k-1)과 fibonacci(k-2) 메서드로 계산된다.

메모이제이션은 반환값을 다시 가져와서 사용하여 재귀 호출 횟수를 줄이는 것인데 이 때 저장한 값을 가져와서 더하는 것은 상수 시간 작업입니다. 따라서 빅 오는 $O(n)$으로 표현할 수 있다.

### 행렬의 1/2 반복 실행

```java
 // 코드 1
 for(int i = 0; i < a.length; i++){
  for(int j = 0; j < a.length; j++){
   System.out.println(a[i] + a[j]);
  }
 }
 
 // 코드 2
 for(int i = 0; i < a.length; i++){
  for(int j = i+1; j < a.length; j++){
   System.out.println(a[i] + a[j]);
  }
 }
```

a의 배열의 크기를 4라고 가정하면 다음과 같은 실행 과정을 도출할 수 있다.

코드1

(0,0) (0,1) (0,2) (0,3)           
(1,0) (1,1) (1,2) (1,3)        
(2,0) (2,1) (2,2) (2,3)                  
(3,0) (3,1) (3,2) (3,3)                        
        
코드2

(0,0) (0,1) (0,2) (0,3)           
      (1,1) (1,2) (1,3)        
            (2,2) (2,3)                  
                  (3,3)    
                  
코드1의 실행 시간 : $n$ x $n$ = $n^{2}$ -> $O(n^{2})$

코드2의 실행 시간(상수 제외) : $\frac{n*n}{2}$ -> $\frac{n^{2}}{2}$ -> $n^{2} * \frac{1}{2}$ -> $O(n^{2})$

따라서 두 코드 모두 빅 오가 $O(n^{2})$ 이다.

### 중첩 반복문에서 O(1) 식별

```java
 for(int i = 0; i < a.length; i++){
  for(int j = 0; j < a.length; j++){
   for(int q = 0; q < 1000000; q++){
    System.out.println(a[i] + a[j]);
   }
  }
 }
```
두 번째 for문만 보자면 빅 오는 $O(n^{2})$ 입니다.
세 번째 for문은 배열 크기에 상관없이 0에서 100만까지 반복하기 때문에 빅 오는 상수인 $O(1)$이다.
따라서 이 코드의 빅 오는 $O(n^{2})$이다.

### 배열의 1/2 반복 실행

```java
 for(int i = 0; i < a.length/2; i++){
  System.out.println(a[i]);
 }
```

배열의 절반만 순회한다고 빅 오 시간에 영향을 주지 않는다.
따라서 $O(n/2)$가 아닌 상수를 제거한 $O(n)$이다.

### 빅 오 표현식 줄이기

- $O(n + p)$
- $O(n + logn)$
 
 $O(n)$으로 표현할 수 있는 것은 $O(n + logn)$이다.
 비우세항으로 $O(n + logn)$은 $O(n)$이 가능하지만 $O(n + p)$는 p가 n과 어떤 관계인지 모르기 때문에 
 두 변수 모두 사용해야 한다.
 
### O(logn)의 시간 복잡도를 가지는 반복 실행

```java
 for(int i = 0; i< a.length; i++){
  for(int j = a.length; j > 0; j /= 2){
   System.out.println(a[i] + ", " + j);
  }
 }
```

외부 for문만 보자면 빅 오는 $O(n)$이다.

내부 for문을 보면 배열의 길이를 절반씩 점차 줄여 나간다.
이렇게 절반으로 줄이는 알고리즘은 대부분 빅 오를 $O(logn)$으로 표현한다.

따라서 이 코드의 빅 오는 $O(n) * O(logn) = O(nlogn)$이다.
 
### 문자열 비교

```java
 String[] sortArrayOfString(String[] a){
  for(int i = 0; i < a.length; i++){
   // O(nlogn) 알고리즘으로 각 문자열을 정렬합니다.
  }
  
  // O(nlogn) 알고리즘으로 배열 자체를 정렬합니다.
  
  return a;
 }
```

하나의 문자열을 정렬할 때는 $O(nlogn)$만큼의 시간과 배열의 크기 $O(n)$를 곱한 $O(n^{2}logn)$ 라고 생각했지만 
$O(nlogn)$ 에서 **n은 문자열의 길이**를 나타내고 a.length개의 문자열을 정렬하기 때문에 여기서 **n은 배열의 크기**를 나타낸다.

두 가지 변수를 사용하기 때문에 각 각 다르게 나타내야 한다.
- s : 가장 긴 String의 길이
- p : String 배열의 크기

s와 p를 사용하면 하나의 문자열 정렬의 시간 복잡도는
$O(slogs)$이며 이 작업을 p번 반복하면 $O(p) * O(slogs) = O(p*slogs)$이다.

String을 비교할 때 고정된 폭을 가진 정수의 경우처럼 상수 시간이 걸린다고 가정했지만 
String의 길이는 다양하므로 비교시간도 다양하다. 
각 String 비교는 $O(s)$가 걸리고 배열 정렬에 $O(plogp)$가 걸리기 때문에 문자열 배열을 정렬하는 총 시간 복잡도는 $O(s) * O(plogp) = O(s*plogp)$이다.

따라서 빅 오는 O(p*slogs) + O(s*p(logs + logp))가 된다.

### 펙토리얼 빅 오

```java
 long factorial(int num) {
  if(num >= 1){
   return num * factorial(num - 1);
  }else {
   return 1;
  }
 }
```

위 코드의 빅 오는 $O(n!)$ 이라고 생각하겠지만 재귀 과정에서 n, n-1, n-2, ... 1의 펙토리얼을 한 번씩 구하기 때문에
빅 오는 $O(n)$이다.

### n 표기법을 사용할 때 주의 사항
```java
 // 코드 1
 int multiply(int x, int y) {
  int result = 1;
  for(int i = 1; i <=y; i++){
   result *= x;
  }
  return result;
 }

 // 코드 2
 int powerxy(int x, int y){
  if(y < 0){
   return 0;
  } else if(y==0){
   return 1;
  } else {
   return x * powerxy(x, y-1);
  }
 }
```

코드 1은 상수 시간이 걸리는 작업을 y번 수행한다. 입력값 x는 실행 시간 증가율에 영향을 주지 않으므로
빅 오는 $O(y)$이다.

코드 2는 y - 1, y - 2, ... , 0을 재귀로 순회한다. 각 y 입력을 한 번 씩 순회하기 때문에 빅 오는 $O(y)$로 표현한다.

### 합과 반복 횟수
