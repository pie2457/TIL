# Java
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
      <summary> <strong> protected와 private은 각각 언제 사용할 수 있나요? </strong> </summary>
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
   
- 자바는 Call by value 입니다. 메서드에서 파라미터를 넘겨줄 때 파라미터의 reference를 넘겨주는 것이 아닌 파라미터의 메모리 주소를 복사해서 넘겨주기 때문에 Call by value입니다. 예시로 파라미터를 넘겨받은 곳에서 파라미터에 새로운 값을 할당하여도 호출처에서 넘겨준 파라미터는 변경되지 않습니다. 
</details>
<br>

### 📌 interface와 abstract class의 차이는 뭐에요?

<details>
   <summary> 답안 </summary>
<br />

- 추상 클래스와 인터페이스 모두 이를 상속받거나 구현하는 클래스들이 추상메서드를 구현합니다. 추상 클래스는 is-a관계이지만 인터페이스는 has-a 관계를 사용합니다. 
   </details>
<br>

### 📌 JVM이란 무엇이며, JVM의 구조에 대해서 설명해주세요

<details>
   <summary> 답안 </summary>
<br />

- JVM (Java Virtual Machine)은 자바 바이트코드(.class)를 운영체제가 이해할 수 있는 기계어로 변환하여 실행하는 역할을 합니다. 
- JVM은 크게 `클래스 로더(ClassLoader)`, `실행 엔진(ExecutionEngine)`, `런타임 데이터 영역(RuntimeDataArea)` 세가지로 이루어져있습니다. <br>
  - `클래스 로더`는 JVM이 프로그램을 실행할 때 필요한 클래스(.class)를 동적으로 로드합니다. 클래스로더는 자바 애플리케이션 실행 시점에 필요한 클래스만을 로드하는데,
     런타임 시점에 모든 클래스를 로드하는것은 비효율적이기 때문입니다.
  - `실행 엔진`은 클래스 로더가 로드한 클래스의 바이트코드를 실행하는 역할입니다. 실행 엔진은 바이트 코드를 한 줄씩 해석하며 실행하거나, JIT 컴파일러를 사용하여
     바이트코드 전체를 기계어로 변환 후 실행합니다. 또한 실행 엔진은 가비지 컬렉터를 포함하고 있어, 더 이상 사용되지 않는 메모리를 자동으로 정리해줍니다.
  - `런타임 데이터 영역`은 프로그램 실행 중에 사용되는 다양한 데이터를 저장하는 공간입니다. 이 영역은 `메서드 영역`, `힙 영역`, `스택 영역`, `PC 레지스터`, `네이티브 메서드 스택`으로 구분됩니다.
   <br>
   <details>
      <summary> <strong> JVM의 메모리 구조에 대해서 설명해주세요 </strong> </summary>
   <br />

   - JVM의 메모리 구조는 크게 `메서드 영역`, `힙 영역`, `스택 영역`, `PC 레지스터`, `네이티브 메서드 스택`으로 구분됩니다.
     - `메서드 영역`은 클래스의 이름, 타입, 접근제어자 등 클래스와 관련된 정보를 저장합니다.
     - `힙 영역`은 new를 통해 생성된 객체와 배열의 인스턴스 등이 저장되어 있습니다. 가비지 컬렉터는 힙 영역을 청소하며 메모리 공간을 확보합니다.
     - `스택 영역`은 메서드가 실행되면 스택 영역에 메서드에 대한 영역이 1개 생깁니다. 이 영역에 지역변수, 매개변수 등이 저장됩니다.
     - `PC 레지스터`영역에는 현재 쓰레드가 실행되는 부분의 주소와 명령을 저장합니다.
     - `네이티브 메서드 스택`에는 자바 외의 언어(C, C++)로 작성된 코드를 위한 메모리 영역입니다. JNI를 통해 실행됩니다. 
   </details>
<br>
   </details>
<br>

### 📌 가비지 컬렉터(Garbage Collector)란?

<details>
   <summary> 답안 </summary>
<br />

