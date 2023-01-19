# 객체지향 프로그래밍의 개념 이해
## 1. 객체란 무엇인가?
  
    객체는 객체지향 프로그래밍의 핵심 개념중 하나로서 실세계의 사물처럼 상태(필드)와 동작(메서드)를 가집니다.
    
    예시) 고양이의 상태는 색, 이름, 품종이 될 수 있고
          동작은 놀고, 먹고, 자고, 울음소리를 내는 것일 수 있다.
          
## 2. 클래스란 무엇인가?
    
    클래스는 객체를 만드는데 필요한 설계도라고 할 수 있습니다. 이때 객체를 만드는 과정을 '인스턴스화' 라고 하는데
    여러번 인스턴스화하여 원하는 수만큼의 객체를 만들수 있다.
    
## 3. 추상화란 무엇인가?

    클래스 간의 공통점을 찾아내서 super 클래스를 만드는 작업이다.
    깊게 들어가보면 클래스를 정의할 때 사용자와 관련 있는 내용만 노출하고 나머지 세부 내용은 숨기는 개념이다.
    추상화를 통해 사용자는 애플리케이션이 일을 수행하는 방법이 아닌 수행하는 일 자체에 집중 할 수 있다.

### 예시
#### 자동차는 페달을 이용해서 속도를 높이거나 늦출 수 있고 핸들을 이용해서 오른쪽이나 왼쪽으로 방향을 바꿀 수 있다.
#### Car 인터페이스로 정의하면 다음과 같다.
```java
public interface Car{
        public void speedUp();
        public void slowDown();
        public void turnRight();
        public void turnLeft();
        public String getCarType();
    }

```
#### ElectricCar 클래스는 Car 인터페이스를 구현하고 메서드를 오버라이드 한다. 이때 구현 내용은 운전자에게 노출되지 않는다.
```java
  public class ElectricCar implements Car{
    private final String carType;
    
    public ElectricCar(String carType){
      this.carType = carType;
    }
    
    @Override
    public void speedUp(){
      System.out.println("Speed up the eletric car");
    }
    
    @Override
    public void slowDown(){
      System.out.println("Slow down the electric car");
    }
    
    @Override
    public void turnRight(){
      System.out.println("Turn right the electric car");
    }
    
    @Override
    public void turnLeft(){
      System.out.println("Turn left then electic car");
    }
    
    @Override
    public void getCarType(){
      return this.carType;
    }
  }
```
#### 운전자는 구현내용을 몰라도 자동차를 용할 수 있다.
```java
  public class Main {
    public static void main(String[] args){
      Car electricCar = new ElectricCar("BMW");
      Car petrolCar = new PetrolCar("Audi");
      
      electricCar.speedUp();
      electricCar.turnLeft();
      
      petrolCar.slowDown();
      petrolCar.turnRight();
    }
  }
```

## 4. 캡슐화란 무엇인가?
    
    코드와 데이터를 하나의 작업 단위인 클래스로 결합하고 외부 코드가 이 데이터에 접근하지 못하게 하는 것을 뜻한다.
    이 캡슐화를 통해 정보를 은닉화 할 수 있고 코드의 느슨한 결합이 가능해진다. 
    자바의 캡슐화는 public, private, protected 같은 접근 제어자로 구현 할 수 있다.
    
## 5. 상속이란 무엇인가?
    
    객체가 다른 객체의 코드를 재사용할 수 있도록 허용하는 것이다. 그러면 코드의 재사용성을 유지할 수 있고, 
    각 객체만의 고유로직도 추가할 수 있다. 자바에서는 extends 키워드를 사용하는데 
    상속된 객체는 슈퍼클래스 또는 부모 클래스라고 하고 상속받은 객체는 서브클래스 또는 자식 클래스라고 한다.
    또한 여러 개의 클래스를 상속할 수 없다.
    
