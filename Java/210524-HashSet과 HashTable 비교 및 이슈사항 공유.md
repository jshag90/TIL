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

- HashTable thread safe하지만 속도 측면에서는 HashMap보다 느림
- HashMap은 순회를 위해 Fail-Fast Iterator 반환, HashTable은 Enumeration를 반환
- 둘다 기본적인 개념과 사용하는 방법은 동일



[해시셋, hash 개념 정리]  https://st-lab.tistory.com/240

[해시셋, 해시맵 비교] https://postitforhooney.tistory.com/entry/JavaHashSet%EA%B3%BC-HashMap

[해시맵] https://techmastertutorial.in/java-collection-internal-hashmap.html



**최근 독스토리 파일 파일보호 이벤트 로그 CSV파일 내보내기 기능 관련**

1) 인덱스란?

- 책의 찾아보기를 통해 알아낼 수 있는 페이지 번호 데이터 파일에 저장된 레코드 주소와 비유
- DBMS의 인덱스도 마찬가지로 컬럼의 값을 주어진 순서로 미리 정렬
- DBMS의 인덱스는 데이터의 저장(insert, update, delete) 성능을 희생하고 대신 데이터의 읽기 속도를 높이는 기능
- B-Tree 알고리즘, Hash 인덱스 알고리즘, Fractal-Tree 알고리즘

2) 독스토리 최근 활용

- 인덱싱 추가 쿼리

```mysql
ALTER TABLE `tbl_wl_log` ADD INDEX `create_tm` (`create_tm`);
ALTER TABLE `tbl_wl_log` ADD INDEX `com_name` (`com_name`);
ALTER TABLE `tbl_wl_log` ADD INDEX `process_name` (`process_name`);
ALTER TABLE `tbl_wl_log` ADD INDEX `com_name_process_name` (`com_name`, `process_name`);
```

- 데이터 조회 쿼리

```mysql
SELECT ACT.* , 
	COUNT(ACT.process_name) PROC_CNT, //프로세스 
    (
        SELECT 
          create_tm 
        from tbl_wl_log 
        WHERE process_name = ACT.process_name 
        AND com_name = ACT.com_name 
        AND create_tm BETWEEN DATE_ADD(NOW(),INTERVAL - 1 DAY ) AND NOW()
        ORDER BY create_tm 
        DESC LIMIT 1 
    ) AS CREATE_TIME //해당 프로세스 최근 차단 시간
	FROM (           
	      	SELECT 
	      	   com_name
               ,process_name	
		    FROM tbl_wl_log 
			WHERE create_tm 
			BETWEEN DATE_ADD(NOW(),INTERVAL - 1 DAY ) AND NOW()
			ORDER BY create_tm DESC
          ) AS ACT
   GROUP BY ACT.com_name, ACT.process_name //com_name별, 프로제스 별 count 정보를 위해서 그룹핑
   ORDER BY com_name DESC, PROC_CNT DESC // 기간이 늘어 남에 따라 이슈가 되서 추후에 제거됨 
```

- 실행 결과

![image-20210524094313659](C:\Users\wltjs\AppData\Roaming\Typora\typora-user-images\image-20210524094313659.png)

- Index 적용 전

![image-20210524095200802](C:\Users\wltjs\AppData\Roaming\Typora\typora-user-images\image-20210524095200802.png)

- Index 적용 후

![image-20210524095253945](C:\Users\wltjs\AppData\Roaming\Typora\typora-user-images\image-20210524095253945.png)

- order by 뺄 경우

  ![image-20210524095334314](C:\Users\wltjs\AppData\Roaming\Typora\typora-user-images\image-20210524095334314.png)