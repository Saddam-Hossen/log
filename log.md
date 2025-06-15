Here's a clean and professional GitHub `README.md` documentation for implementing structured logging in a Spring Boot application using Log4j2:

```markdown
# 📘 Structured Logging in Spring Boot with Log4j2

This project demonstrates how to configure and use **Log4j2** for structured, centralized logging in a **Spring Boot application**.

> 🧩 Logs help track application behavior, performance, and debugging insights — making them essential in production systems.

---

## 🚀 Features

- 📦 Log4j2 configured using `application.properties` (no XML required)
- 💡 Structured JSON logs
- ✅ Logs user login actions, exceptions, and system startup
- 📁 Logs saved to a file (`logs/app.log`)
- 🛠 Ready for use in distributed systems and centralized logging (e.g., ELK, Loki)

---

## 🧱 Project Structure


springboot-logging/
├── src/
│   └── main/
│       └── java/com/example/logging/
│           └── controller/LoginController.java
│       └── resources/
│           └── application.properties
├── logs/
│   └── app.log         <-- Log file created here
├── pom.xml
└── README.md

```


## ⚙️ application.properties

```properties
# Log4j2 Configuration
logging.level.root=INFO
logging.level.com.example=INFO
logging.file.name=logs/app.log
logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} %-5level %logger{36} - %msg%n
logging.pattern.file={"instant":{"epochSecond":%d{UNIX_SECONDS},"nanoOfSecond":%d{UNIX_NANO}},"thread":"%t","level":"%p","loggerName":"%c","message":"%m","endOfBatch":false,"loggerFqcn":"%c","threadId":%tid,"threadPriority":%priority}%n
````

---

## 🧪 Sample Log Entry

```json
{
  "instant": {
    "epochSecond": 1749998362,
    "nanoOfSecond": 368062000
  },
  "thread": "http-nio-8080-exec-1",
  "level": "INFO",
  "loggerName": "com.example.logging.controller.LoginController",
  "message": "User 'admin' logged in from IP [192.168.1.12] with roles [ADMIN]",
  "endOfBatch": false,
  "loggerFqcn": "org.apache.commons.logging.LogAdapter$Log4jLog",
  "threadId": 39,
  "threadPriority": 5
}
```

---

## 🔐 Logging a Login Event

```java
@RestController
public class LoginController {
    private static final Logger logger = LogManager.getLogger(LoginController.class);

    @PostMapping("/login")
    public ResponseEntity<String> login(@RequestParam String username, HttpServletRequest request) {
        String ipAddress = request.getRemoteAddr();
        List<String> roles = List.of("USER"); // Simulate roles

        logger.info("User '{}' logged in from IP [{}] with roles [{}]", username, ipAddress, roles);
        return ResponseEntity.ok("Login successful");
    }
}
```

---

## 🎯 Why Structured Logging?

* 📊 Easily parse logs with tools (e.g., Logstash, Fluentd)
* 🔍 Track user activity (login, logout, errors)
* 🛠 Identify performance bottlenecks
* 📡 Forward logs to external logging platforms (ELK, Loki, CloudWatch)

---

## ✅ Best Practices

* Use proper log levels: `INFO`, `WARN`, `ERROR`, `DEBUG`
* Never log sensitive data (passwords, tokens)
* Use JSON format for machine-readable logs
* Rotate and archive old logs using Log4j2 rollover policies

---

## 📂 Example: Track Events

| Event           | Log Message                                                           |
| --------------- | --------------------------------------------------------------------- |
| User Login      | `User 'john' logged in from IP [10.0.0.1] with roles [ADMIN]`         |
| Invalid Attempt | `Authentication failed for user 'guest'`                              |
| System Startup  | `Started LoggingApplication in 2.318 seconds (JVM running for 3.102)` |
| Exception       | `NullPointerException at LoginService.java:42`                        |

---

## 🔗 Related

* [Spring Boot Logging Docs](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.logging)
* [Log4j2 Documentation](https://logging.apache.org/log4j/2.x/manual/configuration.html)

---



