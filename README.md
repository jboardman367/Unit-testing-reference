# Unit Testing

## What is unit testing?

Unit testing is the practice of testing individual functions and methods
in a code base against prepared inputs and expected outputs. These inputs
are chosen in such a way that maximises coverage of distinct input cases.

## Why do we need unit testing?

Unit testing is used because it allows for individual components within
a piece of software to be tested without requiring the rest of the program
to be running or even correct. Often unit testing is used as part of CI
(Continuous Integration) to catch regressions before they are merged into
a codebase.

## Structuring unit tests

Each unit test should test only one case (some frameworks will have special
ways to consolidate cases into only one piece of code), and will typically
be named using both the function/method being tested and the case, e.g. 
`TestMultiply_BothNegativeIsPositive`.

A good way to structure the code of a unit test is to have a distinct
divide between setup, the operation being tested, and validating the results.
Below is an example in no particular language.
```
function TestMultiply_BothNegativeIsPositive() {
    // Setup
    myMultiplier = new Multiplier()
    myMultiplier.firstNumber = -2
    myMultiplier.secondNumber = -3
    
    // Test
    result = myMultiplier.multiply()

    // Validate
    assert result > 0
}
```

## Common unit testing cases

### Boolean input

Boolean inputs are simple to maximise coverage of, a case for `true` and
a case for `false` are sufficient.

### Numeric input

To test a numeric input, the first step is to identify if there is any limitations
on the range of the value (other than those imposed by the language). Consider
the following as test cases where applicable

- For an input valid or invalid between (`a`, `b`) test a value below `a`, `a`,
a value between `a` and `b`, `b`, and a value above `b`
- For an input with only an upper or lower bound `c`, test a value below `c`,
`c`, and a value above `c`
- Test numbers that have any specifically defined behaviour,  These values will
typically be 0, 1, occasionally -1 or 2, as well as any defined special values
such as a sentinel value.\
For example, a `numRepetitions` parameter would need to have `0` tested to ensure
the function has the expected behaviour when no repetitions are done, and `1` tested
to ensure the function has the expected behaviour when only one repetition is done.
- For signed types, test both positive and negative values.
- For non-integer types, test both integers and non integers.

### Array/List input

For operations on arrays or lists, consider the following test cases where
applicable

- Test a "normal" case
- Test an empty array/list
- Test on an array/list with one element
- For operations that reduce an array/list (return a result of lower dimension),
test on inputs up to the number of elements needed to satisfy the operation's
definition for large numbers of elements.\
For example, the "average" operation needs at least 1 element for its `Sum(A) / Count(A)`
definition, so an additional test for input size 1 is required.
- For operations that rearrange an array/list, test on inputs of size 1, 2, 3 and >3
to cover special cases.\
Also test cases where the elements are already sorted, cases where the elements are
equal.\
If using a hierarchical comparison, test all distinct levels of the hierarchy
- For operations that add/remove elements from a list, test cases of adding/removing
while at maximum capacity

## Mocks

## Writing testable code

## Unit testing frameworks

### C#

#### MSTest