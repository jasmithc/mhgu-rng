This page explains how to find your current RNG position from item combinations and use it to snipe.

It lets you snipe faster and more accurately than the method in "Sniping basics".

---

As preparation, remove your Palico if you have one with you, and set your room service to the Moga Village receptionist (モガの村の看板娘). In your item pouch, carry Combo Book 1 and plenty of Husk Berries and Needleberries. Once that's done, save in Kokoto Village.

You will also use the Switch's 30-second video capture, so make sure your Album is not full.

---


Each press of continue on the title screen advances the RNG by about 700 frames. Use this so that when you load your save, the game starts at least 30 seconds before the target RNG position.

If the target charm's RNG position is close, or you don't mind a longer wait, you can adjust by waiting alone.

For example, say the target this time is Chain Crit 4 / Tenderizer 5 / 3 slots.

Start the game, press continue 4 times, then load your save straight away.

Then go to your house, open the menu with Start, and at the same moment you start the timer, hold down "Combine" and combine Normal S Lv2.

Once you have combined about 50 Normal S Lv2, capture a 30-second video with the Switch's capture function, and pause the timer at the same moment you press the Home button.

Now open the program.

If you already know the position of the charm you want to snipe, you don't need the code at the top this time, so comment it out.

```python

p = parameter('Chain Crit',4,'Tenderizer',5,3,'Melding')

#search(0,10000,p)

#around(4723,60,'Melding')

#watch(4723 - 1717)

```

Next, watch the video you just captured in the Album, enter the changes in your ammo count into combo, and run it.

```python

combo = '''
0 2 4 7 10 13 16 18 22 25
28 30 32 35 39 42 45'''

search_combo(0,10000,combo)

#watch(4723 - 3800)

#around(4723,60,'Melding')

```

This searches frames 0–10000 for RNG values that match this sequence of combination counts, and finds that the RNG position when combining started was 3831.

Next, run

```python

combo = '''
0 2 4 7 10 13 16 18 22 25 28
30 32 35 39 42 45'''

#search_combo(0,10000,combo)

watch(4723 - 3831)

#around(4723,60,'Melding')

```

to convert the difference between the target RNG position and the RNG position when combining started into a time.

29s 22f, that is, 29.73 seconds.

Resume the timer at the same moment you return to the game from the Switch Home screen. Walk (don't run) up to the room service and get ready to meld.

Insert the charms at the exact moment the timer reaches the time you just calculated, and stop the timer.

Next, run

```python

combo = '''
0 2 4 7 10 13 16 18 22 25 28
30 32 35 39 42 45'''

#search_combo(0,10000,combo)

#watch(4723 - 3831)

around(4723,60,'Melding')

```

then complete any quest and check the melding result. Record the calculated time, the timer's time, and how far you were from the target charm, and repeat.

You will probably succeed within a few attempts. Once you succeed, repeat it many times until you are comfortable.


To aim for other charms, snipe a charm reasonably far from Chain Crit 4 / Tenderizer 5 / 3 slots a few times. Then, from the difference between the two RNG positions and the difference in the number of continue presses, work out how many presses you need to aim for distant charms.

Alternatively, as a shortcut, treat the period (in frames) of the continue loop plus 702 as the RNG advance per loop, and increase the number of presses by the difference between the target and the reference divided by that value.
