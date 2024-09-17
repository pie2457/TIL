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

