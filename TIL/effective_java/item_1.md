## Item.1 생성자 대신 정적 팩터리 메서드를 사용하라.

<details>
<summary>생성자 ?</summary>
    Constructor : 클래스로부터 객체를 생성하기위해 호출하는 메서드 <br>
    ✔️ 생성자의 특징 <br>
    1. new 연산자를 통해서 객체 생성 시, 반드시 호출 되고 제일 먼저 실행된다. <br>
    2. 객체의 초기화(Initialize) 역할을 한다. <br>
    3. 생성자의 이름은 클래스의 이름과 동일해야 한다. <br>
    4. 만약 생성자를 생성하지 않으면, 컴파일러가 자동으로 Default Construtor를 생성, 주입한다. <br>
    5. 파라미터의 구성이 같은 생성자는 두개 이상 만들 수 없다. 예를 들어, String 변수 하나 받는 생성자가 두개 일 수 없다. <br>
            
```java
public class Student {
            
  private String name;
  private String email;
  private String phoneNumber;
            	
  public Student(String name) {
    this.name = name;
  }
            	
  // 사용할 수 없다. 
  // 파라미터가 달라도 타입이 같으면 이미 있는 생성자로 판단.
  public Student(String email) {
    this.email = email;
  }
```
</details>

<details>
<summary>정적 팩토리 메서드 ?</summary>
    정적 팩토리 메서드를 설명하기 전에 이해를 위해 개념을 먼저 정리해 보자.
		<details>
    <summary>개념정리</summary>
        - GoF Pattern : “Gang Of Four”의 줄임말로, 네명의 개발자가 정리한 SoftWare Disign Pattern <br>
        - Software Pattern : 소프트웨어를 설계하는 단계에서 참고할 수 있는 Problem & Solving을 정리해 놓은것. <br>
        - Factory : GoF 패턴에 등장하는 기법 중 하나로, 메소드 하나를 두어 객체 생성의 역할만을 하게 한다는 것. <br>
        - Expert : GoF 패턴에 등장하는 기법 중 하나. 한 객체가 한 기능을 최대한 담당하는 것이 좋다는 이론이다. <br>
        - Low Coupling : GoF 패턴에 등장하는 기법 중 하나이며 OOP의 대원칙. 객체와 객체 사이에 최대한 결합도를 낮추는 것. <br>
        - High Coupling : GoF 패턴에 등장하는 기법 중 하나이며 OOP의 대원칙. 한 기능은 최대한 한 객체에 응집되어 있어야 한다는 것. <br>
    </details>
    정적 팩토리 메서드의 예시
    필자는 객체의 생성을 일반적인 생성자(Constructor)를 통하지 않고 생성을 위한 메서드(Method)를 별도로 만들어 두는 것을 제안하고 있다. <br>

```java
public class Student {
    	
  private int grade;
    	
  private Student(int grade) {
     this.grade = grade;
  }
    	
  public static Student withGrade(int grade) {
     return new Student(grade);
  }
}
    
public class Main {
  public static void main(String[] args) {
    Student student = Student.withGrade(2);
  }
}
```
    
이제부터 생성자와 정적 팩토리 메서드와의 차이가 무엇인지, 장점과 단점을 알아보자.
</details>

## 정적 팩토리 메서드의 장점

## 1. 이름을 가질 수 있다.

### 1-1. 객체의 특성을 쉽게 묘사할 수 있다.

앞에서 말했듯 생성자의 이름은 정의할 수 없으며,  생성자의 이름은 클래스의 이름과 같아야 한다. 이는 생성자의 특징이자 제한이다.

만약 정적 팩토리 메서드를 사용한다면, 클래스 이름과는 다른 보다 특징적인 이름을 지어줄 수가 있다. 

```java
public class Consumer {
	
  private String name;
  private int age;
  private boolean delivery = true;
  private boolean isMember = true;
	
  private Consumer() {}
	
  public static Consumer fromDelivery(String name, boolean delivery) {
    Consumer consumer = new Consumer();
    consumer.name = name;
    consumer.delivery = delivery;
    return consumer;
  }
	
  public static Consumer fromMember(String name, boolean isMember) {
    Consumer consumer = new Consumer();
    consumer.name = name;
    consumer.isMember = isMember;
    return consumer;
  }
	
	
public Class Main {
  public static void main(String[] arge) {
    Consumer consumer1 = consumer.fromDelivery("James", true);
    Consumer consumer2 = consumer.fromMember("Olive", true);
  }
}
```

