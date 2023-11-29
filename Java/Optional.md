# Optional

### 옵셔널 (Optional)

코드를 작성하다 보면 NullPointerException 예외가 생기는 경우가 있다. 따라서 이에 따른 적절한 처리를 고려해서 코드를 작성해야 하는데 이는 어렵진 않지만 번거롭고 코드의 가독성을 떨어트릴 수 있다. 그래서 이러한 일을 간단하게 처리할 수 있도록 자바 8부터 Optional 클래스를 지원하고있다.

#

### 옵셔널을 사용하지 않는 경우

```Java
class Person {
  String name;
  String homePhoneNum; // 집전화번호가 없는 사람이 있을 수 있다.
}



 public void showPersonInfo(Person p) {
  String homePhoneNum;
  ...
  if(p.homePhoneNum != null) {
      homePhoneNum = p.getHomePhoneNum();
  }
  else
    homePhoneNum = "집 전화번호 정보가 없습니다.";
  System.out.println(homePhoneNum);
 }
  ...

```

if 문으로 null 체크를 해서 NullPointerException 예외를 처리해야 한다.

### 옵셔널을 사용하는 경우

```Java
class Person {
  String name;
  String homePhoneNum; // 집 전화번호가 없는 사람이 있을 수 있다.
}



 public void showPersonInfo(Person person) {
  String homePhoneNum = Optional.ofNullable(person).map(Person::getHomePhoneNum).orElse("집 전화번호 정보가 없습니다.");

  System.out.println(homePhoneNum);
 }
  ...

```

옵셔널을 사용하면 if else 문을 줄여 코드 가독성을 늘릴 수 있다.

#

### Optional 객체 생성

- Optional.of

  ```Java
  Optional<String> opt = Optional.of(new String("example")); //of는 null을 허용하지 않는다.
  ```

- Optional.ofNullable

  ```Java
  Optional<String> opt = Optional.ofNullable(new String("example")); //ofNullable은 null을 허용한다.
  ```

- Optional.empty
  ```Java
  Optional<String> opt = Optional.empty(); //비어있는 옵셔널 객체를 생성한다.
  ```

### Optional 메소드

- Optional.map

  ```Java
  Optional.ofNullable(person).map(Person::getHomePhoneNum)
  ```

  Optional 객체가 값을 갖고 있으면, map 메서드로 넘겨진 함수를 통해 값의 형태를 변경한다. Optional 객체가 비어있는 경우 연산을 수행하지 않는다.

- Optional.isPresent

  ```Java
  Optional.ofNullable("example").isPresent();
  ```

  Optional 객체가 존재하면 true 비어있으면 false를 반환한다.

- Optional.ifPresent

  ```Java
  Optional.ofNullable(example).ifPresent(System.out::println);
  ```

  Optional 객체가 존재하면 ifPresent에 인자로 전달된 내용을 수행한다. 비어있으면 수행하지 않는다.

- Optional.orElse

  ```Java
  String homePhoneNum = Optional.ofNullable(person).map(Person::getHomePhoneNum).orElse("집 전화번호 정보가 없습니다.");
  ```

  Optional 객체가 비어있으면 대신해서 반환할 내용을 지정한다.
