## Item.6 "불필요한 객체 생성은 피하라."
### 불필요한 객체를 생성하는 경우
```java
String a = new String("hi");
String b = new String("hi");
String c = new String("hi");
```
문자열 a, b, c는 모두 "hi"라는 문자열을 가지게 된다. 하지만, 이 세 문자열이 참조하는 주소는 모두 다르기 때문에 
동일한 데이터에 대해 서로 다른 메모리를 할당하는 낭비가 발생한다. <br>
<img src="https://github.com/user-attachments/assets/8d3d7d27-8ea8-422f-ae2c-b7168f66ead7" width="500" height="250">
<br>
그래서 문자열을 선언할 때는 new 키워드를 사용하는 것이 아닌 리터럴 문자열로 선언해야 한다. 
<br>
```java
String a = "hi";
String b = "hi";
String c = "hi";
```
위 소스 코드는 하나의 인스턴스만 사용한다. 더 나아가 이 방식을 사용한다면 같은 JVM 안에서 "hi" 리터럴 문자열을 사용하는 모든 코드가
같은 객체를 재사용함을 보장한다.

### new Boolean() 사용
```java
Boolean b = new Boolean("true");
```
위 코드는 문자열을 매개변수로 받는 생성자를 통해 Boolean 인스턴스를 만들고 있다. Boolean은 true 혹은 false만 존재하는데,
매번 인스턴스를 만드는 것은 메모리 낭비가 된다. 따라서 정적 팩터리 메서드인 Boolean.valueOf()를 사용하는 것이 좋다. 
```java
Boolean b = Boolean.valueOf("true");
```

### String.matches() 사용
생성 비용이 크면 캐싱하여 재사용하는 것이 좋지만, 항상 우리가 만드는 객체의 비용을 알 수는 없다. 
예를 들어 주어진 문자열이 유효한 로마 숫자인지 확인하는 메서드를 작성하고 싶다면, 다음과 같이 정규표현식을 사용하는 것이 좋다.
```java
public static boolean isRomanNumeral(String s) {
  return s.matches("^(?=.)M*(C[MD]|D?C{0,3})(X[CL]|L?X{0,3})(I[XV]|V?I{0,3})$");
}
```
하지만 String.matches()는 성능적으로 문제가 있는 메서드이다. 이 메서드가 내부에서 만드는 정규표현식용 Pattern 인스턴스는,
한 번 쓰고 버려져서 곧바로 가비지 컬렉션 대상이 되는데, 해당 정규표현식이 반복해서 사용되는 빈도가 높아질수록 동일한 Pattern 인스턴스가
생성되고 버려지는 비용이 커진다. 따라서 Pattern 인스턴스를 미리 캐싱해두고, 나중에 isRomanNumeral() 메서드가 호출될 때 마다
이 인스턴스를 재활용하는 것이 좋다.
```java
public class RomanNumerals {
  private static final Pattern ROMAN = Pattern
		.compile("^(?=.)M*(C[MD]|D?C{0,3})(X[CL]|L?X{0,3})(I[XV]|V?I{0,3})$");

  public static boolean isRomanNumeral(String s) {
    return ROMAN.matcher(s).matches();
  }
}
```
이렇게 개선하면 isRomanNumeral() 메서드가 빈번히 호출되는 상황에서 성능을 상당히 끌어올릴 수 있다.

### 주의사항
위의 모든 예시에서 불필요한 객체를 캐싱할 때 모두 불변 객체로 만들었다. 그래야 재사용해도 안전하기 때문이다.
하지만 불변 객체로 재사용을 한다는 직관에 반대되는 경우가 있다. <br>
어댑터(뷰)는 실제 작업은 뒷단 객체에 위임하고, 자신은 제2의 인터페이스 역할을 해주는 객체다. 어댑터는 뒷단 객체만 관리하면 되므로
뒷단 객체 하나당 어댑터 하나씩만 만들어 주면 된다. <br>
예를 들어 Map 인터페이스의 ketSet() 메서드는 Map 객체 안의 키 전부를 담은 Set뷰를 반환한다.
사용자는 ketSet() 메서드를 호출할 때 마다 새로운 Set 인스턴스가 만들어지리라 생각할 수 있지만, 실제 JDK 구현 내용을 보면
매번 같은 가변 Set 인스턴스를 반환한다. <br>
반환된 Set 인스턴스는 가변일지라도 수행하는 기능이 모두 동일하고, 모든 Set 인스턴스가 Map 인터페이스를 대변하기 때문이다.
따라서 keySet() 객체를 여러 개 만들어도 상관은 없지만, 그럴 필요도 이득도 없다. 
