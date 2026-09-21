# 🚌 Bus Booking Automation Framework

This project demonstrates a **Hybrid Selenium Automation Framework** using **Java, Maven, TestNG, and Page Object Model (POM)** to automate a bus booking application.

---

## 📥 Download Source Code

Click below to download the original bus booking website source code:

[Demo url] (https://mouneshgouda.github.io/busBooking/)




[Download ZIP](https://mouneshgouda.github.io/busBooking/)

# 📁 Project Structure

# Bus Booking Automation Framework

## Project Structure

```text
BusBookingAutomation

├── src
│   │
│   ├── main
│   │   └── java
│   │       │
│   │       ├── base
│   │       │    └── BaseTest.java
│   │       │
│   │       ├── pages
│   │       │    ├── HomePage.java
│   │       │    ├── BusPage.java
│   │       │    ├── PassengerPage.java
│   │       │    └── ConfirmationPage.java
│   │       │
│   │       └── utils
│   │            └── ConfigReader.java
│   │
│   └── test
│       │
│       ├── java
│       │    └── tests
│       │         └── BookingTest.java
│       │
│       └── resources
│            └── config.properties
```

---

# Create the Project Structure

## Step 1: Create a Maven Project

Create a new **Maven Project** in your preferred IDE (IntelliJ IDEA or Eclipse).

---

## Step 2: Create Packages

Under **src/main/java**, create the following packages:

- `base`
- `pages`
- `utils`

Under **src/test/java**, create the following package:

- `tests`

---

## Step 3: Create Resource Directory

Under **src/test**, create the **resources** directory.

```
src
└── test
    └── resources
```

Inside the **resources** folder, create:

```
config.properties
```

---

# Create Packages Using Terminal

## 🖥️ Windows (Command Prompt)

Navigate to your project directory.

```cmd
cd BusBookingAutomation
```

Create packages:

```cmd
mkdir src\main\java\base
mkdir src\main\java\pages
mkdir src\main\java\utils
mkdir src\test\java\tests
mkdir src\test\resources
```

Create Java files:

```cmd
type nul > src\main\java\base\BaseTest.java
type nul > src\main\java\pages\HomePage.java
type nul > src\main\java\pages\BusPage.java
type nul > src\main\java\pages\PassengerPage.java
type nul > src\main\java\pages\ConfirmationPage.java
type nul > src\main\java\utils\ConfigReader.java
type nul > src\test\java\tests\BookingTest.java
type nul > src\test\resources\config.properties
```

---

## 🍎 macOS / Linux (Terminal)

Navigate to your project directory.

```bash
cd BusBookingAutomation
```

Create packages:

```bash
mkdir -p src/main/java/base
mkdir -p src/main/java/pages
mkdir -p src/main/java/utils
mkdir -p src/test/java/tests
mkdir -p src/test/resources
```

Create Java files:

```bash
touch src/main/java/base/BaseTest.java
touch src/main/java/pages/HomePage.java
touch src/main/java/pages/BusPage.java
touch src/main/java/pages/PassengerPage.java
touch src/main/java/pages/ConfirmationPage.java
touch src/main/java/utils/ConfigReader.java
touch src/test/java/tests/BookingTest.java
touch src/test/resources/config.properties
```

---

## ConfigReader
```python


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
        catch(Exception e){
            e.printStackTrace();
        }
    }
    public static String get(String key){

        return p.getProperty(key);

    }

}


```
## BaseTest
```python


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
    public void close(){
        driver.quit();

    }
}


```

## HomePage

```python
package pages;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.support.ui.Select;

public class HomePage {
    WebDriver driver;
    public HomePage(WebDriver driver){
        this.driver=driver;
    }
    public void searchBus(String from,String to ,String date){
        Select selectfrom =new Select(driver.findElement(By.id("from")));
        selectfrom.selectByVisibleText(from);
        Select toselect =new Select(driver.findElement(By.id("to")));
        toselect.selectByVisibleText(to);
        driver.findElement(By.id("date")).sendKeys(date);
        driver.findElement(By.xpath("//button[conatins(text(),'Search Bus'])")).click();
    }


}

```