일반적인 생성자는 클래스 이름과 같은 이름을 가진다는 제약이 있기 때문에 무슨 의도인지, 무엇으로 만드는지 파악하기가 어렵다. 

그런데 위의 예시를 보면, “제임스는 배송을 신청했구나”, “올리브는 회원이구나”라는 정보를 알수있다.

무엇때문에 ? **정적 팩토리 메서드의 이름**때문이다. 결과적으로 **코드의 가독성을 높여준다**.

### 1-2. “하나의 시그니처로 생성자를 하나만 만들 수 있다”라는 제약이 없다.

생성자의 입력 매개변수의 순서를 바꿔 오버라이딩 해보겠다는 생각으로 제한을 피해볼 순 있지만겠지만, **어떤 역할을 하는지 구분할 수 는 없어 좋은 발상은 아니다**.

```java
public class Consumer {
	
  private String name;
  private int age;
  private boolean fromDelivery;
  private boolean fromMember;
	
  public Consumer(String name, int age, boolean fromDelivery) {
    this.name = name;
    this.age = age;
    this.fromDelivery = fromDelivery;
  }
	
  // 단순히 매개변수의 String과 int의 순서만 바꿔도 다른 형태의 매개변수를 받는다고 인식.
  public Consumer(int age, String name, boolean fromMember) {
    this.age = age;
    this.name = name;
    this.fromMember = fromMember;
  }
}

public class Main {
  public static void main(String[] arge) {
    Consumer consumer1 = new Consumer("James", 24, true);
    Consumer consumer2 = new Consumer(24, "Olive", false);
    // 생성자만 보고는 어떤 역할을 하는지 구분할 수 없음.
  }
}
```

따라서 한 클래스에 시그니처(파라미터)가 같은 생성자가 여러개 필요한 경우, 정적 팩토리 메서드를 활용하는 것은 굉장히 효율적인 방법이다.

### 2. 호출될 때마다 인스턴스를 새로 생성하지 않아도 됨.

이 장점에서 유심히 보아야 하는 것은, “**생성하지는**”이라고 표현한 것이다. 

자주 사용하는 인스턴스를 미리 만들어 놓고, 캐시에 저장해놓는 방법으로 새로 생성하지 않고 반환하는 방식으로 정적 팩토리 메서드를 활용할 수 있다는 것이다.

이는 다음과 같은 의미를 내포하게 된다.

> - 필요에 따라 **항상 새로운 객체를 생성**해서 반환할 수 있다.
> - 필요에 따라 **새로운 객체 생성을 금지하고 같은 객체만 반환**할 수 있다.
> - **불필요한 객체를 굳이 만들지 않게 하도록 통제**할 수 있다.
> 

일반적인 생성자를 사용할 경우 호출할 때 마다 항상 새로운 객체를 만들게 된다. 그런데 인스턴스의 내용이 바뀔 일도 없고, 호출 빈도수가 매우 잦은데 생성 비용까지 크다면 자원 낭비가 심하게 된다.

하지만 정적 팩토리 메서드를 사용한다면, 경우에 따라 어떤 클래스는 객체를 만들지 못하도록 하거나, 객체를 오로지 하나만 만들도록 할 수 있기 때문에 위와 같은 특수적인 상황에서는 효율성이 증대되며 빛을 발한다.

가장 대표적인 예시로 Boolean.valueOf(boolean) 메서드는 새로운 객체를 아예 생성하지 않는다.

```java
public static final Boolean TRUE = new Boolean(true);
public static final Boolean FALSE = new Boolean(false);

public static Boolean valueOf(boolean b) {
  return (b ? TRUE : FALSE);
}
```

Boolean.TRUE와 Boolean.FALSE를 미리 불변 객체로 생성한 후에, valueOf 메서드로 해당 불변 객체를 리턴한다. 

