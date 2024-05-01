# ![req 2](./assets/req-two.png)

**Learning objective:** By the end of this lesson, students will be able to apply Test-Driven Development techniques to iteratively develop a string calulator that handles various inputs and requirments while passing specific unit tests.

#### Requirement 2: For an empty string the method will return 0

```java 
  @Test
  @DisplayName("When empty String is used then return value is 0")
  public final void whenEmptyStringIsUsedThenReturnValueIs0(){
        Assert.assertEquals(0,Calculator.add(""));
  }
```

```java
package com.example.demo;

public class Calculator {
    public static int add(final String numbers) {
        String[] numbersArray = numbers.split(",");
        if (numbersArray.length > 2) {
            throw new RuntimeException("Up to 2 numbers separated by comma (,) are allowed");
        } else {
            for (String number : numbersArray) {
                if (!number.isEmpty()) {
                    Integer.parseInt(number);
                }
            }
        }
        return 0; // Added return
    }
}

```

All there was to do to make this test pass was to change the return method from void to int and end it with returning
zero.