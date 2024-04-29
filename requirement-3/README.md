# ![[tktk Module Name] - tktk Microlesson Name](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to apply Test-Driven Development techniques to iteratively develop a string calulator that handles various inputs and requirments while passing specific unit tests.

#### Requirement 3: Method will return their sum of numbers

```java 
  @Test
  @DisplayName("When one number is used then return value is that same number")
  public final void whenOneNumberIsUsedThenReturnValueIsThatSameNumber(){
        Assert.assertEquals(3,Calculator.add("3"));
  }

  @Test
  @DisplayName("When two numbers are used then return value is their sum")
  public final void whenTwoNumbersAreUsedThenReturnValueIsTheirSum(){
        Assert.assertEquals(3+6,Calculator.add("3,6"));
  }
```

```java
package com.example.demo;

public class Calculator {
    public static int add(final String numbers) {
        int returnValue = 0;
        String[] numbersArray = numbers.split(",");
        if (numbersArray.length > 2) {
            throw new RuntimeException("Up to 2 numbers separated by comma (,) are allowed");
        }
        for (String number : numbersArray) {
            if (!number.trim().isEmpty()) { // after refactoring
                returnValue += Integer.parseInt(number);
            }
        }
        return returnValue;
    }
}
```

Here we added iteration through all numbers to create a sum.