# Q: abc & pqr - chmod in absolute (numeric) and relative (symbolic) mode

```bash
touch abc pqr                       # a
ls -l abc pqr                       # default -rw-r--r-- (644)
chmod 100 abc                       # b  absolute: execute for user only (--x------)
ls -l abc
chmod 600 pqr                       # c  absolute: read+write for user (rw-------)
ls -l pqr
chmod u+rx,o+rx abc                 # d  relative: read & execute to user and others
chmod uo+rx abc                     #    (short form)
ls -l abc
chmod uo+wx pqr                     # e  write & execute to user and others of pqr
ls -l pqr
chmod uo-r abc                      # f  remove read from user and others of abc
ls -l abc
```
Reference: r=4 w=2 x=1. u=user, g=group, o=others, a=all. `+` add, `-` remove, `=` set.
