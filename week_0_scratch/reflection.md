# Week 0 — Scratch — Reflection

My own lessons from this week's problem set, in my own words. No solution code (CS50 academic honesty policy).

## Problems

- Signal 0: Made an interactive binary puzzle game where the player turns on 8 light bulbs (values 128 down to 1) to match binary signals and decode ASCII characters to spell out "HI!".

## The idea

- I was thinking of a puzzle about solving a signal coming from space. In the story, I work at NASA, and my job is to detect signals from our different missions and from space, and find the meaning of each message.
- One day I find a suspicious unknown signal, and I need to decode it. The message might be from another species on another planet.
- My plan was: the first screen is the intro with a START button, the second is a control room with buttons like Scan, Analyze and Decode, the third is the puzzle using binary, ASCII or Unicode from Lecture 0, and the final screen shows the message as the ending.
- I'm always into space and NASA stuff and I knew how the logic of the game would work but as it was my first time using scratch I needed to learn about blocks, designing sprites, and screen and color stuff from Claude.

## How I play the game

**Step 1: Start the Game**

- I see the game title, a short story, and a START button.
- When I hover over the START button, it grows slightly.
- I click START to enter the control room.

**Step 2: Enter the Control Room**

- I see a DECODE SIGNAL button.
- I click the button to open the decoder.

**Step 3: Decode the Signal**

- I see an 8-bit binary signal and eight bulbs with values of 128, 64, 32, 16, 8, 4, 2, and 1.
- I figure out which bulbs I need to turn on to match the binary signal.
- I turn on the correct bulbs and press TRANSMIT.

**Step 4: Check My Answer**

- If my answer is correct, the game adds the corresponding letter to the secret message.
- If my answer is wrong, an error sound plays, and I see "Signal mismatch. Try again."
- I try again until I decode the signal correctly.
- I repeat Steps 3–4 for each signal: H, I, then !

**Step 5: Reveal the Message**

- After decoding all the signals, I reach the ending screen.
- I see "TRANSMISSION DECODED" and discover the final message: "HI!"

**Step 6: Play Again**

- The game tells me to press the green flag to start a new game.

## What I learned

- How to split variables between sprites: I learned the difference between "for this sprite only" (local) and "for all sprites" (global). Each of the 8 bulbs needed its own local variable to track whether it was on or off, while the total sum and current round had to be global so the buttons could check them.
- Using broadcasts to control screen changes: Instead of putting everything in one messy loop, I used broadcasts to trigger changes between screens (welcome screen, control room, and win screen) and reset the bulbs between rounds.
- Writing reusable custom blocks: Instead of writing the same check logic three times for each puzzle, I made a custom block with parameters to verify the sum and letter. It kept the transmit script much cleaner.

## Mistakes I made and how I found them

- The checks ran all at once in one click: When checking round 1, my script updated `round` to 2 right away, and then the check for round 2 immediately ran on that exact same click. It skipped straight ahead. I found this by watching the round number jump unexpectedly, and fixed it by nesting the conditions so only the active round is tested per click.
- Costume switching by number instead of name: In the signal display sprite, I tried switching costumes using the round variable directly. Scratch treated the number as costume index position rather than the costume name (`r1`, `r2`, `r3`). I noticed it when the display showed the wrong costume, and fixed it by joining the letter "r" with the round number.
- Resetting bulb states: When moving to the next round, the total sum cleared, but some bulbs visually stayed turned on. I had to use a broadcast to tell every bulb sprite to reset its own on/off status before accepting new clicks.
- The hover animation loop kept running: My hover animation loop on the start button kept running in the background even after switching to the control room screen. I found this when the loop continued after the screen changed.

## What I'll do differently next week

- Stop loops when leaving a screen: Next time, I will make sure to cleanly stop unused loops when leaving a screen.
- Trace click order on paper first: I spent too much time debugging why multiple checks fired on a single button press. Next time I have buttons changing states, I'll trace what happens step-by-step before wiring up all the blocks.
