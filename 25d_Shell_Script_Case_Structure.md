# Q: Shell script to demonstrate case structure

`vi casedemo.sh`
```bash
#!/bin/bash
echo "===== MENU ====="
echo "1. Show date"
echo "2. Show current directory"
echo "3. Show logged-in users"
echo "4. Show disk usage"
echo "5. Exit"
read -p "Enter your choice [1-5]: " ch
case $ch in
    1) date ;;
    2) pwd ;;
    3) who ;;
    4) df -h ;;
    5) echo "Bye"; exit 0 ;;
    *) echo "Invalid choice" ;;
esac
```
```bash
chmod +x casedemo.sh ; ./casedemo.sh
```
Syntax: `case $var in pattern) commands ;; esac`. `*)` is default; `;;` ends each block.

Second example (vowel check):
```bash
read -p "Enter a character: " c
case $c in
  [aeiouAEIOU]) echo "Vowel" ;;
  [a-zA-Z]) echo "Consonant" ;;
  [0-9]) echo "Digit" ;;
  *) echo "Special character" ;;
esac
```
