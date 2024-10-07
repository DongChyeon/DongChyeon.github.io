---
caption: #what displays in the portfolio grid:
  title: 객체지향 개념 정리
  subtitle: 객체지향 프로그래밍을 위한 용어들의 개념 정리하기
  thumbnail: https://velog.velcdn.com/images/dongchyeon/post/f1c99ce3-9ab7-4a98-8ec7-c3058ea70d30/image.png
  
#what displays when the item is clicked:
title: 객체지향 개념 정리
subtitle: 객체지향 프로그래밍을 위한 용어들의 개념 정리하기
image: https://velog.velcdn.com/images/dongchyeon/post/f1c99ce3-9ab7-4a98-8ec7-c3058ea70d30/image.png #main image, can be a link or a file in assets/img/portfolio
---

### 객체지향 개발론

객체지향 개발론은 소프트웨어를 객체라는 단위로 나누어 설계하는 개발 방법론이다. 객체는 데이터와 기능을 하나의 단위로 묶은 것으로, 객체 간의 상호작용을 통해 프로그램은 동작한다. 객체지향 개발론의 핵심 개념에는 클래스, 상속, 다형성, 매시지 패싱, 추상 클래스, 인터페이스 등이 포함된다.

### 클래스, 객체, 메시지 패싱

* 클래스는 객체를 정의하는 틀이며, 객체의 속성(필드)과 행동(메소드)을 정의한다.
* 객체는 클래스를 바탕으로 생성된 인스턴스로, 실질적으로 프로그램 내에서 동작하는 요소이다.
* 메시지 패싱은 객체 간에 메소드를 호출하고 응답하는 방식으로, 객체 간의 상호작용을 구현하는 방법이다.

```kotlin
// Kotlin 예시
class Animal(val name: String) {
	fun makeSound() {
    	println("$name makes a sound.")
    }
}

val dog = Animal("Dog")	// 객체 생성
dog.makeSound()	// 메시지 패싱: 객체 간 메소드 호출
```

```dart
// Dart 예시
class Animal {
	String name;
    
    Animal(this.name);
    
    void makeSound() {
    	print('$name makes a sound.');
    }
}

void main() {
	var dog = Animal('Dog');
    dog.makeSound();
}
```

```swift
// Swift 예시
class Aniaml {
	private var name: String;
    
    init(name: String) {
    	self.name = name
    }
    
    func makeSound() {
    	print("\(name) makes a sound.")
    }
}
```

### 추상화, 캡슐화, 정보은닉, 모듈화, 계층화

* 추상화는 시스템의 중요한 부분만을 모델링하는 과정으로, 불필요한 세부 사항을 감추고 핵심 기능에 집중하는 개념이다.
* 캡슐화는 객체의 데이터(필드)를 외부에서 접근하지 못하게 보호하고, 오직 메소드를 통해서만 접근하는 기법이다.
* 정보 은닉은 캡슐화를 통해 객체의 내부 상태를 숨기고 외부에서의 불필요한 접근을 제한하는 개념이다.
* 모듈화는 프로그램을 독립적인 모듈로 나누어 개발하고, 각 모듈이 명확한 역할을 갖도록 하는 설계 기법이다.
* 계층화는 시스템을 여러 계층으로 나누어 복잡성을 줄이고, 각 계층이 특정 역할을 수행하도록 설계하는 방식이다.

```kotlin
// Kotlin 예시
class Person(private val age: Int) { // 정보은닉 

    private fun getAge(): Int { // 캡슐화
   		return age
    }
}
```

### Stack 과 Heap 메모리

* Stack : 함수 호출 시 사용되는 메모리 공간으로, 지역 변수나 함수 호출 스택이 쌓인다. 메모리 크기가 고정된 데이터는 스택에 저장된다.
  * 예: 기본 타입(int, double 등)과 함수 내부에 선언된 변수들은 Stack에 저장된다.

* Heap: 동적으로 할당된 메모리 공간으로, 객체나 배열 같은 데이터가 저장된다. 메모리 크기가 고정되지 않은 데이터는 런타임에 힙에 저장된다.
  * 예: new 키워드로 생성된 객체들은 Heap에 할당된다.


### Static과 Dynamic 할당

* Static 할당: 컴파일 시점에 메모리가 할당되며, 프로그램이 실행되는 동안 메모리가 유지된다. 주로 전역 변수나 static 키워드가 붙은 변수들이 여기에 해당된다. 
     * Stack 또는 Data 영역에 할당된다.
     * 프로그램이 종료되거나 함수가 끝나도 사라지지 않으며, 고정된 크기로 메모리가 예약된다.

     
