# OverTheWire: Bandit Writeups
Writeups for OverTheWire Bandit levels 0-3

## Level 0 -> Level 1
**Goal:** Find the password in a file called `readme`.
- **Command Used:** `cat readme`
- **Output:** > The password you are looking for is: password retrieved successfully
- **Concept:** Logged in as `bandit0` and used the `cat` command to read the text file in the home directory.

## Level 1 -> Level 2
**Goal:** Find the password in a file named `-`.
- **Command Used:** `cat ./-`
- **Output:**  password retrieved successfully
- **Concept:** The dash `-` is a special character in Linux that often represents "standard input." To read it as a filename, you must use the relative path `./-`.

## Level 2 -> Level 3
**Goal:** Find the password in a file called `spaces in this filename`.
- **Command:** cat ./--spaces\ in\ this\ filename-- or cat ./--spaces in this filename--
- **Output:**  password retrieved successfully
- **Concept:**  Filenames starting with `--` are treated as command options.
Using `./` forces Linux to treat it as a file.
