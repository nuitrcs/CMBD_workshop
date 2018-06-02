# Bash Scripting
<hr>

We were issuing the commands on the command line and
finding them again using the arrow key or `history`
command.

When we need to accomplish many tasks, write long command,
and repeat these tasks form time to time, it is better to save your
commands to a file. Instead of executing the commands
one by one on the command line, we can execute the
file. This file is called a shell script.

So let's start with putting some very common programming constructs
in scripts.

## Variables

In programming, variables are information holders, or labels of information.
You can access the same information through out your programme by calling
its lable. You can also assign new information to the lables.

Let's start editing our first bash script.

```bash
vim mynumber.sh
```

We will type the follwing code block in the script file to look at
variable 'myfavnumber'.

```bash
#!/bin/bash

myfavnumber=34
echo 'My favorite number is' $myfavnumber

myfavnumber=65
echo 'I changed my mind, it is' $myfavnumber
```

`$` symbol tells the shell interpreter to treat *myfavnumber* as
a **variable** and look what is inside this lable. So `$favnumber`
returns the value of the variable which becomes 34 and then 65. In some
bash code, you may see `${favnumber}` which is equivalent to `$favnumber`

## Conditionals

Another important algorithmic construct is conditinonals. The basic
conditional statement is `if/then`. Apart from small syntax differences, the
usage of `if/then` statement in bash scripts is same as other languages.
Conditionals help you to execute commands only when certain conditions
are met.

```bash
#!/bin/bash

myfavnumber=34

if [ $myfavnumber -eq 34 ]
    then
        echo "My favorite number is $myfavnumber"
fi
```

`if/then` statement can be extended to `if/then/else` or `if/then/elif/else`
to test more conditions.

Let's move to *data* folder and create decision tree about your
vegetables when there are rabbits around.

```bash
vim nobunnys.sh
```


```bash
#!/bin/bash

cd data

nrabbits=`cat animals.txt | grep rabbit | wc -l`
# nrabbits=$(cat animals.txt | grep rabbit | wc -l)

if [ $nrabbits -le 2 ]; then
    echo 'Nothing to worry about my vegetable garden'
elif [ $nrabbits -gt 2 ] && [ $nrabbits -le 10 ]  ; then
    echo 'Yellow alert, check your garden'
else
    echo 'Call animal control'
fi

echo "$nrabbits"
```


## LOOPS

Loops will make your life very easy for repetitive tasks and automation. 
Let's move to 'creatures' folder. We will work with the two files but let's 
first create backup copies.

```bash
cd ../creautures
pwd
ls -al
cp *.dat original-*.dat
```

When `cp` receives more than two inputs the last should be a directory for
`cp` to be able to copy all files prior to this directory. So the previous
command will not work. We can use a loop to accomplish this task

```bash
for filename in basilisk.dat unicorn.dat #hit enter#
> do
>     cp $filename original-$filename
> done

#OR

for filename in basilisk.dat unicorn.dat; do cp $filename original-$filename; done

#OR

for x in basilisk.dat unicorn.dat; do cp $x original-$x; done

for color in basilisk.dat unicorn.dat; do cp $color original-$color; done
```

`$` symbol tells the shell interpreter to treat *filename* as a **variable** and 
`$filename` returns the value of the variable which becomes *basilisk.dat* and
*unicorn.dat* within the loop. In some code, you may see `${filename}` which
is equivalent to `$filename`

```bash
echo *.dat

for filename in *.dat #hit enter#
> do
>     echo $filename
>     head -n 100 $filename | tail -n 5  #this selects the lines 96-100
> done
 ```

We can put an empty line before each filename when printing for a better
look

```bash
echo *.dat

for filename in *.dat #hit enter#
> do
> echo ""
> echo $filename
> head -n 100 $filename | tail -n 5  #this selects the lines 96-100
> done
 ```

Say you have white spaces in your file names:

```bash
cp basilisk.dat 'green snake.dat'
cp unicorn.dat 'white horse.dat'
for filename in green snake.dat white horse.dat #hit enter#
> do
>     echo $filename
>     head -n 100 $filename | tail -n 20  #this selects the lines 81-100 
> done

#This should be

for filename in 'green snake.dat' 'white horse.dat' #hit enter#
> do
>     echo $filename
>     head -n 100 $filename | tail -n 20  #this selects the lines 81-100 
> done
 ```

Let's go back to our molecules folder do more looping

```bash
cd ../molecules
```

Say we want to write all molecules in one file:

```bash
for molecule in *.pdb; do echo $molecule; cat $molecule > all_molecules.dat; done
cat all_molecules.dat
```

We could not write all molecules in a single file because each iteration
of the loop we overwrite the previous file. Instead we should have used 
append `>>`

```bash
rm all_molecules.dat
for molecule in *.pdb; do echo $molecule; cat $molecule >> all_molecules.dat; done
```

What if we only want to write molecules if their names start with p

```bash
for molecule in p*; do echo $molecule; cat $molecule >> p_molecules.dat; done
```

What if we only want to write molecules if their names include c

```bash
for molecule in *c*; do echo $molecule; cat $molecule >> c_molecules.dat; done
```

We can construct nested loops for instance creating a grid of folders
for organizing our data

```bash
for temperature in 10 20 ; do 
> for molecule in propane pentane; do mkdir $molecule-$temperature; done
> done

#OR 

for temperature in 10 20 ; do 
> for molecule in propane pentane; do mkdir "$molecule-$temperature"; done
> done

#BUT NOT SAME

for temperature in 10 20 ; do 
> for molecule in propane pentane; do mkdir '$molecule-$temperature'; done
> done
```

There are other loop constructions such as `while` and `until`.

```bash
counter=0
while [ $counter -lt 10 ]; do echo $counter; let counter=counter+1; done
 ```