* Dynamic 할당: 프로그램 실행 중에 런타임에서 필요에 따라 메모리가 할당되고, 더 이상 사용하지 않으면 메모리를 해제해야 한다. 동적으로 할당된 객체는 Heap에 저장된다.
  * 주로 new, malloc, alloc 등을 통해 할당된 객체나 배열이 여기에 해당된다.
  * 메모리 할당과 해제를 관리하기 때문에 유연성이 있지만, 관리하지 않으면 메모리 누수가 발생할 수 있다.

### Stack과 Heap, Static과 Dynamic의 연관성

* Stack은 Static 할당과 관련이 있다. 함수가 호출될 때 지역 변수들이 Stack에 자동으로 할당되며, 함수가 끝나면 자동으로 메모리에서 사라진다. 즉, 정적으로 할당된 메모리처럼 동작한다.
* Heap은 Dynamic 할당과 관련이 있다. 런타임 시 동적으로 할당된 객체들은 Heap에 저장되며, 명시적으로 해제되기 전까지 메모리에 남아 있다. 프로그램의 실행 중 필요한 크기만큼 유연하게 메모리를 할당받는다.

```kotlin
val a = 10;	  // 변수가 Stack에 할당 (Static 할당)

val dog: Animal = Animal('Dog');	// 객체가 힙에 할당 (Dynamic 할당)
```

### 함수 지향 vs. 객체 지향

* 함수 지향 프로그래밍은 함수나 수학적 함수가 기본 단위가 되어 프로그램을 구성한다. 상태를 변경하지 않고, 입력을 받아 출력만을 반환하는 순수 함수를 중시한다.
* 객체 지향 프로그래밍은 상태(필드)와 행동(메소드)를 가지는 객체를 기반으로 프로그램을 구성하며, 객체 간의 상호작용을 통해 프로그램이 동작한다.

### Object vs. Entity

* Object는 객체 지향 프로그래밍의 기본 단위로, 상태와 행동을 가진 요소이다.
* Entity는 데이터베이스나 도메인 모델링에서 사용되는 개념으로, 고유한 식별자를 가진 데이터 단위이다.

### 상속

상속은 기존 클래스를 확장하여 새로운 클래스를 정의하는 방법으로, 코드의 재사용성을 높이고 구조를 체계적으로 만드는 데 도움을 준다.
또한, 메소드 오버라이딩을 활용하면 상속받은 메소드를 서브 클래스에서 재정의하여 사용할 수 있다.

```kotlin
open class Animal {
	open fun sound() {
    	println("Animal maeks sound")
    }
}

class Dog : Animal() {
    override fun sound() {	// 메소드 오버라이딩
        println("Dog barks")
    }
}

class Cat : Animal() {
	override fun sound() {
    	println("Cat meows")
    }
}
```

### 다형성

다형성은 객체나 메소드가 여러 형태를 가질  수 있는 성질을 말하며, 함수 오버로딩이나 연산자 오버로딩을 통해 구현된다.
* 메소드 오버로딩: 같은 이름의 메소드를 여러 개 정의하되, 매개변수의 타입이나 개수가 달라지는 경우이다.
* 연산자 오버로딩: 연산자를 재정의하여 객체 간의 연산을 처리할 수 있다.

```kotlin
class Calculator {
	fun add(a: Int, b: Int): Int = a + b
    fun add(a: Double, b: Double): Double = a + b 	// 메소드 오버로딩
}
```

```kotlin
class Vector(val x: Int, val y: Int) {
	// + 연산자 오버로딩
	operator fun plus(other: Vector): Vector {
    	return Vector(this.x + other.x, this.y + other.y)
    }
}
````

### 추상 클래스

추상 클래스는 객체를 직접 생성할 수 없으며, 이를 상속받은 클래스에서 구체적인 구현을 정의해야 한다. 주로 공통적인 메소드나 속성을 정의할 때 사용된다.

```kotlin
abstract class Animal {
	abstract fun sound(); // 추상 메소드
}

class Dog : Animal() {
	override fun sound() {
    	println("Dog barks")
    }
}
```

### 인터페이스

인터페이스는 클래스가 구현해야될 행동(메소드)을 정의하는 틀을 제공한다. 메소드의 시그니처(이름, 매개변수)만 정의하며, 구체적인 구현은 인터페이스를 구현하는 클래스에서 정의된다.

```kotlin
// 인터페이스 정의
interface Animal {
    fun sound()  // 추상 메소드, 구현 클래스에서 반드시 구현해야 함
}

// Dog 클래스가 Animal 인터페이스를 구현
class Dog : Animal {
    override fun sound() {  // 인터페이스의 메소드를 재정의
        println("Dog barks")
    }
}
```

### 제너릭 클래스

제너릭 클래스는 데이터 타입에 의존하지 않는 클래슬르 말하며, 다양한 타입에 대해 유연하게 동작할 수 있다.

```kotlin
class Box<T>(val value: T)

val intBox = Box(123)
val stringBox = Box("Hello")
```
