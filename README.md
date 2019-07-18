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

Ubuntu:
```
find . -type f -executable -delete
```

MacOC:
```
find . -perm +111 -type f -delete
```

Ref: https://stackoverflow.com/questions/856463/how-to-remove-delete-executable-files-aka-files-without-extension-only
Ref: https://apple.stackexchange.com/questions/116367/find-all-executable-files-within-a-folder-in-terminal

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
### for loop
```
for p1 in 0.05 0.075 0.1 0.25 0.5
do
    for i in {0..150..5}
    do
        python myscript.py -p p1 -v i
    done
done
```
ref: https://stackoverflow.com/questions/41900600/slurm-sbatch-job-array-for-the-same-script-but-with-different-input-arguments-ru

### passing arguments
In terminal:
```
$ sbatch myscript.sh myinput myoutput
```
In .sh:
```
#!/bin/bash

#SBATCH ...
#SBATCH ...
...
# argument 1 is myinput
# argument 2 is myoutput
mybinary.x < ${1} > ${2}
```

### passing arguments (2)

In terminal:
```
$ sbatch myscript.sh myscript
```
In .sh
```
#!/bin/bash

#SBATCH ...
#SBATCH ...
...
# argument 1 is myscript
Rscript ${1}
```
