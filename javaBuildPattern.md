#  자바 빌드패턴

## 빌드패턴의 필요성

객체 생성 시 일관된 프로세스 부족
생성자 매개변수의 증가로 인한 복잡성
불안전한 상태로 객체가 생성될 위험

## 빌더 패턴 개요

동일한 프로세스를 통해 다양한 객체 생성
인터페이스 정의 및 구현체 활용

## 빌더 인터페이스
ToruPlanBuilder 인터페이스 생성

```java
ToruPlanBuilder title(String title);
ToruPlanBuilder nightsAndDays(int nights, int days);
TourPlan getPlan();
```

## 구현체 예시
DefaultTourBuilder 클래스에서 ToruPlanBuilder 구현
getPlan() 메서드에서 최종 객체 생성:
```java
return new TourPlan(title, nights, days, startDate, whereToStay, addPlan);
```

## 클라이언트 사용 예
```java
TourPlanBuilder builder = new DefaultTourBuilder();
TourPlan shortPlan = builder.title("크루즈 여행")
                            .nightsAndDays(2, 3)
                            .whereToStay("리조트")
                            .getPlan();
```

## Director 패턴
```java
TourDirector director = new TourDirector(new DefaultTourBuilder());
TourPlan tourPlan1 = director.shortTrip();
TourPlan tourPlan2 = director.longTrip();
```

## 빌더패턴 상세 설명
1. Product 클래스
- 역할: TourPlan 클래스는 투어 계획을 나타내는 데이터 구조입니다. 이 클래스는 투어의 여러 속성을 담고 있습니다.
- 속성
title: 투어 제목
nights: 숙박 일수
days: 여행 일수
startDate: 시작 날짜
whereToStay: 숙소 정보
- 생성자는 모든 속성을 초기화하는 역할을 합니다. 객체가 생성될 때 모든 필수 정보를 받아서 설정합니다.
```java
public class TourPlan {
    private final String title;
    private final int nights;
    private final int days;
    private final String startDate;
    private final String whereToStay;

    public TourPlan(String title, int nights, int days, String startDate, String whereToStay) {
        this.title = title;
        this.nights = nights;
        this.days = days;
        this.startDate = startDate;
        this.whereToStay = whereToStay;
    }

    // Getter 메서드
    public String getTitle() { return title; }
    public int getNights() { return nights; }
    public int getDays() { return days; }
    public String getStartDate() { return startDate; }
    public String getWhereToStay() { return whereToStay; }
}
```
2. Builder 인터페이스: TourPlanBuilder
- 역할: TourPlanBuilder 인터페이스는 투어 계획 객체를 생성하기 위한 메서드를 정의합니다.

title(String title): 투어 제목을 설정하는 메서드

nightsAndDays(int nights, int days): 숙박 일수와 여행 일수를 설정하는 메서드

startDate(String startDate): 시작 날짜를 설정하는 메서드

whereToStay(String where): 숙소 정보를 설정하는 메서드

getPlan(): 최종적으로 구성된 TourPlan 객체를 반환하는 메서드

- 각 메서드는 TourPlanBuilder를 반환하여 메서드 체이닝을 가능하게 합니다. 이를 통해 여러 설정을 연속적으로 할 수 있습니다.

```java
public interface TourPlanBuilder {
    TourPlanBuilder title(String title);
    TourPlanBuilder nightsAndDays(int nights, int days);
    TourPlanBuilder startDate(String startDate);
    TourPlanBuilder whereToStay(String where);
    TourPlan getPlan();
}
```
3. ConcreteBuilder 클래스: DefaultTourBuilder
- 역할: DefaultTourBuilder 클래스는 TourPlanBuilder 인터페이스를 구현하여 실제 객체 생성 로직을 담고 있습니다.
- 속성: title, nights, days, startDate, whereToStay를 저장하는 내부 상태 변수
- 각 메서드는 해당 속성을 설정하고, this를 반환하여 메서드 체이닝을 지원합니다.
- getPlan() 메서드는 모든 속성을 사용하여 새로운 TourPlan 객체를 생성하고 반환합니다.
```java
public class DefaultTourBuilder implements TourPlanBuilder {
    private String title;
    private int nights;
    private int days;
    private String startDate;
    private String whereToStay;

    @Override
    public TourPlanBuilder title(String title) {
        this.title = title;
        return this;
    }

    @Override
    public TourPlanBuilder nightsAndDays(int nights, int days) {
        this.nights = nights;
        this.days = days;
        return this;
    }

    @Override
    public TourPlanBuilder startDate(String startDate) {
        this.startDate = startDate;
        return this;
    }

    @Override
    public TourPlanBuilder whereToStay(String where) {
        this.whereToStay = where;
        return this;
    }

    @Override
    public TourPlan getPlan() {
        return new TourPlan(title, nights, days, startDate, whereToStay);
    }
}
```
4. 클라이언트 코드: Main
- 역할: Main 클래스는 DefaultTourBuilder를 사용하여 실제 투어 계획을 생성하는 클라이언트 코드입니다.
- 빌더 인스턴스를 생성하고, 체이닝을 통해 필요한 속성을 설정합니다.
- 최종적으로 getPlan() 메서드를 호출하여 TourPlan 객체를 생성합니다.
```java
public class Main {
    public static void main(String[] args) {
        TourPlanBuilder builder = new DefaultTourBuilder();
        TourPlan plan = builder.title("크루즈 여행")
                               .nightsAndDays(2, 3)
                               .startDate("2023-07-01")
                               .whereToStay("리조트")
                               .getPlan();

        System.out.println("투어 제목: " + plan.getTitle());
        System.out.println("숙박 일수: " + plan.getNights());
        System.out.println("여행 일수: " + plan.getDays());
        System.out.println("시작 날짜: " + plan.getStartDate());
        System.out.println("숙소: " + plan.getWhereToStay());
    }
}
```
# 요약 정리
- Product (TourPlan): 투어 정보를 담는 클래스.
- Builder 인터페이스 (TourPlanBuilder): 객체 생성 메서드를 정의.
- ConcreteBuilder (DefaultTourBuilder): 인터페이스를 구현하여 실제 객체 생성.
- 클라이언트 (Main): 빌더를 사용하여 객체를 구성하고 생성.

이러한 구조로 빌더 패턴을 사용하면, 복잡한 객체를 효율적으로 관리하고 생성할 수 있습니다. 

각 구성 요소가 명확히 역할을 나누어 코드의 가독성과 유지보수성을 향상시킵니다.

## 결론
빌더 패턴을 통해 코드 가독성 및 재사용성 향상 및
객체 생성을 일관된 프로세스로 간소화
