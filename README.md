# Cannery Line

A one-button factory game. Tap to push rotten or stray food off the belt before it spoils a can.

- Week 7 (original): https://albedovo.github.io/hello_world_weeek7-8_can/
- Week 8 (revision): https://albedovo.github.io/hello_world_weeek7-8_can/week8/

## Week 8: one revision (Route A · improve an earlier project)

| Part | |
|---|---|
| **Intention** | In week 7, harder levels only made the same decision faster. I want players to think before they tap. |
| **What changed** | Pads are staggered and kept clear of the cans. A pushed item drops onto the line below and needs another push, until the last pad sends it to the bin. A stray pushed onto its own line is sorted into that can. After playing it myself I also evened out the item mix, made every goal reachable when every item is handled correctly, merged 9 levels into 6, and added first-time tips, pad flashes, and icons on the results screen showing what got into each can and which good food was pushed off. I also added an endless mode: no clock, the line keeps speeding up, and every spoiled can or good food pushed off costs a star. At 0 stars the shift ends. In every mode, sealing 5 cans in a row wins back a lost star. |
| **What stayed** | One button, and one tap still fires every pusher. Foods, cans, music and 2-player battle are unchanged. |
| **Mechanism and boundary** | Every item moves at the same speed, so where it will be is known from its position. A new item is only accepted if there will always be a moment to tap that pushes what must go and nothing that must stay. |
| **Prediction** | Without that rule, some rotten items would arrive with no safe moment to tap. With it, none would. |
| **Observed check** | A test bot taps only at safe moments. On the multi-line levels (6 runs each), 56 cans spoiled with the rule off and 0 with it on. The longest wait between taps went from 13.2 s to 5.6 s. These are bot checks, not how a person feels. |
| **Not checked yet** | Whether a person can find the safe moment in time (about 0.2–0.3 s), and whether the goal is too easy. |
| **Decisions and credits** | My decisions: cascade pushing instead of more difficulty, staggered pads, no lose-lose situations, and the second-round changes after my playtest. The code was written with Claude's help. Art is the same as week 7. |
| **Next question** | Does the three-line level feel like a puzzle, or just busy? I'll ask a classmate to play level 4 before I explain anything. |

## Playtest notes

**Observed (me, author):** With the first-time tips, the game is much clearer than before. The revision also adds gameplay. In week 7, new levels only added more information and more lines. Now the new information (drops, sorting) creates new decisions, and it makes more sense: food that falls lands on the next belt, and a stray ends up in its own can.

## Prompt and first response

The prompt where I gave the most feedback, after playing the first version. Original in Chinese with an English translation, so the meaning isn't lost in translation.

<details>
<summary>Prompt (Chinese original)</summary>

> 2竖屏时把三块推板整体往右移，横屏的时候稍微左移动一点，现在推板距离
> 5不要在关卡中显示。在结算的时候显示吧。
> 345这几个总结一下就是让反馈更明显。同时给予提示。还有让新人玩家更好上手。
>
> 现在水果给的太随机了。我玩了几把里面有前面一大段不用按的，修改的平均一点 其次关卡难度设置的太分开了。123可以合并成2关，1正常1条 2两条+其他东西。 在玩家第一次碰到新加入的信息的时候需要给出提示
>
> 还有现在有些关卡就算全部按对了也达不到要求。水果给的不够多，水果的随机性或者过关要求需要修改

</details>

<details>
<summary>Prompt (English translation)</summary>

> 2: In portrait, move all three pads to the right; in landscape, move them slightly left. Right now the pads are [too close to the cans].
> 5: Don't show it during the level. Show it on the results screen.
> 3, 4, 5 in short: make the feedback clearer, give hints, and make it easier for new players to get started.
>
> The fruit is too random right now. In a few runs there was a long stretch at the start with nothing to tap. Make it more even. Also, the difficulty steps are too spread out. Levels 1–3 can be merged into 2: level 1 is normal with one line, level 2 is two lines plus the other items. The first time the player meets something new, show a tip.
>
> Also, on some levels you can't reach the goal even if you tap everything right. There isn't enough fruit. Either the randomness or the goal needs to change.

</details>

<details>
<summary>First response</summary>

> Lots of good feedback. Here's how I read each point; I'll build all of it and test with the bot:
>
> - **Pads**: shift right in portrait, slightly left in landscape, and keep the current spacing between pads (your sentence got cut off, so I'm assuming spacing stays as is).
> - **Where you missed**: shown only on the end-of-level screen, with tips.
> - **Feedback and onboarding**: a tip pops up the first time each new thing appears, and the pads give clearer feedback.
> - **Fruit pacing**: the mix comes out more evenly, with no long stretches where you don't need to tap.
> - **Levels**: old levels 1–3 become 2 levels: level 1 is one line, level 2 is two lines plus the other items.
> - **Goals**: always reachable if you play every item correctly.

</details>
