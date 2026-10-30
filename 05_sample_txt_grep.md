# Q: sample.txt records + grep

## Create the file
```bash
cat > sample.txt <<'EOT'
Roll No. Stud_name Class Subject
101 Amit Sharma FY Linux
102 Neha Patil FY DBMS
103 Rahul Verma FY Python
104 Priya Singh SY Networking
105 Rohan More SY Cyber Security
EOT
cat sample.txt
```
(or use `vi sample.txt` -> i -> type -> Esc -> :wq)

## Tasks
```bash
grep "Rahul Verma" sample.txt          # a. search pattern
grep -v "SY" sample.txt                # b. students NOT in SY (header also shows)
grep -n "Python" sample.txt            # c. Python with line number
grep "FY" sample.txt                   # d. students in FY
```
Extra: `grep -i "linux" sample.txt` (ignore case), `grep -c FY sample.txt` (count), `grep -E "FY|SY" sample.txt`.

## Viva
- `-v` invert match, `-n` line numbers, `-i` ignore case, `-c` count, `-r` recursive.
