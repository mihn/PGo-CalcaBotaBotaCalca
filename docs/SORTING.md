# Sorting Table

**This is the order in which Pokemon displays pokémons when sorting by A-Z.** Useful for working out a custom order you'd like to view your pokémons, by using these characters at the beginning of the `rename:` action.

>_For Gboard users, the character in parenthesis indicates which key on Gboard contains the character in question (with tap&hold)._

>_For very advanced users, **like the ones who would adventure themselves into [modular-config](./config-examples/modular-config/)**, check out [True character length](#True%20character%20length) section below._

- `꩜ ` _(Special @. Not available on Gboard)_
- `!`
- `#`
- `$`
- `%`
- `&`
- `*`
- `@`
- `,`
- `.`
- `?`
- `^`
- `_`
- `¡` _(Inside key `!`)_
- `¿` _(Inside key `?`)_
- `“` _(Inside key `"`)_
- `›` _(Inside key `'`)_
- `‽` _(Inside key `?`)_
- `+`
- `⁺` _(Superscript Plus. Not available on Gboard)_
- `=`
- `±`
- `»` _(Inside key `"`)_
- `§` _(Inside key `¶`)
- `¶`
- `÷`
- `×`
- `∅` _(Inside key `0`)_
- `√`
- `≈` _(Inside key `=`)_
- `↑` _(Inside key `^`)_
- `→` _(Inside key `^`)_
- `↓` _(Inside key `^`)_
- `←` _(Inside key `^`)_
- `⇆` _(Double Arrow. Not available on Gboard)_
- `μ` _(Inside key `π`)_ **[B] Needs Confirmation!**
- `®`
- `·` _(Inside key `-`)_
- `†` _(Inside key `*`)_
- `‡` _(Inside key `*`)_
- `•`
- `‰`
- `☀️` _(It's a sun emoji)_
- `★` _(Inside key `*`)_
- `♠` _(Inside key `•`)_
- `♣` _(Inside key `•`)_
- `♥` _(Inside key `•`)_
- `♦` _(Inside key `•`)_
- `♪` _(Inside key `•`)_
- `✂️` (Emoji)
- `✓`
- `€`
- `∞` _(Inside key `=`)_ **[B] Needs Confirmation!**
- Numbers
- `∞` _(Inside key `=`)_ **[A] Needs Confirmation!**
- Letters
- `μ` _(Inside key `π`)_ **[A] Needs Confirmation!**
- `Π` _(Inside key `π`)_
- `π`
- `Ω` _(Inside key `π`)_

___

### Per device differences


**TODO: Confirm if this is still an issue.**

**Characters above with `[A]` or similar at the end means that the order changes depending on the device. Yeah...**
The letter between the brackets is the device's "type" _(more like mood)_, so if your phone follows pattern [A], you should disregard characters labeled as [B].

---

## True character length

**If you _used_ to get lots of _Please choose another pokemon name_ when renaming, that means that some of your symbols are too big, and the string is exceeding 12 characters.** Though it might look like the name is 12-characters long, some characters are actually composed of several unicode elements (like Emojis, for example, which are usually a combination of three separate characters), making them bigger than they appear, and thus making PoGo think you're trying to set a too big of a name.

PoGo-CalcaBotaBotaCalca deals with this by doing several tricks if the character name's going to exceed 12 characters:

    -


**Below follows a list with each character *true length* from the list above.**

_Keep in mind that 0.5 doesn't mean you can have 24 characters that long, but when counting the whole string it does apply (i.e.: you can't have 24 letters-long name if PoGo's counting is higher than 12 chars.)._

- `꩜ : 2.0`
- `!: 0.5`
- `#: 0.5`
- `$: 0.5`
- `%: 0.5`
- `&: 0.5`
- `*: 0.5`
- `@: 0.5`
- `,: 0.5`
- `.: 0.5`
- `?: 0.5`
- `^: 0.5`
- `_: 0.5`
- `¡: 1.0`
- `¿: 1.0`
- `“: 1.5`
- `›: 1.5`
- `‽: 1.5`
- `+: 0.5`
- `⁺: 1.5`
- `=: 0.5`
- `±: 1.0`
- `»: 1.0`
- `§: 1.0`
- `¶: 1.0`
- `÷: 1.0`
- `×: 1.0`
- `∅: 1.5`
- `√: 1.5`
- `≈: 1.5`
- `↑: 1.5`
- `→: 1.5`
- `↓: 1.5`
- `←: 1.5`
- `⇆: 1.5`
- `μ: 1.0`
- `·: 1.0`
- `†: 1.5`
- `‡: 1.5`
- `•: 1.5`
- `‰: 1.5`
- `☀️: 3.0`
- `★: 1.5`
- `♠: 1.5`
- `♣: 1.5`
- `♥: 1.5`
- `♦: 1.5`
- `✂️: 3.0`
- `✓: 1.5`
- `€: 1.5`
- `∞: 1.5`
- `Numbers: 0.5`
- `∞: 1.5`
- `Letters: 0.5`
- `Π: 1.0`
- `π: 1.0`
- `Ω: 1.0`
