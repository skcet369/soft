# 🚀 Advanced Logging in Automation: Integrating Log4j2 with Selenium WebDriver

A beginner-friendly guide to implementing **Apache Log4j2** logging in Selenium automation projects. Instead of using `System.out.println()` statements, you'll learn how to generate structured log messages with different severity levels while automating a real browser application.

---

# 📖 What You Will Learn

- Introduction to Apache Log4j2
- Integrating Log4j2 with Selenium WebDriver
- Creating Logger instances
- Understanding Log Levels
- Logging Selenium execution steps
- Simulating keyboard actions
- Configuring `log4j2.xml`
- Writing cleaner automation frameworks

---

# 🛠 Technologies Used

- Java
- Selenium WebDriver
- Apache Log4j2
- TestNG
- Chrome Browser
- ChromeDriver
- IntelliJ IDEA / Eclipse
- Maven (Optional)

---

# 📂 Project Structure

```
SeleniumLog4j2Automation/
│
├── src/
│   └── LoggedGameAutomation.java
│
├── resources/
│   └── log4j2.xml
│
├── testng.xml
│
├── README.md
│
└── pom.xml
```

---

# 📥 Prerequisites

Before running the project, make sure you have:

- Java JDK 11 or later
- Chrome Browser installed
- Selenium WebDriver
- TestNG
- Apache Log4j2
- IntelliJ IDEA / Eclipse
- Maven (Optional)

---

# 📦 Maven Dependencies

If you're using Maven, add the following dependencies to your `pom.xml`.

```xml
<dependencies>

    <!-- Selenium -->
    <dependency>
        <groupId>org.seleniumhq.selenium</groupId>
        <artifactId>selenium-java</artifactId>
        <version>4.33.0</version>
    </dependency>

    <!-- TestNG -->
    <dependency>
        <groupId>org.testng</groupId>
        <artifactId>testng</artifactId>
        <version>7.11.0</version>
    </dependency>

    <!-- Log4j2 API -->
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-api</artifactId>
        <version>2.25.1</version>
    </dependency>

    <!-- Log4j2 Core -->
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-core</artifactId>
        <version>2.25.1</version>
    </dependency>

</dependencies>
```

---

# ⚙️ Configure Log4j2

Before running the project, create a file named:

```
log4j2.xml
```

Place it inside the **resources** folder.

Project structure:

```
SeleniumLog4j2Automation/
│
├── src/
│
├── resources/
│   └── log4j2.xml
│
├── testng.xml
│
└── pom.xml
```

Use the following configuration:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="WARN">

    <Appenders>

        <Console name="Console" target="SYSTEM_OUT">
            <PatternLayout
                    pattern="%d{HH:mm:ss} %-5level %msg%n"/>
        </Console>

    </Appenders>

    <Loggers>

        <Root level="trace">
            <AppenderRef ref="Console"/>
        </Root>

    </Loggers>

</Configuration>
```

---

# 🧠 Understanding the Configuration

## status="WARN"

```xml
<Configuration status="WARN">
```

Displays only Log4j2 internal warning messages.

---

## Console Appender

```xml
<Console name="Console" target="SYSTEM_OUT">
```

Sends all log messages directly to the IDE or terminal console.

---

## PatternLayout

```xml
<PatternLayout
        pattern="%d{HH:mm:ss} %-5level %msg%n"/>
```

Formats every log message.

| Pattern | Description |
|----------|-------------|
| `%d{HH:mm:ss}` | Current Time |
| `%-5level` | Log Level |
| `%msg` | Log Message |
| `%n` | New Line |

Example:

```
20:46:45 INFO  Browser Opened
```

---

## Root Logger

```xml
<Root level="trace">
```

Enables every logging level.

The following logs will be displayed:

- TRACE
- DEBUG
- INFO
- WARN
- ERROR
- FATAL

---

## AppenderRef

```xml
<AppenderRef ref="Console"/>
```

Connects the Root Logger with the Console Appender.

Without this line, logs will not appear on the console.

---

# 🎯 Goal

Automate a browser session while logging every important automation event using Apache Log4j2.

**Target Website**

https://play2048.co

**Concepts Covered**

- Logger Initialization
- INFO Logs
- DEBUG Logs
- TRACE Logs
- WARN Logs
- ERROR Logs
- FATAL Logs
- Keyboard Actions
- Selenium Automation

---

# 🔄 Automation Workflow

```
Start
   │
   ▼
