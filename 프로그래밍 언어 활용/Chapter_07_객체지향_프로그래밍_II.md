# Chapter_07_객체지향_프로그래밍_II

## 1 상속

### 1.1 상속의 정의와 장점 [p.310]

* 코드의 재사용성을 높이고 코드의 중복을 제거하여 프로그램의 생산성과 유지보수에 크게 기여한다.
* 상속 클래스
  - 조상 클래스
    - 부모(parent)클래스, 상위(super)클래스, 기반(base)클래스
  - 자손 클래스
    - 자식(child)클래스, 하위(sub)클래스, 파생된(derived)클래스
* 멤버변수 상속
```java
 public class Animal {    
        
    int weight;
}
```
```java
 public class Mammal extends Animal {
    
    int toothSize;
}
```
```java
 public class Dog extends Mammal {

}
```
```java
 public class Main {

    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.weight = 10;
        dog.toothSize = 20;
    }
}
```
* 메서드 상속
```java
public class Animal {    
        
    void eat() {
        System.out.println("음식 먹기");
    }
}
```
```java
public class Mammal extends Animal {    
    
}
```
```java
public class Main {

    public static void main(String[] args) {
        Mammal mammal = new Mammal();
        mammal.eat();
    }
}
```
```java
public class Main {

    public static void main(String[] args) {
        Mammal mammal = new Mammal();
        mammal.eat();
    }
}
```
* 생성자와 초기화 블럭은 상속되지 않는다. 멤버만 상속된다.
* 자손 클래스의 멤버 개수는 조상 클래스보다 항상 같거나 많다.
* 생성자 상속
```java
public class Animal {    

  Animal() {
        System.out.println("Animal Init");
    }
}
```
```java
public class Mammal extends Animal {    
    
}
```
```java
public class Animal {    
        
    int weight;
    
    Animal() {
        System.out.println("Animal Init");
    }
}
```
### 연습문제
* Car와 Bus 클래스를 구현하세요. 단 Bus는 Car를 상속해야 한다.
```java
public class Ch7Ex1 {

    public static void main(String[] args) {
        
        Car car = new Car();
        car.run();  // "달리다" 출력
        
        Bus bus = new Bus();
        bus.run();  // "달리다" 출력
        bus.ppangppang();  // "빵빵~" 출력
    }
}
```
```console
달리다.
달리다.
빵빵~.
```
### 1.2 클래스간의 관계 - 포함관계 [p.316]
```java
public class Point {
    int x;
    int y;
}
```
* 상속관계(is a)
  - Circle is a Point.
```java
public class Circle extends Point {    
    int r;
}
```
* 포함관계
  - Circle has a Point.
```java
public class Circle {
    Point p;
    int r;
}
```
### 1.3 클래스간의 관계 결정하기 [p.317]
* 상속관계
  ```
  ~은 ~이다.(is-a)
  ```
* 포함관계
  ```
  ~은 ~을 가지고 있다.(has-a)
  ```
### [연습문제] 다음 주석부분에 코드를 is-a 관계로 구현해 보자.
* Point.java
```java
public class Point {
    int x;
    int y;
}
```
* Circle.java
```java
public class Circle extends Point {    
    int r;
    
    /*
      draw() 메서드 구현 부분
    */
}
```
* Main.java
```java
public class Main {

    public static void main(String[] args) {
        Circle c = new Circle();
        /*
          멤버변수 초기화 코드 구현 
        */
        c.draw();
    }
}
```
* 실행결과
```console
(10, 20)좌표에 반지름 5크기의 원을 그렸습니다.
```
### [연습문제] 다음 주석부분에 코드를 has-a 관계로 구현해 보자.
* Point.java
```java
public class Point {
    int x;
    int y;
}
```
* Circle.java
```java
public class Circle extends Point {    
    int r;
    
    /*
      draw() 메서드 구현 부분
    */
}
```
* Main.java
```java
public class Main {

    public static void main(String[] args) {
        Circle c = new Circle();
        /*
          멤버변수 초기화 코드 구현 
        */
        c.draw();
    }
}
```
* 실행결과
```console
(10, 20)좌표에 반지름 5크기의 원을 그렸습니다.
```
### 1.4 단일 상속(Simgle inheritance) [p.323]
* 자바는 단일 상속만 허용한다.
```java
public class Point {
    int x;
    int y;
}
```
```java
public class Color {
    int r;
    int g;
    int b;
}
```
```java
public class Circle extends Point, Color {  // 에러 발생

}
```
### 1.5 Object클래스 = 모든 클래스의 조상 [p.325]
* 모든 클래스의 조상 클래스이다.
* 모든 클래스가 자동으로 상속 받는다.
* Object 상속을 생략해도 컴파일러가 자동으로 상속시킨다.

## 2 오버라이딩(overriding)
### 2.1 오버라이딩이란? [p.327]
* 사전적 의미
  - override : ~위에 덥어쓰다(overwite)