- 가비지 컬렉터란 JVM의 실행 엔진의 한 요소입니다. JVM의 Heap 영역을 위주로 탐색하며 new와 같은 연산에 의해 새롭게 생성된 객체들 중에서 더 이상 참조되지 않는 객체를 정리해 줍니다.
  <br>
  <details>
      <summary> <strong> GC 방식에 대해 아는대로 설명해주세요 </strong> </summary>
   <br />
     
     - Young영역과 Old영역은 메모리 구조가 다르게 되어있어 세부적인 동작 방식은 다르지만 공통된 두가지 방식이 있습니다. <br>
       (1). Stop The World : 가비지 컬렉터를 실행하기 위해 JVM이 애플리케이션 실행을 멈추는 작업입니다. GC를 실행하는 쓰레드를 제외하고 모든 쓰레드들이 중단되고, GC가 완료되면 작업이 재개됩니다. <br>
       (2). Mark And Sweep : <br>
          - Mark : 사용되는 메모리와 사용되지 않는 메모리를 구분합니다.
          - Sweep : Mark 단계에서 사용되지 않음 으로 식별된 메모리를 해제하는 작업입니다. <br>
   
       Stop The World를 통해 모든 작업을 중단시키면, GC는 스택의 모든 변수 또는 Reachable 객체를 스캔하면서 각각이 어떤 객체를 참조하고 있는지를 탐색하게 됩니다.
       그리고 사용되고 있는 메모리를 식별하는데, 이러한 과정을 Mark라고 합니다. 이후에 Mark가 되지 않는 객체들을 메모리에서 제거하는데 이 과정을 Sweep이라고 합니다. 
       <br>

       <strong> <Minor GC의 동작 방식> </strong> <br>
       Minor의 동작 방식은 1개의 Eden의 영역과 2개의 Survivor 영역 총 3가지로 나뉘게 됩니다. <br>
       - 새로 생성된 객체가 Eden 영역에 할당됩니다.
       - 객체가 계속 생성되어 <strong> Eden 영역이 꽉차게 되고 Minor GC가 실행 </strong>됩니다.
          - Eden 영역에서 사용되지 않는 객체의 메모리가 해제 됩니다.
          - Eden 영역에서 살아남은 객체는 1개의 Survivor 영역으로 이동됩니다.
       - 1~2번의 과정이 반복되다가 Survivor 영역이 가득 차게 되면 Survivor 영역에서 살아남은 객체를 다른 Survivor 영역으로 이동시킵니다. (1개의 Survivor 영역은 반드시 빈 상태가 됩니다.)
       - 이러한 과정을 반복하여 계속 살아남은 객체는 Old 영역으로 이동됩니다. <br>

       <strong> <Major GC의 동작 방식> </strong> <br>
       Young 영역에서 오래 살아남은 객체는 Old영역으로 이동하게 되는데, 이런 <strong>Old 영역의 메모리가 부족해지면 Major GC가 발생</strong>하게 됩니다. <br>
       또한 Young 영역보다 Old 영역이 크기 때문에 일반적으로  Major GC가 Minor GC보다 시간이 오래걸리며, 10배 이상의 시간을 사용하게 됩니다.
       참고로 Young 영역과 Old 영역을 동시에 처리하는 GC는 Full GC라고 합니다. 
      
   </details>
<br>
   
</details>
<br>

### 📌 Java 의 synchronized 키워드에 대해 설명해주세요

<details>
   <summary> 답안 </summary>
<br />
   
- 자바에서 지원하는 synchronized 키워드는 여러 쓰레드가 하나의 자원을 이용하고자 할 때, 한 쓰레드가 해당 자원을 사용중인 경우, 데이터에 접근할 수 없도록 막아주는 키워드 입니다. synchronized 키워드를 이용하면 병렬 상황에서 자원의 접근을 안전하게 하지만, 자원을 이용하지 않는 쓰레드는 락에 의한 병목 현상이 일어나게 됩니다. 
</details>
<br>

### 📌 자바의 Generic에 대해 설명해주세요

<details>
   <summary> 답안 </summary>
<br />

- 제네릭은 구체적인 타입에 대한 정보를 타입 정의 시점이 아닌 타입의 인스턴스화 시점에 전달함으로써 하나의 타입으로 여러가지 타입을 표현하는 프로그래밍 기법입니다. 제네릭의 주요 기능은
  다양한 타입의 객체를 다루는 메서드나 클래스에 대해서 컴파일 타임에 타입 체크를 가능하게 하여 타입 안정성을 높이고 형 변환의 번거로움을 줄여주는 것입니다. 
</details>
<br>

### 📌 Java8에 추가된 주요 기능들이 뭐가 있을까요?

<details>
   <summary> 답안 </summary>
<br />

