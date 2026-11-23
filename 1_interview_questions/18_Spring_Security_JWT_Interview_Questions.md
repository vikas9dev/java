# Spring Security and JWT Interview Questions

**Spring Security and JWT Interview Questions** | A full guide to authentication, authorization, Spring Security architecture, JWT, OAuth2, and security configuration. Also see: [Spring Core](09_Spring_Core_Interview_Questions.md) | [REST API Design](https://github.com/vikas9dev/system-design/blob/main/iq/05_REST_API_Design_Interview_Questions.md) | [Microservices](17_Spring_Microservices_Interview_Questions.md)

📊 **Question Count by Section**

| # | Section | Questions |
|---|---|---|
| 1 | [Authentication and Authorization Fundamentals](#authentication-and-authorization-fundamentals) | 6 |
| 2 | [Spring Security Architecture](#spring-security-architecture) | 7 |
| 3 | [JWT Deep Dive](#jwt-deep-dive) | 6 |
| 4 | [Security Configuration](#security-configuration) | 6 |
| 5 | [OAuth2 Basics](#oauth2-basics) | 5 |
| 6 | [OAuth for Services and AI Agents](#oauth-for-services-and-ai-agents) | 8 |
| | **Total** | **38** |

> 🔥🔥 Very High — asked in almost every Tier-1 loop &nbsp;·&nbsp; 🔥 High — very frequent in Tier-1 interviews &nbsp;·&nbsp; ⚡ Medium — commonly asked &nbsp;·&nbsp; 💤 Low — good to know, rarely asked

<a id="authentication-and-authorization-fundamentals"></a>

## 1. Authentication and Authorization Fundamentals

1. **🔐 What is the difference between Authentication and Authorization? 🔥🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

Authentication and Authorization are the two base parts of application security. People often mix them up. But they do very different jobs in the security flow.

- 🔐 **Authentication** answers the question: **"Who are you?"** It checks the identity of a user, system, or service. Usually it checks credentials, such as username/password, tokens, biometrics, or certificates.
- 🛡️ **Authorization** answers the question: **"What are you allowed to do?"** It runs after the user's identity is confirmed. It decides which resources or actions the user can access. It decides based on roles, permissions, or policies.

| Feature | Authentication 🅰️ | Authorization 🅱️ |
|---------|-------------------|-------------------|
| **Purpose** | Verify identity | Grant/deny access to resources |
| **Question** | Who are you? | What can you do? |
| **Order** | ✅ Always first | ✅ Always second (after authentication) |
| **Mechanism** | Credentials (password, token, biometrics) | Roles, permissions, policies |
| **HTTP Error Code** | `401 Unauthorized` | `403 Forbidden` |
| **Spring API** | `AuthenticationManager` (interface) | `@PreAuthorize`, `@Secured` (annotations) |
| **Failure Result** | Login rejected | Access denied |
| **Data Checked** | Username, password, token | Roles, authorities, scopes |
| **Stateful Example** | Session ID validation | Session-based role check |
| **Stateless Example** | JWT signature verification | JWT claims/roles check |

```mermaid
graph LR
    subgraph AuthN["🔐 Authentication"]
        A[Client sends credentials] --> B{Valid?}
        B -->|Yes| C[Identity confirmed]
        B -->|No| D[401 Unauthorized]
    end

    subgraph AuthZ["🛡️ Authorization"]
        C --> E{Has permission?}
        E -->|Yes| F[Access granted]
        E -->|No| G[403 Forbidden]
    end

    classDef purple fill:#7C3AED,stroke:#7C3AED,color:#fff
    classDef cyan fill:#0891B2,stroke:#0891B2,color:#fff
    classDef green fill:#059669,stroke:#059669,color:#fff
    classDef red fill:#DC2626,stroke:#DC2626,color:#fff
    classDef orange fill:#D97706,stroke:#D97706,color:#fff

    class A,B purple
    class C,E cyan
    class F green
    class D,G red
```

🧠 **In Simple Words:**

- **Authentication** is like showing your ID card at the office entrance. It proves you are who you say you are.
- **Authorization** is like the access card inside the office. It decides which floors and rooms you can enter.

🎯 **Interview Tip:** Always say that authentication comes **before** authorization. Then map each one to an HTTP status code:

- `401` for authentication failure
- `403` for authorization failure

Interviewers like it when you link concepts to real HTTP behaviour.

---

</details>

---

2. **🔑 What are the common authentication mechanisms used in web applications? 🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

Web applications use different authentication mechanisms. The choice depends on the architecture, the security needs, and the user experience goals. Here are the most common ones:

| Mechanism | How It Works | Best For | Statefulness |
|-----------|-------------|----------|--------------|
| **Basic Auth** | Base64-encoded `username:password` in `Authorization` header | Simple APIs, testing | Stateless |
| **Form-Based** | HTML login form + server-side session | Traditional web apps | Stateful |
| **Token-Based (JWT)** | Signed JSON token in `Authorization: Bearer` header | REST APIs, SPAs, Microservices | Stateless |
| **Session-Based** | Server stores session in memory/Redis, client sends session cookie | MVC web apps | Stateful |
| **Certificate-Based (mTLS)** | Client presents X.509 certificate during TLS handshake | Service-to-service, banking | Stateless |
| **API Key** | Unique key sent in header or query param | Public APIs, rate limiting | Stateless |
| **OAuth2 / OIDC** | Delegated authorization via authorization server | Third-party login (Google, GitHub) | Depends on grant type |

1️⃣ **Basic Authentication:**

```
Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=
```

- 📤 Credentials sent with every request (Base64 encoded, not encrypted).
- ⚠️ Must always be used over HTTPS. Anyone can decode Base64 very easily.
- 🛠️ Simple to build. But not fit for production without TLS.

2️⃣ **Token-Based (JWT):**

```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

- 🔒 Server generates a signed token after successful login.
- 📈 Stateless. The server does not need to store sessions.
- ⚡ Very good for microservices and horizontally scaled systems.

3️⃣ **Session-Based:**

- 🗄️ Server creates an `HttpSession` and returns a `JSESSIONID` cookie.
- 💾 The server stores session data in its memory or in an external store (Redis).
- 🔄 The browser sends the cookie automatically with every request.

4️⃣ **Certificate-Based (mTLS):**

- 🔏 Both client and server present certificates during TLS handshake.
- 🏦 Common in banking, government, and inter-service communication.
- 🛡️ Very strong authentication. To pretend to be a client, an attacker must steal that client's private key.

💡 **Key Insight:** For modern REST APIs and microservices, **JWT-based token authentication** is the industry standard. The reasons:

- it is stateless
- it scales well
- it works smoothly across service boundaries

Teams still prefer session-based authentication for traditional server-rendered web applications.

🎯 **Interview Tip:** If they ask which mechanism you would choose, always start with "it depends on the architecture." Then:

- For microservices, say JWT.
- For a monolith with server-side rendering, say session-based.

This shows architectural thinking.

---

</details>

---

3. **🏗️ What is RBAC vs ABAC? How do they differ in access control? ⚡**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

RBAC (Role-Based Access Control) and ABAC (Attribute-Based Access Control) are two major access control models. Applications use them to enforce authorization policies.

🔹 **RBAC (Role-Based Access Control):**

- 👤 Access decisions are based on the **roles** assigned to a user.
- 🏷️ Each role has a predefined set of permissions.
- 🛠️ Example: A user with the `ADMIN` role can access `/admin/**` endpoints. A user with the `USER` role can only access `/profile/**`.

```java
// Spring Security RBAC example
@PreAuthorize("hasRole('ADMIN')")
public void deleteUser(Long userId) {
    userRepository.deleteById(userId);
}

@PreAuthorize("hasAnyRole('ADMIN', 'MANAGER')")
public List<Report> getReports() {
    return reportRepository.findAll();
}
```

🔸 **ABAC (Attribute-Based Access Control):**

- 📋 Access decisions are based on **attributes** of the user, resource, action, and environment.
- 🧩 Much more fine-grained. You can create policies like "Allow access if user's department is 'Finance' AND the document's classification is 'Internal' AND it is between 9 AM and 6 PM."
- 🔧 More complex to build, but much more flexible.

```java
// Spring Security ABAC-like example using SpEL
// (principal.department needs a custom UserDetails class with a department field)
@PreAuthorize("hasRole('MANAGER') and #report.department == authentication.principal.department")
public void approveReport(Report report) {
    report.setApproved(true);
    reportRepository.save(report);
}
```

| Feature | RBAC 🅰️ | ABAC 🅱️ |
|---------|---------|---------|
| **Access Based On** | Roles assigned to user | Attributes of user, resource, environment |
| **Granularity** | ⚠️ Coarse-grained | ✅ Fine-grained |
| **Complexity** | ✅ Simple to implement | ⚠️ Complex policy engine needed |
| **Scalability** | ⚠️ Role explosion with many combinations | ✅ Scales well with complex policies |
| **Example** | "Admins can delete users" | "Managers in Finance dept can approve reports during business hours" |
| **Spring Support** | `hasRole()`, `@Secured` | SpEL expressions in `@PreAuthorize` |
| **Use Case** | Most web applications | Healthcare, banking, government systems |
| **Maintenance** | ✅ Easy — manage roles | ⚠️ Harder — manage attribute policies |

🧠 **In Simple Words:**

- **RBAC** is like a key card system. Your card (role) opens certain doors.
- **ABAC** is like a smart lock. It checks who you are, what time it is, and what you are trying to access. Then it decides.

💡 **Pro Tip:** Most real-world applications use a **hybrid approach**:

- RBAC for broad access control
- ABAC for fine-grained decisions that depend on context

Spring Security supports both through `@PreAuthorize` with SpEL expressions.

This is the honest way to say it in an interview: *"authorization was a first-class service with its own tables and APIs, not `@PreAuthorize` strings scattered across controllers — because the permission model itself was configurable per tenant."*

Here, also name Spring Security's own `RoleHierarchy` bean. It is the framework version of the same idea. You declare `ROLE_ADMIN > ROLE_MANAGER > ROLE_USER` once. Then `hasRole('USER')` passes for an admin too. You do not need to list every role at every endpoint.

---

</details>

---

4. **🔄 What is the difference between Stateful and Stateless Authentication? 🔥🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

Stateful and stateless authentication are two very different ways to manage user sessions in web applications.

🗄️ **Stateful Authentication (Session-Based):**

- The server creates and keeps an `HttpSession` for each authenticated user.
- The server generates a unique `sessionId` and sends it to the client as a cookie.
- On every later request, the client sends the cookie. The server validates it against the stored session.
- On logout, the server invalidates the session.

🔑 **Stateless Authentication (Token-Based / JWT):**

- The server does **not** store any session data.
- After successful authentication, the server generates a signed token (JWT). The token holds all the user information that is needed.
- The client stores the token and sends it with every request in the `Authorization` header.
- The server validates the token's signature and expiration. It does not need a server-side lookup.

```mermaid
sequenceDiagram
    participant C as Client
    participant S as Server
    participant M as Session Store

    rect rgb(65, 40, 100)
        Note over C,M: Stateful Authentication
        C->>S: Login (username + password)
        S->>M: Create HttpSession
        S-->>C: Set-Cookie: JSESSIONID=abc123
        C->>S: Request + Cookie (JSESSIONID=abc123)
        S->>M: Validate session
        M-->>S: Session valid
        S-->>C: Response
    end

    rect rgb(0, 60, 80)
        Note over C,S: Stateless Authentication
        C->>S: Login (username + password)
        S-->>C: JWT Token
        C->>S: Request + Authorization: Bearer <JWT>
        S->>S: Verify JWT signature locally
        S-->>C: Response
    end
```

<img src="./img/security_jwt_session_vs_token_auth.png" alt="Session-Based vs Token-Based Authentication" style="max-width:100%;"/>

| Feature | Stateful (Session) 🅰️ | Stateless (JWT) 🅱️ |
|---------|----------------------|---------------------|
| **Server Storage** | ❌️ Requires session store (RAM/Redis) | ✅ No server-side storage |
| **Scalability** | ⚠️ Hard to scale horizontally | ✅ Easy horizontal scaling |
| **Performance** | ⚠️ Session lookup on every request | ✅ Token verified locally (signature check) |
| **Revocation** | ✅ Easy — invalidate session on server | ⚠️ Hard — token valid until expiry |
| **Use Case** | Traditional web apps (MVC) | REST APIs, Microservices, SPAs |
| **Security** | ✅ Server controls session | ⚠️ Token theft risk (store securely) |
| **Cross-Domain** | ⚠️ Cookie-based, domain-restricted | ✅ Works across domains easily |
| **Memory** | ❌️ Consumes server memory per user | ✅ Zero server memory |
| **Logout** | ✅ Simple — destroy session | ⚠️ Requires token blacklist or short TTL |

🔑 **Key Point:** In microservices architecture, teams strongly prefer **stateless authentication (JWT)**. Each service can validate the token on its own. It does not need a shared session store. This makes the system handle failures better and easier to scale.

🎯 **Interview Tip:** When you talk about stateless authentication, always mention the **token revocation challenge**. There is no server-side state, so you cannot simply invalidate a token. Solutions:

- short-lived tokens with refresh tokens
- token blacklists
- token versioning

---

</details>

---

5. **👤 What are Principal, GrantedAuthority, and SecurityContext in Spring Security? 🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

These three are core concepts in Spring Security's authentication and authorization model. In order, they stand for:

- the **who**
- **what permissions**
- **where it is stored**

1️⃣ **`Principal`** — The user who is authenticated right now (the "who").

- 📖 It is an interface from `java.security.Principal`.
- 👤 In Spring Security, the principal is usually the `UserDetails` object or the username string.
- 🔍 You can get it with `SecurityContextHolder.getContext().getAuthentication().getPrincipal()`. Or you can inject it directly into a controller method.

```java
@GetMapping("/profile")
public ResponseEntity<String> getProfile(Principal principal) {
    return ResponseEntity.ok("Logged in as: " + principal.getName());
}
```

2️⃣ **`GrantedAuthority`** — A permission or role given to the user (the "what can you do").

- 🛡️ It is an interface with a single method: `getAuthority()` that returns a `String`.
- 🏷️ Roles in Spring Security are `GrantedAuthority` objects with a `ROLE_` prefix (e.g., `ROLE_ADMIN`).
- 📋 A user can have multiple authorities.

```java
// Creating authorities
List<GrantedAuthority> authorities = List.of(
    new SimpleGrantedAuthority("ROLE_ADMIN"),
    new SimpleGrantedAuthority("ROLE_USER"),
    new SimpleGrantedAuthority("PERMISSION_READ_REPORTS")
);

// Checking authorities
@PreAuthorize("hasAuthority('ROLE_ADMIN')")
public void adminAction() { /* ... */ }

@PreAuthorize("hasRole('ADMIN')")  // Automatically checks for ROLE_ADMIN
public void adminAction2() { /* ... */ }
```

3️⃣ **`SecurityContext`** — The container that holds the `Authentication` object (the "where it is stored").

- 🗂️ Accessed via `SecurityContextHolder.getContext()`.
- 🔒 By default, it uses the `ThreadLocal` strategy. Each thread has its own security context.
- 📦 The `Authentication` object inside it holds the principal, credentials, and authorities.

```java
// Reading SecurityContext
SecurityContext context = SecurityContextHolder.getContext();
Authentication authentication = context.getAuthentication();

String username = authentication.getName();                    // Principal
Object credentials = authentication.getCredentials();          // Password (often null after auth)
Collection<? extends GrantedAuthority> authorities =
    authentication.getAuthorities();                           // Roles/Permissions
boolean isAuthenticated = authentication.isAuthenticated();    // Auth status
```

```mermaid
graph TD
    SCH["SecurityContextHolder"] --> SC["SecurityContext"]
    SC --> AUTH["Authentication"]
    AUTH --> P["Principal<br/>(UserDetails / username)"]
    AUTH --> C["Credentials<br/>(password — cleared after auth)"]
    AUTH --> GA["GrantedAuthority[]<br/>(ROLE_ADMIN, ROLE_USER)"]

    classDef purple fill:#7C3AED,stroke:#7C3AED,color:#fff
    classDef cyan fill:#0891B2,stroke:#0891B2,color:#fff
    classDef green fill:#059669,stroke:#059669,color:#fff
    classDef orange fill:#D97706,stroke:#D97706,color:#fff

    class SCH purple
    class SC cyan
    class AUTH orange
    class P,C,GA green
```

<img src="./img/security_jwt_securitycontext_hierarchy.png" alt="Spring Security Architecture — SecurityContext Hierarchy" style="max-width:100%;"/>

📝 **Note:** The `SecurityContextHolder` uses a `ThreadLocal` by default (`MODE_THREADLOCAL`).

For `@Async` / thread-pool work, use Spring's `DelegatingSecurityContextExecutor` (or `DelegatingSecurityContextRunnable` / `...Callable`). Do **not** use `MODE_INHERITABLETHREADLOCAL`. The reason:

- Inheritance happens at thread *creation*.
- So a pooled worker created before the context was set inherits nothing.
- And a reused worker can inherit a **stale** (old) context from a previous request.

That is exactly why the `DelegatingSecurityContext*` wrappers exist.

⚠️ **Reactive / WebFlux does not use `SecurityContextHolder` at all.** It uses `ReactiveSecurityContextHolder`. This stores the context in the **Reactor subscriber `Context`**, not in a `ThreadLocal`. The reason: a reactive chain moves between threads in the middle of a request. So no strategy tied to one thread could work.

🎯 **Interview Tip:** A common follow-up is "How does the SecurityContext survive across requests in a stateful app?" In Spring Security 6 the answer is **`SecurityContextHolderFilter`**:

- At the start of the request, it **loads** the context from the `SecurityContextRepository` (`HttpSessionSecurityContextRepository` by default).
- At the end, it clears the holder.

Saving is now **explicit**. Each authentication filter calls `SecurityContextRepository.saveContext(...)` itself. The old `SecurityContextPersistenceFilter` saved automatically on every request. It is `@Deprecated` in Spring Security 6, so do not mention it in the interview.

---

</details>

---

6. **🛡️ What is the difference between hasRole() and hasAuthority() in Spring Security? ⚡**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

Both `hasRole()` and `hasAuthority()` check user permissions in Spring Security. They differ in how they handle the `ROLE_` prefix.

🔹 **`hasAuthority(String authority)`:**

- Checks for the **exact** string match of the authority.
- It adds no prefix. You must give the full authority string.
- Works with both roles and fine-grained permissions.

🔸 **`hasRole(String role)`:**

- Adds `ROLE_` to the front of the given string before it checks.
- `hasRole("ADMIN")` internally checks for the authority `ROLE_ADMIN`.
- Made only for role-based checks.

```java
// These two are EQUIVALENT:
@PreAuthorize("hasRole('ADMIN')")          // checks for ROLE_ADMIN
public void archiveUser(Long id) { /* ... */ }

@PreAuthorize("hasAuthority('ROLE_ADMIN')") // checks for ROLE_ADMIN
public void archiveUser2(Long id) { /* ... */ }

// For fine-grained permissions, use hasAuthority:
@PreAuthorize("hasAuthority('PERMISSION_DELETE_USER')")
public void deleteUser(Long id) { /* ... */ }
```

| Feature | `hasRole()` 🅰️ | `hasAuthority()` 🅱️ |
|---------|----------------|---------------------|
| **ROLE_ prefix** | ✅ Auto-prepends `ROLE_` | ❌️ No prefix — exact match |
| **`hasRole("ADMIN")`** | Checks for `ROLE_ADMIN` | N/A |
| **`hasAuthority("ADMIN")`** | N/A | Checks for `ADMIN` (no prefix) |
| **Use Case** | Role-based checks | Fine-grained permission checks |
| **Variants** | `hasAnyRole("ADMIN", "MANAGER")` | `hasAnyAuthority("READ", "WRITE")` |

⚠️ **Common Pitfall:** Say you store authorities as `ADMIN` (without the `ROLE_` prefix) in the database. If you then use `hasRole("ADMIN")`, the check fails, because `hasRole` looks for `ROLE_ADMIN`. Fix: either store roles with the prefix, or use `hasAuthority()` instead.

```java
// Storing user with roles:
UserDetails user = User.builder()
    .username("sam")
    .password(encoder.encode("password"))
    .roles("ADMIN")        // Internally stores as ROLE_ADMIN
    .build();

// OR using authorities directly:
UserDetails user = User.builder()
    .username("sam")
    .password(encoder.encode("password"))
    .authorities("ROLE_ADMIN", "PERMISSION_READ", "PERMISSION_WRITE")
    .build();
```

💡 **Pro Tip:** Use `hasRole()` for coarse-grained role checks. Use `hasAuthority()` for fine-grained permission checks. A user can have both roles (`ROLE_ADMIN`) and permissions (`PERMISSION_DELETE_USER`) as `GrantedAuthority` objects.

---

</details>

---

<a id="spring-security-architecture"></a>

## 2. Spring Security Architecture

1. **🏛️ Explain the Spring Security Filter Chain architecture. How does a request flow through it? 🔥🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

Spring Security uses a **filter-based architecture**. It intercepts every HTTP request before the request reaches the `DispatcherServlet`. The core components are:

1️⃣ **`DelegatingFilterProxy`** — A standard Servlet `Filter`, registered with the Servlet container. It passes the actual security work to a Spring-managed bean called `FilterChainProxy`. It connects the Servlet world to Spring's ApplicationContext.

2️⃣ **`FilterChainProxy`** — A Spring bean that holds one or more `SecurityFilterChain` instances. It matches the request URL against URL patterns. Then it decides which `SecurityFilterChain` handles the current request.

3️⃣ **`SecurityFilterChain`** — Holds an ordered list of security `Filter` instances (typically 15-20 filters). Each filter handles one specific security concern.

**① Entry & chain selection — `FilterChainProxy` picks the *first* matching chain:**

```mermaid
graph TD
    Client["🖥️ Client Request"] --> SC["Servlet Container"]
    SC --> DFP["DelegatingFilterProxy"]
    DFP --> FCP["FilterChainProxy"]
    FCP --> SFC1{"Match /api/**?"}
    SFC1 -->|No| SFC2{"Match /**?"}

    classDef purple fill:#7C3AED,stroke:#7C3AED,color:#fff
    classDef cyan fill:#0891B2,stroke:#0891B2,color:#fff
    classDef orange fill:#D97706,stroke:#D97706,color:#fff

    class Client cyan
    class SC,DFP purple
    class FCP orange
    class SFC1,SFC2 orange
```

**② The selected chain runs, then the request finally reaches Spring MVC:**

```mermaid
graph TD
    SFC1{"Match /api/**?"} -->|Yes| Chain1["SecurityFilterChain 1<br/>(JWT filters for APIs)"]
    SFC2{"Match /**?"} -->|Yes| Chain2["SecurityFilterChain 2<br/>(Form login for web)"]

    Chain1 --> DS["DispatcherServlet"]
    Chain2 --> DS
    DS --> Ctrl["Controller"]

    classDef cyan fill:#0891B2,stroke:#0891B2,color:#fff
    classDef green fill:#059669,stroke:#059669,color:#fff
    classDef orange fill:#D97706,stroke:#D97706,color:#fff

    class SFC1,SFC2 orange
    class Chain1,Chain2 green
    class DS,Ctrl cyan
```

> The 🟠 match nodes connect the two diagrams. The key points cover both:
> - **Only one** chain ever runs per request. The first match wins, so declare the specific `/api/**` chain before the catch-all `/**`.
> - The request reaches `DispatcherServlet` only *after* that chain completes.

<img src="./img/security_jwt_filter_chain_architecture.png" alt="Spring Security Filter Chain Architecture" style="max-width:100%;"/>

📋 **Key filters in the default SecurityFilterChain (in order):**

| # | Filter | Purpose |
|---|--------|---------|
| 1 | `DisableEncodeUrlFilter` | Prevents session ID from being added to URLs |
| 2 | `SecurityContextHolderFilter` | Loads the `SecurityContext` (saving is explicit in 6.x) |
| 3 | `HeaderWriterFilter` | Adds security headers (X-Frame-Options, etc.) |
| 4 | `CsrfFilter` | CSRF protection |
| 5 | `LogoutFilter` | Handles `/logout` requests |
| 6 | `UsernamePasswordAuthenticationFilter` | Processes form login |
| 7 | `BasicAuthenticationFilter` | Processes HTTP Basic auth |
| 8 | `RequestCacheAwareFilter` | Caches the request for redirect after login |
| 9 | `SecurityContextHolderAwareRequestFilter` | Wraps the request with security methods |
| 10 | `AnonymousAuthenticationFilter` | Assigns anonymous authentication if none exists |
| 11 | `ExceptionTranslationFilter` | Translates security exceptions to HTTP responses |
| 12 | `AuthorizationFilter` | Final authorization check (replaces `FilterSecurityInterceptor`) |

🔑 **Key Point:** The filters run in a strict order.
- A filter may authenticate the request successfully (e.g., `UsernamePasswordAuthenticationFilter`). Then it sets the `Authentication` object in the `SecurityContext`, and later filters can use it.
- If a later filter throws `AuthenticationException` or `AccessDeniedException`, `ExceptionTranslationFilter` turns it into a 401 or 403 response. (A login filter such as `UsernamePasswordAuthenticationFilter` handles its own failure with an `AuthenticationFailureHandler`.)

📝 **Note:** Spring Security 6 made two replacements:
- `AuthorizationFilter` replaced `FilterSecurityInterceptor`.
- `SecurityContextHolderFilter` replaced `SecurityContextPersistenceFilter` (now `@Deprecated`).

⚠️ That second one is **not just a rename**:
- The old filter loaded *and auto-saved* the context on every request.
- `SecurityContextHolderFilter` only **loads** it. Saving became explicit, via `SecurityContextRepository.saveContext(...)`. The authentication filter that actually authenticated the request calls it.

This is why a stateless chain costs little: it does not save the context back on every request. Always use the Spring Security 6 class names in interviews.

🎯 **Interview Tip:** When you explain the filter chain, draw the flow: `Client -> DelegatingFilterProxy -> FilterChainProxy -> SecurityFilterChain -> DispatcherServlet`. Mention that you can have multiple `SecurityFilterChain` beans for different URL patterns. For example, one for APIs with JWT, and another for web pages with form login.

---

</details>

---

2. **🗂️ What is SecurityContextHolder and how does it work internally? 🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

`SecurityContextHolder` is the most basic object in Spring Security. It is a **static utility class**. It stores the `SecurityContext`, which contains the `Authentication` object. It makes this context available across the whole application.

⚙️ **How it works internally:**

`SecurityContextHolder` uses a **strategy pattern** to decide how it stores the `SecurityContext`. You configure the strategy through the `SecurityContextHolderStrategy` interface.

| Strategy | Constant | How It Stores Context | Use Case |
|----------|----------|----------------------|----------|
| **ThreadLocal** | `MODE_THREADLOCAL` | Each thread has its own context | ✅ Default — web apps (one request per thread) |
| **InheritableThreadLocal** | `MODE_INHERITABLETHREADLOCAL` | Child threads inherit parent's context | Async tasks that spawn child threads |
| **Global** | `MODE_GLOBAL` | Single global context for all threads | Standalone apps, desktop apps |

```java
// Setting the strategy (typically done at startup)
SecurityContextHolder.setStrategyName(SecurityContextHolder.MODE_THREADLOCAL);

// How Spring Security sets the authentication after successful login
SecurityContext context = SecurityContextHolder.createEmptyContext();
Authentication authentication = new UsernamePasswordAuthenticationToken(
    userDetails, null, userDetails.getAuthorities());
context.setAuthentication(authentication);
SecurityContextHolder.setContext(context);

// How to read the current user anywhere in the application
SecurityContext context = SecurityContextHolder.getContext();
Authentication auth = context.getAuthentication();
String username = auth.getName();
Collection<? extends GrantedAuthority> roles = auth.getAuthorities();
```

```mermaid
graph TD
    subgraph Thread1["Thread 1 (Request A)"]
        TL1["ThreadLocal<SecurityContext>"]
        SC1["SecurityContext"]
        AUTH1["Authentication<br/>user: admin"]
        TL1 --> SC1 --> AUTH1
    end

    subgraph Thread2["Thread 2 (Request B)"]
        TL2["ThreadLocal<SecurityContext>"]
        SC2["SecurityContext"]
        AUTH2["Authentication<br/>user: john"]
        TL2 --> SC2 --> AUTH2
    end

    SCH["SecurityContextHolder"] --> TL1
    SCH --> TL2

    classDef purple fill:#7C3AED,stroke:#7C3AED,color:#fff
    classDef cyan fill:#0891B2,stroke:#0891B2,color:#fff
    classDef green fill:#059669,stroke:#059669,color:#fff
    classDef orange fill:#D97706,stroke:#D97706,color:#fff

    class SCH purple
    class TL1,TL2 cyan
    class SC1,SC2 orange
    class AUTH1,AUTH2 green
```

⚠️ **Important:** Spring stores the `SecurityContext` in `ThreadLocal`, so it is **request-scoped** by default. After the request is processed, `SecurityContextHolderFilter` clears the context. This prevents memory leaks and stops one request's data from leaking into another request.

📝 **Note:** With `@Async` methods or `CompletableFuture`, Spring does **not** automatically pass (propagate) the security context to the new thread. You must wrap the executor. For an `@Async` task executor, use `DelegatingSecurityContextAsyncTaskExecutor` (for a plain `Executor`, use `DelegatingSecurityContextExecutor` or `DelegatingSecurityContextRunnable`):

```java
@Bean
public Executor taskExecutor() {
    ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
    executor.setCorePoolSize(5);
    executor.initialize();
    return new DelegatingSecurityContextAsyncTaskExecutor(executor);
}
```

🎯 **Interview Tip:** A common question is "What happens when you use `@Async` with Spring Security?" The answer: the security context is lost. It lives in `ThreadLocal`, and the async task runs on a different thread. You must pass it to the new thread yourself.

---

</details>

---

3. **📦 How do you implement UserDetailsService and UserDetails in Spring Security? 🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

`UserDetailsService` and `UserDetails` are core interfaces in Spring Security's authentication mechanism. Together, they define two things: **how user data is loaded** and **what user information looks like**.

🔹 **`UserDetailsService` (Interface):**

- Has a single method: `loadUserByUsername(String username)`.
- Called by `DaoAuthenticationProvider` during authentication.
- You implement it to load user data from your data source (database, LDAP, API, etc.).

🔸 **`UserDetails` (Interface):**

- Represents the user's core information: username, password, authorities, and account status flags.
- Spring provides a default implementation: `org.springframework.security.core.userdetails.User`.

```java
// 1. Entity class
@Entity
@Table(name = "users")
@Data
@NoArgsConstructor
@AllArgsConstructor
public class AppUser {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(unique = true, nullable = false)
    private String username;

    @Column(nullable = false)
    private String password;

    private boolean enabled = true;

    @ElementCollection(fetch = FetchType.EAGER)
    @CollectionTable(name = "user_roles", joinColumns = @JoinColumn(name = "user_id"))
    @Column(name = "role")
    private Set<String> roles = new HashSet<>();
}
```

```java
// 2. Repository
public interface AppUserRepository extends JpaRepository<AppUser, Long> {
    Optional<AppUser> findByUsername(String username);
}
```

```java
// 3. UserDetailsService implementation
@Service
public class CustomUserDetailsService implements UserDetailsService {

    @Autowired
    private AppUserRepository userRepository;

    @Override
    public UserDetails loadUserByUsername(String username)
            throws UsernameNotFoundException {
        AppUser appUser = userRepository.findByUsername(username)
                .orElseThrow(() -> new UsernameNotFoundException(
                    "User not found: " + username));

        return User.builder()
                .username(appUser.getUsername())
                .password(appUser.getPassword())  // Already encoded in DB
                .authorities(appUser.getRoles().stream()
                    .map(role -> new SimpleGrantedAuthority("ROLE_" + role))
                    .collect(Collectors.toList()))
                .accountExpired(false)
                .accountLocked(false)
                .credentialsExpired(false)
                .disabled(!appUser.isEnabled())
                .build();
    }
}
```

```java
// 4. Alternative: Custom UserDetails implementation
public class CustomUserDetails implements UserDetails {

    private final AppUser appUser;

    public CustomUserDetails(AppUser appUser) {
        this.appUser = appUser;
    }

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        return appUser.getRoles().stream()
                .map(role -> new SimpleGrantedAuthority("ROLE_" + role))
                .collect(Collectors.toSet());
    }

    @Override
    public String getPassword() {
        return appUser.getPassword();
    }

    @Override
    public String getUsername() {
        return appUser.getUsername();
    }

    @Override
    public boolean isAccountNonExpired() {
        return true;
    }

    @Override
    public boolean isAccountNonLocked() {
        return true;
    }

    @Override
    public boolean isCredentialsNonExpired() {
        return true;
    }

    @Override
    public boolean isEnabled() {
        return appUser.isEnabled();
    }

    // Custom method to expose additional user fields
    public Long getUserId() {
        return appUser.getId();
    }
}
```

📝 **Note:** Since Spring Security 6.3, four methods in `UserDetails` have **default implementations** that return `true`: `isAccountNonExpired()`, `isAccountNonLocked()`, `isCredentialsNonExpired()`, and `isEnabled()`. So you only need to override them if your application tracks account status.

🔑 **Key Point:** Prefer the custom `UserDetails` implementation when you need extra user information (like `userId`, `email`, `department`). The default `User` class does not carry these. In your controllers, you can then cast the principal to `CustomUserDetails` to read these fields.

```java
@GetMapping("/profile")
public ResponseEntity<Map<String, Object>> getProfile() {
    CustomUserDetails user = (CustomUserDetails) SecurityContextHolder
        .getContext().getAuthentication().getPrincipal();
    return ResponseEntity.ok(Map.of(
        "userId", user.getUserId(),
        "username", user.getUsername(),
        "roles", user.getAuthorities()
    ));
}
```

---

</details>

---

4. **⚙️ What is AuthenticationManager and AuthenticationProvider? How do they work together? 🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

`AuthenticationManager` and `AuthenticationProvider` are the core interfaces that run the actual **authentication process** in Spring Security.

🔹 **`AuthenticationManager` (Interface):**

- Has a single method: `authenticate(Authentication authentication)`.
- Acts as the **entry point** for authentication. It delegates the actual work to one or more `AuthenticationProvider` instances.
- The default implementation is `ProviderManager`.

🔸 **`AuthenticationProvider` (Interface):**

- Has two methods: `authenticate()` and `supports(Class<?> authentication)`.
- Performs the **actual authentication** against a specific credential type (username/password, LDAP, OAuth, etc.).
- The most common implementation is `DaoAuthenticationProvider`. It uses `UserDetailsService` and `PasswordEncoder`.

```mermaid
sequenceDiagram
    participant C as Client
    participant F as AuthenticationFilter
    participant AM as AuthenticationManager<br/>(ProviderManager)
    participant AP1 as DaoAuthenticationProvider
    participant AP2 as LdapAuthenticationProvider
    participant UDS as UserDetailsService
    participant PE as PasswordEncoder
    participant DB as Database

    C->>F: POST /login (username, password)
    F->>AM: authenticate(UsernamePasswordAuthenticationToken)
    AM->>AP1: supports(UsernamePasswordAuthenticationToken)?
    AP1-->>AM: true
    AM->>AP1: authenticate(token)
    AP1->>UDS: loadUserByUsername(username)
    UDS->>DB: SELECT * FROM users WHERE username=?
    DB-->>UDS: User record
    UDS-->>AP1: UserDetails
    AP1->>PE: matches(rawPassword, encodedPassword)
    PE-->>AP1: true
    AP1-->>AM: Authenticated UsernamePasswordAuthenticationToken
    AM-->>F: Authentication (with authorities)
    F-->>C: 200 OK + JWT Token
```

```java
// Spring Security 6 configuration
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Autowired
    private UserDetailsService userDetailsService;

    @Autowired
    private PasswordEncoder passwordEncoder;

    // AuthenticationProvider bean
    @Bean
    public AuthenticationProvider authenticationProvider() {
        // Since Spring Security 6.5 the no-arg constructor and
        // setUserDetailsService() are @Deprecated — pass it to the constructor.
        // (This constructor does not exist before 6.5.)
        DaoAuthenticationProvider provider =
            new DaoAuthenticationProvider(userDetailsService);
        provider.setPasswordEncoder(passwordEncoder);
        return provider;
    }

    // AuthenticationManager bean
    @Bean
    public AuthenticationManager authenticationManager(
            AuthenticationConfiguration config) throws Exception {
        return config.getAuthenticationManager();
    }
}
```

```java
// Using AuthenticationManager in a login controller
@RestController
@RequestMapping("/auth")
public class AuthController {

    @Autowired
    private AuthenticationManager authenticationManager;

    @Autowired
    private JwtUtil jwtUtil;

    @PostMapping("/login")
    public ResponseEntity<Map<String, String>> login(
            @RequestBody LoginRequest request) {
        // AuthenticationManager delegates to AuthenticationProvider
        Authentication authentication = authenticationManager.authenticate(
            new UsernamePasswordAuthenticationToken(
                request.getUsername(), request.getPassword()));

        // If we reach here, authentication was successful
        String token = jwtUtil.generateToken(authentication.getName());
        return ResponseEntity.ok(Map.of("token", token));
    }
}
```

📋 **How multiple providers work:**

| Step | What Happens |
|------|-------------|
| 1 | `ProviderManager` iterates through registered `AuthenticationProvider` list |
| 2 | For each provider, calls `supports()` to check if it can handle the authentication type |
| 3 | If supported, calls `authenticate()` on that provider |
| 4 | If authentication succeeds, returns the authenticated `Authentication` object |
| 5 | If the provider throws a plain `AuthenticationException`, the exception is remembered and the **next** provider is tried |
| 6 | If the provider throws `AccountStatusException` (locked / disabled / expired) or `InternalAuthenticationServiceException`, `ProviderManager` **rethrows immediately and stops iterating** |
| 7 | If no child provider returned a result, the optional **`parent` `AuthenticationManager`** is consulted |
| 8 | If everything fails, the last `AuthenticationException` is rethrown (or `ProviderNotFoundException` if no provider even supported the token) |

⚠️ **Why step 6 matters:** suppose a locked account just moved on to the next provider. Then a *later* provider could silently authenticate it. The account-status veto (the "no" from the locked check) would have no effect. This is the standard follow-up to "how do multiple providers work."

⚠️ **Common Exception — the one most candidates get wrong:** `DaoAuthenticationProvider` throws **`BadCredentialsException` in *both* cases**: wrong password **and** unknown username.
- `AbstractUserDetailsAuthenticationProvider.hideUserNotFoundExceptions` defaults to **`true`**.
- So Spring catches a `UsernameNotFoundException` from your `UserDetailsService` and rethrows it as `BadCredentialsException`.
- Your failure handler or `AuthenticationEntryPoint` sees `UsernameNotFoundException` only if you call `setHideUserNotFoundExceptions(false)`.

🔒 **The reason is username-enumeration prevention** (stopping an attacker from finding out which usernames exist). Spring does more than change the exception type:
- When the user is not found, `DaoAuthenticationProvider` still runs `mitigateAgainstTimingAttack(...)`.
- This is a dummy `passwordEncoder.matches(presentedPassword, userNotFoundEncodedPassword)` against a pre-computed hash.
- So the **response timing** also does not show whether the account exists.

Never "helpfully" split the message into "user not found" vs "wrong password". That gives an attacker a free way to check which accounts exist.

🎯 **Interview Tip:** Point out the **delegation pattern**. `AuthenticationManager` does not perform authentication itself; it delegates to `AuthenticationProvider`. This lets one application support multiple authentication mechanisms (database, LDAP, OAuth).

---

</details>

---

5. **🏷️ Compare @PreAuthorize, @PostAuthorize, @Secured, and @RolesAllowed annotations. ⚡**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

Spring Security gives several annotations for method-level security. Each one has different features and use cases.

| Feature | `@PreAuthorize` | `@PostAuthorize` | `@Secured` | `@RolesAllowed` |
|---------|----------------|------------------|-----------|-----------------|
| **SpEL Support** | ✅ Full SpEL expressions | ✅ Full SpEL expressions | ❌️ No | ❌️ No |
| **When Checked** | Before method execution | After method execution | Before method execution | Before method execution |
| **Access Return Value** | ❌️ No | ✅ Yes (`returnObject`) | ❌️ No | ❌️ No |
| **Access Parameters** | ✅ Yes (`#paramName`) | ✅ Yes | ❌️ No | ❌️ No |
| **Role Prefix** | Configurable | Configurable | Requires `ROLE_` prefix | Depends on implementation |
| **Specification** | Spring-specific | Spring-specific | Spring-specific | JSR-250 standard |
| **Enable Annotation** | `@EnableMethodSecurity` | `@EnableMethodSecurity` | `@EnableMethodSecurity(securedEnabled = true)` | `@EnableMethodSecurity(jsr250Enabled = true)` |

```java
// Enable all method security annotations
@Configuration
@EnableMethodSecurity(
    prePostEnabled = true,    // @PreAuthorize, @PostAuthorize (default: true)
    securedEnabled = true,    // @Secured
    jsr250Enabled = true      // @RolesAllowed
)
public class MethodSecurityConfig {}
```

1️⃣ **`@PreAuthorize`** — The most powerful one. Spring checks it BEFORE the method runs:

```java
// Role check
@PreAuthorize("hasRole('ADMIN')")
public void deleteUser(Long userId) { /* ... */ }

// Multiple roles
@PreAuthorize("hasAnyRole('ADMIN', 'MANAGER')")
public List<Employee> getAllEmployees() { /* ... */ }

// Access method parameters using SpEL
// (principal.id / principal.department need a custom UserDetails class with these fields)
// @P is Spring Security's name hint; Spring Data's @Param also works
@PreAuthorize("#userId == authentication.principal.id or hasRole('ADMIN')")
public User getUser(@P("userId") Long userId) { /* ... */ }

// Complex expression
@PreAuthorize("hasRole('MANAGER') and #department == authentication.principal.department")
public void approveBudget(String department, BigDecimal amount) { /* ... */ }
```

2️⃣ **`@PostAuthorize`** — Spring checks it AFTER the method runs. It can read the return value:

```java
// Only return the order if it belongs to the authenticated user
@PostAuthorize("returnObject.createdBy == authentication.name")
public Order getOrder(Long orderId) {
    return orderRepository.findById(orderId).orElseThrow();
}

// Admin can see any result, others only their own
@PostAuthorize("hasRole('ADMIN') or returnObject.owner == authentication.name")
public Document getDocument(Long docId) {
    return documentRepository.findById(docId).orElseThrow();
}
```

3️⃣ **`@Secured`** — A simple role check. No SpEL:

```java
@Secured("ROLE_ADMIN")
public void adminOnlyAction() { /* ... */ }

@Secured({"ROLE_ADMIN", "ROLE_MANAGER"})
public void managerOrAdminAction() { /* ... */ }
```

4️⃣ **`@RolesAllowed`** — The JSR-250 standard. It works across frameworks:

```java
@RolesAllowed("ADMIN")
public void adminAction() { /* ... */ }

@RolesAllowed({"ADMIN", "MANAGER"})
public void sharedAction() { /* ... */ }
```

💡 **Pro Tip:**

- Use `@PreAuthorize` as your default choice. It can express the most rules, and it covers most use cases.
- Use `@PostAuthorize` only when the access check depends on the return value (e.g., "user can only see their own orders").
- Avoid `@Secured` and `@RolesAllowed` in new projects, unless you need JSR-250 portability (the same code works on other frameworks).

⚠️ **Caution with @PostAuthorize:** The method **still executes** even if authorization fails. So any side effects (database writes, external API calls) have already happened. Use `@PostAuthorize` only on read-only methods.

---

</details>

---

6. **🔀 What is the difference between method-level security and URL-level security? ⚡**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

Spring Security gives two ways to enforce authorization. They work together:

- **URL-level security** — you configure it in `SecurityFilterChain`.
- **method-level security** — you configure it with annotations on service/controller methods.

| Feature | URL-Level Security 🅰️ | Method-Level Security 🅱️ |
|---------|----------------------|-------------------------|
| **Configuration** | `SecurityFilterChain` bean | `@PreAuthorize`, `@Secured`, etc. |
| **Where Applied** | HTTP request path matching | Java method invocation |
| **Granularity** | URL pattern-based | Method-level, parameter-aware |
| **SpEL Support** | Limited (via `access()`) | ✅ Full SpEL in `@PreAuthorize` |
| **Access to Method Params** | ❌️ No | ✅ Yes (`#paramName`) |
| **Works with Non-Web** | ❌️ Only HTTP requests | ✅ Works with any method call |
| **Layer** | Web/filter layer | Service/business layer |
| **Multiple Rules per Endpoint** | ⚠️ First match wins | ✅ Combine rules with `and` / `or` in one SpEL expression |

🌐 **URL-Level Security Example:**

```java
@Bean
SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    return http
        .authorizeHttpRequests(auth -> auth
            .requestMatchers("/public/**", "/auth/**").permitAll()
            .requestMatchers("/admin/**").hasRole("ADMIN")
            .requestMatchers(HttpMethod.DELETE, "/api/**").hasRole("ADMIN")
            .requestMatchers("/api/**").authenticated()
            .anyRequest().authenticated()
        )
        .build();
}
```

🔐 **Method-Level Security Example:**

```java
@Service
public class OrderService {

    @PreAuthorize("hasRole('USER')")
    public Order createOrder(OrderRequest request) { /* ... */ }

    // a bean checks that the order belongs to the current user
    @PreAuthorize("@orderSecurity.isOwner(#orderId, authentication) or hasRole('ADMIN')")
    public Order getOrder(Long orderId) { /* ... */ }

    @PreAuthorize("hasRole('ADMIN')")
    public void cancelOrder(Long orderId) { /* ... */ }
}
```

🧠 **In Simple Words:**

- **URL-level** is like security guards at the building entrance. They check your badge based on which floor (URL) you want to go to.
- **Method-level** is like security cameras inside each room. They check your authorization for each specific action.

🔑 **Key Point:** In production applications, use **both** together for defense in depth (more than one layer of security checks):

1. URL-level security is the **first layer**. It blocks unauthorized requests early in the filter chain.
2. Method-level security is the **second layer**. It enforces fine-grained authorization at the business logic layer.

🎯 **Interview Tip:** When asked which one to use, always mention "defense in depth". The best practice is to apply both layers:

- URL-level catches broad access violations early.
- Method-level handles authorization rules from the business logic. URL patterns cannot express these rules.

---

</details>

---

7. **🔧 How do you implement a custom AuthenticationProvider in Spring Security? ⚡**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

You write a custom `AuthenticationProvider` when the built-in `DaoAuthenticationProvider` does not meet your authentication needs. For example:

- authenticating against an external API
- LDAP with custom logic
- multi-factor authentication
- a legacy system

✅ **Preferred: extend `DaoAuthenticationProvider`** and override `additionalAuthenticationChecks`. You keep the two protections that the framework already gives you:

- `hideUserNotFoundExceptions` — no user enumeration (finding out which usernames exist) through the exception type.
- `mitigateAgainstTimingAttack` — no user enumeration through response latency.

You only write the extra check.

```java
// Custom provider that adds an OTP check on top of the standard password check
@Component
public class OtpAwareAuthenticationProvider extends DaoAuthenticationProvider {

    private final OtpService otpService;

    public OtpAwareAuthenticationProvider(UserDetailsService userDetailsService,
                                          PasswordEncoder passwordEncoder,
                                          OtpService otpService) {
        super(userDetailsService);
        setPasswordEncoder(passwordEncoder);
        this.otpService = otpService;
    }

    @Override
    protected void additionalAuthenticationChecks(UserDetails userDetails,
                                                  UsernamePasswordAuthenticationToken authentication)
            throws AuthenticationException {
        // 1. Let the superclass do the password comparison
        //    (the timing mitigation already ran earlier, in retrieveUser)
        super.additionalAuthenticationChecks(userDetails, authentication);

        // 2. Then layer on the custom factor
        Object details = authentication.getDetails();
        String otp = (details instanceof OtpDetails od) ? od.otp() : null;
        if (!otpService.verify(userDetails.getUsername(), otp)) {
            throw new BadCredentialsException("Invalid OTP");
        }
    }
}
```

⚠️ **If you must implement `AuthenticationProvider` directly** — for example, authenticating against an external API with no local password at all — you must build both protections yourself:

```java
// Raw AuthenticationProvider — note the two guards marked ⚠️
@Component
public class ExternalApiAuthenticationProvider implements AuthenticationProvider {

    private final RemoteIdentityClient remoteClient;
    private final PasswordEncoder passwordEncoder;

    // Pre-computed dummy hash, used only to burn the same CPU time on a miss
    private final String dummyHash;

    public ExternalApiAuthenticationProvider(RemoteIdentityClient remoteClient,
                                             PasswordEncoder passwordEncoder) {
        this.remoteClient = remoteClient;
        this.passwordEncoder = passwordEncoder;
        this.dummyHash = passwordEncoder.encode("userNotFoundPassword");
    }

    @Override
    public Authentication authenticate(Authentication authentication)
            throws AuthenticationException {

        String username = authentication.getName();

        // ⚠️ Guard 1: credentials are null on a re-authentication of an already-authenticated
        // token — getCredentials().toString() would NPE here.
        Object credentials = authentication.getCredentials();
        if (credentials == null) {
            throw new BadCredentialsException("Bad credentials");
        }
        String password = credentials.toString();

        RemoteUser remoteUser = remoteClient.find(username);  // returns null if unknown

        if (remoteUser == null) {
            // ⚠️ Guard 2: still do the hash work so response timing does not leak
            // whether the username exists, then fail with the SAME generic message.
            passwordEncoder.matches(password, dummyHash);
            throw new BadCredentialsException("Bad credentials");
        }

        if (!passwordEncoder.matches(password, remoteUser.passwordHash())) {
            throw new BadCredentialsException("Bad credentials");
        }
        if (remoteUser.locked()) {
            throw new LockedException("Account is temporarily locked. Try after 15 minutes.");
        }

        UserDetails userDetails = remoteUser.toUserDetails();
        return new UsernamePasswordAuthenticationToken(
            userDetails, null, userDetails.getAuthorities());
    }

    @Override
    public boolean supports(Class<?> authenticationType) {
        return UsernamePasswordAuthenticationToken.class
                .isAssignableFrom(authenticationType);
    }
}
```

```java
// Register the custom provider in SecurityConfig
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    private final OtpAwareAuthenticationProvider otpAwareAuthenticationProvider;

    public SecurityConfig(OtpAwareAuthenticationProvider otpAwareAuthenticationProvider) {
        this.otpAwareAuthenticationProvider = otpAwareAuthenticationProvider;
    }

    @Bean
    public AuthenticationManager authenticationManager(
            AuthenticationConfiguration config) throws Exception {
        return config.getAuthenticationManager();
    }

    @Bean
    SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        return http
            .authenticationProvider(otpAwareAuthenticationProvider)
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/auth/**").permitAll()
                .anyRequest().authenticated()
            )
            .build();
    }
}
```

⚠️ **Watch the global `AuthenticationManager`.** The `authenticationManager` bean above comes from `AuthenticationConfiguration`.
- Spring adds an `AuthenticationProvider` bean to it only when there is **exactly one** such bean. With both `@Component` providers above, it adds neither.
- It then builds a plain `DaoAuthenticationProvider` from your `UserDetailsService` bean.
- So a login controller that injects this bean checks the password but **skips the OTP**.
- `.authenticationProvider(...)` on `http` changes only that chain's own manager.

📋 **Common use cases for custom AuthenticationProvider:**

| Use Case | Why Custom Provider |
|----------|-------------------|
| 🔐 Multi-factor authentication (OTP) | Check password + OTP in same flow |
| 🌐 External API authentication | Validate credentials against remote service |
| 📁 LDAP with custom mappings | Custom role extraction from LDAP attributes |
| 🚫 Rate limiting / account lockout | Block after N failed attempts |
| 🔑 API key authentication | Authenticate using API keys instead of username/password |
| 🏢 Legacy system integration | Authenticate against mainframe or SOAP service |

⚠️ **Important:** The `supports()` method decides which type of `Authentication` token your provider can handle. If it returns `false`, the `ProviderManager` skips your provider. It then tries the next one in the chain.

🎯 **Interview Tip:** Mention that you can register **multiple** `AuthenticationProvider` beans, one for each authentication mechanism. For example: one for database auth, one for LDAP, one for API keys. The `ProviderManager` tries them one by one until one succeeds.

---

</details>

---

<a id="jwt-deep-dive"></a>

## 3. JWT Deep Dive

1. **📜 What is JWT? Explain its structure: Header, Payload, and Signature. 🔥🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

JWT (JSON Web Token) is an open standard (RFC 7519). It sends information securely between parties as a compact, URL-safe JSON object. It is commonly used for **stateless authentication** in REST APIs and microservices.

A JWT has **three Base64URL-encoded parts**, separated by dots:

```
header.payload.signature
```

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwicm9sZXMiOlsiQURNSU4iXSwiaWF0IjoxNTE2MjM5MDIyLCJleHAiOjE1MTYyNDI2MjJ9.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
|___________________________|___________________________________________________________________________________________|___________________________________|
         HEADER                                              PAYLOAD                                                           SIGNATURE
```

```mermaid
graph LR
    subgraph JWT["JWT Token Structure"]
        H["Header<br/>Algorithm + Type"]
        P["Payload<br/>Claims (data)"]
        S["Signature<br/>Integrity check"]
    end

    H -->|"."| P -->|"."| S
    H --> HE["Base64URL(Header)"]
    P --> PE["Base64URL(Payload)"]
    S --> SE["HMAC-SHA256(<br/>base64Header + '.' + base64Payload,<br/>secretKey)"]

    classDef purple fill:#7C3AED,stroke:#7C3AED,color:#fff
    classDef cyan fill:#0891B2,stroke:#0891B2,color:#fff
    classDef green fill:#059669,stroke:#059669,color:#fff
    classDef orange fill:#D97706,stroke:#D97706,color:#fff

    class H purple
    class P cyan
    class S green
    class HE purple
    class PE cyan
    class SE orange
```

<img src="./img/security_jwt_token_structure.png" alt="JWT Structure — Header.Payload.Signature" style="max-width:100%;"/>

1️⃣ **Header** — Contains metadata about the token:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

- `alg` — The signing algorithm (e.g., `HS256`, `RS256`).
- `typ` — The token type. It is optional. It is usually `JWT` (OAuth2 access tokens may use `at+jwt`).

2️⃣ **Payload** — Contains **claims** (data). Three types of claims:

```json
{
  "sub": "john.doe",
  "iss": "myapp.com",
  "iat": 1711234567,
  "exp": 1711238167,
  "roles": ["ADMIN", "USER"],
  "department": "Engineering"
}
```

| Claim Type | Description | Examples |
|-----------|-------------|----------|
| **Registered** | Predefined by JWT spec (recommended but not mandatory) | `sub` (subject), `iss` (issuer), `exp` (expiration), `iat` (issued at), `jti` (JWT ID) |
| **Public** | Defined in IANA JSON Web Token Registry or collision-resistant namespace | `email`, `name`, `picture` |
| **Private** | Custom claims agreed between parties | `roles`, `department`, `userId` |

3️⃣ **Signature** — Proves that nobody has changed (tampered with) the token:

```
HMACSHA256(
  base64UrlEncode(header) + "." + base64UrlEncode(payload),
  secret
)
```

- The server signs the header and payload with a **secret key** (symmetric) or **private key** (asymmetric).
- When validating, the server recomputes the signature and compares it with the one in the token.
- If any part of the header or payload was changed, the signatures will not match. The server rejects the token.

⚠️ **Critical:** JWT payload is **Base64URL-encoded, NOT encrypted**. Anyone can decode and read the payload. Never put sensitive data (passwords, credit card numbers) in the payload. The signature only ensures **integrity** (nobody changed the data). It does not give **confidentiality** (the data is hidden).

💡 **Pro Tip:** Use [jwt.io](https://jwt.io) to decode and inspect JWT tokens during development. It is a very useful debugging tool.

**No key, no signature check, and none needed.** It reads the `exp` of a token the service already trusts. The only goal is to decide how long to cache it. This is a real example of the point above: anyone who has the token can read the payload as plain text. It is *also* a valid example of when unverified decoding is acceptable. You read metadata from your own third-party token. You **never** use it for an authorization decision.

---

</details>

---

2. **🔏 What is the difference between HS256 and RS256 signing algorithms? 🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

HS256 and RS256 are the two most commonly used JWT signing algorithms. They use very different cryptography.

🔹 **HS256 (HMAC with SHA-256)** — Symmetric algorithm:

- Uses a **single shared secret key** for both signing and verification.
- Both the token issuer and the token verifier must know the same secret.
- Faster and simpler. But you must share the secret securely.

🔸 **RS256 (RSA Signature with SHA-256)** — Asymmetric algorithm:

- Uses a **key pair**: a private key to sign and a public key to verify.
- Only the authorization server needs the private key; resource servers only need the public key.
- More secure for distributed systems because the private key never leaves the auth server.

| Feature | HS256 (Symmetric) 🅰️ | RS256 (Asymmetric) 🅱️ |
|---------|----------------------|----------------------|
| **Key Type** | Single shared secret | Private key + Public key pair |
| **Signing** | Secret key | Private key |
| **Verification** | Same secret key | Public key (different from signing key) |
| **Performance** | ⚡ Faster | ⚠️ Slower (RSA operations) |
| **Key Distribution** | ⚠️ Secret must be shared with all verifiers | ✅ Only public key shared (safe) |
| **Key Size** | Min 256 bits (32 bytes) | Min 2048 bits (RSA key pair) |
| **Use Case** | Single service, monolith | Microservices, multi-service, OAuth2 |
| **Risk** | ❌️ If secret leaks, anyone can forge tokens | ✅ Public key cannot forge tokens |
| **JJWT 0.12 Example** | `Jwts.SIG.HS256` | `Jwts.SIG.RS256` |

```java
// HS256 — Symmetric (shared secret). Note: SecretKey, not Key —
// signWith(K, SecureDigestAlgorithm<? super K, ?>) will not compile with a raw Key.
SecretKey hmacKey = Keys.hmacShaKeyFor(
    secretString.getBytes(StandardCharsets.UTF_8));

String hsToken = Jwts.builder()
    .subject(username)
    .signWith(hmacKey, Jwts.SIG.HS256)
    .compact();

// RS256 — Asymmetric (key pair)
KeyPair keyPair = Jwts.SIG.RS256.keyPair().build();
PrivateKey privateKey = keyPair.getPrivate();
PublicKey publicKey = keyPair.getPublic();

// Auth server signs with private key
String rsToken = Jwts.builder()
    .subject(username)
    .signWith(privateKey, Jwts.SIG.RS256)
    .compact();

// Resource server verifies with public key
Claims claims = Jwts.parser()
    .verifyWith(publicKey)      // Only needs public key
    .build()
    .parseSignedClaims(rsToken)
    .getPayload();
```

⚠️ **API version:** the code above uses the **JJWT 0.12+** API. You may write `Jwts.parserBuilder()`, `setSigningKey()`, `parseClaimsJws()`, `getBody()` or `SignatureAlgorithm.HS256` on a whiteboard. Then you are writing the 0.11.x API. It was deprecated in **0.12.0 (Oct 2023)**. The mapping is: `setSubject`→`subject`, `setIssuer`→`issuer`, `setIssuedAt`→`issuedAt`, `setExpiration`→`expiration`, `SignatureAlgorithm.X`→`Jwts.SIG.X`, `parserBuilder()`→`parser()`, `setSigningKey(k)`→`verifyWith(k)`, `parseClaimsJws`→`parseSignedClaims`, `getBody()`→`getPayload()`, `Keys.keyPairFor(RS256)`→`Jwts.SIG.RS256.keyPair().build()`.

<details>
<summary><strong>🤔 Doubt: What are the `alg: none` and RS256→HS256 algorithm-confusion attacks, and how do you stop them?</strong></summary>

These are *the* two JWT security questions. Both come from the same mistake: **the token's own header chooses how the token is verified.**

1️⃣ **`alg: none` (the unsecured JWT).** The attacker does this:

- takes a valid token and edits the payload (`"role":"ADMIN"`)
- sets the header to `{"alg":"none"}`
- **strips the signature**, leaving a trailing dot.

A badly written (naive) parser reads `alg` from the header and sees "no algorithm". It decides there is "nothing to verify" and accepts the token.

2️⃣ **RS256 → HS256 algorithm confusion.** The server is configured for **RS256**. It holds the RSA **public** key for verification. The attacker then:

- changes the header to `{"alg":"HS256"}`
- HMAC-signs the tampered token, using **the RSA public key bytes as the HMAC secret**.

Suppose the verification code does "look up my key, hand it to the algorithm named in the header". Then the server computes the HMAC with a value the attacker also has. A public key is, by definition, public. So the signature matches.

🛡️ **The single fix for both:** never let the header pick the algorithm. **Pin the expected algorithm and key type on the server side.**

- In JJWT 0.12, `verifyWith(SecretKey)` / `verifyWith(PublicKey)` fixes the **key type**. So an attacker cannot force an RS256-configured parser into HMAC verification.
- `parseSignedClaims()` requires a **JWS** (a signed JWT). An `alg: none` token is an *unsecured JWT*, not a JWS. So the parser rejects it with `UnsupportedJwtException`. The parse method itself is the guard.
- `Jwts.parser().sig()` returns a mutable collection of supported algorithms. Use `.remove(...)` to drop algorithms your application never issues. ⚠️ Note: `.add(...)` *registers* an implementation. It does not narrow the allowed set. Only removal narrows it.
- With OAuth2 Resource Server, `jwk-set-uri` + the `kid` header selects the key. Spring's `NimbusJwtDecoder` is built for a specific algorithm. It is the same principle, and Spring does it for you.

💡 **One-liner for the interview:** "The `alg` header is attacker-controlled input. It tells you what the *sender* claims they did; it must never decide what the *receiver* does."

---

</details>
<br/>

🧠 **In Simple Words:**

- **HS256** is like a shared password — both the sender and receiver must know the same password.
- **RS256** is like a wax seal on a letter. Only the sender has the seal (private key). But anyone can check that the seal is real (public key).

🔑 **Key Point:** In a microservices architecture with a separate **Authorization Server**, always use **RS256**. The auth server signs tokens with its private key. Each microservice (resource server) verifies tokens with the public key. So even if an attacker breaks into a microservice, the attacker cannot forge new tokens.

🎯 **Interview Tip:** You may be asked "Which algorithm would you choose?". Say RS256 for microservices and distributed systems, because you can share the verification key safely. Say HS256 only for simple single-service apps, where the secret can stay safe on one server.

---

</details>

---

3. **⏱️ Explain the JWT token lifecycle: creation, validation, and expiration. 🔥🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

The JWT lifecycle has three steps. The server creates a token, checks it on each request, and at the end the token expires. You must understand this lifecycle to build secure authentication.

```mermaid
sequenceDiagram
    participant C as Client
    participant AS as Auth Server
    participant RS as Resource Server
    participant DB as Database

    rect rgb(40, 70, 40)
        Note over C,DB: Phase 1 — Token Creation
        C->>AS: POST /auth/login (username + password)
        AS->>DB: Validate credentials
        DB-->>AS: User found + password matches
        AS->>AS: Build JWT (header + payload + sign)
        AS-->>C: 200 OK { accessToken, refreshToken }
    end

    rect rgb(0, 60, 80)
        Note over C,RS: Phase 2 — Token Usage & Validation
        C->>RS: GET /api/orders (Authorization: Bearer <JWT>)
        RS->>RS: Extract token from header
        RS->>RS: Verify signature (using secret/public key)
        RS->>RS: Check expiration (exp claim)
        RS->>RS: Extract claims (sub, roles)
        RS->>RS: Set SecurityContext
        RS-->>C: 200 OK { orders data }
    end

    rect rgb(80, 40, 40)
        Note over C,AS: Phase 3 — Token Expired
        C->>RS: GET /api/orders (Authorization: Bearer <expired JWT>)
        RS->>RS: Verify signature OK
        RS->>RS: Check expiration FAILED
        RS-->>C: 401 Unauthorized (token expired)
        C->>AS: POST /auth/refresh (refreshToken)
        AS->>AS: Validate refresh token
        AS-->>C: 200 OK { new accessToken }
    end
```

<img src="./img/security_jwt_auth_flow_lifecycle.png" alt="JWT Authentication Flow (Login → Token → Validate → Authorize)" style="max-width:100%;"/>

**Phase 1 — Token Creation:**

```java
@Component
public class JwtUtil {

    @Value("${app.jwt.secret}")
    private String secret;

    @Value("${app.jwt.access-token-expiry-ms}")
    private long accessTokenExpiryMs;  // e.g., 900000 (15 minutes)

    private SecretKey key;   // SecretKey, not Key — required by signWith/verifyWith

    @PostConstruct
    public void init() {
        // Always pin the charset — the platform default would yield a different
        // key for the same secret on a different-locale JVM.
        this.key = Keys.hmacShaKeyFor(secret.getBytes(StandardCharsets.UTF_8));
    }

    public String generateToken(String username, List<String> roles) {
        Instant now = Instant.now();
        return Jwts.builder()
                .subject(username)                                       // Who
                .issuer("myapp.com")                                     // Issuer
                .id(UUID.randomUUID().toString())                        // jti — for blacklisting
                .issuedAt(Date.from(now))                                // iat — when created
                .notBefore(Date.from(now))                               // nbf — not valid before
                .expiration(Date.from(
                    now.plusMillis(accessTokenExpiryMs)))                // exp — when expires
                .claim("roles", roles)                                   // Custom claims
                .signWith(key, Jwts.SIG.HS256)                           // Sign
                .compact();                                              // Build string
    }
}
```

**Phase 2 — Token Validation:**

```java
public boolean validateToken(String token) {
    try {
        Claims claims = Jwts.parser()
                .verifyWith(key)            // pins the key AND the key type
                .requireIssuer("myapp.com") // reject tokens minted by anyone else
                .clockSkewSeconds(30)       // tolerate small clock drift between nodes
                .build()
                .parseSignedClaims(token)   // signature + exp + nbf, all in one call
                .getPayload();
        return true;
    } catch (ExpiredJwtException e) {
        log.warn("Token expired: {}", e.getMessage());
    } catch (MalformedJwtException e) {
        log.warn("Invalid token format: {}", e.getMessage());
    } catch (SignatureException e) {          // io.jsonwebtoken.security.SignatureException
        log.warn("Invalid signature: {}", e.getMessage());
    } catch (UnsupportedJwtException e) {
        log.warn("Unsupported token: {}", e.getMessage());
    } catch (JwtException | IllegalArgumentException e) {  // nbf, requireIssuer, null/empty token
        log.warn("Invalid token: {}", e.getMessage());
    }
    return false;
}
```

📋 **JJWT exceptions and their meanings:**

| Exception | Cause |
|-----------|-------|
| `ExpiredJwtException` | Token's `exp` claim is in the past |
| `PrematureJwtException` | Token's `nbf` (not-before) claim is in the future |
| `MalformedJwtException` | Token string is not a valid JWT format |
| `io.jsonwebtoken.security.SignatureException` | Signature verification failed (tampered token) |
| `UnsupportedJwtException` | Not a signed Claims JWS — e.g. an unsecured `alg: none` token, or a content JWS |
| `IncorrectClaimException` / `MissingClaimException` | A `require*(...)` assertion such as `requireIssuer` / `requireAudience` failed |
| `IllegalArgumentException` | Token is null or empty |

📋 **The time claims — know all three:**

| Claim | Meaning | Who validates it |
|-------|---------|------------------|
| `iat` (issued at) | When the token was minted | **Not** auto-enforced — use it yourself for "re-auth for sensitive actions" or max-token-age policies |
| `nbf` (not before) | Token is invalid until this instant | Auto-enforced by JJWT → `PrematureJwtException` |
| `exp` (expiration) | Token is invalid from this instant | Auto-enforced by JJWT → `ExpiredJwtException` |

🔑 **Key Point:** `parseSignedClaims()` does signature verification **and** the `exp` / `nbf` checks in one call. You do not need a separate expiry check. If the token is expired, it throws `ExpiredJwtException` before you ever get the claims back.

`exp` and `nbf` are absolute instants. So in a distributed system, allow a small `clockSkewSeconds(...)` tolerance. Otherwise a node whose clock is 2 seconds fast will reject tokens that were just issued.

⚠️ **What is *not* validated for you:** `aud` (audience) and `iss` (issuer) are checked only if you ask, via `requireAudience(...)` / `requireIssuer(...)`. If you skip `aud`, service B will accept a token made for service A, with no error. This is a real way to gain extra rights (privilege escalation) when many microservices share one auth server.

💡 **Pro Tip:** Keep access tokens **short-lived** (5-15 minutes) and refresh tokens **longer-lived** (7-30 days). If someone steals an access token, it works only for a short time. Silent refresh (getting a new access token in the background) keeps the user experience smooth.

---

</details>

---

4. **🔄 What is the Access Token vs Refresh Token pattern? Why is it needed? 🔥🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

The Access Token / Refresh Token pattern is a security strategy. It balances two goals: **security** (short-lived access) and **user experience** (no frequent re-login).

🔹 **Access Token:**

- 🕐 Short-lived (5-15 minutes typically).
- 📤 Sent with every API request in the `Authorization` header.
- 🎯 Contains user claims (username, roles).
- ⚡ Stateless validation — no database lookup needed.

🔸 **Refresh Token:**

- 🕐 Long-lived (7-30 days typically).
- 🗄️ Stored securely (HttpOnly cookie or secure storage).
- 🔄 Used **only** to get a new access token when the current one expires.
- 🔒 Store it in the database, so that you can revoke it.

```mermaid
sequenceDiagram
    participant C as Client
    participant AS as Auth Server
    participant RS as Resource Server
    participant DB as Token Store

    C->>AS: POST /auth/login (credentials)
    AS->>AS: Validate credentials
    AS->>DB: Store refresh token
    AS-->>C: { accessToken (15min), refreshToken (30days) }

    Note over C: Access Token valid
    C->>RS: GET /api/data + Bearer accessToken
    RS-->>C: 200 OK { data }

    Note over C: Access Token EXPIRED
    C->>RS: GET /api/data + Bearer expiredToken
    RS-->>C: 401 Unauthorized

    Note over C: Use Refresh Token to get new Access Token
    C->>AS: POST /auth/refresh { refreshToken }
    AS->>DB: Validate refresh token exists & not revoked
    DB-->>AS: Valid
    AS->>AS: Generate new access token
    AS-->>C: { new accessToken (15min) }

    Note over C: Continue with new Access Token
    C->>RS: GET /api/data + Bearer newAccessToken
    RS-->>C: 200 OK { data }

    Note over C: User logs out
    C->>AS: POST /auth/logout { refreshToken }
    AS->>DB: Delete/revoke refresh token
    AS-->>C: 200 OK
```

```java
// Refresh token entity stored in database.
// ⚠️ Store a HASH, never the raw token — see the note below the code.
@Entity
@Table(name = "refresh_tokens")
@Data
public class RefreshToken {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "token_hash", nullable = false, unique = true)
    private String tokenHash;   // SHA-256 of the token handed to the client

    @Column(nullable = false)
    private String username;

    @Column(nullable = false)
    private Instant expiryDate;

    private boolean revoked = false;
}
```

🔒 **Hash refresh tokens at rest, exactly like passwords.** A refresh token is a long-lived bearer credential (whoever holds it can use it). Suppose the table stores the raw value. Then even a read-only leak gives the attacker every live session. Examples of such a leak:

- a SQL-injection `SELECT`
- a stolen backup
- a support query that reads too much.

And unlike a password, the user cannot "change" it. Store `SHA-256(token)` and look up by hash.

(A fast hash is correct here, unlike for passwords. The token is 128+ bits of `SecureRandom` entropy, so there is nothing to brute-force. And you do not want a BCrypt round on every refresh.)

```java
// Refresh token service
@Service
public class RefreshTokenService {

    @Autowired
    private RefreshTokenRepository refreshTokenRepository;

    @Value("${app.jwt.refresh-token-expiry-ms}")
    private long refreshTokenExpiryMs;

    // Returns the RAW token to hand to the client; only the hash is persisted.
    public String createRefreshToken(String username) {
        byte[] raw = new byte[32];
        new SecureRandom().nextBytes(raw);
        String token = Base64.getUrlEncoder().withoutPadding().encodeToString(raw);

        RefreshToken entity = new RefreshToken();
        entity.setUsername(username);
        entity.setTokenHash(sha256(token));
        entity.setExpiryDate(Instant.now().plusMillis(refreshTokenExpiryMs));
        refreshTokenRepository.save(entity);
        return token;
    }

    public RefreshToken verifyRefreshToken(String token) {
        RefreshToken refreshToken = refreshTokenRepository
            .findByTokenHash(sha256(token))
            .orElseThrow(() -> new InvalidRefreshTokenException("Refresh token not found"));

        if (refreshToken.isRevoked()) {
            throw new InvalidRefreshTokenException("Refresh token has been revoked");
        }
        if (refreshToken.getExpiryDate().isBefore(Instant.now())) {
            refreshTokenRepository.delete(refreshToken);
            throw new InvalidRefreshTokenException("Refresh token expired. Please login again.");
        }
        return refreshToken;
    }

    public void revokeRefreshToken(String token) {
        refreshTokenRepository.findByTokenHash(sha256(token))
            .ifPresent(rt -> {
                rt.setRevoked(true);
                refreshTokenRepository.save(rt);
            });
    }

    private String sha256(String value) {
        try {
            byte[] digest = MessageDigest.getInstance("SHA-256")
                .digest(value.getBytes(StandardCharsets.UTF_8));
            return HexFormat.of().formatHex(digest);
        } catch (NoSuchAlgorithmException e) {
            throw new IllegalStateException("SHA-256 not available", e);
        }
    }
}
```

```java
// A typed exception, so the failure surfaces as 401 — not a 500.
public class InvalidRefreshTokenException extends AuthenticationException {
    public InvalidRefreshTokenException(String message) {
        super(message);
    }
}
```

⚠️ **Never `throw new RuntimeException("...")` here.** A raw `RuntimeException` reaches the default error handler as **500 Internal Server Error**. That tells the client "our server broke". The truth is "your credential is no longer valid".

Extend `AuthenticationException` instead (or map a domain exception in `@ControllerAdvice`). Then the same `AuthenticationEntryPoint` that handles every other auth failure returns a clean **401**. The client's silent-refresh logic then knows to send the user back to login.

```java
// Auth controller with refresh endpoint
@RestController
@RequestMapping("/auth")
public class AuthController {

    @PostMapping("/refresh")
    public ResponseEntity<Map<String, String>> refreshToken(
            @RequestBody Map<String, String> request) {
        String refreshToken = request.get("refreshToken");

        RefreshToken verified = refreshTokenService.verifyRefreshToken(refreshToken);
        String newAccessToken = jwtUtil.generateToken(
            verified.getUsername(), getUserRoles(verified.getUsername()));

        return ResponseEntity.ok(Map.of("accessToken", newAccessToken));
    }

    @PostMapping("/logout")
    public ResponseEntity<String> logout(@RequestBody Map<String, String> request) {
        refreshTokenService.revokeRefreshToken(request.get("refreshToken"));
        return ResponseEntity.ok("Logged out successfully");
    }
}
```

📝 **Why is this pattern needed?**

| Problem with Only Access Tokens | Solution with Refresh Tokens |
|---------------------------------|------------------------------|
| Long-lived tokens = large attack window | Short-lived access tokens minimize risk |
| Short-lived tokens = frequent re-login | Refresh tokens silently renew access tokens |
| Cannot revoke stateless JWT | Refresh tokens stored in DB can be revoked |
| Token theft gives prolonged access | Stolen access token expires quickly (15 min) |

🔑 **Key Point:** The refresh token acts as a **revocation mechanism** for stateless JWTs. You cannot invalidate an access token once it is issued (it is stateless). So you make it short-lived. The refresh token is stored in the database, so you can revoke it at any time (on logout, password change, suspicious activity).

🎯 **Interview Tip:** Always explain **Refresh Token Rotation**. When a refresh token is used, issue a new refresh token and invalidate the old one. If an attacker reuses the old refresh token, you know the token was compromised. Then you can revoke the entire family of tokens.

<details>
<summary><strong>🤔 Doubt: Where should the client store the token — localStorage or an HttpOnly cookie?</strong></summary>

This is *the* standard practical follow-up question after any JWT answer. The honest answer: **every option has a cost. You are choosing which type of attack to accept.**

| | `localStorage` / `sessionStorage` | `HttpOnly; Secure; SameSite` cookie |
|---|---|---|
| **XSS** | ❌️ Any injected script reads it with one line (`localStorage.getItem('token')`) and exfiltrates it | ✅ JavaScript cannot read an `HttpOnly` cookie at all |
| **CSRF** | ✅ Immune — the browser never attaches it automatically; JS must set the header | ❌️ Re-exposed — the browser attaches cookies automatically. `SameSite` blocks most cross-site cases, but not requests from a sibling subdomain (same site) |
| **Sent how** | `Authorization: Bearer <token>`, set explicitly by your code | Automatically, on every request to the domain |
| **Must you enable CSRF protection?** | No | **Yes** — plus `SameSite=Strict` or `Lax` |

🔗 **This connects to §4 Q3.** "Disable CSRF for a JWT API" is safe only *because* the token travels in a header. The browser never attaches that header on its own. Now move the same token into a cookie. It becomes an ambient credential (the browser sends it automatically). And `csrf.disable()` becomes a real vulnerability. The storage choice and the CSRF setting are one decision, not two.

✅ **The practical production answer:**

- Keep the short-lived **access token in memory**. That means a JS variable, not `localStorage`. It is lost when the tab closes, and it is not readable from another origin's stored data.
- Keep the long-lived **refresh token in an `HttpOnly; Secure; SameSite=Strict` cookie**. Scope it to the `/auth/refresh` path, with CSRF protection on that one endpoint.

Then XSS cannot read the refresh token. A stolen access token can do damage for at most one TTL (the token's lifetime).

⚠️ **Do not claim "HttpOnly cookies make you XSS-proof."** They stop token *exfiltration* (stealing the token), not token *use*. Injected script can still call your API from the victim's browser, and the browser sends the cookie with it. `HttpOnly` limits the damage to the session's lifetime. Without it, the attacker can steal the token and use it from any machine.

---

</details>
<br/>

---

</details>

---

5. **🚫 What are the strategies for JWT token revocation? 🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

One of the biggest problems with JWT is that tokens are **stateless**. Once the server issues a token, it cannot invalidate it before it expires. Here are the common strategies to handle token revocation:

| Strategy | How It Works | Pros | Cons |
|----------|-------------|------|------|
| **Short-lived tokens + Refresh** | Access tokens expire in 5-15 min; use refresh tokens for renewal | ✅ Simple, minimal server state | ⚠️ Token valid until expiry (5-15 min window) |
| **Token blacklist** | Maintain a list of revoked token IDs (`jti`) in Redis/DB | ✅ Immediate revocation | ❌️ Requires storage (defeats stateless) |
| **Token versioning** | Store a `tokenVersion` per user in DB; reject tokens with old version | ✅ Simple to implement | ⚠️ DB lookup on each request |
| **Refresh token rotation** | Issue new refresh token on each refresh; revoke old ones | ✅ Detects token theft | ⚠️ Complex implementation |
| **Logout event broadcast** | Publish logout events via Kafka/Redis pub-sub to all services | ✅ Works in microservices | ⚠️ Eventual consistency |

1️⃣ **Token Blacklist (Redis-based):**

```java
@Service
public class TokenBlacklistService {

    @Autowired
    private StringRedisTemplate redisTemplate;

    public void blacklistToken(String jti, long expirationMs) {
        // Store the token ID in Redis with TTL matching token expiry
        redisTemplate.opsForValue().set(
            "blacklist:" + jti, "revoked",
            expirationMs, TimeUnit.MILLISECONDS);
    }

    public boolean isBlacklisted(String jti) {
        return Boolean.TRUE.equals(
            redisTemplate.hasKey("blacklist:" + jti));
    }
}
```

2️⃣ **Token Versioning (per-user):**

```java
// User entity with token version
@Entity
public class AppUser {
    @Id
    private Long id;
    private String username;
    private int tokenVersion = 0;  // Incremented on password change, logout, etc.
}

// Include tokenVersion in JWT claims
public String generateToken(String username, int tokenVersion) {
    return Jwts.builder()
        .subject(username)
        .claim("tokenVersion", tokenVersion)
        .expiration(Date.from(Instant.now().plusMillis(expiryMs)))
        .signWith(key, Jwts.SIG.HS256)
        .compact();
}

// Validate token version on each request
public boolean validateToken(String token) {
    Claims claims = getClaims(token);
    int tokenVersion = claims.get("tokenVersion", Integer.class);
    AppUser user = userRepository.findByUsername(claims.getSubject()).orElseThrow();
    return tokenVersion == user.getTokenVersion();
}
```

3️⃣ **Refresh Token Rotation:**

```java
@Transactional
public Map<String, String> rotateRefreshToken(String oldRefreshToken) {
    RefreshToken existing = refreshTokenRepository
        .findByTokenHash(sha256(oldRefreshToken))
        .orElseThrow(() -> new InvalidRefreshTokenException("Invalid refresh token"));

    if (existing.isRevoked()) {
        // Reuse of an already-rotated token — the only innocent explanation is a
        // race, the likely one is theft. Revoke the whole family and force re-login.
        refreshTokenRepository.revokeAllByUsername(existing.getUsername());
        throw new InvalidRefreshTokenException(
            "Refresh token reuse detected — all sessions revoked.");
    }

    // Revoke old refresh token
    existing.setRevoked(true);
    refreshTokenRepository.save(existing);

    // Issue new tokens
    String newAccessToken = jwtUtil.generateToken(
        existing.getUsername(), getRoles(existing.getUsername()));
    String newRefreshToken = createRefreshToken(existing.getUsername());  // raw value

    return Map.of(
        "accessToken", newAccessToken,
        "refreshToken", newRefreshToken
    );
}
```

🔑 **Why rotation detects theft:**

- Each refresh token is single-use. After one use, the server marks it revoked.
- So a revoked token usually comes back because two parties hold the same token: the real client and a thief.
- (A client race can also cause it, for example two tabs that refresh at once. Some servers allow a few seconds of grace for this.)
- You cannot tell which one is which. So you revoke the entire family and make both log in again.
- Without rotation, a stolen refresh token means "attacker has 30 days of access".
- With rotation, it means "attacker has access until the victim's next refresh, and then everyone gets logged out and you have an alert."

🧠 **In Simple Words:**

- **Short-lived tokens** = the problem ends by itself (but you wait 5-15 minutes).
- **Blacklist** = you actively mark tokens as "do not accept" (like canceling a check).
- **Token versioning** = you change the lock, so old keys no longer work.
- **Refresh rotation** = every time you use your key, you get a new key and the old one stops working.

🔑 **Key Point:** Most production systems use a **combination**:

- short-lived access tokens (5-15 min),
- refresh token rotation,
- a token blacklist in Redis for critical revocations (like password change or admin force-logout).

This gives the best balance of security and performance.

🎯 **Interview Tip:** When you discuss JWT revocation, always name the basic trade-off: "Pure JWTs are stateless and cannot be truly revoked. Every revocation strategy introduces some form of state. The goal is to minimize the state while maximizing security."

---

</details>

---

6. **🛠️ How do you implement a JWT authentication filter in Spring Security? 🔥🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

The JWT authentication filter is a custom `OncePerRequestFilter`. For every request, it:

1. extracts the JWT from the `Authorization` header,
2. validates it,
3. sets the authentication in the `SecurityContext`.

The key design decision is **where the authorities come from**. In a truly stateless design, they come from the **token's own claims**. That is the whole reason you sign the token. If you reload `UserDetails` from the database on every request, you add a DB round-trip per request. JWT is designed to avoid exactly this cost (see the ⚠️ note after the code).

```java
// NOTE: deliberately NOT annotated @Component — see the ⚠️ double-registration note below.
public class JwtAuthenticationFilter extends OncePerRequestFilter {

    private final JwtUtil jwtUtil;

    public JwtAuthenticationFilter(JwtUtil jwtUtil) {
        this.jwtUtil = jwtUtil;
    }

    @Override
    protected void doFilterInternal(HttpServletRequest request,
                                    HttpServletResponse response,
                                    FilterChain filterChain)
            throws ServletException, IOException {

        // Step 1: Extract token from Authorization header
        String authHeader = request.getHeader("Authorization");

        if (authHeader == null || !authHeader.startsWith("Bearer ")) {
            // No token present — continue to next filter (might be a public endpoint)
            filterChain.doFilter(request, response);
            return;
        }

        String token = authHeader.substring(7);  // Remove "Bearer " prefix

        try {
            // Step 2: Verify signature + exp/nbf, and get the claims back.
            //         A failure here throws — nothing below runs.
            Claims claims = jwtUtil.parseClaims(token);

            // Step 3: Only process if no authentication exists in context
            if (SecurityContextHolder.getContext().getAuthentication() == null) {

                // Step 4: Build the principal from the CLAIMS — no database call.
                //         The signature is what makes these claims trustworthy.
                List<SimpleGrantedAuthority> authorities =
                    ((List<?>) claims.getOrDefault("roles", List.of())).stream()
                        .map(String::valueOf)
                        .map(SimpleGrantedAuthority::new)
                        .toList();

                // Step 5: Create an ALREADY-authenticated token.
                //         The static factory (5.7+) is clearer than the
                //         3-arg constructor about which state you are building.
                UsernamePasswordAuthenticationToken authToken =
                    UsernamePasswordAuthenticationToken.authenticated(
                        claims.getSubject(),
                        null,  // credentials not needed after auth
                        authorities);

                authToken.setDetails(
                    new WebAuthenticationDetailsSource().buildDetails(request));

                // Step 6: Set authentication on a FRESH context — never mutate
                //         the one currently held (it may be a shared instance).
                SecurityContext context = SecurityContextHolder.createEmptyContext();
                context.setAuthentication(authToken);
                SecurityContextHolder.setContext(context);
            }
        } catch (ExpiredJwtException e) {
            logger.warn("JWT token expired: " + e.getMessage());
        } catch (JwtException | IllegalArgumentException e) {
            logger.warn("Invalid JWT token: " + e.getMessage());
        }

        // Step 7: Continue the filter chain
        filterChain.doFilter(request, response);
    }

    // Shared with the SecurityFilterChain's permitAll() rules — one source of truth.
    // PathPatternRequestMatcher (Spring Security 6.5+) replaces the now
    // @Deprecated(forRemoval = true) AntPathRequestMatcher.
    static final RequestMatcher PUBLIC_PATHS = new OrRequestMatcher(
        PathPatternRequestMatcher.withDefaults().matcher("/auth/**"),
        PathPatternRequestMatcher.withDefaults().matcher("/public/**"));

    @Override
    protected boolean shouldNotFilter(HttpServletRequest request) {
        // ⚠️ This is a SECURITY decision, not a performance tweak — see note below.
        return PUBLIC_PATHS.matches(request);
    }
}
```

⚠️ **`SecurityContextHolder.getContext().setAuthentication(...)` is the wrong pattern.**

- It changes whatever context object the holder has right now.
- Before any authentication has happened, that can be a shared default instance.
- The Spring Security 6 documentation clearly says: call `createEmptyContext()`, fill it, and then call `setContext(...)`.
- The code above does this. So does the `SecurityContextHolder` example in §2 Q2.

⚠️ **`shouldNotFilter` is a second, independent copy of your public-path list.** It must stay in sync with the `permitAll()` rules in the `SecurityFilterChain`. When the two lists stop matching, you get one of two bugs:

- a path that is `permitAll()` here but filtered there (harmless), or
- a path that the filter skips but the chain expects to be `authenticated()`. This is a **bypass**.

Prefer one shared `RequestMatcher` constant that both use. Also note: `getServletPath().startsWith(...)` ignores the context path and URL normalisation. A `RequestMatcher` does not.

<details>
<summary><strong>🤔 Doubt: Should the filter reload UserDetails from the database on every request?</strong></summary>

**Usually no. And if you do, do not call the design stateless.**

The common tutorial snippet calls `userDetailsService.loadUserByUsername(username)` inside the filter. That is a **database read on every authenticated request**. It breaks the main reason you chose JWT: "token verified locally, no session store, no lookup." If an interviewer sees that filter, the obvious question is *"your filter hits the DB per request — in what sense is that stateless?"*

The signed token **is** the authorization data. `generateToken` already puts `roles` into the claims. The filter should read them back. It should not throw them away and query again.

📋 **The trade-off, stated honestly:**

| Approach | Freshness of roles | Cost per request | When it is right |
|---|---|---|---|
| **Authorities from claims** (above) | Stale until the token expires | ✅ Zero I/O — signature check only | Default. Access tokens are 5–15 min, so the staleness window is bounded and small |
| **Reload `UserDetails` per request** | ✅ Immediate | ❌️ One DB (or cache) read per request | You really need instant revocation — a demotion or lock must take effect *now* |

If you do need instant effect, state the trade-off clearly. Do not hide it: *"I traded statelessness for freshness."* And try the cheaper middle options first:

- a **short access-token TTL** (the staleness window *is* the TTL),
- a `tokenVersion` claim compared against a **cached** per-user counter,
- a `jti` **blacklist in Redis** checked only for the revocation cases you actually care about (logout, password change, admin force-logout).

Each of those adds a *little* state for a specific guarantee. This is the same idea as the revocation-strategy table in §3 Q5:

- Pure JWTs cannot be revoked.
- So every revocation mechanism pays for freshness with state.
- The goal is to keep the state small, not to pretend it is zero.

⚠️ **One thing you do lose** when you read claims: the filter does not re-check account status flags (`enabled`, `accountNonLocked`). Suppose locking an account must end active sessions immediately. That is exactly the "instant revocation" case. Use the blacklist, not a `UserDetails` load on every request.

---

</details>
<br/>

<details>
<summary><strong>🤔 Doubt: Why is `@Component` on a `OncePerRequestFilter` a bug?</strong></summary>

Spring Boot auto-registers **every `Filter` bean** in the application context with the **servlet container**, mapped to `/*`. You also call `http.addFilterBefore(jwtAuthFilter, ...)`. So the same filter is registered twice:

1. Once by the servlet container on `/*` — **outside** the `SecurityFilterChain` entirely.
2. Once inside the security chain, where you actually wanted it.

✅ **Be exact about the symptom.** Most blog posts (and most candidates) say more than is true here:

- It does **not** actually execute twice on a path the chain handles. `OncePerRequestFilter` checks a request attribute named `<filterName>.FILTERED`. Both registrations share one bean, so they share one filter name. So the second pass returns early.
- A plain `Filter` / `GenericFilterBean` has no such check. **That** one really does run twice.

⚠️ **The real damage is scope and ordering.**

- Boot registers the Spring Security chain at order `SecurityProperties.DEFAULT_FILTER_ORDER` = **-100**.
- A bare `@Component` filter defaults to `Ordered.LOWEST_PRECEDENCE`.
- So the container-level copy runs on `/*` **after** every filter of the security chain. This includes paths that no `SecurityFilterChain`'s `securityMatcher` covers.
- On those paths, it authenticates the request outside all of your security configuration.
- There, it fills the `SecurityContextHolder` after all security filters have run. Controllers and `@PreAuthorize` checks then see a user that no chain authenticated. (`FilterChainProxy` still clears the context when the request ends, so the thread does not keep it.)

🛠️ **Two fixes — pick one:**

```java
// Fix A (preferred): never make it a bean. Construct it in the config method.
@Bean
SecurityFilterChain securityFilterChain(HttpSecurity http, JwtUtil jwtUtil) throws Exception {
    return http
        .addFilterBefore(new JwtAuthenticationFilter(jwtUtil),
                         UsernamePasswordAuthenticationFilter.class)
        // ...
        .build();
}
```

```java
// Fix B: keep it a bean (e.g. you need @Autowired collaborators or AOP),
// but switch off Boot's container-level auto-registration.
@Bean
FilterRegistrationBean<JwtAuthenticationFilter> jwtFilterRegistration(
        JwtAuthenticationFilter filter) {
    FilterRegistrationBean<JwtAuthenticationFilter> registration =
        new FilterRegistrationBean<>(filter);
    registration.setEnabled(false);   // container registration off; chain still uses it
    return registration;
}
```

---

</details>
<br/>

**① Header check & token parse — no `Bearer` header means the filter does nothing:**

```mermaid
graph TD
    REQ["Incoming Request"] --> CHECK{"Has Authorization<br/>Bearer header?"}
    CHECK -->|No| NEXT["Continue filter chain<br/>(may be public endpoint)"]
    CHECK -->|Yes| EXTRACT["Extract JWT token"]
    EXTRACT --> PARSE["Verify signature<br/>+ exp / nbf"]

    classDef purple fill:#7C3AED,stroke:#7C3AED,color:#fff
    classDef cyan fill:#0891B2,stroke:#0891B2,color:#fff
    classDef orange fill:#D97706,stroke:#D97706,color:#fff

    class REQ cyan
    class CHECK orange
    class EXTRACT,PARSE purple
    class NEXT cyan
```

**② Validation & context population — every failure path just continues the chain, never throws:**

```mermaid
graph TD
    PARSE["Verify signature<br/>+ exp / nbf"] --> VALID{"Parse threw?"}
    VALID -->|Yes — log only| NEXT["Continue filter chain"]
    VALID -->|No| CTX{"SecurityContext<br/>already has auth?"}
    CTX -->|Yes| NEXT
    CTX -->|No| CLAIMS["Read sub + roles<br/>from claims (no DB)"]
    CLAIMS --> SET["Fresh SecurityContext<br/>+ setAuthentication"]
    SET --> NEXT
    NEXT --> DS["DispatcherServlet"]

    classDef purple fill:#7C3AED,stroke:#7C3AED,color:#fff
    classDef cyan fill:#0891B2,stroke:#0891B2,color:#fff
    classDef green fill:#059669,stroke:#059669,color:#fff
    classDef orange fill:#D97706,stroke:#D97706,color:#fff

    class CTX,VALID orange
    class PARSE,CLAIMS purple
    class SET green
    class NEXT cyan
    class DS green
```

> `Verify signature + exp / nbf` joins the two diagrams. Both diagrams end at the same single exit: `Continue filter chain`. This is the design point to say in the interview: this filter **never rejects** a request. It only *fills* the `SecurityContext`. The 401/403 decision belongs to `AuthorizationFilter` and `ExceptionTranslationFilter` later in the chain.

📋 **Why each step matters:**

| Step | Why |
|------|-----|
| Check for `Bearer ` prefix | Standard OAuth2 convention; other auth types might use different prefixes |
| Check `SecurityContext` is empty | Avoids redundant processing if already authenticated |
| Read authorities from **claims**, not the DB | The signature is what makes the claims trustworthy — re-querying per request throws away the whole point of a stateless token (see the doubt block above) |
| `createEmptyContext()` before `setAuthentication` | Never mutate the currently-held context; it may be a shared instance |
| Set `WebAuthenticationDetails` | Captures request metadata (IP address, session ID) for audit logging |
| Catch `JwtException`, not `Exception` | A blanket `catch (Exception)` swallows real bugs (NPEs, DB failures) as "auth failed" and hides them |
| `shouldNotFilter()` | ⚠️ A **security** decision, not a performance tweak — it must mirror `permitAll()` exactly |

📝 **Note:** This filter is registered in the `SecurityFilterChain` using `addFilterBefore()` to execute **before** Spring's `UsernamePasswordAuthenticationFilter`:

```java
http.addFilterBefore(new JwtAuthenticationFilter(jwtUtil),
    UsernamePasswordAuthenticationFilter.class);
```

🎯 **Interview Tip:** Stress that the filter does NOT reject requests without tokens. It just does not set the `SecurityContext`. The authorization decision happens later in the `AuthorizationFilter`. This allows public endpoints (`permitAll()`) to work even without a token.

---

</details>

---

<a id="security-configuration"></a>

## 4. Security Configuration

1. **⚡ How do you configure SecurityFilterChain in Spring Security 6? (with code example) 🔥🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

In Spring Security 6 (Spring Boot 3+), the `WebSecurityConfigurerAdapter` is **removed**. You configure security with `SecurityFilterChain` beans in a `@Configuration` class. This is the **component-based** approach.

```java
@Configuration
@EnableWebSecurity
@EnableMethodSecurity  // Enables @PreAuthorize, @PostAuthorize
public class SecurityConfig {

    private final JwtUtil jwtUtil;
    private final AuthenticationProvider authenticationProvider;
    private final CustomAuthenticationEntryPoint authEntryPoint;
    private final CustomAccessDeniedHandler accessDeniedHandler;

    public SecurityConfig(JwtUtil jwtUtil,
                          AuthenticationProvider authenticationProvider,
                          CustomAuthenticationEntryPoint authEntryPoint,
                          CustomAccessDeniedHandler accessDeniedHandler) {
        this.jwtUtil = jwtUtil;
        this.authenticationProvider = authenticationProvider;
        this.authEntryPoint = authEntryPoint;
        this.accessDeniedHandler = accessDeniedHandler;
    }

    @Bean
    SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        return http
            // 1. Disable CSRF — the API authenticates with a Bearer header, which the
            //    browser never attaches automatically, so there is no ambient credential
            //    to forge with. (NOT "because CSRF needs sessions" — it does not.)
            .csrf(AbstractHttpConfigurer::disable)

            // 2. URL-based authorization rules
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/auth/**", "/public/**").permitAll()
                .requestMatchers("/actuator/health").permitAll()
                .requestMatchers(HttpMethod.POST, "/api/users").hasRole("ADMIN")
                .requestMatchers("/api/admin/**").hasRole("ADMIN")
                .requestMatchers("/api/**").authenticated()
                .anyRequest().authenticated()
            )

            // 3. Stateless session management (no HttpSession)
            .sessionManagement(session ->
                session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))

            // 4. Register authentication provider
            .authenticationProvider(authenticationProvider)

            // 5. Register JWT filter before UsernamePasswordAuthenticationFilter.
            //    Constructed here, not injected as a bean — see §3 Q6 on why
            //    @Component on a Filter causes a second container-level registration.
            .addFilterBefore(new JwtAuthenticationFilter(jwtUtil),
                UsernamePasswordAuthenticationFilter.class)

            // 6. Exception handling
            .exceptionHandling(exception -> exception
                .authenticationEntryPoint(authEntryPoint)    // 401 handler
                .accessDeniedHandler(accessDeniedHandler)    // 403 handler
            )

            // 7. Disable form login and HTTP Basic (REST API only)
            .formLogin(AbstractHttpConfigurer::disable)
            .httpBasic(AbstractHttpConfigurer::disable)

            .build();
    }
}
```

📋 **Key configuration elements explained:**

| Configuration | Purpose | When to Use |
|--------------|---------|-------------|
| `csrf(AbstractHttpConfigurer::disable)` | Disable CSRF protection | REST APIs whose credential is a **header** (Bearer), never a cookie |
| `sessionManagement(STATELESS)` | No `HttpSession` created | JWT-based stateless auth |
| `authorizeHttpRequests()` | URL-level access rules | Always — defines who can access what |
| `addFilterBefore()` | Register custom JWT filter | JWT authentication |
| `exceptionHandling()` | Custom error responses | Always — for clean 401/403 responses |
| `authenticationProvider()` | Register auth provider | Always — defines how auth works |

```java
// Custom 401 handler
@Component
public class CustomAuthenticationEntryPoint implements AuthenticationEntryPoint {
    @Override
    public void commence(HttpServletRequest request,
                        HttpServletResponse response,
                        AuthenticationException authException) throws IOException {
        response.setContentType("application/json");
        response.setStatus(HttpServletResponse.SC_UNAUTHORIZED);
        response.getWriter().write("""
            {"error": "Unauthorized", "message": "%s"}
            """.formatted(authException.getMessage()));
    }
}

// Custom 403 handler
@Component
public class CustomAccessDeniedHandler implements AccessDeniedHandler {
    @Override
    public void handle(HttpServletRequest request,
                      HttpServletResponse response,
                      AccessDeniedException accessDeniedException) throws IOException {
        response.setContentType("application/json");
        response.setStatus(HttpServletResponse.SC_FORBIDDEN);
        response.getWriter().write("""
            {"error": "Forbidden", "message": "Insufficient permissions"}
            """);
    }
}
```

⚠️ **Spring Security 6 Migration Notes:**

| Old (Spring Security 5) | New (Spring Security 6) |
|-------------------------|------------------------|
| `extends WebSecurityConfigurerAdapter` | `@Bean SecurityFilterChain` |
| `antMatchers()` | `requestMatchers()` |
| `authorizeRequests()` | `authorizeHttpRequests()` |
| `.and()` chaining | Lambda DSL (no `.and()` needed) |
| `FilterSecurityInterceptor` | `AuthorizationFilter` |

🎯 **Interview Tip:** If they ask about the move from Spring Security 5 to 6, name the three key changes: (1) `WebSecurityConfigurerAdapter` removed in favor of `SecurityFilterChain` beans, (2) `antMatchers()` renamed to `requestMatchers()`, and (3) lambda DSL replaces `.and()` chaining.

---

</details>

---

2. **🌐 What is CORS? How do you configure it in Spring Security? 🔥🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

CORS (Cross-Origin Resource Sharing) is a browser mechanism. By default, the browser's **same-origin policy** stops a web page from reading responses from another origin. CORS lets the server **relax** this rule with response headers. The **browser** enforces it, not the server.

🧠 **In Simple Words:** Say your frontend runs on `http://localhost:3000` and your backend API is on `http://localhost:8080`. The browser does not let the frontend read the backend's response. It allows it only if the backend clearly permits it through CORS headers.

📋 **How CORS works:**

| Step | What Happens |
|------|-------------|
| 1 | For a non-simple request (e.g. `PUT`/`DELETE`, JSON body, or an `Authorization` header), the browser first sends a **preflight** `OPTIONS` request. Simple requests skip this step |
| 2 | Server responds with allowed origins, methods, and headers |
| 3 | If the origin is allowed, browser sends the actual request |
| 4 | If the origin is NOT allowed, browser blocks the request (CORS error) |

**Three ways to configure CORS in Spring Boot:**

1️⃣ **Global CORS via SecurityFilterChain (Recommended for Spring Security):**

```java
@Bean
SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    return http
        .cors(cors -> cors.configurationSource(corsConfigurationSource()))
        .csrf(AbstractHttpConfigurer::disable)
        .authorizeHttpRequests(auth -> auth
            .anyRequest().authenticated()
        )
        .build();
}

@Bean
CorsConfigurationSource corsConfigurationSource() {
    CorsConfiguration configuration = new CorsConfiguration();
    configuration.setAllowedOrigins(List.of(
        "http://localhost:3000",
        "https://myapp.com"
    ));
    configuration.setAllowedMethods(List.of(
        "GET", "POST", "PUT", "DELETE", "PATCH", "OPTIONS"
    ));
    configuration.setAllowedHeaders(List.of(
        "Authorization", "Content-Type", "X-Requested-With"
    ));
    configuration.setExposedHeaders(List.of("Authorization"));
    configuration.setAllowCredentials(true);
    configuration.setMaxAge(3600L);  // Preflight cache duration

    UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
    source.registerCorsConfiguration("/**", configuration);
    return source;
}
```

2️⃣ **Controller-level CORS:**

```java
@RestController
@CrossOrigin(origins = "http://localhost:3000")
@RequestMapping("/api/users")
public class UserController {

    @CrossOrigin(origins = "https://admin.myapp.com")
    @GetMapping
    public List<User> getAllUsers() { /* ... */ }
}
```

3️⃣ **Global CORS via WebMvcConfigurer:**

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/api/**")
            .allowedOrigins("http://localhost:3000")
            .allowedMethods("GET", "POST", "PUT", "DELETE")
            .allowedHeaders("*")
            .allowCredentials(true);
    }
}
```

⚠️ **Important: know how it works, not just the advice.** With Spring Security you **must call `.cors(...)` on the `SecurityFilterChain`**. Where the *configuration* comes from matters less:

- Spring Security adds its `CorsFilter` to the chain only **if you call `.cors(...)`**. (Since 6.2 it also does this for you when a `UrlBasedCorsConfigurationSource` bean exists.)
  - Leave out the call, and there is no CORS filter.
  - Then the chain rejects an unauthenticated preflight `OPTIONS` before MVC ever sees it.
- Say you *do* call `http.cors(Customizer.withDefaults())`, and there is **no** `CorsConfigurationSource` bean.
  - Then `CorsConfigurer` falls back to the `mvcHandlerMappingIntrospector` bean.
  - So it **will** pick up your `addCorsMappings(...)` from `WebMvcConfigurer`.
  - The `WebMvcConfigurer` approach is not "ignored". The code just never reaches it if you never enable CORS on the chain.

So the correct rule is: *`.cors(...)` on the chain is mandatory (unless a `UrlBasedCorsConfigurationSource` bean turns it on for you, 6.2+); a `CorsConfigurationSource` bean is the explicit option and MVC's `addCorsMappings` is the fallback.*

🎯 **Interview Tip:** Say that you cannot use `allowCredentials(true)` and `allowedOrigins("*")` together.
- This is a rule in the spec: the browser rejects `Access-Control-Allow-Origin: *` on a credentialed request.
- The way around it is `setAllowedOriginPatterns(List.of("https://*.myapp.com"))`.
- It matches by pattern, then sends back the **concrete** origin. So credentials are still allowed.

---

</details>

---

3. **🛡️ What is CSRF protection? When should you enable or disable it? 🔥🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

CSRF (Cross-Site Request Forgery) is an attack. A malicious website tricks a user's browser into sending a request the user did not intend. The request goes to a target site where the user is already authenticated.

🔍 **How CSRF attack works:**

1. User logs into `bank.com` (session cookie stored in browser).
2. User visits `malicious-site.com`.
3. Malicious site has a hidden form that submits a POST request to `bank.com/transfer?amount=10000&to=attacker`.
4. Browser automatically includes the `bank.com` session cookie with the request.
5. `bank.com` processes the request because the session cookie is valid.

<img src="./img/security_jwt_csrf_attack_vs_protection.png" alt="CSRF attack vs protection — the browser sends the forged POST with the cookie; without the CSRF token it gets 403" style="max-width:100%;"/>

🛡️ **How CSRF protection works in Spring Security:**

Spring Security generates a unique **CSRF token**. It requires this token in every state-changing request (POST, PUT, DELETE). The malicious site cannot read the CSRF token from another domain (same-origin policy). So it cannot put the token in its forged request.

```java
// CSRF enabled (default in Spring Security)
@Bean
SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    return http
        .csrf(csrf -> csrf
            .csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse())
            .ignoringRequestMatchers("/api/webhooks/**")  // Exclude specific paths
        )
        .build();
}
```

⚠️ **CSRF tokens do not require a session.**
- Only the *default* repository, `HttpSessionCsrfTokenRepository`, uses one.
- `CookieCsrfTokenRepository` (above) keeps the token in a cookie with **zero server-side state**.
- This is exactly how you run CSRF protection on a `SessionCreationPolicy.STATELESS` chain.
- `withHttpOnlyFalse()` lets the SPA's JavaScript read the cookie. The JavaScript then sends the value back in the `X-XSRF-TOKEN` header. This is the double-submit-cookie pattern.
- ⚠️ In Spring Security 6, the default `XorCsrfTokenRequestAttributeHandler` rejects this raw cookie value. An SPA also needs a request handler that accepts it (the reference docs show one for SPAs).

📋 **When to enable/disable CSRF:**

| Scenario | CSRF Protection | Reason |
|----------|----------------|--------|
| **Server-rendered web app (Thymeleaf, JSP)** | ✅ Enable | Session cookies are vulnerable to CSRF |
| **REST API with JWT (no cookies)** | ❌️ Disable | No cookies = no CSRF risk |
| **SPA with cookie-based auth** | ✅ Enable | Cookies are used for auth |
| **SPA with JWT in `Authorization` header** | ❌️ Disable | Browser does not auto-send headers |
| **Webhook endpoints** | ❌️ Disable (for that path) | External services cannot provide CSRF tokens |
| **Public endpoints** | ❌️ Disable (for that path) | No auth needed, no CSRF risk |

```java
// Typical REST API configuration — CSRF disabled
@Bean
SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    return http
        .csrf(AbstractHttpConfigurer::disable)  // Bearer header, not cookies
        .sessionManagement(session ->
            session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
        .build();
}
```

🔑 **Key Point:** CSRF attacks exploit **cookie-based authentication**. Browsers attach cookies to requests automatically.
- Say your application sends JWT tokens in the `Authorization` header (not cookies).
- Then CSRF is not a concern. The browser never adds the `Authorization` header automatically.
- JavaScript code must set it explicitly.

🎯 **Interview Tip:** The main rule: "If you use cookies for authentication, enable CSRF. If you use Bearer tokens in headers, disable CSRF." Always explain the **why**. It is about whether the browser adds the credential automatically or your code adds it by hand.

---

</details>

---

4. **🔒 Compare BCrypt, Argon2, and SCrypt password encoding algorithms. 🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

All three are **adaptive hashing functions** built for password storage. They are slow on purpose, so brute-force attacks cost a lot of computing power. Spring Security provides implementations for all three through `PasswordEncoder`.

| Feature | BCrypt 🅰️ | Argon2 🅱️ | SCrypt 🅲 |
|---------|-----------|-----------|----------|
| **Algorithm Type** | CPU-intensive hash | Memory + CPU-intensive hash | Memory + CPU-intensive hash |
| **Year Introduced** | 1999 | 2015 (PHC winner) | 2009 |
| **Brute-Force Resistance** | ✅ Good (CPU cost) | ✅ Best (memory + CPU cost) | ✅ Very Good (memory + CPU cost) |
| **GPU Attack Resistance** | ⚠️ Moderate | ✅ Strong (memory-hard) | ✅ Strong (memory-hard) |
| **Tunable Parameters** | Cost factor (work factor) | Memory, iterations, parallelism | CPU cost, memory cost, parallelism |
| **Spring Class** | `BCryptPasswordEncoder` | `Argon2PasswordEncoder` | `SCryptPasswordEncoder` |
| **Industry Adoption** | ✅ Most widely used | 📈 Growing (modern standard) | ⚠️ Less common |
| **Extra dependency** | None (bundled in `spring-security-crypto`) | ⚠️ Needs **BouncyCastle** on the classpath | ⚠️ Needs **BouncyCastle** on the classpath |
| **Input length limit** | ⚠️ **Silently truncates past 72 bytes** | None | None |
| **OWASP ranking (2026)** | 3rd — legacy / compatibility | ✅ **1st — Argon2id** | 2nd |

🧂 **The salt question — interviewers really do ask this.** The usual first question is *"why does hashing the same password twice give two different strings?"*

- **All three generate a random salt per call and store it inside the output.**
  - There is no separate salt column, and no salt parameter to `encode()`.
  - That is why the constructors above take a salt **length**, not a salt value.
- A BCrypt hash describes itself: `$2a$10$` + **22-char Base64 salt** + **31-char Base64 hash**.
  - `matches(raw, stored)` reads the cost factor and the salt back out of `stored`.
  - It re-hashes `raw` with them, and compares.
- Result: `encode("x").equals(encode("x"))` is **false**. Never store or compare hashes with `==` / `equals`. Always go through `matches()`.
- The cost factor is stored in the hash too, so you can raise it later. Existing hashes still verify at their old cost. You re-hash on the next successful login.
- **What the salt really defends against: pre-computation.**
  - Without a salt, an attacker hashes the top few million passwords *once* and keeps the table. This is a **rainbow table**.
  - Then the attacker cracks any stolen database by lookup.
  - With a per-password salt, the attacker would have to rebuild the table per user. That makes the attack far too expensive.
  - The salt defends against *pre-computation*, not against brute-forcing one specific hash. The cost factor handles that.
- **The salt is not secret.** It sits in plain text inside the hash string, and that is fine. Its job is uniqueness, not secrecy. (A secret value added *as well* is a "pepper", stored outside the DB. That is a different mechanism for a different threat.)
- **Why not just SHA-256?**
  - It is a *fast* hash. Speed is its design goal, and that is exactly wrong here.
  - Ordinary GPUs compute billions of SHA-256 hashes per second.
  - MD5 and SHA-1 are even worse, and they are also broken for collisions.
  - "I'd SHA-256 the password" is a common interview answer, and it loses you points.

⚠️ **BCrypt's 72-byte limit.**
- BCrypt only reads the first **72 bytes** of the input. It silently ignores the rest.
- So two 100-character passphrases that share a 72-byte prefix give the same hash.
- This matters for UIs that encourage long passphrases.
- It is also why the "pre-hash with SHA-256 then BCrypt" pattern must Base64-encode the digest. Raw digest bytes can contain a `0x00`, which cuts the BCrypt input short even earlier.

```java
// BCrypt (default and most common)
@Bean
PasswordEncoder bCryptEncoder() {
    return new BCryptPasswordEncoder(12);  // cost factor 4-31 (default: 10)
}

// Argon2 (strongest — Password Hashing Competition winner).
// Spring's encoder always uses the Argon2*id* variant, the one OWASP recommends.
// ⚠️ Requires BouncyCastle (org.bouncycastle:bcprov-jdk18on) on the classpath.
@Bean
PasswordEncoder argon2Encoder() {
    // Prefer the curated factory over hand-tuned numbers — it tracks Spring's
    // current recommended parameters (16-byte salt, 32-byte hash, p=1, 16 MB, 2 iterations).
    return Argon2PasswordEncoder.defaultsForSpringSecurity_v5_8();
}

// ...or tune explicitly if you have measured your hardware:
@Bean
PasswordEncoder tunedArgon2Encoder() {
    return new Argon2PasswordEncoder(
        16,    // salt length (bytes)
        32,    // hash length (bytes)
        1,     // parallelism
        65536, // memory in KB (64 MB)
        3      // iterations
    );
}

// SCrypt
@Bean
PasswordEncoder sCryptEncoder() {
    return new SCryptPasswordEncoder(
        16384, // CPU/memory cost
        8,     // block size
        1,     // parallelism
        32,    // key length
        16     // salt length
    );
}

// DelegatingPasswordEncoder (supports migration between algorithms)
@Bean
PasswordEncoder delegatingEncoder() {
    return PasswordEncoderFactories.createDelegatingPasswordEncoder();
    // Encodes with BCrypt by default
    // Can verify: {bcrypt}..., {argon2}..., {scrypt}..., {noop}...
}
```

💡 **Pro Tip:** Use `DelegatingPasswordEncoder` in production. It adds the algorithm ID in front of the hash (e.g., `{bcrypt}$2a$10$...`). This lets you:

- Support multiple encoding schemes simultaneously.
- Migrate from one algorithm to another without forcing password resets.
- Verify legacy passwords encoded with older algorithms.

📝 **Note:** The `{noop}` prefix in `DelegatingPasswordEncoder` stores passwords as plain text. Use it only for testing. Example: `{noop}mypassword`.

🎯 **Interview Tip:** Start with **Argon2id**.
- OWASP's Password Storage Cheat Sheet ranks it **first**, then scrypt, then bcrypt. (It lists bcrypt mostly for legacy systems and compatibility.)
- The main advantage: Argon2 is **memory-hard** (it needs a lot of memory per hash). So a GPU/ASIC attacker cannot run many guesses in parallel cheaply. Against BCrypt's pure-CPU cost, they can.
- Then add the practical exception: **BCrypt is the right default when you inherit an existing hash column**.
- That is exactly why `DelegatingPasswordEncoder` exists. It lets you verify `{bcrypt}` hashes today. It also lets you re-encode each user to `{argon2}` on their next successful login. This needs two things. First, set `{argon2}` as the default ID, so `upgradeEncoding()` returns `true` for `{bcrypt}` hashes. Second, provide a `UserDetailsPasswordService` bean that saves the new hash.

---

</details>

---

5. **📡 What is SessionCreationPolicy.STATELESS and why is it used for REST APIs? 🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

`SessionCreationPolicy.STATELESS` tells Spring Security to **never create or use an `HttpSession`** for security purposes. REST APIs that use token-based (JWT) authentication need this.

📋 **All session creation policies:**

| Policy | Behavior | Use Case |
|--------|----------|----------|
| `ALWAYS` | Always create a session | Legacy web apps |
| `IF_REQUIRED` | Create session only when needed | ✅ Default — traditional web apps |
| `NEVER` | Never create a session, but use one if it exists | Mixed apps (API + web) |
| `STATELESS` | Never create AND never use any session | ✅ REST APIs with JWT |

```java
@Bean
SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    return http
        .sessionManagement(session ->
            session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
        .build();
}
```

🔍 **What happens when STATELESS is set:**

- 🚫 No `HttpSession` is created on the server.
- 🚫 No `JSESSIONID` cookie is sent to the client.
- 🔁 The `SecurityContextRepository` becomes a `RequestAttributeSecurityContextRepository` (in Spring Security 5.x it was a `NullSecurityContextRepository`).
  - So `SecurityContextHolderFilter` has nothing to load from, and nothing is written to a session.
  - The context lives for exactly one request.
- 📦 Spring Security treats each request on its own. Every request must carry authentication.
- ⚡ Less memory use — no session objects in server memory.

⚠️ **What breaks without session:**

| Feature | Impact |
|---------|--------|
| `SecurityContext` persistence | ❌️ Not persisted between requests |
| Form login (`/login` page) | ❌️ No session to store login state |
| CSRF protection | ⚠️ The **default** `HttpSessionCsrfTokenRepository` has nowhere to store the token — switch to `CookieCsrfTokenRepository`, or disable CSRF because the API uses `Authorization` headers (see below) |
| Remember-me | ⚠️ Still works, but it logs the user in again from its cookie on every request (a user lookup each time) |
| `HttpSession.getAttribute()` | ⚠️ Spring Security never creates or uses a session. Your own code still can, so it is not always null |

🧠 **In Simple Words:** Without `STATELESS`, Spring Security creates a session for every authenticated user. It stores the `SecurityContext` in that session. With `STATELESS`, the server remembers nothing between requests. Every request must carry its own proof of identity (the JWT token).

🔑 **Key Point:** When using `SessionCreationPolicy.STATELESS`, always pair it with:

1. `csrf.disable()` — ⚠️ the reason is **not** "CSRF needs sessions". It does not: `CookieCsrfTokenRepository` is fully stateless (see §4 Q3). The real reason: the token travels in the `Authorization` header, and the browser never attaches that header automatically. No ambient credential (one the browser sends on its own) ⇒ nothing for an attacker to forge with.
2. A JWT authentication filter — to re-authenticate on every request.
3. Custom `AuthenticationEntryPoint` — because there is no login page to redirect to.

⚠️ **Say the right reason.** Say you move the token into a cookie. `STATELESS` stays the same, but CSRF protection becomes **mandatory** again. This proves the session policy never decided the CSRF setting.

🎯 **Interview Tip:** If they ask "Why disable sessions for REST APIs?", explain the three benefits: (1) **Scalability** — no session replication needed across servers; (2) **Simplicity** — no sticky sessions in load balancers; (3) **Statelessness** — matches REST architectural constraints.

---

</details>

---

6. **🏗️ Show a complete JWT security configuration for a Spring Boot REST API. 🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

Here is a complete, production-ready JWT security configuration for Spring Boot 3 + Spring Security 6.

**`application.yml`:**

```yaml
app:
  jwt:
    # ⚠️ NEVER commit the signing secret. Inject it from the environment /
    # a secrets manager (AWS Secrets Manager, Vault, K8s Secret) — a leaked
    # HS512 secret lets anyone mint an admin token for your API.
    secret: ${JWT_SIGNING_SECRET}   # must be >= 64 bytes for HS512
    access-token-expiry-ms: 900000    # 15 minutes
    refresh-token-expiry-ms: 2592000000  # 30 days
```

**`JwtUtil.java`:**

```java
@Component
public class JwtUtil {

    @Value("${app.jwt.secret}")
    private String secret;

    @Value("${app.jwt.access-token-expiry-ms}")
    private long accessTokenExpiryMs;

    private SecretKey key;

    @PostConstruct
    public void init() {
        this.key = Keys.hmacShaKeyFor(secret.getBytes(StandardCharsets.UTF_8));
    }

    public String generateToken(String username, Collection<? extends GrantedAuthority> authorities) {
        List<String> roles = authorities.stream()
            .map(GrantedAuthority::getAuthority)
            .toList();

        Instant now = Instant.now();
        return Jwts.builder()
            .subject(username)
            .issuer("myapp")
            .claim("roles", roles)
            .issuedAt(Date.from(now))
            .expiration(Date.from(now.plusMillis(accessTokenExpiryMs)))
            .signWith(key, Jwts.SIG.HS512)
            .compact();
    }

    /**
     * Verifies the signature and the exp/nbf claims, and returns the claims.
     * Throws JwtException on any failure — there is nothing left to "also check".
     */
    public Claims parseClaims(String token) {
        return Jwts.parser()
            .verifyWith(key)
            .requireIssuer("myapp")
            .clockSkewSeconds(30)
            .build()
            .parseSignedClaims(token)
            .getPayload();
    }

    public String getUsername(String token) {
        return parseClaims(token).getSubject();
    }
}
```

⚠️ **Why there is no `validateToken(token, username)` here.** The common version of that method is dead code:

```java
// ❌️ The expiry clause can never be false
public boolean validateToken(String token, String username) {
    String tokenUsername = getUsername(token);   // → parseSignedClaims → throws on expiry
    return username.equals(tokenUsername) && !isExpired(token);
}
```

- `getUsername` parses the token.
- For an expired token, the parse **already throws `ExpiredJwtException`**.
- So with an expired token, control never reaches `!isExpired(token)`. That clause is always `true`.
- The username comparison is also not needed if you build the principal from `claims.getSubject()` instead of reloading `UserDetails`. You would compare the subject with a value you took *from the same subject*.

Parse once, let it throw, and use the claims.

**`JwtAuthenticationFilter.java`:**

```java
// No @Component — it is constructed by SecurityConfig below, so Spring Boot
// never auto-registers it with the servlet container. (See §3 Q6.)
public class JwtAuthenticationFilter extends OncePerRequestFilter {

    private final JwtUtil jwtUtil;

    public JwtAuthenticationFilter(JwtUtil jwtUtil) {
        this.jwtUtil = jwtUtil;
    }

    @Override
    protected void doFilterInternal(HttpServletRequest request,
                                    HttpServletResponse response,
                                    FilterChain filterChain)
            throws ServletException, IOException {

        String authHeader = request.getHeader("Authorization");

        if (authHeader != null && authHeader.startsWith("Bearer ")) {
            String token = authHeader.substring(7);
            try {
                Claims claims = jwtUtil.parseClaims(token);   // throws if invalid/expired

                if (SecurityContextHolder.getContext().getAuthentication() == null) {
                    List<SimpleGrantedAuthority> authorities =
                        ((List<?>) claims.getOrDefault("roles", List.of())).stream()
                            .map(String::valueOf)
                            .map(SimpleGrantedAuthority::new)
                            .toList();

                    UsernamePasswordAuthenticationToken authToken =
                        UsernamePasswordAuthenticationToken.authenticated(
                            claims.getSubject(), null, authorities);
                    authToken.setDetails(
                        new WebAuthenticationDetailsSource().buildDetails(request));

                    SecurityContext context = SecurityContextHolder.createEmptyContext();
                    context.setAuthentication(authToken);
                    SecurityContextHolder.setContext(context);
                }
            } catch (JwtException | IllegalArgumentException e) {
                logger.warn("JWT authentication failed: " + e.getMessage());
            }
        }
        filterChain.doFilter(request, response);
    }
}
```

**`SecurityConfig.java` (complete configuration):**

```java
@Configuration
@EnableWebSecurity
@EnableMethodSecurity
public class SecurityConfig {

    private final UserDetailsService userDetailsService;
    private final JwtUtil jwtUtil;

    public SecurityConfig(UserDetailsService userDetailsService, JwtUtil jwtUtil) {
        this.userDetailsService = userDetailsService;
        this.jwtUtil = jwtUtil;
    }

    @Bean
    PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    @Bean
    AuthenticationProvider authenticationProvider() {
        DaoAuthenticationProvider provider =
            new DaoAuthenticationProvider(userDetailsService);
        provider.setPasswordEncoder(passwordEncoder());
        return provider;
    }

    @Bean
    AuthenticationManager authenticationManager(
            AuthenticationConfiguration config) throws Exception {
        return config.getAuthenticationManager();
    }

    @Bean
    SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        return http
            .csrf(AbstractHttpConfigurer::disable)
            .cors(cors -> cors.configurationSource(corsConfigurationSource()))
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/auth/**").permitAll()
                .requestMatchers("/actuator/health").permitAll()
                .requestMatchers("/api/admin/**").hasRole("ADMIN")
                .anyRequest().authenticated()
            )
            .sessionManagement(session ->
                session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
            .authenticationProvider(authenticationProvider())
            .addFilterBefore(new JwtAuthenticationFilter(jwtUtil),
                UsernamePasswordAuthenticationFilter.class)
            .exceptionHandling(exception -> exception
                .authenticationEntryPoint((request, response, authException) -> {
                    response.setContentType("application/json");
                    response.setStatus(HttpServletResponse.SC_UNAUTHORIZED);
                    response.getWriter().write(
                        "{\"error\": \"Unauthorized\", \"message\": \""
                        + authException.getMessage() + "\"}");
                })
                .accessDeniedHandler((request, response, accessDeniedException) -> {
                    response.setContentType("application/json");
                    response.setStatus(HttpServletResponse.SC_FORBIDDEN);
                    response.getWriter().write(
                        "{\"error\": \"Forbidden\", \"message\": \"Insufficient permissions\"}");
                })
            )
            .build();
    }

    @Bean
    CorsConfigurationSource corsConfigurationSource() {
        CorsConfiguration config = new CorsConfiguration();
        config.setAllowedOrigins(List.of("http://localhost:3000"));
        config.setAllowedMethods(List.of("GET", "POST", "PUT", "DELETE", "OPTIONS"));
        config.setAllowedHeaders(List.of("Authorization", "Content-Type"));
        config.setAllowCredentials(true);
        config.setMaxAge(3600L);

        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
        source.registerCorsConfiguration("/**", config);
        return source;
    }
}
```

**`AuthController.java`:**

```java
@RestController
@RequestMapping("/auth")
public class AuthController {

    @Autowired
    private AuthenticationManager authenticationManager;

    @Autowired
    private JwtUtil jwtUtil;

    @PostMapping("/login")
    public ResponseEntity<Map<String, String>> login(@RequestBody LoginRequest request) {
        Authentication authentication = authenticationManager.authenticate(
            new UsernamePasswordAuthenticationToken(
                request.getUsername(), request.getPassword()));

        UserDetails userDetails = (UserDetails) authentication.getPrincipal();
        String token = jwtUtil.generateToken(
            userDetails.getUsername(), userDetails.getAuthorities());

        return ResponseEntity.ok(Map.of(
            "token", token,
            "type", "Bearer",
            "username", userDetails.getUsername()
        ));
    }
}
```

📝 **Note:** This configuration covers the basics: stateless session, JWT filter, CORS, CSRF disabled, custom error handlers, password encoding, and method-level security. For production, you would add refresh tokens, rate limiting, and request logging.

📝 **Which version:** everything above targets **Spring Security 6.x** (Spring Boot 3.x). Most production systems run this version, and interviews ask about it. **Spring Security 7.0** was released with Spring Boot 4.0 in Nov 2025. Know it in one sentence ("6.x in production, 7.0 is out with Boot 4"). It is not a reason to rewrite your answers.

<details>
<summary><strong>🤔 Doubt: How do you test a secured endpoint?</strong></summary>

This fits with the JUnit/Mockito material ([16_JUnit_Mockito_Interview_Questions.md](16_JUnit_Mockito_Interview_Questions.md)). It is a very likely follow-up question after you describe a security config.

Add `spring-security-test`, then:

```java
@WebMvcTest(OrderController.class)
@Import(SecurityConfig.class)   // load YOUR rules; otherwise Boot's default security is used
class OrderControllerSecurityTest {

    @Autowired
    private MockMvc mockMvc;

    // SecurityConfig's constructor needs these. @WebMvcTest does not load them.
    // (@MockitoBean needs Boot 3.4+; on older versions use @MockBean.)
    @MockitoBean
    private UserDetailsService userDetailsService;

    @MockitoBean
    private JwtUtil jwtUtil;

    @Test
    @WithMockUser(roles = "ADMIN")           // builds a fake Authentication in the context
    void adminCanDelete() throws Exception {
        mockMvc.perform(delete("/api/orders/1").with(csrf()))
               .andExpect(status().isNoContent());
    }

    @Test
    @WithMockUser(roles = "USER")
    void userCannotDelete() throws Exception {
        mockMvc.perform(delete("/api/orders/1").with(csrf()))
               .andExpect(status().isForbidden());      // 403 — authenticated, not allowed
    }

    @Test
    void anonymousIsRejected() throws Exception {
        mockMvc.perform(delete("/api/orders/1"))
               .andExpect(status().isUnauthorized());   // 401 — not authenticated
    }

    @Test
    void resourceServerJwt() throws Exception {
        // For an oauth2ResourceServer chain — no real token, no signature needed
        mockMvc.perform(get("/api/orders")
                   .with(jwt().authorities(new SimpleGrantedAuthority("SCOPE_read"))))
               .andExpect(status().isOk());
    }
}
```

📋 **The toolkit:**

| Tool | What it does |
|---|---|
| `@WithMockUser(roles = "ADMIN")` | Puts a fake `Authentication` in the `SecurityContext`. Note: `roles = "ADMIN"` becomes the authority `ROLE_ADMIN`. But `authorities = "ADMIN"` is used as written |
| `@WithUserDetails("alice")` | Loads a real principal through your `UserDetailsService`. Use it when the test needs real user data |
| `@WithAnonymousUser` | Sets an unauthenticated user on purpose |
| `.with(csrf())` | Adds a valid CSRF token. You need it for any request that changes data when CSRF is enabled |
| `.with(jwt())` / `.with(opaqueToken())` | Post-processors for `oauth2ResourceServer` chains. They inject claims/authorities without creating a signed token |
| `@WithSecurityContext` | Meta-annotation for building your own custom principal annotation |

⚠️ **The trap:** `@WebMvcTest` **does** load the security filter chain (via `SecurityAutoConfiguration`).

- Candidates write a controller test. They get a **401** instead of the result they expected. They decide the controller is broken.
- It is not broken. The request never reached it.
- Fix: annotate the test with a `@WithMockUser*`, or import a test-only `SecurityFilterChain`.
- Do **not** use `@AutoConfigureMockMvc(addFilters = false)` as the fix. It disables the security chain, so your test now proves nothing about authorization.

---

</details>
<br/>

---

</details>

---

<a id="oauth2-basics"></a>

## 5. OAuth2 Basics

1. **🌍 Explain the OAuth2 Authorization Code flow with a sequence diagram. 🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

The Authorization Code flow is the most secure and commonly used OAuth2 grant type. It was first built for **server-side web applications** (confidential clients). These apps can safely store a client secret. With **PKCE**, public clients (SPAs, mobile apps) use the same flow without a secret.

📋 **OAuth2 Roles:**

| Role | Description | Example |
|------|-------------|---------|
| **Resource Owner** | The user who owns the data | You (the person logging in) |
| **Client** | The application requesting access | Your web app |
| **Authorization Server** | Issues access tokens after authenticating the user | Google, Auth0, Keycloak |
| **Resource Server** | Hosts the protected resources/APIs | Google Calendar API |

```mermaid
sequenceDiagram
    participant U as User (Resource Owner)
    participant C as Client App
    participant AS as Authorization Server
    participant RS as Resource Server

    U->>C: 1. Click "Login with Google"
    C->>AS: 2. Redirect to /authorize?response_type=code&client_id=X&redirect_uri=Y&scope=profile
    AS->>U: 3. Show login page
    U->>AS: 4. Enter credentials + consent
    AS->>C: 5. Redirect (through the user's browser) to callback URL with code
    Note over C: redirect_uri?code=AUTH_CODE

    C->>AS: 6. POST /token (code + client_id + client_secret)
    Note over C,AS: Server-to-server call (code exchange)
    AS-->>C: 7. { access_token, refresh_token, expires_in }

    C->>RS: 8. GET /api/user (Authorization: Bearer access_token)
    RS->>RS: 9. Validate token
    RS-->>C: 10. { user profile data }
    C-->>U: 11. Show user profile
```

<img src="./img/security_jwt_oauth2_auth_code_flow.png" alt="OAuth2 Authorization Code Flow" style="max-width:100%;"/>

**Step-by-step breakdown:**

1️⃣ **User starts login** — The user clicks "Login with Google" on your app.

2️⃣ **Client redirects to Authorization Server** — Your app sends the user's browser to Google's authorization endpoint. It adds these parameters:

```
https://accounts.google.com/o/oauth2/v2/auth?
  response_type=code&
  client_id=YOUR_CLIENT_ID&
  redirect_uri=https://yourapp.com/callback&
  scope=openid profile email&
  state=RANDOM_STATE_VALUE
```

| Parameter | Purpose |
|-----------|---------|
| `response_type=code` | Requesting an authorization code |
| `client_id` | Your app's registered ID |
| `redirect_uri` | Where to send the code after login |
| `scope` | What permissions you are requesting |
| `state` | CSRF protection — random value verified on callback |

3️⃣ **User authenticates** — Google shows its login page. The user enters credentials.

4️⃣ **User consents** — The user approves the requested scopes (e.g., "Allow this app to see your profile").

5️⃣ **Authorization code returned** — Google redirects back to your callback URL. The URL carries a short-lived authorization code:

```
https://yourapp.com/callback?code=AUTH_CODE_HERE&state=RANDOM_STATE_VALUE
```

6️⃣ **Client exchanges code for tokens** — Your **server** (not the browser) sends a POST request to Google's token endpoint:

```
POST https://oauth2.googleapis.com/token
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&
code=AUTH_CODE_HERE&
client_id=YOUR_CLIENT_ID&
client_secret=YOUR_CLIENT_SECRET&
redirect_uri=https://yourapp.com/callback
```

7️⃣ **Tokens received** — Google returns an access token. It may also return a refresh token.

8️⃣-11️⃣ **Access resources** — Your app uses the access token to call Google APIs on behalf of the user.

🔑 **Key Point:** The app exchanges the authorization code for tokens through a **server-to-server call** (step 6). The browser never sees the client secret. This makes the Authorization Code flow more secure than the Implicit flow (now deprecated).

🎯 **Interview Tip:** Always mention two things: the `state` parameter for CSRF protection, and **PKCE** (Proof Key for Code Exchange). ⚠️ Be exact here:

- **OAuth 2.1 *requires* PKCE for all clients using the authorization-code grant** — public *and* confidential. One narrow exception: a confidential client that uses the OpenID Connect `nonce` correctly may skip it. PKCE is still recommended even then. (OAuth 2.1 is still an IETF draft. The OAuth Security BCP, RFC 9700, already requires PKCE for public clients and recommends it for confidential ones.)
- It does not only "recommend" it.
- OAuth 2.1 also **removes** the Implicit grant and the Resource Owner Password Credentials grant completely.

<details>
<summary><strong>🤔 Doubt: How does PKCE actually work, and what attack does it stop?</strong></summary>

**The attack:**

- A public client (a mobile app or SPA) has no `client_secret`. Anyone can read what is shipped to the device.
- So in step 6 of the flow (`POST /token`), the only proof the server checks is *possession of the authorization code*.
- Some attackers can see that code. Examples: a malicious app that registered the same custom URI scheme, or anything that can read the redirect (a logged URL, a compromised browser extension).
- Such an attacker can **intercept the code** and exchange it for tokens itself.
- This is **authorization-code interception**.

**The fix:** make the code useless without a secret the attacker never saw. The client creates this secret *per request*.

| Step | What the client does | What the server does |
|---|---|---|
| 1 | Generate a high-entropy random `code_verifier` (43–128 chars) and keep it **in memory** | — |
| 2 | Compute `code_challenge = BASE64URL(SHA-256(code_verifier))` | — |
| 3 | Call `/authorize?...&code_challenge=<challenge>&code_challenge_method=S256` | Stores the challenge **alongside the issued code** |
| 4 | Receive the authorization code on the redirect | — |
| 5 | Call `/token` with `code=<code>&code_verifier=<the raw verifier>` | Recomputes `SHA-256(code_verifier)` and compares with the stored challenge — mismatch ⇒ reject |

🔑 **Why it works:**

- The interceptor sees the `code_challenge` (it is a hash, on a URL) and the `code`.
- It never sees the `code_verifier`. That value existed only in the real client's memory.
- Without it, the attacker cannot exchange the stolen code for tokens.
- PKCE is basically a **one-time, per-request client secret**. The client proves it knew the secret by revealing the pre-image (the original value before hashing).

⚠️ **Always `S256`, never `plain`.** `code_challenge_method=plain` sends the verifier itself as the challenge. So anyone who can see the `/authorize` request (a log, browser history, a proxy) also gets the verifier. `S256` stays safe even then. RFC 7636 allows `plain` only for clients that cannot do SHA-256. The latest OAuth 2.1 draft (-16) forbids it.

---

</details>
<br/>

---

</details>

---

2. **🤖 What is the Client Credentials grant in OAuth2? When is it used? ⚡**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

The Client Credentials grant is used for **machine-to-machine (M2M) communication**, where no user is involved. The client application authenticates with its own credentials (client ID + client secret). It gets an access token in return.

```mermaid
sequenceDiagram
    participant C as Client (Service A)
    participant AS as Authorization Server
    participant RS as Resource Server (Service B)

    C->>AS: POST /token (grant_type=client_credentials, client_id, client_secret, scope)
    AS->>AS: Validate client credentials
    AS-->>C: { access_token, expires_in, token_type: "Bearer" }
    C->>RS: GET /api/data (Authorization: Bearer access_token)
    RS->>RS: Validate token
    RS-->>C: { response data }
```

```
POST https://auth-server.com/oauth2/token
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&
client_id=SERVICE_A_CLIENT_ID&
client_secret=SERVICE_A_SECRET&
scope=read:users write:logs
```

📋 **When to use Client Credentials:**

| Use Case | Example |
|----------|---------|
| 🔗 Service-to-service communication | Order Service calls Inventory Service |
| ⏰ Scheduled background jobs | Nightly batch processing calling an API |
| 🤖 Server-side automation | CI/CD pipeline accessing deployment API |
| 📊 Reporting/analytics services | Dashboard service fetching metrics from data service |
| 🔧 Infrastructure management | Monitoring service calling health check APIs |

⚠️ **When NOT to use Client Credentials:**

- ❌️ When a user is involved (use Authorization Code flow instead).
- ❌️ When you need user-specific permissions (Client Credentials has no user context).
- ❌️ From browser-based apps (client secret would be exposed).

```java
// Spring Boot — configuring a service as OAuth2 client with Client Credentials
// application.yml
spring:
  security:
    oauth2:
      client:
        registration:
          inventory-service:
            client-id: order-service
            client-secret: ${CLIENT_SECRET}
            authorization-grant-type: client_credentials
            scope: read:inventory
        provider:
          inventory-service:
            token-uri: https://auth.myapp.com/oauth2/token
```

```java
// Using WebClient with OAuth2 client credentials
@Configuration
public class WebClientConfig {

    @Bean
    WebClient webClient(OAuth2AuthorizedClientManager authorizedClientManager) {
        ServletOAuth2AuthorizedClientExchangeFilterFunction oauth2Client =
            new ServletOAuth2AuthorizedClientExchangeFilterFunction(authorizedClientManager);
        oauth2Client.setDefaultClientRegistrationId("inventory-service");

        return WebClient.builder()
            .apply(oauth2Client.oauth2Configuration())
            .build();
    }
}
```

⚠️ **Where the `OAuth2AuthorizedClientManager` comes from:**
- Since Spring Security 6.2 there is a default bean. Before 6.2 you must declare one yourself.
- The default (`DefaultOAuth2AuthorizedClientManager`) needs the current `HttpServletRequest`. So it fails in a `@Scheduled` job or any thread outside a web request.
- For those, declare an `AuthorizedClientServiceOAuth2AuthorizedClientManager` bean.

🔑 **Key Point:** In the Client Credentials flow, there is **no resource owner** (no user). The access token represents the application itself, not a user. The authorization server sets the token's permissions (scopes) per registered client. It does not set them per user.

🎯 **Interview Tip:** Show the difference clearly: "Authorization Code flow is for user-facing applications (user delegates access), while Client Credentials is for server-to-server communication (no user involved)." This shows you understand the basic design idea of OAuth2.

---

</details>

---

3. **🏢 What are the four OAuth2 roles? Explain each with examples. ⚡**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

OAuth2 defines four separate roles that take part in the authorization flow. You must understand these roles to design secure authentication systems.

| Role | Description | Real-World Example |
|------|-------------|-------------------|
| **Resource Owner** 👤 | The entity that owns the protected resource and can grant access to it | You — the person who owns a Google Calendar |
| **Client** 💻 | The application that wants to access the resource on behalf of the resource owner | Calendly — wants to read your Google Calendar |
| **Authorization Server** 🔐 | Issues access tokens after authenticating the resource owner and obtaining consent | Google's OAuth2 server (`accounts.google.com`) |
| **Resource Server** 🗄️ | Hosts the protected resources/APIs and validates access tokens | Google Calendar API (`calendar.googleapis.com`) |

```mermaid
graph TD
    RO["Resource Owner<br/>(You)"] -->|1. Login + Consent| AS["Authorization Server<br/>(Google OAuth)"]
    AS -->|2. Auth Code| C["Client<br/>(Calendly App)"]
    C -->|3. Exchange Code| AS
    AS -->|4. Access Token| C
    C -->|5. API Call + Token| RS["Resource Server<br/>(Google Calendar API)"]
    RS -.->|6. Introspect — opaque tokens only| AS
    RS -->|7. Calendar Data| C

    classDef purple fill:#7C3AED,stroke:#7C3AED,color:#fff
    classDef cyan fill:#0891B2,stroke:#0891B2,color:#fff
    classDef green fill:#059669,stroke:#059669,color:#fff
    classDef orange fill:#D97706,stroke:#D97706,color:#fff

    class RO purple
    class C cyan
    class AS orange
    class RS green
```

1️⃣ **Resource Owner (👤 User):**

- The human (or entity) who owns the data.
- Grants or denies access to the client.
- Example: You authorize Calendly to read your Google Calendar events.
- In Spring Security: The user who logs in and clicks "Allow."

2️⃣ **Client (💻 Application):**

- The application requesting access to the resource.
- Must be registered with the authorization server (receives `client_id` and `client_secret`).
- Two types:
  - **Confidential client** — Can securely store a secret (server-side app).
  - **Public client** — Cannot store a secret (SPA, mobile app) — uses PKCE.

3️⃣ **Authorization Server (🔐 Token Issuer):**

- Authenticates the resource owner.
- Issues access tokens and refresh tokens.
- Manages client registrations and scopes.
- Examples: Google OAuth, Keycloak, Auth0, Okta, Spring Authorization Server.
- Key endpoints:
  - `/authorize` — User login and consent.
  - `/token` — Token issuance.
  - `/userinfo` — User profile (OIDC).
  - `/.well-known/openid-configuration` — Discovery endpoint.

⚠️ **Note the dashed arrow 6.**

- When the Resource Server calls the Authorization Server on every request, that is **introspection**. This is the *opaque-token* path.
- With a JWT access token, the Resource Server validates the signature **locally**. It fetches the public key once from the JWKS endpoint and caches it.
- So arrow 6 does not happen per request.
- Candidates often redraw this diagram from memory. Drawing arrow 6 as a solid line is the most common mistake.
- See §5 Q4 for the JWT-vs-opaque comparison.

4️⃣ **Resource Server (🗄️ API):**

- Hosts the protected API endpoints.
- Validates the access token on every request.
- Returns the protected resource if the token is valid and has sufficient scope.
- In Spring: Configured with `spring-boot-starter-oauth2-resource-server`.

📝 **Note:** In many architectures, the **Authorization Server** and **Resource Server** are the same application (especially in monoliths). In microservices, they are usually separate. There is one central auth server and many resource servers.

🎯 **Interview Tip:** Use a real-world comparison: "Think of it like a valet parking system. You (Resource Owner) give the valet (Client) a special key (Access Token) that only opens the doors (limited scope) but cannot open the trunk. The parking authority (Authorization Server) issued the special key, and the car (Resource Server) accepts it."

---

</details>

---

4. **⚙️ How do you configure a Spring Boot application as an OAuth2 Resource Server? 🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

A Resource Server protects APIs. It checks access tokens that an Authorization Server issued. Spring Boot provides `spring-boot-starter-oauth2-resource-server` for this.

**Two token validation strategies:**

| Strategy | Description | Use Case |
|----------|-------------|----------|
| **JWT (local validation)** | Validate JWT signature locally using public key/JWKS | ✅ Preferred — no network call per request |
| **Opaque token (introspection)** | Call auth server's `/introspect` endpoint to validate | When tokens are not JWTs or need real-time revocation |

1️⃣ **JWT-based Resource Server (Recommended):**

Add the dependency:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-oauth2-resource-server</artifactId>
</dependency>
```

```yaml
# application.yml
spring:
  security:
    oauth2:
      resourceserver:
        jwt:
          # Option A: JWKS URI (auto-discovers public keys)
          jwk-set-uri: https://auth-server.com/.well-known/jwks.json

          # Option B: Issuer URI (auto-discovers everything)
          # issuer-uri: https://auth-server.com
```

```java
@Configuration
@EnableWebSecurity
@EnableMethodSecurity
public class ResourceServerConfig {

    @Bean
    SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        return http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/public/**").permitAll()
                // ⚠️ These MUST match whatever the converter below produces.
                // With the ROLE_/roles converter installed, no SCOPE_* authority
                // exists any more — so hasRole(...), not hasAuthority("SCOPE_...").
                .requestMatchers("/api/admin/**").hasRole("ADMIN")
                .requestMatchers("/api/**").hasRole("USER")
                .anyRequest().authenticated()
            )
            .oauth2ResourceServer(oauth2 -> oauth2
                .jwt(jwt -> jwt.jwtAuthenticationConverter(jwtAuthConverter()))
            )
            .build();
    }

    // Convert JWT claims to Spring Security authorities.
    // This REPLACES the default mapping (scope claim → SCOPE_ prefix) entirely.
    @Bean
    JwtAuthenticationConverter jwtAuthConverter() {
        JwtGrantedAuthoritiesConverter authoritiesConverter =
            new JwtGrantedAuthoritiesConverter();
        authoritiesConverter.setAuthorityPrefix("ROLE_");        // was SCOPE_
        authoritiesConverter.setAuthoritiesClaimName("roles");   // was scope / scp

        JwtAuthenticationConverter converter = new JwtAuthenticationConverter();
        converter.setJwtGrantedAuthoritiesConverter(authoritiesConverter);
        return converter;
    }
}
```

⚠️ **The trap in this snippet — pick one convention and keep to it.**

- Installing a `JwtGrantedAuthoritiesConverter` with `setAuthorityPrefix("ROLE_")` + `setAuthoritiesClaimName("roles")` **replaces** the default `scope`→`SCOPE_` mapping.
- After that, `hasAuthority("SCOPE_admin")` can never match. There is no `SCOPE_*` authority left in the `Authentication`.
- So those endpoints return **403 forever**.

Either:

- **drop the custom converter** and keep the defaults, matching on `hasAuthority("SCOPE_admin")` / `hasAuthority("SCOPE_read")`; **or**
- **keep the converter** and match on `hasRole("ADMIN")` (equivalently `hasAuthority("ROLE_ADMIN")`), as above.

Mixing them is the most common way a working Resource Server config ends up returning 403 on its protected endpoints. Code review does not catch it, because each half looks correct on its own.

2️⃣ **Opaque Token (Introspection-based):**

```yaml
spring:
  security:
    oauth2:
      resourceserver:
        opaquetoken:
          introspection-uri: https://auth-server.com/oauth2/introspect
          client-id: resource-server
          client-secret: ${INTROSPECTION_SECRET}
```

```java
@Bean
SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    return http
        .authorizeHttpRequests(auth -> auth
            .anyRequest().authenticated()
        )
        .oauth2ResourceServer(oauth2 -> oauth2
            .opaqueToken(Customizer.withDefaults())
        )
        .build();
}
```

📋 **JWT vs Opaque Token comparison:**

| Feature | JWT (Local) 🅰️ | Opaque (Introspection) 🅱️ |
|---------|---------------|--------------------------|
| **Validation** | ✅ Local (signature check) | ⚠️ Remote (HTTP call to auth server) |
| **Performance** | ✅ Fast (no network call) | ⚠️ Slower (network call per request) |
| **Revocation** | ⚠️ Delayed (until token expires) | ✅ Immediate (real-time check) |
| **Token Size** | ⚠️ Larger (contains claims) | ✅ Smaller (opaque string) |
| **Dependency** | ✅ Only needs public key | ⚠️ Auth server must be available |

🔑 **Key Point:** The `JwtAuthenticationConverter` is the class that maps JWT claims to Spring Security authorities. By default, Spring reads the `scope` claim with the `SCOPE_` prefix. Your JWT may have a `roles` claim with values like `ADMIN`. Then you need a custom converter to map them to `ROLE_ADMIN`.

🎯 **Interview Tip:** Say that JWT-based validation is preferred. It is **stateless** and needs no network call. But you may need **immediate token revocation** (e.g., in banking). Then opaque tokens with introspection give you real-time control. The cost is an extra network hop per request.

---

</details>

---

5. **🆔 What is OpenID Connect (OIDC)? How does it relate to OAuth2? ⚡**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

OpenID Connect (OIDC) is an **identity layer built on top of OAuth2**. OAuth2 is about **authorization** (what can you access?). OIDC adds **authentication** (who are you?).

🧠 **In Simple Words:**

- **OAuth2** = "I authorize this app to access my data" (but the app does not know who I am).
- **OIDC** = "I authorize this app AND tell it who I am" (authentication + authorization).

| Feature | OAuth2 🅰️ | OpenID Connect (OIDC) 🅱️ |
|---------|-----------|--------------------------|
| **Purpose** | Authorization (access delegation) | Authentication + Authorization |
| **Answers** | "What can this app access?" | "Who is this user?" + "What can this app access?" |
| **Token** | Access Token | Access Token + **ID Token** |
| **ID Token** | ❌️ Not part of OAuth2 | ✅ JWT containing user identity claims |
| **UserInfo Endpoint** | ❌️ No standard endpoint | ✅ `/userinfo` endpoint |
| **Discovery** | ⚠️ Not in the core spec — added later by RFC 8414 (`/.well-known/oauth-authorization-server`) | ✅ `/.well-known/openid-configuration` |
| **Scope** | Custom scopes (e.g., `read`, `write`) | `openid` scope (required) + `profile`, `email` |
| **Built On** | Standalone protocol | OAuth2 + additional standards |

📋 **What OIDC adds to OAuth2:**

1️⃣ **ID Token** — A JWT that contains user identity claims:

```json
{
  "iss": "https://accounts.google.com",
  "sub": "1234567890",
  "aud": "your-client-id",
  "exp": 1711234567,
  "iat": 1711230967,
  "email": "john@gmail.com",
  "name": "John Doe",
  "picture": "https://lh3.googleusercontent.com/photo.jpg",
  "email_verified": true
}
```

2️⃣ **Standard scopes:**

| Scope | Claims Returned |
|-------|----------------|
| `openid` | `sub` (required for OIDC) |
| `profile` | `name`, `family_name`, `given_name`, `picture` |
| `email` | `email`, `email_verified` |
| `address` | `address` (structured) |
| `phone` | `phone_number`, `phone_number_verified` |

3️⃣ **Discovery endpoint** — `/.well-known/openid-configuration` returns all supported endpoints, scopes, and algorithms.

**Spring Boot OIDC Login configuration:**

```yaml
# application.yml
spring:
  security:
    oauth2:
      client:
        registration:
          google:
            client-id: ${GOOGLE_CLIENT_ID}
            client-secret: ${GOOGLE_CLIENT_SECRET}
            scope: openid, profile, email
```

```java
@Configuration
@EnableWebSecurity
public class OidcSecurityConfig {

    @Bean
    SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        return http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/", "/login").permitAll()
                .anyRequest().authenticated()
            )
            .oauth2Login(Customizer.withDefaults())  // OIDC login
            .build();
    }
}
```

```java
// Accessing OIDC user information in a controller
@GetMapping("/user")
public Map<String, Object> getUserInfo(
        @AuthenticationPrincipal OidcUser oidcUser) {
    return Map.of(
        "name", oidcUser.getFullName(),
        "email", oidcUser.getEmail(),
        "picture", oidcUser.getPicture(),
        "claims", oidcUser.getClaims()
    );
}
```

🔑 **Key Point:** The `openid` scope is what separates an OIDC request from a plain OAuth2 request. When you include `scope=openid`, the authorization server returns an **ID Token** along with the access token. Without the `openid` scope, you only get an access token (plain OAuth2).

🎯 **Interview Tip:** The simplest way to explain how they relate: "OIDC is a thin identity layer on top of OAuth2. It adds an ID token and a `/userinfo` endpoint. OAuth2 answers 'what can you access?', OIDC adds 'who are you?'"

---

</details>

---

<a id="oauth-for-services-and-ai-agents"></a>

## 6. OAuth for Services and AI Agents

> This section goes past the basics in §5. It covers what a senior engineer at an identity company is asked: OAuth 2.1, token audience, JWT validation, token exchange, sender-constrained tokens, and how AI agents get access. PKCE mechanics are in the §5 Q1 doubt. The `alg: none` attack is in the §3 Q2 doubt. Refresh token rotation code is in §3 Q4.

1. **📜 What changes in OAuth 2.1 compared to OAuth 2.0? Is it a final standard? 🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

OAuth 2.1 is **not a new protocol**. It collects OAuth 2.0 (RFC 6749), Bearer Token Usage (RFC 6750) and the security fixes learned since 2012 into one document. It removes the unsafe options.

⚠️ **Status:** OAuth 2.1 is still an **IETF Internet-Draft**, not an RFC. The latest version is `draft-ietf-oauth-v2-1-17` (31 October 2026). Many specs already use it. For example, the MCP authorization spec builds on it.

📋 **The main changes (from oauth.net/2.1):**

| # | Change | Why |
|---|---|---|
| 1 | **PKCE is required** for every client that uses the authorization code flow | Stops authorization-code interception and code injection. It also helps confidential clients |
| 2 | **Redirect URIs must match exactly** (string compare) | Wildcard or prefix matching let attackers send the code to their own URL. Exception: the port of a loopback URI (`127.0.0.1`) may change |
| 3 | **Implicit grant removed** (`response_type=token`) | It put the access token in the URL fragment. Browser history, logs and the `Referer` header could leak it |
| 4 | **Password grant removed** (Resource Owner Password Credentials) | The app sees the user's password. It also cannot work with MFA or SSO |
| 5 | **No bearer tokens in the URL query string** | URLs end up in logs and proxies |
| 6 | **Refresh tokens for public clients must be sender-constrained or rotated** | A stolen refresh token from a SPA or mobile app must be useless or detectable |
| 7 | Client types are simpler: a client is **confidential** if it has credentials, **public** if not | Removes the old "credentialed client" confusion |

🔑 **What did *not* change:**

- The authorization code flow, client credentials flow and refresh tokens work the same way.
- A correct OAuth 2.0 setup that already follows the Security BCP (RFC 9700) is almost OAuth 2.1 already.

🧠 **What replaces the removed grants:**

| Removed | Use instead |
|---|---|
| Implicit (SPA) | Authorization code + PKCE |
| Password (first-party login form) | Authorization code + PKCE, with the login page on the authorization server |
| Password (scripts, CI jobs) | Client credentials (no user) or Device Authorization Grant (RFC 8628) for devices without a browser |

🎯 **What to say:** "OAuth 2.1 is still a draft. It is OAuth 2.0 minus the unsafe parts: PKCE for every code flow, exact redirect URI match, no implicit or password grant, no tokens in the query string, and refresh tokens for public clients must be rotated or sender-constrained."

---

</details>

---

2. **🎫 Access token vs refresh token vs ID token — who reads each one, and how long should each live? 🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

The three tokens have **different readers**. Most token bugs come from sending a token to the wrong reader.

| | Access token | Refresh token | ID token (OIDC) |
|---|---|---|---|
| **Purpose** | Call an API | Get a new access token | Tell the **client** who the user is |
| **Who reads it** | The **resource server** (API) | Only the **authorization server** | Only the **client** |
| **`aud` (audience)** | The API | — (often opaque) | The client's `client_id` |
| **Format** | JWT (RFC 9068, `typ: at+jwt`) or opaque | Usually opaque | Always a JWT |
| **Sent to an API?** | ✅ Yes, `Authorization: Bearer` | ❌️ Never | ❌️ Never |
| **Typical lifetime** | 5–60 minutes | Hours to days (often 8–24 h idle, up to 30–90 days max) | Short (minutes to 1 hour). Used once at login |

⚠️ **Two common mistakes:**

1. **Sending the ID token to an API.**
   - The ID token's `aud` is the client, not the API.
   - An API that accepts it skips the audience check. Also, an ID token carries no scopes.
   - Rule: an API accepts **access tokens only**.
2. **Sending the refresh token anywhere except the token endpoint.**
   - OAuth 2.1 says refresh tokens are never sent to resource servers.

🔑 **Why access tokens are short:**

- A JWT access token cannot be recalled after it is issued (see §3 Q5).
- A short life limits how long a stolen token works.
- The refresh token keeps the user logged in without a new login.

🔄 **Refresh token rotation and reuse detection** (code in §3 Q4):

| Step | What happens |
|---|---|
| 1 | Client uses refresh token `RT1` → gets new access token + **new** `RT2`. `RT1` is now invalid |
| 2 | An attacker who stole `RT1` tries to use it |
| 3 | The server sees a **used** token. It cannot tell who is the attacker and who is the real user |
| 4 | So it **revokes the whole token family** (`RT2` too). The real user must log in again |

📏 **How to choose lifetimes:**

| Factor | Shorter | Longer |
|---|---|---|
| Risk of the API (payments, admin) | ✅ | |
| Can the token be revoked fast (opaque + introspection)? | | ✅ possible |
| Load on the authorization server | | ✅ fewer refresh calls |
| Sender-constrained token (DPoP, mTLS)? | | ✅ theft is less useful |

🎯 **What to say:** "Access token goes to the API, refresh token goes only to the token endpoint, ID token stays with the client. Access tokens live minutes, refresh tokens live longer but rotate on every use, and reuse of an old one revokes the whole family."

---

</details>

---

3. **🎯 What is the difference between scopes, audience and claims? What are resource indicators (RFC 8707)? 🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

They answer three different questions about a token.

| Concept | Question it answers | Where it lives | Example |
|---|---|---|---|
| **Audience (`aud`)** | **Which API** may accept this token? | `aud` claim | `https://payments.example.com` |
| **Scope** | **What actions** may the client do there? | `scope` (or `scp`) claim | `payments:read payments:write` |
| **Claims** | **Facts** about the user, client or token | Any claim | `sub`, `client_id`, `roles`, `tenant_id`, `exp` |

🔑 **Why API B must reject a token made for API A:**

- Suppose both APIs trust the same authorization server, and B checks only the signature and `exp`.
- Then any token the server issued works at B. A token for a low-risk API (A) becomes a key for B.
- Worse: if A is compromised, the attacker can **replay** every token A received at B.
- So every resource server must check that **its own identifier is in `aud`**. Spring does **not** check `aud` by default (see Q4).

⚠️ **Scope alone is not enough.** `read` at API A and `read` at API B are the same string. Only `aud` tells them apart. Many teams use names like `payments:read` for this reason, but the real protection is `aud`.

📋 **Resource indicators (RFC 8707):**

The client tells the authorization server **where** it will use the token. It sends a `resource` parameter.

```
POST /oauth2/token
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code
&code=SplxlOBeZQQYbYS6WxSbIA
&redirect_uri=https%3A%2F%2Fclient.example.org%2Fcb
&code_verifier=dBjftJeZ4CVP-mB92K27uhbUJU1p1r_wW1gFWFOEjXk
&resource=https%3A%2F%2Fpayments.example.com
```

| Rule | Detail |
|---|---|
| Format | An **absolute URI**, no fragment (`#`), and should have no query |
| Where it is sent | Authorization request **and** token request (any grant type) |
| Many values | Allowed, but the RFC prefers **one**. A token with many audiences works at all of them |
| What the server does | Sets the token's `aud` to that resource, and may cut the scopes to what that API needs |
| Error | `invalid_target` if the resource is unknown or not allowed |

🤖 **Why this matters for AI agents and MCP:** the MCP authorization spec says MCP clients **MUST** send `resource` (the MCP server's URI) in both requests. MCP servers **MUST** reject tokens whose audience is not them.

🎯 **What to say:** "Audience says which API, scope says which actions, claims are the facts. Every API must check that it is in `aud`, otherwise a token for one service works at every service. RFC 8707 lets the client ask for a token for one specific resource."

---

</details>

---

4. **🔍 How does a resource server validate a JWT access token? Show the Spring Security config with audience validation. 🔥🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

Validation has two parts: **is the token genuine** (signature) and **is it for me, right now** (claims). Do them in this order.

| # | Check | How | Fail → |
|---|---|---|---|
| 1 | **Algorithm** is on my allow-list | Compare the header `alg` with a fixed list (e.g. only `RS256`). Never trust `alg` from the token | 401 |
| 2 | **Signature** | Find the public key by the header `kid` in the issuer's **JWKS** (JSON Web Key Set). Verify | 401 |
| 3 | **`iss`** equals my trusted issuer, exactly | String compare | 401 |
| 4 | **`aud`** contains my API identifier | List contains | 401 |
| 5 | **`exp`** is in the future, **`nbf`** is in the past | Allow a small **clock skew** (Spring: 60 s) | 401 |
| 6 | **Token type** is an access token | RFC 9068 header `typ: at+jwt`, if your server sets it. Stops ID tokens being used as access tokens | 401 |
| 7 | **Scopes / roles** allow this endpoint | Authorization rules | **403** |

⚠️ **Algorithm confusion** (full detail in the §3 Q2 doubt):

- `alg: none` → an unsigned token. It must always be rejected.
- RS256 → HS256 → the attacker signs with HMAC and uses the **public key** as the HMAC secret. A library that trusts the header `alg` accepts it.
- Fix: the server picks the algorithm, not the token. `NimbusJwtDecoder` trusts **only `RS256`** by default.

🔑 **JWKS, `kid` and key rotation:**

- The authorization server publishes its public keys at `jwks_uri`. Each key has a `kid` (key ID).
- The token header says which `kid` signed it.
- **Rotation:** the server publishes the new key first, then starts signing with it, then removes the old key after the longest token lifetime.
- **Caching:** do not fetch JWKS on every request. Spring caches the JWK set **in memory for 5 minutes**. When the server publishes new keys, Spring picks them up without a restart.
- ⚠️ Do not refetch on **every** unknown `kid`. An attacker can send random `kid` values and make you flood the JWKS endpoint. Limit how often you refetch.

**Spring Security 6.x — what is checked by default:**

| Checked by default | Not checked by default |
|---|---|
| ✅ Signature (RS256), `iss`, `exp`, `nbf` | ❌️ `aud` |

**Option A — Spring Boot property (Boot 3.x):**

```yaml
spring:
  security:
    oauth2:
      resourceserver:
        jwt:
          issuer-uri: https://idp.example.com
          audiences: https://payments.example.com
```

**Option B — Java config (more control: audience, clock skew, algorithm):**

```java
@Configuration
public class JwtDecoderConfig {

    private static final String ISSUER = "https://idp.example.com";
    private static final String AUDIENCE = "https://payments.example.com";

    @Bean
    JwtDecoder jwtDecoder() {
        NimbusJwtDecoder decoder = NimbusJwtDecoder.withIssuerLocation(ISSUER)
            .jwsAlgorithm(SignatureAlgorithm.RS256)   // allow-list, not the token's alg
            .build();

        OAuth2TokenValidator<Jwt> audience =
            new JwtClaimValidator<List<String>>(JwtClaimNames.AUD,
                aud -> aud != null && aud.contains(AUDIENCE));

        OAuth2TokenValidator<Jwt> validator = new DelegatingOAuth2TokenValidator<>(
            new JwtTimestampValidator(Duration.ofSeconds(30)),   // exp + nbf, 30 s skew
            new JwtIssuerValidator(ISSUER),
            audience);

        decoder.setJwtValidator(validator);
        return decoder;
    }
}
```

⚠️ **The trap:** `setJwtValidator(...)` **replaces** the default validators. If you pass only the audience validator, Spring stops checking `iss`, `exp` and `nbf`. Always combine them. You can start from `JwtValidators.createDefaultWithIssuer(ISSUER)` and add the audience validator with `DelegatingOAuth2TokenValidator`.

🎯 **What to say:** "First the signature: fixed algorithm list, key picked by `kid` from a cached JWKS. Then the claims: exact `iss`, my API in `aud`, `exp` and `nbf` with a small clock skew. Spring does not check `aud` by default, so I add a `JwtClaimValidator` and keep the default validators with it."

---

</details>

---

5. **🔎 How does token introspection (RFC 7662) work, and when do you choose opaque tokens over JWTs? ⚡**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

An **opaque token** is a random string. It means nothing to the API. To learn what it means, the API asks the authorization server. That call is **introspection** (RFC 7662). The basic JWT-vs-opaque table is in §5 Q4. This answer covers how introspection works and what to watch for.

**The request:**

```
POST /oauth2/introspect
Authorization: Basic cmVzb3VyY2Utc2VydmVyOnNlY3JldA==
Content-Type: application/x-www-form-urlencoded

token=mF_9.B5f-4.1JqM&token_type_hint=access_token
```

| Rule | Why |
|---|---|
| HTTP **POST**, form parameters `token` and optional `token_type_hint` | Keeps the token out of the URL |
| The **resource server must authenticate** to the endpoint | Otherwise anyone can test stolen or guessed tokens |
| TLS is required | The token is a secret |

**The response:**

```json
{
  "active": true,
  "client_id": "agent-app",
  "sub": "user-123",
  "scope": "payments:read",
  "aud": "https://payments.example.com",
  "iss": "https://idp.example.com",
  "exp": 1793000000
}
```

- `active` is the **only required** field.
- For an expired, revoked or unknown token, the server returns just `{"active": false}`. It gives **no reason**, so it does not leak information.
- You must still check `aud` and `scope` yourself.

⚠️ **Caching introspection results:**

- The RFC allows caching to cut load.
- But a revoked token stays accepted until your cache entry ends. That removes the main benefit of opaque tokens.
- Never cache past the token's `exp`. Use a short cache time (seconds), or none for high-risk APIs.

📋 **Opaque + introspection vs JWT — when to pick each:**

| Need | Pick |
|---|---|
| Revoke access **at once** (logout, fraud, employee leaves) | ✅ Opaque |
| Hide claims from the client (JWT payload is only Base64URL, anyone can read it) | ✅ Opaque |
| Very high request rate, low latency, API must work if the auth server is slow | ✅ JWT |
| Many APIs across regions | ✅ JWT (no central call) |
| Small token size on the wire | ✅ Opaque |

💡 **A common mix — the "phantom token" pattern:**

- The outside client gets an **opaque** token, so no claims leak.
- The **API gateway** introspects it once and passes a short-lived **JWT** to internal services.
- Internal services validate the JWT locally.

🎯 **What to say:** "The API posts the token to `/introspect` and authenticates itself. It gets back `active` plus claims. Inactive tokens return only `active: false`. Opaque tokens give instant revocation and hide claims; the cost is one network call per request, which caching reduces at the price of slower revocation."

---

</details>

---

6. **🔁 What is OAuth 2.0 Token Exchange (RFC 8693)? Explain delegation vs impersonation and the `act` claim. 🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

Token Exchange lets a service **trade one token for another**. A typical case: service A gets a user's token. A must call service B **for that user**. A should not forward the user's token (wrong audience, too many scopes). So A asks the authorization server for a **new token for B**.

```mermaid
sequenceDiagram
    participant U as User
    participant A as Service A (or AI agent)
    participant AS as Authorization Server
    participant B as Service B

    U->>A: Request + access token (aud = A)
    A->>AS: POST /token grant_type=token-exchange<br/>subject_token = user token<br/>actor_token = A's own token<br/>audience = B, scope = orders:read
    AS->>AS: Check policy: may A act for this user at B?
    AS-->>A: New token (aud = B, sub = user, act.sub = A)
    A->>B: Call with the new token
    B->>B: Validate: aud = B, sub = user, act = A
    B-->>A: Response
```

📋 **Request parameters:**

| Parameter | Required? | Meaning |
|---|---|---|
| `grant_type` | ✅ | `urn:ietf:params:oauth:grant-type:token-exchange` |
| `subject_token` | ✅ | The token of the party **on whose behalf** the call is made (usually the user) |
| `subject_token_type` | ✅ | e.g. `urn:ietf:params:oauth:token-type:access_token` or `...:id_token` |
| `actor_token` | Optional | The token of the party **doing the acting** (service A, the agent) |
| `actor_token_type` | Only if `actor_token` is sent | Type of the actor token |
| `resource` / `audience` | Optional | The target service. `resource` is a URI, `audience` is a logical name |
| `scope` | Optional | Scopes wanted at the target. Ask for **fewer** than the subject token has |
| `requested_token_type` | Optional | The type of token wanted back |

The response has the usual `access_token` plus a **required** `issued_token_type`.

🔑 **Delegation vs impersonation:**

| | Impersonation | Delegation |
|---|---|---|
| Who the new token says it is | **Only the user**. B cannot tell A was involved | The user **and** A. A keeps its own identity |
| `act` claim | ❌️ Absent | ✅ Present |
| Audit trail | ❌️ "User did X" | ✅ "A did X for the user" |
| Use for AI agents | ⚠️ Avoid | ✅ Preferred |

**The `act` (actor) claim:**

```json
{
  "aud": "https://orders.example.com",
  "sub": "user-123",
  "scope": "orders:read",
  "act": {
    "sub": "agent-travel-bot",
    "act": {
      "sub": "gateway-service"
    }
  }
}
```

- The **top-level `act`** is the **current** actor. Nested `act` objects are **earlier** actors in the chain.
- Only the top-level claims and the current actor are used for access decisions. Earlier actors are for audit only.
- Claims like `exp`, `nbf` and `aud` have no meaning inside `act`.

🤖 **Where it fits for AI agents:** an agent receives a user's token. For each tool or API it calls, it exchanges that token for a **new, narrow, short-lived** token. That token has the tool's audience, only the scopes it needs, and `act` naming the agent. The downstream API sees "agent X, acting for user Y". It can apply rules such as "agents may read orders but not cancel them".

🎯 **What to say:** "Token Exchange trades a subject token, and optionally an actor token, for a new token for a different audience with fewer scopes. With delegation, the new token carries an `act` claim, so the downstream service knows who is acting for whom. That is the right model for an agent acting for a user."

---

</details>

---

7. **🤖 How should an AI agent get access to APIs on behalf of a user? What can go wrong? 🔥🔥**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

📋 **Pick the grant:**

| Situation | Grant | Token says |
|---|---|---|
| Agent works for itself (nightly report, no user) | **Client credentials** | `sub` = the agent |
| Agent acts for a user who is present | **Authorization code + PKCE** with user consent | `sub` = the user, `client_id` = the agent |
| Agent (or MCP server) calls another API for the user | **Token Exchange** (RFC 8693), delegation | `sub` = the user, `act` = the agent |
| Enterprise: the company IdP decides which agent may reach which app | **ID-JAG / Cross App Access** (see below) | Access token from the target app's server |

⚠️ **The main risk — confused deputy and token passthrough:**

- A **confused deputy** is a program with power that is tricked into using that power for someone else.
- Example: an MCP server receives the user's token and **forwards the same token** to a downstream API.
- Problems:
  - The token's audience is the MCP server, not the downstream API. Either the API skips its `aud` check (bad), or it fails.
  - The downstream API cannot see that an agent made the call. Audit and rate limits break.
  - A prompt injection in the agent can now use **all** of the user's rights.
- The MCP spec says it plainly: the MCP server **MUST NOT** pass through the token it received. It must get a **separate** token for the upstream API.

🔒 **Rules for agent tokens:**

| Rule | How |
|---|---|
| **Least privilege** | Ask for one audience (`resource`, RFC 8707) and only the scopes this task needs |
| **Short-lived** | Minutes, not hours. Agents can be tricked, so limit the time window |
| **Down-scope on every hop** | Token Exchange to a narrower token at each step. Never widen |
| **Keep the agent visible** | Delegation (`act` claim), not impersonation. Log both user and agent |
| **Sender-constrain** | DPoP or mTLS (Q8), so a leaked token is useless elsewhere |
| **Human approval for high-risk actions** | Payments, deletes, sending email: ask the user to confirm (step-up or an out-of-band approval, e.g. OpenID CIBA). The agent must not approve its own action |
| **Revocable** | The user and the admin can see and revoke the agent's access |

📋 **ID-JAG and Cross App Access (XAA):**

- **ID-JAG** = Identity Assertion JWT Authorization Grant. It is an **IETF OAuth WG draft** (`draft-ietf-oauth-identity-assertion-authz-grant`, revision -06 on 31 October 2026). It is not an RFC yet. Aaron Parecki (Okta) is one of the authors.
- **Cross App Access** is the common name for the pattern. Okta ships it under that name.
- **Problem it solves:** in a company, the user should not click a consent screen for every app-to-app link. The company **IdP** (the one that runs SSO) should decide which app or agent may reach which other app.
- **Flow:**
  1. The user signs in to the client app (or agent) through the IdP. This is the only user step.
  2. The client sends its ID token to the IdP with **Token Exchange** (RFC 8693) and asks for an ID-JAG for the target app.
  3. The client sends the ID-JAG to the **target app's** authorization server with the **JWT Bearer grant** (RFC 7523, `grant_type=urn:ietf:params:oauth:grant-type:jwt-bearer`).
  4. That server checks the IdP's signature and the audience, then issues its own access token.
- **MCP link:** oauth.net calls MCP "Enterprise-Managed Authorization" an MCP-specific profile of Cross App Access.

🎯 **What to say:** "The agent is its own OAuth client. If a user is involved, it gets a delegated token with the user's consent. At every hop it exchanges for a new short-lived token with one audience and fewer scopes, and the `act` claim names the agent. It never forwards the user's token, because that is the confused deputy problem. Risky actions need a human to approve. In companies, ID-JAG lets the IdP control which agent reaches which app."

---

</details>

---

8. **🔐 What are sender-constrained tokens? Compare DPoP (RFC 9449) and mTLS (RFC 8705). ⚡**

<!-- -->
<details>
<summary>Answer</summary>

**Answer:**

A normal **bearer token** works for anyone who holds it, like cash. A **sender-constrained** token is bound to a key that only the real client has. A stolen token alone is useless. The client must also prove it holds the key on every request.

| | **DPoP** (RFC 9449) | **mTLS** (RFC 8705) |
|---|---|---|
| Layer | Application (HTTP header) | Transport (TLS handshake) |
| Client holds | A key pair (often made in the browser or app) | An X.509 client certificate |
| Proof on each request | A signed JWT in the `DPoP` header. `typ: dpop+jwt`; claims `jti`, `htm` (method), `htu` (URL), `iat`, `ath` (hash of the access token) | The TLS handshake proves the client has the certificate's private key |
| Binding in the token | `cnf.jkt` = SHA-256 thumbprint of the public key | `cnf["x5t#S256"]` = SHA-256 thumbprint of the certificate |
| Auth header | `Authorization: DPoP <token>` | `Authorization: Bearer <token>` over the mTLS connection |
| `token_type` in token response | `DPoP` | `Bearer` |
| Works in a browser SPA | ✅ Yes | ❌️ No practical way |
| Replay protection | `jti` + `iat` + optional server `nonce` | Built into TLS |
| Hard part | Proof checks in app code; replay cache | Certificate issuing and rotation; TLS ending at a load balancer hides the certificate |
| Best fit | SPAs, mobile apps, AI agents, public clients | Service-to-service inside a company, banking APIs (Open Banking / FAPI) |

🔑 **Refresh tokens with DPoP:** for a public client, the server **must bind** the refresh token to the DPoP key. The client must sign a proof with the same key every time it refreshes. This is one way to meet the OAuth 2.1 rule "public-client refresh tokens must be sender-constrained or rotated".

⚠️ **mTLS behind a load balancer:** if TLS ends at the load balancer, the service never sees the client certificate. The load balancer must pass the certificate (or its thumbprint) in a trusted header. The service must accept that header **only** from the load balancer.

🎯 **What to say:** "Bearer tokens work for whoever holds them. DPoP and mTLS bind the token to a key: DPoP with a signed proof JWT per request and `cnf.jkt` in the token, mTLS with the client certificate and `cnf x5t#S256`. DPoP works in browsers and for agents, mTLS fits internal service-to-service traffic."

---

</details>

---
