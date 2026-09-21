## Hotel booking

https://mouneshgouda.github.io/HotelBooking/index.html


### Project Structure

```text
├── src
│   ├── main
│   │   ├── java
│   │   │   ├──
│   │   │   ├── pages
│   │   │   │   ├── BookingPage.java
│   │   │   │   ├── HistoryPage.java
│   │   │   │   ├── HomePage.java
│   │   │   │   └── RoomsPage.java
│   │   │   └── tests
│   │   │       └── HotelTest.java




```
## Folder Cmds

```python
mkdir src\main\java\pages
mkdir src\main\java\tests


```

```python

type nul > src\main\java\pages\BookingPage.java
type nul > src\main\java\pages\HistoryPage.java
type nul > src\main\java\pages\HomePage.java
type nul > src\main\java\pages\RoomsPage.java
type nul > src\main\java\tests\HotelTest.java
```



## Mac Cmds

```python
mkdir -p src/main/java/pages
mkdir -p src/main/java/tests



```

```python

touch src/main/java/pages/BookingPage.java
touch src/main/java/pages/HistoryPage.java
touch src/main/java/pages/HomePage.java
touch src/main/java/pages/RoomsPage.java
touch src/main/java/tests/HotelTest.java
```
## HomePage.java
```python
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class HomePage {

    WebDriver driver;

    public HomePage(WebDriver driver) {
        this.driver = driver;
    }

    public void openWebsite() {

        driver.get(
                "https://mouneshgouda.github.io/HotelBooking/"
        );
    }


    public void searchRoom(String checkIn, String checkOut, String guests) {

        driver.findElement(By.id("checkIn"))
                .sendKeys(checkIn);

        driver.findElement(By.id("checkOut"))
                .sendKeys(checkOut);

        driver.findElement(By.id("guests"))
                .sendKeys(guests);

        driver.findElement(By.id("searchRooms"))
                .click();
    }
}

```

## RoomsPage.java
```python

package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.JavascriptExecutor;

public class RoomsPage {

    WebDriver driver;

    public RoomsPage(WebDriver driver) {
        this.driver = driver;
    }


    public void bookRoom() throws InterruptedException {


        WebElement button =
                driver.findElement(
                        By.xpath("(//button[contains(text(),'Book Reservation')])[1]")
                );


        JavascriptExecutor js =
                (JavascriptExecutor) driver;


        js.executeScript(
                "arguments[0].scrollIntoView(true);",
                button
        );


        Thread.sleep(1000);


        button.click();
    }
}

```

## BookingPage

```python
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.JavascriptExecutor;

public class BookingPage {

    WebDriver driver;


    public BookingPage(WebDriver driver) {
        this.driver = driver;
    }


    public void enterDetails() throws InterruptedException {


        driver.findElement(By.id("name"))
                .sendKeys("John Smith");


        driver.findElement(By.id("email"))
                .sendKeys("johnsmith@gmail.com");


        JavascriptExecutor js =
                (JavascriptExecutor) driver;



        WebElement checkIn =
                driver.findElement(By.id("bookingCheckIn"));


        js.executeScript(
                "arguments[0].value='2026-08-10';",
                checkIn
        );



        WebElement checkOut =
                driver.findElement(By.id("bookingCheckOut"));


        js.executeScript(
                "arguments[0].value='2026-08-12';",
                checkOut
        );



        driver.findElement(By.id("bookingGuests"))
                .clear();


        driver.findElement(By.id("bookingGuests"))
                .sendKeys("2");


        Thread.sleep(2000);
    }



    public void confirmBooking() throws InterruptedException {


        WebElement button =
                driver.findElement(
                        By.xpath("//button[contains(text(),'Confirm Reservation')]")
                );


        JavascriptExecutor js =
                (JavascriptExecutor) driver;


        js.executeScript(
                "arguments[0].scrollIntoView(true);",
                button
        );


        Thread.sleep(1000);


        button.click();
    }
}


```

## History.java

```python
package pages;

import org.openqa.selenium.WebDriver;

public class HistoryPage {

    WebDriver driver;


    public HistoryPage(WebDriver driver) {
        this.driver = driver;
    }


    public void verifyPage() {
          System.out.println("Booking Done");


    }
}


```

tests/HotelTest

```python
package tests;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.*;

import pages.*;

import java.time.Duration;

public class HotelTest {

    WebDriver driver;

    HomePage home;
    RoomsPage rooms;
    BookingPage booking;
    HistoryPage history;

    @BeforeMethod
    public void setup() {

        driver = new ChromeDriver();

        driver.manage().window().maximize();
        home = new HomePage(driver);
        rooms = new RoomsPage(driver);
        booking = new BookingPage(driver);
        history = new HistoryPage(driver);
    }
    @Test
    public void hotelBookingTest() throws Exception {

        home.openWebsite();

        home.searchRoom(
                "08/10/2026",
                "08/12/2026",
                "2"
        );

        Thread.sleep(2000);

        rooms.bookRoom();

        Thread.sleep(2000);

        booking.enterDetails();
        booking.confirmBooking();

        Thread.sleep(3000);

        history.verifyPage();
    }

    @AfterMethod
    public void tearDown() {
          driver.quit();

       
        }
    }
}
```
