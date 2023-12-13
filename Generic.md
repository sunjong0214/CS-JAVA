제네릭(Generic)이란 '데이터 형식에 의존하지 않고, 하나의 값이 여러 다른 데이터 타입을 가질 수 있도록 하는 방법' 입니다.

우리가 흔히 쓰는 ArrayList, LinkedList 등을 생성할 때, 객체 <타입> 객체명 = new 객체 <타입> (); 과 같이 쓰인다.

```java
ArrayList<Integer> list1 = new ArrayList<Integer>();
ArrayList<String> list2 = new ArrayList<Integer>();
 
LinkedList<Double> list3 = new LinkedList<Double>():
LinkedList<Character> list4 = new LinkedList<Character>();
```

위와 같이 <타입> 안에 객체가 가질 타입을 정의 해준다.

하지만 우리가 만약 어떤 자료구조를 만들어 배포하려고 할 때, String, Integer 등 여러 타입을 지원하고 싶을 때 문제가 발생한다. 

위 예제처럼 타입을 정의했을 땐, String에 대한 클래스, Integer에 대한 클래스 등 하나하나 타입에 대한 클래스를 만들어야하는 비효율적인 일을 해야한다. 

이런 문제를 해결하기 위해 우리는 제네릭이라는 것을 사용한다.



그렇다. 

제네릭(Generic)은 **클래스 내부에서 지정하는 것이 아닌 외부에서 사용자에 의해 지정되는 것**을 의미한다.

한 마디로 특정(Specific) 타입을 미리 지정해주는 것이 아닌 필요에 의해 지정할 수 있도록 하는 일반(Generic) 타입인 것이다.

(정확히 말하자면 지정된다는 것 보다는 타입의 경계를 지정하고, 컴파일 때 해당 타입으로 캐스팅하여 매개변수화 된 유형을 삭제하는 것이다. 이 것을 여기서 모두 설명하기에는 너무 길어지므로 일단 지정된다 정도로 알고가도 이해하는데 큰 문제는 없을 것이다.)

## Generic의 장점

1. 제네릭을 사용하면 잘못된 타입이 들어올 수 있는 것을 컴파일 단계에서 방지할 수 있다.
2. 클래스 외부에서 타입을 지정해주기 때문에 따로 타입을 체크하고 변환해줄 필요가 없다. 즉, 관리하기가 편하다. (형변환 필요 X)
3. 비슷한 기능을 지원하는 경우 코드의 재사용성이 높아진다.

## Generic 사용 방법

제네릭은 아래 표의 타입들이 많이 쓰인다.

| 타입 |  설명   |
| :--: | :-----: |
| <T>  |  Type   |
| <E>  | Element |
| <K>  |   Key   |
| <V>  |  Value  |
| <N>  | Number  |

물론 표에 나온 것처럼 반드시 한글자일 필요도, 설명과 같은 의미로 쓰이지 않아도 된다. 하지만 많은 개발자들이 암묵적으로 표와 같이 쓰기 때문에 우리도 그렇게 사용하자.



## 각 상황별 선언 및 생성 방법

### 1. 클래스 및 인터페이스 선언

```java
public class ClassName <T> {....}
public interface InterfaceName <T> {....}
```

기본적으로 제네릭 타입의 클래스나 인터페이스의 경우 위와 같이 선언한다. T타입은 해당 블록 {....} 안에서까지 유효하다.

또한 여기서 더 나아가 제네릭 타입을 두개로 둘 수 있다. (대표적으로 HashMap이 있다.)

```java
public class ClassName <T, K> { ... }
public interface InterfaceName <T, K> { ... }
 
// HashMap의 경우 아래와 같이 선언되어있을 것이다.
public class HashMap <K, V> { ... }
```

이렇듯 데이터 타입을 외부로부터 지정할 수 있도록 할 수 있다.

그럼 이렇게 생성된 제네릭 클래스를 사용하고 싶을 것이다. 즉, 객체를 생성해야 하는데 이 때 구체적인 타입을 명시 해주어야 한다.