## 6. 다형성이란 무엇인가?
    
    'polymor-phism' 그리스어로 많은 형태라는 뜻이다. 즉, 다형성은 많은 형태를 의미한다.
    객체지향 프로그래밍에서 다형성은 객체가 때에 따라 다르게 동작할 수 있도록 하는 역할을 한다.
    다형성을 구현한 방법 중 대표적인 것이 오버로딩과 오버라이딩입니다.
    
### 예시
#### Traingle 클래스는 여러개의 메서드가 동일한 이름을 가지고 있지만 매개변수가 각 각 다르기 때문에 
#### 오버로드된 메서드의 형태에 따라 객체는 다르게 동작한다 . 이를 컴파일 타입 다형성이라고 한다.
```java
    public class Triangle {
      public void draw(){
        System.out.println("Draw default triangle ...");
      }

      public void draw(String color){
        System.out.println("Draw a trianlge of color " + color);
      }

      public void draw(int size, String color){
        System.out.println("Draw a trianlge of color " + 
        color + " and scale it up with the new size of " + size); 
      }
    }
```

### 예시
#### draw 메서드를 Shape 인터페이스에 정의한다.
```java
  public interface Shape {
    public void draw();
  }
```
#### Triangle, Rectangle, Circle 클래스는 Shape 인터페이스를 구현하고 각 각 draw 메서드를 오버라이드 한다.
```java
  public class Triangle implements Shape{
    @Override
    public void draw(){
      System.out.println("Draw a triangle ...");
    }
  }
  
  public class Rectangle implements Shape{
    @Override
    public void draw(){
      System.out.println("Draw a rectangle ...");
    }
  }
  
  public class Circle implements Shape{
    @Override
    public void draw(){
      System.out.println("Draw a circle ...");
    }
  }
```
#### 각 각의 클래스는 draw 메서드를 오버라이드 해서 다향한 모양을 출력할 수 있다. 이를 런타임 다형성이라고 한다.
```java
  public static void main(String[] args) {
    Shape triangle = new Triangle();
    Shape rectangle = new Rectangle();
    Shpae circle = new Circle();
    
    triangle.draw();
    rectangle.draw();
    circle.draw();
  }
```

## 7. 연관이란 무엇인가?
    
    연관은 서로 독립적인 두 클래스 간의 관계를 의미한다. 연관에는 단방향, 역방향, 일대일, 일대다, 다대일, 다대다 관계가 있습니다.

## 8. 집약이란 무엇인가?
    
    집약은 단방향 연관 관계의 특별한 경우입니다. 연관이 서로 독립적인 두 클래스 간의 관계라면 집약은 두 객체 간의 관계를 의미한다.
    집약 관계의 두 객체는 자체 생명 주기를 가지고 있어서 한 객체가 종료되어도 다른 객체는 영향이 가지 않는다.

## 9. 구성이란 무엇인가?
    
    구성은 더 제한적인 집약 관계입니다. 집약이 자체 생명 주기를 가진다면 구성은 단독으로 존재할 수 없는 객체 관계를 의미한다.
   
## SOLID 원칙 이해하기
 
    클래스를 작성하기 위해서는 SOLID 원칙이라는 디자인 패턴 원칙을 가지고 있다. 
    SOLID 원칙은 
    S(단일 책임 원칙) O(개방-폐쇄 원칙) L(리스코프 치환 원칙) I(인터페이스 분리 원칙) D(의존관계 역전 원칙)의 약자이다.
    
### S란 무엇인가?
S는 SOLID의 첫 번째 원칙인 '단일 책임 원칙'이며 '하나의 객체는 하나의 책임만 가져야 한다' 는 의미이다.
이 원칙은 높은 유지보수성을 유지할 수 있고 애플리케이션 모듈 전반에서 가시성 제어를 제공함으로써 캡슐화를
유지할 수 있다.
    