`while` iterates as long as the condition is true where as `until` stops
the loop when the condition is true
 
```bash
counter=0
until [ $counter -ge 10 ]; do echo $counter; let counter=counter+1; done
echo $counter
```


# SHELL SCRIPTS

Let's go to molecules folder and start writing a script
 
```bash
cd ../molecules
vim middle.sh
```

When we start vim, to write characters we first hit
**i** (entering inset mode) and then we write the following

```bash
#!/usr/bin/env bash     # you may not need this line
head -n 15 octane.pdb | tail -n 5
```

Then we hit **Esc**, then we hit **:** (entering  command mode) 
and type **wq** (save and quit) and hit **Enter**.

```bash
bash middle.sh
```

Your input in the `head` command was octane.pdb.
Instead of hardcoding the file name in the script
we can make it a variable. Let's edit our script
with vim again

```bash
vim middle.sh
```

hit **i** (inset mode) and then we write the 
following

```bash
# head -n 15 octane.pdb | tail -n 5
head -n 15 "$1" | tail -n 5
```

A comment starts with a `#` character and runs to 
the end of the line. The computer ignores comments. 

In case the filename happens to contain any spaces, 
we surround $1 with double-quotes.

Then we hit **Esc**, then we hit **:** and type
**wq** and hit **Enter**. Now we can identify 
our file as an input to the script on the command line

```bash
bash middle.sh octane.pdb
bash middle.sh pentane.pdb
```

Let's make the number of lines printed by `head` and
`tail` also variables

```bash
vim middle.sh
```

hit **i** (inset mode) and then we write the 
following

```bash
# head -n 15 octane.pdb | tail -n 5
head -n "$2" "$1" | tail -n "$3"
```

Then we hit **Esc**, then we hit **:** and type
**wq** and hit **Enter**. Now let's change the 
number of lines on the command line.

```bash
bash middle.sh pentane.pdb 15 5
bash middle.sh pentane.pdb 20 5
```

It is a good coding practice to add comments 
in your script to explain what is being done
to another user of your script.

```bash
vim middle.sh
```

We will repeat the routine to insert save and
quit in vim.

```bash
# Select lines from the middle of a file.
# Usage: bash middle.sh filename end_line num_lines
# head -n 15 octane.pdb | tail -n 5
head -n "$2" "$1" | tail -n "$3"
```

Comments are invaluable for helping people (including 
your future self) understand and use scripts. However 
each time you modify the script, you should check that 
the comment is still accurate.

Let's write another script to find the number of lines
for each file and sort them according to these
numbers. 

```bash
vim sorted.sh
```

Repeat the routine to insert save and
quit in vim.

```bash
#!/usr/bin/env bash

wc -l "$1" "$2" | sort -n
```

Let's execute the script

```bash
bash sorted.sh *.pdb
```

As you see we did not get all the files. Only two files
reported because we entered two variables in the script.
If we want to enter any number of input arguments,
instead of using `"$1"`, `"$2"` etc., we could use 
`"$@"`

```bash
vim sorted.sh
```

Repeat the routine to insert save and
quit in vim.

```bash
wc -l "$@" | sort -n
```

Let's execute the script

```bash
bash sorted.sh *.pdb ../creatures/*.dat
```

If you forget to provide input as show below, the script
will start but not do anything. To exit from this state
hit Ctrl+C

```bash
bash sorted.sh
```

A short cut to save some useful commands is to redirect 
the current history to a file which becomes a script

```bash
history | tail -n 5 > redo-commands.sh
```

As you see it is natural to stack more than one command
in a script. So let's write a script that takes any
number of files (i.e. *.pdb* files) in molecules folder as
input and
<br>
1. Prints the file names that are provided 
2. Prints out 4<sup>th</sup> line from each 
file 
3. Combines all files in "all_molecules.txt"
4. Create copies with names "bckp-<file_name>"

except if the file name is cubane.pdb

```bash
vim myscript.sh
```

Repeat the routine to insert save and
quit in vim.

```bash
#!/usr/bin/env bash

for filename in "$@"
    do
        if [ "$filename" == "cubane.pdb" ] ; then
            continue
        fi

        echo $filename
        head -n 4 $filename | tail -n 1
        cat $filename >> all_molecules.txt
        cp $filename bckp-$filename
    done
```

Issue the following command to see the result:
```bash
bash myscript.sh *.pdb
```

We can convert this script to an executable and run without identifying
the interpreter (i.e. bash)

```bash
chmod u+x myscript.sh
./myscript.sh *.pdb
```


Let's do some scripting with random numbers. 
Write a bash script to generate 1000 random numbers 
between 1 and 1000 and write them to a file. Find 
out how many unique numbers are obtained. <br>
(Hint: Try issuing `echo $RANDOM`, what do you get?)

```bash
#!/usr/bin/env bash

rm randomnumbers.txt
touch randomnumbers.txt

for i in `seq 1000`
    do
        echo $(((RANDOM%1000)+1)) >> randomnumbers.txt
    done

sort -n randomnumbers.txt | uniq | wc -l
```

Write a script that creates a folder at every 2 seconds with names
folder_01, ... folder_10 and lets you know when each folder is created
and the operation is ended. Finally, the script should show the created
folders and then delete them.

```bash
#!/usr/bin/env bash
counter=1

while [ $counter -le 10 ]; do
    sleep 2 #wait for 2 seconds
    mkdir folder_$(printf "%02d" $counter)

    if [ $counter -eq 10 ]; then
        echo "Folder ${counter} has been created"
        echo 'All folders are created'
    else
        echo "Folder ${counter} has been created"
    fi

    let counter=counter+1
done

ls -al | grep folder_
rm -Rf folder_*
```