따라서 생성자를 통해 Boolean 객체를 생성하면 새로운 인스턴스가 생성되지만, valueOf를 통해 Boolean 객체를 생성하면, 새로운 인스턴스가 생성된 것이 아니라 이미 만들어 놓은 불변 객체를 반환할 수 있다.

### 3.  반환 타입의 하위 타입 객체를 반환할 수 있는 능력이 있다.

이 능력은 반환할 객체의 클래스를 자유롭게 선택할 수 있게 하는 엄청난 유연성을 제공한다. 아래의 예제를 살펴보자.

인터페이스를 예로 들면,

```java
public interface Grade {
	
  String toText();
	
  static Grade of (int score) {
    if (score >= 90) {
      return new A();
    } else if (score >= 80) {
      return new B();
    } else {
      return new F();
    }
  }
```

```java
public class A implements Grade {
	
  @Override
  public String toText() {
    return "A";
  }
}

public class B implements Grade {
	
  @Override
  public String toText() {
    return "B";
  }
}

public class F implements Grade {
	
  @Override
  public String toText() {
    return "F";
  }
}
```

```java
public class Application {
  public static void main(String[] args) {
    Grade grade = Grade.of(95);
    System.out.println(grade);
  }
}
```

코드를 간략히 설명해보자면, Grade라는 인터페이스를 A, B, C라는 클래스가 구현하고 있다. 또 정적 팩토리 메서드인 of()의 반환 타입은 Grade이다. 그런데 실제로 of()메서드를 보면 반환은 A, B, C 클래스의 인스턴스(생성자)로 하고 있다.

이처럼 **정적 팩토리 메서드를 사용하면, 반환 타입 (인터페이스 : Grade)의 하위 타입 (구현 클래스 : A, B, C) 객체를 반환하는게 가능**하다. 

이게 유연성과 무슨 상관이 있느냐? 먼저 위 코드에서 볼 수 있듯 **Grade의 of() 메서드는 조건에 따라 다른 객체를 자유롭게 선택하여 반환**한다. 즉 **엄청난 유연성**을 보여준다.

또, Grade 클래스 내에 구현체가 있는 것이 아니고 **Grade는 실제 구현체를 연결해주는 역할만 하기 때문에 구현 로직은 숨길 수 있으면서, API는 매우 경량화** 된다. 

### 4. 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다.

3번의 장점과 4번의 장점의 내용의 맥락이 서로 같다. **3번은 반환 타입의 하위 객체를 반환할 수 있다는 유연성에 초점**을 두고있고, **4번은 반환 타입의 하위 타입이기만 하면, 어떤 클래스의 객체를 반환해도 상관없기 때문에  다양한 객체를 선택적으로 반환할 수 있다는 기능적인 측면에 초점**을 두고 있다. 

예를 들면, EnumSet 클래스는 public 생성자 없이 정적 팩토리 메서드만 제공한다고 한다. 원소의 수에 따라서 64개 이하면 원소를 long변수 하나로 관리하는 RegularEnumSet 인스턴스를, 65개 이상이면 long 배열로 관리하는 JumboEnumSet의 인스턴스를 반환한다고 한다. 

```java
public static <E extends Enum<E>> EnumSet<E> noneOf(Class<E> elementType) {
  Enum<?>[] universe = getUniverse(elementType);
        
  if (universe == null)
     throw new ClassCastException(elementType + " not an enum");
  if (universe.length <= 64)
     return new RegularEnumSet<>(elementType, universe);
  else
     return new JumboEnumSet<>(elementType, universe);
}
```

우리가 EnumSet 클래스를 정적 팩토리 메서드로 생성한다고 했을 때, 우리는 이 내부 존재를 몰라도 된다. 하위 클래스의 삭제가 일어나도, 성능을 개선해도, 새로운 하위 클래스가 생겨도 전혀 지장이 없다는 것도 또 하나의 장점이다. 

### 5. 정적 팩토리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다.

5번 장점의 설명이 어렵게 되어 있지만 쉽게 말해서 **아예 선언한 적 없는 클래스를 정적 팩토리 메서드의 리턴 값으로 정의할 수 있다는 뜻이 아니라**, **‘인터페이스’를 생성하고 내부 구현체 클래스를 구현하지 않은 상태**에서 정적 팩토리 메서드의 리턴 값으로 사용이 가능하다는 뜻이다. 