- Lambda, Stream, Optional, 함수형 인터페이스, 인터페이스의 Default 메서드 등이 있습니다. 
</details>
<br>

### 📌 Java의 final 키워드에 대해 설명해주세요

<details>
   <summary> 답안 </summary>
<br />

- 자바의 final 키워드는 어떤 데이터의 불변성을 보장하고 싶을 때 사용합니다. 하지만 인스턴스 타입의 final 키워드를 붙일 경우 그 데이터의 주소값은 변하지 않겠지만, 인스턴스가 가지고있는 데이터는 변할 수 있음을 알고 주의해서 사용해야 합니다. 
</details>
<br>

### 📌 문자열을 "abc"로 선언하는 것과 new String("abc")로 선언하는 것의 차이?

<details>
   <summary> 답안 </summary>
<br />

- 리터럴 문자열을 사용할 경우 JVM 내의 특별한 공간이 String constantPool안에 생성이 되기 때문에 같은 리터럴 문자열에 대해서 새로운 인스턴스를 생성하는 것이 아닌 constantPool안에 선언되어 있는 리터럴 문자열을 그대로 사용하게 됩니다. 하지만 new 연산자를 통해서 String 인스턴스를 만드는 경우 String constantPool안에 생성이 되지 않고 JVM의 Heap 메모리 안에 생성이 됩니다. 같은 문자열이라 할지라도 new 연산자를 통해 생성된 String 인스턴스인 경우 매번 새로운 인스턴스를 생성하게 됩니다. 
</details>
<br>


### 📌 HashMap에 대해 설명해주세요

<details>
   <summary> 답안 </summary>
<br />

- Java의 HashMap은 Map 인터페이스의 구현체 중 하나로 조회의 성능에 있어 O(1)의 시간복잡도를 가지고 있습니다. 내부적으로 값을 저장하기 위한 배열을 가지고 있으며 이를 해시 버킷이라고 부릅니다. 

  <details>
     <summary> <strong> Hash collision 발생 시 자바는 어떻게 대처할까요? </strong> </summary>
   <br />
     
  - Java의 해시맵은 해시 충돌을 해결하기 위해 내부적으로 연결리스트를 활용한 체이닝 방식을 사용하고 있으며, 체이닝의 길이가 일정 길이를 넘어가는 순간 연결리스트가 아닌 트리 자료구조를 사용하고 있습니다. 
  </details>
  <br>

</details>
<br>

### 📌 ==과 equals의 차이?

<details>
   <summary> 답안 </summary>
<br />

- `==`과 `equals`의 차이는 동일성과 동등성의 차이입니다. 동일성은 두 개의 객체와 완전히 같은 경우를 의미합니다. 완전히 같다는 것은 사실상 하나의 객체로 봐도 무방하며
  주소 값이 같기 때문에 두 변수가 같은 객체를 가르키고 있습니다. 동등성은 두 개의 객체가 같은 정보를 갖고 있는 경우를 의미합니다. 동등성은 변수가 참조하고 있는 객체의 주소가
  서로 다르더라도 내용(데이터)만 같으면 두 변수는 동등하다고 얘기할 수 있습니다.

   <details>
     <summary> <strong> Enum의 비교는 ==일까 equals()일까요? </strong> </summary>
   <br />
      
   - enum의 비교는 equals() 메서드를 사용하고 있지만, eqauls 메서드의 내부를 보면 ==으로 비교하고 있기 때문에 사실상 ==과 equals() 메서드 모두 사용이 가능합니다. 
   </details>
   <br>
   
</details>
<br>

### 📌 OOP에 대해 설명해주세요.

<details>
   <summary> 답안 </summary>
<br />
   
