Spring Security 공부하기

**\<http> \</http>** 태그의 엘리먼트의 속성 이해햐기

1) use-expressions : SpEL을 사용하도록 설정(true, false)

2) entry-point-ref : 내부적으로 지원하는 인증 방식이 아닌 다른 방법을 사용하고 있어서 새로운 인증 필터와 EntryPoint를 사용한다면 새로 만든 EntryPoint를 이곳에 설정

3) access-decision-manager-ref : AccessDecisionManager를 구현한 빈의 레퍼러스 참조

\<intercept-url pattern="/api/**" access="ROLE_APP" />

Spring Security가 감시해야 할 URL과 이 URL이 접근가능한 권한을 정의하는 태그

access 속성 조건

1) permitAll : 모든 접근자를 항상 승인

2) denyAll : 모든 사용자의 접근을 거부

3) anonymous : 사용자가 익명 사용자인지 확인

**\<anonymous enabled="false" />**

4) authenticated : 인증된 사용자인지 확인 

5) rememberMe : 사용자가 본인 인증했는지를 확인 

6) fullyAuthenticated : 사용자가 모든 크리덴션을 갖춘 상태에서 인증했는지 확인

access = "hasAnyRole('ROLE_USER','ROLE_ADMIN') or authenticated"

와 같이 AND, OR 연산 가능

\<http>

\<http-basic entry-point-ref="clientAuthenticationEntryPoint" />

\</http>

브라우저에서 로그인 대화상자나 사용자 로그인을 위한 특정 로그인 페이즐 보여준다.

기본 인증은 설정 위치에 상관없이 가장 우선시 된다.

\<custom-filter ref="clientCredentialsTokenEndpointFilter" after="BASIC_AUTH_FILTER" />

기존 필터를 상속하거나 Filter를 직접 구현하여 Bean으로 생성

ref="생성 할 필터 Bean" 

위치 지시자 = "위치Alias"

before는 위치 Alias보다 앞에, after는 뒤에, position은 해당 위치에 있는 필터 대체

FIRST : 맨앞, LAST : 맨뒤

*`position`을 사용하는 경우에는 `auto-config=“false”`로 해서 모든 것을 개발자가 직접 설정 해줘야 한다.

\<access-denied-handler ref="oauthAccessDeniedHandler" />

 접근 거부 상황일 경우에 사용하며 ref로 참조된 Handler로 처리 가능하도록 함



OAuth2_클래스 공부하기

class="org.springframework.security.oauth2.provider.error.OAuth2AuthenticationEntryPoint"

설명

만약 인증에 실패하고 요청자가 특별한 콘텐츠 타입 응답을 위한 요청을 한다면, 이 엔트리 포인트는 401 표준 상태를 따라서 보낸다. 일반적인 방법의 한가지로  `AuthenticationEntryPoint`로 스프링 시큐리티 설정을 더한다. 

class="org.springframework.security.oauth2.provider.error.OAuth2AccessDeniedHandler"

만약 인증에 실패하고 요청자가 특별한 콘텐츠 타입 응답을 위한 요청을 한다면, 이 엔트리 포인트는 403 표준 상태를 따라서 보낸다.일반적인 방법의 한가지로 AccessDeniedHandler로 스프링 시큐리티 설정을 더한다.

class="org.springframework.security.oauth2.provider.client.ClientCredentialsTokenEndpointFilter"

OAuth2 토큰 앤드 포인트을 위한 필터와 인증 앤드포인트이다. 보안 필터나  명세를 허가할지 말지에 대한 파라미터 요청을 사용하는 클라이언트 인증을 허락한다. 이것은 클라이언트를 위한 HTTP 기본 인증 허가와 전체의 필터 사용 하지 않는 명세로 추천된다.

class="org.springframework.security.access.vote.UnanimousBased"

모든 보터(voters)들이 기권하거나 액세스 권한을 부여하기를 요구하는 AccessDecisionManager의 구체적인 구현은 간단하다.

class="org.springframework.security.oauth2.provider.vote.ScopeVoter"

OAuth2 범위를 가리키는 접두사와 함께 ConfigAttribute.getAttribute()를 시작하여 보트(vote)취합한다. 기본 접두사 문자열은 SCOPE_이지만, 어떠한 값을 위해서 오버라이든 될 수 있다. 

또한, 정확하게 지정한 DENY_OAUTH 속성값으로 OAuth2 클라이언트를 위한 접근 거부하는 것에 사용될 수 있다. 전형적으로 여러분은 일부 범위가 아닌 모든 비공식적인 자원들의 접근을 거부하기를 원한다.

class="org.springframework.security.access.vote.RoleVoter" 

