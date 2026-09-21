# 🚀 Getting Started with TestNG: Unit Testing in Java

A beginner-friendly guide to writing, organizing, and validating test cases using the **TestNG Framework** and **Assertions**. This project introduces the basics of TestNG annotations, test execution order, and result validation.

---

# 📖 What You Will Learn

- Introduction to TestNG
- Writing TestNG test methods
- Using the `@Test` annotation
- Controlling execution order with `priority`
- Validating results using Assertions
- Running TestNG test suites
- Understanding TestNG reports

---

# 🛠 Technologies Used

- Java
- TestNG Framework
- IntelliJ IDEA / Eclipse
- Maven (Optional)

---

# 📂 Project Structure

```
TestNGCalculatorProject/
│
├── src/
│   └── CalculatorTest.java
│
├── testng.xml (Optional)
│
├── README.md
│
└── pom.xml (Optional if using Maven)
```

---

# 📥 Prerequisites

Before running the project, make sure you have:

- Java JDK 11 or later
- IntelliJ IDEA / Eclipse
- TestNG Plugin
- Maven (Optional)

---

# 📦 Maven Dependency (Optional)

If you're using Maven, add the following dependency to your `pom.xml`.

```xml
<dependencies>

    <dependency>
        <groupId>org.testng</groupId>
        <artifactId>testng</artifactId>
        <version>7.11.0</version>
        <scope>test</scope>
    </dependency>

</dependencies>
```

---

# 🎯 Goal

Instead of running Java programs using the `main()` method, we'll execute test cases through the TestNG framework.

This project demonstrates:

- `@Test` Annotation
- Test Priorities
- Assertions
- Test Execution
- Test Reporting

---

# 🔄 Test Execution Workflow

```
Start TestNG Engine
        │
        ▼
Run Test Priority = 1
        │
        ▼
Addition Test
        │
        ▼
Assert Result = 30
        │
        ▼
Run Test Priority = 2
        │
        ▼
Subtraction Test
        │
        ▼
Assert Result = 10
        │
        ▼
Generate Test Report
        │
        ▼
End
```

---

# 💻 Java Code

Create a file named:

```
CalculatorTest.java
```

```java
import org.testng.Assert;
import org.testng.annotations.Test;

public class CalculatorTest {

    // 1. First Priority Test Case
    @Test(priority = 1)
    public void testAddition() {

        int result = 10 + 20;

        // Validating expected output vs actual calculation
        Assert.assertEquals(result, 30);

        System.out.println("Addition Test Passed");
    }

    // 2. Second Priority Test Case
    @Test(priority = 2)
    public void testSubtraction() {

        int result = 20 - 10;

        // Validating expected output vs actual calculation
        Assert.assertEquals(result, 10);

        System.out.println("Subtraction Test Passed");
    }
}
```

---

# 🧠 Code Explanation

## 1. Import TestNG Classes

```java
import org.testng.Assert;
import org.testng.annotations.Test;
```

Imports the TestNG annotation and assertion library required for writing test cases.

---

## 2. Create a Test Class

```java
public class CalculatorTest
```

Defines a Java class that contains multiple TestNG test methods.

---

## 3. The `@Test` Annotation

```java
@Test
```

Marks a method as a TestNG test case.

Unlike standard Java applications, TestNG does **not** require a `main()` method.

Any method annotated with `@Test` becomes executable by the TestNG engine.

---

## 4. Test Priority

```java
@Test(priority = 1)
```

Assigns the execution order for test methods.

Lower priority values execute first.

Example:

```
priority = 1
priority = 2
priority = 3
```

Execution order:

```
1 → 2 → 3
```

---

## 5. Perform Calculation

```java
int result = 10 + 20;
```

Calculates the actual value to be tested.

---

## 6. Validate Result

```java
Assert.assertEquals(result, 30);
```

Compares the actual value with the expected value.

If they match:

```
PASS
```

Otherwise:

```
FAIL
```

---

## 7. Console Output

```java
System.out.println("Addition Test Passed");
```

Prints a confirmation message when the assertion succeeds.

---

# 🔍 TestNG Annotations

TestNG provides many useful annotations.

| Annotation | Purpose |
|------------|----------|
| `@Test` | Marks a test method |
| `@BeforeMethod` | Runs before every test |
| `@AfterMethod` | Runs after every test |
| `@BeforeClass` | Runs before all tests in a class |
| `@AfterClass` | Runs after all tests in a class |
| `@BeforeSuite` | Runs before the test suite |
| `@AfterSuite` | Runs after the test suite |

