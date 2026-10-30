# Q: Redirection, pipe, cat/head/tail/sort/wc, grep+regex, cut/awk

## a. Redirection and pipe
```bash
ls /etc > out.txt              # overwrite stdout
echo "second line" >> out.txt  # append
ls /nonexistent 2> err.txt     # redirect stderr
ls /etc /nonexistent > out.txt 2> err.txt
ls /etc /nonexistent &> all.txt # both
cat < out.txt                   # input redirection
ls /etc | wc -l                 # pipe
ps -ef | grep sshd | wc -l
```
## b. Text file and tools
```bash
cat > data.txt <<'EOT'
banana
apple
cherry
apple
date
EOT
cat data.txt
head -n 2 data.txt
tail -n 2 data.txt
sort data.txt
sort -r data.txt
sort data.txt | uniq
wc data.txt ; wc -l data.txt
```
## c. grep and regex
```bash
grep "apple" data.txt
grep -i "APPLE" data.txt
grep "^a" data.txt           # starts with a
grep "e$" data.txt           # ends with e
grep -E "apple|date" data.txt
grep "a.p" data.txt          # . any char
grep -c apple data.txt ; grep -n cherry data.txt
```
## d. cut / awk
```bash
cat > emp.csv <<'EOT'
1,Amit,Manager,50000
2,Neha,Clerk,30000
3,Rahul,Analyst,40000
EOT
cut -d',' -f2,4 emp.csv
awk -F',' '{print $2, $4}' emp.csv
awk -F',' '$4 > 35000 {print $2}' emp.csv
awk -F',' '{sum+=$4} END {print "Total:", sum}' emp.csv
```
