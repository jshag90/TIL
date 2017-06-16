**SimpleUrlAuthenticationFailureHandler**

`AuthenticationFailureHandler` 은  `onAuthenticationFailure` 메서드를 호출을 통해서 `defaultFailureUrl` 속성으로 설정한 값으로 리다이렉트 시켜주는 것을 실행한다.

만약 적절한 속성이 설정이 안되어 있다면 클라이언트에게 `AuthenticationException` 과 함께 401응답을 해준다. 



**SimpleUrlLogoutSuccessHandler**

기본 로직에 AbstractAuthenticationTargetUrlRequestHandler로 로그아웃을 위임해준다. 



**SavedRequestAwareAuthenticationSuccessHandler**

ExceptionTranslationFilter에 의해 세션에 저장되었을 수있는 DefaultSavedRequest를 사용할 수있는 인증 성공 전략. 이러한 요청이 인터셉트되어 인증을 요구하면 인증 프로세스가 시작되기 전에 원본 대상을 기록하고 동일한 URL로 리디렉션이 발생하면 요청을 재구성 할 수 있도록 요청 데이터가 저장됩니다. 이 클래스는 적절한 경우 원래 URL로 리디렉션을 수행합니다.(구글 번역)



**org.springframework.security.core.userdetails.User**의 **User** 클래스

사용자 정보를 저장해 두는 클래스



**BadCredentilasException**

사용자 정보가 무효가 되어서 인증 요청이 거부되는 것을 던진다. 이러한 예외처리를 던지게 되기 위해서, 이것은 계정이 잠기거나 disabled 되는 것은 아니다. 



**FilterInvocationSecurityMetadataSource**

URL/METHOD를 이용한 접근권한이 어떻게 되는지 확인합니다. 우리가 Spring Security에 각각의 URL별 권한을 hard coding으로 넣어주는 경우에는, 이 MetadataSource가 hard coding된 것과 같은 역할을 하게 된다.



**FactoryBean**

인스턴스를 생성하는 방법 중에 하나이다. 

Spring으로 DI 할 수 없는 Class의 beand르 Spring에서 관리가 가능하게 하도록 Wrapper해주는 기능이다. 예를 들어 POJO형태가 아닌 singleton패턴이 구현된 Class 혹은 서드파티에서 제공하는 Class, JNDI lookup을 통해서 리턴 받아야 하는 객체, 혹은 생성과 기본 세팅과정이 복잡한 객체들은 Spring에서 직접 생성관리 하는게 불가능할 경우에 사용한다. 

Spring의 일반적인 DI패턴으로 생성하기 힘든 객체를 Spring에서 생성/관리하고자 할 때 Wrapping 기능 제공(타 객체에 의존성 주입 등)한다.  

Spring을 대신하여 사용자가 getObject를 구현하고 적절히 Instance를 생성하여 리턴하여 준다. 

reference

http://javaslave.tistory.com/53











