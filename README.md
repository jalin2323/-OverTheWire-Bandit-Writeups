# OverTheWire: Bandit Writeups
Writeups for OverTheWire Bandit levels 0-3

## Level 0 -> Level 1
**Goal:** Find the password in a file called `readme`.
- **Command Used:** `cat readme`
- **Output:**  password retrieved successfully
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

## Level 3 -> Level 4
**Goal:** Find the password in a hidden file inside the inhere directory.
- **Command Used:** ls -a inhere/ and cat inhere/.hidden
- **Output:** Password retrieved successfully
- **Concept:** Files starting with a dot (.) are hidden in Linux. Using ls -a lists all files including hidden ones, allowing access to the password file.

## Level 4 -> Level 5
**Goal:** Find the password in the only human-readable file inside the inhere directory.
- **Command Used:** file ./* and cat ./-file07
- **Output:** Password retrieved successfully
- **Concept:** The file command helps identify file types. Since filenames start with -, the ./ prefix is used to prevent the shell from misinterpreting the filename as a command option.

## Level 5 -> Level 6
**Goal:** Find the password in a file that is human-readable, exactly 1033 bytes, and not executable.
- **Command Used:** find . -type f -size 1033c ! -executable
- **Output:** Password retrieved successfully
- **Concept:** The find command is used with size and permission filters (-size and ! -executable) to accurately locate the required file among many directories.

## Level 6 -> Level 7
**Goal:** Find the password stored in a file owned by user bandit7, group bandit6, and of size 33 bytes.
- **Command Used:** find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
- **Output:** Password retrieved successfully
- **Concept:** Searching from the root directory with ownership and size conditions helps locate restricted files. Error messages are suppressed using 2>/dev/null to keep the output clean.

## Level 7 -> Level 8
**Goal:** Find the password inside data.txt next to the word millionth.
- **Command Used:** grep millionth data.txt
- **Output:** Password retrieved successfully
- **Concept:** The grep command searches for specific text patterns within a file, making it efficient to isolate the password line in large datasets.