```java
public class ClassName <T, K> { ... }
 
public class Main {
	public static void main(String[] args) {
		ClassName<String, Integer> a = new ClassName<String, Integer>();
	}
}
```

위 예시대로라면 T = String, K = Integer 타입이 된다.

이때 주의해야 할 점은 타입 파라미터로 명시할 수 있는 것은 참조 타입(Reference Type)밖에 올 수 없다. 즉, int, double, char와 같은 primitive type은 올 수가 없다. 

그래서 int형 double형 등 primitive type의 경우 Integer, Double 같은 Wrapper Type으로 쓰는 이유가 바로 위와 같은 이유이다.

또한 바꿔 말하면 참조 타입이 올 수 있다는 것은 사용자가 정의한 클래스도 타입으로 올 수 있다는 것이다.

```java
public class ClassName <T> { ... }
 
public class Student { ... }
 
public class Main {
	public static void main(String[] args) {
		ClassName<Student> a = new ClassName<Student>();
	}
}
```

### 2. 제네릭 클래스

- 제네릭 클래스

```java
// 제네릭 클래스
class ClassName<E> {
	
	private E element;	// 제네릭 타입 변수
	
	void set(E element) {	// 제네릭 파라미터 메소드
		this.element = element;
	}
	
	E get() {	// 제네릭 타입 반환 메소드
		return element;
	}
	
}
 
class Main {
	public static void main(String[] args) {
		
		ClassName<String> a = new ClassName<String>();
		ClassName<Integer> b = new ClassName<Integer>();
		
		a.set("10");
		b.set(10);
	
		System.out.println("a data : " + a.get());
		// 반환된 변수의 타입 출력 
		System.out.println("a E Type : " + a.get().getClass().getName());
		
		System.out.println();
		System.out.println("b data : " + b.get());
		// 반환된 변수의 타입 출력 
		System.out.println("b E Type : " + b.get().getClass().getName());
		
	}
}
```

위 예제를 보면 ClassName이란 객체를 생성할 때 <> 안에 타입 파라미터(Type parameter)를 지정한다.

그러면 a 객체의 ClassName의 E 제네릭 타입은 String으로 모두 변환된다.

반대로 b 객체의 ClassName의 E 제네릭 타입은 Integer으로 모두 변환된다.

위의 코드를 실행시키면 다음과 같이 출력된다.

