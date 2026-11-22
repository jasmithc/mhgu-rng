This page describes how Halcyon Melding and Juju Melding decide how many charms you get, and of which types.

Consider the following function:

Take the given value modulo 65536 as the initial value.

If the current value is 0, set it to 1; then the next value is the current value × 176 modulo 65363.

With a as the given value and b as the number of times the value is advanced, write the function's value as rand(a,b).



**Halcyon Melding**

① Let w be the current RNG value.

rand(w,1) modulo [charm count range], plus [minimum charm count], is the number of charms produced.

(These values depend on the rank inserted. At the highest rank they are 5 and 2.)

② If rand(w,2) modulo 100 is less than 10, the first charm is a Mystery Charm; less than 55, a Shining Charm; less than 85, a Timeworn Charm.

If it is 85 or more, calculate rand(w,3) and check again in the same way to decide the first charm's type. Keep advancing the ◯ in rand(w,◯) and repeating until the value is below 85.

③ Advance the ◯ in rand(w,◯) by 1 from where it last stopped, and decide the second charm's type in the same way as ②.

④ Repeat until every charm's type has been decided.

⑤ Advance the RNG by one. Following the results up to ④, appraise the charms one after another.



**Juju Melding**

① Let w be the current RNG value.

rand(w,1) modulo [Enduring Charm count range], plus [minimum Enduring Charm count], is the number of Enduring Charms produced.

rand(w,2) modulo [Timeworn Charm count range], plus [minimum Timeworn Charm count], is the number of Timeworn Charms produced.

② Advance the RNG by one. Following the results from ①, appraise the charms one after another: Enduring Charms first, then Timeworn Charms.
