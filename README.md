# mhxx-rng

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/apmnnn/mhxx-rng/blob/main/mhxx-rng.ipynb)

> [!NOTE]
> This is an English translation of [apmnnn/mhxx-rng](https://github.com/apmnnn/mhxx-rng) (MIT License). The documentation has been translated, the code comments are in English, and the notebook's example cell now calls `set_en()` and uses English skill names.
> The Colab badge above still opens the original repository's notebook, which defaults to Japanese (`set_ja()`). To use the English version, open this copy's `mhxx-rng.ipynb`, or call `set_en()` in the first cell.


# Contents

1. [Introduction](#introduction)  
1. [How charms are generated](docs/charm_generation.md) 
1. [The RNG formula and how the RNG behaves](docs/rng.md) 
1. [Function reference](docs/functions.md)  
1. [Sniping basics 1](#sniping-basics-1)  
1. [Sniping basics 2](#sniping-basics-2)  
1. [Sniping in practice](#sniping-in-practice)
1. [Sniping using item combinations](docs/combo_snipe.md)  
1. [Analysis and observations](docs/analysis.md)  
1. [Halcyon Melding and Juju Melding](docs/melding.md)  
1. [Ranks](docs/rank.md)
1. [Quest rewards and item combinations](docs/reward_combo.md)  
1. [Future plans](docs/future.md)
1. [Notes and cautions](#notes-and-cautions)
1. [Well-known charms](docs/charms.md)
1. [Changelog](docs/history.md) 

## Introduction

This is an RNG analysis tool for sniping charms in MHXX (Monster Hunter Generations Ultimate).

If you don't have a Google account, create one, then open the "Open in Colab" link above and run the notebook.

This program has been tested with Python 3.12.13.

## [How charms are generated](docs/charm_generation.md)


## [The RNG formula and how the RNG behaves](docs/rng.md)


## [Function reference](docs/functions.md)


## Sniping basics 1

> [!NOTE]
> It is now possible to determine your RNG position from item combinations, so you may want to try the faster and more accurate [sniping using item combinations](docs/combo_snipe.md) instead.

Let's start by aiming for a "Chain Crit 4 / Tenderizer 5 / 3 slots" charm, which sits at a very early RNG position.


This guide uses the Switch version, digital download, saved to system memory.

It should also be possible on the 3DS version, with data saved to an SD card, or with a physical cartridge.


What you need:

- A timer
(one that measures to hundredths of a second)

- Somewhere to record the result of each attempt


Here we use the app "Timer & Stopwatch Plus". Anything that lets you switch between two timers will do.


First, save in Kokoto Village.

Start the timer at the same moment you select MHXX on the Home screen. While watching the timer, press A at a pace of 4 times per second.

Stop the timer at the same moment you press "continue". Then mash A to select your save file.

Go straight to the Melding Pot, skip the dialogue with B, and insert the charms as fast as possible.

Then complete any quest and check the melding result.


Suppose you got a Crisis 4 / Rec Level 2 / 0 slots charm. 


Next, open the program.

First, run the 1st, 2nd and 3rd cells.

Then change part of the top cell to

```python
p = parameter('Crisis',4,'Rec Level',2,0,'Melding')

search(0,10000,p)

#around(4723,60,'Melding')

#watch(4723 - 1717)
```

and run it.

See the 3rd cell for skill names. If there is no second skill, enter '' (an empty string). Lines starting with \# are not executed.

This searches the melding charms in frames 0–10000, and shows that this charm is the charm at frame 1725.

Next, change the cell to

```python
p = parameter('Crisis',4,'Rec Level',2,0,'Melding')

#search(0,10000,p)

around(1740,60,'Melding')

#watch(4723 - 1717)
```

and run it.
This shows the melding charm at frame 1740 and every charm within 60 frames either side of it.

Use this as a reference point to work out your own average.


Go back to the Home screen, close the game, and repeat the charm appraisal above about 10–30 times.

Notes and tips:


By pressing A 4 times per second on the title screen, you can (on Switch) press continue at around 13.00 seconds.

Pressing continue advances the RNG by a very unstable amount.

However, if you press it on nearby frames, you will land on the same RNG position.

So you don't need to worry about being a few frames off.

Also, how far the RNG advances when you press continue has little to do with how early you press it.

Keep in mind that you can press continue earlier and still get a larger advance, landing on a later RNG position.


The movement after you enter the village aims to keep the number of frames until the melding (≈ the amount the RNG advances) constant.

Melding as fast as possible should reduce variation.


Overall, focus on reducing the variation in RNG advance.


From pressing the timer until pressing continue, it is probably easier to stay consistent if you watch only the timer, not the game screen.


It may help to practise stopping a stopwatch at an exact time with little variation beforehand, or to practise sensing 30F, 15F and so on without a timer.


## Sniping basics 2

Once you have done about 10–30 melds and found the variation and your own baseline, the next target is Chain Crit 4 / Tenderizer 5 / 3 slots.


First, take 1717 as the initial baseline.

Next, change the cell to

```python
p = parameter('Chain Crit',4,'Tenderizer',5,3,'Melding')

search(0,10000,p)

#around(1740,60,'Melding')

#watch(4723 - 1717)
```

and run it.

This shows that Chain Crit 4 / Tenderizer 5 / 3 slots is at frame 4723.

Then run the cell with

```python
p = parameter('Chain Crit',4,'Tenderizer',5,3,'Melding')

#search(0,10000,p)

#around(1740,60,'Melding')

watch(4723 - 1717)
```

The result is 1m 40s 6f, that is, 1 minute 40.20 seconds.

This is how long you wait on the title screen.

Next, run the cell with

```python
p = parameter('Chain Crit',4,'Tenderizer',5,3,'Melding')

#search(0,10000,p)

around(4723,60,'Melding')

#watch(4723 - 1717)
```

This shows the charms around Chain Crit 4 / Tenderizer 5 / 3 slots.


As before, start the timer at the same moment you select the game on the Home screen, and press A 4 times per second.

This time, press continue, and at the same moment you press A on your save file (as fast as possible) stop the first timer and start the second.

Up to this point, watch only the timer, not the game screen.

When the second timer reaches 1:40.20, press A and stop the timer. Your save file loads.

As before, do the melding as fast as possible.


Repeat this a few times.

At first, you will probably be a few tenths of a second away from the target charm.

After a few attempts, once you have a feel for the offset, fine-tune when you load.

The first snipe should take about 20–30 attempts.


If the timer shows that you pressed continue at the wrong moment, it's best to restart right away.

If you make a small mistake partway through, or think you took the wrong route or talked to the Melding Pot from the wrong distance, adjust your timing accordingly.


## Sniping in practice

Once a snipe succeeds, repeat until you have collected 5 Chain Crit 4 / Tenderizer 5 / 3 slots charms.

Get used to keeping the variation stable.

With practice you can snipe about 1 in every 5–7 attempts.

After 5 snipes you should have enough data, so use that time as your new baseline.

Next, use search(), watch() and around() for the charm you actually want.

For example, for Tenderizer 6 / Expert 10 / 3 slots,

```python
p = parameter('Tenderizer',6,'Expert',10,3,'Melding')

search(0,1000000,p)
```

shows that it is at frame 296260.

The difference from Chain Crit 4 / Tenderizer 5 / 3 slots (frame 4723) is

```python
watch(296260 - 4723)
```

which gives 2h 41m 57s 27f, or 2 hours 41 minutes 57.9 seconds.

Then check the surrounding charms with

```python
around(296260,60,'Melding')
```

The charm 6 positions earlier has two skills, so this is not an isolated charm.

Press continue just as you did for Chain Crit 4 / Tenderizer 5 / 3 slots, and wait for the Chain Crit 4 / Tenderizer 5 / 3 slots waiting time plus the time you just calculated.

While waiting, keep the console charging, and on Switch turn off auto-sleep.

It helps to work out in advance when you need to check on the game.

The melding is done the same way as before.


## [Sniping using item combinations](docs/combo_snipe.md)


## [Analysis and observations](docs/analysis.md)


## [Halcyon Melding and Juju Melding](docs/melding.md)


## [Ranks](docs/rank.md)


## [Quest rewards and item combinations](docs/reward_combo.md)


## [Future plans](docs/future.md)


## Notes and cautions

Load from heat, or game software downloading in the background, may cause frames to advance more slowly.

(For example, fewer than 30F passing in one second.)

It may be best to avoid downloading other software, and if you leave the console running in summer, to keep it at a suitable temperature with a fan or similar.

Also, since system or other game updates might download without you noticing and add load, it may be best to turn on airplane mode.


This program was not built from a complete analysis of the game's behaviour, so it may show results that differ from the actual game where the behaviour has not been fully reproduced.
There is also no guarantee that the program is free of human error.
Use it at your own risk.


In Colab, if the output exceeds 5000 lines, the oldest lines are cut off. If you want to output many results, split them into smaller batches.


If you want to use more advanced features, read the [function reference](docs/functions.md).


## [Well-known charms](docs/charms.md)


## [Changelog](docs/history.md)