![제네릭 클래스](https://blog.kakaocdn.net/dn/bwZf3n/btqLeqtwL2Z/juSEIt48ifvKRIPZ6PALL1/img.png)

만약 제네릭을 두 개 쓰고 싶다면 이렇게 할 수도 있다.

```java
// 제네릭 클래스 
class ClassName<K, V> {	
	private K first;	// K 타입(제네릭)
	private V second;	// V 타입(제네릭) 
	
	void set(K first, V second) {
		this.first = first;
		this.second = second;
	}
	
	K getFirst() {
		return first;
	}
	
	V getSecond() {
		return second;
	}
}
 
// 메인 클래스 
class Main {
	public static void main(String[] args) {
		
		ClassName<String, Integer> a = new ClassName<String, Integer>();
		
		a.set("10", 10);
 
 
		System.out.println("  fisrt data : " + a.getFirst());
		// 반환된 변수의 타입 출력 
		System.out.println("  K Type : " + a.getFirst().getClass().getName());
		
		System.out.println("  second data : " + a.getSecond());
		// 반환된 변수의 타입 출력 
		System.out.println("  V Type : " + a.getSecond().getClass().getName());
	}
}
```

결과는 다음과 같다.

![제네릭](https://blog.kakaocdn.net/dn/cOmFzN/btqLcU2HSy0/Ba7cK2T5szTxVrLzGKnKeK/img.png)

이렇게 외부 클래스에서 제네릭 클래스를 생성할 때 <> 괄호 안에 타입을 파라미터로 보내 제네릭 타입을 지정해주는 것. 이것이 바로 제네릭 프로그래밍이다.

### 3. 제네릭 메소드

위 과정까지는 클래스 이름 옆에 예로들어 <E>라는 제네릭 타입을 붙여 해당 클래스 내에서 사용할 수 있는 E 타입으로 일반화를 했다. 그러나 그 외에 별도로 메소드에 한정한 제네릭도 사용할 수 있다.

일반적으로 선언 방법은 다음과 같다.

```java
public <T> T genericMethod(T o) {	// 제네릭 메소드
		...
}
 
[접근 제어자] <제네릭타입> [반환타입] [메소드명]([제네릭타입] [파라미터]) {
	// 텍스트
}
```

클래스와는 다르게 반환타입 이전에 <> 제네릭 타입을 선언한다. 위에서 다룬 제네릭 클래스에서 활용해 보도록 하자.

[제네릭 클래스]

```java
// 제네릭 클래스
class ClassName<E> {
	
	private E element;	// 제네릭 타입 변수
	
	void set(E element) {	// 제네릭 파라미터 메소드
		this.element = element;
	}
	
	E get() {	// 제네릭 타입 반환 메소드 
		return element;
	}
	
	<T> T genericMethod(T o) {	// 제네릭 메소드
		return o;
	}
 
	
}
 
public class Main {
	public static void main(String[] args) {
		
		ClassName<String> a = new ClassName<String>();
		ClassName<Integer> b = new ClassName<Integer>();
		
		a.set("10");
		b.set(10);
	
		System.out.println("a data : " + a.get());
		// 반환된 변수의 타입 출력 
		System.out.println("a E Type : " + a.get().getClass().getName());
		
		System.out.println();
		System.out.println("b data : " + b.get());
		// 반환된 변수의 타입 출력 
		System.out.println("b E Type : " + b.get().getClass().getName());
		System.out.println();
		
		// 제네릭 메소드 Integer
		System.out.println("<T> returnType : " + a.genericMethod(3).getClass().getName());
		
		// 제네릭 메소드 String
		System.out.println("<T> returnType : " + a.genericMethod("ABCD").getClass().getName());
		
		// 제네릭 메소드 ClassName b
		System.out.println("<T> returnType : " + a.genericMethod(b).getClass().getName());
	}
}
```

보면 ClassName이란 객체를 생성할 때 <> 안에 타입 파라미터를 지정한다.

그러면 a객체의 ClassName의 E 제네릭 타입은 String으로 모두 변환된다.

반대로 b객체의 ClassName의 E 제네릭 타입은 Integer으로 모두 변환된다.

genericMethod()는 파라미터 타입에 따라 T 타입이 결정된다.

실제 위 코드를 실행 시키면 다음과 같이 출력된다.

![제네릭 메소드](https://blog.kakaocdn.net/dn/czs31x/btq8zxKbZ05/ftKMjz295wRPDhCSa2UZtK/img.png)

a 객체는 ClassName<String>으로 선언되었기 때문에 <E>의 제네릭 타입은 모두 String이 된다. 그럼에도 a.genericMethod(3).getClass().getName()); 이 부분의 결과가 a 객체의 제네릭 타입에 영향을 받지 않고 Interger 타입을 리턴했다.

이 부분에서 제네릭 메소드는 클래스에 선언된 제네릭 타입을 (그 클래스 안에 들어있는 메소드임에도 불구하고) 무시하고 자신만의 독립적인 타입(파라미터로 받은)을 가지는 것을 확인할 수 있다.

즉, 클래스에서 지정한 제네릭 유형과 별도로 메소드에서 독립적으로 제네릭 유형을 선언하여 쓸 수 있다.

그럼 위와 같은 방식이 왜 필요할까? 바로 '**정적 메소드로 선언할 때 필요**'하기 때문이다.

Static의 성격에 대해 떠올리며 생각해보자. 제네릭의 경우 유형을 외부에서 지정해준다고 했다. 즉, 해당 클래스 객체가 인스턴스화 했을 때, 쉽게 말해 new 생성자로 객체를 생성할 때, <> 괄호 사이에 파라미터로 넘겨준 타입으로 지정 된다는 뜻이다.

하지만 Static은 정적이다. static이 붙은 변수, 메서드의 경우 프로그램이 실행시 메모리에 이미 올라가있다.

이 말은 객체 생성을 통해 접근할 필요 없이 이미 메모리에 올라가 있기 때문에 클래스 이름을 통해 바로 쓸 수 있다는 것이다.

그럼 한 가지 의문이 생긴다. 'Static의 경우 이미 메모리에 올라가있는데 그 타입은 언제 어디서 얻어오는 것이지?'

```java
class ClassName<E> {
 
	/*
	 * 클래스와 같은 E 타입이더라도
	 * static 메소드는 객체가 생성되기 이전 시점에
	 * 메모리에 먼저 올라가기 때문에
	 * E 유형을 클래스로부터 얻어올 방법이 없다.
	 */
	static E genericMethod(E o) {	// error!
		return o;
	}
	
}
 
class Main {
 
	public static void main(String[] args) {
 
		// ClassName 객체가 생성되기 전에 접근할 수 있으나 유형을 지정할 방법이 없어 에러남
		ClassName.getnerMethod(3);
 
	}
}
```

위 내용을 보면 에러가 난다. 그렇기 때문에 제네릭이 사용되는 메소드를 정적 메소드로 두고 싶은 경우 제네릭 클래스와 별도로 독립적인 제네릭이 사용되어야 한다.

```java
static <E> E genericMethod(E o) {...} //이런 식으로 말이다.
```



```java
// 제네릭 클래스
class ClassName<E> {
 
	private E element; // 제네릭 타입 변수
 
	void set(E element) { // 제네릭 파라미터 메소드
		this.element = element;
	}
 
	E get() { // 제네릭 타입 반환 메소드
		return element;
	}
 
	// 아래 메소드의 E타입은 제네릭 클래스의 E타입과 다른 독립적인 타입이다.
	static <E> E genericMethod1(E o) { // 제네릭 메소드
		return o;
	}
 
	static <T> T genericMethod2(T o) { // 제네릭 메소드
		return o;
	}
 
}
 
public class Main {
	public static void main(String[] args) {
 
		ClassName<String> a = new ClassName<String>();
		ClassName<Integer> b = new ClassName<Integer>();
 
		a.set("10");
		b.set(10);
 
		System.out.println("a data : " + a.get());
		// 반환된 변수의 타입 출력
		System.out.println("a E Type : " + a.get().getClass().getName());
 
		System.out.println();
		System.out.println("b data : " + b.get());
		// 반환된 변수의 타입 출력
		System.out.println("b E Type : " + b.get().getClass().getName());
		System.out.println();
 
		// 제네릭 메소드1 Integer
		System.out.println("<E> returnType : " + ClassName.genericMethod1(3).getClass().getName());
 
		// 제네릭 메소드1 String
		System.out.println("<E> returnType : " + ClassName.genericMethod1("ABCD").getClass().getName());
 
		// 제네릭 메소드2 ClassName a
		System.out.println("<T> returnType : " + ClassName.genericMethod1(a).getClass().getName());
 
		// 제네릭 메소드2 Double
		System.out.println("<T> returnType : " + ClassName.genericMethod1(3.0).getClass().getName());
	}
}
```

결과

![제네릭 메소드](https://blog.kakaocdn.net/dn/lC9WD/btq8xDRNmH3/Asbt4i2eMEHH2gNCMalvWk/img.png)

보다시피 제네릭 메소드는 제네릭 클래스 타입과 별도로 지정된다.

<> 괄호 안에 타입을 파라미터로 보내 제네릭 타입을 지정해주는 것이다.

그런데 이런 의문이 들 수 있다. "아니 그러면 특정 범위만 허용하고 나머지 타입은 제한 할 수 없나요?"라는 얘기가 나오기 마련이다. 당연히 가능하다. 다음 파트로 넘어가보자.

## 제한된 Generic 과 와일드 카드

