# 🚀 Building Your First Automation Script: Selenium WebDriver with Java

A beginner-friendly guide to automating a login workflow using **Selenium WebDriver** and **Java**.

---

# 📖 What You Will Learn

- Setting up Selenium WebDriver
- Launching Chrome Browser
- Navigating to a website
- Locating web elements
- Entering text into input fields
- Clicking buttons
- Verifying successful login
- Closing the browser properly

---

# 🛠 Technologies Used

- Java
- Selenium WebDriver
- Chrome Browser
- ChromeDriver
- IntelliJ IDEA / Eclipse (or any Java IDE)
- Maven (Optional)

---

# 📂 Project Structure

```
SeleniumLoginAutomation/
│
├── src/
│   └── LoginAutomation.java
│
├── README.md
│
└── pom.xml (Optional if using Maven)
```

---

# 📥 Prerequisites

Before running the project, make sure you have:

- Java JDK 11 or later
- Chrome Browser installed
- Compatible ChromeDriver (or Selenium Manager with Selenium 4.6+)
- Selenium Java Library
- IntelliJ IDEA / Eclipse / VS Code

---

# 📦 Maven Dependency (Optional)

If you're using Maven, add the following dependency to your `pom.xml`.

```xml
<dependencies>

    <dependency>
        <groupId>org.seleniumhq.selenium</groupId>
        <artifactId>selenium-java</artifactId>
        <version>4.33.0</version>
    </dependency>

</dependencies>
```

---

# 🎯 Goal

Automate the login process for the Selenium practice website.

**Website**

https://practicetestautomation.com/practice-test-login/

**Username**

```
student
```

**Password**

```
Password123
```

---

# 🔄 Automation Workflow

```
Start
   │
   ▼
Launch Chrome
   │
   ▼
Open Website
   │
   ▼
Maximize Browser
   │
   ▼
Enter Username
   │
   ▼
Enter Password
   │
   ▼
Click Login
   │
   ▼
Verify Login
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
LoginAutomation.java
```

```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

public class LoginAutomation {

    public static void main(String[] args) {

        // Launch Chrome Browser
        WebDriver driver = new ChromeDriver();

        // Open Website
        driver.get("https://practicetestautomation.com/practice-test-login/");

        // Maximize Window
        driver.manage().window().maximize();

        // Locate Username Field
        WebElement username = driver.findElement(By.id("username"));

        // Enter Username
        username.sendKeys("student");

        // Locate Password Field
        WebElement password = driver.findElement(By.id("password"));

        // Enter Password
        password.sendKeys("Password123");

        // Locate Login Button
        WebElement loginButton = driver.findElement(By.id("submit"));

        // Click Login
        loginButton.click();

        // Print Page Title
        System.out.println("Page Title : " + driver.getTitle());

        // Close Browser
        driver.quit();
    }
}
```

---

# 🧠 Code Explanation

## 1. Launch Browser

```java
WebDriver driver = new ChromeDriver();
```

Creates a new Chrome browser session.

---

## 2. Open Website

```java
driver.get("https://practicetestautomation.com/practice-test-login/");
```

Navigates to the practice login page.

---

## 3. Maximize Window

```java
driver.manage().window().maximize();
```

Expands the browser window for better visibility.

---

## 4. Locate Elements

```java
driver.findElement(By.id("username"));
```

Finds the username textbox using its unique HTML `id`.

Similarly,

```java
driver.findElement(By.id("password"));
driver.findElement(By.id("submit"));
```

find the password field and login button.

---

## 5. Enter Text

```java
username.sendKeys("student");
password.sendKeys("Password123");
```

`sendKeys()` simulates typing into the input fields.

---

## 6. Click Login

```java
loginButton.click();
```

Simulates a mouse click on the Login button.

---

## 7. Verify Login

```java
System.out.println(driver.getTitle());
```

Prints the page title after login.

Expected title:

```
Logged In Successfully | Practice Test Automation
```

---

## 8. Close Browser

```java
driver.quit();
```

Ends the WebDriver session and closes every browser window.

---

