# Python Testing

This lesson is an shortened adaptaion of [MolSSI's Testing Lesson](https://education.molssi.org/python-package-best-practices/08-testing.html).

Until now, we have been writing functions and checking their behavior using an interactive Python interpreter and manually inspecting the output.
While this seems to work, it can be tedious, and prone to error.
In this lesson, we'll discuss how to write tests and run them using the `pytest` testing framework.

Using a testing framework will allow us to easily define tests for all of our functions and modules, and to test these each time we make a change.
This will ensure that our code is behaving the way we expect, and that we do not break any features existing in the code by making new changes.

## Why testing

Software should be tested regularly throughout the development cycle to ensure correct operation.
Thorough testing is typically an afterthought, but for larger projects, it is essential for ensuring changes in some parts of the code do not negatively affect other parts.

**Software testing is checking the behavior of part of the code (such as a method, class, or a module) by comparing its expected output or behavior with the observed one.**
We will explain this in more detail shortly.

## Levels of Testing

There are three main levels of testing:

- **Unit tests**:
The purpose is to verify that each part of the code is functioning as expected.
Unit testing is done on smaller units (such as single functions or classes) as you work on your code.
This is helpful for catching errors in uncommonly-used parts of the code.
Unit tests should be added as new features are added, resulting in better code coverage.
In unit tests, you are testing a part of your code independent of any other factors;
therefore, you should avoid using the file system, databases, network, or any other resources unless you are testing a function directly related to that resource.

- **Integration tests**:
This is a more holistic approach where you test the interface between modules, and how they combine and integrate together.

- **System tests**:
Where you test your system as a whole to check if it meets all the requirements.

Another important type of testing is **Regression tests**.
In Regression tests, given a known input, does the software correctly and consistently return the correct values.
This kind of testing can catch problems in previously working code that may have been broken by new changes or new features.

It is highly encouraged to have Unit tests that *cover* most of your code.
It is also helpful to have some Integration and System tests.

In this lesson, we are focusing on unit testing.

## The pytest testing framework

We recommend using the [pytest](https://pytest.org) testing framework.
Other testing frameworks are available (such as unittest and nose tests);
however, the combination of easy implementation, [parametrization of tests](https://docs.pytest.org/en/latest/parametrize.html),
[fixtures](https://docs.pytest.org/en/latest/fixture.html), and [test marking](https://docs.pytest.org/en/latest/example/markers.html)
make `pytest` an ideal testing framework.

## How to Run Tests

When we run `pytest`, it will look for directories and files which start with `test` or `test_`.
It then looks inside those files and executes any functions that begin with the word `test_`.
This syntax lets pytest know that these functions are tests.
If these functions do not result in an error, `pytest` counts the function as passing.
If an error occurs, the test fails.

## Exercises

To complete the exercises, you should write code into a file called `test_monte_carlo.py` and and write answers to the questions in a README.md (you will need to create both of these files.)

1. **Running our First Test** - Create a file called `test_monte_carlo.py`. Add the following to your file.
   
```python
from monte_carlo import calculate_LJ, calculate_distance
```
Next, define a test function for the `calculate_LJ` function.

```python
def test_calculate_LJ():
    assert calculate_LJ(1) == 0
```

Run your test from the terminal using

```bash
pytest -v
```

If all goes well, you will see an indication that your tests passed.

**Question** - What was the output of the `pytest -v` command? What happens if you remove `-v`? What does `-v` mean (you may have to refer to pytest documentation to figure this out.)

2. **A failing test** - Change your expected value to `1`. **Question** -  What happens when you run your test?

3. **Investigating Failure** - Remove the `assert` statement. **Question** - What happens when you remove the `assert` statement and run your test? Why do you think this happens?

4. **Another way to test a value** - Using your answer to problem 3, write another test which uses an alternate way of making a test fail if the expected value is not calculated. Hint: You will use a skill you learned during Chem 274A week 1. **Question** What different approach did you use in your test. Why did you choose this?

5. Write at least two more test cases for your `calculate_LJ` function. **Question** - What test cases did you write and how did you choose them?

6. Add the following test for your `calculate_distance_function`

```python
def test_calculate_distance():
    coordA = [0, 0, 0]
    coordB = [1, 0, 0]

    expected_value = 1

    assert calculate_distance(coordA, coordB) == 1
```

**Question** - Is this a good test, why or why not?

7. Write at least four more test cases for your calculate distance function. Make sure to test the case where you have a box length and where you don't. Also make sure you are testing variation in all dimensions: x, y, and z. **Question** - What test cases did you write and how did you choose them? Did your function behave as expected? If not, investigate why. How did testing help you evaluate this?