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
