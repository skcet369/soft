# 🚀 Advanced Test Reporting: Extent Reports with Embedded Screenshots in Selenium

A beginner-friendly guide to generating professional HTML automation reports with embedded screenshots using **Extent Reports** and **Selenium WebDriver**. Instead of relying on console output, you'll create interactive reports that clearly show every important automation step with supporting screenshots.

---

# 📖 What You Will Learn

- Introduction to Extent Reports
- Generating HTML Test Reports
- Integrating Selenium with Extent Reports
- Capturing Screenshots
- Embedding Screenshots into Reports
- Organizing Automation Results
- Creating Reusable Screenshot Utilities

---

# 🛠 Technologies Used

- Java
- Selenium WebDriver
- Extent Reports
- Chrome Browser
- ChromeDriver
- IntelliJ IDEA / Eclipse
- Maven (Optional)

---

# 📂 Project Structure

```
ExtentReportsAutomation/
│
├── src/
│   └── ReportedAutomation.java
│
├── reports/
│   ├── report.html
│   ├── 01_Home.png
│   ├── 02_Dashboard.png
│   ├── 03_PIM.png
│   ├── 04_Admin.png
│   └── 05_Logout.png
│
├── README.md
│
└── pom.xml
```

---

# 📥 Prerequisites

Before running the project, make sure you have:

- Java JDK 11 or later
- Chrome Browser
- Selenium WebDriver
- Extent Reports Library
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

    <!-- Extent Reports -->
    <dependency>
        <groupId>com.aventstack</groupId>
        <artifactId>extentreports</artifactId>
        <version>5.1.2</version>
    </dependency>

</dependencies>
```

---

# 🎯 Goal

Generate a professional HTML automation report with screenshots after executing Selenium automation.

**Target Website**

https://opensource-demo.orangehrmlive.com/

**Concepts Covered**

- HTML Report Generation
- Screenshot Capture
- Step Logging
- Reusable Utility Methods
- Report Management

---

# 🔄 Automation & Reporting Workflow

```
Start
   │
   ▼
Create Reports Folder
   │
   ▼
Initialize Extent Reports
   │
   ▼
Launch Chrome
   │
   ▼
Open OrangeHRM
   │
   ▼
Capture Home Screenshot
   │
   ▼
Login
   │
   ▼
Capture Dashboard Screenshot
   │
   ▼
Open PIM Module
   │
   ▼
Capture Screenshot
   │
   ▼
Open Admin Module
   │
   ▼
Capture Screenshot
   │
   ▼
Logout
   │
   ▼
Capture Screenshot
   │
   ▼
Generate HTML Report
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
ReportedAutomation.java
```

```java
import com.aventstack.extentreports.*;
import com.aventstack.extentreports.reporter.ExtentSparkReporter;
import org.openqa.selenium.*;
import org.openqa.selenium.chrome.ChromeDriver;

import java.io.File;
import java.nio.file.Files;
import java.nio.file.StandardCopyOption;

public class ReportedAutomation {

    public static void main(String[] args) throws Exception {

        // 1. Initialize local execution artifact directory
        new File("reports").mkdir();

        // 2. Set up Extent Reports engine
        ExtentReports extent = new ExtentReports();
        ExtentSparkReporter spark = new ExtentSparkReporter("reports/report.html");
        extent.attachReporter(spark);

        ExtentTest test = extent.createTest("OrangeHRM Automation Test");

        // 3. Launch Browser
        WebDriver driver = new ChromeDriver();
        driver.manage().window().maximize();

        // Home Page
        driver.get("https://opensource-demo.orangehrmlive.com/");
        Thread.sleep(3000);

        test.pass("Website Opened Successfully");
        capture(driver, test, "01_Home");

        // Login
        driver.findElement(By.name("username")).sendKeys("Admin");
        driver.findElement(By.name("password")).sendKeys("admin123");
        driver.findElement(By.cssSelector("button[type='submit']")).click();

        Thread.sleep(3000);

        test.pass("Login Validation Successful");
        capture(driver, test, "02_Dashboard");

        // PIM Module
        driver.findElement(By.xpath("//span[text()='PIM']")).click();
        Thread.sleep(2000);

        test.pass("PIM View Engine Loaded");
        capture(driver, test, "03_PIM");

        // Admin Module
        driver.findElement(By.xpath("//span[text()='Admin']")).click();
        Thread.sleep(2000);

        test.pass("Admin Management Frame Loaded");
        capture(driver, test, "04_Admin");


        driver.quit();

        extent.flush();

        System.out.println("Automation Completed Successfully!");
        System.out.println("Report Path: reports/report.html");
    }

