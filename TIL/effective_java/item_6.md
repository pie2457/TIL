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