# 🔍 Locating Elements

Selenium provides multiple locator strategies.

| Locator | Example |
|----------|----------|
| id | `By.id("username")` |
| name | `By.name("username")` |
| className | `By.className("button")` |
| tagName | `By.tagName("input")` |
| linkText | `By.linkText("Home")` |
| partialLinkText | `By.partialLinkText("Hom")` |
| cssSelector | `By.cssSelector("#username")` |
| xpath | `By.xpath("//input[@id='username']")` |

For this project we use:

```java
By.id()
```

because IDs are generally the fastest and most reliable locators.

---

# ⌨ Selenium Actions Used

## sendKeys()

Types text into an input field.

```java
username.sendKeys("student");
```

---

## click()

Clicks a button or link.

```java
loginButton.click();
```

---

## getTitle()

Returns the current page title.

```java
driver.getTitle();
```

---

## quit()

Closes all browser windows and ends the WebDriver session.

```java
driver.quit();
```

---

# 📊 Expected Console Output

```
Page Title : Logged In Successfully | Practice Test Automation
```

---

# ▶ How to Run

1. Install Java.
2. Install Selenium dependencies.
3. Open the project in IntelliJ IDEA or Eclipse.
4. Create `LoginAutomation.java`.
5. Paste the code.
6. Run the Java program.
7. Watch Selenium launch Chrome and perform the login automatically.

---

# ✅ Best Practices

- Prefer `By.id()` whenever available.
- Keep locators readable and maintainable.
- Always call `driver.quit()`.
- Use assertions instead of `System.out.println()` in real automation projects.
- Store test data separately from test code.
- Use explicit waits for dynamic web applications.
- Organize tests using Page Object Model (POM) as projects grow.

---

# 🚀 Future Improvements

You can enhance this project by adding:

- ✅ TestNG
- ✅ JUnit 5
- ✅ Page Object Model (POM)
- ✅ Explicit Waits
- ✅ Screenshots on Failure
- ✅ Data-Driven Testing using Excel or CSV
- ✅ Cross-Browser Testing
- ✅ Headless Execution
- ✅ Parallel Test Execution
- ✅ CI/CD with GitHub Actions or Jenkins
- ✅ HTML Reports using Extent Reports or Allure

---

# 📚 Useful Selenium Methods

| Method | Purpose |
|---------|----------|
| get() | Open a webpage |
| findElement() | Locate one element |
| findElements() | Locate multiple elements |
| sendKeys() | Type text |
| click() | Click element |
| getText() | Read visible text |
| getAttribute() | Read attribute value |
| getTitle() | Get page title |
| getCurrentUrl() | Get current URL |
| navigate().back() | Browser back |
| navigate().forward() | Browser forward |
| navigate().refresh() | Refresh page |
| close() | Close current tab |
| quit() | Close entire browser |

---

# ❓ Common Errors

### SessionNotCreatedException

ChromeDriver version doesn't match your Chrome browser version.

---

### NoSuchElementException

The locator is incorrect or the element hasn't loaded yet.

---

### TimeoutException

The page or element took too long to load.

Use an explicit wait.

---

# 🎯 Learning Outcomes

After completing this project, you'll understand how to:

- Launch a browser using Selenium
- Navigate to a website
- Locate web elements
- Enter user input
- Click buttons
- Validate application behavior
- Close browser sessions correctly

---

# ⭐ Next Challenge

Instead of printing the page title:

```java
System.out.println(driver.getTitle());
```

Try using a testing framework like **TestNG** or **JUnit** to automatically verify that the login was successful.

Example (JUnit):

```java
assertEquals(
    "Logged In Successfully | Practice Test Automation",
    driver.getTitle()
);
```

---

## 🎉 Congratulations!

You have successfully built your **first Selenium WebDriver automation script using Java**.

This simple project introduces the core concepts used in real-world UI automation testing. From here, you can continue exploring advanced topics such as waits, assertions, Page Object Model (POM), data-driven testing, reporting, and continuous integration to build scalable and maintainable automation frameworks.

Happy Testing! 🚀
