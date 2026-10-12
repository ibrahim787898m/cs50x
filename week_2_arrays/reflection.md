# Week 2 — Arrays — Reflection

My own lessons from this week's problem set, in my own words. No solution code (CS50 academic honesty policy).

## Problems

### Scrabble

- What I learned: I learned how an array can store related values and how a function can be reused to do the same job for both players. I also learned how to handle uppercase and lowercase letters so the program treats them the same way.
- How it went: This was my cleanest problem. Once I had tested the score function for one player, I could reuse it for the other player, which made the rest of the program easier to build and test.

### Readability

- What I learned: I learned how to split one program into smaller functions. Making separate functions for the different counts made the main part of the program easier to read. I also learned about converting values so a calculation can use decimals instead of only whole numbers.
- Mistakes and how I found them: In my first pseudocode calculation, I rounded the averages too early, and my code copied the same mistake. I found it when my results were off by a grade. Now I check the numbers in my plan as carefully as my code.
- I also had a boundary mistake with the `Grade 16+` result. The normal tests passed either way, so it reminded me to check the edge cases around a condition, not only the usual cases.

### Caesar

- What I learned: I learned how command-line arguments work and how to check that a user gives a valid key before the program continues. I also learned more about working with individual characters, including checking whether a letter is uppercase or lowercase.
- Mistakes and how I found them: At one point, only the first character printed. I noticed it when I tested my own inputs and expected the whole message to appear. I also found that an earlier version of my key check accepted keys it should not have, such as a negative key or a key with a symbol.
- check50 passed, but testing my own edge cases showed me that a green result does not always mean the program is completely finished.

## Patterns from this week

- Breaking a bigger program into smaller functions made it easier to test and understand.
- Temporary print checks helped me see what the program was doing at each step instead of guessing.
- Passing check50 does not mean the program is completely correct, so I need to test edge cases myself.
- For input checks, I should define what is allowed instead of trying to list everything that is not allowed.
- I am getting more comfortable using strings, characters, and arrays, but I still need to choose clearer variable names and clean up test lines before submitting.

## What I'll do differently next week

- For longer programs, I will test each function with temporary print checks as I write it, then delete those checks before submitting.