### O란 무엇인가?
O는 SOLID의 두 번째 원칙인 '개방 폐쇄 원칙'이며 '확장에는 열려 있고 수정에는 닫혀 있어야 한다'는 의미이다.
따라서 클래스는 다른 개발자가 작업을 수행하기 위해 반드시 수정해야 하는 제약 사항을 클래스에 포함해서는 안되며
다른 개발자가 클래스를 확장하기만 하면 원하는 작업을 할 수 있도록 해야 한다.
  
  #### 예시
  ##### 개방-폐쇄 원칙을 적용하지 않음
  ```java
    public interface Shape { }
  ```
  
  ```java 
    public class Rectangle implements Shape {
      private final int width;
      private final int height;
      
      // 생성자와 getter는 생략
   }
   
    public class Circle implements Shape {
      private final int radius;
      
      // 생성자와 getter는 생략
    }
  ```
  ##### 면적의 합을 구하기 위한 AreaCalculator 클래스는 다음과 같이 정의하였다.
  ```java
    public class AreaCalculator {
      private final List<Shape> shapes;
      
      public AreaCalculator(List<Shape> shapes){
        this.shapes = shapes;
      }
      
      // 도형을 추가하려면 수정해야 하는 코드
      public double sum(){
        int sum = 0;
        for(Shape shape : sahpes){
          if(shape.getClass().equals(Circle.class)) {
            sum += Math.PI * Math.pow((Circle) shape).getRadius(), 2);
          }else if(shape.getClass().equals(Rectangle.class)) {
            sum += ((Rectangle) shape).getHeight() * ((Rectangle) shape).getWidth();
          }
        }
        return sum;
      }
  ```
##### 만약 여기서 삼각형의 면적도 구하고 싶어하면 Triangle 클래스를 추가 하고 AreaCalculator 코드까지도 수정해야 한다.
##### 이렇듯 개방-폐쇄 원칙을 준수하지 않으면 여러 곳에 코드를 수정해야 하는 번거로운 사항이 생긴다.
<hr>

#### 개방-폐쇄 원칙을 적용
```java
    public interface Shape { public double area(); }
  ```
  
  ```java 
    public class Rectangle implements Shape {
      private final int width;
      private final int height;
      
      public Rectangle(int width, int height){
        this.width = width;
        this.height = height;
      }
      
      @Override
      public double area(){
        return width * height;
      }
   }
   
    public class Circle implements Shape {
      private final int radius;
      
      public Circle(int radius){
        this.radius = raduis;
      }
      
      @Override
      public double area(){
        return Math.PI * Math.pow(radius, 2);
      }
    }
  ```
  ##### 이제 AreaCalculator 클래스는 수정하지 않고도 각 도형마다 해당하는 area 메서드를 호출하면 면적을 구할 수 있다.
  ```java
    public class AreaCalculator {
      private final List<Shape> shapes;
      
      public AreaCalculator(List<Shape> shapes){
        this.shapes = shapes;
      }
      
      public double sum(){
       int sum = 0;
       
       for(Shape shape : shapes){
        sum += shapes.area();
       }
       return sum;
      }
    }
  ```
### L이란 무엇인가?
L은 SOLID의 세 번째 원칙인 '리스코프 치환 원칙'이며 '파생 타입은 반드시 기본 타입을 완벽하게 대체할 수 있어야 한다.'는 의미이다.
즉 서브클래스 객체가 슈퍼클래스의 객체와 반드시 같은 방식으로 동작해야 한다는 의미이다.

#### 예
##### '프리미엄', 'VIP', '무료' 세 가지 유형의 회원이 있는 체스 동호회가 있다. 기본 클래스 역할을 하는 Member(회원) 추상 클래스와 PremiumMember(프리미엄 회원), VipMember(VIP 회원), FreeMember(무료 회원)의 세 가지 서브클래스가 있다. 

<hr>

#### 리스코프 치환 원칙을 따르지 않는 경우

##### Member 추상 클래스는 체스 동호회 구성원을 나타내는 기본 클래스이다.
```java
  public abstract class Member {
    private final String name;
    
    public Member(String name){
      this.name = name;
    }
    
    public abstract void joinTournament();
    public abstract void organizeTournament();
  }
```

