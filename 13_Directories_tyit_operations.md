# Q: Directory and file operations

```bash
mkdir tyit1 tyit2 tyit3                 # a
mkdir tyit2/linux                       # b
mv tyit3 tyit4                          # c  rename
touch pqr ; mv pqr tyit1/               # d  create & move
cp tyit1/pqr xyz                        # e  copy contents (add text first: echo hi > tyit1/pqr)
rmdir tyit4                             # f  (or rm -r tyit4)
ls -R
tree          # dnf install tree
```
Notes: `cp` copies file contents to new file `xyz`; `rmdir` removes only empty dirs, `rm -r` removes non-empty.