```java
public class Animal {    
        
    void eat() {
        System.out.println("Animal 음식 먹기");
    }
}
```
```java
public class Mammal extends Animal {    
    
    void eat() {
        System.out.println("Mammal 음식 먹기");
    }
}
```
```java
public class Main {

    public static void main(String[] args) {
        Mammal mammal = new Mammal();
        mammal.eat();
    }
}
```

### 2.2 오버라이딩의 조건 [p.328]
* 자손클래스에서 오버라이딩하는 메서드는 조상 클래스의 메서드와
  - 이름이 같아야 한다.
  - 매재변수가 같아야 한다.
  - 반환타입이 같아야 한다.

### 2.3 오버로딩 vs. 오버라이딩 [p.329]
* 오버로딩(overloading)
  - 기존에 없는 새로운 메서드를 정의하는 것
* 오버라이딩(overrding)
  - 상속받은 메서드의 내용을 변경하는 것(change, modify)
### 연습문제
* Car와 Bus 클래스를 구현하세요. 단 Bus는 Car를 상속해야 한다.
```java
public class Ch7Ex2 {

    public static void main(String[] args) {
        
        Car car = new Car();
        car.run();  // "달리다" 출력
        
        Bus bus = new Bus();
        bus.run();  // "버스가 달리다" 출력
        bus.ppangppang();  // "빵빵~" 출력
    }
}
```
```console
달리다.
버스가 달리다.
빵빵~.
```  
### 2.4 super [p.330]
```java
public class Animal {    
        
    int weight = 10;    
}
```
```java
public class Mammal extends Animal {    
    
    // int super_weight = 20; 실제로는 super_weight로 상속되어 있다.
    int weight = 20; // 실제로는 this_weight로 보면 된다.
    
    public Mammal() {
        System.out.println(super.weight);
    }
}
```
### 연습문제
* Car와 Bus 클래스를 구현하세요. 단 Bus는 Car를 상속해야 한다.
```java
public class Ch7Ex3 {

    public static void main(String[] args) {
    
        Bus bus = new Bus();
        bus.run();  // "달리다" super()를 통해서 출력한 뒤에 "버스가 달리다"를 출력
        bus.ppangppang();  // "빵빵~" 출력
    }
}
```
```console
달리다.
버스가 달리다.
빵빵~.
```

## 3 package와 import

### 3.1 패키지(package) [p.336]
* 목적 - 이름 충돌을 막을 수 있다.
* 패키지 조건
  - 하나의 소스파일에는 첫번째 문장으로 단 한번의 패키지 선언만 허용한다.
  - 모든 클래스는 반드시 하나의 패키지에 속해야 한다.
  - 패키지는 점(.)을 구분자로 하여 계층구조로 구성할 수 있다.
  - 패키지는 물리적으로 클래스 파일(.class)을 포함하는 하나의 디렉토리이다.

### 3.2 패키지 선언 [p.337]
```java
package 패키지명;
```
```java
package com.javachobo.book;

class PackageTest {
	public static void main(String[] args) {
		System.out.println("Hello World!");
	}
}
```
* 338쪽 생략...
### 연습문제
* Car와 Bus 클래스를 구현하세요. 
	- 단 Bus는 Car를 상속해야 한다.
  - 패키지를 kr.hkit.ch7로 만들기.
```java
package kr.hkit.ch7;

public class Ch7Ex4 {

    public static void main(String[] args) {

        Bus bus = new Bus();
        bus.run();
        bus.ppangppang();
    }
}
```
```console
달리다.
버스가 달리다.
빵빵~.
```

### 3.3 import문 [p.340]
* 목적 : 패키지 일부를 생략하고 클래스를 사용할 수 있음.
* 이클립스 단축키 : Ctrl + Shift + o

### 3.4 import문의 선언 [p.340]
* 일반적으로 소스파일(.java)의 구성은 다음 순서로 되어 있다.
  - package문
  - import문
  - 클래스 선언
  
* import문을 선언하는 방법
  - import 패키지명.클래스명;
  - import 패키지명.*;
  
* ImportTest.java
```java
import java.text.SimpleDateFormat;
import java.util.Date;

class ImportTest 
{
    public static void main(String[] args) 
    {
         Date today = new Date();
         
         SimpleDateFormat date = new SimpleDateFormat("yyyy/MM/dd");
         SimpleDateFormat time = new SimpleDateFormat("hh:mm:ss a");

         System.out.println("오늘 날짜는 " + date.format(today));
         System.out.println("현재 시간은 " + time.format(today));
    }
}
```
* 실행결과
```console
오늘 날짜는 2020/02/17
현재 시간은 01:13:40 오전
```

### 연습문제
* Car와 Bus 클래스를 구현하세요. 
  - 단 Bus는 Car를 상속해야 한다.
  - Ch7Ex5는 kr.hkit.ch7패키지로, 
  - Car와 Bus는 kr.hkit.ch7.model 패키지로 생성하고, 
  - Ch7Ex5에서 Bus 클래스를 사용할 수 있도록 import 하세요.
```java
package kr.hkit.ch7;

/*
   Car와 Bus 클래스를 적절히 import 하세요.
*/
public class Ch7Ex5 {

    public static void main(String[] args) {

        Bus bus = new Bus();
        bus.run();
        bus.ppangppang();
    }
}
```
```console
달리다.
버스가 달리다.
빵빵~.
```
### 3.5 static import문
* 생략...

