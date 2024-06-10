## Item.2 "생성자에 매개변수가 많다면 빌더를 고려하라."
정적 팩터리 메서드와 생성자에 선택적 매개변수가 많을 때 고려할 수 있는 방안을 살펴보자.

### 대안1. 점층적 생성자 패턴 또는 생성자 체이닝
```java
public class NutritionFacts {
  private final int servingSize;    // (ml, 1회 제공량)        필수
  private final int servings;       // (회, 총 n회 제공량)      필수
  private final int calories;       // (1회 제공량당)          선택
  private final int fat;            // (g/1회 제공량당)        선택
  private final int sodium;         // (mg/1회 제공량당)       선택
  private final int carbohydrate;   // (g/1회 제공량)         선택

  public NutritionFacts(int servingSize, int servings, int calories, int fat, int sodium, int carbohydrate) {
    this.servingSize = servingSize; 
    this.servings = servings;
    this.calories = calories;
    this.fat = fat;
    this.sodium = sodium;
    this.carbohydrate = carbohydrate;
  }
}
```
먼저 점층적 생성자 패턴 또는 생성자 체이닝을 알아보기 위해 위와 같은 예제를 이용한다. <br>
위 예제를 보면 필수적인 필드와 선택적인 필드가 존재하게 되는데, 필수로 있어야 하는 필드들 같은 경우 생성자의 파라미터로 받는게 필수적인 값을 받도록 강제할 수 있기 때문에
생성자에 넘겨주는 것이 좋다. 
```java
public class NutritionFacts {
  private final int servingSize;    // (ml, 1회 제공량)        필수
  private final int servings;       // (회, 총 n회 제공량)      필수
  private final int calories;       // (1회 제공량당)          선택
  private final int fat;            // (g/1회 제공량당)        선택
  private final int sodium;         // (mg/1회 제공량당)       선택
  private final int carbohydrate;   // (g/1회 제공량)         선택

  public NutritionFacts(int servingSize, int servings) {
    this.servingSize = servingSize;
    this.servings = servings;
    this.calories = 0;
    this.fat = 0;
    this.sodium = 0;
    this.carbohydrate = 0;
  }

  public NutritionFacts(int servingSize, int servings, int calories) {
    this.servingSize = servingSize;
    this.servings = servings;
    this.calories = calories;
    this.fat = 0;
    this.sodium = 0;
    this.carbohydrate = 0;
  }
  // . . . 생략
}
```
하지만 위와 같이 Optional한 필드들의 생성자까지 전부 다 만들기엔 코드가 지저분해지고 중복이 심해진다. <br>
이런 코드를 그나마 줄이려고 사용하는 방식이 생성자 체이닝 즉, 점층적 생성자 패턴이다. 
```java
  public NutritionFacts(int servingSize, int servings) {
    this(servingSize, servings, 0, 0, 0, 0);
  }

  public NutritionFacts(int servingSize, int servings, int calories) {
    this(servingSize, servings, calories, 0, 0, 0);
  }

  public NutritionFacts(int servingSize, int servings, int calories, int fat) {
    this(servingSize, servings, calories, fat, 0, 0);
  }

  public NutritionFacts(int servingSize, int servings, int calories, int fat, int sodium) {
    this(servingSize, servings, calories, fat, sodium, 0);
  }

// . . . 생략
}
```
생성자 체이닝이란 위와 같이 매개변수가 적은쪽에서 매개변수가 많은쪽의 생성자를 this를 이용하여 호출하는 방식이다. <br>
하지만 생성자 체이닝 방식은 매개변수가 많아지면 인스턴스를 생성할 때 마다 타입이 같은 매개변수를 혼동하여 잘못된 값을 전달할 수 도 있고, 
코드를 읽을 때 각 값의 의미가 무엇인지 헷갈리게 된다.

### 대안2. 자바 빈즈 패턴
자바 빈즈는 자바 표준 스펙 중 하나이며, 매개변수가 없는 생성자로 객체를 만든 후, setter 메서드들을 호출하여 원하는 매개변수의 값을 설정하는 방식이다.
```java
public class NutritionFactsWithJavaBeansPattern {
  private int servingSize = -1; // 필수. 기본 값 없음
  private int servings = -1;    // 필수. 기본 값 없음
  private int calories;
  private int fat;
  private int sodium;
  private int carbohydrate;

  public void setServingSize(int servingSize) {
      this.servingSize = servingSize;
  }

  public void setServings(int servings) {
      this.servings = servings;
  }

  public void setCalories(int calories) {
      this.calories = calories;
  }

  public void setFat(int fat) {
      this.fat = fat;
  }

  public void setSodium(int sodium) {
      this.sodium = sodium;
  }

  public void setCarbohydrate(int carbohydrate) {
      this.carbohydrate = carbohydrate;
  }
}
```
자바 빈즈 패턴은 매개변수가 많아지더라도 값을 헷갈리지 않고 인스턴스를 만들어줄 수 있다. 하지만 객체 하나를 만드려면 여러 개의 setter 메서드를 호출해야 하고,
객체가 완전히 완성되기 전까지는 일관성이 깨지게된다. 또한 setter 메서드 때문에 클래스를 불변으로 만들 수 없다.
