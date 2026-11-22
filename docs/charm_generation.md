This is basically almost the same as MH3G (Monster Hunter 3 Ultimate).

However, it differs in the following 3 ways:

- The RNG used

- The initial RNG state

- How many RNG values melding consumes


These are explained in the next section.


The way a charm is generated is described below.

---

① Advance the RNG by one.

Let ◯ be the RNG value modulo the number of skills that can be a first skill. Of the skills that can be a first skill, sorted by ID, the (◯+1)th one becomes the first skill.

② Advance the RNG by one.

The RNG value modulo the first skill's (maximum − minimum + 1), plus the minimum, becomes the first skill's skill points.

③ Advance the RNG by one.

If the RNG value modulo 100 is X or more, a second skill is added.
If it is less than X, no second skill is added. Jump to ⑦.

(X depends on the charm type. For an Enduring Charm, X is 15.)

④ Advance the RNG by one.

Let ◯ be the RNG value modulo the number of skills that can be a second skill. Of the skills that can be a second skill, sorted by ID, the (◯+1)th one becomes the second skill.

For melding, jump to ⑥.

⑤ Advance the RNG by one.

If the RNG value modulo 2 is 1, the second skill's value is positive.

If it is 0, it is negative. 

⑥ Advance the RNG by one.

- If ⑤ decided positive, or for melding:

The RNG value modulo the second skill's maximum, plus 1, becomes the second skill's skill points.

- If ⑤ decided negative:

Let −A be the second skill's negative lower limit.

The RNG value modulo (A + 1), minus A, becomes the second skill's skill points.

If the first and second skills are the same, or the second skill comes out as negative 0, the charm is treated as having no second skill.

⑦ Advance the RNG by one.

Determine the "fill value", which measures how high the skill points are.

Let S1 be the first skill's maximum and S2 the second skill's maximum.

Let T1 be the first skill's value and T2 the second skill's value decided above.

T1 ÷ S1 × 10 + T2 ÷ S2 × 10

Compute the sum, then drop the fractional part; the result is the "fill value".

However, if there is no second skill, the first and second skills are the same, or the second skill is negative, T2 is taken as 0 here.

The RNG value modulo 100 is the roll value.

For each fill value from 2 to 20 there is a table mapping roll values to slot counts; look it up to decide the number of slots.

For example, with a fill value of 17 and a roll value of 92: the table for fill value 17 is (79,91,98), and the roll is at least 91 but below 98, so the charm gets 2 slots.

---

That completes the charm.

If more charms remain, go back to ① and generate the next charm straight away.
