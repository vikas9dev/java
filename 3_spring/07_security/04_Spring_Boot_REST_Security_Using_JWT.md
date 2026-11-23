# Spring Boot REST Security Using JWT

**Spring Boot REST Security Using JWT** | Securing REST APIs with Spring Security and JSON Web Tokens (JWT) for stateless authentication and authorization.

- [User/Client Register Process](#1-userclient-register-process)
- [JwtUtil Class Code](#2-jwtutil-class-code)
- [JWT Token Generation Without Security](#3-jwt-token-generation-without-security)
- [JWT Token After User Authentication](#4-jwt-token-after-user-authentication)
- [JWT Token Verification from 2nd Request Onwards](#5-jwt-token-verification-from-2nd-request-onwards)

---

## 1. User/Client Register Process

**Model:** `User` (id, name, username, password, roles)

The client must send the above details in JSON format, which will be converted into a `User` class object and saved in the database. The password won't be stored as plain text, instead, it will be encoded using `PasswordEncoder` before saving into the database.

The `roles` field of the `User` class will be a `Set` because one user can have more than one role, therefore a separate table will be created to store the roles.

🏗️ **Project Setup:**

Create a new Spring Starter Project `SpringSecurityJWTMySQL` with the following dependencies:

- 🔧 Spring Boot DevTools
- 📦 Lombok
- 💾 Spring Data JPA
- 🗄️ MySQL Driver
- 🌐 Spring Web

📝 **Note:** We will add Spring Security and JWT-related dependencies (`jjwt-api`, `jjwt-impl` & `jjwt-jackson`) in later stages.

🔗 **GitHub Project URL:** [SpringSecurityJWTMySQL](https://github.com/Know-Program/Spring-Boot-Examples/tree/main/SpringSecurityJWTMySQL)

🔧 **Configuration** (`application.properties`):

```properties
# database details
spring.datasource.url=jdbc:mysql://localhost:3306/test
spring.datasource.username=root
spring.datasource.password=root

# jpa details
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

**Model class:**

```java
package com.example.demo.model;

@Entity
@Data
@AllArgsConstructor
@NoArgsConstructor
@Table(name = "usertab")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Integer id;
    private String name;
    private String username;
    private String password;

    @ElementCollection
    @CollectionTable(
            name = "rolestab",
            joinColumns = @JoinColumn(name = "id")
    )
    private Set<String> roles;
}
```

**Repository:**

```java
package com.example.demo.repo;
public interface UserRepository extends JpaRepository<User, Integer> {}
```

**Service Interface:**

```java
package com.example.demo.service;
public interface IUserService {
    Integer save(User user);
}
```

**Service Implementation:**

```java
package com.example.demo.service;
@Service
public class UserServiceImpl implements IUserService {
    @Autowired
    UserRepository repository;

    @Override
    public Integer save(User user) {
        // TODO: Encode password
        return repository.save(user).getId();
    }

}
```

**RestController:**

```java
@RestController
@RequestMapping("/user")
public class UserRestController {

    @Autowired
    private IUserService service;

    @PostMapping("/save")
    public ResponseEntity<String> saveUser(@RequestBody User user) {
        Integer uid = service.save(user);
        String body = "User " + uid + " saved";
        return new ResponseEntity<String>(body, HttpStatus.CREATED);
    }
}
```

Let us run the application and create a user.

📥 **Request** (`POST http://localhost:8080/user/save`):

```json
{
    "name": "JERRY",
    "username": "jerry12",
    "password": "jerry@123",
    "roles": ["ADMIN","EMP"]
}
```

🧪 **Verify in Database:**

```sql
use test;
select * from usertab;
select * from rolestab;
```

---

## 2. JwtUtil Class Code

To work with JWT in your Spring Boot application, we need to include three dependencies:

| Dependency 📦 | Purpose 📋 |
|---------------|-----------|
| **`jjwt-api`** | Core JWT API |
| **`jjwt-impl`** | Implementation of the JWT API |
| **`jjwt-jackson`** (or `jjwt-gson`) | JSON processing |

**Dependencies:**

Maven (`pom.xml`):

```xml
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-api</artifactId>
    <version>0.11.5</version>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-impl</artifactId>
    <version>0.11.5</version>
    <scope>runtime</scope>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-jackson</artifactId> <!-- or jjwt-gson if you prefer -->
    <version>0.11.5</version>
    <scope>runtime</scope>
</dependency>
```

Gradle (`build.gradle`):

```groovy
implementation 'io.jsonwebtoken:jjwt-api:0.11.5'
runtimeOnly 'io.jsonwebtoken:jjwt-impl:0.11.5'
runtimeOnly 'io.jsonwebtoken:jjwt-jackson:0.11.5'
```

🔧 **Configuration** (`application.properties`):

```properties
# JWT secret key
app.secret=knowprogram_secret_key_extended_to_more_than_64_characters_long_for_security
```

> ⚠️ **Warning:** Since we are going to use `SignatureAlgorithm.HS512`, the length of the secret key value (i.e. value of `app.secret`) must be at least 512 bits (64 characters) long, else we will get an error: `io.jsonwebtoken.security.WeakKeyException: The signing key's size is 344 bits which is not secure enough for the HS512 algorithm.` Consider using `Keys.secretKeyFor(SignatureAlgorithm.HS512)` to create a key guaranteed to be secure enough.

**JwtUtil class:**

```java
package com.example.demo.util;

import java.security.Key;
import java.util.Date;
import java.util.concurrent.TimeUnit;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import io.jsonwebtoken.security.Keys;
import jakarta.annotation.PostConstruct;

@Component
public class JwtUtil {

    @Value("${app.secret}")
    private String secret;

    private Key key;

    @PostConstruct
    public void init() {
        if (secret.length() < 64) {
            throw new IllegalArgumentException(
              "The secret key must be at least 512 bits (64 characters) long.");
        }
        key = Keys.hmacShaKeyFor(secret.getBytes());
    }

    // generate token
    public String generateToken(String subject) {
        return Jwts.builder()
                .setSubject(subject)
                .setIssuer("KnowProgram-PVT")
                .setIssuedAt(new Date(System.currentTimeMillis()))
                .setExpiration(new Date(System.currentTimeMillis() +
                        TimeUnit.MINUTES.toMillis(10)))
                .signWith(key, SignatureAlgorithm.HS512).compact();
    }

    // read claims
    public Claims getClaims(String token) {
        return Jwts.parserBuilder()
                .setSigningKey(key)
                .build()
                .parseClaimsJws(token)
                .getBody();
    }

    // read expire date & time
    public Date getExpDate(String token) {
        return getClaims(token).getExpiration();
    }

    // read subject/username
    public String getUsername(String token) {
        return getClaims(token).getSubject();
    }

    // validate is token expired?
    public boolean isTokenExpired(String token) {
        Date expireDate = getClaims(token).getExpiration();
        return expireDate.before(new Date(System.currentTimeMillis()));
    }

    // validate username in token and database, expDate
    public boolean validateToken(String token, String username) {
        String tokenUserName = getUsername(token);
        return username.equals(tokenUserName) && !isTokenExpired(token);
    }
}
```

🔑 **Key Methods in JwtUtil:**

- 🔐 `generateToken()` — Creates a signed JWT with subject, issuer, issued-at, and expiration claims
- 📖 `getClaims()` — Parses the token and extracts all claims
- 👤 `getUsername()` — Reads the subject (username) from the token
- ⏰ `isTokenExpired()` — Checks if the token's expiration date has passed
- ✅ `validateToken()` — Validates both username match and token expiry

---

## 3. JWT Token Generation Without Security

Let us test by generating a JWT token without security to verify whether the `JwtUtil` class is working correctly or not.

For the `POST /user/login` URL, we will pass a username and password. The controller should take the username, call the `JwtUtil` class `generateToken()` method, and return the token with a message.

Read username and password in JSON format, convert to `UserRequest` object (TODO: validate with database rows). Generate a token and define one message, return this data in JSON format using the `UserResponse` object.

**UserRequest** (HTTP Request JSON Data):

```java
package com.example.demo.model;
import lombok.Data;
@Data
public class UserRequest {
    private String username;
    private String password;
}
```

**UserResponse** (HTTP Response JSON Data):

```java
package com.example.demo.model;
import lombok.Data;
@Data
@AllArgsConstructor
public class UserResponse {
    private String token;
    private String message;
}
```

**UserRestController** (add login endpoint):

```java
@Autowired
private JwtUtil jwtUtil;

// validate user and generate token (login)
@PostMapping("/login")
public ResponseEntity<UserResponse> loginUser(@RequestBody UserRequest request) {
    // TODO: validate with username & password with database
    String token = jwtUtil.generateToken(request.getUsername());
    return ResponseEntity.ok(new UserResponse(token,
            "Success! Generated By KnowProgram"));
}
```

Now, let us make an API call.

📥 **Request** (`POST http://localhost:8080/user/login`):

```json
{
    "username": "abc",
    "password": "mno"
}
```

📤 **Response:**

```json
{
    "token": "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJhYmMiLCJpc3MiOiJLbm93UHJvZ3JhbS1QVlQiLCJpYXQiOjE3MjcyNzc4MzgsImV4cCI6MTcyNzI3ODQzOH0.8cOLyWXzYATM-oVdDH9T2vsLzePYRYfdGoH0XLpdWuYGChhyesEQyDZIAi2UZJifr_L-C3eH3zcd78inZ7R2bw",
    "message": "Success! Generated By KnowProgram"
}
```

---

## 4. JWT Token After User Authentication

```mermaid
sequenceDiagram
    participant C as 🖥️ Client
    participant F as 🛡️ SecurityFilter
    participant SC as ⚙️ SecurityConfig
    participant AM as 🔐 AuthenticationManager
    participant UDS as 👤 UserDetailsService
    participant JWT as 🔑 JwtUtil
    participant DB as 🗄️ Database

    C->>SC: POST /user/save (permitAll)
    SC->>DB: Save user (password encoded)
    DB-->>SC: User saved

    C->>SC: POST /user/login (permitAll)
    SC->>AM: Authenticate(username, password)
    AM->>UDS: loadUserByUsername()
    UDS->>DB: Find user
    DB-->>UDS: User details
    UDS-->>AM: UserDetails
    AM-->>SC: Authentication success
    SC->>JWT: generateToken(username)
    JWT-->>C: JWT Token

    C->>F: GET /user/welcome + Token
    F->>JWT: Validate token
    JWT-->>F: Valid
    F->>UDS: loadUserByUsername()
    UDS-->>F: UserDetails
    F->>F: Set SecurityContext
    F-->>C: Hello User jerry12
```

1️⃣ **Add the Spring Security dependency.**

2️⃣ **AppConfig** — Define a `PasswordEncoder` bean and use it before saving the `User`. Modify the code in `UserServiceImpl` to encode the password before saving.

**AppConfig class:**

```java
package com.example.demo.config;

@Configuration
public class AppConfig {

    @Bean
    PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}
```

💡 **Tip:** To see all TODO in Eclipse/STS: Windows > Show View > Other > Tasks.

3️⃣ **Update Repository and Service interfaces.**

**UserRepository** (add method):

```java
Optional<User> findByUsername(String username);
```

**IUserService** (add method):

```java
Optional<User> findByUsername(String username);
```

4️⃣ **Update UserServiceImpl** — Encode the password before saving, and implement `UserDetailsService`.

```java
package com.example.demo.service;

import java.util.Optional;
import java.util.stream.Collectors;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.core.authority.SimpleGrantedAuthority;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.stereotype.Service;

import com.example.demo.model.User;
import com.example.demo.repo.UserRepository;

@Service
public class UserServiceImpl implements IUserService, UserDetailsService {

    @Autowired
    UserRepository repository;

    @Autowired
    PasswordEncoder passwordEncoder;

    @Override
    public Integer save(User user) {
        // Encode password
        user.setPassword(passwordEncoder.encode(user.getPassword()));
        return repository.save(user).getId();
    }

    @Override
    public Optional<User> findByUsername(String username) {
        return repository.findByUsername(username);
    }

    @Override
    public UserDetails loadUserByUsername(String username)
            throws UsernameNotFoundException {
        User user = findByUsername(username)
                .orElseThrow(() -> new UsernameNotFoundException("User Not Exist"));
        return new org.springframework.security.core.userdetails.User(username,
                user.getPassword(),
                user.getRoles().stream()
                               .map(role -> new SimpleGrantedAuthority(role))
                               .collect(Collectors.toSet())
                );
    }

}
```

5️⃣ **Handle Unauthorized access** — Create an `AuthenticationEntryPoint` implementation.

**InvalidUserAuthEntryPoint class:**

```java
package com.example.demo.config;

import java.io.IOException;

import org.springframework.security.core.AuthenticationException;
import org.springframework.security.web.AuthenticationEntryPoint;
import org.springframework.stereotype.Component;

import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

@Component
public class InvalidUserAuthEntryPoint implements AuthenticationEntryPoint {

    @Override
    public void commence(HttpServletRequest request, HttpServletResponse response,
            AuthenticationException authException) throws IOException, ServletException {
        response.setContentType("application/json");
        response.setStatus(HttpServletResponse.SC_UNAUTHORIZED);
        response.getOutputStream().println("{ \"error\": \"Unauthorized User\" }");
    }
}
```

6️⃣ **SecurityFilter** — Define one filter that gets executed for every request. Use the `OncePerRequestFilter` abstract class, and override the `doFilterInternal()` method.

**SecurityFilter class (initial version):**

```java
package com.example.demo.filter;

import java.io.IOException;

import org.springframework.stereotype.Component;
import org.springframework.web.filter.OncePerRequestFilter;

import jakarta.servlet.FilterChain;
import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

@Component
public class SecurityFilter extends OncePerRequestFilter {

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)
            throws ServletException, IOException {
        // TODO: Handle JWT Token Verification from 2nd Request Onwards
        filterChain.doFilter(request, response);
    }

}
```

7️⃣ **SecurityConfig** — Configure Spring Security with stateless session management.

`SecurityConfig` will have:

- 👤 `UserDetailsService` (`loadUserByUsername`)
- 🚫 `authenticationEntryPoint` (optional)
- 🔒 `SessionCreationPolicy.STATELESS`

> 📝 **Note:** `AuthenticationManager` checks username and password. In the case of Session, here no session, checking should be done manually.

**SecurityConfig class:**

```java
package com.example.demo.config;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.authentication.AuthenticationProvider;
import org.springframework.security.authentication.dao.DaoAuthenticationProvider;
import org.springframework.security.config.annotation.authentication.configuration.AuthenticationConfiguration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Autowired
    private UserDetailsService userDetailsService;

    @Autowired
    private PasswordEncoder passwordEncoder;

    @Autowired
    private InvalidUserAuthEntryPoint authEntryPoint;

    @Autowired
    private SecurityFilter securityFilter;

    // AuthenticationProvider
    @Bean
    AuthenticationProvider authenticationProvider() {
        DaoAuthenticationProvider provider = new DaoAuthenticationProvider();
        provider.setPasswordEncoder(passwordEncoder);
        provider.setUserDetailsService(userDetailsService);
        return provider;
    }

    @Bean
    AuthenticationManager authenticationManager(AuthenticationConfiguration
                           authenticationConfiguration) throws Exception {
        return authenticationConfiguration.getAuthenticationManager();
    }

    @Bean
    SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        return http
            .csrf(csrf -> csrf.disable())
            .authorizeHttpRequests(auth -> {
                auth.requestMatchers("/user/save", "/user/login").permitAll()
                .anyRequest().authenticated();
            })
            .exceptionHandling(exception -> exception.authenticationEntryPoint(authEntryPoint))
            .sessionManagement(session ->
                        session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
             // register filter for 2nd request onwards
            .addFilterBefore(securityFilter, UsernamePasswordAuthenticationFilter.class)
            .build();
    }
}
```

| URL Path 🌐 | Access Level 🔒 | Description 📋 |
|-------------|----------------|---------------|
| **`/user/save`** | ✅ `permitAll()` | User registration endpoint |
| **`/user/login`** | ✅ `permitAll()` | Login and JWT token generation |
| **All other URLs** | 🔐 `authenticated()` | Requires valid JWT token |

8️⃣ **Update UserRestController** — Use `AuthenticationManager` to validate username and password. If valid, a JWT token is generated; otherwise, `InvalidUserAuthEntryPoint` is triggered.

**UserRestController** (updated login endpoint):

```java
@Autowired
private AuthenticationManager authenticationManager;

// validate user and generate token (login)
@PostMapping("/login")
public ResponseEntity<UserResponse> loginUser(@RequestBody UserRequest request) {
    // validate with username & password with database
    authenticationManager
            .authenticate(new UsernamePasswordAuthenticationToken(
                            request.getUsername(),
                            request.getPassword()));

    String token = jwtUtil.generateToken(request.getUsername());
    return ResponseEntity.ok(new UserResponse(token,
                        "Success! Generated By KnowProgram"));
}
```

🗑️ **Clean Up Old Data:**

Delete the old data from the database because the password was not encoded at that time.

```sql
use test;
delete from rolestab where id in(1,2);
alter table rolestab auto_increment=1;
delete from usertab where id=1;
alter table usertab auto_increment=1;
```

🧪 **Testing the Authentication Flow:**

Now, create a new user and try to log in.

📥 **Register** (`POST http://localhost:8080/user/save`):

```json
{
    "name": "JERRY",
    "username": "jerry12",
    "password": "jerry@123",
    "roles": ["ADMIN","EMP"]
}
```

📥 **Login with invalid credentials** (`POST http://localhost:8080/user/login`):

```json
{
    "username": "abc",
    "password": "mno"
}
```

📤 **Response** (401 Unauthorized):

```json
{
    "error": "Unauthorized User"
}
```

📥 **Login with valid credentials:**

```json
{
    "username": "jerry12",
    "password": "jerry@123"
}
```

📤 **Response** (200 OK):

```json
{
    "token": "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJqZXJyeTEyIiwiaXNzIjoiS25vd1Byb2dyYW0tUFZUIiwiaWF0IjoxNzI3MzE1MDEzLCJleHAiOjE3MjczMTU2MTN9.K6AtxAD--6OjPbSiegBo-381TQ7_5tTSmdCPtyzllshimNVC--yXL3RBet9QYkkp2bsWdWxhRE1iT8rTLMv-zw",
    "message": "Success! Generated By KnowProgram"
}
```

---

## 5. JWT Token Verification from 2nd Request Onwards

Modify the `SecurityFilter`. If the request has an `Authorization` header, then validate using `JwtUtil`. If valid, then create `Authentication` inside `SecurityContext`.

**SecurityFilter class (final version):**

```java
package com.example.demo.filter;

import java.io.IOException;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.web.authentication.WebAuthenticationDetailsSource;
import org.springframework.stereotype.Component;
import org.springframework.web.filter.OncePerRequestFilter;

import com.example.demo.util.JwtUtil;

import jakarta.servlet.FilterChain;
import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

@Component
public class SecurityFilter extends OncePerRequestFilter {

    @Autowired
    private JwtUtil util;

    @Autowired
    private UserDetailsService userDetailsService;

    @Override
    protected void doFilterInternal(HttpServletRequest request,
                         HttpServletResponse response, FilterChain filterChain)
            throws ServletException, IOException {

        // 1. read token from Auth header
        String token = request.getHeader("Authorization");
        if (token != null) {
            // do validation
            String username = util.getUsername(token);

            // username should not be empty & context-auth must be empty
            if (username != null &&
                       SecurityContextHolder.getContext().getAuthentication() == null) {

                UserDetails user = userDetailsService.loadUserByUsername(username);
                // validate token
                boolean isValid = util.validateToken(token, user.getUsername());
                if (isValid) {
                    UsernamePasswordAuthenticationToken authToken =
                      new UsernamePasswordAuthenticationToken(username,
                            user.getPassword(), user.getAuthorities());
                   authToken.setDetails(new WebAuthenticationDetailsSource()
                                  .buildDetails(request));

                    // final object stored in SecurityContextHolder
                    // with User Details (username, password)
                    SecurityContextHolder.getContext().setAuthentication(authToken);
                }
            }
        }
        filterChain.doFilter(request, response);
    }
}
```

**Welcome endpoint in UserRestController:**

```java
// after login only
@GetMapping("/welcome")
public ResponseEntity<String> accessData(Principal p){
    return ResponseEntity.ok("Hello User " + p.getName());
}
```

> ⚠️ **Caution:** In the `User` model class, make sure to set `@ElementCollection(fetch = FetchType.EAGER)`:

```java
@ElementCollection(fetch = FetchType.EAGER)
@CollectionTable(
        name = "rolestab",
        joinColumns = @JoinColumn(name = "id")
)
private Set<String> roles;
```

🧪 **Testing the Protected Endpoint:**

To test the endpoint, first login with valid credentials, and copy the generated token.

📥 **Request** (`GET http://localhost:8080/user/welcome`):

In Headers, set `Key="Authorization"` and put the generated token in the value field.

![JWT Token](../img/JWT-Token.webp)

**CURL Request:**

```bash
curl --location 'http://localhost:8080/user/welcome' \
--header 'Authorization: eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJqZXJyeTEyIiwiaXNzIjoiS25vd1Byb2dyYW0tUFZUIiwiaWF0IjoxNzI3MzE3NjQ3LCJleHAiOjE3MjczMTgyNDd9.WH5Yxu7HlX7oLcVPjBGiPfR8DOgOsMf5un-pGTO5OhL4dZBlcjNc9o-wAqwQyaBRgfGxC4cTHXdSPmiwpSyy5w'
```

### Using Bearer Token Auth Type

Instead of mentioning the token through headers, we can directly specify in the Auth section as **Auth Type = "Bearer Token"**. In that case, the prefix `"Bearer "` will be applied to the token, therefore we have to remove that part in our `SecurityFilter` class as follows:

**Updated `doFilterInternal()` method:**

```java
@Override
protected void doFilterInternal(HttpServletRequest request,
      HttpServletResponse response, FilterChain filterChain)
          throws ServletException, IOException {

    // code
    String token = request.getHeader("Authorization");
    if (token != null) {
        // if using Bearer Token in Auth Type
        if(token.startsWith("Bearer")) {
                token = token.substring(7).trim();
        }

        // rest of the code
    }
    filterChain.doFilter(request, response);
}
```

![JWT Bearer Token](../img/JWT-Bearer-Token.webp)

**CURL Request (with Bearer prefix):**

```bash
curl --location 'http://localhost:8080/user/welcome' \
--header 'Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJqZXJyeTEyIiwiaXNzIjoiS25vd1Byb2dyYW0tUFZUIiwiaWF0IjoxNzI3MzE4NzA4LCJleHAiOjE3MjczMTkzMDh9.Tvcq_exBqhAVkK1Rw1IyteH68SneAk-L2Un71R9bCaQej4wohoaQi6Ewa0l7CLLmrMMcel6O7yLY3KhRg_GoQA'
```
