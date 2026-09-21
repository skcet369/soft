# 🚌 Bus Booking Automation

A beginner-friendly **Selenium WebDriver automation project using Java, TestNG, Maven, and Page Object Model (POM)** to automate a complete bus booking workflow.

---

# 📖 What You Will Learn

* Setting up Selenium WebDriver with Java
* Launching Chrome Browser
* Using Maven dependencies
* Using TestNG
* Implementing Page Object Model (POM)
* Reading test data from a properties file
* Using `ConfigReader`
* Selecting values from dropdowns
* Locating web elements using ID and XPath
* Entering passenger details
* Selecting a bus
* Confirming a booking
* Verifying booking confirmation
* Using TestNG assertions
* Organizing a Selenium automation framework

---

# 🛠 Technologies Used

* Java
* Selenium WebDriver
* TestNG
* Maven
* Chrome Browser
* Selenium Manager
* IntelliJ IDEA / Eclipse / VS Code
* Page Object Model (POM)

---

# 🌐 Website Under Test

**Bus Booking Application**

https://mouneshgouda.github.io/busBooking/

---

# 📂 Project Structure

```text
BusBookingAutomation/
│
├── src/
│   │
│   ├── main/
│   │   └── java/
│   │       │
│   │       ├── base/
│   │       │    └── BaseTest.java
│   │       │
│   │       ├── pages/
│   │       │    ├── HomePage.java
│   │       │    ├── BusPage.java
│   │       │    ├── PassengerPage.java
│   │       │    └── ConfirmationPage.java
│   │       │
│   │       └── utils/
│   │            └── ConfigReader.java
│   │
│   └── test/
│       │
│       ├── java/
│       │    └── tests/
│       │         └── BookingTest.java
│       │
│       └── resources/
│            └── config.properties
│
└── pom.xml
```

---

# 🎯 Goal

The goal of this project is to automate a complete bus booking process.

The automation performs the following steps:

```text
Start
   │
   ▼
Launch Chrome
   │
   ▼
Open Bus Booking Website
   │
   ▼
Select From City
   │
   ▼
Select To City
   │
   ▼
Enter Journey Date
   │
   ▼
Click Search Bus
   │
   ▼
Select Bus
   │
   ▼
Enter Passenger Details
   │
   ▼
Enter Seat Number
   │
   ▼
Click Book
   │
   ▼
Verify Booking Confirmation
   │
   ▼
Close Browser
   │
   ▼
End
```

---

# 📥 Prerequisites

Before running the project, make sure you have:

* Java JDK 11 or later
* Chrome Browser
* Maven
* IntelliJ IDEA / Eclipse / VS Code
* Selenium Java
* TestNG

Modern Selenium versions can use **Selenium Manager**, so a manually downloaded ChromeDriver is generally not required.

---

# 📦 Maven Dependencies

Add the following dependencies to `pom.xml`.

```xml
<dependencies>

    <dependency>
        <groupId>org.seleniumhq.selenium</groupId>
        <artifactId>selenium-java</artifactId>
        <version>4.33.0</version>
    </dependency>

    <dependency>
        <groupId>org.testng</groupId>
        <artifactId>testng</artifactId>
        <version>7.11.0</version>
        <scope>test</scope>
    </dependency>

</dependencies>
```

---

# ⚙️ Configuration File

Create the following file:

```text
src/test/resources/config.properties
```

Add the following test data:

```properties
browser=chrome

url=https://mouneshgouda.github.io/busBooking/

from=Bangalore
to=Mumbai
date=08/10/2026

bus=Green Line Travels

name=Mounesh
age=25
phone=9876543210
seat=A1
```

> **Note:** Do not add Markdown brackets around the URL. Use `url=https://...` directly.

---

# 🧠 Why Use config.properties?

Instead of hard-coding test data:

```java
home.searchBus("Bangalore", "Mumbai", "08/10/2026");
```

the values are stored separately:

```properties
from=Bangalore
to=Mumbai
date=08/10/2026
```

and retrieved using:

```java
ConfigReader.get("from")
ConfigReader.get("to")
ConfigReader.get("date")
```

This makes the test data easier to change without modifying the Java test code.

---

# 🔧 ConfigReader.java

Location:

