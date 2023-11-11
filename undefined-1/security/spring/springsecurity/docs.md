---
description: https://docs.spring.io/spring-security/reference/servlet/index.html
---

# Docs

## Architecture

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><img src="../../../../.gitbook/assets/image (1) (1).png" alt=""></td><td></td><td></td></tr><tr><td><p></p><p>클라이언트 요청을 받으면, 컨테이너는 Filter 인스턴스와 Servlet(DispatcherServlet) 을 포함하는 FilterChain 을 생성</p><ul><li>Servlet : HttpServletRequest를 처리. Spring MVC 에서는 DispatcherServlet 인스턴스</li></ul></td><td></td><td></td></tr><tr><td></td><td><img src="../../../../.gitbook/assets/image (2) (1).png" alt=""></td><td></td></tr><tr><td><p></p><p></p><p>DelegatingFilterProxy : Servlet Container 와 Spring ApplicationContext 간 연결하는 필터. </p><p></p><p>수동으로 Servlet Container 에 필터 인스턴스를 등록할 순 있지만, 해당 필터를 Spring Bean 으로 자연스럽게 연결할 수 없음 → DelegatingFilterProxy를 통해 Servlet Container 에 Spring Bean 으로 등록된 필터를 손쉽게 등록 가능.</p></td><td></td><td></td></tr><tr><td><img src="../../../../.gitbook/assets/image (127).png" alt=""></td><td></td><td></td></tr><tr><td><p>Spring Security 의 경우, FilterChainProxy 을 통해 Servlet 지원.</p><p></p><p>FilterChainProxy 는 SecurityFilterChain 을 통해 다수의 필터를 등록할 수 있고, FilterChainProxy Bean은 DelegatingFilterProxy 로 wrapping 처리됨</p></td><td></td><td></td></tr><tr><td><img src="../../../../.gitbook/assets/image (128).png" alt=""></td><td></td><td><img src="../../../../.gitbook/assets/image (129).png" alt=""></td></tr><tr><td><p>SecurityFilterChain은 현재 요청에 대해 어떤 Spring Security Filter 인스턴스를 호출해야 하는지 결정</p><p></p><p>SecurityFilterChain 내 Security Filter 는 일반적으로 FilterChainProxy에 등록. 이는 Servlet Container 또는 DelegatingFilterProxy에 등록하는 데 아래와 같은 도움을 줌.</p><p>1. Spring Security Debug</p><p>2. 임의 동작 수행 (Security Context 삭제, 특정 공격 방어 등)</p><p>3. RequestMatcher 를 사용한 HttpServletRequest 가 관리하는 항목을 기반으로 SecurityFilterChain 호출 가능</p><p>→ 다중 SecurityFilterChain 에서 어떤 필터를 사용할 지 결정 가능</p></td><td>ex. 그림처럼 /api/** 경로와 /** 경로에 대한 필터 별도 지정</td><td></td></tr><tr><td><img src="../../../../.gitbook/assets/image (130).png" alt=""></td><td></td><td></td></tr><tr><td><p>SecurityFilter 의 경우, api 를 사용하여 삽입. 인증, 인가, 보안 등의 다양항 목적으로 사용 가능.</p><p></p><p>특정한 순서로 실행 (ex. 인가보다 인증이 먼저)</p><p></p><p>실행 순서가 알고싶다면 <a href="https://github.com/spring-projects/spring-security/blob/6.1.2/config/src/main/java/org/springframework/security/config/annotation/web/builders/FilterOrderRegistration.java">FilterOrderRegistration</a> 확인</p></td><td></td><td><p>샘플 구성은 다음 순서와 같이 동작</p><ol><li>csrf [CsrfFilter]</li><li>formLogin [UsernamePasswordAuthenticationFilter]</li><li>httpBasic [BasicAuthenticationFilter]</li><li>authrizeHttpRequests [AuthorizationFilter]</li></ol></td></tr><tr><td><p> </p><pre><code>2023-06-14T08:55:22.321-03:00  INFO 76975 --- [           main] o.s.s.web.DefaultSecurityFilterChain     : Will secure any request with [
org.springframework.security.web.session.DisableEncodeUrlFilter@404db674,
org.springframework.security.web.context.request.async.WebAsyncManagerIntegrationFilter@50f097b5,
org.springframework.security.web.context.SecurityContextHolderFilter@6fc6deb7,
org.springframework.security.web.header.HeaderWriterFilter@6f76c2cc,
org.springframework.security.web.csrf.CsrfFilter@c29fe36,
org.springframework.security.web.authentication.logout.LogoutFilter@ef60710,
org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter@7c2dfa2,
org.springframework.security.web.authentication.ui.DefaultLoginPageGeneratingFilter@4397a639,
org.springframework.security.web.authentication.ui.DefaultLogoutPageGeneratingFilter@7add838c,
org.springframework.security.web.authentication.www.BasicAuthenticationFilter@5cc9d3d0,
org.springframework.security.web.savedrequest.RequestCacheAwareFilter@7da39774,
org.springframework.security.web.servletapi.SecurityContextHolderAwareRequestFilter@32b0876c,
org.springframework.security.web.authentication.AnonymousAuthenticationFilter@3662bdff,
org.springframework.security.web.access.ExceptionTranslationFilter@77681ce4,
org.springframework.security.web.access.intercept.AuthorizationFilter@169268a7]
</code></pre></td><td></td><td></td></tr><tr><td><p></p><p></p><p>보안 필터 목록은 응용 프로그램 시작 시 INFO 수준의 로그에서 확인 가능</p></td><td></td><td></td></tr></tbody></table>



### Add custom filter

* 예시\
  요청 헤더에서 X-Tenant-Id 값을 가져와서 사용자 정보 처리 → 즉, 인증 전에 처리해야 함

<pre class="language-java" data-line-numbers><code class="lang-java">import java.io.IOException;

import jakarta.servlet.Filter;
import jakarta.servlet.FilterChain;
import jakarta.servlet.ServletException;
import jakarta.servlet.ServletRequest;
import jakarta.servlet.ServletResponse;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import org.springframework.security.access.AccessDeniedException;

public class TenantFilter implements Filter {

    @Override
    public void doFilter(
        ServletRequest servletRequest,
        ServletResponse servletResponse,
        FilterChain filterChain
    ) throws IOException, ServletException {
        HttpServletRequest request = (HttpServletRequest) servletRequest;
        HttpServletResponse response = (HttpServletResponse) servletResponse;

        String tenantId = request.getHeader("X-Tenant-Id");
        boolean hasAccess = isUserAllowed(tenantId);
        if (hasAccess) {
            filterChain.doFilter(request, response);
            return;
        }
        throw new AccessDeniedException("Access denied");
<strong>    }
</strong>
}
</code></pre>

* 20 line : X-Tenant-Id 값 획득
* 21 line : 사용자 정보 획득
* 23 line : 사용자가 맞다면, 이후 filter 처리 진행
* 26 line : 사용자가 아니라면, AccessDeniedException 에러 throw

<details>

<summary>OncePerRequestFilter를 extend 하여 구현해도 된다</summary>

참고 : [https://velog.io/@dhwlddjgmanf/%EA%BC%AC%EB%A6%AC%EB%B3%84-%EC%98%A4%EB%A5%98%EC%9D%BC%EC%A7%80-Spring-Security-%EC%A0%81%EC%9A%A9%EA%B8%B0](https://velog.io/@dhwlddjgmanf/%EA%BC%AC%EB%A6%AC%EB%B3%84-%EC%98%A4%EB%A5%98%EC%9D%BC%EC%A7%80-Spring-Security-%EC%A0%81%EC%9A%A9%EA%B8%B0)

이 OncePerRequestFilter는 사용자 요청 당 단 1회만 동작하는 필터 (이름에서부터 유추 가능)

{% code lineNumbers="true" %}
```kotlin
@Component
class AuthenticationFilter(
    private val tokenProvider: TokenProvider,
) : OncePerRequestFilter() {

    override fun doFilterInternal(
        request: HttpServletRequest,
        response: HttpServletResponse,
        filterChain: FilterChain
    ) {
        val token = tokenProvider.extractToken(request)

        if (token != null && tokenProvider.validateToken(token)) {
            val authentication = tokenProvider.getAuthentication(token) as UsernamePasswordAuthenticationToken
            authentication.details = WebAuthenticationDetailsSource().buildDetails(request)
            SecurityContextHolder.getContext().authentication = authentication
        }

        filterChain.doFilter(request, response)
    }
}
```
{% endcode %}



</details>



위처럼 필터 생성 후, 아래와 같이 등록한다

{% code lineNumbers="true" %}
```kotlin
@Bean
fun filterChain(http: HttpSecurity): SecurityFilterChain {
    http
        // ...
        .addFilterBefore(TenantFilter(), AuthorizationFilter::class.java)
    return http.build()
}
```
{% endcode %}

* 5 line :  AuthorizationFilter 앞에 등록함으로서 인가 처리 전에 TenantFilter 가 동작한다

cf. `addFilterAfter` 를 통해 어떤 필터 뒤에도 등록이 가능. `addFilterAt` 을 통해 특정 위치에 등록도 가능.



`@Component` 또는 `@Bean` 등으로 Spring Container 에 등록할 때는 Spring boot embedded container 에도 자동으로 등록되므로 주의해야 함

→ 필터가 2번 호출될 수도 있음 (Spring Container + Spring Security)

→ DI 를 사용하면서 위 사항을 방지하려면, FilterRegistrationBean 을 선언하고,\
해당 Filter 의 setEnabled 값을 false 로 등록

```java
@Bean
public FilterRegistrationBean<TenantFilter> tenantFilterRegistration(TenantFilter filter) {
    FilterRegistrationBean<TenantFilter> registration = new FilterRegistrationBean<>(filter);
    registration.setEnabled(false);
    return registration;
}
```



### Exception Handling

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td></td><td><img src="../../../../.gitbook/assets/image (131).png" alt=""></td><td></td></tr><tr><td></td><td><p><code>ExceptionTranslationFilter</code> 는 <code>FilterChainProxy</code> 에 등록할 수 있는 <code>SecurityFilter</code>.</p><p><code>AccessDeniedException</code> 과 <code>AuthenticationException</code> 을 HTTP 응답으로 변환</p></td><td><p></p><p>그림에서 …</p><ol><li><code>ExceptionTranslationFilter</code> 는 <code>FilterChain.doFilter()</code> 호출</li><li><p>인증되지 않은 사용자거나, <code>AuthenticationException</code>(인증 에러)인 경우, 인증을 시작</p><ul><li><code>SecurityContextHolder</code> 삭제</li><li><code>HttpServletRequest</code> 는 인증이 성공했을 때, 재사용 할 수 있도록 저장 (<code>RequestCache</code>)</li><li><code>AuthenticationEntryPoint</code> 는 클라이이언트로부터 자격 증명을 요청하는 데 사용 (리디렉션 등)</li></ul></li><li><code>AccessDeniedException</code> (엑세스 거부)의 경우, <code>AccessDeniedHandler</code> 에 의해 처리</li></ol><p></p><p>cf. <code>ExceptionTranslationFilter</code>는 <code>AccessDeniedException</code>, <code>AuthenticationException</code> 예외에만 처리. 그 외엔 동작 안함.</p></td></tr></tbody></table>

<details>

<summary>ExceptionTranslationFilter() : 코드로 보자면 이런 느낌…</summary>

```java
try {
	filterChain.doFilter(request, response);
} catch (AccessDeniedException | AuthenticationException ex) {
	if (!authenticated || ex instanceof AuthenticationException) {
		startAuthentication();
	} else {
		accessDenied();
	}
}
```

</details>



### 인증 요청 (임시) 저장

인증 처리 후 요청에 대한 처리를 하기 위해, `RequestCache` 에 HttpServlet 을 임시 저장한다 (위 ExceptionHandling 구조에서 확인 가능)

이는 인증이 완료된 요청에 대해 기존에 사용하던 페이지로 돌아가게 하는 데에 사용

ex. 로그인이 필요한 페이지에서 로그인이 처리된 후, 그 페이지로 되돌아갈 때

→ 무조건 홈페이지로 돌아가게 하기 위해서는 `nullRequestCache` 를 사용하면 된다

```java
// 기본적으로 HttpSessionRequestCache 를 사용
// 아래 코드는 continue 매개변수를 통해 동일 세션인지 아닌지를 판별
@Bean
DefaultSecurityFilterChain springSecurity(HttpSecurity http) throws Exception {
	HttpSessionRequestCache requestCache = new HttpSessionRequestCache();
	requestCache.setMatchingRequestParameterName("continue");
	http
		// ...
		.requestCache((cache) -> cache
			.requestCache(requestCache)
			// .requestCache(nullRequestCache) 를 사용하면 세션에 저장하지 않음
		);
	return http.build();
}
```

`RequestCacheAwareFilter` 를 사용하여 `RequestCache` 를 편하게 사용이 가능하다



### Logging

401, 403 에러에 대해 로깅 또는 디버깅을 위해 아래 properties 를 추가할 수 있음

```properties
logging.level.org.springframework.security=TRACE
```



## Authentication (인증)

### Authentication Architecture : 주요 아키텍처

* `SecurityContextHolder` : 인증된 사용자에 대한 정보를 저장
* `SecurityContext` : 위의 `SecurityContextHolder` 에서 받아올 수 있으며, 인증된 사용자의 `Authentication` 정보를 가지고 있음
* `Authentication` : 접근 주체에 대한 정보. `SecurityContext` 에 저장되며, 실제 `Authentication` 을 만들고 인증을 처리하는 건 `AuthenticationManager` 에서 담당
* `GrantedAuthority` : 인증 주체에 부여된 권한 (role, scopes 등)
* `AuthenticationManager` : Spring Security Filter 가 실제 인증 처리를 진행하는 부분 (`Authentication` 부분 참고)
* `ProviderManager` : 가장 일반적인 `AuthenticationManager` 의 구현체
* `AuthenticationProvider` : 특정 인증 처리를 위한 `ProviderManager`
* Request Credenticals with `AuthenticationEntryPoint` : 로그인 페이지 redirect, `WWW-Authenticate` 응답 등에 사용하는 클라이언트의 자격증명 요청
* `AbstractAuthenticationProcessingFilter` : 인증을 위한 기본 필터. 고수준의 인증 flow 와 여러 처리가 동작할 수 있도록 지원



### SecurityContextHolder

![](<../../../../.gitbook/assets/image (132).png>)

Spring Security 가 가지는 인증된 사용자에 대한 정보. Spring Security 는 `SecurityContextHolder` 가 어떻게 채워지는지 관심없으며, 값이 저장되어 있다면 인증된 사용자로 판단

{% code lineNumbers="true" %}
```kotlin
val context: SecurityContext = SecurityContextHolder.createEmptyContext()
val authentication: Authentication = TestingAuthenticationToken("username", "password", "ROLE_USER")
context.authentication = authentication

SecurityContextHolder.setContext(context)
```
{% endcode %}

* line 1 : 빈 `SecurityContext` 를 생성 → 여러 쓰레드의 영향을 피하기 위해 새로운 SecurityContext 를 생성하는 것이 좋다
* line 2 : `Authentication` 생성. 일반적으로는 `UsernamePasswordAuthenticationToken(userDetails, password, authorities)` 를 사용.

```kotlin
val context = SecurityContextHolder.getContext()
val authentication = context.authentication
val username = authentication.name
val principal = authentication.principal
val authorities = authentication.authorities
```

기본적으로 `SecurityContextHolder` 는 `ThreadLocal` 을 사용하여 `SecurityContext` 를 저장하여 관리하기에, 동일 쓰레드에서 `SecurityContext` 는 모두 동일.

request 처리 후에 `FilterChainProxy` 에 의해 `SecurityContext` 는 안전하게 삭제됨을 보장

기본적으로는 `ThreadLocal` 처리지만, 시작 옵션을 통해 `SecurityContextHolder` 의 `SecurityContext` 저장 방법을 정의할 수도 있음

→ 단일 App : SecurityContextHolder.MODE\_GLOBAL\
→ 다중 App 의 보안 쓰레드에서 처리 : SecurityContextHolder.MODE\_INHERITABLETHREADLOCAL



### Authentication (인증)