예제를 통해 다시 이해해보자.

```java
package algorithm.dataStructure;

public abstract class StaticFactoryMethodType {

  public abstract void getName();

  public static StaticFactoryMethodType getNewInstance() {
        StaticFactoryMethodType temp = null;
        try {
            Class<?> childClass = Class.forName("algorithm.dataStructure.StaticFactoryMethodTypeChild"); // 리플렉션
            temp = (StaticFactoryMethodType) childClass.newInstance(); // 리플렉션
        } catch (Exception e) {
           // error handling..
        }

        return temp;
    }
}
```

위 코드를 보면 인터페이스 구현체의 위치를 통해 Class 객체를 생성하고, 리플렉션 기술을 사용하여 실제 구현체를 초기화 하는 것을 확인할 수 있다. 이때 정적 팩토리 메서드를 작성하는 시점에는 StaticFactoryMethodTypeChild 클래스는 존재하지 않아도 된다. 

만약 정적 팩토리 메서드를 사용하는 시점에 algorithm.dataStructure.StaticFactoryMethodTypeChild  경로에 대해 구현체가 없다면 에러가 발생하겠지만, 정적 팩토리 메서드를 작성하는 시점에는 문제가 없으므로 유연하다고 하는 것이다. 

```java
public interface Test {

    int sum(int a, int b);

 // Test는 인터페이스고 구현체가 없더라도 정적 팩터리 메서드 작성 시점에는 문제가 발생하지 않는다.
    static Test create() {
        return null;
    }
}

public class Main {
    public static void main(String[] args) {
        Test test = Test.create();
        System.out.println(test.sum(1, 2)); // NPE 발생
    }
}
```

리플렉션을 사용하지 않더라도 똑같은 유연함을 얻을 수 있다. **Test의 정적 팩토리 메서드인 Create()를 보면, 구현체가 없더라도 작성 시점에는 아무 문제가 발생하지 않는다**. 물론 실제 사용 시점에는 NPE가 발생하니, 나중에 구현체를 반환해 주어야 한다.

이러한 유연함은 서비스 제공자 프레임워크를 만드는 근간이 되는데, 대표적으로 JDBC가 있다. JDBC 서비스 제공자 프레임워크의 제공자는 서비스의 구현체이고, 이 구현체들은 클라이언트에 제공하는 역할을 프레임워크가 통제하여, 클라이언트를 구현체로부터 분리한다. (DIP)

## 정적 팩토리 메서드의 단점

## 1. 상속을 하려면 public이나 protected 생성자가 필요하므로 정적 팩토리 메서드만 제공한다면 하위 클래스는 만들 수 없다.

상속(Extend) 기능을 사용하기 위해서는 public이나 protected 형태의 생성자가 필요한데, 정적 팩토리 메서드는 외부에서 생성자를 사용하지 못하게 해야하니 private 형태로 선언하기 때문에 상속을 통한 확장이 불가능 하다. 하지만 방법이 아예 없는 것은 아니다.

```java
public class Child { 
	
  Parent parent;
}
```

위 예제와 같이 상속받고 싶은 클래스(Child)에서 상속하고 싶은 클래스(Parent)를 Delegation해서  Parent를 가지고 있게한다면 굳이 상속을 하지 않더라도 Child 클래스 안에서 Parent클래스의 기능들을 활용할 수 있어서 일종의 장점으로도 볼 수 있다. 

### 2. 정적 팩토리 메서드는 프로그래머가 찾기 어렵다.

보통 생성자(Constructor)의 경우 클래스의 최상단부에 위치하고 이름 또한 클래스 명과 같은데, 
정적 팩토리 메서드의 경우 별다른 위치가 정해져있지 않고 이름 또한 제약이 없기 때문에 언뜻 보았을 땐 일반 메서드와의 차이를 구별하기 쉽지 않다. 

생성자처럼 API 설명에 명확하게 드러나지 않으니 단점을 극복하기 위해선 문서를 잘 관리하는 것도 하나의 방법으로 생각된다.
