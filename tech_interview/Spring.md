# Spring

### 📌 Spring과 Springboot 차이 

<details>
   <summary> 답안 </summary>
<br />

- Spring은 스프링 프로젝트의 모음집입니다. 스프링은 필요한 빈 객체를 등록하고, 빈 객체들간의 의존성을 설정해주어야 했으며 또한 개발자가 필요한 라이브러리들을 직접 추가하고
  여러가지 설정들을 직접 함으로써 스프링 프레임워크를 사용하는데 어려움이 있었습니다. 이런 문제를 해결하기 위해 나온 서브 프로젝트가 Springboot입니다.
  스프링부트를 사용함으로써 자동으로 빈 객체를 등록하고, 객체간의 의존성을 설정해 주는 등 스프링에서 제공하는 여러 기능들을 자동으로 설정하여
  개발자가 보다 쉽게 사용할 수 있도록 도와주는 도구입니다.
  </details>
<br>

### 📌 Springboot가 해결하려 했던 건 뭐라고 생각하나요?

<details>
   <summary> 답안 </summary>
<br />

- Springboot가 등장하기 이전 Spring을 사용해 간단한 서버를 띄우기 위해서는 수많은 빈 설정과 의존관계를 개발자가 하나하나 설정해줘야 했습니다.
  이러한 이유들로 개발자는 비즈니스 로직에 집중하기 어려웠고, 많은 시간을 쏟아야 했습니다. 이런 문제들을 해결하기 위해 등장한 것이 스프링 부트라고 생각합니다.
  </details>
<br>

### 📌 FrontController 패턴이 뭐에요?

<details>
   <summary> 답안 </summary>
<br />
   
- FrontController 패턴은 요청을 받는 컨트롤러를 하나로 두어 요청을 한 곳에서 처리하도록 한 패턴입니다. Spring MVC에서는 이 패턴을 적용한
  FrontController가 DispatcherServlet이라 할 수 있습니다.
  </details>
<br>

### 📌 Spring MVC의 동작원리

<details>
   <summary> 답안 </summary>
<br />
   
