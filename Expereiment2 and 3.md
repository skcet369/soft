# 🚀 Automating Complex Form Submissions: Selenium WebDriver with Java

A beginner-friendly guide to automating a complete web form using **Selenium WebDriver** and **Java**. In this project, you'll learn how to automate text inputs, radio buttons, checkboxes, file uploads, keyboard actions, and form submission.

---

# 📖 What You Will Learn

- Launching Chrome Browser
- Navigating to a website
- Filling text fields
- Selecting radio buttons
- Selecting checkboxes
- Uploading files
- Using keyboard actions
- Scrolling the page
- Submitting forms
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
SeleniumFormAutomation/
│
├── src/
│   └── FormAutomation.java
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

Automate filling and submitting a complete registration form on the DemoQA practice website.

**Website**

https://demoqa.com/automation-practice-form

**Elements Covered**

- Text Inputs
- Radio Buttons
- Checkboxes
- File Upload
- Keyboard Actions
- Form Submission

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
Fill Text Fields
   │
   ▼
Select Radio Button
   │
   ▼
Select Checkbox
   │
   ▼
Upload File
   │
   ▼
Scroll Down
   │
   ▼
Submit Form
   │
   ▼
View Confirmation
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
FormAutomation.java
```

```java
import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class FormAutomation {

    public static void main(String[] args) throws InterruptedException {

        // 1. Initialize Browser and Maximize View
        WebDriver driver = new ChromeDriver();
        driver.manage().window().maximize();

        // 2. Open Target URL
        driver.get("https://demoqa.com/automation-practice-form");

        // 3. Fill Out Basic Text Fields
        driver.findElement(By.id("firstName")).sendKeys("Mounesh");
        driver.findElement(By.id("lastName")).sendKeys("Patil");
        driver.findElement(By.id("userEmail")).sendKeys("hi@gmail.com");

        // 4. Handle Radio Buttons & Checkboxes via Text Labels
        driver.findElement(By.xpath("//label[text()='Male']")).click();
        driver.findElement(By.id("userNumber")).sendKeys("1234567890");
        driver.findElement(By.xpath("//label[text()='Sports']")).click();

        // 5. Fill Textarea & Upload a Local File
        driver.findElement(By.id("currentAddress")).sendKeys("Bangalore, Karnataka");
        driver.findElement(By.id("uploadPicture"))
                .sendKeys("C:\\Users\\gurup\\Downloads\\WhatsApp Image 2026-06-15 at 8.59.21 AM.jpeg");

        Thread.sleep(2000);

        // 6. Scroll Down to Reveal Covered Elements
        driver.findElement(By.tagName("body")).sendKeys(Keys.END);
        Thread.sleep(1000);

        // 7. Click Submit using Keyboard Enter
        driver.findElement(By.id("submit")).sendKeys(Keys.ENTER);

        // 8. Observe Result and Close Session
        Thread.sleep(5000);
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
driver.get("https://demoqa.com/automation-practice-form");
```

Navigates to the DemoQA Automation Practice Form.

---

## 3. Maximize Window

```java
driver.manage().window().maximize();
```

Expands the browser window for better visibility.

---

## 4. Fill Text Fields

```java
driver.findElement(By.id("firstName")).sendKeys("Mounesh");
driver.findElement(By.id("lastName")).sendKeys("Patil");
driver.findElement(By.id("userEmail")).sendKeys("hi@gmail.com");
```

Uses `sendKeys()` to simulate typing into the text fields.

---

## 5. Select Radio Button

```java
driver.findElement(By.xpath("//label[text()='Male']")).click();
```

Clicks the visible **Male** label instead of the hidden radio input.

---

## 6. Enter Mobile Number

```java
driver.findElement(By.id("userNumber")).sendKeys("1234567890");
```

Types the mobile number into the input field.

---

## 7. Select Checkbox

```java
driver.findElement(By.xpath("//label[text()='Sports']")).click();
```

Selects the **Sports** checkbox using its visible label.

---

## 8. Fill Address

```java
driver.findElement(By.id("currentAddress"))
      .sendKeys("Bangalore, Karnataka");
```

Types the current address into the textarea.

---

## 9. Upload File

```java
driver.findElement(By.id("uploadPicture"))
      .sendKeys("C:\\Users\\gurup\\Downloads\\WhatsApp Image 2026-06-15 at 8.59.21 AM.jpeg");
```

Uploads a file by sending its absolute file path directly to the file input element.

---

## 10. Pause Execution

```java
Thread.sleep(2000);
```

Waits briefly to ensure the file upload completes.

---

## 11. Scroll to Bottom

```java
driver.findElement(By.tagName("body")).sendKeys(Keys.END);
```

Uses the keyboard **END** key to scroll the page.

---

## 12. Submit Form

```java
driver.findElement(By.id("submit")).sendKeys(Keys.ENTER);
```

Presses the **ENTER** key on the Submit button to submit the form.

---

## 13. Close Browser

```java
driver.quit();
```

Closes all browser windows and ends the Selenium session.

---

# 🔍 Locating Elements

Selenium supports multiple locator strategies.

| Locator | Example |
|----------|----------|
| id | `By.id("firstName")` |
| name | `By.name("firstName")` |
| className | `By.className("form-control")` |
| tagName | `By.tagName("body")` |
| linkText | `By.linkText("Home")` |
| partialLinkText | `By.partialLinkText("Hom")` |
| cssSelector | `By.cssSelector("#firstName")` |
| xpath | `By.xpath("//label[text()='Male']")` |

This project mainly uses:

- `By.id()`
- `By.xpath()`
- `By.tagName()`

---

# ⌨ Selenium Actions Used

## sendKeys()

Types text or keyboard keys.

```java
driver.findElement(By.id("firstName")).sendKeys("Mounesh");
```

---

## click()

Clicks a visible element.

```java
driver.findElement(By.xpath("//label[text()='Male']")).click();
```

---

## Keyboard Keys

```java
Keys.END
```

Scrolls to the bottom of the page.

```java
Keys.ENTER
```

Submits the form using the keyboard.

---

## quit()

Ends the WebDriver session.

```java
driver.quit();
```

---

# 🔍 Code Breakdown: Pro Tips Used Here

## 1. Handling Dynamic Elements via Text-Based XPath

```java
driver.findElement(By.xpath("//label[text()='Male']")).click();
```

Sometimes, the actual `<input>` elements for radio buttons or checkboxes are hidden or covered by custom CSS on modern web pages.

Clicking the visible `<label>` using a text-based XPath avoids click interception issues and provides a more reliable interaction.

---

## 2. The Direct File Upload Trick

```java
driver.findElement(By.id("uploadPicture"))
      .sendKeys("C:\\absolute\\path\\to\\file.jpg");
```

Instead of trying to automate the operating system's file chooser dialog (which Selenium cannot control), simply send the absolute file path directly to the `<input type="file">` element using `sendKeys()`.

This is the recommended and most reliable way to upload files with Selenium.

---

## 3. Avoiding Click Interception Using Keyboard Actions

```java
driver.findElement(By.tagName("body")).sendKeys(Keys.END);
driver.findElement(By.id("submit")).sendKeys(Keys.ENTER);
```

Some websites display sticky headers, advertisements, or floating elements that may block the Submit button.

Sending an **END** key scrolls the page into view, while pressing **ENTER** submits the form without relying on a mouse click.

This technique helps avoid `ElementClickInterceptedException`.

---

# 📊 Expected Output

After clicking **Submit**, the website displays a confirmation modal containing all the submitted registration details.

The modal includes information such as:

- Student Name
- Student Email
- Gender
- Mobile Number
- Address
- Uploaded Picture
- Selected Hobbies

If all fields are filled correctly, the form submission is successful.

---

# ▶ How to Run

1. Install Java.
2. Install Selenium dependencies.
3. Open the project in IntelliJ IDEA or Eclipse.
4. Create `FormAutomation.java`.
5. Paste the code.
6. Update the file upload path to match your local system.
7. Run the Java program.
8. Watch Selenium automatically complete and submit the form.

---

# ✅ Best Practices

- Use `By.id()` whenever possible.
- Use XPath only when necessary.
- Prefer explicit waits over `Thread.sleep()`.
- Keep file paths configurable.
- Always call `driver.quit()`.
- Store test data separately from test code.
- Use Page Object Model (POM) for larger projects.

---

# 🚀 Future Improvements

You can enhance this project by adding:

- ✅ Explicit Waits (`WebDriverWait`)
- ✅ TestNG
- ✅ JUnit 5
- ✅ Page Object Model (POM)
- ✅ Data-Driven Testing
- ✅ Reading Test Data from Excel
- ✅ Screenshots on Failure
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
| sendKeys() | Type text or keyboard input |
| click() | Click an element |
| getText() | Read visible text |
| getAttribute() | Read attribute values |
| getTitle() | Get page title |
| navigate().back() | Browser back |
| navigate().forward() | Browser forward |
| navigate().refresh() | Refresh page |
| close() | Close current tab |
| quit() | Close entire browser |

---

# ❓ Common Errors

### NoSuchElementException

The locator is incorrect or the element hasn't loaded yet.

---

### ElementClickInterceptedException

Another element is blocking the click.

Use scrolling or keyboard actions.

---

### InvalidArgumentException

The specified file path for upload does not exist.

Verify the absolute file path on your computer.

---

### TimeoutException

The page or element took too long to load.

Replace `Thread.sleep()` with explicit waits.

---

# 🎯 Learning Outcomes

After completing this project, you'll understand how to:

- Launch a browser
- Navigate to a webpage
- Fill text fields
- Handle radio buttons
- Handle checkboxes
- Upload files
- Perform keyboard actions
- Scroll web pages
- Submit complex forms
- Close browser sessions correctly

---

# ⭐ Next Challenge

Instead of using:

```java
Thread.sleep(2000);
```

Replace the fixed delays with **Explicit Waits** using `WebDriverWait` and `ExpectedConditions` for more reliable and faster automation.

---

## 🎉 Congratulations!

You have successfully automated a **complex web form using Selenium WebDriver with Java**.

This project demonstrates many real-world Selenium concepts including text input, XPath locators, radio buttons, checkboxes, file uploads, keyboard actions, scrolling, and form submission. These skills form the foundation for building robust UI automation frameworks for professional testing projects.

Happy Testing! 🚀
