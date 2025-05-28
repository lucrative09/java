#  프로토타입

## 프로토타입 정의
- 기존 인스턴스를 복제하여 새로운 인스턴스를 만드는 방법

복제 기능을 갖추고 있는 기존 인스턴스를 프로토타입으로 사용해 새 인스턴스를 만들 수 있다.


## 프로토타입 예시
```java
GithubRepository repository = new GithubRepository();
repository.setUser("Kimmoonki");
repository.setName("live-study");
```
GithubRepository 객체를 생성하고, 사용자와 이름을 설정

```java
GithubIssue githubIssue = new GithubIssue(repository);
githubIssue.setId(1);
githubIssue.setTitle("1주차 과제: JVM은 무엇이며 자바 코드는 어떻게 실행하는 것인가.");
```
GithubIssue 객체를 생성하고, 해당 이슈의 ID와 제목을 설정

```java
GithubIssue clone = (GithubIssue) githubIssue.clone();
System.out.println(clone.getUrl());
```
클론을 생성

```java
repository.setUser("Keesun");
```
원본 repository의 사용자 이름을 변경을 하였지만 이 변경은 clone 객체에 영향을 미치지 않음


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
