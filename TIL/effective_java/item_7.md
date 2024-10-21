## Item.7 "다 쓴 객체 참조를 해제하라."
자바의 가비지 컬렉터는 주기적으로 사용되지 않는 객체들을 알아서 회수해가기 때문에 프로그래머가 메모리 관리에 신경써야 하는 부분이 적다.
하지만, 가비지 컬렉터만 믿고 코드를 짜다보면 문제가 발생할 수 있다. <br>
가비지 컬렉터는 일반적으로 객체 참조가 해제되서 객체를 참조하는 곳이 없게되면 해당 객체를 수거해 간다.
하지만, 참조객체가 리스트에 저장되어 있다면 수십개의 객체를 저장해 놓은 상태에서는 특정 객체가 더 이상
리스트에서 사용되지 않고 있더라도 가비지 컬렉터는 수거해가지 않는다. 
```java
public class Stack {
  private Object[] elements;
  private int size = 0;
  private static final int DEFAULT_INITIAL_CAPACITY = 16;

  public Stack() {
    elements = new Object[DEFAULT_INITIAL_CAPACITY];
  }

  public void push(Object e) {
    ensureCapacity();
    elements[size++] = e;
  }

  public Object pop() {
    if (size == 0) {
      throw new EmptyStackException();
    }
    return elements[--size];
  }

  /**
  * 원소를 위한 공간을 적어도 하나 이상 확보한다.
  * 배열 크기를 늘려야 할 때마다 대략 두 배씩 늘린다.
  */
  private void ensureCapacity() {
    if (elements.length == size) {
      elements = Arrays.copyOf(elements, 2 * size + 1);
    }
  }
}
```
