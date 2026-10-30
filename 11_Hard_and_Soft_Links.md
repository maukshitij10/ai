# Q: Hard links and soft (symbolic) links

```bash
echo "Hello Linux" > original.txt
ln original.txt hardlink.txt          # hard link
ln -s original.txt softlink.txt       # soft link
ls -li                                # inode numbers & link count
```
Observation: `original.txt` and `hardlink.txt` have the **same inode** and link count 2; `softlink.txt` has a different inode and shows `softlink.txt -> original.txt`.

## Demonstrate behaviour
```bash
cat hardlink.txt ; cat softlink.txt
echo "More data" >> hardlink.txt ; cat original.txt     # change reflects in both
rm original.txt
cat hardlink.txt          # still works (data retained)
cat softlink.txt          # error: No such file (broken/dangling link)
ls -l
```
Restore: `echo test > original.txt` -> soft link works again.

## Differences (viva)
| Hard link | Soft link |
|---|---|
| Same inode as original | Own inode |
| Works after original deleted | Breaks if original deleted |
| Cannot link directories | Can link directories |
| Cannot cross filesystems | Can cross filesystems |
| `ln src dst` | `ln -s src dst` |
