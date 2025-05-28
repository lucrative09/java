#  프로토타입

## 프로토타입 정의
- 기존 인스턴스를 복제하여 새로운 인스턴스를 만드는 방법

복제 기능을 갖추고 있는 기존 인스턴스를 프로토타입으로 사용해 새 인스턴스를 만들 수 있다.


```java
System.out.println(clone != githubIssue);
System.out.println(clone.equals(githubIssue));
System.out.println(clone.getClass() == githubIssue.getClass());
System.out.println(clone.getRepository() == githubIssue.getRepository());
```
clone과 githubIssue는 서로 다른 객체이므로 clone != githubIssue는 true입니다.
clone.equals(githubIssue)는 두 객체가 동일한 값을 가지지 않기 때문에 false입니다.
두 객체는 같은 클래스이므로 clone.getClass() == githubIssue.getClass()는 true입니다.
clone.getRepository() == githubIssue.getRepository()는 false일 수 있습니다. 
클론된 객체는 원본 레포지토리와 별도의 인스턴스를 가질 수 있습니다.

## 장점
• 복잡한 객체를 만드는 과정을 숨길 수 있다.
• 기존 객체를 복제하는 과정이 새 인스턴스를 만드는 것보다 비용(시간 또는 메모리)적인
면에서 효율적일 수도 있다.
• 추상적인 타입을 리턴할 수 있다.

## 단점
• 복제한 객체를 만드는 과정 자체가 복잡할 수 있다. (특히, 순환 참조가 있는 경우)


• 자바 Object 클래스의 clone 메소드와 Cloneable 인터페이스
• shallow copy와 deep copy
• ModelMapper
