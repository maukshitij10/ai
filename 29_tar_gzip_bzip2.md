# Q: Directory with 5 files, archive with tar, compress with gzip & bzip2, extract and verify

```bash
mkdir mydir
touch mydir/file{1..5}.txt
for i in 1 2 3 4 5; do echo "content $i" > mydir/file$i.txt; done
ls mydir                                   # a

tar -cvf mydir.tar mydir                   # b archive
tar -tvf mydir.tar                         # list contents

gzip mydir.tar                             # c -> mydir.tar.gz (replaces .tar)
gunzip mydir.tar.gz                        # to undo, recreate tar
bzip2 -k mydir.tar                         # -k keeps original -> mydir.tar.bz2
ls -lh mydir.tar*

mkdir newdir                               # d extract
tar -xvzf mydir.tar.gz -C newdir           # (if gzip file exists)
tar -xvjf mydir.tar.bz2 -C newdir          # bzip2
ls -R newdir
diff -r mydir newdir/mydir && echo "Files identical"
```
Tip: use `gzip -k mydir.tar` to keep the .tar so both gzip and bzip2 files exist.
One-step: `tar -czvf a.tar.gz mydir` (gzip), `tar -cjvf a.tar.bz2 mydir` (bzip2).
Flags: c create, x extract, t list, v verbose, f file, z gzip, j bzip2, C target dir.
