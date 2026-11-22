### `ascend()`

Advances the RNG by one.


### `descend()`

Calculates what the previous RNG value was.


### `roll()`

Keeps the last 7 RNG values and advances the RNG by one.


### `init()`

Initialises the variables.


### `jump(◯)`

Moves quickly to RNG position ◯, then calls roll() 7 times.


### `set_ja()`

Sets the language to Japanese.

set_en() sets it to English, and set_zh() to Simplified Chinese.

Skill names are listed in ID order. If needed, refer to Kiranico or similar.


### `set_blue()`

Sets the mode to search for Enduring Charms.

set_red() sets it to Timeworn Charms, set_yellow() to Shining Charms, and set_white() to Mystery Charms.

Note that for Shining Charms, the maximum number of slots depends on the fill value.


### ■

```python
p = parameter('first skill',first_SP,'second skill',second_SP,slots,'origin')

search(start_position,count,p)
```

Searches for the specified charm and shows its RNG position.

Enter skill names exactly as written in the 3rd cell. If a skill name is entered incorrectly, you will get an error.

For 'origin', enter 'Melding' for melding or 'Quest' for quests (in Japanese mode these are 'マカ' and '炭鉱'). For other languages, enter an element of `origin` from the 3rd cell.

A loop of 10 million takes about 15 seconds.

A time is shown underneath, but treat it only as a rough guide.

If 'second skill' is '' (an empty string), only charms with no second skill are searched.

```python
p = parameter('Chain Crit',4,'',5,3,'Melding')

search(0,10000,p)
```

Using search_greater instead of search searches ◯ RNG values ahead for charms with the specified first and second skills and at least the specified first SP, second SP and slot count, and shows their RNG positions and the charms.

The "● aim points exist" line and the ◯ and X marks below it show whether there are hit frames. The [◯] or [X] at the right-hand end shows the position of the charm being searched for.

With search_greater, if 'second skill' is '', it searches for charms with the specified first skill and at least the specified first SP and slot count, and shows their RNG positions and the charms.

With search_greater, if 'first skill' is '', it searches for charms with the specified second skill and at least the specified second SP and slot count, and shows their RNG positions and the charms.

### ■

```python
search_fill_slot(start_position,count,fill_value,slots,'origin')
```

Searches for charms with the specified fill value and slot count, and shows their RNG positions and the charms.

For example, search_fill_slot(0,1000000,20,3,'Melding') searches 0 to 1 million for melding charms with both first and second SP at their maximum and 3 slots.


### ■

```python
p = parameter('first skill',first_SP,'second skill',second_SP,slots,'origin')

show_fast(start_position,count,'function_name',p)
```

Searches for charms that meet the specified conditions.

It searches 200 times faster than the search functions. Only the first run starts up a little slowly.

If you enter too large a count, it may not stop.

For 'function_name', enter either 'search' or 'search_greater' to specify the conditions.


### `show_fast_multi(start_position,count,charm1,charm2,charm3,…)`

Searches for charms that meet or exceed the conditions of any of the given charms.

For the trailing arguments you can pass any number (one or more) of charms set up with parameter().

Every charm you specify must have two skills.

Whether it searches melding or quest charms is decided by the first charm argument. In the example below, p1 is 'Melding', so the other charms are also searched as 'Melding'.

It is a little slower than show_fast(), and gets a little slower again as you add charms.

**Example**

```python
p1 = parameter('Sharpness',5,'Tenderizer',5,3,'Melding')
p2 = parameter('Sharpness',5,'Critical Up',5,3,'Melding')
p3 = parameter('Tenderizer',6,'Handicraft',4,3,'Melding')
p4 = parameter('Tenderizer',6,'Sharpness',5,2,'Melding')

show_fast_multi(0,10**7,p1,p2,p3,p4)
```


### `around(◯,□,'origin')`

Shows every charm within □ positions either side of RNG position ◯.

For ◯, enter a charm's RNG position found with search() or similar.


### `jujupush(◯,□)`

