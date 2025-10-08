# Unit Testing (Java)

## Types of Tests

### The Testing Pyramid Model

```
                    /\
                   /  \
                  / E2E \          ← End-to-End / UI Tests
                 /______\
                /        \
               /Integration\       ← Integration Tests
              /____________\
             /              \
            /  Unit Tests    \     ← Unit Tests
           /__________________\
```

**Key Principle**: More tests at the bottom, fewer at the top

### Levels of Testing

| Level           | Scope               | Speed  | Cost (create/debug) | Quantity   | Maintenance |
| :-------------- | :------------------ | :----- | :------------------ | :--------- | :---------- |
| **Unit**        | Single component    | fast   | Low                 | Many (70%) | Easy        |
| **Integration** | Multiple components | Medium | Medium              | Some (20%) | Moderate    |
| **System/E2E**  | Entire application  | Slow   | High                | Few (10%)  | Difficult   |


### Unit Tests (Base of Pyramid)

**Scope:** Individual methods, classes, or functions in isolation

**Characteristics:**
- Test smallest pieces of code
- Mock/stub external dependencies
- Run in milliseconds
- No database, network, or file system

**Example:**
```java
@Test
public void testCalculateTax() {
    TaxCalculator calc = new TaxCalculator();
    double tax = calc.calculate(100.0, 0.15);
    assertEquals(15.0, tax);
}
```

**When to Use:** every time you add/modify code (aspirational goal: 100% coverage)

**Proportion:** ~70% of your test suite

### Integration Tests (Middle of Pyramid)

**Scope:** How multiple components work together

**Characteristics:**
- Test interaction between modules
- May involve real databases, APIs, or file systems
- Run in seconds
- Verify communication between layers

**Example:**
```java
@Test
public void testSaveUserToDatabase() {
    UserRepository repo = new UserRepository(realDatabase);
    UserService service = new UserService(repo);
    
    User user = service.createUser("john@example.com", "John");
    
    User retrieved = repo.findById(user.getId());
    assertEquals("john@example.com", retrieved.getEmail());
}
```

**Types of Integration Tests:**
- **Component Integration:** Testing interaction between classes
- **Database Integration:** Testing DAO/Repository layers with real DB
- **API Integration:** Testing REST endpoints
- **Service Integration:** Testing calls to external services

**When to Use:**
- Testing data access layers
- Verifying API contracts
- Checking configuration and wiring
- Validating cross-component workflows

**Proportion:** ~20% of your test suite

### System/End-to-End Tests (Top of Pyramid)

**Scope:** Entire application from user perspective

**Characteristics:**
- Test complete user workflows
- Run through UI or full API stack
- Run in minutes
- Use real or production-like environment

**Example (Selenium):**
```java
@Test
public void testUserRegistrationFlow() {
    driver.get("http://localhost:8080/register");
    driver.findElement(By.id("email")).sendKeys("test@example.com");
    driver.findElement(By.id("password")).sendKeys("password123");
    driver.findElement(By.id("submit")).click();
    
    String welcome = driver.findElement(By.id("welcome")).getText();
    assertEquals("Welcome, test@example.com!", welcome);
}
```

**Also Known As:**
- E2E (End-to-End) tests
- UI tests
- Acceptance tests
- System tests

**When to Use:**
- Testing critical user journeys
- Validating entire feature flows
- Smoke testing after deployment
- Regression testing major functionality

**Proportion:** ~10% of your test suite

### Other Testing Types (Beyond the Pyramid)

#### Acceptance Tests
- Verify business requirements are met
- Often written with business stakeholders
- May use BDD (Behavior-Driven Development) tools like Cucumber

#### Performance Tests
- Load testing, stress testing, scalability testing
- Verify system performs under expected/extreme load

#### Security Tests
- Penetration testing, vulnerability scanning
- Verify authentication, authorization, data protection

#### Manual Testing
- Exploratory testing
- Usability testing
- Tests that are too complex or expensive to automate

### Test Execution Strategy

**During Development:**
```
Unit tests → Run continuously (every save)
Integration tests → Run before commit
E2E tests → Run before push
```

