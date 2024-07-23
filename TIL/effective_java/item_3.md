## "생성자나 열거 타입으로 싱글톤임을 보증하라."
### 싱글톤 개념
싱글톤(singleton)이란 인스턴스를 오직 하나만 생성할 수 있는 클래스를 말한다. 싱글톤의 전형적인 예로는 무상태 객체나
설계상 유일해야 하는 시스템 컴포넌트를 들 수 있다. 하지만 인터페이스로 정의하고 그것을 구현해서 만든 싱글톤 클래스가 아니라면 
테스트하기 어려워질 수 있다는 문제가 발생한다.
### 싱글톤을 만드는 방법 : public static 멤버가 final 필드인 방식
```java
public class Elvis {
  public static final Elvis INSTANCE = new Elvis();

  private Elvis() {}

  public void sing() {
    System.out.println("sing ~ ");
  }

  public static void main(String[] args) {
    Elvis elvis = Elvis.INSTANCE;
    elvis.sing();
  }
}
```
private 생성자는 public static final 필드인 Elvis.INSTANCE를 초기화할 때 딱 한번만 호출된다. public이나 protected 생성자가
없으므로 Elvis 클래스가 초기화될 때 만들어진 인스턴스가 전체 시스템에서 하나뿐임이 보장된다. 단, AccessibleObject.setAccessible()을 사용하여
private 생성자를 호출할 수 있는데, 이러한 리플렉션으로 변조하는 방법은 2번째 객체가 생성될 때 예외를 던져서 막을 수 있다. 
- 장점
  - 해당 클래스가 싱글톤임이 API에 명백히 드러난다.
  - 간결하다.
- 단점1. 싱글톤을 사용하는 클라이언트 코드를 테스트하기 어려워진다.

