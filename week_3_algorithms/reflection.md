# Week 3 — Algorithms — Reflection

This week I learned about sorting algorithms and also did the Plurality and Runoff problem in C. The main reason I made mistakes in Plurality and Runoff is I was rushing, so I skipped making rough notes and a plan before writing code.

## Problems

### Sort

- I ran all the sorting files with sorted, reversed and random input. I tested it with 5000, 10000 and 50000 values.
- I collected all the time data and compared them. I looked more at the user time because it shows the time the program was using.
- I learned that real time is the total time passed, but user time is the CPU time the program used. For comparing the sorting algorithms, user time helped me more.
- I learned that input order can make a big difference. For one sorting algorithm, sorted input was much faster, but reversed and random input took much more time. When the input size got bigger, the difference was very big.
- I learned about Bubble Sort, Merge Sort and Selection Sort. Bubble Sort can be good when the list is already sorted because it can stop after checking the pairs. But for random or reversed input it can take much more time.
- I learned Selection Sort does not really know if the list is sorted or not, so it still checks the values again and again. Because of this, the input order does not help it much and it is still slow when the input gets bigger.
- I learned Merge Sort was more consistent for sorted, reversed and random input. It was much faster with the bigger input size, but it needs extra space when it divides the list and merges the halves.
- I learned Big O, best case, average case and worst case. I understand more now why O(n) is better than O(n^2) when the input size gets bigger, and why O(n log n) is useful for big data.
- I did not write the exact answers for the sorting file identification questions because I do not want to upload problem answers in the repo. My approach was to run the tests, collect the data, compare the timings and use what I learned about the algorithms.
- At first I missed the sorted test files. I also thought sort1 was Insertion Sort and I thought reversed input was the best case for Bubble Sort. After I ran all the input orders and compared the data again, I saw my first thinking was wrong.

### Plurality

- In this problem I was first struggling because I did not read the entire half pre written file properly and I did not write the pseudocode.
- I needed to understand the candidate struct, how it stores candidate names and votes, and which function is doing what.
- I was missing the global variable and the macro that was predefined. I needed to understand which variable is holding which value and how to use this value.
- When switching from Python to C I was struggling with C syntax like semicolon, `strcmp`, and writing conditions.
- After I understood the file, I used a two pass way for finding the winner. First find the highest votes, then check the candidates again and print every candidate with that vote. This also works if there is a tie.
- I used `printf` to debug the code while solving the problem, and check50 was green on my first submit.
- I learned that if the problem is half written and I need to solve the rest, first I need to read the entire file up to down each line and note it.

### Runoff

- In this problem I made the same first mistake. I did not read the entire half pre written file properly and I did not write the pseudocode.
- I was struggling with the 2D preferences array, how they are storing each voter choice and rank, and how all the functions work together in the runoff loop.
- One bug was my debug print showed 0 votes. I found that I put the print in the wrong place, before the counting happened.
- Another bug was the minimum vote was including candidates who were already out. I found this by tracing the election by hand.
- My tie check stopped after checking the first candidate. My first tests passed, but it failed when I changed the order of the candidates. This showed me I need to test different input orders too.
- The tie check was also counting eliminated candidates, so a real tie was missed. I found it with a test where one candidate was already out and the other two were tied.
- At first I thought elimination means removing ranks from a ballot. I learned it means removing a candidate from the election, then the voter next choice can be used in the next round.
- I was missing the global variables and the macros that were predefined. I was also struggling with the candidate struct, especially votes and eliminated value.
- I used `printf` and tracing by hand to debug the problem. After I understood the vote count and elimination logic I could solve each function one by one.
- I learned how to work with a 2D array for storing voter preference and more about using bool value in C struct.

## Patterns from this week

- I learn better when I test and compare the result by myself. In Sort, running all the tests and looking at the times helped me understand why input size and input order matter.
- The root cause for Plurality and Runoff was I was rushing. I skipped the rough notes and plan, then I started writing code before fully understanding the pre written file.
- In Runoff, just passing the normal tests was not enough. Changing the candidate order showed a bug that I did not see before.
- Using `printf` and tracing by hand helped me find what was happening in the code.

### C things I learned

- `==` on strings compares their addresses, so I need `strcmp` to compare the text.
- `int` does not have infinity, so I can use `INT_MAX` when I need a starting value bigger than the votes.
- `!x` checks if x is false. It does not set x to false.
- `=` is for giving a value and `==` is for comparing values.

## What I'll do differently next week

- Understand the problem before writing code.
- Read the entire provided file line by line before changing anything.
- Write pseudocode first and make good planning and preparation before coding.
- Write which function is doing what, what it returns and what it is taking as argument.
- Write which variable is holding which value.
- Solve one function at a time after understanding how it connects with other functions.
- Trace the program by hand before running it.
- Test with different input orders, not only different values.
