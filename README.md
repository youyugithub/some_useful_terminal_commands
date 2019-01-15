# some useful terminal commands
(for personal reference, glad to share)

### delete ALL files ending with .out
(all .out files in the subfolders are also deleted.)
```
find . -type f -iname \*.out -delete
find . -name "*.out" -type f -delete
```

### delete ALL executables (without extensions)
(all executable files in the subfolders are also deleted.)
```
find . -type f -executable -delete
```
Ref: https://stackoverflow.com/questions/856463/how-to-remove-delete-executable-files-aka-files-without-extension-only

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

### copy all contents in folder1 to folder2
```
cp -a folder1/. folder2
```
ref: https://askubuntu.com/questions/86822/how-can-i-copy-the-contents-of-a-folder-to-another-folder-in-a-different-directo

### specify python 3/2 when installing libraries
```
python3 -m pip install seaborn
python3 -m pip install seaborn
```

