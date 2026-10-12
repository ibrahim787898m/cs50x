# Week 1 — C — Reflection

My own lessons from this week's problem set, in my own words. No solution code (CS50 academic honesty policy).

## Problems

### Hello, World and Hello, It's Me

These were my first C programs after Scratch. I learned how to include libraries, use `main`, print text to the terminal, get a name from the user, and put that name into a greeting.

### Mario (Less and More)

- What I learned: I learned how to use nested loops to print a pattern one row at a time and to keep asking for the height until it was between 1 and 8. When I made Mario More, I reused the idea from Mario Less to make the second pyramid. I also ended up repeating a similar loop twice, which taught me that repeated code can be a sign that I should move it into a function later.
- Mistakes and how I found them: I made mistakes with the loop limits at first. Testing small heights like 1, 2, and 3 helped me catch off-by-one mistakes and check whether both pyramids had the correct number of rows.

### Cash

- What I learned: I learned how variables can change inside a loop and how conditions can control what happens next. I also learned to check that the user gives a valid input before the rest of the program runs.
- Mistakes and how I found them: My program worked, but it only handled one coin on each loop pass. For 99 cents, it took 9 passes. Afterwards, I learned there was a more direct way to do the same work.

### Credit

- What I learned: This was the longest program because I had to check both whether a card number passes the checksum and what type of card it is. Splitting one big problem into smaller functions helped me keep the program organized. I also learned that a valid checksum alone was not enough, so I also had to check the card type.
- Mistakes and how I found them: At first, I needed to understand exactly which digits I was getting from the number. I used temporary print lines to check values such as the remaining number, the current digit, and the running sum. This helped me find where I was getting confused.
- I submitted the file with a lot of commented-out experiments still in it. The tests helped me debug, but next time I will delete them before submitting or keep them in a separate test file.

## Patterns from this week

- Clear variable names are something I need to improve. I used names like `x` and `counter`, but more descriptive names would have made the longer programs easier to read and debug.
- I learned that repeated work can be placed in a loop or a function instead of writing the same instructions again.
- Testing small parts of a program made debugging easier. For example, I printed temporary values in Credit and tried small inputs in Mario and Cash.
- I learned that temporary testing lines should be deleted before submitting or moved into a separate test file.
- Before submitting, I need to check input rules, test normal and edge cases, and make sure the output says exactly what the problem asks for.
- Before coding the problem I did think about the problem in my head and then tried to write how the program would work in pseudocode. I think this helped me understand the problem better and made it easier to write the code.

## What I'll do differently next week

- For a bigger problem like Credit, I will add print checks from the start to test each small part instead of waiting until the whole program is finished. I will delete those checks before submitting or keep them in a separate test file.
