# Java-Spring
<br>

### 📌 Spring과 Springboot 차이 

<details>
   <summary> 답안 </summary>
<br />

- Spring은 스프링 프로젝트의 모음집입니다. 스프링은 필요한 빈 객체를 등록하고, 빈 객체들간의 의존성을 설정해주어야 했으며 또한 개발자가 필요한 라이브러리들을 직접 추가하고 여러가지 설정들을 직접 함으로써 스프링 프레임워크를 사용하는데 어려움이 있었습니다. 이런 문제를 해결하기 위해 나온 서브 프로젝트가 Springboot입니다. 스프링부트를 사용함으로써 자동으로 빈 객체를 등록하고, 객체간의 의존성을 설정해 주는 등 스프링에서 제공하는 여러 기능들을 자동으로 설정하여 개발자가 보다 쉽게 사용할 수 있도록 도와주는 도구입니다.
</details>
<br>

### 📌 Java의 접근 제어자에는 어떤게 있어요?

<details>
   <summary> 답안 </summary>
<br />
   
- 자바의 접근 제어자는 크게 `public`, `private`, `protected`, `default`가 있습니다. <br>
  public은 모든 접근을 허용하여 외부 클래스에서도 자유롭게 사용이 가능합니다 <br>
  private 모든 접근을 제한하여 외부에서의 접근은 불가하고, 같은 클래스 내에서만 접근이 가능합니다. <br>
  protected는 이를 상속받은 자식 클래스와, 같은 패키지안의 모든 클래스만 접근이 가능합니다. <br>
  default는 클래스에 접근제어자가 없으면 default로 선언되며, 같은 패키지안의 클래스에서만 접근이 가능합니다.<br>

  <details>
      <summary> protected와 private은 각각 언제 사용할 수 있나요? </summary>
   <br />
   
  - protected를 사용하는 주된 이유는 무분별한 인스턴스 생성을 방지하고 , 해당 클래스를 상속받은 클래스와 같은 패키지내의 클래스만 생성자를 호출할 수 있게 제한함으로써 객체의 일관성을 유지하기 위해서 사용합니다. <br>
        private을 사용하는 주된 이유는 정보은닉과 캡슐화를 위해 사용합니다. 클래스 내부에 있는 데이터를 보호하고 데이터에 접근 자체를 막아주어 일관성을 보장하기 위해 사용됩니다. 
   
   </details>
   <br>
   
</details>
<br>

### 📌 Java는 Call by value일까요 Call by reference 일까요? 

<details>
   <summary> 답안 </summary>
<br />
   
- 자바는 Call by value 입니다. 메서드에서 파라미터를 넘겨줄 때 파라미터의 reference를 넘겨주는 것이 아닌 파라미터의 메모리 주소를 복사해서 넘겨주기 때문에 Call by value입니다. 예시로 파라미터를 넘겨받은 곳에서 파라미터에 새로운 값을 할당하여도 호출처에서 넘겨준 파라미터는 변경되지 않습니다. 
</details>
<br>

### 📌 interface와 abstract class의 차이는 뭐에요?

<details>
   <summary> 답안 </summary>
<br />

- 추상 클래스와 인터페이스 모두 이를 상속받거나 구현하는 클래스들이 추상메서드를 구현합니다. 추상 클래스는 is-a관계이지만 인터페이스는 has-a 관계를 사용합니다. 
   </details>
<br>

### 📌 JVM의 구조에 대해서 설명해주세요

<details>
   <summary> 답안 </summary>
<br />

- JVM은 크게 `클래스로더(ClassLoader)`, `실행 엔진(ExecutionEngine)`, `런타임 데이터 영역(RuntimeDataArea)` 세가지로 이루어져있습니다. <br>
  클래스로더는 JVM이 프로그램을 실행할 때 필요한 클래스(.class)를 동적으로 로드합니다. 클래스로더는 자바 애플리케이션 실행 시점에 필요한 클래스만을 로드하는데,
  런타임 시점에 모든 클래스를 로드하는것은 비효율적이기 때문입니다. 
  
  
   </details>
<br>