```text
src/main/java/utils/ConfigReader.java
```

```java
package utils;

import java.io.FileInputStream;
import java.util.Properties;

public class ConfigReader {

    static Properties p = new Properties();

    static {
        try {
            p.load(new FileInputStream(
                    "src/test/resources/config.properties"));
        }
        catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static String get(String key) {
        return p.getProperty(key);
    }
}
```

## Explanation

The `Properties` class is used to read key-value pairs from `config.properties`.

For example:

```java
ConfigReader.get("from");
```

returns:

```text
Bangalore
```

Similarly:

```java
ConfigReader.get("bus");
```

returns:

```text
Green Line Travels
```

---

# 🌐 BaseTest.java

Location:

```text
src/main/java/base/BaseTest.java
```

```java
package base;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import utils.ConfigReader;

public class BaseTest {

    public static WebDriver driver;

    public void setup() throws Exception {

        driver = new ChromeDriver();

        driver.manage().window().maximize();

        Thread.sleep(2000);

        driver.get(ConfigReader.get("url"));

        Thread.sleep(3000);
    }

    public void close() {
        driver.quit();
    }
}
```

## Explanation

### Launch Chrome

```java
driver = new ChromeDriver();
```

Creates a new Chrome browser session.

### Maximize Browser

```java
driver.manage().window().maximize();
```

Maximizes the browser window.

### Open Website

```java
driver.get(ConfigReader.get("url"));
```

The application URL is read from `config.properties`.

### Close Browser

```java
driver.quit();
```

Closes the browser and ends the WebDriver session.

---

# 🏠 HomePage.java

Location:

```text
src/main/java/pages/HomePage.java
```

```java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.support.ui.Select;

public class HomePage {

    WebDriver driver;

    public HomePage(WebDriver driver) {
        this.driver = driver;
    }

    public void searchBus(String from, String to, String date) {

        Select fromSelect =
                new Select(driver.findElement(By.id("from")));

        fromSelect.selectByVisibleText(from);

        Select toSelect =
                new Select(driver.findElement(By.id("to")));

        toSelect.selectByVisibleText(to);

        driver.findElement(By.id("date")).sendKeys(date);

        driver.findElement(
                By.xpath("//button[contains(text(),'Search Bus')]")
        ).click();
    }
}
```

## Explanation

The `HomePage` class handles the bus search functionality.

### Select From City

```java
Select fromSelect =
        new Select(driver.findElement(By.id("from")));

fromSelect.selectByVisibleText(from);
```

Selects the source city from the dropdown.

The value comes from:

```properties
from=Bangalore
```

### Select Destination

```java
Select toSelect =
        new Select(driver.findElement(By.id("to")));

toSelect.selectByVisibleText(to);
```

Selects the destination.

The value comes from:

```properties
to=Mumbai
```

### Enter Date

```java
driver.findElement(By.id("date")).sendKeys(date);
```

Enters the journey date.

```properties
date=08/10/2026
```

### Search Bus

```java
driver.findElement(
        By.xpath("//button[contains(text(),'Search Bus')]")
).click();
```

Clicks the Search Bus button.

---

# 🚌 BusPage.java

Location:

```text
src/main/java/pages/BusPage.java
```

```java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class BusPage {

    WebDriver driver;

    public BusPage(WebDriver driver) {
        this.driver = driver;
    }

    public void selectBus(String busName) {

        driver.findElement(
                By.xpath("//tr[td='" + busName + "']//button")
        ).click();
    }
}
```

## Explanation

The bus name is passed dynamically from the configuration file.

```properties
bus=Green Line Travels
```

The test calls:

```java
bus.selectBus(
        ConfigReader.get("bus")
);
```

The XPath dynamically searches for the row containing the requested bus and clicks its button.

---

# 👤 PassengerPage.java

Location:

```text
src/main/java/pages/PassengerPage.java
```

```java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class PassengerPage {

    WebDriver driver;

    public PassengerPage(WebDriver driver) {
        this.driver = driver;
    }

    public void enterDetails(
            String name,
            String age,
            String phone,
            String seat) {

        driver.findElement(By.id("name")).sendKeys(name);

        driver.findElement(By.id("age")).sendKeys(age);

        driver.findElement(By.id("phone")).sendKeys(phone);

        driver.findElement(By.id("seat")).sendKeys(seat);
    }

    public void confirmBooking() {

        driver.findElement(
                By.xpath("//button[contains(text(),'Book')]")
        ).click();
    }
}
```

