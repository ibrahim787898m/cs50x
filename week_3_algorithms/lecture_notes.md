# Lecture 3 — Algorithms

## Searching

An algorithm is a step-by-step way to solve a problem. The lecture's example is a row of closed lockers with numbers behind the doors: find the number 50. A computer can only look behind **one door at a time**, so the question is how few doors you need to open.

**Linear search**: open the doors one by one, left to right, until you find it or run out of doors.

```
For each door from left to right
    If the number is behind the door
        Return true
Return false
```

It works on any list, sorted or not, but in the worst case you open every door.

**Binary search**: if the numbers are **sorted**, open the middle door. If the number you want is smaller, throw away the right half; if bigger, throw away the left half. Repeat on the half that's left.

```
If no doors left
    Return false
If the number is behind the middle door
    Return true
Else if the number < middle door
    Search the left half
Else if the number > middle door
    Search the right half
```

Each step halves the problem, so 1,000 doors take about 10 steps and 1,000,000 take about 20. The catch: the list must already be sorted.

## Running time

We describe how an algorithm's work **grows** as the input size `n` grows, ignoring constants and smaller terms. `n/2` steps and `n` steps both count as "linear", because for huge `n` the shape of the curve matters more than the constant.

| Symbol | Means | Think of it as |
| --- | --- | --- |
| **O** (big O) | upper bound | the worst case |
| **Ω** (omega) | lower bound | the best case |
| **Θ** (theta) | O and Ω are the same | always this, whatever the input |

Common classes, from fastest to slowest:

| Class | Example |
| --- | --- |
| `O(1)` | constant: one step, whatever `n` is |
| `O(log n)` | binary search |
| `O(n)` | linear search |
| `O(n log n)` | merge sort |
| `O(n²)` | selection sort, bubble sort |

| Algorithm | O (worst) | Ω (best) |
| --- | --- | --- |
| Linear search | `O(n)` | `Ω(1)`, found at the first door |
| Binary search | `O(log n)` | `Ω(1)`, found at the middle door |

## Linear search in C

Searching numbers uses `==`. Searching **strings** needs `strcmp` from `<string.h>`, which returns 0 when two strings match:

```c
string names[] = {"Yuliia", "David", "John"};

for (int i = 0; i < 3; i++)
{
    if (strcmp(names[i], "David") == 0)
    {
        printf("Found\n");
        return 0;
    }
}
printf("Not found\n");
return 1;
```

**Why not `names[i] == "David"`?** A string in C is really the address of its first character. `==` compares the two addresses, not the text, so it compiles but gives the wrong answer. This becomes clear in Week 4 (Memory).

The `return 0;` / `return 1;` inside `main` are exit statuses: 0 for success, anything else for failure.

## Structs

Keeping related data in separate arrays (`names[]` and `numbers[]`) works, but nothing ties `names[0]` to `numbers[0]` except your promise to keep them in sync. A **struct** creates your own type that groups them:

```c
typedef struct
{
    string name;
    string number;
} person;

person people[2];
people[0].name = "David";
people[0].number = "+1-617-495-1000";
```

- `typedef struct { ... } person;` defines a new type called `person`.
- The **dot operator** reaches inside: `people[0].name`.
- Phone numbers are stored as strings because they can contain `+`, `-` and leading zeros, and you never do arithmetic on them.

## Sorting

Sorting makes binary search possible, so it's worth the cost if you'll search many times.

### Selection sort

For each position from left to right, **scan** the unsorted part to find the smallest value, then **swap** it into that position once.

```
For i from 0 to n-1
    Find the smallest number between numbers[i] and numbers[n-1]
    Swap the smallest number with numbers[i]
```

- Comparisons: `(n-1) + (n-2) + ... + 1 = n(n-1)/2`, which is `O(n²)`.
- It doesn't notice when the list is already sorted, so it still does every scan: `Ω(n²)`, which makes it **`Θ(n²)`**.
- At most one swap per pass. The comparisons are what make it slow, not the swaps.

### Bubble sort

Walk through the list comparing **neighbouring pairs**, swapping any pair that's out of order. After each pass, the largest remaining value has "bubbled" to the end.

```
Repeat n-1 times
    For i from 0 to n-2
        If numbers[i] and numbers[i+1] out of order
            Swap them
    If no swaps
        Quit
```

- Worst case `O(n²)`.
- The "if no swaps, quit" line is what gives it a good best case: on an already sorted list, one pass of `n-1` comparisons with zero swaps, then stop. That's **`Ω(n)`**.
- Without that check, bubble sort would be `n²` even on sorted input.

| | Swaps per pass | Best case | Worst case |
| --- | --- | --- | --- |
| Selection sort | at most 1 | `Ω(n²)` | `O(n²)` |
| Bubble sort | many | `Ω(n)` | `O(n²)` |

## Recursion

A **recursive** function calls itself on a smaller version of the same problem. It needs a **base case**, a size small enough to answer directly, or it calls itself forever.

The lecture rebuilds the Mario pyramid: a pyramid of height `n` is a pyramid of height `n - 1` with one more row underneath.

```c
void draw(int n)
{
    // Base case
    if (n <= 0)
    {
        return;
    }

    // Draw the smaller pyramid first, then this row
    draw(n - 1);
    for (int i = 0; i < n; i++)
    {
        printf("#");
    }
    printf("\n");
}
```

Binary search is naturally recursive too: "search the left half" is the same algorithm on a smaller list.

## Merge sort

Merge sort uses recursion: sort each half, then merge the two sorted halves.

```
If only one number
    Quit
Else
    Sort left half of numbers
    Sort right half of numbers
    Merge sorted halves
```

- **Merging** two sorted lists is easy: look at the front of each, take the smaller, repeat.
- The list can be halved `log n` times, and each level of halving does `n` work merging, so it's **`Θ(n log n)`**, the same for sorted, random and reversed input.
- The trade-off is **memory**: merging needs a second array, so it uses `O(n)` extra space. Selection and bubble sort sort in place.

## From my study sessions

**Measuring with `time`**: `time ./sort1 file.txt` prints three numbers.

- `real`: wall-clock time, everything including waiting (disk, printing to the terminal, other programs).
- `user`: CPU time spent running the program's own code. Use this one to compare algorithms.
- `sys`: CPU time the operating system spent on the program's behalf (reading files, printing).
- Add `> /dev/null` to throw away the output so printing doesn't dominate the timing.
- Tiny differences (0.003s vs 0.004s) are noise. Don't explain them.

**To identify an algorithm from timings**, test the input where the candidates behave *differently* (sorted input separates bubble sort from selection sort) and compare a program against **itself** across input orders and sizes. 10× more data taking ~10× longer looks linear; ~100× longer looks quadratic.

**2D arrays**: `int grid[ROWS][COLS];` is a table. `grid[i][j]` is row `i`, column `j`. Keep straight which numbers are **indexes** (where you are) and which is the **value stored** (what's there). A value can itself be an index into another array.

**Ints have no infinity.** `INFINITY` from `<math.h>` is a float. For a "bigger than anything" starting value with ints, use `INT_MAX` from `<limits.h>`, or a bound from the problem itself.

**Checking vs setting a bool**: `if (!x)` *checks* that `x` is false. On its own line, `!x;` does nothing (clang reports "expression result unused"). To *set* it, assign: `x = true;`.

**Working in code someone else started**

1. Read `main` top to bottom first, like a story.
2. List the global data and what each one holds; draw a tiny example.
3. Treat each TODO function as a contract: what goes in, what comes out, what it changes.
4. Trace a small example by hand.
5. Write one function at a time and test it before moving on.
