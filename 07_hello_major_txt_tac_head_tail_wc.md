# Q: Create hello.txt (also major.txt) with 7 lines; reverse, head, tail, wc

## a. Create file with 7 lines
```bash
cat > hello.txt <<'EOT'
Line 1: Linux is open source
Line 2: Red Hat is an enterprise distribution
Line 3: Kernel is the core of the OS
Line 4: Shell is the command interpreter
Line 5: Everything in Linux is a file
Line 6: Root is the super user
Line 7: Learning Linux is fun
EOT
cat -n hello.txt
```
(For major.txt just replace the file name.)

## b. Display file in reverse
```bash
tac hello.txt                 # reverse line order
rev hello.txt                 # reverse characters in each line
tac hello.txt | rev           # both
```
## c. First 2 lines
```bash
head -n 2 hello.txt
```
## d. Last 3 lines
```bash
tail -n 3 hello.txt
```
## e. Lines, words, characters
```bash
wc hello.txt          # lines words bytes
wc -l hello.txt       # lines
wc -w hello.txt       # words
wc -m hello.txt       # characters
```