Initialize Log4j2
   │
   ▼
Launch Chrome Browser
   │
   ▼
Open 2048 Website
   │
   ▼
INFO Log
   │
   ▼
DEBUG Log
   │
   ▼
Move UP
   │
   ▼
Move LEFT
   │
   ▼
Move RIGHT
   │
   ▼
Move DOWN
   │
   ▼
WARN Log
   │
   ▼
ERROR Log
   │
   ▼
FATAL Log
   │
   ▼
Disable Logger
   │
   ▼
Close Browser
   │
   ▼
End
```

---

# 💻 Java Code

Create a file named:

```
LoggedGameAutomation.java
```

```java
import org.apache.logging.log4j.Level;
import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.core.config.Configurator;
import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.Test;

public class LoggedGameAutomation {

    static Logger log = LogManager.getLogger(LoggedGameAutomation.class);

    @Test
    public void gameLoopTest() throws InterruptedException {

        log.info("Opening web browser environment context.");

        WebDriver driver = new ChromeDriver();

        driver.get("https://play2048.co");

        Thread.sleep(2000);

        log.debug("Target sandbox verified. Starting game interaction loops.");

        log.trace("Simulating Action: Moving Grid UP");
        driver.findElement(By.tagName("body")).sendKeys(Keys.ARROW_UP);

        Thread.sleep(1000);

        log.trace("Simulating Action: Moving Grid LEFT");
        driver.findElement(By.tagName("body")).sendKeys(Keys.ARROW_LEFT);

        Thread.sleep(1000);

        log.trace("Simulating Action: Moving Grid RIGHT");
        driver.findElement(By.tagName("body")).sendKeys(Keys.ARROW_RIGHT);

        Thread.sleep(1000);

        log.trace("Simulating Action: Moving Grid DOWN");
        driver.findElement(By.tagName("body")).sendKeys(Keys.ARROW_DOWN);

        Thread.sleep(1000);

        log.warn("Mock Warning: Resource thresholds or element responsiveness is dropping below ideal standards.");

        log.fatal("Mock Fatal Exception: Critical framework or environment core failure observed.");

        log.error("Mock Error Alert: Minor localized step validation checkpoint missed.");

        Thread.sleep(3000);

        Configurator.setRootLevel(Level.OFF);

        driver.quit();
    }
}
```

---

# 🧠 Code Explanation

## 1. Create Logger

```java
static Logger log = LogManager.getLogger(LoggedGameAutomation.class);
```

Creates a Log4j2 logger for the current class.

---

## 2. Launch Browser

```java
WebDriver driver = new ChromeDriver();
```

Starts Chrome Browser.

---

## 3. Open Website

```java
driver.get("https://play2048.co");
```

Loads the 2048 game.

---

## 4. Log Execution

```java
log.info(...)
log.debug(...)
log.trace(...)
```

Records execution events.

---

## 5. Keyboard Actions

```java
driver.findElement(By.tagName("body"))
      .sendKeys(Keys.ARROW_UP);