##### PremiumMember, VipMember 클래스는 체스 토너먼트에 참가하거나 주최할 수 있다.
```java
  public class PremiumMember extends Member {
    public PremiumMember(String name){
      super(name);
    }
    
    @Override
    public void joinTournament(){
      System.out.println("Premium member joins tournament ...");
    }
    
    @Override
    public void organizeTournament(){
      System.out.println("Premium member organize tournament ...");
    }
  }
  
  public class VipMember extends Member {
    public VipMember(String name){
      super(name);
    }
    
    @Override
    public void joinTournament(){
      System.out.println("VipMember joins tournament ...");
    }
    
     @Override
    public void organizeTournament(){
      System.out.println("VipMember organize tournament ...");
    }
  }
  
```
##### FreeMember 클래스는 토너먼트에 참가할 수 있지만 주최는 할 수가 없습니다. 이는 기본 클래스를 대체할 수 없어 리스코프 치환 원칙에 맞지 않다.
```java
  public class FreeMember extends Member {
    public FreeMember(String name){
      super(name);
    }
    
    @Override
    public void joinTournament(){
      System.out.println("Classic Member joins tournament ...");
    }
    
    // 이 메서드는 리스코프 치환 원칙에 맞지 않습니다.
    @Override
    public void organizeTournament(){
      System.out.println("A free Member cannot organize tournaments");
    } 
  }
```
<hr>

#### 리스코프 치환 원칙을 따르는 경우
##### 체스 토너먼트에 참가하거나 주최하는 두 가지 일을 분리하기 위해 두 가지 인터페이스를 정의 하는 것으로 리펙터링을 시작한다.
```java
  public interface TournamentJoiner {
    public void joinTournament();
  }
  
  public interface TournamentOrganizer {
    public void organizeTournament();
  }
```

##### Member 추상 클래스는 두 가지 인터페이스를 구현한다.
```java
  public abstract class Member implements TournamentJoiner, TournamentOrganizer {
    private final String name;
    
    public Member(String name){
      this.name = name;
    }
  }
```

##### FreeMember 클래스는 토너먼트를 주최할 수 없기 때문에 Member 기본 클래스가 아닌 TournamentJoiner 인터페이스만 구현한다.
```java
  public class FreeMember implements TournamentJoiner {
    private final String name;
    
    public FreeMember(String name){
      this.name = name;
    }
    
    @Override
    public void joinTournament(){
      System.out.println("Free member joins tournament ...");
    }
  }
```

##### 이로써 FreeMember 클래스는 TournamentJoiner 인터페이스를 PremiumMember, VipMember 클래스는 TournamentOrganizer 인터페이스로 대체가 가능하다.

### I란 무엇인가?
I란 SOLID의 네 번째 원칙인 '인터페이스 분리 원칙'이며 '클라이언트가 사용하지 않을 불필요한 메서드를 강제로 구현하게 해서는 안 된다'는 의미이다. 따라서 하나의 인터페이스를 2개 이상의 인터페이스로 분할해야 한다.

#### 예시  
#### 인터페이스 분리 원칙을 따르지 않는 경우
##### Connection 인터페이스
```java
  public interface Connection {
    public void socket();
    public void http();
    public void connect();
  }
```

##### WwwPingConnection 클래스는 http 메서드가 필요하고 socket 메서드는 필요하지 않지만 Connection 인터페이스를 구현하기 때문에 socket 메서드도 강제로 구현해야 한다.

