# Rust
---
title: Rust

updated: 2021-11-30

keywords:
  - Variables
  - Functions
  - Interpolation
  - Brace expansions
  - Loops
  - Conditional execution
  - Command substitution
---

Getting started
---------------
Rust input is interpreted as a sequence of Unicode code points encoded in UTF-8.

### Introduction
This is a quick reference to getting started with Rust.

- [Learn Rust in hours](https://doc.rust-lang.org/stable/reference/introduction.html)_

### Notations

```<img width="762" alt="Screen Shot 2021-11-29 at 9 35 33 PM" src="https://user-images.githubusercontent.com/95258457/144323345-bcc464ef-b944-4a5f-ba2d-cec2b66da198.png">
```

### Variables

```bash
NAME="John"
echo $NAME
echo "$NAME"
echo "${NAME}!"
```

### String quotes

```bash
NAME="John"
echo "Hi $NAME"  #=> Hi John
echo 'Hi $NAME'  #=> Hi $NAME
```

### Shell execution

```bash
echo "I'm in $(pwd)"
echo "I'm in `pwd`"
# Same
```

See [Command substitution](http://wiki.bash-hackers.org/syntax/expansion/cmdsubst)

### Conditional execution

```bash
git commit && git push
git commit || echo "Commit failed"
```

### Functions
{: id='functions-example'}

```bash
get_name() {
  echo "John"
}

echo "You are $(get_name)"
```

See: [Functions](#functions)

### Conditionals
{: id='conditionals-example'}

```bash
if [[ -z "$string" ]]; then
  echo "String is empty"
elif [[ -n "$string" ]]; then
  echo "String is not empty"
fi
```

See: [Conditionals](#conditionals)

### Strict mode

```bash
set -euo pipefail
IFS=$'\n\t'
```

See: [Unofficial bash strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/)

### Brace expansion

```bash
echo {A,B}.js
```

| Expression | Description         |
| ---------- | ------------------- |
| `{A,B}`    | Same as `A B`       |
| `{A,B}.js` | Same as `A.js B.js` |
| `{1..5}`   | Same as `1 2 3 4 5` |

See: [Brace expansion](http://wiki.bash-hackers.org/syntax/expansion/brace)


Parameter expansions
--------------------
{: .-three-column}

### Basics

```bash
name="John"
echo ${name}
echo ${name/J/j}    #=> "john" (substitution)
echo ${name:0:2}    #=> "Jo" (slicing)
echo ${name::2}     #=> "Jo" (slicing)
echo ${name::-1}    #=> "Joh" (slicing)
echo ${name:(-1)}   #=> "n" (slicing from right)
echo ${name:(-2):1} #=> "h" (slicing from right)
echo ${food:-Cake}  #=> $food or "Cake"
```

```bash
length=2
echo ${name:0:length}  #=> "Jo"
```

See: [Parameter expansion](http://wiki.bash-hackers.org/syntax/pe)

```bash
STR="/path/to/foo.cpp"
echo ${STR%.cpp}    # /path/to/foo
echo ${STR%.cpp}.o  # /path/to/foo.o
echo ${STR%/*}      # /path/to

echo ${STR##*.}     # cpp (extension)
echo ${STR##*/}     # foo.cpp (basepath)

echo ${STR#*/}      # path/to/foo.cpp
echo ${STR##*/}     # foo.cpp

echo ${STR/foo/bar} # /path/to/bar.cpp
```

```bash
STR="Hello world"
echo ${STR:6:5}   # "world"
echo ${STR: -5:5}  # "world"
```

```bash
SRC="/path/to/foo.cpp"
BASE=${SRC##*/}   #=> "foo.cpp" (basepath)
DIR=${SRC%$BASE}  #=> "/path/to/" (dirpath)
```

### Substitution

| Code              | Description         |
| ----------------- | ------------------- |
| `${FOO%suffix}`   | Remove suffix       |
| `${FOO#prefix}`   | Remove prefix       |
| ---               | ---                 |
| `${FOO%%suffix}`  | Remove long suffix  |
| `${FOO##prefix}`  | Remove long prefix  |
| ---               | ---                 |
| `${FOO/from/to}`  | Replace first match |
| `${FOO//from/to}` | Replace all         |
| ---               | ---                 |
| `${FOO/%from/to}` | Replace suffix      |
| `${FOO/#from/to}` | Replace prefix      |

### Comments

```bash
# Single line comment
```

```bash
: '
This is a
multi line
comment
'
```

### Substrings

| Expression      | Description                    |
| --------------- | ------------------------------ |
| `${FOO:0:3}`    | Substring _(position, length)_ |
| `${FOO:(-3):3}` | Substring from the right       |

### Length

| Expression | Description      |
| ---------- | ---------------- |
| `${#FOO}`  | Length of `$FOO` |

### Manipulation

```bash
STR="HELLO WORLD!"
echo ${STR,}   #=> "hELLO WORLD!" (lowercase 1st letter)
echo ${STR,,}  #=> "hello world!" (all lowercase)

STR="hello world!"
echo ${STR^}   #=> "Hello world!" (uppercase 1st letter)
echo ${STR^^}  #=> "HELLO WORLD!" (all uppercase)
```
