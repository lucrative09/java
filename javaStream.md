#  자바 스트림

## 스트림 정의
- 다양한 데이터 소스를 표준화된 방법으로 다루기 위한 것!

JDK1.8 이후 등장한 개념으로 컬렉션(List, set, map) 배열을 stream 생성,
즉 위 내용을 Stream으로 만들어서 중간연산 최종연산을 수행하는것을 말한다.

중간연산은 n번, 최종연산은 한번만 진행한다.

## 스트림으로 변환 생성

```java
Stream<T> Collection.stream();

Stream<Integer> intStream = list.stream();                          // 컬렉션
Stream<String> strStream = Stream.of(new String[]{"a", "b", "c"});  // 배열
Stream<Double> randomStream = Stream.generate(Math::random);        // 람다식
```

데이터소스 -> Stream -> 중간연산(0 ~ n번) -> 최종연산(0 ~ 1번)

cheonggyecheon stream 청계천?
데이터의 연속적인 흐름을 Stream이라고 합니다.

## 연산의 종류
```java
/* 중간연산 */
stream.filter();    // 걸러내기
stream.distinct();  // 중복제거
stream.sort();      // 정렬
stream.limit(5);    // 스트림 자르기

/* 최종연산 */
stream.count();
stream.forEach();
collect();
```

## 스트림의 특징
- 스트림은 데이터 소스로부터 데이터를 읽기만 할 뿐 변경하지 않는다.

```java
List<Integer> list = Arrays.asList(3,1,5,4,2);
List<Integer> sortedList = list.stream().sorted().collect(Collectors.toList());
System.out.println(list);
System.out.println(sortedList);

/* 결과값
[3, 1, 5, 4, 2]
[1, 2, 3, 4, 5]
*/
```

위의 소스를 보면 list 원본은 변경되지않고 읽는 기능만 수행한다.

- 스트림은 일회용이다. (필요하면 다시 스트림을 생성해야한다.)

```java
List<Integer> list_01 = Arrays.asList(1,2,3,4,5);
Stream<Integer> stream01 = list_01.stream(); // 최종연산

stream01.forEach(System.out::print);

// stream01 = list_01.parallelStream();// 생성을 해야 사용 가능하다.

stream01.forEach(System.out::print); // 이대로 진행 시 스트림 이미 닫힘
```