This project uses:

```
@Test
```

---

# 🔍 Code Breakdown: Pro Tips Used Here

## 1. The `@Test` Annotation

```java
@Test
```

In a normal Java program, execution begins from the `main()` method.

With TestNG, simply adding the `@Test` annotation above a public method tells the TestNG engine to treat it as an executable test case.

This makes your test code cleaner, modular, and easier to manage.

---

## 2. Test Execution Using Priority

```java
@Test(priority = 1)
```

By default, TestNG executes test methods in alphabetical order.

The `priority` attribute allows you to override this behavior by specifying the execution sequence.

Example:

```java
@Test(priority = 1)
@Test(priority = 2)
@Test(priority = 3)
```

Execution order:

```
1 → 2 → 3
```

---

## 3. Hard Assertions (`Assert.assertEquals`)

```java
Assert.assertEquals(result, 30);
```

Assertions compare the expected value with the actual value.

If both values match:

- Test Status = **PASS**

If they do not match:

- Test Status = **FAIL**
- Execution of that test method stops immediately.

This is called a **Hard Assertion** because the test does not continue after a failed assertion.

---

# 📊 Expected Output

After running the TestNG class, your IDE console will display something similar to:

```text
Addition Test Passed
Subtraction Test Passed

===============================================
Default Suite
Total tests run: 2, Passes: 2, Failures: 0, Skips: 0
===============================================
```

---

# ▶ How to Run

1. Install Java.
2. Add the TestNG dependency.
3. Open the project in IntelliJ IDEA or Eclipse.
4. Create `CalculatorTest.java`.
5. Paste the code.
6. Right-click the class.
7. Select **Run As → TestNG Test**.
8. View the execution results and TestNG report.

---

# ✅ Best Practices

- Write one logical test per method.
- Give test methods meaningful names.
- Use assertions instead of `System.out.println()` for validation.
- Keep tests independent.
- Avoid duplicate test logic.
- Use priorities only when execution order matters.
- Prefer descriptive assertions.

---

# 🚀 Future Improvements

You can enhance this project by adding:

- ✅ `dependsOnMethods`
- ✅ `groups`
- ✅ `enabled = false`
- ✅ `@BeforeMethod`
- ✅ `@AfterMethod`
- ✅ Parameterized Tests
- ✅ Data Providers
- ✅ Soft Assertions
- ✅ Parallel Test Execution
- ✅ HTML Reports
- ✅ Selenium WebDriver Integration

---

# 📚 Common TestNG Assertions

| Assertion | Purpose |
|-----------|----------|
| `assertEquals()` | Compare two values |
| `assertNotEquals()` | Verify values are different |
| `assertTrue()` | Verify condition is true |
| `assertFalse()` | Verify condition is false |
| `assertNull()` | Verify object is null |
| `assertNotNull()` | Verify object is not null |
| `assertSame()` | Verify both references point to the same object |

---

# ❓ Common Errors

### AssertionError

The expected and actual values do not match.

---

### NoSuchMethodError

An incompatible TestNG version is being used.

---

### TestNG Plugin Missing

Your IDE may not recognize `@Test`.

Install the TestNG plugin.

---

### Class Not Found

The required TestNG dependency has not been added.

---

# 🎯 Learning Outcomes

After completing this project, you'll understand how to:

- Write TestNG test cases
- Use the `@Test` annotation
- Control execution order with priorities
- Validate outputs using assertions
- Run TestNG test suites
- Read execution reports
- Build a strong foundation for automated testing

---

# ⭐ Next Challenge

Instead of relying only on `priority`, try using:

```java
dependsOnMethods
```

to create dependencies between test methods.

Example:

```java
@Test
public void login() {

}

@Test(dependsOnMethods = "login")
public void placeOrder() {

}
```

This ensures that `placeOrder()` executes only if `login()` completes successfully.

---

## 🎉 Congratulations!

You have successfully created your **first TestNG test suite using Java**.

This project introduces the core concepts of TestNG, including annotations, execution priorities, assertions, and reporting. These fundamentals are widely used in real-world automation frameworks and serve as the foundation for advanced testing concepts such as Selenium integration, data-driven testing, parallel execution, and continuous integration.

Happy Testing! 🚀