```java
  public clas WwwPingConnection implements Connection {
    private final String www;
    
    public WwwPingConnection(String www){
      this.www = www;
    }
    
    @Override
    public void http(){
      System.out.println("Setup an HTTP connection to " + www);
    }
    
    @Override
    public void connect(){
      System.out.println("Connnect to " + www);
    }
    
    // socket 메서드가 필요하지 않지만 강제로 재정의 해야 한다.
    @Override
    public void socket() { }
    
  }
```
#### 인터페이스 분리 원칙을 따르는 경우
##### 인터페이스 분리 원칙을 지키려면 Connection 인터페이스는 connect 메서드만 남기고 http와 socket 메서드는 확장시킨다.
```java
  public interface Connection {
    public void connect();
  }
  
  public interface HttpConnection extends Connection {
    public void http();
  }
  
  public interface SocketConnection extends Connection {
    public void socket();
  }
```
##### 이렇게 하면 WwwPingConnection 클래스는 HttpConnection 인터페이스만 구현하면서 http 메서드를 사용할 수 있다.

### D란 무엇인가?
D란 SOLID의 다섯 번째 원칙인 '의존관계 역전 원칙'이며 '구체화가 아닌 추상화에 의존해야 한다'는 의미이다. 다른 구상 모듈에 의존하는 구상 모듈 대신, 구상 모듈을 결합하기 위해 추상 계층에 의존해야 한다는 것을 의미한다.

#### 예시  
#### 의존관계 역전 원칙을 따르지 않는 경우

##### JDBC URL 타입을 connect 메서드에 인수로 넣어주는 경우이다. 하지만 다른 JDBC URL 타입을 추가하고 싶다면 이 connect 메서드는 사용할 수가 없다. 이는 구체화에 의존하는 경우이므로 의존관계 역전 원칙을 무시하는 경우이다.
```java
  public class PostgreSQLJdbcUrl {
    private final String dbName;
    
    public PostgreSQLJdbcUrl(String dbName){
      this.dbName = dbName;
    }
    
    public String get(){
      return "jdbc:postresql:// ... " + this.dbName;
    }
  }
  
  public class ConnectToDatabase {
    public void connect(PostgreSQLJdbcUrl postgresql) {
      System.out.println("Connecting to " + postgresql.get());
    }
  }
```
#### 의존관계 역전 원칙을 따르는 경우
##### JDBC URL에서 구현해야 하는 인터페이스로 추상화 시킨다.
```java
  public interface JdbcUrl {
    public String get();
  }
```

```java
  public class PostgreSQLJdbcUrl implements JdbcUrl {
    private final String dbName;
    
    public PostgreSQLJdbcUrl(String dbName){
      this.dbName = dbName;
    }
    
    @Override 
    public String get(){
      return "jdbc:postgresql:// ... " + this.dbName;
    }
  }
  
  public class MySQLJdbUrl implements JdbcUrl {
    private final String dbName;
    
    public MySQLJdbcUrl(String dbName){
      this.dbName = dbName;
    }
    
    @Override
    public String get(){
      return "jdbc:mysql:// ... " + this.dbName;
    }
  }
  
  public class OracleJdbcUrl implements JdbcUrl {
    private final String dbName;
    
    public OracleJdbcUrl(String dbName){
      this.dbName = dbName;
    }
  }
```

##### 이로써 connect 메서드는 JdbcUrl 인터페이스에 의존하기 때문에 JdbcUrl 인터페이스를 구현한 PostgreSQLJdbcUrl, MySQLJdbcUrl, OracleJdbcUrl 클래스를 사용할 수 잇다.
```java
  public class ConnectToDatabase {
    public void connect(JdbcUrl jdbcUrl){
      System.out.println("Connecting to "  + jdbcUrl.get());
    }
  }
```

## 객체지향 프로그래밍에서 메서드 오버라이딩(Overriding)이란 무엇인가?
    
    상위 클래스에 메서드를 하위 클래스에서 내용을 변경 하는 것을 뜻한다. 메서드 오버라이딩은 상속 혹은 런타임 다형성에서 사용할 수 있는데
    상속에서는 슈퍼클래스에 있는 메서드를 서브클래스에서 상속받아 사용할 수가 있다. 이러한 메서드를 오버라이딩 메서드라고한다.
    런타임 다형성에서는 인터페이스를 구현한 클래스 인터페이스에 있는 메서드를 오버라이딩한다고 할 수 있다.
    이러한 오버라이딩의 장점은 객체 타입에 따라 실제 호출할 메서드를 런타입에서 결정할 수 있기 때문에 유연하고 확장 가능하다.
    그래서 최소한의 코드 변경으로 새로운 기능을 추가할 수 있게 해준다.
    
