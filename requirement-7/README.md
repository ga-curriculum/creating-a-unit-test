# ![[tktk Module Name] - tktk Microlesson Name](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to apply Test-Driven Development techniques to iteratively develop a string calulator that handles various inputs and requirments while passing specific unit tests.

#### Requirement 7: Negative numbers will throw an exception

Calling Add with a negative number will throw an exception **negatives not allowed** – and the negative that was passed.
If there are multiple negatives, show all of them in the exception message.

```java 
    @Test(expected = RuntimeException.class)
    @DisplayName("When negative number is used then runtime exception is thrown")
    public final void whenNegativeNumberIsUsedThenRuntimeExceptionIsThrown() {
        Calculator.add("3,-6,15,18,46,33");
    }

    @Test
    @DisplayName("When negative numbers is used then runtime exception is thrown")
    public final void whenNegativeNumbersAreUsedThenRuntimeExceptionIsThrown() {
        RuntimeException exception = null;
        try {
            Calculator.add("3,-6,15,-18,46,33");
        } catch (RuntimeException e) {
            exception = e;
        }
        Assert.assertNotNull(exception);
        Assert.assertEquals("Negatives not allowed: [-6, -18]", exception.getMessage());
    }
```

There are two new tests. First one checks whether exception is thrown when there are negative numbers. The second one
verifies whether the exception message is correct.

```java 
      private static int add(final String numbers, final String delimiter) {
          int returnValue = 0;
          String[] numbersArray = numbers.split(delimiter);
          List<Integer> negativeNumbers = new ArrayList<Integer>();
          for (String number : numbersArray) {
              if (!number.trim().isEmpty()) {
                  int numberInt = Integer.parseInt(number.trim());
                  if (numberInt < 0) {
                      negativeNumbers.add(numberInt);
                  }
                  returnValue += numberInt;
              }
          }
          if (negativeNumbers.size() > 0) {
              throw new RuntimeException("Negatives not allowed: " + negativeNumbers.toString());
          }
          return returnValue;
      }
```

This time code was added that collects negative numbers in a List and throws an exception if there was any.

**Note** :- In order to `whenNewLineIsUsedBetweenNumbersThenReturnValuesIsTheirSums`
and `whenDelimiterIsSpecifiedThenItIsUsedToSeparateNumbers` pass you need to modify the assert statements like so :

```java 
    @Test
    @DisplayName("When new line is used between numbers then return values is their sum")
    public final void whenNewLineIsUsedBetweenNumbersThenReturnValuesIsTheirSums() {
        Assert.assertEquals(3 + 6 + 15, Calculator.add("3,6\n15"));
    }

    @Test
    @DisplayName("When delimiter is specified then it is used to separate numbers")
    public final void whenDelimiterIsSpecifiedThenItIsUsedToSeparateNumbers() {
        Assert.assertEquals(3 + 6 + 15, Calculator.add("//;\n3;6;15"));
    }
```