# Lecture 1 — C

## C basics

The Scratch ideas carry over to C; only the syntax changes. Judge code by **correctness, design and style**.

**Compiling**

- Source code (human-readable) → compiler → machine code (binary the CPU runs).
- `make hello` compiles `hello.c`; `./hello` runs it.

```c
#include <stdio.h>

int main(void)
{
    printf("hello, world\n");
}
```

- `#include` pulls in a header file (a library's function list). `stdio.h` gives `printf`; `cs50.h` gives `get_string`, `get_int`, etc.
- `\n` = newline. Every statement ends with `;`.

**Variables and types**

- `string answer = get_string("What's your name? ");` then `printf("hello, %s\n", answer);`
- Types: `int`, `long`, `float`, `double`, `char`, `bool`, `string`.
- Format codes: `%i` int, `%li` long, `%f` float/double, `%c` char, `%s` string.
- `=` assigns (right to left). `counter++` adds 1.

**Conditionals** — `if`, `else if`, `else`. Compare with `==`, `!=`, `<`, `>`, `<=`, `>=`; combine with `&&` (and), `||` (or).

**Loops**

```c
for (int i = 0; i < 3; i++)
{
    printf("meow\n");
}
```

- `while (condition) { … }` — repeats while true.
- `do { … } while (condition);` — runs at least once; good for re-prompting input (e.g. until n > 0).
- `while (true)` loops forever unless you `break`.

**Functions**

- Define your own to avoid repetition: `void meow(int n)` takes an input and returns nothing; `int get_size(void)` returns a value.
- Declare a prototype above `main` so the compiler knows the function exists before it is used.
- Scope: a variable only exists inside the `{ }` where it was declared.

**Mario example** — nested loops print a grid: outer loop = rows, inner loop = columns.

**Command line (Linux)** — `ls` list, `cd` change folder, `mkdir` make folder, `mv` move/rename, `cp` copy, `rm` remove, `rmdir` remove folder, `clear` clear screen.

## Gotchas

Computers have finite memory, so numbers have limits. These three bugs come from that.

| Problem | What happens | Fix |
| --- | --- | --- |
| Integer overflow | An `int` is 32 bits (max about 2.1 billion). Go past it and it wraps to a negative number. | Use `long` (64 bits) for big values. |
| Truncation | `int / int` gives an `int`, so `1 / 3` = 0 — the decimal part is thrown away. | Cast first: `(float) x / y`. |
| Floating-point imprecision | `1.0 / 3` printed to 20 places shows garbage digits; decimals can't all be stored exactly in finite bits. | Use `double` for more precision; never compare floats with `==`. |

Real-world examples from lecture: the Y2K bug (years stored as 2 digits) and the 2038 problem (32-bit Unix time overflows on 19 Jan 2038).
