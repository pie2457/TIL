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
하지만 생성자 체이닝 방식은 매개변수가 많아지면 인스턴스를 생성할 때 마다 타입이 같은 매개변수를 혼동하여 잘못된 값을 전달할 수 도 있고, 
코드를 읽을 때 각 값의 의미가 무엇인지 헷갈리게 된다.
