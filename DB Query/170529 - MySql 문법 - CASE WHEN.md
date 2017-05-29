MySql 문법 - CASE WHEN

CASE

WHEN 조건

THEN '대체값'

WHEN 조건

THEN '대체값'

ELSE  'WHEN 저건에 해당안될 경우의 기본값'

END



example

SELECT mmember_name,

​	      CASE

​		   WHEN memeber_name = '이순신'

​		    THEN '중복 1'

​		    WHEN member_name = '홍길동'

 		     THEN '중복 2'

​		     ELSE '중복아님'

​             END AS result

FROM member

* member 테이블의 member_name의 결과값이 '이순신'이면 '중복1',
* '홍길동'이면 중복2
* 그외에는 '중복아님' 출력



reference

http://hellogk.tistory.com/21