> 오버라이딩의 조건
 - 메서드 이름, 매개변수와 타입, 반환 타입은 슈퍼클래스와 서브클래스 모두 동일해야 한다.
 - 접근 제어자는 슈퍼 클래스의 메서드보다 좁은 범위로 변경 할 수 없다.
 - 슈퍼 클래스의 메서드보다 많은 수의 예외를 선언할 수 없다.
 - private, static, final 메서드는 오버라이드할 수 없다.
 - 오버라이딩 메서드에는 @Override 어노테이션을 사용해야 한다.

## 객체지향 프로그래밍에서 메서드 오버로딩(Overloading)이란 무엇인가?
    
    한 클래스 내에 같은 이름의 메서드를 여러 개 정의하는 것을 메서드 오버로딩(method Overloading) 또는 오버로딩(Overloading) 이라고 한다.
    컴파일러가 오버로딩된 메서드 호출을 실제 해당하는 메서드로 연결해준다. 따라서 런타임 동안 이러한 연결이 이루어지는 것은 아니다.
    
> 오버로딩의 조건  
  - 매개변수의 개수 또는 타입이 달라야 한다.
  - 반환 타입은 달라도 상관이 없다.
  - private, static, final 메서드를 오버로드 할 수 있다.
  - 같은 클래스에 있는 메서드를 오버로드 할 수 있다.
  
## 자바에서 공변 메서드 오버라이딩이란 무엇인가?
  
    '공변'은 함께 변한다는 의미로 오버라이딩시 슈퍼 클래스의 반환 타입을 서브 클래스의 타입으로 변경이 가능하게 만드는 것이다.
    즉, 메서드의 클라이언트가 반환된 타입의 명시적인 타입 변환을 하지 않아도 된다는 의미이다.
    