**In CI/CD Pipeline:**
```
Commit → Run unit tests (30 seconds)
   ↓
   ✓ Pass → Run integration tests (5 minutes)
   ↓
   ✓ Pass → Run E2E tests (30 minutes)
   ↓
   ✓ Pass → Deploy to staging
```

### Decision Tree: Which Test Type?

**Questions to ask:**
1. **Am I testing a single method/class?** → Unit Test
2. **Am I testing how two components interact?** → Integration Test
3. **Am I testing a complete user workflow?** → E2E Test
4. **Does it need a database/network?** → Integration or E2E
5. **Can I mock dependencies?** → Unit Test

## Focus: Unit Test

- Why focus on unit test?
  - Part of your coding workflow
    - No commits w/o unit tests!
  - The most critical part of any testing strategy
- Benefits include:
  - Catch bugs early in development cycle
  - Make refactoring safer
  - Serve as documentation for code behavior
  - Reduce debugging time
  - Increase confidence in code changes
  - Support continuous integration/deployment

## JUnit Framework

**JUnit** is the most popular unit testing framework for Java
- Current version: JUnit 5 (also called JUnit Jupiter)
- Provides annotations, assertions, and test runners
- Integrates with IDEs and build tools (Ant, Maven, Gradle)

**Ant Target:**
```xml
<!-- Target: Run JUnit tests -->
<target name="test" depends="compile-tests" description="Run JUnit tests">
    <junit printsummary="yes" haltonfailure="no" fork="true">
        <classpath refid="test.classpath"/>
        
        <!-- Format test output -->
        <formatter type="plain" usefile="false"/>
        <formatter type="xml"/>
        
        <!-- Run all test classes -->
        <batchtest todir="${reports.dir}">
            <fileset dir="${test.classes.dir}">
                <include name="**/*Test.class"/>
            </fileset>
        </batchtest>
    </junit>
    
    <echo message="Test execution complete. Reports in ${reports.dir}"/>
</target>
```

## Basic Test Structure

**Anatomy of a Test Class:**
```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {
    
    @Test
    public void testAddition() {
        // Arrange (setup)
        Calculator calc = new Calculator();
        
        // Act (execute)
        int result = calc.add(2, 3);
        
        // Assert (verify)
        assertEquals(5, result);
    }
}
```

**AAA Pattern:**
- **Arrange**: Set up test data and preconditions
- **Act**: Execute the method being tested
- **Assert**: Verify the expected outcome

## Common JUnit Annotations

| Annotation     | Purpose                                     |
| :------------- | :------------------------------------------ |
| `@Test`        | Marks a method as a test method             |
| `@BeforeEach`  | Runs before each test method                |
| `@AfterEach`   | Runs after each test method                 |
| `@BeforeAll`   | Runs once before all tests (must be static) |
| `@AfterAll`    | Runs once after all tests (must be static)  |
| `@Disabled`    | Temporarily disable a test                  |
| `@DisplayName` | Provide custom display name for test        |

**Example:**
```java
public class UserServiceTest {
    private UserService userService;
    
    @BeforeEach
    public void setUp() {
        userService = new UserService();
    }
    
    @Test
    @DisplayName("Should create user with valid email")
    public void testCreateUser() {
        User user = userService.create("john@example.com");
        assertNotNull(user);
    }
}
```

## Common Assertions

**Basic Assertions:**
```java
// Equality
assertEquals(expected, actual);
assertNotEquals(value1, value2);

// Boolean conditions
assertTrue(condition);
assertFalse(condition);

// Null checks
assertNull(object);
assertNotNull(object);

// Object identity
assertSame(expected, actual);
assertNotSame(obj1, obj2);

// Array equality
assertArrayEquals(expectedArray, actualArray);
```

**Exception Testing:**
```java
@Test
public void testDivisionByZero() {
    Calculator calc = new Calculator();
    assertThrows(ArithmeticException.class, () -> {
        calc.divide(10, 0);
    });
}
```

**Custom Messages:**
```java
assertEquals(5, result, "Addition should return correct sum");
```

## Test Organization Best Practices

**Naming Conventions:**
- Test class: `<ClassUnderTest>Test`
  - e.g. `CalculatorTest`