## Explanation

The passenger information is stored in `config.properties`.

```properties
name=Mounesh
age=25
phone=9876543210
seat=A1
```

The `enterDetails()` method enters these values into the passenger form.

The `confirmBooking()` method clicks the Book button.

---

# ✅ ConfirmationPage.java

Location:

```text
src/main/java/pages/ConfirmationPage.java
```

```java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class ConfirmationPage {

    WebDriver driver;

    public ConfirmationPage(WebDriver driver) {
        this.driver = driver;
    }

    public boolean verifyBooking() {

        return driver.findElement(
                By.xpath("//h1[contains(text(),'Booking Confirmed')]")
        ).isDisplayed();
    }
}
```

## Explanation

This page is responsible for verifying that the booking was successfully completed.

The method searches for:

```xpath
//h1[contains(text(),'Booking Confirmed')]
```

If the heading is displayed, the method returns:

```text
true
```

---

# 🧪 BookingTest.java

Location:

```text
src/test/java/tests/BookingTest.java
```

```java
package tests;

import org.testng.Assert;
import org.testng.annotations.*;

import base.BaseTest;
import pages.*;
import utils.ConfigReader;

public class BookingTest extends BaseTest {

    @BeforeMethod
    public void start() throws Exception {
        setup();
    }

    @Test
    public void bookingTest() {

        // Step 1: Search Bus
        HomePage home = new HomePage(driver);

        home.searchBus(
                ConfigReader.get("from"),
                ConfigReader.get("to"),
                ConfigReader.get("date")
        );

        // Step 2: Select Bus
        BusPage bus = new BusPage(driver);

        bus.selectBus(
                ConfigReader.get("bus")
        );

        // Step 3: Enter Passenger Details
        PassengerPage passenger = new PassengerPage(driver);

        passenger.enterDetails(
                ConfigReader.get("name"),
                ConfigReader.get("age"),
                ConfigReader.get("phone"),
                ConfigReader.get("seat")
        );

        // Step 4: Click Book/Confirm Button
        passenger.confirmBooking();

    }

    @AfterMethod
    public void end() {
        close();
    }
}
```

---

# 🧠 BookingTest Explanation

`BookingTest` is the main test class.

It extends:

```java
BaseTest
```

Therefore it can use the WebDriver and browser setup methods from `BaseTest`.

---

## Step 1 — Search Bus

```java
HomePage home = new HomePage(driver);

home.searchBus(
        ConfigReader.get("from"),
        ConfigReader.get("to"),
        ConfigReader.get("date")
);
```

The test reads:

```text
From     → Bangalore
To       → Mumbai
Date     → 08/10/2026
```

from the configuration file.

---

## Step 2 — Select Bus

```java
BusPage bus = new BusPage(driver);

bus.selectBus(
        ConfigReader.get("bus")
);
```

The selected bus is:

```text
Green Line Travels
```

---

## Step 3 — Enter Passenger Details

```java
PassengerPage passenger = new PassengerPage(driver);

passenger.enterDetails(
        ConfigReader.get("name"),
        ConfigReader.get("age"),
        ConfigReader.get("phone"),
        ConfigReader.get("seat")
);
```

The passenger details are:

```text
Name  : Mounesh
Age   : 25
Phone : 9876543210
Seat  : A1
```

---

## Step 4 — Confirm Booking

```java
passenger.confirmBooking();
```

Clicks the Book button.

---

## Step 5 — Verify Booking

```java
ConfirmationPage confirmation =
        new ConfirmationPage(driver);

Assert.assertTrue(
        confirmation.verifyBooking(),
        "Booking confirmation was not displayed"
);
```

This verifies that the booking confirmation is displayed.

Using an assertion is better than simply printing a message because TestNG can automatically mark the test as **PASS** or **FAIL**.

---

# 🔄 Complete Automation Flow