    public static void capture(WebDriver driver, ExtentTest test, String name) throws Exception {

        File src = ((TakesScreenshot) driver).getScreenshotAs(OutputType.FILE);

        File dest = new File("reports/" + name + ".png");

        Files.copy(src.toPath(), dest.toPath(), StandardCopyOption.REPLACE_EXISTING);

        test.addScreenCaptureFromPath(name + ".png");
    }
}
```

---

# 🧠 Code Explanation

## 1. Create Reports Folder

```java
new File("reports").mkdir();
```

Creates a folder named **reports** where the HTML report and screenshots will be stored.

---

## 2. Initialize Extent Reports

```java
ExtentReports extent = new ExtentReports();
```

Creates the main reporting engine.

---

## 3. Configure Spark Reporter

```java
ExtentSparkReporter spark =
new ExtentSparkReporter("reports/report.html");
```

Creates a modern HTML report.

---

## 4. Attach Reporter

```java
extent.attachReporter(spark);
```

Connects the reporting engine with the HTML report.

---

## 5. Create Test

```java
ExtentTest test =
extent.createTest("OrangeHRM Automation Test");
```

Creates a test entry inside the report.

---

## 6. Log Test Steps

```java
test.pass("Website Opened Successfully");
```

Marks the current automation step as **PASS**.

---

## 7. Capture Screenshot

```java
capture(driver, test, "01_Home");
```

Captures the browser screen and attaches it to the report.

---

## 8. Generate Report

```java
extent.flush();
```

Writes all logs and screenshots to `report.html`.

---

# 🔍 Extent Reports Components

| Component | Purpose |
|------------|----------|
| ExtentReports | Main reporting engine |
| ExtentSparkReporter | HTML report generator |
| ExtentTest | Represents one test |
| test.pass() | Marks a successful step |
| addScreenCaptureFromPath() | Embeds screenshots |
| flush() | Generates the final report |

---

# 🔍 Code Breakdown: Pro Tips Used Here

## 1. Extent Reports Engine Architecture

```java
ExtentReports extent = new ExtentReports();
ExtentSparkReporter spark = new ExtentSparkReporter("reports/report.html");
extent.attachReporter(spark);
```

- **ExtentReports** manages the complete reporting lifecycle.
- **ExtentSparkReporter** generates a modern, interactive HTML report.
- **extent.flush()** writes all recorded information to disk.

---

## 2. Capturing and Embedding Screenshots

```java
File src = ((TakesScreenshot) driver)
        .getScreenshotAs(OutputType.FILE);
```

Selenium captures the browser screen into a temporary file.

The image is then copied into the **reports** directory using:

```java
Files.copy(...)
```

---

## 3. Relative Screenshot Paths

```java
test.addScreenCaptureFromPath(name + ".png");
```

Only the screenshot filename is stored.

This makes the report portable—you can copy or zip the entire **reports** folder without breaking image links.

---

# 📊 Expected Output

After execution, your project will contain:

```
ExtentReportsAutomation/
│
└── reports/
    ├── report.html
    ├── 01_Home.png
    ├── 02_Dashboard.png
    ├── 03_PIM.png
    ├── 04_Admin.png
    └── 05_Logout.png
```

Open **report.html** in any web browser to view the interactive report.

---

# ▶ How to Run

1. Install Java.
2. Add Selenium and Extent Reports dependencies.
3. Open the project in IntelliJ IDEA or Eclipse.
4. Create `ReportedAutomation.java`.
5. Paste the code.
6. Run the Java program.
7. Open `reports/report.html` after execution.

---

# ✅ Best Practices

- Create a separate reports folder.
- Capture screenshots after important steps.
- Use meaningful screenshot names.
- Keep reports portable with relative paths.
- Replace `Thread.sleep()` with explicit waits.
- Use reusable screenshot utility methods.

---

# 🚀 Future Improvements

You can enhance this project by adding:

- ✅ TestNG Integration
- ✅ Failure Screenshots
- ✅ Try-Catch Error Logging
- ✅ `test.fail()`
- ✅ `test.skip()`
- ✅ System Information
- ✅ Custom Themes
- ✅ Timestamped Report Names
- ✅ Jenkins Integration
- ✅ Email Report Generation

---

# 📚 Common Extent Reports Methods

| Method | Purpose |
|---------|----------|
| `createTest()` | Create a test |
| `pass()` | Log success |
| `fail()` | Log failure |
| `warning()` | Log warning |
| `info()` | Log information |
| `skip()` | Log skipped step |
| `flush()` | Generate report |
| `addScreenCaptureFromPath()` | Attach screenshot |

---

# ❓ Common Errors

### Report Not Generated

Ensure `extent.flush()` is called before the program ends.

---

### Screenshot Missing

Verify the screenshot was copied into the `reports` folder.

---

### NoSuchElementException

The locator is incorrect or the page has not finished loading.

---

### FileAlreadyExistsException

Use:

```java
StandardCopyOption.REPLACE_EXISTING
```

to overwrite existing screenshots.

---

# 🎯 Learning Outcomes

After completing this project, you'll understand how to:

- Generate professional HTML reports
- Log automation steps
- Capture browser screenshots
- Embed screenshots into reports
- Create reusable reporting utilities
- Organize automation artifacts

---

# ⭐ Next Challenge

Instead of logging only successful steps, wrap your Selenium actions in **try-catch** blocks. When an exception occurs, call:

```java
test.fail("Step Failed");
capture(driver, test, "Failure");
```

This automatically records the failure and embeds a screenshot at the exact point where the test failed, making debugging much easier.

---

# 🎉 Congratulations!

You have successfully integrated **Extent Reports** with **Selenium WebDriver**.

This project demonstrates how to replace basic console output with professional HTML reports that include detailed execution logs and embedded screenshots. These reporting techniques are widely used in enterprise automation frameworks to improve test visibility, simplify debugging, and communicate test results effectively.

Happy Testing! 🚀