- Test method: `test<MethodName>_<Scenario>_<ExpectedResult>`
  - e.g. `testDivide_WithZeroDivisor_ThrowsException`

**One Assert Per Test (Guideline):**
- Focus each test on one behavior
- Makes failures easier to diagnose
- Not a strict rule, but generally good practice

**Test Independence:**
- Tests should not depend on each other
- Each test should be runnable in isolation
- Use `@BeforeEach` to set up fresh state

## Testing Different Scenarios

**Test Edge Cases:**
```java
@Test
public void testEmptyString() {
    assertTrue(StringUtils.isEmpty(""));
}

@Test
public void testNullInput() {
    assertThrows(NullPointerException.class, 
        () -> StringUtils.reverse(null));
}

@Test
public void testLargeNumber() {
    assertEquals(Integer.MAX_VALUE, calc.add(Integer.MAX_VALUE, 0));
}
```

**Parameterized Tests:**
```java
@ParameterizedTest
@ValueSource(ints = {1, 2, 3, 5, 8})
public void testIsPositive(int number) {
    assertTrue(number > 0);
}

@ParameterizedTest
@CsvSource({"2,3,5", "10,20,30", "0,0,0"})
public void testAdd(int a, int b, int expected) {
    assertEquals(expected, calc.add(a, b));
}
```

## Code Coverage

**What is Code Coverage?**
- Metric indicating percentage of code executed by tests
- Types: line coverage, method coverage
- 

**Common Tools:**
- JaCoCo (Java Code Coverage)
- IntelliJ built-in coverage
- SonarQube

**Target:**
- Aim for 70-90% coverage
- 100% isn't always practical or necessary
- Coverage ≠ quality (you can have high coverage with poor tests)

## Test-Driven Development (TDD)

**The TDD Cycle:**
1. **Red**: Write a failing test first
2. **Green**: Write minimal code to make test pass
3. **Refactor**: Improve code while keeping tests green

**Benefits:**
- Forces you to think about design before implementation
- Ensures testable code
- Provides immediate feedback
- Results in better test coverage

## 10. Common Pitfalls to Avoid

- ❌ **Testing implementation details instead of behavior**
- ❌ **Tests that depend on execution order**
- ❌ **Tests with too much setup (code smell)**
- ❌ **Ignoring failing tests**
- ❌ **Not testing edge cases and error conditions**
- ❌ **Copy-pasting test code (DRY principle applies)**

## Example: Complete Test Class

```java
import org.junit.jupiter.api.*;
import static org.junit.jupiter.api.Assertions.*;

public class BankAccountTest {
    private BankAccount account;
    
    @BeforeEach
    public void setUp() {
        account = new BankAccount("12345", 100.0);
    }
    
    @Test
    @DisplayName("Deposit should increase balance")
    public void testDeposit() {
        account.deposit(50.0);
        assertEquals(150.0, account.getBalance());
    }
    
    @Test
    @DisplayName("Withdraw valid amount should decrease balance")
    public void testWithdraw() {
        account.withdraw(30.0);
        assertEquals(70.0, account.getBalance());
    }
    
    @Test
    @DisplayName("Withdraw more than balance should throw exception")
    public void testWithdrawInsufficientFunds() {
        assertThrows(InsufficientFundsException.class, 
            () -> account.withdraw(200.0));
    }
    
    @Test
    @DisplayName("Negative deposit should throw exception")
    public void testNegativeDeposit() {
        assertThrows(IllegalArgumentException.class, 
            () -> account.deposit(-10.0));
    }
    
    @AfterEach
    public void tearDown() {
        account = null;
    }
}
```

## Key Takeaways

- ✅ Unit tests verify individual components work correctly
- ✅ JUnit is the standard framework for Java unit testing
- ✅ Follow AAA pattern: Arrange, Act, Assert
- ✅ Test normal cases, edge cases, and error conditions
- ✅ Write independent, focused tests with clear names
- ✅ Aim for good coverage, but prioritize quality over quantity
- ✅ Unit testing is an investment that pays off in maintainability

**Additional Resources:**
- JUnit 5 User Guide: https://junit.org/junit5/docs/current/user-guide/


