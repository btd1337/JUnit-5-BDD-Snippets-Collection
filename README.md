# 📦 JUnit 5 BDD Snippets Collection

A collection of Eclipse snippets following JUnit 5 best practices, Clean Code principles, and Behavior Driven Development (BDD).

## 🚀 Available Snippets

### 1. 🔧 Basic BDD Snippet
**Template Name:** `junit5_bdd_basic_test`

**Context:** Simple unit tests with Given-When-Then structure

```java
@Test
@DisplayName("${testName}")
void ${methodName}() {
	// Given
	final ${firstType} ${firstVar} = ${firstValue};
	final ${secondType} ${secondVar} = ${secondValue};
	final ${expectedType} expectedResult = ${expectedValue};

	// When
	final ${resultType} actualResult = ${classUnderTest}.${methodUnderTest}(${firstVar}, ${secondVar});

	// Then
	assertNotNull(actualResult, "${resultMessage}");
	assertEquals(expectedResult, actualResult, ${delta}, 
		() -> String.format("${formatMessage}"));
}
```

### 2. 📊 Parameterized CSV Snippet

**Template Name:** `junit5_bdd_parametrized_csv`

**Context:** Tests with multiple data sets

```java
@ParameterizedTest
@DisplayName("${testName}")
@CsvSource({
	"${csvData}"
})
void ${methodName}(${parameterTypes}) {
	// When
	final ${resultType} actualResult = ${classUnderTest}.${methodUnderTest}(${firstVar}, ${secondVar});

	// Then
	assertEquals(${expectedVar}, actualResult, ${delta},
		() -> String.format("${formatMessage}"));
}
```

### 3. 🏗️ Complete Test Class Snippet

**Template Name:** `junit5_bdd_test_class`

**Context:** Complete test class creation

```java
package ${package};

import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.CsvSource;
import org.junit.jupiter.params.provider.ValueSource;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertNotNull;

class ${testClassName} {
	// Test methods will be here
}
```

### 4. 🔢 Identity Test Snippet

**Template Name:** `junit5_bdd_identity_test`

**Context:** Mathematical property tests

```java
@Test
@DisplayName("Should return same number when summing with zero")
void shouldReturnSameNumberWhenSummingWithZero() {
	// Given
	final double number = 5.0;
	final double zero = 0.0;

	// When
	final Double actualResult = SimpleMath.sum(number, zero);

	// Then
	assertEquals(number, actualResult, 0.001,
		() -> String.format("%.2f + 0 should equal %.2f", number, number));
}
```

### 5. 🎯 AssertAll Snippet

**Template Name:** `junit5_bdd_assert_all`

**Context:** Multiple validations in one test

```java
@Test
@DisplayName("Should perform multiple assertions correctly")
void shouldPerformMultipleAssertions() {
	// Given
	final double a = 5.0;
	final double b = 3.0;
	
	// When
	final Double result = SimpleMath.sum(a, b);
	
	// Then
	assertAll(
		() -> assertNotNull(result, "Result should not be null"),
		() -> assertEquals(8.0, result, 0.001, "Sum should be correct"),
		() -> assertEquals(Double.class, result.getClass(), "Should return Double type")
	);
}
```

### 6. 📝 Standard Imports Snippet

**Template Name:** `junit5_standard_imports`

**Context:** Common imports for JUnit 5 tests

```java
import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertNotNull;
import static org.junit.jupiter.api.Assertions.assertAll;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.CsvSource;
import org.junit.jupiter.params.provider.ValueSource;
```

## 📋 Eclipse Setup Guide

### Method 1: Code Templates
1. Go to **Window → Preferences → Java → Editor → Templates**
2. Click **"New"**
3. Fill in:
   - **Name:** Snippet name (e.g., `junit5_bdd_basic_test`)
   - **Description:** Usage context description
   - **Pattern:** Paste the snippet code

### Method 2: Live Templates
1. Install the **"Live Templates"** plugin in Eclipse
2. Import snippets through the plugin

### Method 3: Quick Fix
Use **Ctrl+1** to automatically import classes during coding.

## 🏷️ Naming Conventions

### BDD Pattern for Methods:

```java
should[Behavior]When[Condition]
// Examples:
shouldSumTwoPositiveNumbersCorrectly
shouldReturnZeroWhenSummingZeroWithZero
shouldHandleNegativeNumbersInSum
```

### Context Pattern for Methods:

```java
[Context]_[Behavior]
// Examples:
sumOperation_withPositiveNumbers_returnsCorrectResult
sumOperation_withZeroValues_returnsZero
```

### DisplayName Suggestions:

```java
// Successful operations
@DisplayName("✅ Should correctly sum two decimal numbers")
@DisplayName("🧮 Should handle addition of positive numbers")

// Edge cases
@DisplayName("🔄 Should maintain identity property with zero")
@DisplayName("⚠️ Should handle negative number addition")

// Specific validations
@DisplayName("📊 Should validate sum with various data sets")
@DisplayName("🎯 Should return precise decimal results")
```

## 🎯 Recommended BDD Structure

### 1. **Given** (Arrange)
- Test scenario preparation
- Variable and dependency setup
- Initial value definition

### 2. **When** (Act)
- Execution of the method under test
- Main functionality call
- Result capture

### 3. **Then** (Assert)
- Result validation
- Descriptive assertion messages
- Expected behavior verification

## 📊 Complete Usage Example

```java
import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertNotNull;

import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.CsvSource;

class SimpleMathTest {

	@Test
	@DisplayName("✅ Should sum two positive decimal numbers correctly")
	void shouldSumTwoPositiveDecimalNumbers() {
		// Given
		final double firstNumber = 6.2;
		final double secondNumber = 2.0;
		final double expectedResult = 8.2;

		// When
		final Double actualResult = SimpleMath.sum(firstNumber, secondNumber);

		// Then
		assertNotNull(actualResult, "Result should not be null");
		assertEquals(expectedResult, actualResult, 0.001, 
			() -> String.format("Expected %.2f + %.2f = %.2f", 
				firstNumber, secondNumber, expectedResult));
	}

	@ParameterizedTest
	@DisplayName("📊 Should sum various number combinations correctly")
	@CsvSource({
		"6.2, 2.0, 8.2",
		"0.0, 0.0, 0.0",
		"-5.0, 3.0, -2.0"
	})
	void shouldSumVariousNumberCombinations(double firstNumber, 
										   double secondNumber, 
										   double expectedResult) {
		// When
		final Double actualResult = SimpleMath.sum(firstNumber, secondNumber);

		// Then
		assertEquals(expectedResult, actualResult, 0.001,
			() -> String.format("%.2f + %.2f should equal %.2f", 
				firstNumber, secondNumber, expectedResult));
	}
}
```

## 🔧 Implemented Best Practices

- ✅ **JUnit 5 Best Practices**: Parameterized tests, static imports, descriptive messages
- ✅ **Clean Code**: Meaningful names, final variables, proper formatting
- ✅ **BDD**: Given-When-Then structure, behavior-focused testing
- ✅ **Error Handling**: Descriptive error messages with lambda expressions
- ✅ **Decimal Precision**: Delta parameter for floating-point comparisons
- ✅ **Null Safety**: Validation of non-null results

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🤝 Contribution

Contributions are welcome! Please:

1. Fork the project
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

---

**⭐ If this project was helpful, please leave a star on GitHub!**