## 4 제어자(modifier)

### 4.1 제어자란? [p.344]
* 접근 제어자 : public, protected, drfault, private
* 그외 : static, final , abstract, native, transient, synchronized, volatile, strictfp

### 4.2 static - 클래스의, 공통적인 [p.344]

### 4.3 final - 마지막의, 변경될 수 없는 [p.345]
* final
  - 클래스
    - 상속 불가    
    - 상속 계층 구조에서 '마지막' 클래스입니다.
  - 메서드
    - 오버라이딩 불가
  - 멤버변수, 지역변수
    - 변수값 변경 불가
    - p.30쪽에서 설명함
    
    
### 4.4 abstract - 추상의, 미완성의 [p.347]
* 추상화 : 실제 기능 부분의 구체적인 구현을 추상화해서 표현
* p.375에서 설명...

### 4.5 접근 제어자(access modifier) [p.348]
* 접근 제어자 종류
  - private : 같은 클래스 내에서만 접근이 가능
  - default : 같은 패키지 내에서만 접근이 가능
  - protected 
    - 같은 패키지 내에서
    - 다른 패키지의 자손 클래스에서 접근이 가능
  - public : 접근 제한이 없음
* public > protected > default > private
* 접근 제어자 대상
  - 클래스 
    - public, (default)
  - 메서드, 멤버변수
    - public, protected, (default), private
  - 지역변수
    - 없음
* 접근 제어자를 사용하는 이유
  - 외부로부터 데이터를 보호하기 위해서
  - 외부에서 불필요한, 내부적으로만 사용되는, 부분을 감추기 위해서

### 연습문제
* Car와 Bus 클래스를 구현하세요. 
  - 단 Bus는 Car를 상속해야 한다.
  - Ch7Ex5는 kr.hkit.ch7패키지로, 
  - Car는 kr.hkit.ch7.parent로, 
  - bus는 kr.hkit.ch7.model 패키지로 생성하고, 
  - Ch7Ex5에서 Bus 클래스를 사용할 수 있도록 import 하세요.
```java
package kr.hkit.ch7;

public class Ch7Ex6 {

    public static void main(String[] args) {

        Bus bus = new Bus();
        bus.run();
        bus.ppangppang();
    }
}
```
```console
달리다.
버스가 달리다.
빵빵~.
```

* 생성자의 접근 제어자
  * 싱글톤 패턴
  ```java
  public class Device {

      private static Device instance;

      private Device() {

      }

      public static Device getInstance() {
          if(instance == null) {
              instance = new Device();
          }
          return instance;
      }
  }  
  ```
### 4.6 제어자(modifier)의 조합
* 대상에 따라 사용할 수 있는 제어자
  - 클래스 
    - public, (default)
    - final, abstract
  - 메서드
    - 모든 접근 제어자
    - final, abstract, static
  - 멤버변수
    - 모든 접근 제어자
    - final, static
  - 지역변수
    - final
    
## 5 다형성

### 5.1 다형성이란? [p.354]
* 부모클래스로 자클래스 인스턴스를 참조할 수 있도록 하였음.

```java
public interface Queen {

    public void spawn();
}
```
```java
public interface Soldier {

    public void attack();
}
```
```java
public interface Worker {

    public void work();
}
```
```java
public class Ant implements Worker, Soldier, Queen {

    public void spawn() {
        // TODO Auto-generated method stub
        
    }

    public void attack() {
        // TODO Auto-generated method stub
        
    }

    public void work() {
        // TODO Auto-generated method stub
        
    }

}
```
```java
public class Main {

    public static void main(String[] args) {
                
        Queen queenAnt = new Ant(); 
        queenAnt.spawn();
        
        Soldier soldierAnt = new Ant();
        soldierAnt.attack();
        
        Worker workAnt = new Ant();
        workAnt.work();        
    }
}
```

### 5.2 참조변수의 형변환 [p.356]
* 자손타입 -> 조상타입(Up-casting)
	- 형변환 생략가능
* 자손타입 <- 조상타입(Down-casting)
  - 형변환 생략불가
  
### 5.3 instanceof 연산자 [p.362]
* 참조변수(객체)의 타입을 알아내는 명령어

### 5.4 참조변수와 인스턴스의 연결 [p.364]
* 멤버변수의 경우 참조변수의 타입에 따라 달라진다.

### 5.5 매개변수의 다형성 [p.367]
* 참조변수의 다형성은 메서드의 매개변수에도 적용된다.(당연한 소리)

### 5.6 여러 종류의 객체를 배열로 다루기 [p.370]
```java
public class Product {

}
```
```java
public class TV extends Product {

}
```
```java
public class PC extends Product {

}
```
```java
public class Audio extends Product {

}
```
```java
ublic class Main {

    public static void main(String[] args) {
                
        TV tv = new TV();
        PC pc = new PC();
        Audio audio = new Audio();
        
        Product[] products = {tv, pc, audio};
    }
}
```

