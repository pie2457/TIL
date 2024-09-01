## Item.5 "자원을 직접 명시하지 말고 의존 객체 주입을 사용하라."
클래스가 내부적으로 하나 이상의 자원에 의존하고, 사용하는 자원에 따라 동작이 달라지는 클래스에는
정적 유틸리티 클래스나 싱글턴 방식이 적합하지 않다. 이 자원들을 클래스가 직접 만들게 해서도 안되며,
그 대신 필요한 자원을 생성자에게 넘겨주는 것이 바람직하다. 의존 객체 주입을 통해 클래스의 유연성, 재사용성, 테스트 용이성을 개선할 수 있다.
```java
public class SpellChecker {
  private static final Lexicon dictionary = new Lexicon();

  private SpellChecker() {} // 객체 생성 방지

  public static boolean isVaild(String word) {
    // dictionary를 사용한 로직
  }

  public static List<String> suggestions(String typo) {
    // dictionary를 사용한 로직
  }
}
```
해당 클래스는 사전을 하나만 사용한다고 가정하고 있다. 하지만 현실에서는 사전이 언어별로 따로 있고, 
심지어 특수 어휘용 사전을 별도로 두는 경우도 있다.
```java
public class SpellChecker {
  private final Lexicon dictionary = new Lexicon();

  public static SpellChecker INSTANCE = new SpellChecker();

  private SpellChecker() {}

  public static boolean isVaild(String word) {
    // dictionary를 사용한 로직
  }

  public static List<String> suggestions(String typo) {
    // dictionary를 사용한 로직
  }
}
```
싱글턴 클래스도 마찬가지로 사전을 하나만 사용한다고 가정하므로 위와 같은 단점이 발생한다.
```java
public class SpellChecker {
  private Lexicon dictionary = new Lexicon();

  public static SpellChecker INSTANCE = new SpellChecker();

  private SpellChecker() {}

  public static void changeDictionary(Lexicon dictionary) {
    this.dictionary = dictionary;
  }

  public static boolean isVaild(String word) {
    // dictionary를 사용한 로직
  }
	
  public static List<String> suggestions(String typo) {
    // dictionary를 사용한 로직
  }
}
```
정적 유틸리티 클래스 혹은 싱글턴 클래스의 dictionary에 대해 final 키워드를 제거하고 외부에서
dictionary를 다른 사전으로 교체하도록 설계할 수 있다. 하지만 해당 방식은 사용이 어색하고,
오류를 내기 쉬우며 멀티스레드 환경에선 동시성 문제를 야기할 수 있다.
```java
public class SpellChecker {
  public final Lexicon dictionary;

  public SpellChecker(Lexicon dictionary) {
    this.dictionary = dictionary;
  }

  public static boolean isVaild(Strinf word) {
    // dictionary를 사용한 로직
  }

  public static List<String> suggestions(String typo) {
    // dictionary를 사용한 로직
  }
}
```
정적 클래스와 싱글턴 클래스는 내부적인 자원에 의존하면 안된다는 사실을 위 예제를 통해 느낄 수 있었다.
즉, 내부 자원은 외부에서 주입을 받는 것이 바람직하다는 뜻이다.<br>
의존 객체 주입을 사용한 클래스는 final 키워드 덕분에 불변을 보장할 수 있고, 여러 자원 인스턴스를 지원한다는
장점이 있다. 또한, 의존 객체 주입은 생성자 뿐 아니라 정적 팩터리와 빌더에서도 응용이 가능하다. <br>
의존 객체 주입은 단순하게 자원 그 자체를 넘겨주는 방법도 있지만, 자원 팩터리를 넘겨주는 방식도 종종 사용된다.
팩터리란 호출할 때 마다 특정 타입의 인스턴스를 반복해서 만들어주는 객체를 말한다. 이러한 방식은 팩터리 메서드 패턴이라고 하며,
자바 8에서 Supplier<T> 인터페이스가 팩터리를 표현한 완벽한 예시이다.
```java
public static List<Car> create(Supplier<? extends Car> generator) {
  ...
}
```
Supplier<T>를 입력으로 받는 메서드는 일반적으로 한정적 와일드카드 타입을 사용해 팩터리의 타입 매개변수를 제한한다.
이 방식을 사용해 클라이언트는 자신이 명시한 타입의 하위 타입이라면 무엇이든 생성할 수 있는 팩터리를 넘길 수 있다.<br>
의존 객체 주입이 유연성과 테스트 용이성을 개선해주긴 하지만, 의존성이 수천 개나 되는 큰 프로젝트에서는 코드를 어지럽게 만들기도 한다.
이런 경우 의존 객체 프레임워크(Dagger, Guice, Spring 등)을 사용하면 해결할 수 있다.
