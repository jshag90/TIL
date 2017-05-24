**MyBatis 동적쿼리 - choose, when, otherwise**

자바에서 switch 구문과 유사하다.

\<select id="findActiveBlogLike" resultType="Blog">

SELECT * FROM BLOG WHERE state = 'ACTIVE'

\<choose>

   \<when test="title != null">

​	AND title like #{title}

  \</when>

  \<when test="author != null  and author.name != null">

​	AND author_name like #{author.name}

 \</when>

 \<otherwise>

​	AND featured = 1

\</otherwise>

\</choose>

\</select>

reference

http://www.mybatis.org/mybatis-3/ko/dynamic-sql.html