```java
public class Concert {
  private boolean lightsOn;
  private boolean mainStageOpen;
  private Elvis elvis;

  public Concert(Elvis elvis) {
    this.elvis = elvis;
  }

  public void perform() {
    mainStateOpen = true;
    lightsOn = true;
    elvis.sing();
  }
}
```
Concert라는 클래스가 있고 Concert가 Elvis를 사용하고 있다. 즉, **Concert라는 클래스 자체가 Elvis의 클라이언트 코드**이다. <br>
Cocert 클래스에서 Elvis를 사용하고 있고 Elvis의 sing을 호출할 때 마다 Elvis는 노래를 부르게 된다.
하지만 Elvis가 노래를 부를 때 마다 굉장히 많은 돈이 든다고 가정해 보자. <br>
우리는 Concert를 시작하기 전에 Elvis가 노래를 부를 때 mainState가 Open이 되는지, light가 켜지는지 완벽한 무대와 안전을 위해 여러번 확인을 하고 싶은데,
그 때 마다 Elvis가 와서 노래를 부를 수 없다. 그래서 우리는 대역을 필요로 하는데 대역으로 쓸 수 있는 사람이 없다. 왜? 싱글톤은 인스턴스가 단 하나임을
보장하기 때문이다. 이런 문제를 해결하기 위해 인터페이스로 정의하고 그 구현체를 사용해보자.
```java
public interface IElvis {
  void sing();
}

public class Elvis implements IElvis {
  public static final Elvis INSANCE = new Elvis();

  private Elvis() {}

  @Override
  public void sing() {
    System.out.println("I'm Elvis ! sing ~ ");
  }

  public static void main(String[] args) {
    Elvis elvis = Elvis.INSTANCE;
    elvis.sing();
  }
}

public class Concert {
  private boolean lightsOn;
  private boolean mainStateOpen;
  private Elvis elvis;

  public Concert(IElvis elvis) {
    this.elvis = elvis;
  }

  public void perform() {
    mainStateOpen = true;
    lightsOn = true;
    elvis.sing();
  }
}

public class MockElvis implements IElvis {

  @Override
  public void sing() {
    System.out.println("I'm (mock)Elvis ! sing ~ ");
  }
}
```
```java
class ConcertTest {

  @Test
  void perform() {
    Concert concert = new Concert(new MockElvis());
    concert.perform();
  }
}
```
- 단점2. 리플렉션으로 private 생성자를 호출할 수 있다.
리플렉션을 사용하면 같은 타입의 인스턴스를 여러 개 생성할 수 있게되어 싱글톤이 깨지게 된다.
```java
public class ElvisReflection {
  public static void main(String[] args) {
    try {
      // getDeclaredConstructor()
      // -> 선언되어 있는 기본 생성자. 접근 지시자에 상관없이 private한 생성자도 접근이 가능하다.
      Constructor<Elvis> defaultConstructor = Elvis.class.getDeclaredConstructor();

      // setAccessible(true)로 해주지 않으면 private이어서 생성자를 호출할 수 없게 된다.
      defaultConstructor.setAccessible(true);

      //defaultConstructor를 통해 인스턴스를 생성하면 생성할 때 마다 각기 다른 인스턴스가 생성된다.
      Elvis elvis1 = defaultConstructor.newInstance();
      Elvis elvis2 = defaultConstructor.newInstance();
      System.out.println(elvis1 == elvis2); // -> false
      System.out.println(elvis1 == Elvis.INSTANCE()); // -> false
    } catch (..exception || ..exception etc ..) {
        e.printStackTrace();
    }
  }
}
```
그래서 책에서 권장하는 대안으로는 두번째 객체가 생성되려할 때 예외를 던지게 하는 방식이다.
```java
public class Elvis {
  public static final Elvis INSTANCE = new Elvis();
  private static final boolean created;

  private Elvis() {
    if(created) {
      throw new UnsupportedOperationException("can't be created by constructor");
    }
    created = true;
  }

  public void sing() {
    System.out.println("sing ~ ");
  }

  public static void main(String[] args) {
    Elvis elvis = Elvis.INSTANCE;
    elvis.sing();
  }
}
```
```java
public class ElvisReflection {
  public static void main(String[] args) {
    try {
      Constructor<Elvis> defaultConstructor = Elvis.class.getDeclaredConstructor();
      defaultConstructor.INSTANCE.sing();
      // 두번째 인스턴스 생성 요청 -> 에러 발생.
      Elvis elvis = defaultConstructor.newInstance();
    } catch(..exception || .. exction etc﹒﹒) {
        e.printStackTrace();
    }
  }
}
```
두번째 객체를 생성하려 할 때 예외를 던지도록 코드를 변경해보았다. <br>
Elvis.INSTANCE.sing()을 호출할 땐 문제없이 실행할 수 있지만 리플렉션을 통해 새로운 인스턴스를 생성하려고 하면 에러가 발생하게 된다. 
### 싱글톤을 만드는 방법 : 정적 팩터리 메서드를 public static으로 제공하는 방식
```java
public class Elvis {
  private static final Elvis INSTANCE = new Elvis();

  private Elvis() { }

  public static Elvis getInstance() {
    return INSTANCE;
  }

  public void sing() {
    System.out.println("sing~~");
  }
}
```
리플렉션을 통한 변조 외에는 해당 방법도 전체 시스템에서 유일한 인스턴스임을 보장한다. 단지 필드를 private로 바꾸고,
객체 반환을 정적 팩터리 메서드를 사용해 주고 있다.
- 장점1. API를 바꾸지 않고도 싱글턴이 아니게 할 수 있다.
  - 가령, 정적 팩터리 메서드가 호출하는 스레드 별로 다른 인스턴스를 넘겨주도록 할 수 있다.
```java
public class Elvis {
  private static final Elvis INSTANCE = new Elvis();

  private Elvis() { }

  public static Elvis getInstance() {
    return new Elvis(); // -> private한 기본 생성자를 넘겨주도록 변경
  }
...
}
```
