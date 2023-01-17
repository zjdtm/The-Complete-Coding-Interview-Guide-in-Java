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
    
