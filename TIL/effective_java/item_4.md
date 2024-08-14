## Item.4 "인스턴스화를 막으려거든 private 생성자를 사용하라."
가끔 정적 메서드와 정적 필드만을 담은 클래스를 만들고 싶을 때가 있을 것이다. 예를 들어 java.lang.Math와 java.util.Arrays처럼 
기본 타입 값이나 배열 관련 메서드들을 모아 놓을 수 있다. 혹은 java.util.Collections와 같이 특정 인터페이스를 구현하는 객체를 생성해주는
정적 팩터리 메서드를 모아놓을 수 도 있다.<br>
이러한 정적 멤버만 담은 유틸리티 클래스는 별도의 인스턴스 변수나 메서드가 없어도 사용이 가능하므로 생성자가 필요 없다. 
하지만 생성자를 명시해 두지 않으면 컴파일러는 자동으로 public한 생성자를 만들어준다.
하지만 사용자는 이 생성자가 컴파일러에 의해 자동으로 생성된 것인지, 필요에 의해 구현된 것인지 구분할 수 없다. <br>
이러한 상황을 막기 위해 가끔 추상 클래스로 만드는 경우가 있는데, 추상 클래스로 만드는 것으로는 인스턴스화를 막을 수 없다.
하위 클래스를 만들어 인스턴스화하면 그만이기도 하고, 이를 본 사용자는 상속해서 쓰라는 뜻으로 오해를 불러 일으킬 수 있는게 더 큰 문제이다.
```java
public abstract class Utility {

  public static String hello() {
    return "hello";
  }
}

public class DefaultUtility extends Utility {
  public DefaultUtility() {
    super();
  }
}
```
유틸리티 클래스의 인스턴스화를 막는 방법은 아주 간단하다. 
컴파일러가 기본 생성자를 만들기 전에 생성자를 private으로 만들면 클래스의 인스턴스화를 막을 수 있다.
```java
public class Utility {

  private Utility() {
    throw new AssertionError();
  }

  public static String hello() {
    return "hello";
  }
}
```
위와 같이 기본 생성자가 private이니 클래스 외부에서는 접근할 수 없다. 이때 꼭 AssertionError를 던질 필요는 없지만,
클래스 안에서 실수로라도 생성자를 호출하지 않도록 해준다. <br>
하지만 생성자는 있지만 호출할 수는 없다는 것이 사용자 입장에선 이해하기 어려울 수 있다. 이런 상황에서는 적절한 주석을 달아주어
혼란을 방지하는 것도 좋은 방법이 될 수 있다. <br>
또한 생성자를 private으로 선언하는 것은 상속을 불가능하게 하는 효과도 있다.
모든 생성자는 명시적이든 묵시적이든 상위 클래스의 생성자를 호출하게 되는데, 이를 private으로 선언했으니
하위 클래스가 상위 클래스의 생성자에 접근할 길이 막혀버린다.