![image](https://github.com/pie2457/TIL/assets/104147789/6cabb7d3-310d-4ff1-b3d4-5825f72e0aba)

1. 클라이언트는 URL을 통해 요청을 전송합니다.
2. 디스패처 서블릿은 핸들러 매핑을 통해 해당 요청이 어느 컨트롤러에게 온 요청인지 찾습니다.
3. 디스패처 서블릿은 핸들러 어댑터에게 요청의 전달을 맡깁니다.
4. 핸들러 어댑터는 해당 컨트롤러에 요청을 전달합니다.
5. 컨트롤러는 비즈니스 로직을 처리한 후에 반환할 뷰의 이름을 반환합니다.
6. 디스패처 서블릿은 뷰 리졸버를 통해 반환할 뷰를 찾습니다.
7. 디스패처 서블릿은 컨트롤러에서 뷰에 전달할 데이터를 추가합니다.
8. 데이터가 추가된 뷰를 반환합니다.
  </details>
<br>

### 📌 IoC/DI는 무엇이고 어떠한 장점이 있나요?

<details>
   <summary> 답안 </summary>
<br />

- 스프링의 핵심 철학 중 하나는 Ioc/DI, 제어의 역전과 의존성 주입입니다. IoC는 프로그램의 실행 흐름이나 객체의 생명주기를 개발자가 아닌 외부에 위임하는 기술이며,
  DI는 객체를 직접 생성하는게 아니라 외부에서 생성한 후 주입시켜주는 방식입니다.
  IoC를 이용 함으로써 개발자는 부품을 만들어 조립하는 다양한 형태의 개발이 가능해졌고
  DI를 사용함으로써 코드 간의 재사용성을 높이고, 코드를 다양한 곳에 사용하며 객체간의 결합도를 낮출 수 있습니다.

   <details>
      <summary> <strong> Spring IoC 컨테이너는 뭐에요? </strong> </summary>
   <br />

   - Spring IoC 컨테이너는 개발자를 대신해 빈의 생성과 의존성 주입,생명주기 관리를 책임집니다.
   </details>
   <br>

  </details>
<br>

### 📌 Spring으로 개발하실 때 어떠한 DI 방식을 사용하시나요?

<details>
   <summary> 답안 </summary>
<br />

- 생성자 주입, Setter 주입, 필드 주입 방식 중 Spring에서 권장하는 방식인 생성자 주입 방식을 사용하고 있습니다. 
   - `생성자 주입(Constructor Injection)` : 생성자 주입 방식은 생성자의 호출 시점에 1회 호출되는 것이 보장됩니다. 그렇기 때문에 주입받은 객체가 변하지 않거나, 반드시 객체의 주입이 필요한 경우에 강제하기 위해 사용할 수 있습니다.
   - `Setter 주입(Setter Injection)` : Setter 주입 방식은 필드 값을 변경하는 Setter를 통해서 의존 관계를 주입하는 방식입니다. Setter 주입은 생성자 주입과 다르게 주입받는 객체가 변경될 가능성이 있는 경우에 사용됩니다.
   - `필드 주입(Field Injection)` : 필드 주입 방식은 필드에 바로 의존 관계를 주입하는 방식입니다. 과거에는 필드 주입을 이용하면 코드가 간결해져 많이 사용했던 방법입니다.
   <br>
   <details>
      <summary> <strong> 왜 필드 주입은 사용하면 안된다 할까요? 단점이 뭐라고 생각하세요? </strong> </summary>
   <br />

   - 필드 주입 방식은 final 키워드를 사용할 수 없으며, 외부에서의 접근이 불가하여 테스트 코드를 작성하기 어려워진다는 단점이 있습니다. 
   </details>
   <br>
   
   <br>
   <details>
      <summary> <strong> 그러면 생성자 주입은 뭐가 좋아요? </strong> </summary>
   <br />

   - 테스트 코드 작성에 용이하며, 객체의 변경 가능성을 제거하고 불변성을 확보할 수 있는 등의 이점이 있습니다.
   </details>
   <br>
   
  </details>
<br>

### 📌 Spring AOP(Asept Oriented Programming)는 뭔가요?

<details>
   <summary> 답안 </summary>
<br />

- AOP는 관점 지향 프로그래밍으로 여러 객체에 공통적으로 적용할 수 있는 기능을 분리해서 재사용성을 높여주는 프로그래밍 기법입니다. <br>

   <details>
     <summary> 언제 AOP를 사용할 수 있을까요? </summary>
   <br />

   - 로깅 처리를 하거나 트랜잭션 처리를 할 때 사용할 수 있을 것 같습니다. 
   </details>
<br>
  </details>
<br>

### 📌 Spring bean이란?

<details>
   <summary> 답안 </summary>
<br />

- Spring bean이란 스프링 IoC 컨테이너에 의해 관리되는 자바 객체로써 컨테이너에 의해 생명주기가 관리되는 객체를 의미합니다. 


   <details>
      <summary> <strong> Bean Scope의 종류에 대해 아는 만큼 알려주세요 </strong> </summary>
   <br />
      
   -  Scope의 종류는 크게 `싱글톤`, `프로토타입`, `웹` 3가지로 나뉘어져 있습니다.
      - `싱글톤` : 싱글톤은 스프링 프레임워크에서 기본이 되는 스코프이며 스프링 컨테이너의 시작과 종료까지 1개의 객체로 유지됩니다.
      - `프로토타입` : 프로토타입 빈의 생성과 의존관계 주입까지만 관여하고 더는 관리하지 않는 스코프입니다. 요청이 오면 항상 새로운 인스턴스를 생성하여 반환하고
       그 이후로는 관리하지 않습니다.
      - `웹` : 웹 안에서도 3가지 종류로 구분되는데
         - `request` : 각각의 요청이 들어오고 나갈때까지 유지되는 스코프입니다.
         - `session` : 세션이 생성되고 종료될 때까지 유지되는 스코프입니다.
         - `application` : 웹의 서블릿 컨텍스트와 같은 범위로 유지되는 스코프입니다. 
   </details>
   <br>
      
  </details>
<br>

### 📌 Spring MVC에서 Interceptor와 Filter차이

<details>
   <summary> 답안 </summary>
<br />

- Filter의 경우 Spring Context 영역 밖에서 동작합니다. 또한 요청이 Servlet으로 가기 전 요청을 가로채 로직을 수행할 수 있습니다. 필터의 다른 특징은 여러 필터들을 모아
  체이닝을 할 수 있다는 것입니다. <br>
  Interceptor는 Spring Context 영역 내 DispatcherServlet과 Controller 사이에서 동작하는 것이 필터와의 다른점 입니다.
  Interceptor 또한 필터처럼 체이닝을 구성할 수 있다는 것이 특징입니다. 
  </details>
<br>

### 📌 ORM(Object-Relational Mapping)이란?

<details>
   <summary> 답안 </summary>
<br />

- ORM이란 객체와 데이터베이스의 패러다임 불일치를 해결하기 위한 도구입니다. 관계형 데이터베이스와 객체 지향 프로그래밍 언어 간의 호환되지 않는 데이터를 자동으로 매핑(연결)해주어
  SQL문이 아닌 프로그래밍 언어로도 데이터베이스에 접근할 수 있게 해주는 툴입니다. ORM은 SQL문법 대신 프로그래밍 언어를 그대로 사용할 수 있게 함으로써, 프로그래밍 언어의 일관성과
  가독성을 높여준다는 장점을 가지고 있습니다. 
  </details>
<br>

### 📌 JPA(Java Persistence API)란?

<details>
   <summary> 답안 </summary>
<br />

- JPA는 Java에서 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스입니다. 실제적으로 구현되어 있는 것이 아니라 구현된 클래스와 매핑을 해주기 위해
  사용되는 프레임워크입니다. JPA를 구현한 대표적인 오픈소스로는 Hibernate가 있습니다. <br>
  <img src="https://velog.velcdn.com/images/murphytklee/post/ffac55b5-ff42-4156-aa3c-f3c494dad492/image.png" width="700" height="300">
  
   <details>
      <summary> <strong> Hibernate란? </strong> </summary>
   <br />

   - JPA의 구현체 중 하나인 Hibernate는 SQL을 사용하지 않고 직관적인 코드(메서드)를 사용해 데이터를 조작할 수 있습니다.
     하이버네이트는 JPA 인터페이스를 구현하고 있으며 내부적으로 JDBC API를 사용합니다. 하이버네이트의 역할은 JPA에서 메서드로 요청된 정보들을 JDBC가 잘 알아 들을 수 있도록
     한번 더 표준화 작업을 해준 뒤 JDBC에게 넘겨줍니다.
   </details>
   <br>

   <details>
      <summary> <strong> JDBC(Java Database Connectivity)란 ? </strong> </summary>
   <br />

   - JDBC란 데이터베이스에 연결 및 작업을 하기 위한 자바 표준 인터페이스입니다.
     JDBC는 DBMS의 종류에 상관없이 하나의 JDBC API를 이용해서 하나의 문법으로 통일시켜 데이터베이스 작업을 처리합니다.
   </details>
   <br>
  </details>
<br>


### 📌 JPA 영속성 컨텍스트의 특징이 뭐가있나요?

<details>
   <summary> 답안 </summary>
<br />

- 영속성 컨텍스트의 특징은 `1차 캐시`, `동일성 보장`, `트랜잭션을 지원하는 쓰기 지연`, `변경 감지`, `지연 로딩` 등이 있습니다.
   - 1차 캐시는 Map<Key, Value> 형태로 저장됩니다. 엔티티가 존재할 경우 해당 엔티티를 반환하고, 엔티티가 없으면 데이터베이스에서 조회 후 1차 캐시에 저장 및 반환합니다.
   - 동일성을 보장은 하나의 트랜잭션에서 같은 키값으로 영속성 컨텍스트에 저장된 엔티티 조회 시 같은 엔티티 조회를 보장합니다 (1차 캐시에 저장된 엔티티를 조회하기 때문에 가능).
   - 영속성 컨텍스트에는 쓰기 지연 SQL 저장소가 존재하여 SQL을 쌓아두고 트랜잭션을 커밋하는 시점에 저장소에 저장해놨던 SQL문들이 flush되면서 데이터베이스에 한번에 반영됩니다. 모아서 보내기 때문에 성능에서 이점을 볼 수 있습니다.
   - 변경감지는 엔티티를 조회하는 시점과 커밋하는 시점에 데이터 변경 내용을 감지하면 커밋 시점에 자동으로 데이터베이스에 반영해줍니다. 
   - 지연로딩은 JPA가 하나의 Entity를 조회할 때 연관 관계에 있는 객체들을 전부 가져오지 않고 필요한 시점에 연관된 데이터를 불러옵니다.
  </details>
<br>

### 📌 JPA의 N+1 문제에 대해 설명해주세요.

<details>
   <summary> 답안 </summary>
<br />

- N+1 문제란 1번의 쿼리가 발생할 때, 의도치 않은 N번의 쿼리가 추가적으로 발생하는 것을 의미합니다.
  N+1 문제는 두 엔티티의 연관관계를 즉시로딩이나, 지연로딩으로 설정한 두 경우 모두 발생할 수 있습니다. <br>
  N+1 문제를 해결하는 방법은 fetch join 혹은 Entity Graph 이용하여 해결할 수 있습니다.
  
   <details>
      <summary> <strong> fetch join은 무엇이고 Entity Graph는 무엇인가요? </strong> </summary>
   <br />

   - `fetch join`은 어떤 Entity를 영속화 시킬 때 연관된 entity들도 함께 영속화 시키는 방법이며,
     `Entity Graph`는 spring data jpa에서 fetch join을 간단하게 사용하기 위해 제공하는 애노테이션 입니다.

  </details>
<br>
  </details>
<br>

### 📌 @Transactional의 동작 원리

<details>
   <summary> 답안 </summary>
<br />
   
- Transactional 애노테이션은 Spring AOP 방식으로 동작합니다. Transactional 애노테이션이 붙은 메서드의 클래스를 프록시 클래스로 상속받아 타켓 메서드를 호출하며,
  타겟 메서드 호출 전 후로 트랜잭션 관련 처리를 하는 방식으로 동작합니다. 
  </details>
<br>