- OOP(Object Oriented Programming)란 객체 지향 프로그래밍을 의미합니다. 객체 지향 프로그래밍은 현실 세계를 프로그래밍으로 옮겨와 현실 세계의 사물들을 객체로 보고,
  그 객체로 부터 개발하고자 하는 특징과 기능을 뽑아와 프로그래밍 하는 기법입니다. OOP를 코드로 작성하면 재사용성과 변형 가능성을 높일 수 있습니다.

   <details>
      <summary> <strong> 객체 지향 프로그래밍의 특징에 대해 설명해 주세요. </strong> </summary>
   <br />

   - 객체 지향 프로그래밍은 크게 `추상화`, `캡슐화`, `상속`, `다형성`의 네가지 특징을 가지고 있습니다.
   - 추상화란 객체에서 공통된 속성과 행위를 추출하여 정의하는 것을 의미합니다. 자바에서 추상화를 구현할 수 있는 방법은 인터페이스와 추상클래스가 있습니다.
   - 상속이란 기존의 클래스를 재활용하여 새로운 클래스를 작성하는 방식이며, 클래스들 간의 공유하는 속성과 기능들을 반복적으로 정의할 필요 없이 딱 한번만 정의해두고 재사용 할 수 있어
     반복적인 코드를 최소화하고 공유하는 속성과 기능에 간편하게 접근하여 사용하는 방식입니다. 
   - 다형성이란 어떤 객체의 속성이나 기능이 상황에 따라 여러가지 형태를 가질 수 있는 성질을 의미합니다. 대표적인 예로 메서드 오버라이딩과 오버로딩이 있습니다.
   - 캡슐화란 서로 연관있는 속성과 기능들을 하나의 캡슐로 만들어 데이터를 외부로부터 보호하는 것을 의미합니다. 캡슐화를 하는 이유는 크게
     외부로부터 클래스에 정의된 속성과 기능들을 보호하는 데이터 보호 역할과 내부의 동작을 감추고 외부에는 필요한 부분만을 노출하는 데이터 은닉 두가지로 나뉘어져 있습니다. 
   </details>
   <br>
   
</details>
<br>

### 📌 OOP의 SOLID 원칙에 대해 설명해주세요

<details>
   <summary> 답안 </summary>
<br />

- SOLID원칙은 객체 지향 개발에 대한 5가지 원칙을 가지고 있습니다.
   - SRP(Single Responsibility Principle, 단일 책임 원칙) : 클래스는 단 하나의 목적을 가져야 하며, 클래스를 변경하는 이유는 단 하나의 이유여야 한다.
   - OCP(Open-Closed Principle, 개방 폐쇠 원칙) : 클래스는 확장에 열려있고, 변경에는 닫혀있어야 한다.
   - LSP(Liskov Substitution Principle, 리스코프 치환 원칙) : 상위 타입 객체를 하위 타입으로 변경하여도 프로그램은 일관되게 동작되어야 한다.
   - ISP(Interface Segregation Principle, 인터페이스 분리 원칙) : 클래스는 자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다는 것을 의미한다. ISP는 하나의 일반적인 인터페이스 보단 여러개의 구체적인 인터페이스가 낫다 라고 정의할 수 도 있다. 
   - DIP(Dependency Inversion Principle, 의존 역전 법칙) : 구체화된 클래스가 아닌, 추상화된 인터페이스에 의존해야 한다. 
   </details>
<br>

### 📌 직렬화(Serialization)와 역직렬화(Deserialization)

<details>
   <summary> 답안 </summary>
<br />

   - 직렬화란 객체들의 데이터를 연속적인 데이터(스트림)로 변형하여 전송 가능한 형태로 만드는 것이며, 역직렬화란 직렬화된 데이터를 다시 객체의 형태로 변환하는 것입니다. <br>
     객체 데이터를 통신하기 쉬운 포맷(Byte, CSV, Json..)형태로 만들어주는 작업을 직렬화로 볼 수 있으며, 역으로 포맷(Byte, CSV, Json..)형태에서 객체로 변환하는
     과정을 역직렬화라고 할 수 있습니다. 
   </details>
<br>

### 📌 Boxing과 UnBoxing이 무엇인지 알고있나요?

<details>
   <summary> 답안 </summary>
<br />

- Primitive Type을 Wrapper Class(Reference Type)으로 변환하는 것을 박싱(Boxing)이라고 하며,
  Wrapper Class(Reference Type)을 Primitive Type으로 변환하는 것을 언박싱(UnBoxing)이라고 합니다. <br>
  <img src="https://github.com/pie2457/TIL/assets/104147789/f5c0f3f3-fe59-43c7-9431-71774a977e9d" width="350" height="350"> <br>

   <details>
      <summary> <strong> Boxing과 UnBoxing을 사용하는 이유는? </strong> </summary>
   <br />

   - 제네릭, 자료구조, 매개변수 등 Primitive Type이 아닌 Reference Type을 필요로 하는 경우가 많고,
     Wrapper Class가 메서드를 가지고 있어 다양하게 활용하기 위해 사용됩니다. <br>
     ex) Integer.parseInt(문자열)
</details>
<br>
</details>
<br>
