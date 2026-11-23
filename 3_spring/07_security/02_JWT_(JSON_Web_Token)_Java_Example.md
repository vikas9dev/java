# JWT (JSON Web Token) Java Example

**JWT (JSON Web Token) Java Example** | JWT (JSON Web Token) is an open-source service (API) that supports generating tokens based on client details and secretKey. It is token-based and stateless authentication (No HTTP session). Also see: Stateful and Stateless Authentication

- [JWT Format](#1-jwt-format)
- [JWT Token Flow](#2-jwt-token-flow)
- [Dependencies](#3-dependencies)
- [Implementation](#4-implementation)
- [Output](#5-output)

---

## 1. JWT Format

A JWT token has three parts separated by dots: `header.payload.signature` (e.g., `aaaaaa.bbbbb.cccc`)

| Part 🏷️ | Description 📋 |
|----------|----------------|
| **Header** | JWT-specific information (algorithm, token type) |
| **Payload** | Claims (ClientID, ClientName, ProviderName, Date, expiryDate, etc.) |
| **Signature** | `Base64Encode(Header)` + `Base64Encode(Payload)` signed with secretKey |

```mermaid
graph LR
    H["🔑 Header"] --> T["📦 JWT Token"]
    P["📋 Payload"] --> T
    S["🔒 Signature"] --> T
    T --> E["📤 Encoded String"]

    classDef purple fill:#A162F7,stroke:#A162F7,color:#fff
    classDef cyan fill:#00b4d8,stroke:#00b4d8,color:#fff
    classDef green fill:#28C76F,stroke:#28C76F,color:#fff
    classDef orange fill:#FF9F43,stroke:#FF9F43,color:#fff

    class H purple
    class P cyan
    class S green
    class T orange
    class E pink
```

🛠️ **Sample Encoded JWT:**

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

🔍 **Sample Decoded JWT:**

**Header:**

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

**Payload:**

```json
{
  "id": "1234567890",
  "subject": "John Doe",
  "issuer": "KnowProgram",
  "issueDate": "<dateAndTime>",
  "expiryDate": "<dateAndTime>",
  "iat": 1516239022
}
```

**Signature:**

```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  <your-256-bit-secret>
)
```

---

## 2. JWT Token Flow

The process of working with JWT involves two main steps:

1. 🔐 Generate Token using JWT Java API
2. ✅ Read and Validate the Token using JWT Java API

```mermaid
sequenceDiagram
    participant Client as 🖥️ Client
    participant API as 🌐 JWT API
    participant Key as 🔑 Secret Key

    Client->>API: Request token (id, subject)
    API->>Key: Sign with secret key
    Key-->>API: Signed token
    API-->>Client: JWT Token (header.payload.signature)
    Client->>API: Send token for validation
    API->>Key: Verify signature
    Key-->>API: Validation result
    API-->>Client: Claims (subject, issuer, expiry, etc.)
```

---

## 3. Dependencies

To implement this we have to use JJWT dependencies (Java JWT). Java JWT API is an open-source Java API.

📦 **Maven Dependencies:**

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

💡 **Tip:** Create a Simple Maven Project and add the above dependencies in `<dependencies></dependencies>`.

---

## 4. Implementation

Claims allow you to read/parse JWT details by providing two inputs:

- 🔑 **Token** — The generated JWT string
- 🔒 **Secret Key** — The key used to sign the token

1️⃣ **JwtUtil class:**

```java
import java.security.Key;
import java.util.Date;
import java.util.concurrent.TimeUnit;

import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import io.jsonwebtoken.security.Keys;

public class JwtUtil {
    // Generate a secure random key
    Key key = Keys.secretKeyFor(SignatureAlgorithm.HS256);

    // generate token
    public String generateToken(String id, String subject) {
        return Jwts.builder()
        .setId(id).setSubject(subject)
        .setIssuer("KnowProgram")
        .setIssuedAt(new Date(System.currentTimeMillis()))
        .setExpiration(new Date(System.currentTimeMillis() +
                TimeUnit.MINUTES.toMillis(10)))
        .signWith(key)
        .compact();
    }

    // get claims
    public Claims getClaims(String token) {
        return Jwts.parserBuilder()
                .setSigningKey(key)
                .build()
                .parseClaimsJws(token)
                .getBody();
    }

    public String getSubject(String token) {
        return getClaims(token).getSubject();
    }

    public boolean isValidToken(String token) {
        return getClaims(token)
                .getExpiration().after(
                        new Date(System.currentTimeMillis()
                 ));
    }
}
```

2️⃣ **Test class:**

```java
import io.jsonwebtoken.Claims;

public class Test {
    public static void main(String[] args) {
        JwtUtil jwtUtil = new JwtUtil();

        String token = jwtUtil.generateToken("AA885", "Jerry");
        System.out.println("Generated token: " + token);

        Claims claims = jwtUtil.getClaims(token);
        System.out.println();
        System.out.println(claims);
        System.out.println(claims.getSubject());
        System.out.println(claims.getId());
        System.out.println(claims.getIssuer());
        System.out.println(claims.getExpiration());
    }
}
```

---

## 5. Output

📤 **Console Output:**

```
Generated token: eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJBQTg4NSIsInN1YiI6IkplcnJ5IiwiaXNzIjoiS25vd1Byb2dyYW0iLCJpYXQiOjE3MjcyNDE5MTYsImV4cCI6MTcyNzI0MjUxNn0.Cf9n76DvVfdisATeU3HdcTcgCShgpWHP2CZ9MgDqca0

{jti=AA885, sub=Jerry, iss=KnowProgram, iat=1727241916, exp=1727242516}
Jerry
AA885
KnowProgram
Wed Sep 25 11:05:16 IST 2024
```
