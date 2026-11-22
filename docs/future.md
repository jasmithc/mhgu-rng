When calculating the fill value, if a quotient has the form s/t (s and t integers, t not a power of 2) and the result comes out to exactly an integer, the 3DS's floating-point error might make the actual in-game value 1 less than that integer.

If the result is anything other than 5, 10 or 15, this may have no effect.

(Think of something like 50/6 + 60/9 = 14.999999999 → 14.)

(Apparently earlier games had patterns where the fill value calculation didn't match like this. Also, examples of this error showing up in damage calculations and similar have been confirmed in XX.)

No such case has been confirmed so far, but if such a pattern exists and the rule behind the error can be found, I plan to fix it.

---

If I could build in a feature like Gansimu (頑シミュ, an armor-set skill simulator) that searches for the list of charms needed for the skills you want, then combined with show_fast_multi() it might be possible to implement a feature where you enter the skills you want and it shows the RNG positions of charms that satisfy them.
