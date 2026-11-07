# Cannery Line

A one-button factory game. Food rides the belts into each line's can. Tap to push rotten or stray food off the belt before it spoils a can.

- Week 7 (original): https://albedovo.github.io/hello_world_weeek7_can/ (`index.html`)
- Week 8 (cascade revision): https://albedovo.github.io/hello_world_weeek7_can/week8/ (`week8/index.html`)

Open either file through any static host to play. Both share the art in `cannery/`.

## Week 8 revision: cascade pushing

### Intention
In the week 7 version, extra levels only made the same decision faster ("tap when something rotten is on the pad and nothing good is"). I wanted the player to **think before tapping**, not just react faster.

### What changed
- **Staggered pads.** With two or three lines, the pads step to the right from the top line down instead of lining up vertically.
- **Pushed items drop to the line below.** Rotten food on the top line needs a push on every pad until the last one sends it into the bin, which now sits under the last pad.
- **Sorting.** A fresh stray pushed down onto the line that cans its food becomes good food there ("Sorted +$"), and it fills that can.
- **Money for a reject** is paid once, when the item reaches the bin or gets sorted, not on every push.
- **Levels** went from 9 to 6. The old one-line levels 1–3 became level 1 (one line) and level 2 (two lines plus strays and big items). After that: two lines at speed, three lines, three lines with strays, rush.

### What stayed
One button. One tap fires every pusher. Same foods, cans (6 per can, +$30 seal), quality stars, timer, music and 2-player battle.

### The rule I protect
**At every moment there is at least one safe tap: a moment that pushes what must go and nothing that must stay.**

How it works: every item moves at the same belt speed, so where an item will be is fixed by its position alone. When an item is created, the game plans the pads it will meet if played correctly: pushed where it doesn't belong, kept where it does. It accepts the item only if every "must push" window keeps at least 30 px of belt travel free of every "must keep" window. Otherwise it tries another line or waits a moment. Good food knocked off by mistake falls straight into the bin, so a mistake never creates a new unsolvable situation.

### Before / after check
A test bot taps whenever something that must go is on a pad and nothing that must stay is (open `week8/index.html#debug`). It never pushes good food, so any can it spoils is a situation with no safe tap.

| Levels 4–9, 6 runs each, phone layout | Cans spoiled |
|---|---|
| Fairness rule off | 56 |
| Fairness rule on | 0 |

Desktop layout and all three battle sizes also showed 0. Level targets are about 70% of what the bot earns.

### Second round, after my own playtest
What I noticed playing it, and what changed:

| I noticed | Change |
|---|---|
| Long stretches with nothing to tap | Items now come from a bag of 10 with the level's exact mix, and the ones that need a tap are spread evenly through it. |
| Some levels couldn't be cleared even with every tap right | The goal is no longer set by hand. Before each shift, the game plays the exact same items once offscreen without mistakes and sets the goal to 85% of that run's base pay. No new items start after the last moment they could still reach a can. Handling every item correctly always clears the level. |
| Levels 1–3 were too similar | Merged into two levels (see above). |
| Hard to tell what's going on | The first time something new appears (rotten food, big item, stray, a stray to sort, a drop to the next line, good and bad on pads at once), the shift freezes and a bubble points at it. Each tip shows once; "Show tips again" in the level menu resets them. A pad turns darker while something sits on it and flashes green or red after each push. |
| Where I made mistakes | Shown only after the shift: which pad things got past, where good food was pushed, plus a tip for next time. |
| Top-line pad too close to the left edge on phones | Portrait: pads moved right (smaller cans make room), same spacing. Landscape: pads moved slightly left. |

Check with the same bot (10 runs per level, desktop layout):

| | Longest wait between taps | No-mistake run clears |
|---|---|---|
| Round 1 (9 levels) | up to 13.2 s | 90/90 |
| Round 2 (6 levels) | up to 5.6 s | 60/60, guaranteed by how the goal is set |

A bot that misses 10% of the items it should push still cleared every level. One that misses 25% failed about 1 in 10 shifts. The goal may still be too easy for people who don't miss much; that's for playtesting.

### Decisions, credits and AI contribution
- My decisions: cascade pushing instead of extra difficulty; pads must stagger to the right; no situation may force a lose-lose choice.
- Round 2: I playtested and asked for an even mix, achievable goals, merged early levels, first-time tips, clearer feedback, mistakes shown only on the results screen, and the pad positions.
- AI (Claude) proposed the staggered layout, sorting, the position-based fairness check, the bag and the offscreen run that sets the goal. It implemented the code and ran the bot checks.
- Art and assets: same as week 7.

### Playtest notes (to fill in)
- Who played, which level:
- What they did before I explained anything:
- Did they discover sorting on their own?
- Did the tips help, or get in the way?

### Remaining question
The bot proves a safe tap always exists, but not that a person can find it in time. Is 30 px (about 0.2–0.3 s) enough for a human, and does the three-line level feel like a puzzle or just busy?
