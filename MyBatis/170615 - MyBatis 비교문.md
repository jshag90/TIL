MyBatis 비교문 사용

MyBatis 매핑 구문에서 비교문 문법인 <, >을 사용할 경우에 에러가 발생함

이에 따라서 2가지 방법을 통해서 문제를 해결 가능함

- CDATA로 감싸주는 방법

ex) 

\<select id="selectExample">

<![CDATA[

SELECT * FROM example_data where no<10

]]

\</select>

- <를 &lt로 치환, >는 \&\gt;로 치환

ex)

\<select id ="selectExample">

SELECT * FROM example_data where no &lt 10

\</select>