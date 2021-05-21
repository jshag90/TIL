**1) Hash란**

- 임의의 길이를 갖는 데이터를 고정된 길이의 데이터로 변환(매핑) 하는 것

- 동일한 메시지(값)에 대해서 동일한 다이제스트

<img src="https://blog.kakaocdn.net/dn/bwCA7Y/btq2uWgFDmx/HYtcRDsCtm9vkARKCInPkk/img.png" alt="img" style="zoom:25%;" />

- 다이제스트의 값을 배열의 위치(index)로 활용한 것임
  (feat. db의 primary key와 같은 개념이라고 생각하면 될꺼 같습니다.)

<img src="https://blog.kakaocdn.net/dn/zZup5/btq2oSmuZSz/0iZTUqyo0dsjP8n6tQBsi0/img.png" alt="img" style="zoom:14%;" />

**2) 해시 충돌**

- 위와같은 해시로 데이터를 접근하면 값은 다르지만 버킷의 크기에 따라서 동일한 해시가 발생하여 충돌이 생길 수 있음
- 이를 해결하기 위한 방법으로 크게 Open Addressing, Separate Chainging, 이중 해시 등 다양한 방식 존재
-  JAVA 8에서는 Separate Chaining 방식 선택

<img src="https://blog.kakaocdn.net/dn/CoiPf/btq2qyoJVrN/ERiH4UbKnKHQyF4R0HGjOk/img.png" alt="img" style="zoom:20%;" />

**3) JAVA 자료구조 구성도**

![Java 자료구조 - List, Set, Map](https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdXCHuf%2FbtqEw1TsKk5%2Fqcnv89UU6LstM7edvURqTk%2Fimg.jpg)

**4) 해시셋, Set 인터페이스**

- 순서의 의미가 없음
- 데이터를 중복해서 포함할 수 없음
- add() 메소드를 통해 데이터를 저장
- java에서 내부적으로 equals()와 hashCode() 메소드를 구현해야 하는데 이 메소드를 가지고 중복된 객체가 여부 체크함

<img src="https://blog.kakaocdn.net/dn/cOpqbM/btq2u2CiJ3W/OFwGpDkr29qnRVs7vqkMfK/img.png" alt="img" style="zoom:33%;" />

**5) 해시맵, Map 인터페이스** 

- 데이터를 Key-Value 형식으로 저장

- PUT() 메소드를 통해서 데이터를 저장

- HashCode값을 key-value를 이용해서 생성

- unique key를 이용하여 데이터에 바로 접근하기 때문에 해시셋에 비해서 빠름

  <img src="https://techmastertutorial.in/images/java/collections/HashMap_Orchestration.png" alt="HashMap.png" style="zoom:50%;" />

**6) 해시맵과 해시테이블**

- Hashtable thread safe하지만 속도 측면에서는 HashMap보다 느림
- HashMap은 순회를 위해 Fail-Fast Iterator 반환, HashTable은 Enumeration를 반환
- 둘다 기본적인 개념과 사용하는 방법은 동일



[해시셋, hash 개념 정리]  https://st-lab.tistory.com/240

[해시셋, 해시맵 비교] https://postitforhooney.tistory.com/entry/JavaHashSet%EA%B3%BC-HashMap

[해시맵] https://techmastertutorial.in/java-collection-internal-hashmap.html