역할(role)을 나타내는 접두사로 [`ConfigAttribute.getAttribute()`](http://docs.spring.io/spring-security/site/docs/current/apidocs/org/springframework/security/access/ConfigAttribute.html#getAttribute--) 을 보트(vote) 취합한다. 기본 접두사 문자열은 ROLE_이지만, 특정 값은 오버라이드 될 수 있다. 이것은 비우도록 설정 될 수 있고, 이것은 필수적인 어떠한 속성은 보트(vote) 취합될 수 있을 것이다. 

 class="org.springframework.security.access.vote.AuthenticatedVoter"

```의 
IS_AUTHENTICATED_FULLY
```

의 `ConfigAttribute.getAttribute()` 이거나 

```
IS_AUTHENTICATED_REMEMBERED나
IS_AUTHENTICATED_ANONYMOUSLY를 제공한다.
```

The current `Authentication` will be inspected to determine if the principalhas a particular level of authentication. 

현재 `Authentication` 는 주체가 특정 수준의 인증을 가지고 있는지를 판별하기 위해 검사된다.

The "FULLY" authenticated option means the user is authenticated fully (i.e.[`AuthenticationTrustResolver.isAnonymous(Authentication)`](http://docs.spring.io/spring-security/site/docs/current/apidocs/org/springframework/security/authentication/AuthenticationTrustResolver.html#isAnonymous-org.springframework.security.core.Authentication-)is false and[`AuthenticationTrustResolver.isRememberMe(Authentication)`](http://docs.spring.io/spring-security/site/docs/current/apidocs/org/springframework/security/authentication/AuthenticationTrustResolver.html#isRememberMe-org.springframework.security.core.Authentication-)is false). 

 "FULLY" 로 인증된 옵션은 사용자가 완전히 인증 된것을 의미한다. ([`AuthenticationTrustResolver.isAnonymous(Authentication)`](http://docs.spring.io/spring-security/site/docs/current/apidocs/org/springframework/security/authentication/AuthenticationTrustResolver.html#isAnonymous-org.springframework.security.core.Authentication-))는 false이고 d[`AuthenticationTrustResolver.isRememberMe(Authentication)`](http://docs.spring.io/spring-security/site/docs/current/apidocs/org/springframework/security/authentication/AuthenticationTrustResolver.html#isRememberMe-org.springframework.security.core.Authentication-)도 false 이다. 

*보터(voter)는 관리자가 설정한 리소스에 대한 접근 권한과 사용자가 가진 authority 들(Authentication의 getAuthorities() 로 획득)을 비교하여 접근
가능 여부 (ACCESS_GRANTED, ACCESS_DENIED, ACCESS_ABSTAIN)를 결정하는 객체이다. 

*보터(voter)는 권한부여 과정에서 다음 중 하나 또는 전체를 판단한다.

1) 보호된 리소스에 대한 요청(IP 주소를 요청하는 URL) 컨텍스트

2) (존재할 경우) 사용자가 제시한 크리덴셜

3) 접근하려는 보호된 리소스

4) 시스템의 설정 매개변수와 리소스 자체 

\<authentication-manager>\</authentication-manager>

스프링 시큐리티 3부터 모든 AuthenticationProvider 엘리먼트가 \<authentication-manager> 엘리먼트 자식이 돼야 한다. 

Authentication Manager는 인증를 시도(authenticate 메서드 호출)해서 성공하면, Authentication 객체를 반환하고, 실패하면, AuthenticationException 예외를 던지는 메소드를 가지고 있다. 

\<authentication-provider/>

인증로직을 추가로 작성하기 위한 태그 `<``authentication-manager``>`와 함께 사용한다.

class="org.springframework.security.oauth2.provider.client.ClientDetailsUserDetailsService"

client정보를 받기 위한 클래스로 예상됨

class="org.springframework.security.oauth2.provider.token.InMemoryTokenStore"

인 메모리에 토큰들을 저장하는 토큰 서비스 

class="org.springframework.security.oauth2.provider.token.DefaultTokenServices"

access 토큰과 refresh 토큰 값을 위한 랜덤 UUID 값을 사용하는 토큰 서비스를 위해서 구현되었다. 

확장하는 사용자 저의 관점의 요점은 [`TokenEnhancer`](http://docs.spring.io/spring-security/oauth/apidocs/org/springframework/security/oauth2/provider/token/TokenEnhancer.html)이며, 이것은 토큰들이 저장소에 저장되기 전에 access 토큰과 refresh 토큰은 생성하게 요청할 것이다. 

class="org.springframework.security.oauth2.provider.approval.TokenServicesUserApprovalHandler"

존재하는 토큰들을 확인하면서 승인을 결정을 기억하여 사용자 승인을 다룬다. 



Authentication Manager(인증담당자) : 사용자 정보의 목록에서 주체의 신원증명이 일치하는지 검사한다.

keyword : UserDetails(사용자 정보), Pricipal(주체), Credentials(신원증명)

























