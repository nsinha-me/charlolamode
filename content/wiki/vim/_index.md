---
Title: Vim
type: list
---


Vim is a highly configurable text editor built to make creating and changing any kind of text very efficient.



### To remove the last word from each line -
```
:%s/\s*\w\+\s*$//
```
This tells it to find optional whitespace, followed by one or more word characters, followed by optional whitespace, followed by end of line—then replace it with nothing.

Before:
```
abcdef 123
xyz 1256
qwert 2
asdf 159
```

After:
```
abcdef
xyz
qwert
asdf
```

### Delete everything after every a specified word -

With substitutions you can do many things (see :help substitute). One is that you can remember the first word with a capture group by enclosing that part with \( and \), matching the rest of the line (but not remembering it) and then replacing the line with the remembered group using \1

```
:%s/\(fruit\).*$/\1/
```

Before:
```
fruit banana
fruit apple
fruit grape
planet jupiter
planet mars
planet saturn
```

After:
```
fruit
fruit
fruit
planet jupiter
planet mars
planet saturn
```
