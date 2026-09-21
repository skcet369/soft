## Demo url

https://mouneshgouda.github.io/Hospital-Appointment/

```python
src
├── main
│   └── java
│       └── pages
│           ├── DepartmentPage.java
│           ├── DoctorPage.java
│           ├── AppointmentPage.java
│           └── PatientPage.java
│
└── test
    └── java
        └── tests
            └── HospitalAppointmentTest.java

```

```python
mkdir src\main\java\pages
mkdir src\test\java\tests


```


```python
type nul > src\main\java\pages\DepartmentPage.java
type nul > src\main\java\pages\DoctorPage.java
type nul > src\main\java\pages\AppointmentPage.java
type nul > src\main\java\pages\PatientPage.java

type nul > src\test\java\tests\HospitalAppointmentTest.java

```


##  DepartmentPage.java

```python
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class DepartmentPage {

    WebDriver driver;

    public DepartmentPage(WebDriver driver) {
        this.driver = driver;
    }

    public void selectCardiology() {
        driver.findElement(
                By.cssSelector(".department[data-dept='Cardiology']")
        ).click();
    }
}


```

## DoctorPage
```python

package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;

public class DoctorPage {

    WebDriver driver;

    public DoctorPage(WebDriver driver) {
        this.driver = driver;
    }

    public void selectDoctor() {

        WebElement doctor = driver.findElement(
                By.xpath("//h4[normalize-space()='Dr. Ananya Rao']")
        );

        doctor.findElement(
                By.xpath("./ancestor::div[contains(@class,'doctor')]")
        ).click();
    }

    public void clickNext() {
        driver.findElement(By.id("doctorNext")).click();
    }
}


```


## Appoitmentpage
```python
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class AppointmentPage {

    WebDriver driver;

    public AppointmentPage(WebDriver driver) {
        this.driver = driver;
    }

    public void selectDate() {
        driver.findElement(
                By.cssSelector(".date")
        ).click();
    }

    public void selectTime() {
        driver.findElement(
                By.cssSelector(".time:not(.booked)")
        ).click();
    }

    public void clickNext() {
        driver.findElement(
                By.id("dateNext")
        ).click();
    }
}

```


## Patientpage
```python
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class PatientPage {

    WebDriver driver;

    public PatientPage(WebDriver driver) {
        this.driver = driver;
    }

    public void enterPatientDetails() {

        driver.findElement(
                By.id("patientName")
        ).sendKeys("Rahul Kumar");

        driver.findElement(
                By.id("phone")
        ).sendKeys("9876543210");

        driver.findElement(
                By.id("email")
        ).sendKeys("rahul@gmail.com");

        driver.findElement(
                By.id("dob")
        ).sendKeys("05/15/1995");

        driver.findElement(
                By.id("gender")
        ).sendKeys("Male");

        driver.findElement(
                By.id("patientType")
        ).sendKeys("New patient");

        driver.findElement(
                By.id("reason")
        ).sendKeys("Regular consultation");
    }

    public void clickNext() {
        driver.findElement(
                By.id("patientNext")
        ).click();
    }

    public void confirmAppointment() {
        driver.findElement(
                By.id("confirmButton")
        ).click();
    }

    public String getBookingId() {
        return driver.findElement(
                By.id("bookingId")
        ).getText();
    }
}



```

## python

```python
package tests;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.Test;

import pages.AppointmentPage;
import pages.DepartmentPage;
import pages.DoctorPage;
import pages.PatientPage;

public class HospitalAppointmentTest {

    WebDriver driver;

    DepartmentPage departmentPage;
    DoctorPage doctorPage;
    AppointmentPage appointmentPage;
    PatientPage patientPage;

    @BeforeMethod
    public void setup() {

        driver = new ChromeDriver();

        driver.get(
                "https://mouneshgouda.github.io/Hospital-Appointment/"
        );

        driver.manage().window().maximize();

        departmentPage = new DepartmentPage(driver);
        doctorPage = new DoctorPage(driver);
        appointmentPage = new AppointmentPage(driver);
        patientPage = new PatientPage(driver);
    }

    @Test
    public void bookHospitalAppointment() {

        // 1. Select Cardiology
        departmentPage.selectCardiology();

        // 2. Select Doctor
        doctorPage.selectDoctor();

        // 3. Continue
        doctorPage.clickNext();

        // 4. Select Date
        appointmentPage.selectDate();

        // 5. Select Time
        appointmentPage.selectTime();

        // 6. Continue
        appointmentPage.clickNext();

        // 7. Enter Patient Details
        patientPage.enterPatientDetails();

        // 8. Continue
        patientPage.clickNext();

        // 9. Confirm Appointment
        patientPage.confirmAppointment();

        // 10. Get Appointment ID
        String appointmentId = patientPage.getBookingId();

        System.out.println(
                "Appointment booked successfully!"
        );

        System.out.println(
                "Appointment ID: " + appointmentId
        );

        // TestNG validation
        Assert.assertTrue(
                appointmentId != null && !appointmentId.isEmpty(),
                "Appointment ID was not generated"
        );
    }

    @AfterMethod
    public void tearDown() throws InterruptedException {

        Thread.sleep(3000);

        driver.quit();
    }
}

```
