# Lecture 2 — Arrays

## Compiling

"Compiling" is really four steps, and `make` hides all of them. Under the hood, `make hello` runs `clang`, the actual compiler, with the right options for you:

```bash
clang -o hello hello.c -lcs50
```

- `-o hello` names the output file, and `-lcs50` links in the CS50 library so `get_string` works.

1. **Preprocessing**: every `#include` line is replaced with the contents of that header file, so the compiler knows the prototypes of functions like `printf` and `get_string`.
2. **Compiling**: your C code is translated into assembly language, low-level instructions specific to the CPU.
3. **Assembling**: the assembly is turned into machine code, the actual 0s and 1s.
4. **Linking**: your machine code is combined with the machine code of the libraries you used (like `cs50.c` and `stdio`) into one runnable file.

Because machine code can be read back, a compiled program isn't truly secret. Reverse engineering it is possible, just painful.

## Debugging

A bug is code that doesn't do what you intended. The lecture gives three tools, from simplest to most powerful.

- **`printf`**: print the values of variables at key points to see what the program is actually doing.
- **`debug50`**: set a breakpoint by clicking left of a line number, then run `debug50 ./program`. Execution pauses there, and you can watch variables change as you **step over** (run the next line) or **step into** (go inside a function call).
- **Rubber duck debugging**: explain your code, line by line, out loud to an object. Saying it forces you to notice where your belief and the code disagree.

A classic bug from lecture is the **off-by-one** error, like `for (int i = 0; i <= 3; i++)` running four times instead of three.

## Types and memory

Every type takes a fixed number of bytes in memory, which is why C makes you declare types.

| Type | Size (bytes) |
| --- | --- |
| `bool` | 1 |
| `char` | 1 |
| `int` | 4 |
| `float` | 4 |
| `long` | 8 |
| `double` | 8 |
| `string` | varies (one byte per character, plus one) |

Think of memory (RAM) as a long grid of bytes, each with its own address. Declaring `int x = 50;` reserves 4 neighbouring bytes somewhere in that grid. Variables declared one after another may end up next to each other, but nothing guarantees it, and that's exactly the problem arrays solve.

## Arrays

An array is a sequence of values of the same type, stored back to back in memory and accessed by index starting at 0.

The lecture's example starts with three separate variables, `score1`, `score2`, `score3`, which doesn't scale. An array replaces them:

```c
int scores[3];      // room for 3 ints, 12 bytes in a row
scores[0] = 72;
scores[1] = 73;
scores[2] = 33;     // the last index is size - 1
```

Pair arrays with loops, and use a constant for the size so it lives in one place:

```c
const int N = 3;
int scores[N];
for (int i = 0; i < N; i++)
{
    scores[i] = get_int("Score: ");
}
```

**Passing an array to a function**: C arrays don't know their own length, so you pass the length along with the array.

```c
float average(int length, int array[])
{
    int sum = 0;
    for (int i = 0; i < length; i++)
    {
        sum += array[i];
    }
    return sum / (float) length;   // cast, or integer division drops the decimals
}
```

C doesn't stop you from reading `scores[3]` or `scores[-1]`. Going past the end touches memory you don't own, and the result is unpredictable.

## Strings

A `string` is just an array of `char`s that ends with a special byte, `'\0'` (called NUL), which marks where the string stops.

`string s = "HI!";` takes 4 bytes, not 3:

| `s[0]` | `s[1]` | `s[2]` | `s[3]` |
| --- | --- | --- | --- |
| `'H'` (72) | `'I'` (73) | `'!'` (33) | `'\0'` (0) |

**Characters are numbers.** Each `char` is stored as its ASCII code, so `printf("%i", s[0])` prints 72, and you can do arithmetic on letters. Lowercase and uppercase letters are exactly 32 apart (`'a'` is 97, `'A'` is 65).

**`strlen` counts characters until it hits `'\0'`.** You could write it yourself:

```c
int n = 0;
while (s[n] != '\0')
{
    n++;
}
```

Since `strlen` walks the whole string each time, call it once instead of in every loop check:

```c
for (int i = 0, n = strlen(s); i < n; i++)
```

**Useful libraries:**

- `<string.h>`: `strlen`
- `<ctype.h>`: `isalpha`, `isdigit`, `isupper`, `islower`, `toupper`, `tolower`

**Arrays of strings** work too: with `string words[2]`, `words[0]` is a whole string and `words[0][0]` is its first character.

## Command-line arguments and exit status

`main` can take input straight from the command line instead of prompting for it:

```c
int main(int argc, string argv[])
```

- `argc` (argument count) is how many words were typed, **including the program name**.
- `argv` (argument vector) is an array of those words as strings.

For `./caesar 13`, `argc` is 2, `argv[0]` is `"./caesar"`, and `argv[1]` is `"13"`. Note that `"13"` is a string; convert it with `atoi` from `<stdlib.h>` to get the number 13.

Always check `argc` before touching `argv[1]`. If the user typed nothing, `argv[1]` doesn't exist.

**Exit status**: `main` returns an `int` to the operating system. By convention, `return 0;` means success and any other number (like `return 1;`) means something went wrong. Run `echo $?` right after a program to see the status it returned; check50 uses this to test your error handling.

## Cryptography

Cryptography scrambles a message so only someone with the key can read it: **plaintext** + **key** go into a **cipher**, which produces **ciphertext**. Decryption runs the cipher in reverse. The Caesar cipher shifts every letter by the key; with key 1, `HI!` becomes `IJ!`, and shifting back by 1 recovers it.
