**Mybatis 동적 SQL - trim, where, set**

\<select id="findActiveBlogLike" resultType="Blog">

SELECT * FROM BLOG WHERE

\<if test="state != null">

  state = #{state}

\</if>

\<if test = "title != null">

  AND title like #{title}

\</if>

\<if test="author ! = null and authoer.name != null">

  AND author_name like #{author.name}

\</if>

\</select>



위 문번에서 if 조건에 해당 될 경우에는 쿼리문이 만들어진다. 

위와 유사한 경우에서 update를 하는 쿼리가 있다고 가정하자. 

**1. 맨 끝에 있는 콤마(,)를 제거하는 경우**

\<update id="updateAuthorIfNecessary" parameterType="domain.blog.Author">

UPDATE AUTHOR

\<trim prefix="SET" suffixOverrides=",">

  \<if test="username != null">username=#{username},\</if>

  \<if test="password != null">password=#{password},\</if>

  \<if test="email != null">email = #{email},\</if>

  \<if test="bio !=null">bio=#{bio},\</if>

\</trim>

WHERE id=#{id}

\</update>

이럴경우 쿼리가 생성 될 경우 마지막에 콤마(,)가 항상 붙게 된다.

이럴 경우 trim 태그를 이용하여서 suffixOverrrides로 지정된 콤마를 제거하도록 한다. 

**2. 맨 앞에 있는 연산자를(AND 또는 OR) 제거하는 경우**

\<select id="selectInfo" parameterType="domain.blog.Author" resultType="authorResultMap">

SELECT * FROM AUTHOR

  \<trim prefix="WHERE" prefixOverrides = "AND | OR">

  \<if test="username != null"> AND username=#{username}\</if>

  \<if test="password != null"> OR password =#{password}\</if>

  \<if test = "email != null"> AND email =#{email} \</if>

  \</trim>

\</select>

위와 같이 조건에 따라서 AND, OR이 앞에 남는 잘못된 쿼리가 될 수 있는데 이를 \<trim> 태그로써 제거할 수 있다. 

 

reference

http://www.mybatis.org/mybatis-3/ko/dynamic-sql.html

http://marobiana.tistory.com/14

