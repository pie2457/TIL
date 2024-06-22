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
### 권장하는 방법 : 빌더 패턴
점층적 생성자 패턴의 안정성과 자바 빈즈 패턴의 가독성을 겸비한 빌더 패턴을 살펴보자. 클라이언트는 필요한 객체를 직접 만드는 대신, 필수 매개변수만으로 생성자를 호출하여
빌더 객체를 얻는다. 그런 다음 빌더 객체가 제공하는 일종의 setter 메서드들로 원하는 선택 매개변수를 설정한다. 마지막으로 매개변수가 없는 build() 메서드를 호출하여
필요한 객체를 얻게 된다.
```java
public class NutritionFactsWithBuilderPatten {
  private final int servingSize;
  private final int servings;
  private final int calories;
  private final int fat;
  private final int sodium;
  private final int carbohydrate;

  private NutritionFactsWithBuilderPattern(Builder builder) {
    servingSize = builder.servingSize;
    servings = builder.servings;
    calories = builder.calories;
    fat = builder.fat;
    sodium = builder.sodium;
    carbohydrate = builder.carbohydrate;
  }
	
  public static class Builder {
    private final int servingSize;
    private final int servings;
    private int calories;
    private int fat;
    private int sodium;
    private int carbohydrate;
		
    public Builder(int servingSize, int serving) {
      this.servingSize = servingSize;
      this.serving = serving;
    }
		
    public Builder calories(int val) {
      calories = val;
      return this;
    }
		
    public Builder fat(int val) {
      fat = val;
      return this;
    }

    public Builder sodium(int val) {
      sodium = val;
      return this;
    }

    public Builder carbohydrate(int val) {
      carbohydrate = val;
      return this;
    }

    public NutritionFactsWithBuilderPattern build() {
      return new NutritionFactsWithBuilderPattern(this);
    }
  }
}
```
Builder 클래스 내의 생성자는 필수 매개변수만을 입력받고, 나머지 선택 매개변수는 일종의 setter 메서드로 채워 넣는다. 그리고 마지막으로 build() 메서드를 통해
완성된 `NutritionFactsWithBuilderPattern` 객체를 생성한다. `NutritionFactsWithBuilderPattern` 클래스는 불변이며, 빌더의 setter 메서드들은
빌더 자신을 반환하기 때문에 `.`을 이용하여 연쇄적으로 호출할 수 있다. 이런 방식을 **플루언트 혹은 API 메서드 체이닝**이라고 한다.
```java
NutritionFactsWithBuilderPattern nutritionFacts =
  new NutritionFactsWithBuilderPattern.Builder(240, 8)
      .calories(100)
      .sodium(35)
      .build();
```
클라이언트 입장에서는 빌더 패턴을 통해 코드를 쓰기 쉽고, 읽기도 쉽게 작성할 수 있다. 

### 계층적으로 설계된 클래스와 잘 어울리는 빌더 패턴
```java
public abstract class Pizza {
  public enum Topping {
    HAM, MUSHROOM, ONION, PEPPER, SAUSAGE
  }
	
  final Set<Topping> toppings;
	
  Pizza(Builder<?> builder) {
    toppings = builder.toppings.clone();
  }
	
  abstract static class Builder<T extends Builder<T>> {
    private EnumSet<Topping> toppings = EnumSet.noneOf(Topping.class);
		
    public T addTopping(Topping topping) {
      topping.add(topping);
      return self();
   }
		
  abstract Pizza build();
		
  protected abstract T self();
 }
}
```
Pizza.Builder 클래스는 재귀적 타입 한정을 이용하는 제네릭 타입이며, 추상 메서드인 self()를 더해 하위 클래스에서는 형 변환을 하지 않고도 메서드 체이닝을 지원한다.
하위 클래스에서는 이 추상 메서드의 반환 값을 자기 자신을 주면 된다. <br>
