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

## Level 8 -> Level 9
**Goal:** Find the password in data.txt, which is the only line of text that occurs exactly once.
- **Command Used:** sort data.txt | uniq -u
- **Output:** Password retrieved successfully
- **Concept:** The sort command organizes the data, and uniq -u filters out any lines that have duplicates, leaving only the unique password.

## Level 9 -> Level 10
**Goal:** Find the password among human-readable strings, preceded by = characters, in data.txt.
- **Command Used:** strings data.txt | grep "=="
- **Output:** Password retrieved successfully
- **Concept:** The strings command finds printable sequences in binary files, while grep filters for the specific visual markers (=) described in the goal.

## Level 10 -> Level 11
**Goal:** Decode the password which is Base64 encoded in data.txt.
- **Command Used:** base64 -d data.txt
- **Output:** Password retrieved successfully
- **Concept:** Base64 is a binary-to-text encoding scheme. The -d flag reverses this process to reveal the original password.

## Level 11 -> Level 12
**Goal:** Decode the password which is encoded using ROT13.
- **Command Used:** cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
- **Output:** Password retrieved successfully
- **Concept:** ROT13 is a simple substitution cipher. The tr (translate) command is used to shift every letter 13 places forward in the alphabet.

## Level 12 -> Level 13
**Goal:** Extract the password from a repeatedly compressed file (data.txt).
- **Command Used:** xxd -r data.txt > data; file data; (repeat decompression)
- **Output:** Password retrieved successfully
- **Concept:** This involves "reverse engineering" a hex dump using xxd, identifying the file type with file, and using the corresponding decompression tool (gzip, bzip2, tar).

## Level 13 -> Level 14
**Goal:** Use the SSH private key to log in as bandit14.
- **Command Used:** ssh -i sshkey.private bandit14@localhost -p 2220
- **Output:** Password retrieved successfully
- **Concept:** Private keys are used for passwordless authentication. The -i flag specifies the identity file (private key) used to prove your identity to the server.

## Level 14 -> Level 15
**Goal:** Retrieve the password by submitting the current password to port 30000 on localhost.
- **Command Used:** nc localhost 30000
- **Output:** Password retrieved successfully
- **Concept:** Netcat (nc) is used to read from and write to network connections. Sending the correct string to a specific port triggers the server to return the next password.

## Level 15 -> Level 16
**Goal:** Retrieve the password using SSL encryption on port 30001.
- **Command Used:** openssl s_client -connect localhost:30001
- **Output:** Password retrieved successfully
- **Concept:** Unlike raw ports, SSL/TLS ports require a secure handshake. openssl s_client establishes this encrypted tunnel so you can communicate safely.

## Level 16 -> Level 17
**Goal:** Find the correct SSL service and retrieve the password for the next level.
- **Command Used:** nmap -sV localhost -p 31000-32000; openssl s_client -connect localhost:[port]
- **Output:** Private SSH key retrieved
- **Concept:** Port scanning with nmap identifies which ports are listening. Connecting to the correct SSL-enabled service allows you to submit the current password and receive an RSA private key.

## Level 17 -> Level 18
**Goal:** Find the password by comparing two files passwords.old and passwords.new.
- **Command Used:** diff passwords.old passwords.new
- **Output:** Password retrieved successfully
- **Concept:** The diff command compares files line by line. In this level, it isolates the single line that was changed between the old and new versions.

## Level 18 -> Level 19
**Goal:** Retrieve the password despite being logged out immediately after login.
- **Command Used:** ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
- **Output:** Password retrieved successfully
- **Concept:** By appending a command to the end of an SSH login string, you can execute that command (like cat) on the remote server before the login shell (which is modified to exit) closes the session.

## Level 19 -> Level 20
**Goal:** Use the SUID binary to read the password.
- **Command Used:** ./bandit20-do cat /etc/bandit_pass/bandit20
- **Output:** Password retrieved successfully
- **Concept:** SUID (Set-user Identification) allows a user to execute a binary with the permissions of the file owner. Using the provided binary allows you to read the bandit20 password file which is otherwise restricted.

## Level 20 -> Level 21
**Goal:** Use a network service that requires sending the current password.
- **Command Used:** nc -l -p [port] <<< "current_password" & ./suconnect [port]
- **Output:** Password retrieved successfully
- **Concept:** This level requires establishing a local listener (nc) that sends the current password when the SUID binary (suconnect) connects to it, creating a "handshake" to release the next password.

## Level 21 -> Level 22
**Goal:** Find the password from a cron job script.
- **Command Used:** ls /etc/cron.d/; cat /usr/bin/cronjob_bandit22.sh; cat /tmp/[filename]
- **Output:** Password retrieved successfully
- **Concept:** Cron jobs are scheduled tasks. By reading the cron configuration and the associated shell script, you can find the location where the script automatically saves the password.

## Level 22 -> Level 23
**Goal:** Find the password generated dynamically by a cron job.
- **Command Used:** cat /usr/bin/cronjob_bandit23.sh; (echo I am user bandit23 | md5sum)
- **Output:** Password retrieved successfully
- **Concept:** This level involves reverse-engineering a script that uses a mathematical function (like md5sum) to create a unique filename in /tmp/ based on the username.

## Level 23 -> Level 24
**Goal:** Exploit a writable cron job directory to retrieve the password.
- **Command Used:** echo "cat /etc/bandit_pass/bandit24 > /tmp/my_pass" > /var/spool/bandit24/foo.sh; chmod 777 /var/spool/bandit24/foo.sh
- **Output:** Password retrieved successfully
- **Concept:** If a cron job executes every file in a directory, you can drop a custom script into that directory to perform actions (like reading a password) with the cron user's higher privileges.

## Level 24 -> Level 25
**Goal:** Brute-force the 4-digit PIN to retrieve the password.
- **Command Used:** for i in {0000..9999}; do echo "password $i"; done | nc localhost 30002
- **Output:** Password retrieved successfully
- **Concept:** Shell scripting can automate the process of trying every possible combination (0000-9999). Piping this list into netcat allows you to brute-force a network service efficiently.



