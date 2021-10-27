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

## compare documents/directories: diff
```
diff file1 file2
diff dir1 dir2
```

## combine pdf

```
cpdf () {    gs -q -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -sOutputFile="$1" "${@:2}"; }
cpdf merged.pdf 1.pdf 2.pdf

## combing all jpg to pdf
convert *.jpg pictures.pdf
convert 1.jpg 2.jpg pictures.pdf
```

## directory structure

```
tree .
```

## unzip unrar

```
unrar x ...
```

## zip with password

```
zip -er zipname.zip /foldername
```

## split video into different parts

(in a fast way)
```
ffmpeg -i xxx.mov -ss 00:00:00 -t 00:25:00 -c copy part1.mov
ffmpeg -i xxx.mov -ss 00:25:00 -t 00:25:00 -c copy part2.mov
ffmpeg -i xxx.mov -ss 00:50:00 -t 00:25:00 -c copy part3.mov
ffmpeg -i xxx.mov -ss 01:15:00 -t 00:25:00 -c copy part4.mov
ffmpeg -i xxx.mov -ss 01:40:00 -t 00:25:00 -c copy part5.mov
```

## launch docker

The docker setup does not work as in a normal Linux machine, on a Mac it is much more complicated. But it can be done!

https://apple.stackexchange.com/questions/373888/how-do-i-start-the-docker-daemon-on-macos

```
brew cask install docker virtualbox
brew install docker-machine
docker-machine create --driver virtualbox default
docker-machine restart
eval "$(docker-machine env default)" # This might throw an TSI connection error. In that case run docker-machine regenerate-certs default
(docker-machine restart) # maybe needed
docker run hello-world
```

These steps are based on information given in these two questions:

Cannot connect to the Docker daemon on macOS
Mac OS X sudo docker Cannot connect to the Docker daemon. Is the docker daemon running on this host?.

## slurm

```
squeue -u <username>
scancel -u <username>
```

## RNAseq related

```
zcat ERR458493.fastq.gz | head

for ACC_NR in ERR458493 ERR458494 ERR458495 ERR458496 ERR458497 ERR458498
do
  wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR458/${ACC_NR}/${ACC_NR}.fastq.gz
done
```

## git

```
$ git init
($ git status)
$ git add mars.txt
($ git status)
$ git commit -m "some comments"

$ git push
Uploads all local branch commits to GitHub
$ git pull
Updates your current local working branch with all new commits from the corresponding remote branch on GitHub. git pull is a combination of git fetch and git merge
```
## convert pdf to eps/ps

```
pdf2ps cputime.pdf cputime.ps # pdf to ps
ps2eps -l -r 500 cputime.ps # ps to eps
```

## run multiple .sh

https://stackoverflow.com/questions/41079143/run-all-shell-scripts-in-folder

Use this:

```
for f in *.sh; do
  bash "$f" 
done
```
If you want to stop the whole execution when a script fails:
```
for f in *.sh; do
  bash "$f" || break  # execute successfully or break
  # Or more explicitly: if this execution fails, then stop the `for`:
  # if ! bash "$f"; then break; fi
done
```
If you want to run, e.g., x1.sh, x2.sh, ..., x10.sh:
```
for i in `seq 1 10`; do
  bash "x$i.sh" 
done
```
To preserve exit code of failed script (responding to @VespaQQ):
```
#!/bin/bash
set -e
for f in *.sh; do
  bash "$f"
done
```