```

Controls the game using keyboard arrows.

---

## 6. Log Warnings

```java
log.warn(...)
```

Logs non-critical warnings.

---

## 7. Log Errors

```java
log.error(...)
```

Logs execution failures.

---

## 8. Log Fatal Events

```java
log.fatal(...)
```

Logs severe framework failures.

---

## 9. Disable Logging

```java
Configurator.setRootLevel(Level.OFF);
```

Stops logging.

---

## 10. Close Browser

```java
driver.quit();
```

Ends the Selenium session.

---

# 🔍 Code Breakdown: Pro Tips Used Here

## 1. Logger Instance

```java
static Logger log = LogManager.getLogger(LoggedGameAutomation.class);
```

Creates a reusable logging engine for the class.

---

## 2. Logging Levels

| Level | Purpose |
|--------|----------|
| TRACE | Detailed execution |
| DEBUG | Developer debugging |
| INFO | General execution |
| WARN | Warning messages |
| ERROR | Recoverable errors |
| FATAL | Critical failures |

---

## 3. Keyboard Actions

```java
driver.findElement(By.tagName("body"))
      .sendKeys(Keys.ARROW_UP);
```

The 2048 game listens to keyboard events on the page body, so sending arrow keys directly controls the game.

---

# 📊 Expected Console Output

```
20:46:45 INFO  Opening web browser environment context.
20:46:47 DEBUG Target sandbox verified. Starting game interaction loops.
20:46:48 TRACE Simulating Action: Moving Grid UP
20:46:49 TRACE Simulating Action: Moving Grid LEFT
20:46:50 TRACE Simulating Action: Moving Grid RIGHT
20:46:51 TRACE Simulating Action: Moving Grid DOWN
20:46:52 WARN  Mock Warning: Resource thresholds dropped.
20:46:52 ERROR Mock Error Alert: Validation checkpoint missed.
20:46:52 FATAL Mock Fatal Exception: Critical framework failure observed.
```

---

# ▶ How to Run

1. Install Java.
2. Add Selenium, TestNG, and Log4j2 dependencies.
3. Create `log4j2.xml` inside the **resources** folder.
4. Open the project in IntelliJ IDEA or Eclipse.
5. Create `LoggedGameAutomation.java`.
6. Paste the Java code.
7. Run the TestNG class.
8. Observe browser automation and formatted logs.

---

# ✅ Best Practices

- Use logging instead of `System.out.println()`.
- Choose the correct log level.
- Keep TRACE logs for debugging.
- Store logs in files for production.
- Replace `Thread.sleep()` with explicit waits.
- Keep log messages meaningful.

---

# 🚀 Future Improvements

- ✅ Rolling File Appender
- ✅ HTML Log Reports
- ✅ Extent Reports
- ✅ Allure Reports
- ✅ Screenshots on Failure
- ✅ Explicit Waits
- ✅ TestNG Listeners
- ✅ Jenkins Integration

---

# 📚 Common Logger Methods

| Method | Purpose |
|---------|----------|
| trace() | Detailed logs |
| debug() | Debug logs |
| info() | General logs |
| warn() | Warning logs |
| error() | Error logs |
| fatal() | Critical logs |

---

# ❓ Common Errors

### Logger Not Printing

Ensure `log4j2.xml` is placed inside the **resources** folder.

---

### NoClassDefFoundError

The Log4j2 dependency is missing.

---

### SessionNotCreatedException

ChromeDriver version doesn't match Chrome Browser.

---

### NoSuchElementException

The element locator is incorrect.

---

# 🎯 Learning Outcomes

After completing this project, you'll understand how to:

- Configure Log4j2
- Create Logger instances
- Use different logging levels
- Log Selenium execution
- Automate keyboard actions
- Build maintainable automation frameworks

---

# ⭐ Next Challenge

Instead of displaying logs only in the console, configure a **RollingFileAppender** in `log4j2.xml` to automatically save logs into timestamped files while keeping a history of previous test executions.

---

# 🎉 Congratulations!

You have successfully integrated **Apache Log4j2** with **Selenium WebDriver**.

This project demonstrates how professional automation frameworks replace simple console output with structured logging. By combining Selenium, TestNG, and Log4j2, you've learned how to categorize execution events by severity, improve debugging, and build more maintainable automation frameworks.

Happy Testing! 🚀