### 예시     
### Cloneable 인터페이스를 구현하는 Rectangle 클래스에 clone 메서드는 Object 대신 Rectangle을 반환할 수 있다.
```java
  public class Rectangle implements Cloneable {
    
    private final int height;
    private final int width;

    public Rectangle(int height, int width) {
        this.height = height;
        this.width = width;
    }

    public int getHeight() {
        return height;
    }

    public int getWidth() {
        return width;
    }
    
    @Override
    protected Rectangle clone() throws CloneNotSupportedException {
      Rectangle clone = (Rectangle) super.clone();
    }
    
  }
  
  ```java
  public class Main {
    public static void main(String[] args) throws CloneNotSupportedException {
        Rectangle r = new Rectangle(4, 3);
        Rectangle clone = r.clone();

        System.out.println("Width: " + clone.getWidth());
        System.out.println("Height: " + clone.getHeight());
    }
}
```

## 오버라이딩 및 오버로딩 메서드에서 예외를 다룰 때 주요 제한 사항은 무엇입니까?

    확인되지 않은 예외의 경우 오버라이딩 메서드에서 사용하는데 아무런 제한 사항이 없습니다. 반면에 확인된 예외의 경우
    오버라이딩 메서드는 오버라이드된 메서드의 확인된 예외 혹은 그 서브클래스 예외만 발생시킬 수 있습니다. 
    오버로딩 메서드의 경우 예외를 다룰 때 어떤 제한 사항도 없습니다.

## 슈퍼클래스의 오버라이드된 메서드를 서브클래스의 오버라이딩 메서드에서 어떻게 호출할 수 있는가?
    
    자바의 super 키워드를 이용해서 슈퍼클래스의 오버라이드된 메서드를 서브클래스의 오버라이딩 메서드에서 호출할 수 있다.
    
## main 메서드를 오버라이드 또는 오버로드할 수 있는가?
  
    main 메서드는 오버로드할 수 있지만 오버라이드 할 수 없습니다. 그 이유는 오버라이드 할 수 있는 메서드는 객체 타입에 
    따라 런타임에 결정되는 반면에 static 메서드는 컴파일 시간에 결정되기 때문이다.
    
## 자바에서 static이 아닌 메서드를 static 메서드로 오버라이드 할 수 있는가?
    
    static이 아닌 메서드는 static 메서드로 오버라이드할 수 없습니다.
    
## 자바 인터페이스 안에 abstract가 아닌 메서드를 포함할 수 있는가?
    
    자바 8 전까지는 abstract가 아닌 메서드는 사용할 수 없었지만 자바 8부터는 default 및 static 키워드를 사용해서
    구현된 메서드를 직접 추가 할 수 있게되었습니다. 이는 이전 버전과의 호환성을 보장하면서 기존의 인터페이스를 발전
    시키기 위함이다.
    
## 추상 클래스와 인터페이스의 주요 차이점은 무엇인가?

    먼저 목적 부분에서 차이점이 있는데 인터페이스의 주요 목적 완전히 추상화된 상태를 구현하는 것이지만, 
    추상 클래스는 부분적인 추상화를 위한 것입니다. 또한 인터페이스는 생성자를 지원하지 않지만 
    추상 클래스는 생성자를 가질 수 있고, 인터페이스는 default 메서드만 가지고 있는 것은 비효율적이거나 
    비생산적이지만, 추상 클래스는 추상 메서드가 없어도 문제가 되지 않는다.
    
## abstract 메서드가 없는 추상 클래스를 만들 수 있는가?
    
    가능합니다. abstract 키워드를 클래스에 추가하면 추상 클래스가 된다. 생성자오 abstract가 아닌 메서드만 있어도 상관없다.
    
## 추상이면서 동시에 final인 클래스를 만들 수 있는가?
    
    final 클래스는 상속할 수 없습니다. 

## 다형성, 오버라이딩, 오버로딩의 차이점은 무엇인가?

    오버로딩은 컴파일 타입 다형성으로 컴파일 시에 바인딩되고, 오버라이딩은 런타입 다형성으로 런타임 시에 바인딩 된다.
    여기서 바인딩이란 코드 라인에서 참조한 결과로 메서드 또는 변수를 결정하는 것이다. 즉, 메서드 호출을 메서드 본문에
    연결하는 과정을 바인딩 작업이라고 한다.
    
## 정적 바인딩과 동적 바인딩의 주요 차이점은 무엇인가?
    
    정적 바인딩은 컴파일 시간에 발생하며 자바의 클래스 정보를 통해 결정된다.
    반면 동적 바인딩은 런타임에 발생하며 Object에 의해 결정된다.
    
## 자바에서 메서드 하이딩이란 무엇인가?
    
    슈퍼클래스와 서브클래스에서 같은 이름과 시그니처인 static 메서드를 선언하면 두 메서드는 서로를 숨기는 것이다.
    따라서 슈퍼클래스에서 메서드를 호출하면 슈퍼클래스의 static 메서드가 서브클래스에서 메서드를 호출하면 서브클래스의
    static 메서드가 호출된다.
    
## 자바에서 가상 메서드를 작성할 수 있는가?

    가능하다. 자바에서 static이 아닌 메서드는 모두 기본적으로 가상 메서드이다.
    단 private 또는 final 키워드로 표시한 메서드는 가상 메서드가 아니다.
  
## 추상화와 다형성의 차이점은 무엇인가?

    추상화는 개발자가 재사용 및 맞춤형 정의가 가능한 일반적인 솔루션을 설계할 수 있게 하는 반면에 
    다형성은 개발자가 런타임에 실행해야 하는 코드 선택을 미룰 수 있게 합니다.
    
    