```text
                  BookingTest
                       │
                       ▼
                BaseTest.setup()
                       │
                       ▼
              Launch Chrome Browser
                       │
                       ▼
                Open Application
                       │
                       ▼
                  HomePage
                       │
              ┌────────┴────────┐
              ▼                 ▼
       Select Bangalore    Select Mumbai
              │                 │
              └────────┬────────┘
                       ▼
                 Enter Date
                       │
                       ▼
                 Search Bus
                       │
                       ▼
                   BusPage
                       │
                       ▼
            Select Green Line Travels
                       │
                       ▼
               PassengerPage
                       │
              ┌────────┼────────┐
              ▼        ▼        ▼
            Name      Age      Phone
                       │
                       ▼
                     Seat
                       │
                       ▼
                  Click Book
                       │
                       ▼
              ConfirmationPage
                       │
                       ▼
            Verify Booking Confirmed
                       │
                       ▼
                TestNG Assertion
                       │
                       ▼
              BaseTest.close()
                       │
                       ▼
                      End
```

---

# 🏗️ Page Object Model

This project follows the **Page Object Model (POM)** design pattern.

Each page has its own Java class.

```text
HomePage.java
    ↓
Handles bus search

BusPage.java
    ↓
Handles bus selection

PassengerPage.java
    ↓
Handles passenger information

ConfirmationPage.java
    ↓
Handles booking verification
```

The test class controls the overall workflow.

This keeps the framework:

* Clean
* Readable
* Reusable
* Maintainable
* Scalable

---

# 🔍 Locator Strategies Used

## ID

The project uses ID locators for form fields:

```java
By.id("from")
```

```java
By.id("to")
```

```java
By.id("date")
```

```java
By.id("name")
```

```java
By.id("age")
```

```java
By.id("phone")
```

```java
By.id("seat")
```

---

## XPath

The project also uses XPath for buttons and dynamic elements.

### Search Bus

```java
By.xpath("//button[contains(text(),'Search Bus')]")
```

### Select Bus

```java
By.xpath("//tr[td='" + busName + "']//button")
```

### Book Button

```java
By.xpath("//button[contains(text(),'Book')]")
```

### Booking Confirmation

```java
By.xpath("//h1[contains(text(),'Booking Confirmed')]")
```

---

# ⌨️ Selenium Methods Used

| Method                  | Purpose                                |
| ----------------------- | -------------------------------------- |
| `get()`                 | Opens a webpage                        |
| `findElement()`         | Locates an element                     |
| `sendKeys()`            | Enters text                            |
| `click()`               | Clicks an element                      |
| `isDisplayed()`         | Checks whether an element is displayed |
| `quit()`                | Closes the browser                     |
| `maximize()`            | Maximizes the browser                  |
| `selectByVisibleText()` | Selects an option from a dropdown      |

---

# 🧪 TestNG Annotations Used

## `@BeforeMethod`

```java
@BeforeMethod
public void start() throws Exception {
    setup();
}
```

Runs before every test method.

---

## `@Test`

```java
@Test
public void bookingTest() {
}
```

Marks the method as a TestNG test.

---

## `@AfterMethod`

```java
@AfterMethod
public void end() {
    close();
}
```

Runs after the test and closes the browser.

---

# 📊 Test Data

| Property | Value              |
| -------- | ------------------ |
| Browser  | Chrome             |
| From     | Bangalore          |
| To       | Mumbai             |
| Date     | 08/10/2026         |
| Bus      | Green Line Travels |
| Name     | Mounesh            |
| Age      | 25                 |
| Phone    | 9876543210         |
| Seat     | A1                 |

---

# ▶️ How to Run

## 1. Install Java

Install JDK 11 or later.

Verify:

```bash
java -version
```

---

## 2. Install Maven

Verify:

```bash
mvn -version
```

---

## 3. Open the Project

Open `BusBookingAutomation` in IntelliJ IDEA, Eclipse, or VS Code.

---

## 4. Update `config.properties`

Make sure the test data is correct:

```properties
browser=chrome
url=https://mouneshgouda.github.io/busBooking/
from=Bangalore
to=Mumbai
date=08/10/2026
bus=Green Line Travels
name=Mounesh
age=25
phone=9876543210
seat=A1
```

---

## 5. Run BookingTest

Run:

```text
BookingTest.java
```

or run the test using Maven:

```bash
mvn test
```

---

# 📊 Expected Result

The automation should:

```text
Launch Chrome
      ↓
Open Bus Booking Website
      ↓
Search Bangalore → Mumbai
      ↓
Select Green Line Travels
      ↓
Enter Mounesh's Details
      ↓
Select Seat A1
      ↓
Click Book
      ↓
Display Booking Confirmed
      ↓
Test PASSED
```

Expected TestNG result:

```text
PASSED
```

If the confirmation message is not displayed, the assertion fails:

```text
FAILED
```

with:

```text
Booking confirmation was not displayed
```

---

# ⚠️ Common Errors

## SessionNotCreatedException

Possible reasons:

* Chrome version and driver compatibility issue
* Browser installation problem

Modern Selenium versions use Selenium Manager to help manage the browser driver.

---

## NoSuchElementException

Possible reasons:

* Incorrect locator
* Element is not available
* Page has not loaded
* Application HTML has changed

Check the locator and application page.

---

## TimeoutException

The page or element may take longer to load.

For real-world automation, use explicit waits instead of fixed delays.

---

## Configuration File Error

Make sure the configuration file is located at:

```text
src/test/resources/config.properties
```

---

# ⚠️ Improvement: Explicit Waits

The current project uses:

```java
Thread.sleep(2000);
```

and:

```java
Thread.sleep(3000);
```

This is acceptable for a beginner experiment, but explicit waits are recommended for a professional automation framework.

Example:

```java
WebDriverWait wait =
        new WebDriverWait(driver, Duration.ofSeconds(10));

wait.until(
        ExpectedConditions.visibilityOfElementLocated(
                By.id("from")
        )
);
```

Explicit waits allow Selenium to wait for a specific condition instead of waiting for a fixed amount of time.

---

# 🚀 Future Improvements

The framework can be enhanced with:

* ✅ Explicit Waits
* ✅ TestNG Assertions
* ✅ TestNG DataProvider
* ✅ Multiple Test Cases
* ✅ Screenshot on Failure
* ✅ Extent Reports
* ✅ Allure Reports
* ✅ Excel Data-Driven Testing
* ✅ CSV Data-Driven Testing
* ✅ Cross-Browser Testing
* ✅ Headless Execution
* ✅ Logging
* ✅ Git and GitHub
* ✅ GitHub Actions
* ✅ Jenkins CI/CD
* ✅ Parallel Test Execution

---

# 🧪 Future Test Scenarios

### Successful Booking

```text
Bangalore → Mumbai
Green Line Travels
Valid passenger details

Expected:
Booking Confirmed
```

### Invalid Passenger Details

```text
Enter invalid phone number

Expected:
Validation message
```

### Empty Passenger Name

```text
Leave name field empty

Expected:
Validation message
```

### Invalid Seat

```text
Enter invalid seat number

Expected:
Validation message
```

### Different Bus

```text
Select another available bus

Expected:
Successful booking
```

---

# 📚 Learning Outcomes

After completing this project, you will understand how to:

* Launch a browser using Selenium
* Navigate to a website
* Locate web elements
* Select dropdown values
* Enter user information
* Click buttons
* Use XPath
* Read external test data
* Create a reusable configuration reader
* Use Page Object Model
* Use TestNG
* Write assertions
* Organize Selenium projects
* Automate an end-to-end business workflow

---

# ⭐ Key Concept

The main idea of this framework is:

```text
config.properties
       │
       ▼
ConfigReader
       │
       ▼
BookingTest
       │
       ├── HomePage
       │
       ├── BusPage
       │
       ├── PassengerPage
       │
       └── ConfirmationPage
       │
       ▼
     Result
```

The **test data**, **browser setup**, **page actions**, and **test execution** are separated into different components.

This is the basic structure used when building larger Selenium automation frameworks.

---

# 🎉 Conclusion

The **BusBookingAutomation** project is a simple end-to-end Selenium automation framework built using:

* Java
* Selenium WebDriver
* TestNG
* Maven
* Page Object Model
* Properties-based test data

The project demonstrates a complete bus booking workflow from searching for a bus to verifying the booking confirmation.

It provides a strong foundation for learning advanced Selenium concepts such as explicit waits, data-driven testing, reporting, cross-browser testing, and CI/CD.

**Happy Testing! 🚀🚌**
