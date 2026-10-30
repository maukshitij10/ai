# Q: employee.txt - cut, sort

## a. Create file (use a delimiter such as comma ',')
```bash
cat > employee.txt <<'EOT'
1101,Amit Sharma,C.E.O,Linux,250000
1102,Neha Patil,Executive,DBMS,200000
1103,Rahul Verma,Manager,Python,100000
1104,Priya Singh,President,Networking,300000
1105,Rohan More,Technician,Cyber Security,75000
EOT
```
(Header line is skipped here to keep sorting clean; add `Empid,Ename,Designation,DoJ,Salary` if the examiner wants it.)

## b. Display only Ename and Salary using delimiter
```bash
cut -d',' -f2,5 employee.txt
```
## c. Empid, Ename, DoJ -> emp.txt
```bash
cut -d',' -f1,2,4 employee.txt > emp.txt
cat emp.txt
```
## d. Ascending order of salary, appended to emp.txt
```bash
sort -t',' -k5 -n employee.txt           # display
sort -t',' -k5 -n employee.txt >> emp.txt
cat emp.txt
```
## e. Descending order of DoJ
```bash
sort -t',' -k4 -r employee.txt
```
## Viva
- `-d` delimiter, `-f` field; `-t` separator, `-k` key column, `-n` numeric, `-r` reverse, `>` overwrite, `>>` append.
