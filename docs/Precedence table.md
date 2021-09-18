---
layout: default
title: Precedence Table
permalink: precedence
nav_order: 7
---

# Precedence table

For descriptions of each operator, see the [operator list](operators). For guaranteed up-to-date information, your best bet is to read the code: there's a reasonably human-readable precedence table in [operators.py](https://github.com/dloscutoff/pip/blob/master/operators.py).

### Terminology

- **Chaining** associativity means multiple comparisons can be strung together. For example, `x<y=z` isn't equivalent to either `(x<y)=z` (left-associative) or `x<(y=z)` (right-associative) but rather to `(x<y)&(y=z)`.
- **Fold default** is the value returned when folding an empty iterable on this operator. For example, `$+[]` returns `0`, while `$*[]` returns `1`.
- **Itemwise** indicates whether the operator applies item-by-item to lists, both lists and ranges, or neither.
- **In lambda** indicates whether the operator can be applied to functions (typically starting from the identity function `_`) to build bigger functions.

Category | Arity | Associativity | Symbol | Name | Fold default | Itemwise? | In lambda?
-------- | ----- | ------------- | ------ | ---- | ------------ | --------- | ----------
Output and yank operators | Unary | – | `O` <br> `P` <br> `Y` <br> `YO` <br> `YP` | Output <br> Print <br> Yank <br> Yankoutput <br> Yankprint | None <br> None <br> None <br> None <br> None | No <br> No <br> No <br> No <br> No | No <br> No <br> No <br> No <br> No
Assignment | Binary | Right | `:` <br> `::` | Assign <br> Swap | None <br> None | No <br> No | No <br> No
If-then-else | Ternary | Right | `?` | Ifte | None | No | No
Logical or | Binary | Left | `|` | Or | `0` | No | No
Logical and | Binary | Left | `&` | And | `1` | No | No
Logical not | Unary | – | `!` | Not | None | No | No
Exact equality | Binary | Left | `==` | Objequal | `1` | No | No
Recursion | Unary | – | `RE` | Recurse | None | No | No
Map and other function operators | Binary | Right | `M` <br> `MC` <br> `ME` <br> `MJ` <br> `MM` <br> `MP` <br> `MS` <br> `MU` <br> `FI` <br> `SK` <br> `V` | Map <br> Mapcoords <br> Mapenumerate <br> Mapjoin <br> Mapmap <br> Mappairs <br> Mapsum <br> Mapunpack <br> Filter <br> Sortkeyed <br> Eval | `[]` <br> `[]` <br> `[]` <br> `""` <br> `[]` <br> `[]` <br> `0` <br> `[]` <br> `[]` <br> `[]` <br> None | No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No | No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No
Ternary map | Ternary | Right | `MR` <br> `MZ` | Mapregex <br> Mapzip | `[]` <br> `[]` | No <br> No | No <br> No
Function operators | Unary | – | `V` <br> `FI` | Eval <br> Filter | None <br> None | No <br> No | No <br> No
Lambda-usable if-then-else | Ternary | Right | `\?` | Ifte | None | No | Yes
Lambda-usable or | Binary | Left | `\|` | Or | `0` | No | Yes
Lambda-usable and | Binary | Left | `\&` | And | `1` | No | Yes
Lambda-usable not | Unary | – | `\!` | Not | None | No | Yes
Comparison operators | Binary | Chaining | `<` <br> `>` <br> `=` <br> `<=` <br> `>=` <br> `!=` <br> `LT` <br> `GT` <br> `Q` <br> `LE` <br> `GE` <br> `NE` <br> `#=` <br> `#<` <br> `#>` <br> `~=` | Numless <br> Numgreater <br> Numequal <br> Numlesseq <br> Numgreatereq <br> Numnotequal <br> Strless <br> Strgreater <br> Strequal <br> Strlesseq <br> Strgreatereq <br> Strnotequal <br> Lenequal <br> Lenless <br> Lengreater <br> Fullmatch | `1` <br> `1` <br> `1` <br> `1` <br> `1` <br> `1` <br> `1` <br> `1` <br> `1` <br> `1` <br> `1` <br> `1` <br> `1` <br> `1` <br> `1` <br> `1` | No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No | Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes
In and not in | Binary | Left | `N` <br> `NI` | In <br> Notin | None <br> None | No <br> No | Yes <br> Yes
String conversion | Unary | – | `RP` <br> `ST` | Repr <br> Str | None <br> None | No <br> No | No <br> No
Low-precedence list operators | Binary | Left | `CB` | Combinations | `[]` | No | Yes
Low-precedence list operators | Unary | – | `MX` <br> `MN` <br> `RC` <br> `SN` <br> `SS` <br> `UQ` <br> `EN` <br> `PM` | Max <br> Min <br> Randchoice <br> Sortnum <br> Sortstring <br> Unique <br> Enumerate <br> Permutations | None <br> None <br> None <br> None <br> None <br> None <br> None <br> None | No <br> No <br> No <br> No <br> No <br> No <br> No <br> No | Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes
Append and push | Binary | Left | `AE` <br> `AL` <br> `PE` <br> `PU` <br> `PB` <br> `PK` | Appendelem <br> Appendlist <br> Prependelem <br> Push <br> Pushback <br> Pick | `[]` <br> `[]` <br> `[]` <br> `[]` <br> `[]` <br> `[]` | No <br> No <br> No <br> No <br> No <br> No | Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes
Pop and dequeue | Unary | – | `PO` <br> `DQ` | Pop <br> Dequeue | None <br> None | No <br> No | Yes <br> Yes
High-precedence list operators | Binary | Left | `^` <br> `^@` <br> `@?` <br> `@*` <br> `<>` <br> `J` <br> `JW` <br> `RL` <br> `Z` <br> `ZD` <br> `H` <br> `S` <br> `WV` <br> `UW` <br> `CP` <br> `CG` <br> `ZG` <br> `OG` <br> `TD` <br> `FD` | Split <br> Splitat <br> Find <br> Findall <br> Group <br> Join <br> Joinwrap <br> Repeatlist <br> Zip <br> Zipdefault <br> Prefix <br> Suffix <br> Weave <br> Unweave <br> Cartesianproduct <br> Coordinategrid <br> Zerogrid <br> Onegrid <br> Todigits <br> Fromdigits | `[]` <br> `[]` <br> None <br> `[]` <br> `[]` <br> `""` <br> None <br> `[]` <br> `[]` <br> `[]` <br> `[]` <br> `[]` <br> `[]` <br> `[]` <br> `[]` <br> None <br> None <br> None <br> `[]` <br> `0` | Both <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> Both <br> Both <br> Both <br> No <br> No | Yes <br> Yes <br> Yes <br> Yes <br> <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes
Replace-like operators | Ternary | Left | `RA` <br> `TR` | Replaceat <br> Transliterate | None <br> None | No <br> No | Yes <br> Yes
High-precedence list operators | Unary | – | `^` <br> `<>` <br> `J` <br> `R`/`RV` <br> `RF` <br> `PZ` <br> `QR` <br> `QP` <br> `Z` <br> `ZD` <br> `H` <br> `S` <br> `WV` <br> `UW` <br> `CP` <br> `CG` <br> `ZG` <br> `OG` <br> `EY` <br> `TD` <br> `FD` | Split <br> Group <br> Join <br> Reverse <br> Reflect <br> Palindromize <br> Quadreflect <br> Quadpalindromize <br> Zip <br> Zipdefault <br> Prefix <br> Suffix <br> Weave <br> Unweave <br> Cartesianproduct <br> Coordinategrid <br> Zerogrid <br> Onegrid <br> Identitymatrix <br> Todigits <br> Fromdigits | None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None | Both <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> No <br> Both <br> Both <br> Both <br> Both <br> No <br> No | Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes
Replace | Ternary | Left | `R` | Replace | None | No | No
Low-precedence string/regex operators | Binary | Left | `WR` <br> `~` | Wrap <br> Firstmatch | `""` <br> `""` | Yes <br> Yes | Yes <br> Yes
Concatenate | Binary | Left | `.` | Cat | `""` | Both | Yes
Regex modifiers | Unary | – | `X` <br> `.` <br> `K` | Regex <br> Dot <br> Kleenestar | None <br> None <br> None | No <br> List <br> List | Yes <br> Yes <br> Yes
Remove | Binary | Left | `RM` <br> `DC` | Remove <br> Deletechars | `""` <br> `""` | No <br> Both | Yes <br> Yes
String repetition | Binary | Left | `X` | Strmul | `""` | Both | Yes
Strip and trim | Binary | Left | `||` <br> `|>` <br> `<|` <br> `TM` | Strip <br> Lstrip <br> Rstrip <br> Trim | `""` <br> `""` <br> `""` <br> `""` | List <br> List <br> List <br> List | Yes <br> Yes <br> Yes <br> Yes
Strip and trim | Unary | – | `||` <br> `|>` <br> `<|` <br> `TM` <br> `LC` <br> `UC` <br> `SC` | Strip <br> Lstrip <br> Rstrip <br> Trim <br> Lowercase <br> Uppercase <br> Swapcase | None <br> None <br> None <br> None <br> None <br> None <br> None | List <br> List <br> List <br> List <br> List <br> List <br> List | Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes
Range and to-base | Binary | Left | `,` <br> `\,` <br> `RR` <br> `TB` | Range <br> Inclrange <br> Randrange <br> Tobase | None <br> None <br> `0` <br> `0` | Both <br> Both <br> Both <br> Both | Yes <br> Yes <br> Yes <br> Yes
Range and to-base | Unary | – | `,` <br> `\,` <br> `RR` <br> `TB` | Rangeto <br> Inclrangeto <br> Randrangeto <br> Tobase | None <br> None <br> None <br> None | Both <br> Both <br> Both <br> Both | Yes <br> Yes <br> Yes <br> Yes
Low-precedence numeric operators | Binary | Left | `BA` <br> `BO` <br> `BX` <br> `AT` <br> `CM` | Bitwiseand <br> Bitwiseor <br> Bitwisexor <br> Arctan <br> Numcmp | `-1` <br> `0` <br> `0` <br> None <br> `0` | Both <br> Both <br> Both <br> Both <br> No | Yes <br> Yes <br> Yes <br> Yes <br> Yes
Low-precedence numeric operators | Unary | – | `BN` | Bitwisenot | None | Both | Yes
Addition and subtraction | Binary | Left | `+` <br> `-` <br> `AD` | Add <br> Sub <br> Absolutediff | `0` <br> `0` <br> `0` | List <br> List <br> Both | Yes <br> Yes <br> Yes
Multiplication and division | Binary | Left | `*` <br> `/` <br> `%` <br> `//` | Mul <br> Div <br> Mod <br> Intdiv | `1` <br> `1` <br> `0` <br> `1` | Both <br> Both <br> Both <br> Both | Yes <br> Yes <br> Yes <br> Yes
Unary arithmetic operators | Unary | – | `+` <br> `-` <br> `/` <br> `%` | Pos <br> Neg <br> Invert <br> Mod2 | None <br> None <br> None <br> None | List <br> Both <br> Both <br> Both | Yes <br> Yes <br> Yes <br> Yes
Exponentiation | Binary | Right | `E`/`**` <br> `EE` <br> `RT` | Pow <br> Poweroften <br> Root | `1` <br> `1` <br> `1` | Both <br> Both <br> Both | Yes <br> Yes <br> Yes
High-precedence numeric operators | Unary | – | `E`/`**` <br> `EE` <br> `RT` <br> `SQ` <br> `HV` <br> `DB` <br> `SI` <br> `CO` <br> `TA` <br> `SE` <br> `CS` <br> `CT` <br> `AT` <br> `RD` <br> `DG` <br> `EX` <br> `LN` | Pow <br> Poweroften <br> Sqrt <br> Square <br> Halve <br> Double <br> Sine <br> Cosine <br> Tangent <br> Secant <br> Cosec <br> Cotan <br> Arctan <br> Radians <br> Degrees <br> Exponential <br> Naturallog | None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None <br> None | Both <br> Both <br> Both <br> Both <br> Both <br> Both <br> Both <br> Both <br> Both <br> Both <br> Both <br> Both <br> Both <br> Both <br> Both <br> Both <br> Both | Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes
Very high-precedence operators | Binary | Left | `FB` | Frombase | `0` | Both | Yes
Very high-precedence operators | Unary | – | `U` <br> `D` <br> `#` <br> `A` <br> `C` <br> `AB` <br> `SG` <br> `FB` | Inc <br> Dec <br> Len <br> Asc <br> Chr <br> Abs <br> Sign <br> Frombase | None <br> None <br> None <br> None <br> None <br> None <br> None <br> None | List <br> List <br> No <br> Both <br> Both <br> Both <br> Both <br> Both | Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes <br> Yes
Highest-precedence operators | Binary | Left | `@` <br> `@<` <br> `@>` | At <br> Leftof <br> Rightof | None <br> None <br> None | No <br> No <br> No | Yes <br> Yes <br> Yes
Highest-precedence operators | Unary | – | `@` <br> `@<` <br> `@>` <br> `++` <br> `--` | At <br> Leftof <br> Rightof <br> Inc <br> Dec | None <br> None <br> None <br> None <br> None | No <br> No <br> No <br> List <br> List | Yes <br> Yes <br> Yes <br> Yes <br> Yes
