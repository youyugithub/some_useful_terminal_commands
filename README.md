# some useful terminal commands
(for personal reference, glad to share)

### delete files ending with .out
(all .out files in the subfolders are also deleted.)
```
find . -type f -iname \*.out -delete
```

### pass current directory as an argument to R
In R:
```
args=commandArgs(trailingOnly=TRUE)
cat("==========","\n")
cat(args,"\n")
cat("==========","\n")
```
In terminal:
```
cd /home/Documents
Rscript test.R $(pwd)
```
Then get:
```
==========
/home/Documents
==========
```
