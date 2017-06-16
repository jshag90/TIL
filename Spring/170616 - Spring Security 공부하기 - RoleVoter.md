Spring Security - RoleVoter

Spring에서 Security를 적용하면 인증받을 사용자의 아이디, 비밀번호를 입력한 뒤에 해당 사용자에게 권한(ROLE_USER)을 부여한다. 별도의 튜닝을 하지 않으면 사용자의 권한은 'ROLE_'란 문자열로 시작해야 한다. 

Spring Security에서는 부여된 권한을 검사하는 RoleVoter라는 클래스를 가지고 있다. 

ex)  security-context.xml 파일 설정

\<beans:bean id="roleVoter" class="org.springframework.security.access.vote.RoleVoter">

​	\<beans:property name="rolePrefix" value="" />
\</beans:bean>

