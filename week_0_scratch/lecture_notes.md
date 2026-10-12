# Lecture 0 — Scratch

Computer science is problem solving: **input → algorithm → output**. Everything a computer stores comes down to bits.

**Binary**

- A bit is 0 or 1 (off/on, like a switch or transistor). 8 bits = 1 byte.
- Place values are powers of 2: 1, 2, 4, 8, 16… So `101` = 4 + 0 + 1 = 5.
- n bits give 2ⁿ patterns. 8 bits → 256 values (0–255).

**Representing data**

- Text: ASCII maps numbers to characters (`A` = 65, `a` = 97). Unicode extends this to cover every language and emoji, using up to 4 bytes.
- Colour: RGB — three bytes for red, green, blue (0–255 each). Each pixel stores one RGB value.
- Images are grids of pixels; video is many images shown quickly; sound is numbers for notes, volume and duration.
- Same bits, different meaning — context (the program) decides whether `72` is a number, `H`, or a shade of red.

**Algorithms**

- An algorithm is step-by-step instructions to solve a problem. It must be correct first, then efficient.
- Phone-book search: one page at a time is n steps; two at a time is n/2; halving each time (binary search) is log₂ n. Doubling the book adds just one step.

**Pseudocode** — plain-English steps. Its building blocks recur in every language:

- Functions (verbs: pick up, open, call)
- Conditionals (if / else if / else)
- Boolean expressions (yes/no questions)
- Loops (go back to step 3)

**Scratch**

- Drag-and-drop blocks that show the same ideas: functions, conditionals, loops, variables, events, and abstraction.
- Abstraction = wrap details in a named block (e.g. a custom `meow` block) so you can think at a higher level.
- Good design: avoid copy-paste; use loops and custom blocks instead.
