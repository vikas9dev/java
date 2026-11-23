# Troubleshooting — Spring Data JPA

Common issues and fixes when working with Spring Data JPA, databases, and cross-machine connections.

---

## 1. PostgreSQL "Asia/Calcutta" Timezone Error (Windows)

**Error:**

```
FATAL: invalid value for parameter "TimeZone": "Asia/Calcutta"
```

**Cause:** Java on Windows sends the deprecated timezone `Asia/Calcutta` instead of `Asia/Kolkata`. PostgreSQL rejects it.

**Fix — Spring Boot `application.properties`:**

```properties
spring.jpa.properties.hibernate.jdbc.time_zone=Asia/Kolkata
```

**Fix — JVM argument (IntelliJ):**

Run → Edit Configurations → VM Options:

```
-Duser.timezone=Asia/Kolkata
```

**Fix — DBeaver:**

Edit `dbeaver.ini` (in DBeaver installation folder) and add:

```
-Duser.timezone=Asia/Kolkata
```

Restart DBeaver after this change.

---

## 2. Connecting Spring Boot to a Remote PostgreSQL (Another Laptop on Same WiFi)

**Scenario:** PostgreSQL is running on Ubuntu (e.g., in Docker), and Spring Boot runs on Windows.

### Find the Ubuntu IP

```bash
hostname -I
# Example: 192.168.1.7
```

### `application.properties`

```properties
spring.datasource.url=jdbc:postgresql://192.168.1.7:5432/mydb
spring.datasource.username=postgres
spring.datasource.password=postgres

spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.properties.hibernate.jdbc.time_zone=Asia/Kolkata
```

### Ensure PostgreSQL Allows Remote Connections

If running via Docker Compose, port must be mapped:

```yaml
ports:
  - "5432:5432"
```

Allow port through Ubuntu firewall:

```bash
sudo ufw allow 5432
```

---