Shows the result of Juju Melding at RNG position ◯ with rank □.

If □ is omitted, the result for the highest rank is shown.


### `halcyonpush(◯,□)`

Shows the result of Halcyon Melding at RNG position ◯ with rank □.

If □ is omitted, the result for the highest rank is shown.


### `sequence_charm(◯,□)`

Shows the result of appraising □ charms at once in the quest rewards, starting from RNG position ◯.


### ■

```python
reward_table = {reward table}
reward = 'rewards obtained'

search_reward(start_position, count, luck_threshold, reward, reward_table)
```

Works out the RNG position just before the quest rewards were generated, from the quest rewards you got on a Gathering Tour, and shows it.

Note that generating rewards consumes RNG values; on a Gathering Tour, for example, an extra 5–12 values are consumed depending on the number of rewards. (For 4, 5, 6, 7 or 8 rewards, it consumes 5, 7, 9, 11 or 12.)

If you start a timer at the moment the rewards are generated, the RNG position currently in progress in the game is the frame output by search_reward, plus the frames equivalent to the timer's elapsed time, plus the RNG consumed by reward generation.

In reward_table, enter that quest's reward table.

In reward, enter the item names of the first row of rewards you got from the quest (up to 8 items), as a whitespace-separated string.

For the luck threshold, enter 22 with no luck skill, 25 with Good Luck, 28 with Great Luck, or 31 with Amazing Luck.

If you rewrite reward_table appropriately, you may be able to find the RNG position from other quests' rewards too.

The item names in reward_table can be anything you can recognise, but use the same names in reward_table and reward. Each name must be a single word with no spaces, because reward is split on whitespace.

A count of 100 million takes about 1 second. Only the first run starts up a little slowly.

**Example**

```python
reward_table = {'MysteryBone':20,'Fishing':40,'RawMeat':65,'Whetstone':85,'PowerBait':90,'HeavyBait':95,'SpeedBait':100}
reward = 'PowerBait Fishing RawMeat MysteryBone MysteryBone RawMeat Fishing'

search_reward(0, 10**7, 28, reward, reward_table)
```

(Translator's note: the original uses Japanese shorthand labels: 謎骨, 釣り, 生肉, 砥石, 力餌, 重餌, 速餌. The English labels above are literal renderings, not the in-game English item names. Since the labels are only matched against each other, any consistent names work.)


### ■

```python
combo = 'combination count record'
search_combo(start_position, count, combo)
```

Works out the RNG position when you started combining, from how your ammo count changes as you combine items, and shows that frame plus the RNG advance from combining (number of combinations × 2).

If you start a timer at the moment you start combining, the RNG position currently in progress in the game is the frame output by search_combo plus the frames equivalent to the timer's elapsed time.

For 'combination count record', go to your house in Kokoto Village, with no Felyne room service or Palico, and a 100% combination success rate. Combine Normal S Lv2 repeatedly and enter how many you hold after each combination, as a whitespace-separated string.

It doesn't have to start at 0 and end at 99, but enter the record from beginning to end without gaps.

About 60 combined in total should be enough to identify the position.

If it can't search properly because of irregular RNG consumption, shorten the record or enter the record from a new round of combining.

A count of 100 million takes about 1 second. Only the first run starts up a little slowly.

**Example**

```python
combo = '''
00 03 06 09 11 13 16 18 21 23 25 27 30
32 35 38 41 44 47 50 52 55 58 61 65 69
72 75 78 81 85 88 91 93 97 99'''

search_combo(0, 10**7, combo)
```


### `watch(◯)`

Converts a frame count ◯ to a time.


### `num_of_charms`

When searching for quest reward charms with search_greater or similar, the hit frames shown are for appraising this many charms of the same type at once in the quest rewards.


### `showallrank`

When searching Timeworn or Shining Charms for melding, if this is True, hit frames for every rank are shown. If False, only hit frames for the highest rank are shown.


### `showrare`

If True, the charm's rarity is shown; if False, it is hidden.
