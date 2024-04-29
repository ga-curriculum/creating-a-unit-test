# ![[tktk Module Name] - tktk Microlesson Name](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to apply Test-Driven Development techniques to iteratively develop a string calulator that handles various inputs and requirments while passing specific unit tests.

#### Requirement 5: Allow the Add method to handle new lines between numbers (instead of commas).

```java 
    @Test
    @DisplayName("When new line is used between numbers then return values is their sum")
    public final void whenNewLineIsUsedBetweenNumbersThenReturnValuesIsTheirSums(){
        Assert.assertEquals(3+6+15,Calculator.add("3,6n15"));
    }
```

```java
public class Calculator {
    public static int add(final String numbers) {
        int returnValue = 0;
        String[] numbersArray = numbers.split(",|n"); // added |n to the split regex
        for (String number : numbersArray) {
            if (!number.trim().isEmpty()) {
                returnValue += Integer.parseInt(number.trim());
            }
        }
        return returnValue;
    }
}
```

All we had to do to was to extend the split regex by adding `|\n`.