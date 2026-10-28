[Polski](README.md) · **English**

---

# Computer Science Matura, extended level - Python course, part 6. "Functions"

> ### 🎬 Video lesson
> You can find a full step-by-step walkthrough of this lesson on my YouTube channel:
> **[Watch the video on YouTube](https://youtu.be/uw6NC9ycLPE)**
>
> In the video I write functions that calculate the area and perimeter of a rectangle. I show parameters and arguments, default values, type hints, the `return` statement, returning several values in a tuple and a program template with a `main` function.

---

## Description

Code for the sixth part of a Python course that prepares students for the Computer Science Matura exam at the extended level. This part is about writing your own functions.

A function is a named piece of code. You write it once and call it as many times as you need instead of copying the same code. In this lesson I show how to pass data to a function, how to return the result the function calculates, and how to build a program template with a `main` function. We use this template in the rest of the course.

Functions make the code you write during the exam shorter and more readable. Under exam stress it is easier to find your way around it than around one long script with no functions.

The repository also contains files from the previous parts of the course, from `app-1` to `app-5`.

## Requirements

- Python 3.10 or newer. The `app-6-funkcje.py` file on its own works from version 3.9, but `app-4-instrukcje-warunkowe.py` uses the `match` statement, which is available from Python 3.10
- No external dependencies. Files from the previous parts of the course use only the `random` and `math` modules from the standard library

## Running

```bash
git clone https://github.com/kmprograms/matura-kurs-python-6-funkcje
cd matura-kurs-python-6-funkcje
python app-6-funkcje.py
```

The program does not wait for keyboard input, because the calls to `input` are commented out. In the video I run the script with the green arrow in PyCharm. Under the hood it executes the same `python` command with the file name.

You run the files from the previous parts of the course the same way, e.g. `python app-5-petle.py`.

## Project structure

| File | Description |
| --- | --- |
| `app-1-pierwszy-program-zmienne.py` | First program, variables of different types, f-strings with formatting, arithmetic operators, swapping variable values, the `end` and `sep` parameters of `print`, type conversion, the `+=`, `-=` and `*=` operators |
| `app-2-liczby-calkowite.py` | Integer arithmetic, including `//` and `%`, parity and divisibility, relational operators, the `and` and `or` connectives, extracting the digits of a number, converting seconds into hours, minutes and seconds |
| `app-3-pozyskiwanie-danych-systemy-liczbowe-float.py` | Reading data with `input`, random numbers with the `random` module, number systems, bitwise operations, the `math` module |
| `app-4-instrukcje-warunkowe.py` | Logical operators, short-circuit evaluation, `if`, `elif` and `else` statements, the conditional expression, the `match` statement, the `min`, `max` and `abs` functions |
| `app-5-petle.py` | The `while` loop, the `break` and `continue` statements, the `for` loop with `range`, iterating over a list and a string, nested loops |
| `app-6-funkcje.py` | Code from this lesson: custom functions, parameters and arguments, default values, type hints, `return`, returning a tuple, the `main` function and the `if __name__ == '__main__':` section |

## Lesson scope and code walkthrough

All snippets in this section come from the `app-6-funkcje.py` file.

### Defining and calling a function

```python
def pole_prostokata_v1() -> None:
    a = int(input("Podaj pierwszy bok prostokąta: "))
    b = int(input("Podaj drugi bok prostokąta: "))
    pole = a * b
    print(f"Pole prostokąta o bokach {a} oraz {b} wynosi {pole}")

# pole_prostokata_v1()  # Tak wywołasz funkcję pole_prostokata_v1
# pole_prostokata_v1()
```

You define a function with the `def` keyword. After it you write the function name, parentheses and a colon. The function body is indented with four spaces, just like with `if` or `while`.

The definition alone does not run anything. The code in the function body runs only when you call it with `pole_prostokata_v1()`. Each call runs the same code again, so you do not have to copy it to different places in your program. In the file both calls are commented out so that the program does not wait for keyboard input.

A function name should clearly say what its code does. A program usually consists of several functions, so readable names help you quickly find the one you need.

The weakness of this version is the lack of flexibility. The function always reads the side lengths from the user, so you cannot generate them randomly or hard-code them.

### Parameters, arguments and type hints

```python
# a oraz b to parametry
# type hints
def pole_prostokata_v2(a: int = 1, b: int = 2) -> None:
    pole = a * b
    print(f"Pole prostokąta o bokach {a} oraz {b} wynosi {pole}")


# Kiedy wywołujesz funkcję i podstawiasz konkretne dane, wtedy mówimy,
# że podajesz argumenty
pole_prostokata_v2(10, 20)

# x = int(input("Podaj pierwszy bok prostokąta: "))
# y = int(input("Podaj drugi bok prostokąta: "))
# pole_prostokata_v2(x, y)
pole_prostokata_v2(b=11, a=22)
pole_prostokata_v2()
pole_prostokata_v2(11)
pole_prostokata_v2(b=11)
```

`a` and `b` in the function header are parameters. The concrete values you pass in a call are arguments. Many people use these words interchangeably, but it is worth knowing the difference.

Parameter names only tell you how to refer to the data inside the function body. When calling the function you can pass variables with any names, e.g. `x` and `y` read with `input`. The data can also come from a random generator or from a text file. The function stays the same, only the way the data is supplied changes.

The `a: int` notation is a type hint, an explicit declaration of the parameter type. Python does not require it and the program works without it. Still, treat it as mandatory. During the exam it is a quick reminder of what data your function takes, especially when stress makes you lose track. The `-> None` notation after the parentheses means that the function returns nothing.

### Default values, positional and keyword arguments

Positional arguments are assigned to parameters from left to right. A keyword argument, e.g. `b=11`, names the parameter directly, so the order no longer matters. The default values `a: int = 1` and `b: int = 2` let you skip arguments in a call.

| Call | `a` | `b` | Area | Notes |
| --- | --- | --- | --- | --- |
| `pole_prostokata_v2(10, 20)` | 10 | 20 | 200 | Positional arguments |
| `pole_prostokata_v2(b=11, a=22)` | 22 | 11 | 242 | Keyword arguments, order does not matter |
| `pole_prostokata_v2()` | 1 | 2 | 2 | Both default values |
| `pole_prostokata_v2(11)` | 11 | 2 | 22 | The only argument goes to `a`, `b` keeps its default value |
| `pole_prostokata_v2(b=11)` | 1 | 11 | 11 | `a` keeps its default value |

### Returning a result with return

```python
def pole_prostokata_v3(a: int = 1, b: int = 2) -> int:
    pole = a * b
    print(f"Pole prostokąta o bokach {a} oraz {b} wynosi {pole}")
    return pole

p = pole_prostokata_v3(10, 30)
if p > 100:
    print("Pole jest duże")
```

Printing a message with `print` does not mean you can use the value calculated inside the function after it finishes. That is what the `return` keyword is for. After it you write what the function should return. The value from `return`, here 300, appears where the function was called and is stored in the variable `p`. You describe the type of the returned value in the header after the arrow, here `-> int`.

`print` inside a function is not mandatory and does not conflict with `return`. It is used to inspect variable values or to inform the user about results. Parameters handle the input data and `return` handles the result. Functions can communicate this way: the result of one function becomes an argument of the next one, and you build your program from functions like building blocks.

A function without `return` returns `None` by default. If you assigned the result of `pole_prostokata_v2` to `p` and compared it with 100, the program would raise an error, because `NoneType` cannot be compared with `int`. That is why the headers of `pole_prostokata_v1` and `pole_prostokata_v2` contain `-> None`.

### Invalid input data

```python
def pole_prostokata_v4(a: int = 1, b: int = 2) -> int:  # -> int | None:

    # W przypadku nieprawidłowych długości boków zwracamy specyficzną wartość
    # if a <= 0 or b <= 0:
    #     print(f"Podałeś złe długości boków {a=}, {b=}")
    #     # return None
    #     return -1

    # if a <= 0 or b <= 0:
    #     raise ValueError(f"Podałeś złe długości boków {a=}, {b=}")

    pole = a * b
    print(f"Pole prostokąta o bokach {a} oraz {b} wynosi {pole}")
    return pole


print(f"Pole prostokąta: {pole_prostokata_v4(10, -20)}")
print("Koniec")
```

The sides of a rectangle must be positive, but someone may pass e.g. `-20`. The function shows three ways to react to such data:

1. Returning the special value `-1`. The area of a rectangle cannot be negative, so `-1` clearly means that something went wrong. You can assign the result to a variable and check it with an `if` statement.
2. Returning `None`. This stresses the lack of a valid result even more and is useful when any number could be a valid result of the function. The return type must then be written as `int | None`. However, type checking tools may force you to check the result every time you use the function.
3. Raising an exception with `raise ValueError(...)`. The program displays the error type, the message and the location of the error in red, and then stops. The `print("Koniec")` statement is no longer executed. In practice, raising and catching exceptions is the recommended approach in situations like this. I do not cover exception handling at this stage of exam preparation.

`return` not only returns a value but also ends the function immediately. In the `-1` variant, once invalid sides are detected, the code below the `if` is not executed. Thanks to this, you can check the conditions that end the function early at the beginning of its body, and only then move on to the main calculations. I mentioned this when discussing `break` and `continue` in loops.

In the repository both validation variants are commented out, so the call with `-20` returns `-200`. To test a chosen variant, uncomment the relevant fragment.

During the exam you usually do not have to do this. The task description always states the assumptions, e.g. that you work with positive numbers, and the algorithm is designed for them. Still, validating arguments is an important topic when talking about functions, which is why I show it.

### Returning multiple values in a tuple

```python
def min_max_srednia(a: int, b: int, c: int) -> tuple[int, int, float]:
    najmniejsza = min(a, b, c)
    najwieksza = max(a, b, c)
    srednia = (a + b + c) / 3
    # return min(a, b, c), max(a, b, c), (a + b + c) / 3
    return najmniejsza, najwieksza, srednia

wynik = min_max_srednia(10, 20, 30)
print(wynik)
print(wynik[0])
print(wynik[1])
print(wynik[2])

najm, najw, sr = min_max_srednia(20, 30, 40)
print(najm, najw, sr)

_, najw_2, _ = min_max_srednia(20, 30, 40)
print(najw_2)
```

For three numbers, the function finds the smallest value, the largest value and the average. Values after `return` separated by commas form a tuple. In type hints you use the name `tuple` and list the types of the consecutive elements in square brackets: `tuple[int, int, float]`.

You can use the result in three ways:

1. Assign the whole tuple to one variable and access its elements by position, just like in lists. The first element has position 0.
2. Unpack the tuple into separate variables. Their names, e.g. `najm`, `najw` and `sr`, do not have to match the names used inside the function.
3. Replace the elements you do not need with `_`. The left-hand side must have as many positions as the tuple has elements.

The commented-out line shows that you can put expressions directly after `return`, without helper variables.

### Program template with a main function

```python
def obwod_prostokata(a: int, b: int) -> int:
    return 2 * (a + b)

def main() -> None:
    print("--")
    print(obwod_prostokata(10, 20))

if __name__ == '__main__':
    main()
```

Python lets you interleave function definitions with their calls. In an exam task where you need to read data from a file, write several functions implementing an algorithm and solve consecutive subtasks, such a structure quickly turns into a mess. That is why we use a fixed layout:

1. At the top, the definitions of all functions, one below another.
2. Below them, the `main` function, which contains all the calls and the program logic.
3. At the end, the startup section `if __name__ == '__main__':`, which calls `main`.

Some languages, e.g. C++, require a main function. Python does not, but we use it for order and to follow good practices.

When you run a script with the `python` command, the special variable `__name__` (read as "dunder name", from double underscore) gets the value `"__main__"`. The condition checks whether this script was the one that was run, and if so, it calls the `main` function. The name `main` is not required, but it is what everyone uses and I encourage you to use it too.

## Output

Running the `app-6-funkcje.py` file prints:

```
Pole prostokąta o bokach 10 oraz 20 wynosi 200
Pole prostokąta o bokach 22 oraz 11 wynosi 242
Pole prostokąta o bokach 1 oraz 2 wynosi 2
Pole prostokąta o bokach 11 oraz 2 wynosi 22
Pole prostokąta o bokach 1 oraz 11 wynosi 11
Pole prostokąta o bokach 10 oraz 30 wynosi 300
Pole jest duże
Pole prostokąta o bokach 10 oraz -20 wynosi -200
Pole prostokąta: -200
Koniec
(10, 30, 20.0)
10
30
20.0
20 40 30.0
40
--
60
```

The line with the area `-200` appears because the side validation in `pole_prostokata_v4` is commented out. The tuple returned by `min_max_srednia` is printed in parentheses, with its elements separated by commas.

## Implementation notes

Python does not require type hints. In professional projects, code goes through tools that check its quality and correctness before deployment, and there type hints are practically mandatory. In this course we use them to describe the parameter types and the return type of every function.

The `tuple[int, int, float]` notation in a function header works from Python 3.9. The commented-out `int | None` notation requires Python 3.10.

When you call a function, PyCharm shows which parameter each positional argument goes to. It also warns you when you assign the result of a function that returns nothing. The `-> None` and `-> int` annotations make the work of such tools easier.

You can put a whole expression after `return`, as in `obwod_prostokata`. The version with separate variables, as in `min_max_srednia`, is sometimes more readable.

In the next lessons, functions will also return whole lists and possibly dictionaries. The next video is about lists.